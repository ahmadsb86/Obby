## Question 1

Let $X$ represent the set of all advisors and $Y$ represent the set of all students

1. There exists some advisor $x$, such that there exists a student $y$ that makes $P(x,y)$ true.
	$\exists x \in X, \exists y \in Y, P(x,y)$
2. For every advisor $x$, there exists a student $y$ such that $P(x,y)$ is false 
	$\forall x \in X, \exists y \in Y, \neg P(x,y)$
3. There exists a student $y$, such that $P(y,y)$ is true.
	$\exists y \in Y, P(y,y)$
4. There exists an advisor $x$, and there exists a set $S$, such that for every student $y$ in $S$, $P(x,y)$ is true AND the size of $S$ is greater than one
	Alternatively: There exists an advisor $x$, there exists a student $a$, and there exists a student $b$, such that $P(x,a)$ AND $P(x,b)$ AND $a \neq b$
	$\exists x \in X, \exists a \in Y, \exists b \in Y, P(x,a) \land P(x,b) \land a \neq b$

## Question 2

1. Let $Q(x,y,z)$ be a predicate that means "Inside building $x$, student $y$ has a class $z$". Then $\exists x, \forall y, \exists z, Q(x,y,z)$ means that there is a building in which all students have some class.
2. Let $R(x,y)$ be a predicate that means "x and y are friends". Then, $∃x, ∃y, ∃z, R(x, y) ∧ ¬R(y, z)$ can be interpreted as:  3 people that can be chosen such that one of them is friends with ONLY one of the other two. 

# Question 3

**Version 1**: Assuming we can do basic arithmetic operations like division.
Simply divide both sides of the equation by 3.
$0=3 \implies \frac{0}{3}=\frac{3}{3} \implies 0=1$ 

**Version 2**: Weird contrapositive proof 
By contraposition we can prove that $0=3 \implies 0=1$ by proving that $0 \neq 1 \implies 0 \neq 3$.
- By repeatedly adding 1 to each side, we get $0 \neq 1 \implies 1 \neq 2 \implies 2 \neq 3 \implies 3 \neq 4$. 
- Let us define $S$ to be the set of all positive integers less than or equal to 4. Thus, $S = \left\{  x \in \mathbb{Z}^+ \mid x \leq 4 \right\} = \{ 1,2,3,4 \}$. Clearly, there are 4 positive integers less than or equal to 4, so $S$ must contain 4 elements. However, if 1 was equal to 4 then the set $S$ would also contain 3 elements. Since $S$ cannot contain both 3 elements and 4 elements at the same time (since $3\neq 4$ was established before), 1 cannot be equal to 4. 
- By subtracting 1 from both sides  $1\neq 4 \implies 0 \neq 3$.
Therefore $0\neq 1 \implies 0 \neq 3$

**Version 3**: Assuming that the intersection between non-empty sets is a subset of their union
Consider the following sets:

- $A=\{ 0\}$
- $B=\{ 1 \}$
- $C = \{ 2 \}$

Now consider the intersection of these 3 sets. It must contain 0 elements since there are no common elements, but it must also contain 3 elements because $0=3$. Since the intersection is always a subset of the union (from the aforementioned assumption), and the union also contains 3 elements (i.e. 0,1, and 2), the intersection must have the same elements as the union. If the intersection of three sets is equal to their union, it must follow that the three sets contain the same elements (otherwise, there must exist elements not common to all sets, and therefore an element present in the union but not the intersection).

Therefore, $0=1=2$ and thus, $0=1$.

After writing this proof, I realized the second sentence, "(the intersection) must contain 0 element since there are no common elements" draws upon the fact that 0, 1, and 2 are different numbers. However, comparing whether some integers are equal or not seems very circular for a proof about $0=3$. To fix this, maybe one can prove that 0, 1, and 2 are different numbers by describing a property that only one of those numbers holds (e.g. 0 is different from 1 and 2 because it is the only number of the three strictly less than 1).

