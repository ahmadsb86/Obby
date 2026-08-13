# Order File Maintenance

Split array in chunks of $\log N$. Each chunk is a leaf of conceptual bintree. To update, we update chunk then travel up the tree till we see a node whose interval is within density threshold (DT). Then uniformly distribute elms in that node's interval

DT is between $1/4$ and $1$ for leaf nodes and between $1/2$ and $3/4$ for root and linerp'ed for intermediates. 

Done. Analysis. For an intermediate node, when we redistribute, our children fall WELL within thresh (since their DT bounds are looser than even us). Specifically their density must be additive $\frac{1}{4h}$ distance to threshold or $\frac{1}{4h} \cdot s$ updates away from thresh where $s$ is size of interval.  

Redistribution costs $s$. Attribute to $\frac{1}{4h} \cdot s$ updates till then seemingly brings amortization to $\frac{1}{4h} = O(\log N)$ but we are overcharging by $\log N$ factor since each update to a chunk is being charged by all its $\log N$ ancestors $\implies$ total amortized  is $O(\log ^{2} N)$  

gap size is $O(1)$ since redist sets gap size to $O(1)$ and subsequent inserts till next redist only reduce gap size.

# List Labelling

Maintain LL w/ update/delete s.t. nodes have labels that you must design to always be strictly monotone. Symmetrical to OFM since labels can be though of OFM array indices. However, we get better bounds since labels can take super-linear universe space but not array indices.  

Known Results (by label universe size $m$ vs $n$ items; cost = amortized relabels/insert):

- **Linear**, $(1+\epsilon)n \le m \le n\log n$: $\Theta(\log^2 n)$
- **In between**, $n\log n < m < n^{1+\Theta(1)}$: interpolates $\log^2 n \to \log n$ as slack grows.
- **Polynomial**, $m = n^{1+\Theta(1)}$: $\Theta(\log n)$. DT threshes become exponential instead of constants  
- **Exponential**, $m = 2^{\Omega(n)}$: $\Theta(1)$ (just gap-halve).

# List Order Maintainence

Maintain LL subject to update/delete and order queries (is x before y?). Use poly result above but get constant time using indirection! 

Use DS from poly bound above to stores $\Theta(\log N)$ sized chunks, each stored with exponential DS from above. Update expo DS first till full or less than $\frac{1}{4}$ capacity, then split or merge w/ neighbor and update poly DS. Every elm is indexed with an ordered pair (index in either DS). 

$\Theta(\log n)$ update time in poly DS is amortized over $\Theta(\log n)$ const time updates in expo DS.  Since expo DS spans $\Theta \log n$ elms, label space is only $2^{\Theta(\log n)} = \Theta (n)$

This isn't valid List label since from the poly DS perspective, we are updating $\log n$ labels simultaneously


# Cache Oblivious Priority Queue

Assume tall cache ($M=B^{1+\epsilon}$ ). Store layers of doubly exponential size. $\epsilon=1$ works with this progression of sizes:  $n, n^{2/3}, n^{4/9}, \dots , O(1)$. Each layer of size $x^{3/2}$ has up buffer of parent size, $x^{9/4}$, and $x^{1/2}$ down buffers of child size, $x$. 

Invariants. Items in a down buffer are always larger than items in the layer's previous down buffers but always smaller than the layer's up buffer.

To insert, push item into $O(1)$ layer up buffer and swap around with down buffers s.t. invariants satisfied but only up buffer inc in size. The layers under size $B^{4/3}$ can all be cached so all they are all free

If up buffer full, sort up buffer using $\frac{x}{B}\log_{\frac{M}{B}} \frac{x}{B}$ sorting algo and with a single linear pass of parent's down buffers, greedily insert items into the down buffers if an item is less than the down buffer stored max. Down buffer full/almost empty $\implies$ split or merge with neighbor. No room for another down buffer $\implies$ throw last buffer into up buffer

linear pass takes $O(x^{1/2})$ to check all maxes and writing to a buffer through linear pass takes $O\left( \frac{x}{B} \right)$ but it is argued that $\frac{x}{B}$ dominates for all non-free layers which is dominated by sorting bound. Amortization wasn't explained thoroughly.

