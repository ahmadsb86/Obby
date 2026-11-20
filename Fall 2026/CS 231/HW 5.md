# Problem 1

We can prove this by counting in two ways the number of possible subsets from a set of size n.

Method 1:
Let $\Omega$ represent the set of all subsets. We can partition $\Omega$ into $n$ distinct partitions such that each partition $i$ contains all the subsets of size $i$. We can count the size of the first partition by counting how many subsets of size 1 exist. This is equivalent to the number of ways we can choose one element from a set of size n. That is $n$ choose 1.
Then we can count the size of the second partition (the number of subsets of size 2) by doing $n$ choose 2. In this way, the size of every partition $i$ can be found. by calculating $n$ choose $i$.  To find the total size of $\Omega$ we can simply sum the size of all these partitions. Therefore,
$$
	\Omega = \sum_{i=1}^{n} \binom{n}{i}
$$
This is due to the **sum rule**.

Method 2:
A single subset can also be thought of a bitstring of size $n$, where the $i$th boolean value denotes whether the $i$th element of the original set is included in the subset. Thus, the total number of different subsets is equal to the number of different bitstrings we can create of size $n$. Since each bit can either be 1 or 0, and these are all independent disjoint events, we can use the **product rule**. The total number of bitsrings would be $2 \times 2 \times 2 \times \dots \times 2 = 2^{n}$.


Since both of these methods count the same thing, it must follow that 
$$2^{n}=\sum_{i=1}^{n} \binom{n}{i}$$
# Problem 2

The partitions of $S$ are:

1. $\{\{2,3,5,7\}\}$
2. $\{\{2\},\{3,5,7\}\}$
3. $\{\{3\},\{2,5,7\}\}$
4. $\{\{5\},\{2,3,7\}\}$
5. $\{\{7\},\{2,3,5\}\}$
6. $\{\{2,3\},\{5,7\}\}$
7. $\{\{2,5\},\{3,7\}\}$
8. $\{\{2,7\},\{3,5\}\}$
9. $\{\{2,3\},\{5\},\{7\}\}$
10. $\{\{2,5\},\{3\},\{7\}\}$
11. $\{\{2,7\},\{3\},\{5\}\}$
12. $\{\{3,5\},\{2\},\{7\}\}$
13. $\{\{3,7\},\{2\},\{5\}\}$
14. $\{\{5,7\},\{2\},\{3\}\}$
15. $\{\{2\},\{3\},\{5\},\{7\}\}$

Therefore, there are $15$ different partitions of $S$.

# Problem 3

Let $P(n)$ denote the statement $r_{n} = 7\cdot r_{n-1} - 10 \cdot r_{k-2}$

**Claim:**
$\forall n \in \mathbb{N}\ \text{, } P(n)$

**Base Case:**
$r_{0} = 5$
$r_{0} = 3 \cdot 2^{0} + 2 \cdot 5^{0} = 5 \quad \checkmark$
$r_{1} = 16$
$r_{0} = 3 \cdot 2^{1} + 2 \cdot 5^{1} = 15 \quad \checkmark$


**Inductive Step:**
Towards a proof by induction, suppose that $P(k)$ holds for all $k \in [0,k]$. From this we will prove $P(k+1)$.
