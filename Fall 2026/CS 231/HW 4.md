# Problem 1

Let $P(n)$ represent the predicate that $3|r_{4n}$. The claim is that $P(n)$ is true for all $n \in \mathbb{N}$

First, we will prove the base case of P(1),
$$
	\begin{align}
		r_{4(1)} = r_{3}+r_{2} &= r_{2} + r_{1} + r_{1} + r_{0}  \\
		& = r_{1} + r_{0} + r_{1} + r_{1} + r_{0} \\
		& = 1 + 0 + 1 + 1 + 0 \\
		& =3
	\end{align}
$$
Since 3 clearly divides 3, we can safely say $3 | r_{4}$ and thus $P(1)$ is true.

Towards a proof by induction, we will assume $P(k)$ is true for some arbitrary $k$. From this assumption we will show $P(k+1)$ is true. 

Consider $r_{4(k+1)}$

$$
	\begin{align}
	r_{4(k+1)} = r_{4k+4} &= r_{4k + 3} &+ r_{4k + 2}  \\
	& = r_{4k+2} + r_{4k+ 1} &+ r_{4k + 1} + r_{4k} \\
	& = r_{4k + 1} + r_{4k} + r_{4k+1} &+ r_{4k + 1} + r_{4k}\\
	\end{align}
$$
After rearranging,
$$
	r_{4(k+1)} = 3 \cdot r_{4k+1} + 2 \cdot r_{4k}
$$
$2 \cdot r_{4k}$ must be divisible by 3, because $3 | r_{4k}$ (inductive assumption) and the sum of any two numbers divisible by 3 must be divisible by 3. This is derived from the following property of modular arithmetic:
$$
	a + b \text{ (mod d)} = \left[    a \text{ (mod d)} + b\text{ (mod d)} \right] \text{ (mod d)}
$$
Also, by the definition of divisibility, 
$$3|3 \cdot r_{4k+1} \iff \exists c \in \mathbb{N}, 3c = 3 \cdot r_{4k+1}$$
Since $r_{4k+1} \in \mathbb{N}$, it is a valid value for $c$. Thus, $3 \cdot r_{4k+1}$ is divisible by 3.

It follows that $3 | 3 \cdot r_{4k+1} + 2 \cdot r_{4k}$. Hence, $3 | r_{4(k+1)}$. Therefore, $P(k+1)$ is shown. 

Thus, by the principle of mathematical induction, $\forall n \in \mathbb{N}, P(n)$.

# Problem 2

Writing the first few terms of $r_{n}$ helps us find a general pattern
$$r = 0, 1, 2, 3, 6, 12, 24, 48, ..$$
We can clearly see that after $r_{3}$, every next term of $r$ is double the previous term. Why?

Consider $r_{n}$. By definition, 
$$
\begin{align}
r_{k} &= r_{0} + r_{1} + r_{2} + r_{3} + \dots r_{n-2} + r_{n-1} \\
&= (r_{0} + r_{1} + r_{2} + r_{3} + \dots r_{n-2}) + r_{n-1} \\
&= (r_{n-1}) + r_{n-1} \\
&= 2 \cdot r_{n-1}
\end{align}
$$
It is important to note that this rule breaks until (and including) $r_{3}$ because $r_{0}$ and $r_{1}$ do not follow the recurrence relation. Our result above requires that up the term $r_{n-2}$ follows the recurrence relation definition in the question.

However, this is still a non-recursive definition. Since every term from $r_{3}$ onwards is a geometric progression (with first term 3 and common ratio 2), we can use the formula for term of geometric progression.

$$r_{n} = 
\begin{cases}
n &n\leq 2\\
3 \cdot 2^{n-3} &n>2\\
\end{cases}
$$