Here are two ideas that appear often.

## Changing the order of summation


This one you definitely know. Addition is **commutative**. Namely, $a+b=b+c$. It is also **associative**. Namely, $(a+b)+c=a+(b+c)$. These allow us to do things like $\sum\_{x\in A}\sum_{y\in B}f(x,y)=\sum\_{y\in B}\sum\_{x\in A}f(x,y)$, swap the order of summation. We can look at this a bit geometrically by thinking that we have a bunch of numbers to add, that are arranged in some $2$-dimensional shape

$$\begin{matrix} &1&2&\\ 3&4&5&6\\ &7&8&9\\ &&10&\\ &11&& \end{matrix}$$

If you want we can imagine that there are zeros in the empty spaces

$$\begin{matrix} 0&1&2&0\\ 3&4&5&6\\ 0&7&8&9\\ 0&0&10&0\\ 0&11&0&0 \end{matrix}$$

The set $A$ is the set of rows, perhaps numbered $0,1,2,3,4$, and $B$ the set of columns $0,1,2,3$. The function $f(x,y)$ is the value in the table at row $x$ and column $y$.

We could add all these values in any order.

The sum $\sum\_{x\in A}\sum\_{y\in B}f(x,y)$ is adding first each row and then adding those sums.

$$\begin{align*} 0+1+2+0&=3\\ 3+4+5+6&=18\\ 0+7+8+9&=24\\ 0+0+10+0&=10\\ 0+11+0+0&=11\\\hline\\&\phantom{{}={}}66 \end{align*}$$

The sum $\sum\_{y\in B}\sum\_{x\in A}f(x,y)$ is adding first each column and then adding those sums.

$$\begin{matrix} 0&1&2&0\\ +&+&+&+\\ 3&4&5&6\\ +&+&+&+\\ 0&7&8&9\\ +&+&+&+\\ 0&0&10&0\\ +&+&+&+\\ 0&11&0&0\\ ||&||&||&||\\ 3&+23&+25&+15&=66 \end{matrix}$$

Other orders are possible, and interesting, too. For example, we could add by diagonals. The key is to always be alert for the possibility of changing the order of summation. In some problems, it can yield interesting results, or make the computation simpler.

Sticking our neck out to look at the future, this idea of swapping the order of summation you will all see again in Calculus (or Mathematical Analysis), in the form of Fubini’s theorem. This theorem is about when we can and how to swap integrals. Sums are a particular case of integrals.

## Looking at the inverse function


The idea is as simple as the title. Sometimes we could be working with some function, that is a bit annoying to play with, but it has an inverse function, and this inverse is nicer somehow. Then, instead of studying the original function, we study the inverse and through it we gain knowledge about the original function.

One important event in the history of mathematics in which this idea was applied, was when Niels Abel did exactly this to to study elliptic integrals (it doesn’t matter what that is). He looked at the inverse function, which turn out much nicer to study (elliptic functions).

Let’s review first inverse functions. The inverse $f^{-1}(x)$ of the function $f(x)$ (if it exists) is a function that satisfies $f(f^{-1}(y))=y$.

**Algebraically:** The value $f^{-1}(y)$ is a (rather is **the**) solution of the equation $f(x)=y$, for a given $y$. So, to compute inverse functions, we often end up solving equations.

**Geometrically:** If $(x,f(x))$ is a point on the graph of $f$, then $(f(x),x)$ is a point on the graph of the inverse $f^{-1}$. In fact, we could call $f(x)=y$, and then $x=f^{-1}(y)$. Therefore, $(f(x),x)=(y,f^{-1}(y))$, which is a point on the graph of $f^{-1}$. Note that swapping the order of the coordinates, which is what we did to go from $(x,f(x))$ to $(f(x),x)$, geometrically, in the Cartesian plane, is the same as reflecting the plane with respect to the diagonal line $\nearrow$, with equation $y=x$.

We see now why I put these two ideas in the same note. What happens with a table of numbers, if we reflect them with respect to a diagonal, for example $\nearrow$? Well, rows become columns and columns become rows. See above, that when we swapped the order of summation, that is sort of what we did too. In the first case we added rows first. We can think that in the second case, instead of adding columns, we reflect the table across a diagonal (so columns swap with rows) and then we still add rows (which are the former columns).

Examples can be any function that you think is not so nice in some sense (this is always relative) and the inverse nice in some other sense. For instance:

1.  $\ln(x)$ has problems at $x=0$ among other inconveniences. However its inverse $e^x$ is nice in many senses. It is even periodic $e^{x+2\pi i}=e^x$.
2.  $\sqrt{x}$ is annoying to add, but its inverse $x^2$ is even a polynomial.
3.  $\ln(x+\sqrt{x^2+1})$ is at least as spooky as the two previous examples combined, but its inverse is $\sinh(x)=\frac{e^x-e^{-x}}{2}$ is nicer.

## Applications

The ideas above are so general that they could be useful in many situations. Here I will only consider a set of problems that have all a similar flavor.

Suppose that we want to compute

$S=\sum\_{k=0}^n\lfloor f(k)\rfloor$$

for some given function $f$. Even if the function $f$ were nice, the floor $\lfloor\cdot\rfloor$ makes it inconvenient to sum. Before looking at the inverse function, let’s look at this sum geometrically. If we plot the graph of $f$, note that $\lfloor f(k)\rfloor$ is counting how many points with integer coordinates are strictly above the point $(k,0)$ and below or on the point $(k, f(k))$. So, the sum $S$ is counting the number of integer points that are below or on the graph of $f$ and above the $X$-axis, between the vertical lines $x=0$ and $x=n$. The sum $\sum_{k=0}^n\lfloor f(k)\rfloor$ is computing this sum counting how many integer points are in each vertical line (columns) and adding to get the total. Ok, but what about if we count in a different order?

Let’s count how many integer points are in each horizontal line and then sum. Let’s look at a horizontal line $y=k$, with $k\in\mathbb{Z}$. The latter condition because $\lfloor f(x)\rfloor$ will only spit out integer values. We need to solve $k=\lfloor f(x)\rfloor$. We know that $k=\lfloor f(x)\rfloor$ is the same as the system of inequalities $k\leq f(x)<k+1$. It doesn’t need to be the case that $f$ has an inverse, and it doesn’t need to be the case that that inverse is monotonic (or increasing), but if it is, solving these inequalities is just $f^{-1}(k)\leq x<f^{-1}(k+1)$. Counting all the integer $x$ could be simple, specially if $f^{-1}$ is a nicer function than $f$.

> **Exercise 1:** Prove that $\sum\_{k=1}^{m}\lfloor k\pi\rfloor+\sum_{k=1}^{n}\lfloor\frac{k}{\pi}\rfloor=mn$

**Hint:** Think on the problem geometrically and mixing in the ideas above. Look at the integer points, in the Cartesian plane, that are inside an $m\times n$ rectangle. Think of the line $y=\pi x$, which is the graph of the function $f(x)=\pi x$. What is the first sum counting? What is the second sum counting?

> **Exercise 2:** Prove that $\sum\_{k=1}^{n}\lfloor\sqrt{k}\rfloor=n\lfloor\sqrt{n}\rfloor-\frac{1}{3}\lfloor\sqrt{n}\rfloor^3-\frac{1}{2}\lfloor\sqrt{n}\rfloor^2+\frac{5}{6}\lfloor\sqrt{n}\rfloor$

Don’t get spooked by the look of the right hand side. This exercise is a direct application of the ideas above. You can do first the case of $n$ being a perfect square. That makes the formula look nicer.
