Some terminology I'll use:
1. $d$ is the distance between a $j_{2}$ column and the closest 0 left of that $j_{2}$ column.
2. $k$ is the row index of the 0 value closest to the bottom of a certain column. 

# Logarithmic Time Approaches:

Balanced Binary Search Tree.

The easiest logarithmic time approach is to simply use a balanced binary search tree that supports $O(\log n)$ deletion and $O(\log n)$ predecessor query. 

Algorithm: Store each row in a group based on $d$. Initially keep all row indexes in a balance binary search tree $S$. Sweep all possible $j_{1}$ columns from right to left. For a certain $j_{1}$, simply run predecessor on $k(j_{1})$, i.e. the lowest 0 value in $j_{2}$. Then check which $d$-groups that will be out of range for the next iteration. Delete these from $S$.

Complexity Analysis: For every $j_{1}$ in our sweep, we spend $O(\log n)$ time to run the predecessor query. Thus, the total time complexity for all predecessors queries is  $O(n \log n)$. Reading out the elements to delete from the $d$-groups takes $O(x)$ time, where $x$ is the number of rows to delete from $S$. The deletion of $x$ elements from $S$ takes $O(x \log n)$. However, every element is only read out from the $d$-groups once and only deleted once, so the total time complexity of all deletions is also $O(n \log n)$. Hence, our algorithm takes $O(n \log n)$.

Fractional Cascading.
Fractional Cascading yields  

$$
	n \left(  \log n + n  \right) 
$$