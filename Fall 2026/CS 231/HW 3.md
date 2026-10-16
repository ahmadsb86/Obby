# Problem 1

In this problem, I will use $P$ to denote  $\mathcal{P}$ for ease of typesetting.

Towards a proof by contradiction, suppose $A \subseteq B$ and $P(A) \not\subseteq P(B)$. Therefore, there exists a set $x$ such that $x \in P(A) \land x \not\in P(B)$. Since $x$ is an element of $P(A)$, $x$ must be a subset of A. Hence, $\forall y \in x,  y \in A$.

However, since $x$ is not an element of $P(B)$, $x$ is not a subset of $B$ (by definition of $P$). Thus, $\exists z \in x, z \not\in B$. 

Combining the logical conclusions of the previous two paragraphs, we have: $\exists z \in x, z \in A \land z \not\in B$
In other words, there exists an element within $A$ but not in $B$. Hence, $A$ is not a subset of $B$ (by definition of subset). This is a contradiction because of our initial assumption that $A$ is a subset of $B$. 

Thus, the initial assumption must be false.

# Problem 2

Towards a direct proof, suppose that $d|a$ and $d|b$. This would mean that there exists some integer $x$ and some integer $y$ such that $a = xd$ and $b = yd$. Then, $a+b = xd+yd$.  It follows that, $a+b = d(x+y)$ by the distributive property. Since $x$ and $y$ are integers, $x+y$ must be an integer. Therefore, $d|(a+b)$ by definition of divisibility.

# Problem 3

Towards a proof by contradiction, suppose that there does exist a largest $x \in \mathbb{Q}$ such that $x<1$. Consider the  number $y = \frac{x+1}{2}$. This is the mean of that number $x$ and $1$.

First, we will prove that $y$ is rational. 

Since $x$ is rational, it can be expressed as $x=\frac{a}{b}$ where $a$ and $b$ are integers. Therefore, $x+1 = \frac{a}{b}+1 = \frac{a+b}{b}$. Let $c=a+b$. Since $c$ is the sum of two integers, $c$ must also be an integer. Hence, $x+1$ can be represented as $\frac{a+b}{b} = \frac{c}{b}$ where $c$ and $b$ are both integers. Hence, $\frac{x+1}{2}$ can be represented as $\frac{c}{2b}$. Since 2 is an integer and $b$ is an integer, the denominator $2b$ is also an integer. Therefore, $\frac{x+1}{2}$ can be represented as an integer divided by another integer (both $c$ and $2b$ are integers). It follows that $\frac{x+1}{2}$ (and therefore $y$) is rational.

Next, we will prove that $x<y<1$.

Since $x<1$, it must be true that $\frac{x+1}{2} < \frac{1+1}{2}$ (adding 1 and dividing by 2 on both sides). Therefore, $\frac{x+1}{2}<1$. Hence, $y<1$

Also, since $y$ is the average of $x$ and $1$, $y$ must lie between them. Therefore, if $x<1$, then $y>x$. However, this can be proved more formally. Consider
$$
\begin{align}  
y - x &= \frac{x+1}{2} - x = -\frac{x}{2} + \frac{1}{2} \\  
&= \frac{1 - x}{2}.  
\end{align}

$$

Since $x < 1$, we have $1 - x > 0$. Dividing a positive number by 2 keeps it positive, therefore

$$\frac{1 - x}{2} > 0.$$

This means $y - x > 0$, so $y > x$.




# Problem 4

By squaring both sides, it is clear that the equation
$$
	x^{2}=x+a
$$
is implied from the equation in the problem statement. It is important to note that this implication only goes one way because the square of two distinct numbers can possibly be equal. Therefore, any conclusion drawing from this must be cross-verified with the equation in the problem statement.

Now, we subtract $x$ and $a$ from both sides of the equation:
$$x^{2} - x -a = 0$$
Using the quadratic formula, we know $$x = \frac{1\pm \sqrt{ (-1)^{2} -4(1)(-a)}}{2(1)}=\frac{1\pm \sqrt{ 1+4a }}{2}$$
The discriminant for this quadratic is $(-1)^{2} -4(1)(-a)=1+4a$. For a quadratic solution to have 2 real solutions, the discriminant must positive. Therefore,
$$
\begin{align}
&1+4a>0 \\
& a >-\frac{1}{4}
\end{align}
$$
However, as mentioned before, we must cross-validate with the original statement to find the tightest bound on $a$. 

Since $\sqrt{ x+a }$ can never be negative, $x$ can never be negative. Therefore, 
$$
\begin{align}
&\frac{1\pm \sqrt{ 1+4a }}{2} \geq 0 \\
\end{align}
$$
We can safely treat the $\pm$ sign as a $-$ sign, because if the inequality holds for $-$, it must hold for $+$. Therefore,
$$
\begin{align}
&1-\sqrt{ 1+4a } \geq 0 \\
&1 \geq 1+4a \\
& 0 \geq 4a \\
& a \leq 0
\end{align}
	
$$
Tightening the previous bound with this result, we have:
$$
	-\frac{1}{4} < a \leq 0
$$

# Problem 5

Let $P(k)$ represent the predicate that 
$$\sum_{i=1}^{k} i \cdot (i-1) = \frac{k(k-1)(k+1)}{3}$$
First, we will prove the base case of $P(1)$:
$$
	\begin{align}
	& \sum_{i=1}^{1}  i \cdot (i-1) = 1 \cdot (1-1) = 0 \\
	& \frac{1(1-1)(1+1)}{3} = 0
	\end{align}
$$
Therefore, $P(1)$ holds true.

Towards a proof by induction, suppose that $P(k)$ holds true. Therefore

$$
\begin{align}
\sum_{i=1}^{k} i \cdot (i-1) &= \frac{k(k-1)(k+1)}{3} \\
\sum_{i=1}^{k+1} i \cdot (i-1) &= \frac{k(k-1)(k+1)}{3} + (k+1)(k) \\
&= k(k+1)\left( \frac{k-1}{3} + 1 \right) \\ 
&= k(k+1) \cdot \frac{k+2}{3} \\
&= \frac{(k+1)\big((k+1)-1\big)\big((k+1)+1\big)}{3}
\end{align}
	
$$
It follows that $P(k+1)$ holds. Hence, by the principle of mathematical induction, $P(k)$ must hold for any $k$. Therefore, the original claim must hold.

# Problem 6

Let $P(n)$ represent the predicate that
$$6|(n^{3} + 5n)$$
First, we will prove the base case of $P(1)$:
$$
	\begin{align}
	& 1^{3} + 5(1) = 1 + 5 = 6 \\
	& 6 = 6 \cdot 1
	\end{align}
$$
Since $1$ is an integer, $6|6$ by definition of divisibility. Therefore, $P(1)$ holds true.

Towards a proof by induction, suppose that $P(k)$ holds true. Therefore, there exists some integer $x$ such that $k^{3} + 5k = 6x$. Now consider

$$
\begin{align}
(k+1)^{3} + 5(k+1) &= k^{3} + 3k^{2} + 3k + 1 + 5k + 5 \\
&= (k^{3} + 5k) + 3k^{2} + 3k + 6 \\
&= 6x + 3k(k+1) + 6
\end{align}
$$
Since $k$ and $k+1$ are consecutive integers, one of them must be even. Hence, $k(k+1)$ is even, so there exists some integer $y$ such that $k(k+1) = 2y$. It follows that $3k(k+1) = 3(2y) = 6y$. Substituting this, we have:
$$
\begin{align}
(k+1)^{3} + 5(k+1) &= 6x + 6y + 6 \\
&= 6(x + y + 1)
\end{align}
$$
by the distributive property. Since $x$, $y$, and $1$ are integers, $x + y + 1$ must be an integer. Therefore, $6|\big((k+1)^{3} + 5(k+1)\big)$ by definition of divisibility.

It follows that $P(k+1)$ holds. Hence, by the principle of mathematical induction, $P(n)$ must hold for any $n$. Therefore, the original claim must hold.

# Problem 7

Since $n \equiv 5 \pmod{7}$, there exists some integer $a$ such that $n = 7a + 5$ (by definition of congruence). Substituting this into the second congruence, we have:
$$
\begin{align}
& 7a + 5 \equiv 4 \pmod{9} \\
& 7a \equiv -1 \pmod{9} \\
& 7a \equiv 8 \pmod{9}
\end{align}
$$
Since $7 \cdot 4 = 28 \equiv 1 \pmod{9}$, we can multiply both sides by $4$ to isolate $a$. Hence,
$$
\begin{align}
& 28a \equiv 32 \pmod{9} \\
& a \equiv 5 \pmod{9}
\end{align}
$$
Therefore, there exists some integer $b$ such that $a = 9b + 5$. Substituting this back into $n = 7a + 5$:
$$
\begin{align}
n &= 7(9b + 5) + 5 \\
&= 63b + 40
\end{align}
$$
However, as in Problem 4, we must cross-verify with the original statement. First, $n = 63b + 40 = 7(9b + 5) + 5$. Since $9b + 5$ is an integer, $n \equiv 5 \pmod{7}$. Next, $n = 63b + 40 = 9(7b + 4) + 4$. Since $7b + 4$ is an integer, $n \equiv 4 \pmod{9}$. Hence, every number of this form satisfies both congruences.

Since $n$ must be a natural number, $b$ cannot be negative. It follows that all possible $n$ are represented by the formula
$$
	n = 63b + 40, \quad b \in \mathbb{Z}, \ b \geq 0
$$

# Problem 8

Towards a proof by contradiction, suppose that there does exist $n \in \mathbb{N}$ such that $n \equiv 5 \pmod{6}$ and $n \equiv 7 \pmod{15}$.

Since $n \equiv 5 \pmod{6}$, there exists some integer $x$ such that $n = 6x + 5$. Therefore,
$$
n = 6x + 5 = 6x + 3 + 2 = 3(2x + 1) + 2
$$
Since $2x + 1$ is an integer, $n$ leaves a remainder of $2$ when divided by $3$. Hence, $n \equiv 2 \pmod{3}$.

Also, since $n \equiv 7 \pmod{15}$, there exists some integer $y$ such that $n = 15y + 7$. Therefore,
$$
n = 15y + 7 = 15y + 6 + 1 = 3(5y + 2) + 1
$$
Since $5y + 2$ is an integer, $n$ leaves a remainder of $1$ when divided by $3$. It follows that $n \equiv 1 \pmod{3}$.

Combining the logical conclusions of the previous two paragraphs, we have: $n \equiv 2 \pmod{3}$ and $n \equiv 1 \pmod{3}$. In other words, $n$ leaves two different remainders when divided by $3$. This is a contradiction because the remainder of an integer divided by $3$ is unique (by the division algorithm). Therefore, there does not exist $n \in \mathbb{N}$ such that $n \equiv 5 \pmod{6}$ and $n \equiv 7 \pmod{15}$.

