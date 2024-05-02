# Linear homogeneous recurrence relations with constant coefficients and finite order

This note is about a family of recurrence relations (some people call them also **difference equations**) that are the easiest to solve. More general cases can also be solved, like some non-homogeneous, some cases of non-constant coefficients, etc. This is only a minimum that is good to have in your toolbox.

Consider a recurrence like

$x\_{n+d}=a\_{d-1}x\_{n+d-1}+a\_{d-2}x\_{n+d-2}+...+a\_1x\_{x+1}+a\_0x\_n$

where $a\_0,a\_1,...,a\_{d-1}$ and $d$ do not depend on $n$. The value $d$ is called the order of the difference equation (or recurrence). It is how far back into the history of the sequence one needs to look, for the recurrence equation to give the next term. The equation is supposed to be satisfied for all $n\geq0$. If someone gives us the values of the first $d$ terms $x\_0,x\_1,...,x\_{d-1}$ of the sequence, then the sequence $x\_n$ is uniquely determined.

## The name

* **Linear:** In the equation, there are only $x\_k$ multiplied by some constants and added.
* **Homogeneous:** There is no extra term, like $+n^2$ in $x\_{n+2}=3x\_{n+1}+n^2$.
* **Constant coefficients:** Self-explanatory. The coefficients in front of the $a\_k$ are constant.
* **Finite order:** The $d$, the (maximum) amount of history that the equation needs to compute the next term stays the same. Compare the equation above, with $x\_{n}=x\_{n-1}+x\_{n-2}+...+x\_1+x\_0$. In this one, to compute $x\_n$ we need to look back at all previous terms. So, when $n$ increases, so does the amount of terms that the equation requires to compute the next term. **Note:** We are seeing order as a property of the equation. In this example, it is possible to transform the family of equations into a new one that does have finite order, by subtracting $x\_{n}=x\_{n-1}+x\_{n-2}+...+x\_1+x\_0$ from $x\_{n+1}=x\_{n}+x\_{n-1}+...+x\_1+x\_0$.

## The recipe for the solution

The polynomial

$t^d=a\_{d-1}t^{d-1}+a\_{d-2}t^{d-2}+...+a\_1t+a\_0$

is called its **characteristic polynomial**. The concept of characteristic polynomial will appear also in linear algebra, associated to linear transformations. They are called the same name because the one here is a particular case of the other.

Assume that

$r\_1, r\_2,...,r\_k$

are the different roots of the characteristic polynomial (complex in general) and that they have multiplicities

$m\_1,m\_2,...,m\_k$, respectively. Note, that in particular $m\_1+m\_2+...+m\_k=d$.

So, the general solution of the recurrence relation is

$x\_n=(c\_{1,0}+c\_{1,1}n+...+c\_{1,m\_1-1}n^{m\_1-1})r\_1^n+(c\_{2,0}+c\_{2,1}n+...+c\_{2,m\_2-1}n^{m\_2-1})r\_2^n+...+(c\_{k,0}+c\_{k,1}n+...+c\_{k,m\_k-1}n^{m\_k-1})r\_k^n$

An easy way to remember this is that we take each root $r\_i$, raise it to the power $n$ and multiply it by a polynomial $c\_{i,0}+c\_{i,1}n+...+c\_{i,m\_i-1}n^{m\_i-1}$ of degree at most $m\_i-1$ (or less than $m\_i$).

Here, all $c\_{i,j}$ are some arbitrary constants not depending on $n$.

If someone gives us $d$ consecutive particular values of the sequence, for example $x\_0,x\_1,...,x\_{d-1}$, then we can determine the specific values of the constants $c\_{i,j}$.

When you get more comfortable with linear algebra it will be a good exercise to prove that in fact the solution above is the general solution. For the moment, do practice some linear recurrences to make sure you remember how it goes.

## Exercises

1. [Fibonacci] Find an algebraic expression for $F\_n$ in terms of $n$, if $F\_{n+2}=F\_{n+1}+F\_{n}$ for all $n\in\mathbb{Z}$. **Note:** The solution will depend on two arbitrary constants. Then impose that $F\_0=1$ and $F\_1=1$ to get what is known as [Binet's formula](https://en.wikipedia.org/wiki/Fibonacci\_sequence#Closed-form\_expression) for the Fibonacci sequence.
2. Find all solutions of $S\_n=2S\_{n-1}-S\_n$.
3. Find all solutions of $D\_{n}=4D\_{n-1}-D\_{n-2}$.
4. If $X\_{n}=5X\_{n-1}-6X\_{n-2}$, show that $|X\_n/3^n|$ is bounded. In other words, that there is some constant $M$ such that for all $n$ we have $|X\_n/3^n|\leq M$. **Hint:** First compute the solution of the recurrence and then divide it by $3^n$.

## A little taste of why the general solution looks like that

You can completely ignore this part for the moment.

Let $S$ be the function that takes in a sequence, and returns the same sequence shifted to the right. This is, $Sx\_n=x\_{n+1}$. This is called the **right-shift operator**. We will denote $S^k$ to applying the right shift $k$ times. In other words $S^kx\_n=x\_{n+k}$

So, we can re-write the recurrence relation as

$(S^d-a\_{d-1}S^{d-1}-a\_{d-2}S^{d-2}-...-a\_1S-a\_0)x\_n=0$

Note that, in parentheses, what we have is the characteristic polynomial evaluated on the operator $S$.

The rest I will do with a particular example, to not overwhelm you with the notation.

Let's take the recurrence

$X\_{n+2}=3X\_{n+1}-X\_{n}$

We can write it as

$(S^2-3S+2)x\_n=0$

We can factor the characteristic polynomial completely (going to complex numbers if needed) as $t^2-3t+2=(t-1)(t-2)$.

So, the recurrence becomes

$(S-1)(S-2)x\_n=0$

Now look at this. A sequence like $y\_n=C\_22^n$, is "killed" by the operator $S-2$. In fact,

$(S-2)y\_n=Sy\_n-2y\_n=y\_{n+1}-2y\_n=C2^{n+1}-2C2^n=0$

Note that $y\_n$ would also be killed by $(S-1)(S-2)$, since already the factor $S-2$ makes it zero.

Similarly, the sequence $z\_n=C\_11^n$ is killed by the operator $S-1$. Check it. Therefore, $z\_n$ is also killed by $(S-1)(S-2)$, since this operator is the same as $(S-1)(S-2)=S^2-3S+2=(S-2)(S-1)$ and when we apply $(S-2)(S-1)z\_n$ already the $(S-1)z\_n$ is becoming the zero sequence.

Ok, so the sequence $x\_n=C\_11^n+C\_22^n=y\_n+z\_n$ satisfies the recurrence relation too, since

$(S^2-3S+2)x\_n=(S-1)(S-2)y\_n+(S-2)(S-1)z\_n=0$

Proving that $x\_n=C\_11^n+C\_22^n=y\_n+z\_n$ are in fact all solutions of $X\_{n+2}=3X\_{n+1}-2X\_n$ is done with a bit of linear algebra. It turns out that we can determine that the dimension of the space of solutions of the linear recurrence has dimension $d$ (the order of the recurrence) ($d=2$ in the example). This, together with checking that the solutions $x\_n=C\_11^n+C\_22^n$ also generate a space of the same dimension, is what ultimately proves that we got them all.

> **Note:** We can use the example to see that we indeed got all solutions. Note that if $x\_n$ is an arbitrary solution of the recurrence, then there are $C\_1, C\_2$ such that $C\_11^0+C\_22^0=x\_0$ and $C\_11^1+C\_22^1=x\_1$. Then, because the recurrence is linear, and $C\_11^n+C\_22^n$ is a solution, we get that $a\_n=x\_n-C\_11^n-C\_22^n$ is also a solution. However, $a\_0=a\_1=0$. An application of induction shows that for all $n$ we have $a\_n=0$. Therefore, $x\_n=C\_11^n+C\_22^n$. Note that the crucial point was that we managed to match whichever values were the **initial values** $x\_0$ and $x\_1$.

By the way, the polynomials that appear in the general solution, when roots of the characteristic polynomial have multiplicity is of course because they are killed by the corresponding powers of the shift operator. For example, check that $(C\_1+C\_2n)2^n$ is killed by $(S-2)^2$.
