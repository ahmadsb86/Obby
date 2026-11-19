# Defining the Problem

Consider an $n \times n$ grid system such that every row $i$ contains one horizontal ray of length $a_{i}$ ($0 < a_{i} \leq n)$ starting from the right-most column. Every column $j$ contains one query point at row $q_{j}$  ($0 \leq q_{j} < n)$.

Our goal is to create an algorithm that finds the horizontal ray directly below every query point (essentially vertical ray-casting). More specifically, for every $q_{j}$ our algorithm must find the highest row $r_{j}$ such that $r_{j} \geq q_{j}$ ($r_{j}$ is below $q_{j}$) and $a_{r_{j}} \geq j$ (the horizontal ray at $r_{j}$ reaches column $j$).

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

Fractional cascading also gives the same bo