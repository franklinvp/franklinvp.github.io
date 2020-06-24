---
layout: post
title: Number tomography
subtitle: A cute problem that my students got in a competition
---

This problem has appeared in many math competitions. It is quite interesting and connects to a lot of interesting mathematics.

{: .box-note}
For a collection (multiset) of numbers $A=\\{\\{a_1\leq a_2\leq\ldots\leq a_n\\}\\}$ one can compute the multiset of all the pairwise sums $a_i+a_j$ with $i\neq j$ of its elements $S=\\{\\{s_1\leq s_2\leq\ldots\leq s_m\\}\\}$, with $m=\frac{n(n-1)}{2}$. The main question is whether one can uniquely recover the multiset $A$ from the multiset $S$.

The process of obtaining $S$ from $A$ is like a tomography. For any choice of *direction* $i,j$, the *superposition* $a_i+a_j$ of the multiset $A$ along this direction is computed. The problem consists in reconstructing the original multiset $A$ from its *tomography* $S$. See, [Radon transform](https://en.wikipedia.org/wiki/Radon_transform) and [X-ray transform](https://en.wikipedia.org/wiki/X-ray_transform) for reconstruction problems that are similar in spirit.

**Claim 1:**  
When $n$ is not a power of $2$, then one can uniquely recover $A$ from $S$.

**Proof of claim 1 [Symmetric polynomials]:**[^1]

Assume that $n$ is not a perfect power of $2$. Denote

$$
\begin{align}
P_{k} &= \sum_{i=1}^{m}s_i^k\\
p_k&=\sum_{i=1}^{n}a_i^k
\end{align}
$$

for $k=1,2,3,\ldots$ These are the [power-sum symmetric polynomials](https://en.wikipedia.org/wiki/Power_sum_symmetric_polynomial) in the variables $s_i$ and $a_i$, respectively.

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


**Proof of claim 1 [Generating polynomials]:**[^2]

Assume that $n$ that $B=\\{\\{b_1,b_2,\ldots,b_n\\}\\}$ is another multiset producing the same multiset of pairwise sums $S$. Define 

$$
\begin{align}
f(x)&=x^{a_1}+x^{a_2}+\ldots+ x^{a_n}\\
g(x)&=x^{b_1}+x^{b_2}+\ldots+ x^{b_n}
\end{align}
$$

The condition on the pairwise sums implies that 

$$
\begin{align}
f^2(x)-g^2(x)&=\left(\sum_{i=1}^{n}x^{2a_i}+2\sum_{1\leq i<j\leq n}x^{a_i+a_j}\right)-\left(\sum_{i=1}^{n}x^{2b_i}+2\sum_{1\leq i<j\leq n}x^{b_i+b_j}\right)\\
&=f(x^2)-g(x^2)
\end{align}
$$

Since $f(1)=g(1)=n$, then $x=1$ is a root of $f-g$. Observe that $f-g$ is a nonzero polynomial because $a_1,a_2,\ldots,a_n$ and $b_1,b_2,\ldots,b_n$ are distinct sequences. Let $f(x)-g(x)=(x-1)^kh(x)$, for $k\geq 1$ and $h(1)\neq0$. Then

$$
\begin{align}
f(x)+g(x)&=\frac{f^2(x)-g^2(x)}{f(x)-g(x)}\\
&=\frac{f(x^2)-g(x^2)}{f(x)-g(x)}\\
&=\frac{(x^2-1)h(x^2)}{(x-1)^kh(x)}\\
&=(x+1)^k\frac{h(x^2)}{h(x)}
\end{align}
$$

Setting $x=1$ we get that 

$$
2n=f(1)+g(1)=(1+1)^k\frac{h(1^2)}{h(1)}=2^k
$$

Therefore, $n$ must be a power of $2$.

**Claim 2:**  
For $n=2^k$, there are multisets $S=\\{\\{s_1,s_2,\ldots,s_{m}\\}\\}$, with $m=\frac{n(n-1)}{2}$ that are the pairwise sums of more than one multiset $A=\\{\\{a_1,a_2,\ldots,a_n\\}\\}$.

**Proof of Claim 2 [Doubling the size of the example]**[^1]

Assume that the two multisets $\\{\\{x_1,x_2,...,x_n\\}\\}$ and $\\{\\{y_1,y_2,\ldots,y_n\\}\\}$ produce the same multiset of pairwise sums $S$. Let $a\neq0$. Then the multisets 

$$
\begin{align}
X'&=\{\{x_1,x_2,...,x_n,y_1+a,y_2+a,\ldots,y_n+a\}\}\\
Y'&=\{\{x_1+a,x_2+a,\ldots,x_n+a,y_1,y_2,\ldots,y_n\}\}
\end{align}
$$

produce the same multiset of pairwise sums.

Applying this transformation to a small example, like $X=\\{\\{1,4\\}\\}$, $Y=\\{\\{2,3\\}\\}$, we can double its size multiple times and obtain examples with size any power of $2$.

**Proof of Claim 2 [Thue-Morse sequence]:**  
The [Thue-Morse sequence](https://en.wikipedia.org/wiki/Thue%E2%80%93Morse_sequence) is obtained by the following procedure: 

We start with $0$ as its first element. At every step we repeat the elements of the sequence that have been generated so far, but replace each occurrence of $0$ with a $1$ and each occurrence of $1$ with a $0$. In the first 3 steps we obtain

  * $0$
  * $0,1$
  * $0,1,1,0$
  * $0,1,1,0,1,0,0,1$

If $n=2^k$, for some integer $k$, we can write the numbers $0,1,2,\ldots,2^{k+1}-1$ above the elements of the Thue-Morse sequence. Let $A$ be the set of all numbers above a $0$ from the Thue-Morse sequence and $B$ the set of those above a $1$. The sets $A$ and $B$ are each of size $2^k$ and have the property of producing the same multiset of pairwise sums.

A [presentation](../assets/files/Talk.pdf) for my young students.

[^1]: Selfridge and Straus, *On the determination of numbers by their sums of a fixed order*, 1958.  
[^2]: Andreescu and Savchev, *Mathematical Miniatures*, 2003.
