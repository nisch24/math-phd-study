---
layout: default
title: "0.1 — Proofs, Logic & Sets"
parent: "Module 0 — Foundations"
nav_order: 1
permalink: /module_0/proofs/
---

# 0.1 — Proofs, Logic &amp; Sets

> *A proof is an argument that holds up against an adversary. This course teaches the logical grammar of mathematics (quantifiers, implications, sets, and functions) and the handful of proof techniques that every later course uses.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Read and negate quantified statements** mechanically and correctly, including nested $\forall\exists$ statements.
2. **Choose and execute a proof technique**: direct proof, contrapositive, contradiction, induction, or counterexample.
3. **Work with functions as set maps**: images, preimages, injectivity, surjectivity, and composition.
4. **Compare the sizes of infinite sets** using bijections, and prove that $\mathbb{Q}$ is countable while $\mathbb{R}$ is not.

---

## Core Theory

### Unit 1: Logic and Quantifiers

#### 1.1 Implications

A statement $P \Rightarrow Q$ is false only when $P$ is true and $Q$ is false.

| Form | Statement | Equivalent to $P \Rightarrow Q$? |
|------|-----------|-------------------------------|
| Contrapositive | $\neg Q \Rightarrow \neg P$ | **Yes**, always |
| Converse | $Q \Rightarrow P$ | No |
| Inverse | $\neg P \Rightarrow \neg Q$ | No (it is equivalent to the converse) |

**Intuition**: "If it is raining, the ground is wet" has the contrapositive "if the ground is dry, it is not raining", which says the same thing. Its converse, "if the ground is wet, it is raining", fails for sprinklers.

#### 1.2 Quantifiers and Negation

The negation rules are:

$$\neg(\forall x\; P(x)) \equiv \exists x\; \neg P(x), \qquad \neg(\exists x\; P(x)) \equiv \forall x\; \neg P(x).$$

To negate a nested statement, move left to right, flipping each quantifier and finally negating the inner condition.

**Worked example (the most important one in analysis).** "$a_n \to L$" means

$$\forall \varepsilon > 0\;\; \exists N\;\; \forall n \geq N: \quad |a_n - L| < \varepsilon.$$

Its negation, "$a_n \not\to L$", is

$$\exists \varepsilon > 0\;\; \forall N\;\; \exists n \geq N: \quad |a_n - L| \geq \varepsilon.$$

**Intuition — the game**: a quantified statement is a game between you ($\exists$) and an adversary ($\forall$). To prove convergence, you must answer *any* tolerance $\varepsilon$ the adversary names with a cutoff $N$ that works. To disprove it, *you* get to name one bad $\varepsilon$, and must then beat any $N$ the adversary proposes. **Order matters**: $\forall x\, \exists y$ lets $y$ depend on $x$; $\exists y\, \forall x$ demands one $y$ for all $x$. The difference between continuity and uniform continuity is exactly this swap.

---

### Unit 2: Proof Techniques

#### 2.1 Direct Proof
Assume the hypothesis, then chain known facts to reach the conclusion. *Example*: if $a$ and $b$ are odd, then $ab$ is odd. Write $a = 2k+1$, $b = 2m+1$; then $ab = 2(2km + k + m) + 1$.

#### 2.2 Contrapositive
Prove $\neg Q \Rightarrow \neg P$ instead. Use it when the negated conclusion gives you something concrete to work with. *Example*: if $n^2$ is even then $n$ is even. Contrapositive: if $n$ is odd, then $n^2$ is odd (by 2.1).

#### 2.3 Contradiction
Assume the conclusion is false and derive something impossible.

**Theorem**: $\sqrt{2}$ is irrational.
*Proof*: Suppose $\sqrt{2} = p/q$ in lowest terms. Then $p^2 = 2q^2$, so $p^2$ is even, so $p$ is even (2.2). Write $p = 2r$: then $4r^2 = 2q^2$, so $q^2 = 2r^2$ and $q$ is even too. This contradicts lowest terms.

#### 2.4 Induction
To prove $P(n)$ for all $n \geq 1$: prove $P(1)$, and prove $P(k) \Rightarrow P(k+1)$ for every $k$. **Strong induction** assumes $P(1), \ldots, P(k)$ in the inductive step. Both are equivalent to the **well-ordering principle**: every nonempty set of positive integers has a least element.

**Intuition**: induction is a row of dominoes. The base case knocks over the first one; the inductive step guarantees each one knocks over the next. A common bug is an inductive step that silently fails for one value of $k$. In the classic "all horses are the same color" fallacy, the step fails from $k=1$ to $k=2$ because the two overlapping groups of horses don't actually overlap.

#### 2.5 Counterexamples
To disprove "$\forall x\, P(x)$", exhibit one $x$ with $\neg P(x)$. A good counterexample is the simplest one: try $0$, $1$, $-1$, the empty set, a constant function, $\mathbb{Q}$, or $x^2$ first.

---

### Unit 3: Sets and Functions

#### 3.1 Images and Preimages

For $f: X \to Y$, $A \subseteq X$, $B \subseteq Y$:
- Image: $f(A) = \{f(a) : a \in A\}$. Preimage: $f^{-1}(B) = \{x \in X : f(x) \in B\}$. (The preimage is defined whether or not $f$ is invertible.)

**Theorem**: Preimages preserve **all** set operations:

$$f^{-1}\Big(\bigcup_\alpha B_\alpha\Big) = \bigcup_\alpha f^{-1}(B_\alpha), \quad f^{-1}\Big(\bigcap_\alpha B_\alpha\Big) = \bigcap_\alpha f^{-1}(B_\alpha), \quad f^{-1}(B^c) = f^{-1}(B)^c.$$

Images preserve unions but **not** intersections or complements in general: $f(A_1 \cap A_2) \subseteq f(A_1) \cap f(A_2)$, with equality when $f$ is injective.

**Why this matters later**: continuity ("preimages of open sets are open") and measurability ("preimages of Borel sets are measurable") are both defined through preimages, precisely because preimages behave so well.

#### 3.2 Injective, Surjective, Bijective
- **Injective**: $f(x_1) = f(x_2) \Rightarrow x_1 = x_2$. **Surjective**: every $y \in Y$ is some $f(x)$. **Bijective**: both, equivalently $f$ has a two-sided inverse.
- Compositions of injections are injections; if $g \circ f$ is injective then $f$ is injective; if $g \circ f$ is surjective then $g$ is surjective.

#### 3.3 Equivalence Relations
A relation $\sim$ that is reflexive, symmetric, and transitive partitions its set into disjoint **equivalence classes**, and every partition arises this way. *Examples*: congruence mod $n$; "differ by a rational number" on $\mathbb{R}$, which is the relation behind the non-measurable Vitali set.

---

### Unit 4: Cardinality

Two sets have the **same cardinality** if there is a bijection between them. A set is **countable** if it is finite or in bijection with $\mathbb{N}$.

**Theorems**:
1. A countable union of countable sets is countable. Hence $\mathbb{Z}$ and $\mathbb{Q}$ are countable (list fractions $p/q$ by increasing $|p| + q$).
2. **(Cantor)** $\mathbb{R}$ is uncountable. *Diagonal argument*: given any list $x_1, x_2, \ldots$ of numbers in $(0,1)$, build $y$ whose $n$-th decimal digit differs from that of $x_n$ (choosing digits from $\{4, 5\}$ avoids the $0.0999\ldots = 0.1$ ambiguity). Then $y$ is missing from the list.
3. **(Cantor–Schröder–Bernstein)** If there are injections $A \to B$ and $B \to A$, then there is a bijection $A \to B$.

**Intuition**: countable sets are "listable". The rationals are dense, but they can still be listed. This explains why, later on, a countable set has Lebesgue measure zero while every interval has positive length.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *How to Prove It* (3rd ed.) | Daniel J. Velleman | **Primary** — The best book for learning proof technique from scratch |
| [*Book of Proof*](https://richardhammack.github.io/BookOfProof/) (3rd ed.) | Richard Hammack | **Free alternative** — Clear, with many exercises and some solutions |
| *Mathematics for Computer Science* | Lehman, Leighton &amp; Meyer | **Supplementary** — Free MIT 6.042J text; ideal for CS backgrounds |
| *Understanding Analysis* (2nd ed.), Ch. 1 | Stephen Abbott | **Bridge** — Applies these techniques to the real numbers |

---

## Problem Sets

### Problem Set 1: Logic

1. **(Core)** Write the negation of each statement without using "not" in front of a quantifier: (a) $f$ is bounded on $\mathbb{R}$; (b) $f$ is continuous at $x_0$; (c) $f$ is uniformly continuous on $\mathbb{R}$; (d) every Cauchy sequence in $X$ converges.
2. **(Core)** Decide whether each is true over $\mathbb{R}$: (a) $\forall x\, \exists y: y > x^2$; (b) $\exists y\, \forall x: y > x^2$. Explain the difference in terms of the game.
3. **(Core)** Show that $P \Rightarrow Q$ is logically equivalent to $\neg P \vee Q$ using a truth table.
4. **(Core)** Prove: an integer $n$ is odd if and only if $n^2$ is odd.
5. **(Challenge)** Prove that $\sqrt{3}$ is irrational, then find exactly where the same argument breaks down for $\sqrt{4}$.

### Problem Set 2: Induction and Proof Techniques

1. **(Core)** Prove $\sum_{k=1}^n k^3 = \left(\frac{n(n+1)}{2}\right)^2$.
2. **(Core)** Prove Bernoulli's inequality: $(1 + x)^n \geq 1 + nx$ for all $x \geq -1$ and integers $n \geq 1$.
3. **(Core)** Use strong induction to prove that every integer $n \geq 2$ is a product of primes.
4. **(Core)** Find the error in this "proof" that all horses are the same color: *In any group of $k+1$ horses, remove one; the remaining $k$ share a color. Remove a different one; those $k$ also share a color. The groups overlap, so all $k+1$ share a color.*
5. **(Challenge)** Prove there are infinitely many primes. Then prove there are arbitrarily long gaps between consecutive primes. *(Hint: $(n+1)! + 2, \ldots, (n+1)! + (n+1)$.)*

### Problem Set 3: Functions and Cardinality

1. **(Core)** Prove $f^{-1}(B_1 \cap B_2) = f^{-1}(B_1) \cap f^{-1}(B_2)$, then show by example that $f(A_1 \cap A_2) \neq f(A_1) \cap f(A_2)$ is possible.
2. **(Core)** Prove: if $g \circ f$ is injective, then $f$ is injective. Must $g$ be injective?
3. **(Core)** Construct an explicit bijection between $(0, 1)$ and $\mathbb{R}$, and between $[0,1]$ and $(0,1)$.
4. **(Proof)** Prove that $\mathbb{N} \times \mathbb{N}$ is countable, and deduce that a countable union of countable sets is countable.
5. **(Challenge)** Prove Cantor's theorem: for any set $X$, there is no surjection $X \to \mathcal{P}(X)$. *(Hint: consider $\{x \in X : x \notin f(x)\}$.)*

---

## Study Guide

{: .important }
> **What you must be able to do on demand**
>
> - Negate any $\forall\exists\forall$ statement correctly in under a minute
> - Recognize which technique a statement invites: a "for all $n$" statement suggests induction; a "not" or "irrational" statement suggests contradiction
> - Prove $\sqrt{2} \notin \mathbb{Q}$, the countability of $\mathbb{Q}$, and the uncountability of $\mathbb{R}$ from memory
> - Manipulate preimages fluently; measure theory and topology are built on them

**Writing tips**:
- State what you are proving and which technique you'll use: "We argue by contradiction. Suppose…"
- Introduce every variable before using it ("Let $\varepsilon > 0$ be arbitrary").
- End with a sentence that restates the conclusion. The reader should never have to reconstruct where the proof ended up.
