# Problem 1

1. $\{  \}$
2. $\{ 0 \}$
3. $\{ 1 \}$
4. $\{ 0,1 \}$
5. $\{ 2 \}$
6. $\{ 0,2 \}$
7. $\{ 1,2 \}$
8. $\{ 0,1,2 \}$
9. $\{ 3 \}$
10. $\{ 0,3 \}$
11. $\{ 1,3 \}$
12. $\{ 2,3 \}$
13. $\{ 0,1,3 \}$
14. $\{ 0,2,3 \}$
15. $\{ 1,2,3 \}$
16. $\{ 0,1,2,3 \}$

In general there will always be $2^n$ subsets of a set with $n$ items. This is because each subset is really just a sequence of $n$ boolean values representing whether or not an element in the original set exists within that subset. Since each boolean value can take one of two values, there are two options for $n$ independent choices, or $2^n$ total possible sequences. Therefore, there are $2^n$ possible subsets.

# Problem 2

Yes. The following set is an example:
$\{ 0, 1, \{ 6,7,8,9 \} \}$
A set can be the member of a larger set. A set of size 4 can be one of the members of a larger set of size 3.

# Problem 3

Yes. Consider the following sets as an example.

Let set A represent all real numbers between 1 and 4
Let set B represent all real numbers between 3 and 6 inclusive
Let set C represent all real numbers either less than 2 or greater than 5

The intersection between A and B is infinite. All real numbers between 3 and 4 are part of both set A and set B, and there are an infinite number of real numbers between 3 and 4. As a short proof by contradiction, let's assume that there did exist a finite number of real numbers between 3 and 4. If you wrote them all out in ascending order, and took the average between two consecutive numbers, you would find a number that is between 3 and 4 yet not in that list. Therefore, the original list must not have contained all numbers between 3 and 4. It follows that there is an infinite number of real numbers between 3 and 4. 

The intersection between B and C is infinite. All real numbers between 5 and 6 are part of both set B and set C, and there are an infinite number of real numbers between 5 and 6. This is a result of the same logic used in the previous paragraph.

The intersection between A and C is infinite. All real numbers between 1 and 2 are part of both set A and set C, and there are an infinite number of real numbers between 1 and 2. This is a result of the same logic used before.

However, there is no real number that belongs to all 3 sets. Consider the intersection of A and B. This includes all numbers between 3 and 4. However, set C must not contain any of these elements since it only contains real numbers less than 2 (which is already less than 3) or greater than 5 (which is already greater than 4). Thus, the intersection of A and B has no common elements with C. This is enough to prove that no element belongs in all 3 sets. 

Hence, the intersection between all 3 sets is the empty set.

# Problem 4

Table 1: $(P →Q) ∨R$

| $P$ | $Q$ | $R$ | $P →Q$ | $(P →Q) ∨R$ |
| --- | --- | --- | ------ | ----------- |
| F   | F   | F   | T      | T           |
| F   | F   | T   | T      | T           |
| F   | T   | F   | T      | T           |
| F   | T   | T   | T      | T           |
| T   | F   | F   | F      | F           |
| T   | F   | T   | F      | T           |
| T   | T   | F   | T      | T           |
| T   | T   | T   | T      | T           |

Table 2: $¬P →(P →P )$

| $P$ | $\neg P$ | $P \to P$ | $\neg P \to (P \to P)$ |
| --- | -------- | --------- | ---------------------- |
| T   | F        | T         | T                      |
| F   | T        | T         | T                      |

Table 3: $(P ∧Q ∧¬R) ∨¬Q$

| $P$ | $Q$ | $R$ | $P \wedge Q \wedge \neg R$ | $\neg Q$ | $(P ∧Q ∧¬R) ∨¬Q$ |
| --- | --- | --- | -------------------------- | -------- | ---------------- |
| F   | F   | F   | F                          | T        | T                |
| F   | F   | T   | F                          | T        | T                |
| F   | T   | F   | F                          | F        | F                |
| F   | T   | T   | F                          | F        | F                |
| T   | F   | F   | F                          | T        | T                |
| T   | F   | T   | F                          | T        | T                |
| T   | T   | F   | T                          | F        | T                |
| T   | T   | T   | F                          | F        | F                |

# Problem 5

The existence of an x, such that $x^{2} > 5x + 12$ can be proved by example. For $x=10$, the statement is true. This is because the left hand side evaluates to $10^{2}=100$, while the right hand side evaluates to $5(10)+12=62$ and $100>62$. 

The smallest positive integer $x$, such that the inequality holds can be found by rearranging this into the form $x^{2}-5x-12 > 0$ and solving as a quadratic inequality as normal. The result is $x=7$

# Problem 6

**Proof for EVEN+EVEN=EVEN:**

Let $a$ and $b$ represent two elements which are elements of EVEN. Since they are both even, $\frac{a}{2}$ and $\frac{b}{2}$ are both integers by definition. Therefore, $\frac{a}{2}+\frac{b}{2}$ is an integer. It follows that $\frac{a+b}{2}$ must be an integer, and thus $a+b$ must be EVEN.

Since nothing about $a$ and $b$ was specified except that they must be elements of EVEN, it follows that the sum of any two numbers within EVEN must be an even number. Since every element in EVEN+EVEN must be the sum of two elements within EVEN, the set EVEN+EVEN must only contain even integers. Thus, EVEN+EVEN must equal the set of even numbers. Therefore, EVEN+EVEN=EVEN

**Proof for EVEN+{1} = ODD**

Every element of EVEN + {1} must, by definition, be the sum of an element within EVEN and a number within the set {1}. Since the set {1} only contains the number 1, every element of EVEN + {1} must be the sum of an even number and 1.

Let $a$ represent any even number. By definition, $\frac{a}{2}$ must be an integer. $\frac{a+1}{2}$ can be rewritten as $\frac{a}{2} + \frac{1}{2}$. Since $\frac{a}{2}$ is an integer and $\frac{1}{2}$ is not an integer, their sum clearly must not be an integer. Therefore $\frac{a+1}{2}$ cannot be an integer. This implies that $a+1$ is not divisible by 2, and therefore $a+1$ is not even (i.e. $a+1$ is odd). Since nothing was specified about $a$ apart from the fact that it must be an even number, it follows that any even number summed with 1 must be odd.

Therefore, the set of all even numbers summed with 1, EVEN + {1}, must only contain odd numbers. Hence, EVEN + {1} = ODD

**Is Z+Z=EVEN?**

No. Z+Z refers to the set containing all sums of any two integers. These two integers do not have to be the same integer, so the facts that EVEN+EVEN=EVEN and ODD+ODD=EVEN do not logically imply that Z+Z=EVEN. Z+Z could very well contain the sum of an element within EVEN and an element within ODD. As a proof, consider the counter-example of 3+4. Both 3 and 4 are elements of Z, but their sum would not be within the set EVEN. The sum would, however, be an element of Z+Z.

# Problem 7

It is clear that if $A=B$ then $A \times C$ is the same as $B \times C$. Since $A$ and $B$ are the same set, any operation on one set will have the same result as applying that operation on the other. The cartesian product with C is no different. Therefore, $A=B$ implies that $A \times C = B \times C$

Proving the implication in the other direction is less trivial. We can do so by proving the contrapositive. The statement "$A \times C = B \times C$ implies that $A=B$" is logically equivalent to "$A \neq B$ implies that $A \times C \neq B \times C$". 

Now, let us assume for the sake of the proof that $A \neq B$. This means that one of the following cases must be true:

Case 1: There exists an element $x$ such that $x \in A \cap x \not\in B$
Let $y$ represent any member of the set $C$ ($y$ must exist becasue $C \neq \emptyset$). Since $x$ is a member of $A$, the cartesian product $A \times C$ must contain the pair $(x,y)$. However, since $x \not\in B$, the pair $(x,y)$ cannot exist in $B \times C$, by definition of the cartesian product. Thus, the pair $(x,y)$ only exists in $A \times C$ but not in $B \times C$, which shows that $A \times C \neq B \times C$.

Case 2: There exists an element $x$ such that $x \in B \cap x \not\in A$
Let $y$ represent any member of the set $C$ ($y$ must exist becasue $C \neq \emptyset$). Since $x$ is a member of $B$, the cartesian product $B \times C$ must contain the pair $(x,y)$. However, since $x \not\in A$, the pair $(x,y)$ cannot exist in $A \times C$, by definition of the cartesian product. Thus, the pair $(x,y)$ only exists in $B \times C$ but not in $A \times C$, which shows that $A \times C \neq B \times C$.

Assuming that $A \neq B$, logically leads us to the conclusion that $A \times C \neq B \times C$ in both cases. Therefore $A \neq B$ implies that $A \times C \neq B \times C$. It follows that $A \times C = B \times C$ implies $A = B$.

Since $A \times C = B \times C$ implies $A = B$ and $A = B$ implies $A \times C = B \times C$, the two statements must be logically equivalent.

# Problem 8

$A \times A = \{ (0,0), (0,1), (1,0), (1,1) \}$

I will first try to deduce how to find a non-transitive relationship. We can derive the definition of a non-transitive relationship from that of a transitive relationship.

$$\exists x, \exists y, \exists z, R(x,y) \land R(y,z) \nRightarrow R(x,z)$$
which is the same as saying:
$$\exists x, \exists y, \exists z, R(x,y) \land R(y,z) \land \neg R(x,z)$$

First, notice that in the definition $x$ must be chosen different from $y$ and $y$ must be different from $z$, otherwise the statement is always false. 
If $x$ and $y$ are the same, then the statement reduces to $R(x,x) \wedge R(x,z) \land \neg R(x,z)$ which is a contradiction (a statement that is always false)
If $y$ and $z$ are the same, then the statement reduces to $R(x,y) \wedge R(y,y) \land \neg R(x,y)$ which is a contradiction (a statement that is always false)

The only two values that we can choose from for $x$, $y$, and $z$ are 0 and 1. Therefore, if we want to create a non-transitive relationship, we must choose from one of the following cases:

Case 1: $x = 0, y = 1, z = 0$. R contains $(0,1)$ and $(1,0)$ but not $(0,0)$. 
Case 2: $x = 1, y = 0, z = 1$. R contains $(1,0)$ and $(0,1)$ but not $(1,1)$.

Notice that the two cases require the same two cartesian pairs to be in R. Therefore to create a non-transitive relationship, the following must hold $R(0,1) \land R(1,0) \land \neg(R(0,0) \land R(1,1))$. In other words if R contains (0,1) and (1,0) but it does not contain either (0,0) or (1,1) then R is non-transitive. It follows that only the following subsets of $A \times A$ are non-transitive:

- $\{ (0,1), (1,0) \}$
- $\{ (0,1), (1,0), (0,0) \}$
- $\{ (0,1), (1,0), (1,1) \}$

Thus, finding every $R \subseteq A \times A$ such that $R$ is transitive boils down to writing down every subset of $A \times A$ except the non-transitive cases outlined above. It follows that only the following subsets of $A \times A$ are transitive:

1. $\emptyset$
2. $\{ (0,0) \}$
3. $\{ (0,1) \}$
4. $\{ (1,0) \}$
5. $\{ (1,1) \}$
6. $\{ (0,0), (0,1)\}$
7. $\{ (0,0), (1,0) \}$
8. $\{ (0,0), (1,1) \}$
9. $\{ (0,1),(1,1) \}$
10. $\{ (1,0), (1,1) \}$
11. $\{ (0,0), (0,1),  (1,1) \}$
12. $\{ (0,0), (1,0), (1,1) \}$
13. $\{ (0,0), (0,1), (1,0), (1,1) \}$
