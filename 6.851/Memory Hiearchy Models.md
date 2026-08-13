# Cache Obliviousness

DAM model: only two levels of memory, cache (infinitely fast, size $m$, divided into blocks of size $b$) and disk (infinitely slow, transferring one block to cache is one operation)

Trivially, upper bound is RAM time and lower bound is cell probe time (only read times count, computation is free) divided by $B$

Linear Scan: $O(\lceil N/b \rceil)$
Search Trees: $\log_{b+1}(N)$ which is lower bound in comparison model
other results listed

Cache oblivious: algo doesn't know $b$ or $m$ so it reads as a RAM algo but analysis is diff. We assume cache replacement is handled for us in the optimal manner (since LRU/FIFO is generally very close to optimal)

# Static Cache Oblivious B-tree
Just do binary search and encode into memory in a way that minimizes block reads. Best is Van Emde Boas order (split tree at half height and recursively layout first the top subtree of size $\sqrt{n}$ and then the $\sqrt{n}$ bottom subtrees each of size $\sqrt{n}$)

This gets you $\leq 4 \log_{B+1} N$ mem transfers (although const factor can be proved to be $\log_{2} e$). Proof Omitted

# Dynamifying
Storing each element of a OFM (Ordered file maintaince) structure in the leaves of that tree. Intermediate nodes store max of children. 

Let $a$ = smallest possible size of a subtree (a power of 2) greater than $B$
Let $b$ = greatest possible size of a subtree (a power of 2) less than $B$

Since updating in OFM shifts at most $\log ^{2} N$ elements, we need to update  $>\frac{\log ^{2} N}{B}$ last layer $b$-sized subtrees and all their ancestors. We can update last two layers with post-order traversal keeping parent subtree (second lat layer) in cache when updating its child subtree causing parent accesses to be free amortized over children.

Since parent access free, analysis is effectively linear scan over last layer in-interval $b$-sized subtrees which is $O\left( \frac{\log ^{2} N}{B} \right)$

Root nodes of second last layer $b$-sized subtrees have $a$ nodes beneath so our interval falls under $< \frac{\log ^{2}N}{B}$ root nodes .  $O\left( \frac{\log ^{2} N}{B} \right)$ to update the entire subtree that spans over those root notes. Then $O(\log_{B+1}N)$ to update the path from the root node of that subtree to the root of tree.

