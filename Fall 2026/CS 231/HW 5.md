# Problem 1

We can prove this by counting in two ways the number of possible subsets from a set of size n.

Method 1:
Let $\Omega$ represent the set of all subsets. We can partition $\Omega$ into $n$ distinct partitions such that each partition $i$ contains all the subsets of size $i$. We can count the size of the first partition by counting how many subsets of size 1 exist. This is equivalent to the number of ways we can choose one element from a set of size n. That is $n$ choose 1.
Then we can count the size of the second partition (the number of subsets of size 2) by doing $n$ choose 2. In this way, the size of every partition $i$ can be found by calculating $n$ choose 