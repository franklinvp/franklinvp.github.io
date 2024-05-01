[Euclid 2011, Problem 9](https://www.cemc.uwaterloo.ca/contests/past_contests.html). In this problem they gave us:

> Two functions on the positive integers $\mathbb{Z}\_{>0}$
>
>$$\begin{align*}f(n)&=2n-\left\lfloor\frac{1+\sqrt{8n-7}}{2}\right\rfloor\\g(n)&=2n+\left\lfloor\frac{1+\sqrt{8n-7}}{2}\right\rfloor \end{align*}$$
>
>and we need to prove that their ranges are two infinite sets that are disjoint and their union are all of $\mathbb{Z}_{>0}$, in other words their ranges are a partition of the positive integers into two infinite sets.

This problem can be solved by completely determining the ranges of $f$ and $g$. This is, finding for which $m$ the equation $f(n)=m$ has solutions, and for which $m$ the equation $g(n)=m$ has solutions. Note that a floor $\left\lfloor x\right\rfloor$ is equivalent to a pair of inequalities $\left\lfloor x\right\rfloor \leq x<\left\lfloor x\right\rfloor+1$. So, each of these equations is just a system of two inequalities in disguise. The proposed solution attacked the problem this way.

This type of problem (pairs of infinite sets partitioning the positive integers, or also the natural numbers) has been studied and completely characterized in terms of the functions that enumerate them. That is what **Lambek-Moser theorem** does. As often happens, you can choose to only remember the statement of the theorem, but I highly recommend studying and learning the technique in the proof below.

Before stating the theorem, proving it and using it to solve Euclid 2011 Problem 9, let’s mention another similar classical problem that you might have seen.

> **Exercise 1:** (**Beatty sequence** or **Rayleigh’s theorem**) Assume that $r,s$ are two irrational numbers such that $\frac{1}{r}+\frac{1}{s}=1$. Show that the sets $\left\lbrace\left\lfloor rn\right\rfloor:\ n\in\mathbb{Z}\_{>0}\right\rbrace$ and $\left\lbrace\left\lfloor sn\right\rfloor:\ n\in\mathbb{Z}\_{>0}\right\rbrace$ are two infinite sets that partition $\mathbb{Z}\_{>0}$. Actually, the converse is also true. If these two sets are infinite and form a partition of $\mathbb{Z}\_{>0}$, then $r,s$ are irrational and $\frac{1}{r}+\frac{1}{s}=1$.

> **Exercise 2:** The function $F(n)=n^2$, for $n=0,1,2,3,...$ enumerates the perfect squares. Find a formula to enumerate the non-perfect squares using only algebraic operations and the floor function.

I am going to state the theorem speaking of the natural numbers $\mathbb{N}={0,1,2,\ldots}$, for my convenience. Adding $1$ where appropriate, we get similar statements for the positive integers $\mathbb{Z}\_{>0}$.

> **Definition:** A pair of functions $f,g:\mathbb{N}\to\mathbb{N}$ is called a Galois connection on $\mathbb{N}$ when they are monotonic (non-decreasing) and for all $m,n\in\mathbb{N}$ we have

$$f(n)\leq m\iff n\leq g(m)\qquad\qquad\qquad\qquad(*)$$

**Note:** Never mind the name _Galois connection_. It comes from $(\*)$ being a property that appears in, among many other places, in an area of study called Galois Theory. You don’t even need to remember this name for now. The name might sound fancy, but the property is very simple. two simple-looking inequalities that we can jump from one to another. Now, what we do need to notice, to have a mature understanding of why $(\*)$ must be an interesting property to study, is how $(\*)$ is allowing us to make the $f$ jump to the other side of an inequality. Of course, it jumps as the function $g$. Where have we seen something like that? Well, if instead of inequalities we had equations, that is what inverse functions do: $f$ and $g$ are inverses when $f(n)=m\iff n=g(m)$. So, property $(\*)$ is kind of "being inverses”, but in the world of inequalities.

> **Lambek-Moser Theorem:** $f,g:\mathbb{N}\to\mathbb{N}$ are a Galois connection on $\mathbb{N}$, if and only if the sets $$A=\{f(n)+n:\ n\in\mathbb{N}\}\qquad\text{ and }\qquad B=\{g(m)+m+1:\ m\in\mathbb{N}\}$$ are infinite and partition $\mathbb{N}$. This is, are disjoint and their union is $\mathbb{N}$.

**Proof:** Let’s start with the “only if” direction, which is the most interesting for us, to solve Problem 9 of Euclid 2011. So, we assume that $f,g$ are a Galois connection and prove that $A,B$ partition $\mathbb{N}$.

Proving that $A,B$ are disjoint: For every $m,n\in\mathbb{N}$, let $N=m+n$. Now, either $f(m)+m\leq N$ or $f(m)+m>N$. We will prove that in both cases $f(m)+m$ and $g(n)+n+1$ are different numbers. If $f(m)+m\leq N$, then $f(m)\leq n$. By (*) we get from this that $m\leq g(n)$. From this $N=n+m\leq g(n)+n<g(n)+n+1$. So, $f(m)+m\leq N < g(n)+n+1$ are different. In the other case, if $f(m)+m>N$, then $f(m)>n$. By the contrapositive of (*) we get that $m>g(n)$. Therefore $N=n+m>g(n)+n$. And from this $N\geq g(n)+n+1$. So, $f(m)+m>N\geq g(n)+n+1$ are different. Pretty, eh?

Proving that the union of $A,B$ is all of $\mathbb{N}$: For each $k\in{0,1,2,...,N}$ we have $f(k)+k\leq N$ or $g(k)+k+1\leq N$, but not both (as we saw in the previous paragraph). So, if we collect the values of $f(k)+k$ and $g(k)+k+1$ that are in ${0,1,2,...,N}$, those are $N+1$ different values. So, they must be all of ${0,1,2,...,N}$, which only contains $N+1$ values.

For completeness, lets prove the “if” direction. So, now we assume that $A=\{a_0<a_1<a_2<...\}, B=\{b_0<b_1<b_2<...\}$ are infinite and partition $\mathbb{N}$. Assume that $A$ is the one that contains $a_0=0$. Otherwise, we swap their names. Define $f(n)=a_n-n$ and $g(m)=b_m-m-1$. Let’s prove that $f,g$ satisfy (*). Note that, if we put $N=n+m$, then condition (*) can be re-written as

$$a_n=f(n)+n\leq n+m=N\iff N=n+m< g(m)+m+1=b_m$$

In other words, among $f(n)+n$ and $g(m)+m+1$ one and only one of them is inside ${0,1,2,...,N}$. OK. Let’s look at the numbers $a_0<a_1<...<a_n$ and $b_0<b_1<...<b_m$. These together are $n+m+2$ different numbers, by assumption. So, $a_n$ and $b_m$ cannot both be in $X=\{0,1,2,...,n+m\}$, because otherwise all the $n+m+2$ of these numbers would also be inside this set of $n+m+1$ elements. On the other hand, one of $a_n$ or $b_m$ must be inside $X$. If not, inside $X$ we would have at most $a_0,...,a_{n-1},b_0,...,b_{m-1}$, which are only $n+m$ numbers and $A$ union $B$ wouldn’t include all of $X$, that contains $n+m+1$ elements.

QED.

**Solution of Problem 9 using Lambek-Moser theorem:** Since the exercise is about positive integers, let’s shift things to the natural numbers by subtracting $1$, where appropriate. Define

$$\begin{align*}a(n)&=f(n+1)-n-1=n+1-\left\lfloor\frac{1+\sqrt{8n+1}}{2}\right\rfloor\\ b(m)&=g(m+1)-1-m-1=m+\left\lfloor\frac{1+\sqrt{8m+1}}{2}\right\rfloor\end{align*}$$

Note that all those $+1$ and $-1$ there are just to get $a,b:\mathbb{N}\to\mathbb{N}$. If we prove that $a(m)\leq n\iff m\leq b(n)$ then Lambek-Moser theorem gives us that the two sets in the problem partition the positive integers.

This is only a play with inequalities. If $a(n)\leq m$, then $n-m+1\leq \left\lfloor\frac{1+\sqrt{8n+1}}{2}\right\rfloor\leq \frac{1+\sqrt{8n+1}}{2}$. Isolating the square root and squaring, this implies that $(2n-2m+1)^2-8n-1\leq0$. We want to get to the inequality $n\leq b(m)$, in which $n$ is isolated. The inequality that we have is quadratic, so we can solve for $n$. We get that $n$ must be between the two solutions that the quadratic formula gives us. The inequality with the larger root is the one that we want to look at $n\leq m+\frac{1+\sqrt{8m+1}}{2}$. Since $n$ is an integer, this inequality implies that we also have $n\leq m+\left\lfloor\frac{1+\sqrt{8m+1}}{2}\right\rfloor=b(m)$.

The other direction is almost the same work. If $n\leq b(m)$, then $n-m\leq\left\lfloor\frac{1+\sqrt{8m+1}}{2}\right\rfloor\leq \frac{1+\sqrt{8m+1}}{2}$. Massaging this gives $(2n-2m-1)^2-8m-1\leq 0$. We solve for $m$, and we only need to look at the resulting inequality with the smaller root this time. $n+1-\frac{1+\sqrt{8n+1}}{2}\leq m$. Since $m$ is an integer, we have that $n+1-\left\lfloor\frac{1+\sqrt{8n+1}}{2}\right\rfloor\leq m$, which is $a(m)\leq n$.

> **Exercise 3:** You will get a good command on the technique in the proof of Lambek-Moser theorem, if you now solve Problem 9 without invoking Lambek-Moser theorem, you instead imitate the proof, with these two functions $a,b$. In other words, imitate the two paragraphs that begging with “Proving that $A,B$ are disjoint” and "Proving that the union of $A$ and $B$ is all of $\mathbb{N}$.

**Note:** There is another observation that we should make about $(*)$, that is what allow us to do computations (produce formulas) of Galois connections. This is useful in problems like Exercise 2. In this problem, we have a formula $F(n)=n^2$ for the perfect squares, and we need to produce a formula for the complementary set. Note that the $f$ that we would care about is $f(n)=n^2-n$. We only need to “compute” its “kind of inverse” $g$ that forms $f,g$ a Galois connection.

Well, note that $(*)$ is equivalent to

$$\begin{align*}f(n)&=\min{m\in\mathbb{N}:\ n\leq g(m)}\ g(m)&=\max{n\in\mathbb{N}: f(n)\leq m}\end{align*}$$

The formula that we are looking for, is a formula for $G(m)=g(m)+m+1$.

Note also that the floor function is also defined by maximum (the maximum integer that is smaller than the number input). That is why we can obtain a formula for $G(m)$ using the floor function and playing with the formula for $f$ when solving the inequality $f(n)\leq m$.

Pretty stuff, eh? You can imagine that the organizers of math competitions have here a plethora of possible pretty exercises to ask, that would also be a bit annoying to solve if we didn’t know how the Lamberk-Moser theorem goes. They can put any simple formula for $f(m)$, and ask something about the complement. $f(m)$ could be the the squares $m^2$, cubes $m^3$, triangular numbers $\frac{m(m+1)}{2}$, ... anything increasing really. Or they could give use a mysterious pair of function with floors, like in Problem 9. Or two complementary infinite subsets of the natural numbers and no formulas at all, like the primes and composite numbers and we need to say something about the function $p_n$ that gives the $n$-th prime.

> **Exercise 4:** This should be simple, but good to practice our understanding. If $A$ and $B$ are the even and odd natural numbers, respectively. Who are the corresponding functions $f,g$ that form a Galois connection?
