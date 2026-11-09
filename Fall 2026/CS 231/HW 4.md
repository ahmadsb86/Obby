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

However, this is still a non-recursive definition. Since every term from $r_{3}$ onwards is a geometric progression (with first term 3 and common ratio 2), we can use the formula for term of geometric progression ($a \cdot r^{d-1}$). 

$$r_{n} = 
\begin{cases}
n &n\leq 2\\
3 \cdot 2^{n-3} &n>2\\
\end{cases}
$$

# Problem 3

Let $f:A\to B$ be defined as  $$f(x,y)  = (x-1)k + y$$First, I will prove this function is injective by showing that  
$$
	f(a,b) = f(c,d) \implies (a,c) = (b,d)
$$
Towards a proof of this implication, let us assume $f(a,b) = f(c,d)$. Then,
$$
	\begin{align}
	(a - 1)k + b &= (c - 1)k + d \\
	ak - k + b &= ck - k + d \\
	ak + b &= ck + d \\
	ak + b \text{ (mod k)} & = ck + d \text{ (mod k)} \\
	b \text{ (mod k)} &= d \text{ (mod k)} \\
	\end{align}
$$
Since $1 \leq b,d \leq k$ , it follows that $b=d$. Plugging this back into our equation,
$$
\begin{align}
ak + b &= ck + b \\
ak &= ck \\
a &= c
\end{align}
$$
We can divide by $k$ since we can safely assume $k>1$ from the problem statement. Since $a=c$ and $b=d$, it must necessarily be true that $(a,b)=(c,d)$. Therefore, it has been proved that
$$
	f(a,b) = f(c,d) \implies (a,c) = (b,d)
$$

Let's now prove that the function is surjective. First, we check that $f$ actually maps into $B$. Since $1 \leq x \leq n$ and $1 \leq y \leq k$, we have

$$  
\begin{align}  
\min{f(x,y)} &= (1-1)k + 1 = 1 \\ 
\max{f(x,y)} &= (n-1)k + k = nk  
\end{align}  
$$

so $1 \leq f(x,y) \leq nk$. Thus, $f(x,y) \in [n\cdot k]$.

Now we must show that for every $m \in B$ there exists $(x,y) \in A$ with $f(x,y) = m$. Let $m \in [n\cdot k]$ be arbitrary. Since $m - 1 \geq 0$, the division algorithm gives integers $q, r$ such that

$$  
m - 1 = qk + r, \qquad 0 \leq r \leq k-1.  
$$

Define $x = q + 1$ and $y = r + 1$. We check that $(x,y) \in A$.

- Since $0 \leq r \leq k-1$, we have $1 \leq y \leq k$.
- Since $m - 1 \geq 0$ and $r \geq 0$ with $k > 0$, we get $q \geq 0$, so $x \geq 1$.
- Since $m \leq nk$, we have $qk \leq qk + r = m - 1 \leq nk - 1 < nk$. Dividing by $k$ gives $q < n$, so $q \leq n-1$ and $x \leq n$.

Therefore $(x,y) \in [n] \times [k] = A$. Finally,

$$  
\begin{align}  
f(x,y) &= (x-1)k + y \\  
&= qk + (r+1) \\  
&= (qk + r) + 1 \\  
&= (m-1) + 1 = m  
\end{align}  
$$

Since $m \in B$ was arbitrary, every element of $B$ has a source in $A$, so $f$ is surjective. Combined with injectivity, $f$ is a bijection, and hence $|A| = |B|$.

# Problem 4

First, I will prove this function is injective by showing that  
$$
	f(x) = f(y) \implies x = y
$$
Towards a proof of this implication, let us assume $f(x) = f(y)$. It follows that,
$$
\begin{align}
	& ax + b = ay + b \\
	& ax = ay \\
	& x = y \quad \text{(since }a \neq 0 \text{)}
\end{align}
$$
Therefore, the function is injective.
Now, I will prove this function is surjective by showing that
$$
	\forall y \in \mathbb{R}, \exists x \in \mathbb{R} \quad f(x) = y
$$
Towards a direct proof, let $y \in \mathbb{R}$ be arbitrary. Define $x = \dfrac{y - b}{a}$, which is a well-defined real number since $a \neq 0$. Then,

$$  
\begin{align}  
f(x) &= a\left(\frac{y-b}{a}\right) + b \\  
&= (y - b) + b \\
&= y  
\end{align}  
$$

Therefore, the function is surjective.

Since $f$ is both injective and surjective, $f$ is a bijection. 

# Problem 5

We essentially need a function $f(x)$ such that
$$
	\lim_{ x \to 1 }  f(x) = \infty \\
	\lim_{ x \to -1 } f(x) = -\infty
$$
Consider the function 
$$f(x) = \frac{1}{1-x}-\ \frac{1}{1+x} = \frac{2x}{1-x^{2}}$$
First, I will prove this function is injective by showing that
$$f(x) = f(y) \implies x = y$$
Towards a direct proof of this implication, let us assume $f(x) = f(y)$. Then,
$$  
\begin{align}  
\frac{2x}{1-x^2} &= \frac{2y}{1-y^2} \\  
x(1-y^2) &= y(1-x^2) \\  
x - y + xy(x - y) &= 0 \\ 
(x-y)(1+xy) &= 0  
\end{align}  
$$
Since $|x|,|y| < 1$, we have $|xy| < 1$, so $1 + xy > 0$. Hence $1+xy \neq 0$, and therefore $x = y$. It follows that the function is injective.

Now, I will prove this function is surjective by showing that
$$\forall y \in \mathbb{R}, \exists x \in (-1,1) \quad f(x) = y$$
Let $y \in \mathbb{R}$ be arbitrary. Let $s = \sqrt{1+y^2}$, so $s \geq 1$ and $s^2 - 1 = y^2$. Define
$$x = \frac{y}{1+s}.$$
We first check if $x \in (-1,1)$. Since $y^2 < 1 + y^2$, we have $|y| < s < 1 + s$, so $|x| = \dfrac{|y|}{1+s} < 1$. Thus, $x \in (-1,1)$

Next, we find the value of $f(x)$. We have
$$x^2 = \frac{y^2}{(1+s)^2} = \frac{(s-1)(s+1)}{(s+1)^2} = \frac{s-1}{s+1}, \qquad 1 - x^2 = \frac{2}{s+1}.$$
Then,
$$  
\begin{align}  
f(x) &= \frac{2x}{1-x^2} \\  
&= \frac{2y}{1+s}\cdot\frac{s+1}{2} \\ 
&= y  
\end{align}  
$$
Therefore, the function is surjective. Since $f$ is both injective and surjective, $f$ is a bijection. 