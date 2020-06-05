---
layout: post
title: Polya enumeration theorem applied to a foobar
subtitle: Nice combinatorial theorem + implementation
---

{: .box-note}
For positive integers $w$, $h$, $s$ consider the equivalence classes of $w\times h$ matrices, with entries on the set $S=\\{1,2,3,\ldots,s\\}$, identified by arbitrary permutations of the rows and the columns. The goal is to compute the number of those classes.

This is an application of [Polya's enumeration theorem](https://en.wikipedia.org/wiki/P%C3%B3lya_enumeration_theorem). 

Consider the group  $G=S_w\times S_h$, where $S_w$ and $S_h$ are the [symmetric group](https://en.wikipedia.org/wiki/Symmetric_group) of the sets $W=\\{1,2,3,\ldots,w\\}$ and $H=\\{1,2,3,\ldots,h\\}$ with $w$ and $h$ elements, respectively. The group $G$ acts on the set $X=W\times H$, which we view as the set of indexes of the entries of the matrices.

Each matrix is a function $f:X\to S$, and element $f\in S^X$. 

So, the problem consists of computing the cardinality 

$$\|S^X/G\|$$

## Cycle index polynomial of a group of permutations

For a permutation group $G$ acting on a set $X=\\{1,2,3,\ldots,n\\}$ define the polynomial 

$$Z(G,s_1,s_2,s_3,\ldots,s_n)=|G|^{-1}\sum_{g\in G}\prod_{k=1}^{n}s_k^{c_k(g)}$$

where $c_k(g)$ is the number of cycles of length $k$ in the cycle decomposition of the permutation $g$.

Polya's enumeration theorem tell us that 

$$\|S^X/G\|=Z(G,s,s,\ldots,s)=|G|^{-1}\sum_{g\in G}s^{c_k(g)}$$

## Cycle index of the Cartesian product

In our case, $G$ is the Cartesian product $S_w\times S_h$. In [this paper](../assets/files/WeiXuCycleIndexCartesianProduct.pdf) they prove the following formula

$$\require{textcomp}Z(G_1\times G_2,s_1,s_2,\ldots,s_{n_1\cdot n_2}) = Z(G_1,s_1,\ldots,s_{n_1})\otimes Z(G_1,s_1,s_2,\ldots,s_{n_2})$$

where the product $$\otimes$$ (In the paper they use the symbol [text reference mark](https://en.wikipedia.org/wiki/Reference_mark)) of polynomials is defined by:

{: .box-note}
If $f(x_1,x_2,...,x_m)=\sum a_{i_1i_2\ldots i_m}x_1^{i_1}x_2^{i_2}\dotsm x_m^{i_m}$ and $g(x_1,x_2,...,x_n)=\sum b_{j_1j_2\ldots j_n}x_1^{j_1}x_2^{j_2}\dotsm x_n^{j_n}$ then

$$\require{textcomp}f(x_1,x_2,\ldots,x_m)\otimes g(x_1,x_2,\ldots,x_n)=\sum a_{i_1i_2\ldots i_m}b_{j_1j_2\ldots j_n}\times\prod_{\substack{1\leq r\leq m\\1\leq s\leq n}}(x_{r}^{i_l}\otimes x_{s}^{j_s})$$

and 

$$\require{textcomp}x_{r}^{i_l}\otimes x_{s}^{j_s} = x_{\lcm(r,s)}^{\gcd(r,s)i_rj_s}$$

## Cycle index of the symmetric group

For the case of the symmetric group $S_n$ acting on $\\{1,2,3,\ldots,n\\}$ we have 

$$Z(S_n)=\frac{1}{n}\sum_{k=1}^{n}s_kZ(S_{n-k})$$

or explicitly

$$Z(S_n,s_1,s_2,\ldots,s_n)=\sum_{r_1+2r_2+3r_3+\ldots nr_n=n}\frac{s_1^{r_1}s_2^{r_2}\dotsm s_n^{r_n}}{1^{r_1}r_1!2^{r_2}r_2!\dotsm n^{r_n}r_n!}$$
