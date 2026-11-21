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

Let $P(n)$ denote the statement $r_{n} = 3 \cdot 2^{n} + 2 \cdot 5^{n}$

**Claim:**
$\forall n \in \mathbb{N}\ \text{, } P(n)$

**Base Case:**
$r_{0} = 5$
$r_{0} = 3 \cdot 2^{0} + 2 \cdot 5^{0} = 5 \quad \checkmark$
$r_{1} = 16$
$r_{1} = 3 \cdot 2^{1} + 2 \cdot 5^{1} = 16 \quad \checkmark$


**Inductive Step:**
Towards a proof by induction, suppose that $P(k)$ holds for all $k \in [0,n]$. From this we will prove $P(n+1)$.

From the definition of $r$, we have:
$r_{n+1} = 7\cdot r_{n} - 10 \cdot r_{n-1}$
Since $P(n)$ and $P(n-1)$, we have
$r_{n} = 3 \cdot 2^{n} + 2 \cdot 5^{n}$ and $r_{n-1} = 3 \cdot 2^{n-1} + 2 \cdot 5^{n-1}$
Plugging these two expressions back into the previous equation, we have:
$$
\begin{align}
r_{n+1} &= 7 \cdot (3 \cdot 2^{n} + 2 \cdot 5^{n}) - 10 \cdot (3 \cdot 2^{n-1} + 2 \cdot 5^{n-1}) \\
& = 21 \cdot 2^{n} + 14 \cdot 5^{n} - 30 \cdot 2^{n-1} - 20 \cdot 5^{n-1} \\
&= 21 \cdot 2^{n} - 30 \cdot 2^{n-1} + 14 \cdot 5^{n} - 20 \cdot 5^{n-1} \\
&= 21 \cdot 2^{n} - 15 \cdot 2^{n} + 14 \cdot 5^{n} - 4 \cdot 5^{n} \\
&= 6 \cdot 2^{n} + 10 \cdot 5^{n} \\
&= 3 \cdot (2 \cdot 2^{n}) + 2(5 \cdot 5^{n}) \\
&= 3 \cdot (2^{n+1}) + 2 \cdot (5^{n+1}) \\
& \therefore P(n+1)
\end{align}
$$
Therefore, $P(n-1) \land P(n) \implies P(n+1)$ and also $P(0) \land P(1)$. Hence, by the principle of strong mathematical induction, $\forall n \in \mathbb{N} \text{, } P(n)$.

# Problem 4

i) Each of the three letters can be chosen in $26$ ways and each of the three digits can be chosen in $10$ ways. Since these choices are independent, we can use the product rule.
$$26^{3} \cdot 10^{3} = 17576 \cdot 1000 = 17{,}576{,}000$$

ii) Now each choice reduces the option space for the next one. There are $26$ options for the first letter, $25$ for the second, and $24$ for the third. There are $10$, $9$, and $8$ options for the digits. By the product rule,
$$(26 \cdot 25 \cdot 24)(10 \cdot 9 \cdot 8) = 15600 \cdot 720 = 11{,}232{,}000$$

iii) I'll count the complement of each condition separately. The number of letter strings with at least one H is the total number of letter strings minus those with no H at all:
$$26^{3} - 25^{3} = 17576 - 15625 = 1951$$
Similarly, the number of digit strings with at least one 4 is
$$10^{3} - 9^{3} = 1000 - 729 = 271$$
The letters and the digits are chosen independently so we can use the product rule.
$$1951 \cdot 271 = 528{,}721$$

# Problem 5

Let $f(x,y) = (u,v)$, so that
$$u = x + y + 1 \quad \text{and} \quad v = x - y$$
To find the inverse, we solve for $x$ and $y$ in terms of $u$ and $v$. Adding the two equations gives
$$u + v = 2x + 1 \implies x = \frac{u + v - 1}{2}$$
Subtracting the second from the first gives
$$u - v = 2y + 1 \implies y = \frac{u - v - 1}{2}$$
So we define $g : \mathbb{R} \times \mathbb{R} \to \mathbb{R} \times \mathbb{R}$ by
$$g(x,y) = \left( \frac{x + y - 1}{2},\ \frac{x - y - 1}{2} \right)$$
