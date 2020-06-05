---
layout: post
title: Polya enumeration theorem applied to a foobar
subtitle: Nice combinatorial theorem + implementation
---

{: .box-note}
For positive integers $w$, $h$, $s$ consider the equivalence classes of $w\times h$ matrices, with entries on the set $S=\{1,2,3,\ldots,s\}$, identified by arbitrary permutations of the rows and the columns. The goal is to compute the number of those classes.

This is an application of [Polya's enumeration theorem](https://en.wikipedia.org/wiki/P%C3%B3lya_enumeration_theorem). 

Consider the group  $G=S_w\times S_h$, where $S_w$ and $S_h$ are the [symmetric group](https://en.wikipedia.org/wiki/Symmetric_group) of the sets $W=\\{1,2,3,\ldots,w\\}$ and $H=\\{1,2,3,\ldots,h\\}$ with $w$ and $h$ elements, respectively. The group $G$ acts on the set $X=W\times H$, which we view as the set of indexes of the entries of the matrices.

Each matrix is a function $f:X\to S$, and element $f\in S^X$. 

So, the problem consists of computing the cardinality $$\\|S^X/G\\|$$


==Cycle index polynomial of a group of permutations

For a permutation group $G$ acting on a set $X=\\{1,2,3,\ldots,n\\}$ define the polynomial 

$$Z(G,s_1,s_2,s_3,\ldots,s_n)=|G|^{-1}\sum_{g\in G}\prod_{k=1}^{n}s_k^{c_k(g)}$$

where $c_k(g)$ is the number of cycles of length $k$ in the cycle decomposition of the permutation $g$.


