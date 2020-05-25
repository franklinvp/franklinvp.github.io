---
layout: post
title: Number tomography
subtitle: A cute problem that my students got in a competition
---

This problem has appeared in many math competitions. It is quite interesting and connects to a lot of interesting mathematics.

{: .box-note}
For a collection (multiset) of numbers $A=\\{\\{a_1\leq a_2\leq\ldots\leq a_n\\}\\}$ one can compute the multiset of all the pairwise sums $a_i+a_j$ with $i\neq j$ of its elements $S=\\{s_1\leq s_2\leq\ldots\leq s_m\\}$, with $m=\frac{n(n-1)}{2}$. The main question is whether one can uniquely recover the multiset $A$ from the multiset $S$.

**Claim 1:**  
When $n$ is not a power of $2$, then one can uniquely recover $A$ from $S$.

**Proof of claim 1 [Symmetric polynomials]:**  
Assume that $n$ is not a perfect power of $2$. Denote

$$
\begin{align}
P_{k} &= \sum_{i=1}^{m}s_i^k\\
p_k&=\sum_{i=1}^{n}a_i^k
\end{align}
$$

for $k=1,2,3,\ldots$ 

Observe that the $s_i$ uniquely determine the $P_k$ and the $p_k$ uniquely determine the [elementary symmetric polynomials](https://en.wikipedia.org/wiki/Elementary_symmetric_polynomial) in the $a_i$ via [Girard-Newton formulae](https://en.wikipedia.org/wiki/Newton%27s_identities). In turn, the *elementary symmetric polynomials* in the $a_i$ uniquely determine these via [Vieta's formulas](https://en.wikipedia.org/wiki/Vieta%27s_formulas).

If we show that the $P_k$, $k=1,2,3,\ldots$, uniquely determine the $p_k$, then we are done.

$$
\begin{align}
P_k&=\sum_{i=1}^{m}s_i^k\\
&=\sum_{1\leq i<j\leq n}(a_i+a_j)^k\\
&=\frac{1}{2}\sum_{\substack{i,j=1\\i\neq j}}^{n}(a_i+a_j)^k\\
&=\frac{1}{2}\left(\sum_{i,j=1}^{n}(a_i+a_j)^k-\sum_{i=1}^{n}(2a_i)^k\right)\\
&=\frac{1}{2}\left(\sum_{i=0}^{k}\binom{k}{i}p_ip_{k-i}-2^kp_k\right)\\
&=\frac{1}{2}\left(2n-2^k\right)p_k - \frac{1}{2}\sum_{i=1}^{k-1}\binom{k}{i}p_ip_{k-i}
\end{align}
$$

these equations, for $k=1,2,3,\ldots$ determine $p_k$ from $P_k$ and the $p_i$, for $1\leq i\leq k-1$ since the coefficients $2n-2^k$ are never zero.



