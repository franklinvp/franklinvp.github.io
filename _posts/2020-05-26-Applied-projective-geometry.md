---
layout: post
title: Applied projective geometry
subtitle: Trying to draw a horizontal like without a level
---

One day I was too lazy to go get a level and didn't want to measure.
So, I tried to apply projective geometry to draw one with a no-compass, straightedge-only construction.

{: .box-note}
Two different parallel lines and a point not on them are given. Using only [straightedge](https://en.wikipedia.org/wiki/Straight_edge) construct a line passing through the given point that is parallel to the two given lines.

![Applied projective geometry](../assets/img/appliedprojectivegeometry.jpg){: .mx-auto.d-block style="max-height: 80vh; width: auto;"}

<details>
    <summary>Solution</summary>

    Let the two given lines be called $\alpha$ and $\beta$, and the given point $P_1$.
    First we draw two points $A\_1$ and $A\_2$ on $\alpha$ and learn how to construct the midpoint of the segment $A\_1A\_2$.

    **Constructing midpoint of a segment:**

    1. Take a point $B\_1$ on $\beta$ and draw the line $A\_1B\_1$.
    2. Take a point $C$ on $A\_1B\_1$, that is outside $\alpha$ and $\beta$.
    3. Draw the line $CA\_2$ and let $B\_2$ be the point of intersection of this like with $\beta$.
    4. Draw the lines $A\_1B\_2$ and $A\_2B\_1$. Let $D$ be the point of intersection of these lines.
    5. Draw the line $CD$. The point of intersection of this line and the line $\alpha$ is the midpoint of $A\_1A\_2$.

    **Construction of the third parallel line:**

    Let the two given parallel lines be $\alpha$ and $\beta$, and the given point $P\_1$.

    1. Select to points $A\_1$ and $A\_2$ on $\alpha$.
    2. Construct the midpoint $A\_3$, of the segment $A\_1A\_2$. [The line $\beta$ is no longer needed.]
    3. Draw the line $A\_1P\_1$.
    4. Select a point $Q$ on the line $A\_1P\_1$, different from $A\_1$ and from $P\_1$.
    5. Draw the lines $QA\_2$ and $QA\_3$.
    6. Draw the line $A\_2P\_1$ and let $R$ be its intersection with $QA\_3$.
    7. Draw the lines $A\_1R$ and $QA\_3$ and their intersection $P\_2$.
    8. The line $P\_1P\_2$ is parallel to the line $\alpha$.
</details>
