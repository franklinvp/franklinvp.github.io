In **Cayley 2016, problem 24**, among other things, we had to add all rational numbers between $0$ and $1$ that have denominators not larger than $10$. With denominators so small we can just list them all and add, but let’s look at some of the marvelous interconnected web of ideas related to this problem.

> **Definition:** \[Farey sequence\]. The **Farey sequence of order $n$** (denoted as $F_n$) consists of all rational numbers $0\leq\frac{a}{b}\leq1$, with $\gcd(a,b)=1$ and $0<b\leq n$, and _written in increasing order_.

Here I will only mention very few of the ideas around Farey sequences that are worth knowing at this point. To dig further see also [the Wikipedia article](https://en.wikipedia.org/wiki/Farey_sequence), [this video](https://www.youtube.com/watch?v=uFWJuZQLKJs) regarding rational approximation. Perhaps [this other video](https://www.youtube.com/watch?v=uFWJuZQLKJs). Maybe also [Stern-Brocot tree](https://en.wikipedia.org/wiki/Stern%E2%80%93Brocot_tree).

## Generaring $F_n$ from $F_{n-1}$.

We have that $F_1=(\frac{0}{1}, \frac{1}{1})$. These are all the reduced fractions between $0$ and $1$ with denominators not larger than $1$.

To produce $F_2$ we only need to insert $\frac{1}{2}$ in between. Note that $\frac{1}{2}=\frac{0+1}{1+1}$ is the [mediant](https://en.wikipedia.org/wiki/Mediant_(mathematics)) of $\frac{0}{1}$ and $\frac{1}{1}$. In general, the mediant of the fractions $\frac{a}{b}$ and $\frac{c}{d}$ is the fraction $\frac{a+c}{b+d}$. Note that the name is **mediant**, not median. Median is a different concept.

> **Exercise:** Prove that if $\frac{a}{b}\leq\frac{c}{d}$, then their mediant is always in between these two fractions. That is $\frac{a}{b}\leq \frac{a+c}{b+d}\leq\frac{c}{d}$.

In general, to obtain $F_n$ from $F_{n-1}$ we insert all mediants of the pairs of consecutive elements of $F_{n-1}$ that produce denominators $n$.

For example, we have $F_3=(\frac{0}{1},\frac{1}{3},\frac{1}{2},\frac{2}{3},\frac{1}{1})$, to get $F_4$ we insert $\frac{0+1}{1+3}=\frac{1}{4}$ between $\frac{0}{1}$ and $\frac{1}{3}$, and insert $\frac{2+1}{3+1}=\frac{3}{4}$ between $\frac{2}{3}$ and $\frac{1}{1}$. We don’t insert the mediant $\frac{1+1}{3+2}=\frac{2}{5}$ of $\frac{1}{3}$ and $\frac{1}{2}$, yet, because that has denominator $5$. We leave that one to insert when building $F_5$.

Do practice at least once constructing a few of the Farey sequences. You could go all the way to $F_{10}$, which are the fractions that we needed to sum in the homework.

## Consecutive terms in a Farey sequence.

If $\frac{a}{b}<\frac{c}{d}$ are two consecutive terms in a Farey sequence, then $\det\begin{pmatrix}c&a\d&b\end{pmatrix}=cb-ad=1$.

Verify some examples. For example, $F_4=(\frac{0}{1},\frac{1}{4},\frac{1}{3},\frac{1}{2},\frac{2}{3},\frac{3}{4},\frac{1}{1})$. If we take, say, $\frac{1}{2}<\frac{2}{3}$, that are two consecutive terms, then $2\cdot 2-1\cdot 3=1$.

> **Exercise:** Prove this property in general. **Hint:** Do induction on $n$. Assume that the property is true for the sequence $F_{n-1}$, take two consecutive terms in it $\frac{a}{b}<\frac{c}{d}$, assume by induction that they satisfy $cb-ad=1$. Then consider their mediant $\frac{a+c}{b+d}$ and assume that this is a fraction in $F_n$. So, $b+d=n$. Prove that $\frac{a}{b}<\frac{a+c}{b+d}$ satisfy the property of that determinant being $1$, and also $\frac{a+c}{b+d}<\frac{c}{d}$ also satisfy the property.

This property is in fact an _if and only if_ condition. This is, if two reduced fractions $0\leq\frac{a}{b}<\frac{c}{d}\leq1$ satisfy $cb-ad=1$, then they appear as consecutive fractions in the Farey sequence of order $\max(b,d)$. \[This would be the first Farey sequence that contains both of these fractions\].

> **Exercise:** If you compute the **continued fraction** of $\sqrt{7}$, it results in $2+\frac{1}{1+\frac{1}{1+\frac{1}{1+\frac{1}{4+\frac{1}{\ddots}}}}}$ and the pattern $1,1,1,4$ repeats periodically. Do the following now. Truncate the continued fraction at two consecutive places and compute the fractions that you get. For example, remove everything after the third $1$ and compute resulting fraction. Then remove everything after the first $4$ and compute the resulting fraction. You could choose any two consecutive places to truncate. Say that you got the fractions $\frac{a}{b}<\frac{c}{d}$. Check that $cb-ad=1$. That means that the truncations of continued fractions are consecutive terms in some Farey sequence. 

## Number of elements in $F_n$

The number of elements of $F_1$ is $|F_1|=2$. Which fractions get inserted when we go from $F_{n-1}$ to $F_n$? Well, all reduced fractions with denominator $n$. How many of those are there? Well, one for each numerator between $1$ and $n$ that are relatively prime to $n$. Remember one of the definitions of [Euler’s totient function](https://en.wikipedia.org/wiki/Euler%27s_totient_function) $\phi(n)$. Yes, the same function that appeared in Euler’s theorem. We mentioned that $\phi(n)$ is the number of integers between $1$ and $n$ that are relatively prime to $n$. So, that means that $|F_n|=|F_{n-1}|+\phi(n)$.

From this we can deduce that

$|F_n|=1+\phi(1)+\phi(2)+\phi(3)+...+\phi(n)$

## Sum of the elements of $F_n$

As some of you noticed when adding the elements of $F_{10}$, the fractions in $F_n$ appear in pairs that add up to $1$. In fact, if $\frac{a}{b}\in F_n$, then $\gcd(a,b)=1$. Therefore, the fraction $\frac{b-a}{b}$ also satisfies $\gcd(b-a,b)=1$. This means that $\frac{b-a}{b}\in F_n$. Adding these two fractions we get $\frac{a}{b}+\frac{b-a}{b}=1$.

This observation tells us that if we take the sum of all elements of $F_n$ twice, we add a $1$ for each element of $F_n$. That is, the total is the same as the number of elements $|F_n|$. So,

$2\sum_{r\in F_n}r=|F_n|$

## Application

We needed to add all reduced fractions between $23$ and $24$ with denominators not larger than $10$. If we take out $23$ from each of those fractions, we would need to add all elements of $F_{10}$ and $23$ times $|F_{10}|$. According to the properties above, that would be $\frac{1}{2}|F_{10}|+23|F_{10}|$, where $|F_{10}|=1+\phi(1)+\phi(2)+...+\phi(10)$.

Well, strictly speaking, in the problem the fractions were supposed to be strictly greater than $23$. So, I guess we must subtract this $23$, or only add $23(|F_{10}|-1)$.

Do finish the exercise with these ideas, and in particular practice computing $\phi(1),\phi(2),...\phi(10)$. Note that with these ideas, we could solve the same problem if they had made it more difficult by allowing the denominators go to larger values. Who knows, what if it was the same problem but the denominators are allowed to go all the way up to $100$ or up to $2023$?
