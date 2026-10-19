  

Picking a starting node to minimize cascade depth.

Here is the whole procedure in order. The short answer to your sizing question comes out of the bridge construction: you don’t size the first candidate set by selectivity at all. Because of the bridges, every candidate lands somewhere useful in each child, so a set about the size of a normal beam is enough.

### Build time

1. **Segment tree.** Sort points by attribute and build a binary segment tree. Each node v stores a proximity graph G_v over the points in its subtree.
2. **Bridges.** For every node v and every point p in v, store one pointer into each child c:
    - If p lies in c, the pointer is p itself.
    - Otherwise it points to p’s nearest neighbor among c’s points, found by an ANN search in G_c.In a binary tree, p lies in exactly one child, so only one real pointer per point per level needs storing. That gives O(n log n) pointers and O(n log n) ANN lookups at build time. Optionally, store the b nearest points instead of one, which helps later with collisions. DIGRA’s graph-building step already runs, for each point, a search over the graph of every child the point doesn’t belong to. The top result of that search is exactly this bridge, so if you build DIGRA-style, the bridges are nearly free.

### Query time

3. **Locate the structure.** Find the split node s, the lowest node whose range contains the whole query interval. Below it are the two boundary paths and the O(log n) canonical nodes hanging off them. Start at s rather than the root, which saves levels of cascading.
4. **One real search.** Run a normal beam search in G_s with beam width ef_s. This ignores the filter, since s contains in-range and out-of-range points alike. Keep the top L candidates as C_s.
5. **Cascade down each boundary path.** At a path node v, each child c gets seeds equal to the deduplicated bridge images of C_v. At each path node, one child is usually canonical (fully inside the range) and the other continues the path.
    - **Canonical child:** run a beam search in G_c initialized with those seeds and return its top-k for merging. This is the step that should take fewer hops than a cold start.
    - **Path child:** run a cheap refinement, a short beam search with small ef, to get C_c, then repeat this step one level down.
6. **Merge.** Combine the canonical nodes’ results into a global top-k. Keep a running k-th-best distance so later canonical searches can terminate early.

### Why L doesn’t depend on selectivity

The worry is the post-filtering one. If you searched the split node unfiltered and then kept only candidates lying in a small canonical node holding fraction σ of the points, you’d need L ≈ k/σ candidates to expect k survivors. For the small canonical nodes near the leaves, that blows up.

Bridges remove the problem, because a candidate doesn’t need to be in the child to be useful: it maps to its nearest point there. There’s also a clean guarantee for the best seed. Let x* be the query’s true nearest neighbor within child c, and let p be the parent’s nearest candidate. Then:

- Since c ⊂ v, the parent’s nearest neighbor is at least as close as the child’s, so d(q, p) ≤ d(q, x*).
- By definition the bridge is p’s nearest point in c, so d(p, bridge(p)) ≤ d(p, x*) ≤ d(p, q) + d(q, x*).
- By the triangle inequality, d(q, bridge(p)) ≤ d(q, p) + d(p, bridge(p)) ≤ 2d(q, p) + d(q, x*) ≤ 3d(q, x*).

So one level of cascading gives a 3-approximate seed for the child’s nearest neighbor, regardless of how small the child is.

Two caveats keep this from being the whole story:

- **High dimensions.** Distances concentrate in high dimensions, so a factor of 3 may be no better than a random point. The bound shows the method is well-defined, not that it’s fast. Speed is the empirical question.
- **Compounding.** If you chain bridges down several levels without refining, the bound grows roughly as 2^j at depth j. That is why step 5 refines at each path node, keeping each level’s candidates near the true answers before mapping them down again.

### So how big should L be?

Treat L as an ordinary tuning knob tied to the child searches’ beam width, not to selectivity. Somewhere between k and the child ef is the natural range, because the seed set is just the initial beam for the child’s search. Two things push it up:

- **Collisions.** Many far-away parent candidates can map to the same few points in a small child, so the number of distinct seeds after deduplication can fall well below L. Storing b > 1 bridges per point counters this.
- **Correlated attributes.** If vectors cluster by attribute (timestamps, say), a canonical node can sit far from the parent’s answers. Seeds then land near the node’s boundary with the query region, and the refinement does more of the work.

For the benchmark, sweep three knobs:

- L
- the path-node refinement ef
- b

Log the distinct-seed count and the seed hit rate at each canonical node: the fraction of that node’s true top-k already in the seed set. If the hit rate stays high as σ shrinks, the cascade is doing its job. If it collapses for small nodes, those nodes are where the extra distance computations will appear.

define beam real quick

A beam is the bounded list of best candidates found so far during a graph search, and the beam width (ef in HNSW terms) is its maximum size.

The search keeps two structures: the beam, holding the ef closest points seen so far, and a queue of points whose neighbors haven’t been checked yet. At each step it takes the closest unexpanded point and computes distances to that point’s graph neighbors. Any neighbor closer than the worst point in the beam goes in, and the worst point gets dropped. The search stops when no unexpanded point is closer than the beam’s worst member, and it returns the top k from the beam.

A wider beam explores more of the graph before stopping, which raises recall and costs more distance computations. With a beam of 1 you get plain greedy search, which gets stuck in local minima easily.

In the cascade, the seeds simply become the beam’s starting contents instead of a single default entry point. That’s why L and the child’s ef are naturally tied together.

so does the beam get full at the very top few layers and then just get modified in the lower layers?

Working out how search beams narrow across HNSW layers.

Working out how search beams narrow across HNSW layers.

Not quite. It depends on whether you mean HNSW’s layers or the levels of our segment tree, and in neither case does one beam persist all the way down.

**Inside HNSW.** The upper layers don’t use a beam at all, or rather they use a beam of width 1. The search does plain greedy descent there: in each layer it hops to whichever neighbor is closer until it can’t improve, then passes that single point down as the entry for the next layer. Only at the bottom layer does it open a real beam of width ef. So the beam starts with one point at layer 0 and fills up during that bottom-layer search.

**In the cascade.** Each segment tree node has its own separate graph, so each node’s search starts a fresh beam. What carries over between levels is not the beam but its contents, mapped through the bridges:

1. At the split node, a normal search fills a beam and leaves its top L candidates.
2. Those candidates are mapped into each child and deduplicated, and become the starting contents of the child’s new beam. Because of collisions there may be fewer distinct seeds than the beam holds, so it starts partly full.
3. The child’s search then runs as usual: it fills any empty slots, replaces seeds with closer points, and stops when nothing improves.
4. The child’s final beam is mapped down again for the next level.

So the picture is a fresh beam per node, each initialized much closer to the answer than a cold start would be. The hoped-for saving is that each of these searches converges after only a few expansions, because its starting contents are already mostly correct.

Expand on query time point 4 onwards. explain in more depth. Im confused

Thought for 32s

Let’s use a small concrete example: 16 points sorted by attribute, so their ranks run from 0 to 15, and a query range of [3, 12]. Here is the part of the segment tree the query touches:

Three kinds of node matter:

- **Split node.** [0, 15] is the lowest node containing the whole range, because 3 falls in its left half and 12 in its right half.
- **Boundary path nodes (purple).** These straddle an endpoint of the range, so they hold a mix of in-range and out-of-range points. They exist only to pass seeds downward; nothing is returned from them.
- **Canonical nodes (teal).** These lie entirely inside the range, and their union is exactly [3, 12]. The query’s answer is the best k points across these four nodes.

Gray nodes lie entirely outside the range and are never touched.

Call the points p0 to p15 by rank. Say we want k = 2 results and carry L = 4 candidates between levels.

### Step 4: one real search at the split node

Run an ordinary beam search in G_[0,15], the graph over all 16 points, ignoring the filter. Suppose the 4 closest points to q are C = {p1, p6, p9, p13}.

Two of these, p1 and p13, are outside the range. That’s fine, because nothing from this search is returned. Its only job is to produce points near q that we can map downward.

### Step 5: walk down the two boundary paths

Each path node does the same thing: take its candidate list, push it through the bridges into its children, and handle each child by type.

**Root to its children.** For [0, 7], points already inside map to themselves (p1 → p1, p6 → p6). Points outside map to their precomputed nearest point inside: say p13 → p5 and p9 → p6. p6 now appears twice, so after deduplication the seeds are {p1, p5, p6}. The same mapping into [8, 15] gives seeds such as {p9, p13, p10}.

**At [0, 7], a path node.** Its points still include out-of-range ones (p0 to p2), so it is not an answer source. We run a short refinement, a beam search in G_[0,7] with a small beam starting from the seeds, to tidy the candidates. Say we get {p1, p6, p5, p2}. Then we map these into both children:

- **[4, 7] is canonical.** Mapping gives seeds such as {p6, p5, p4}. We run a full beam search in G_[4,7] starting from those seeds. Every point in this node is in range, so no filtering happens inside this search; it is a plain ANN search over a smaller graph. Say it returns {p6, p5}. These are this node’s contribution to the answer.
- **[0, 3] is the next path node.** Mapping gives seeds such as {p1, p2, p3}. We refine again and keep descending.

**At [0, 3].** Its left child [0, 1] is entirely out of range, so we skip it with no mapping and no search. Its right child [2, 3] continues the path. We map and refine.

**At [2, 3].** Leaf 2 is out of range and skipped. Leaf 3 is canonical; a single point needs no search, so it just becomes a candidate result.

The right side mirrors this. [8, 15] maps into canonical [8, 11], which gets a seeded search, and into path node [12, 15]. That leads to [12, 13], whose leaf 12 is canonical and whose leaf 13 is skipped.

The rhythm at every path node is the same: map the candidates down, give the canonical child a full seeded search, give the path child a cheap refinement, and ignore any out-of-range child.

### Step 6: merge

We now have results from the four canonical nodes: about 2 points each from [4, 7] and [8, 11], plus single points 3 and 12. Take the 2 closest overall as the answer.

The early-termination trick works like this. Keep τ, the distance of the current k-th best result across all canonical nodes searched so far. In any later canonical search, a candidate farther than τ can never enter the final top-k, so that search can stop once its closest unexpanded point is beyond τ. It helps to search canonical nodes in order of their best seed’s distance, since that shrinks τ early.

### Where the savings and costs are

In the baseline, each canonical node’s search starts cold from its default entry point and has to travel across its graph to reach q’s neighborhood. In the cascade, it starts with seeds already near q, often including its true answers, so it should converge after a few expansions.

The cost is the work the baseline never does: the search at the split node, plus a refinement at every path node. There are about as many path nodes as canonical nodes, so the method wins only if what each canonical search saves exceeds what the refinements cost. You can tune this:

- Make path refinements very cheap, with a beam barely larger than L.
- Skip refinement at some levels and chain bridges directly. This costs only pointer lookups, but as covered earlier, seed quality degrades the more levels you skip.

Both knobs are worth including in your benchmark next to L and b.

  

Incognito chats stay out of your history, memory, and search, and aren’t used to train Claude.

Claude finished the response