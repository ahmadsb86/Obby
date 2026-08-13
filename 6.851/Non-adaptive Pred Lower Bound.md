# 2 Non-Adaptive Lower Bound for  
 _If $n < w/2$, then we have_

$$\max(t_q, t_u) = \Omega\left(\frac{n \log m}{w \log w}\right)$$

The proof of Theorem 1 depends on the following technical lemma, whose proof we defer to Subsection 2.1.

> **Lemma 9** (Main Technical Lemma). _Let $C$ be a set of cells in the data structure, and let $A \subseteq [m]$. If_
> 
> 1. $|A| \geq \sqrt{m}$,
> 2. $|C| \leq \frac{\alpha \log m}{5w}$, and
> 3. _for all $i \in A$, $q_i$ probes all cells in $C$,_
> 
> _then there exists $j \in A$ and a subset $A' \subseteq A$ such that $|A'| \geq \frac{|A|}{w^2}$ and for each $i \in A'$ there is a cell $c \notin C$ such that $u_j$ and $q_i$ both probe $c$._

At a high level, this lemma says that if we have a large enough set of queries $A$ and a small enough set of cells $C$ such that each query in $A$ probes each cell in $C$, then there must be an update $u_j$ that has a nontrivial intersection _outside of $C$_ with a large subset of $A$.

**Proof of Theorem 1.** We prove this theorem by induction. Fix an arbitrary non-adaptive data structure for Predecessor. As mentioned in the introduction, we'll prove this theorem by iteratively growing a large set of cells $C$ in the data structure and a not-too-small set of queries $A$ such that each query in $A$ probes each cell in $C$. If we can grow the set of cells until $|C| = \frac{\alpha \log m}{2w \log(w \cdot t_u)}$ while keeping the set of queries nonempty, the theorem will follow.

This intuition is captured by the following inductive claim.

> **Claim 10.** For all integers $1 \leq k \leq \frac{\alpha \log m}{2w \log(w \cdot t_u)}$, there is a set of $k$ cells $C$ and a set queries $A \subseteq [m]$ such that
> 
> 1. $|A| \geq \frac{m}{w^{2(k-1)} t_u^k}$
> 2. $C \subseteq Q_i$ for all $i \in A$.

Setting $k = \frac{\alpha \log m}{2w \log(w \cdot t_u)}$ proves the theorem.

It remains to prove the claim. First, we prove the base case of $k = 1$. Fix an arbitrary update $u_j$, and note that $U_j$ must intersect $Q_i$ for each $i \in [m]$. Otherwise, the contents of the cells queried by $q_i$ would be the same for the empty set and for $T = {j}$, but $\text{Pred}(i) = \perp$ when the set is empty, and $\text{Pred}(i) = j$ when the set is ${j}$. Note also that $|U_j| \leq t_u$, so by the pigeonhole principle, there must be a cell $c \in U_j$ probed by at least $m/t_u$ queries $i \in [m]$. Fix this cell $c$, define $C := {c}$, and let $A$ be the set of queries that probe $c$. This set of cells $C$ and queries $A$ fit the premise of Claim 10, completing the base case.

For the induction hypothesis, assume Claim 10 holds for some arbitrary $k < \frac{\alpha \log m}{2w \log(w \cdot t_u)}$.

In the induction step, we'll show that Claim 10 holds for $k+1$ as well. By the induction hypothesis, there is a set of $k$ cells $C_k$ and queries $A_k$ such that $|A_k| \geq m/(w^{2(k-1)} t_u^k)$ and $C_k \subseteq Q_i$ for all $i \in A$. To invoke Lemma 9, $|A_k|$ must be at least $\sqrt{m}$. This holds as long as $k \lesssim \frac{\log(m)}{2 \log(w^2 t_u)}$, which is valid since $\alpha \leq w/2$.

By Lemma 9, there is an update $j \in A_k$ and subset $A'_k \subset A_k$ such that $|A'_k| \geq |A_k|/w^2$ and for each $i \in A'_k$ there is a cell $c \notin C_k$ such that $u_j$ and $q_i$ both probe $c$. Next, we again use the pigeonhole principle. Since $|U_j \setminus C| \leq |U_j| \leq t_u$, there must be a cell $c \in U_j \setminus C$ and a set $A''_k \subseteq A'_k$ such that $|A''_k| \geq |A'_k|/t_u$ and such that for each $i \in A''_k$, $Q_i$ probes $c$. Set $C_{k+1} := C \cup {c}$ and $A_{k+1} := |A''_k|$. Note that $|A_{k+1}| \geq |A_k|/w^2 t_u$ and that $C_{k+1} \subseteq Q_i$ for all $i \in A_{k+1}$. The sets $C_{k+1}, A_{k+1}$ fit the premise of Claim 10 for $k+1$, completing the induction step. $\blacktriangleleft$

> **Note (on the two cells named $c$ and the pigeonhole step).** This paragraph introduces two *different* cells, both written $c$; the pigeonhole step converts the first into the second.
> 
> **First $c$ — from Lemma 9 (query-dependent).** Read the quantifiers: "for each $i \in A'_k$ there is a cell $c$." The cell is chosen *after* $i$, so it may be a **different cell for every query** $i$. Rename it $c_i$ to make this explicit: for each $i \in A'_k$ there is a cell $c_i$ with $c_i \in U_j$, $c_i \in Q_i$, and $c_i \notin C_k$. This alone is not enough to grow $C$: the invariant of Claim 10 requires *one single cell* probed by *all* surviving queries, but a different cell per query does not provide that.
> 
> **Where these cells live.** Since $u_j$ probes $c_i$ we have $c_i \in U_j$, and $c_i \notin C_k$, so
> 
> $$c_i \in U_j \setminus C_k \quad\text{for every } i \in A'_k.$$
> 
> The number of *distinct* cells available here is small: $|U_j \setminus C_k| \le |U_j| \le t_u$.
> 
> **Second $c$ — from pigeonhole (one fixed cell).** Set up the pigeonhole:
> - **Pigeons:** the queries $i \in A'_k$ (there are $|A'_k|$ of them).
> - **Holes:** the cells of $U_j \setminus C_k$ (at most $t_u$ of them).
> - **Assignment:** put pigeon $i$ into hole $c_i$.
> 
> Distributing $|A'_k|$ pigeons among $\le t_u$ holes, some hole receives at least $|A'_k|/t_u$ pigeons. Call that hole $c$ — a single, now-fixed cell — and let $A''_k$ be the queries assigned to it. Then $|A''_k| \ge |A'_k|/t_u$, and every $i \in A''_k$ has $c_i = c$, so $q_i$ probes the *same* cell $c$.
> 
> **Why this is what we needed.** The pigeonhole step *consolidates* the many query-specific cells $\{c_i\}$ into one cell $c$ that a $1/t_u$ fraction of the queries all probe. Now $C_{k+1} := C_k \cup \{c\}$ satisfies $C_{k+1} \subseteq Q_i$ for all $i \in A_{k+1} := A''_k$, because $C_k \subseteq Q_i$ (induction hypothesis) and $c \in Q_i$ (that is what $A''_k$ guarantees). Since $c \notin C_k$, we get $|C_{k+1}| = k+1$, i.e. genuine growth.
> 
> **Size bookkeeping.** Lemma 9 costs a factor $w^2$ ($|A'_k| \ge |A_k|/w^2$) and the pigeonhole costs a factor $t_u$ ($|A''_k| \ge |A'_k|/t_u$), giving $|A_{k+1}| \ge |A_k|/(w^2 t_u)$ — exactly the $w^{2(k-1)}t_u^k$ denominator in Claim 10.
> 
> *(Typo: the line "$A_{k+1} := |A''_k|$" should read $A_{k+1} := A''_k$ — the set itself, not its size.)*

## 2.1 Proof of Main Technical Lemma

We prove Lemma 9 using an encoding argument—we show that if the lemma is false, then we can use $C$ to encode more than $|C| \cdot w$ bits of information, a contradiction.

Before delving into the technical details of the proof, we introduce some notation. Say that a set of cells $C$ _satisfies_ $(u_j, q_i)$ if $U_j \cap Q_i \subseteq C$; that is, if $C$ contains all cells probed by both $u_j$ and $q_i$. Similarly, for a set $T \subseteq [m]$, say that $C$ satisfies $(T, q_i)$ if $C$ satisfies $(u_j, q_i)$ for all $j \in T$. Lemma 9 states that there is $j \in A$ and a large subset $A' \subseteq A$ (with $|A'| \geq |A|/w^2$) such that for all $i \in A'$, $C$ _fails_ to satisfy $(u_j, q_i)$.

**Proof of Lemma 9.** Towards a contradiction, assume that for all $j \in A$, there are less than $|A|/w^2$ queries $i \in A$ such that the given set of cells $C$ fails to satisfy $(u_j, q_i)$. We'll then use the data structure and $C$ to encode the following set:

$$\mathcal{S} := \left\{ T \subseteq A : |T| = \alpha \text{ and } |j - j'| \geq \frac{|A|}{w} \text{ for all } j, j' \in T \right\}$$

$\mathcal{S}$ is the set of all possible "spread-out" subsets of $A$ with size $\alpha$.

> **Claim 11.** $|\mathcal{S}| \geq 2^{\frac{\alpha \log(m)}{4}}$.

**Proof.** We construct a subset of $\mathcal{S}$ with the desired size. Let $x_1, \ldots, x_\alpha$ be arbitrary elements of ${1, \ldots, |A|/w}$. Set $y_i := \frac{(2i-1)|A|}{w} + x_i$, and set $T := {y_i}$. Note that $y_1 > \frac{|A|}{w}$, $y_\alpha \leq \frac{(2\alpha-1)|A|}{w} + \frac{|A|}{w} = \frac{2\alpha|A|}{w} \leq |A|$, and that by definition of $T$ we have

$$\frac{2i-1}{w}|A| < y_i \leq \frac{2i}{w}|A| = \frac{2(i+1)-1}{w}|A| - \frac{|A|}{w} \leq y_{i+1} - \frac{|A|}{w}$$

This means that $y_{i+1} - y_i \geq \frac{|A|}{w}$ for all $i$, hence $T$ is a valid element of $\mathcal{S}$. There are $\frac{|A|}{w}$ choices for each $x_i$, and $\alpha$ elements of $T$, so there are $(|A|/w)^\alpha$ choices for $T$. Thus, we have

$$|\mathcal{S}| \geq \left(\frac{|A|}{w}\right)^\alpha = 2^{\alpha \log(|A|/w)} \geq 2^{\frac{\alpha}{4}\log(m)}$$

where the final inequality holds because $w \leq m^{1/4}$ and $|A| \geq \sqrt{m}$. $\blacktriangleleft$

**Encoding Procedure.** Given an arbitrary $T \in \mathcal{S}$, the encoder takes the non-adaptive data structure, initially storing an empty set. She then inserts each $j \in T$. After performing all insertions, the encoder sends the contents of each cell in $C$.

**Decoding Procedure.** The decoder first takes the non-adaptive data structure, initialized to store the empty set. Then, she overwrites the contents of each cell in $C$ using the encoder's message. The decoder then executes $q_i$ for each $i \in A$ and outputs the set of all elements that appear at least $\frac{|A|}{2w}$ times as answers; that is, the decoder returns the set $T' := {j \in A : \text{there are at least } \frac{|A|}{2w} \text{ elements } i \text{ with Query(i)} == j}$.

**Analysis.** It is easy to see that the length of the encoding is $w \cdot |C| \leq \frac{\alpha \log(m)}{5}$ bits, since the encoder sends the memory contents of each cell in $C$. Next, we claim that the decoder correctly recovers $T$. By assumption, we have that for all $j \in A$, the set of cells $C$ satisfies $(u_j, q_i)$ for all but at most $\frac{|A|}{w^2}$ queries. Therefore, for any $T \in \mathcal{S}$, $C$ satisfies $(T, q_i)$ for all but at most $\frac{|A|}{w^2}\alpha < \frac{|A|}{2w}$ queries $i \in A$.

Now, consider what happens when $C$ satisfies $(T, q_i)$. For any $j \in T$, $C$ contains all cells probed by both $u_j$ and $q_i$. Since this holds for all $j \in T$, $C$ contains all cells that changed during insertions _that were probed by $q_i$_. Thus the decoder can correctly compute $q_i$ when $C$ satisfies $(T, q_i)$.

When $C$ does not satisfy $(T, q_i)$, then the decoder is not guaranteed to correctly compute $q_i$; we assume without loss of generality that this is an error. The decoder executes query $q_i$ for each $i \in A$, but computes this query incorrectly whenever $C$ does not satisfy $(T, q_i)$. Moreover, since the decoder does not know $T$ in advance, she cannot know a priori which queries failed. We claim that because less than $\frac{|A|}{2w}$ queries are not satisfied, the decoder still has enough information to recover $T$.

To see this, take any $j \in T$. By construction, $|j - j'| \geq \frac{|A|}{w}$ for any $j, j' \in T$. Hence $j$ is the correct answer to query $q_i$ for all $i \in [j, j + \frac{|A|}{w} - 1]$. Even if all errors were in this range, there would still be more than $\frac{|A|}{2w}$ queries for which the decoder correctly computes $j$. Hence, the decoder will place $j \in T'$. Conversely, consider any $j \notin T$. Then, $j$ is not a correct answer for any query. In the worst case, the decoder computes $j$ for each possible query on which she errs. Since there are less than $\frac{|A|}{2w}$ such queries, the decoder will not place $j \in T'$. The decoder adds $j$ to $T'$ if and only if $j \in T$, hence the decoder correctly outputs $T$.

We've shown how to encode an arbitrary $T \in \mathcal{S}$ using $w \cdot |C|$ bits. By Fact 6 and Claim 11, we must have

$$w \cdot |C| \geq \log(|\mathcal{S}|) \geq \frac{\alpha \log m}{4}$$

Therefore, we must have $|C| \geq \frac{\alpha \log(m)}{4w}$, contradicting our assumption that $|C| \leq \frac{\alpha \log m}{5w}$. $\blacktriangleleft$
