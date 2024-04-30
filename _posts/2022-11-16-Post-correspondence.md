---
layout: post
title: Post's correspondence problem
subtitle: A type of problem that can be attempted at any age
---

A word is a concatenation of $0$ or more letters from a finite alphabet. Consider the alphabet $\{a,b\}$ consisting of the letters $a$ and $b$. Examples of words on this alphabet are $a, b, aab, babaa$ and the _empty word_ $""$, which is often denoted by $\epsilon$. Words can be concatenated. This means putting them one right after the other to form longer words. For example, the concatenation of $aab$ and $bba$ results in the word $aabbba$. The concatenation of the empty word $\epsilon$ and any other word $w$, results on the same word $w$.

**Problem 1:** Assume that we are given two sets of words. The **"top words"**: 
$$t_1=aa, t_2=bb, t_3=abb$$
and the **"bottom words"**:
$$b_1=aab, b_2=ba and b_3=b$$
You can imagine that they come written on dominoes, like
$$\binom{t_1}{b_1}=\binom{aa}{aab}, \binom{t_2}{b_2}=\binom{bb}{ba}, \binom{t_3}{b_3}=\binom{abb}{b}$$
Find a sequence $i_1,i_2,\ldots, i_n\in\{1,2,3\}$, with $n>0$ such that the concatenation of the top words and the concatenation of the bottom words are the same: $t_{i_1}t_{i_2}\ldots  t_{i_n}=b_{i_1}b_{i_2}\ldots b_{i_n}$.
Another way of saying this is a sequence of one or more copies of those three dominoes, such that when putting them one next to the other, the word written concatenating all the tops of the dominoes is the same as the word written concatenating the bottoms. For example, if we put $\binom{t_1}{b_1}$ followed by $\binom{t_3}{b_3}$, we get $\binom{aa}{aab}\binom{abb}{b}$ or $\binom{aaabb}{aabb}$. In this case the resulting top and bottom words are not the same. You need to find a way to make them the equal.

**Problem 2:**  Assume that we have the following _top words_ $t_1=aa$, $t_2=ba$, $t_3=aba$, and the _bottom words_  $b_1=b$, $b_2=baa$, $b_3=a$. Show that this time, there is no choice of the tuple $i_1,i_2,\ldots i_n\in\{1,2,3\}$, with $$n>0$$, such that $t_{i_1}t_{i_2}\ldots  t_{i_n}=b_{i_1}b_{i_2}\ldots b_{i_n}$.

These two are not difficult, but part of the beauty of this problem is that changing the given top and bottom words the problem can be made as difficult as you want. The reason for this is that the sequences of top and bottom words can be made to encode the running of any program on any computer, in such a way that the cases in which there is a solution correspond to the programs and inputs that don't run forever.
