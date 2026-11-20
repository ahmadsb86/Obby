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

Every partition of $S$ must "draw a line" between two elements such that elements to the left of that line exist in a separate partition from the elements on the right. To find the number of different partitions of $S$, we simply need to find how many such lines can be drawn. 

The cardinality of $S$ is 4, so the number of possible lines between two elements must be $3$. Every partitioning of $S$ is essentially a subset of these three possible partition lines. As discussed in problem 1, the number of such subsets would just be $2^{3}$.

Therefore, there are $2^{3}=8$ different partitions


# Problem 3

