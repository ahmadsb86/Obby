# Defining the Problem

Consider an $n \times n$ grid system such that every row $i$ contains one horizontal ray of length $a_{i}$ ($0 < a_{i} \leq n)$ starting from the right-most column. Every column $j$ contains one query point at row $q_{j}$  ($0 \leq q_{j} < n)$. The rays are really just abstractions for the horizontal streaks of 1s and the query points are abstractions for the element below the lowest 0 in every column.

The goal is to create an algorithm that finds the horizontal ray directly below every query point (essentially vertical ray-casting). More specifically, for every $q_{j}$ our algorithm must find the highest row $r_{j}$ such that $r_{j} \geq q_{j}$ ($r_{j}$ is below $q_{j}$) and $a_{r_{j}} \geq j$ (the horizontal ray at $r_{j}$ reaches column $j$). 

The row $r_{j}$, column $j$, and the right-most column will form a "staple" shape of 1s. This assumes the right-most column only consists of 1s but that is okay because we can always discard all rows above the lowest 0 in the right-most column before running our algorithm.

# $O(n\log n)$ approach - Balance Binary Search Tree:

The easiest logarithmic time approach by far, in my opinion, is to simply use a balanced binary search tree that supports $O(\log n)$ deletion and $O(\log n)$ predecessor query. 

Algorithm: 
1. Store each row $i$ in a group based on $a_{i}$, such that groups are adjacent in memory and within each group rows are sorted. 
2. Initially keep all row indexes in a balanced binary search tree $S$. 
3. Sweep all columns from right to left. For a certain column $j$,
	1. Run predecessor of $q_{j}$ on $S$ (i.e. find the highest row $r_{j}$ in $S$ such that $r_{j}$ is still below $q_{j}$).  
	2. Then check if there are any rows in the group corresponding to $a_{i} = j$. In other words, use the grouping mechanism to find all rays whose left endpoint is at $j$. Delete these from $S$ (because we know these rays are too short to be the answer in later iterations).

Complexity Analysis: For every $j$ in our sweep, we spend $O(\log n)$ time to run the predecessor query. Thus, the total time complexity for all predecessors queries is  $O(n \log n)$. Reading out the elements to delete from the $a$-groups takes $O(x)$ time, where $x$ is the number of rows to delete from $S$. The deletion of $x$ elements from $S$ takes $O(x \log n)$. However, every element is only read out from the $a$-groups once and only deleted once, so the total time complexity of all deletions is also $O(n \log n)$. Hence, our algorithm takes $O(n \log n + n \log n) = O(n\log n)$.

The crux of this algorithm, and most others I will talk about, lies in the fact that during a right-to-left sweep, rows can only become inactive (impossible to be the $r_{j}$ we are looking for when processing later columns). Once they become inactive, they can't become active again. 

The same principle follows for a left-to-right sweep. In this, rows only ever become active throughout the swewping.


# $O(n\log n)$ approach - Fractional Cascading

I haven't worked this out all the way since it seems like a far more complicated way to reach the same bound as BBST (and thus, probably not worth the effort), but fractional cascading seems like it could also work in $O(n \log n)$.

A more detailed explanation of how it works can be found in the notes for lecture 3 and lecture 4 of MIT 6.851 *Advanced Data Structures*: https://courses.csail.mit.edu/6.851/spring12/lectures/


# $O(n \log^2 n)$ approach - Order File Maintainance

Similar to the BBST approach but swap out BBST with an OFM structure. These are essentially sparse arrays which store elements in order with guaranteed $O(1)$-sized gaps between elements but $O(\log ^{2} n)$ amortized update time complexity.  OFM is surprisingly pretty easy to implement, and most of the juice comes from the interesting amortization argument.

A detailed explanation of how it works can be found in the notes for lecture 8 of MIT 6.851: https://courses.csail.mit.edu/6.851/spring12/lectures/

Attached here are my personal notes from the class relevant to how OFM works (although it is probably infuriatingly difficult to read).

> Split array in chunks of $\log N$. Each chunk is a leaf of conceptual bintree. To update, we update chunk then travel up the tree till we see a node whose interval is within density threshold (DT). Then uniformly distribute elms in that node's interval
> 
> DT is between $1/4$ and $1$ for leaf nodes and between $1/2$ and $3/4$ for root and linerp'ed for intermediates. 
> 
> Done. Analysis. For an intermediate node, when we redistribute, our children fall WELL within thresh (since their DT bounds are looser than even us). Specifically their density must be additive $\frac{1}{4h}$ distance to threshold or $\frac{1}{4h} \cdot s$ updates away from thresh where $s$ is size of interval.  
> 
> Redistribution costs $s$. Attribute to $\frac{1}{4h} \cdot s$ updates till then seemingly brings amortization to $\frac{1}{4h} = O(\log N)$ but we are overcharging by $\log N$ factor since each update to a chunk is being charged by all its $\log N$ ancestors $\implies$ total amortized  is $O(\log ^{2} N)$  
> 
> gap size is $O(1)$ since redist sets gap size to $O(1)$ and subsequent inserts till next redist only reduce gap size.

# $O(n)$ approach - Rank/Select Inspired Indirection 

To find this approach, I took inspiration from a succinct rank/select algorithm discussed in lecture 17 of MIT 6.851. That problem is different, and our solution doesn't directly use any part of the algorithm for it, but the general idea is very similar.

Recall that if we do our sweep from left-to-right, rays only ever become active. Another way to think about this is that whenever we step to the next column over, a new ray can slice the gap between two previously active rays. Importantly, however, a gap will never have to merge with another gap throughout the sweeping process.

This means we can relatively easily label each row with the gap that exists above it.   During our sweep, when a new ray slices a gap, the gap is split into two parts. We can relabel all the rows in the smaller half. 

If we create a map that stores the row under every gap, then queries are easy to answer. When we are column $j$, we can answer query $q_{j}$ by checking the gap that $q_{j}$ falls within. Then we can use the map to find the ray under that gap, and thus our answer for $q_{j}$.

Every ray can only slice a gap once, and in the worst case every ray slices a gap in half. This means in total, the worst case is the first ray slices a gap of size $n$, the second ray slices a gap of size $\frac{n}{2}$, the third slices a gap of size $\frac{n}{4}$, etc. Thus, the total time complexity for relabelling is $O(n \log n)$. 

To remove the log factor, we can use a similar indirection trick to the aforementioned rank/select algorithm. We split the rows into blocks of size $b=\frac{1}{2} \log n$. Then, we change the algorithm explained to span blocks instead of individual rows. A block is active if it contains at least one active row, and whole blocks get relabelled instead of rows. Now the relabelling time complexity (excluding work done within a block) is $$O\left( \frac{n}{b} \log n \right) = O\left(\frac{n}{0.5\log n} \log n\right) = O(n)$$
All that remains is to figure out how to handle inserting rows and processing queries within a block in $O(1)$.

Within each block we can keep a bit-vector of size $b=\frac{1}{2}\log n$ where every bit $i$ represents whether the row $i$ within the bit-vector is active. Making a row active within a block is clearly $O(1)$ since we just need to turn on that specific bit. But how can we do predecssor in $O(1)$ to answer queries in $O(1)$? 

Notice that since $b=\frac{1}{2}\log n$, there are at most $\sqrt{ n }$ unique bit-vectors. We can just precompute the lowest set bit queries for every one of these in $O(\sqrt{ n })$ time which is negligible. Then, finding the predecessor 1 in a bit-vector of size $b$ comes down to masking all the bits that succeed our query and comparing to the 

Answering a query now takes three steps. 
1. Look inside query row's own block. Take its mask, clear the bits for rows above row 3, and ask whether any bit remains.
2. If none remains, as here, ask the block-level gap records for the next active block. Block 1 is in the gap covering blocks 1–2, so the next active block is block 3.
3. Take the lowest set bit of block 3’s mask, which gives row 13.

Insert image

