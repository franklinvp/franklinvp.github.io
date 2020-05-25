---
layout: post
title: Number tomography
subtitle: A cute problem that my students got in a competition
---

This problem has appeared in many math competitions. It is quite interesting and connects to a lot of interesting mathematics.

{: .box-note}
For a collection (multiset) of numbers $A=\{\{a_1\leq a_2\leq\ldots\leq a_n\}\}$ one can compute the multiset of all the pairwise sums $a_i+a_j$ with $i\neq j$ of its elements $S=\{\{s_1\leq s_2\leq\ldots\leq s_m\}\}$, with $m=\frac{n(n-1)}{2}$. The main question is whether one can uniquely recover the multiset $A$ from the multiset $S$.

**Answer:** When $n$ is not a power of $2$, then one can uniquely recover $A$ from $S$. If $n$ is a power of $2$, then it is possible to have multiple solutions.

Proof:

