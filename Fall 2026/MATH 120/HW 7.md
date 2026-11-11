# Problem 1

For an underestimate, we can construct imaginary rectangular prisms under the surface. The base of these prisms will be a $2\text{x}1$ rectangle in the $x$-$y$ plane. Their height will be the approximate height of the surface at the top right corner of that $2\text{x}1$ rectangle (towards positive $y$, positive $x$). Since there is a peak near the middle of the $R$, some boxes will inevitably overestimate while others underestimate. As it turns out, the overestimating boxes towards the left/bottom of the peak outweigh the underestimating boxes towards the right/top of the peak. Thus, the sum of these boxes is an underestimate.

In the screenshot below, my estimates for surface height at those top-right corners are written in black text. The black lines outline the $2\text{x}1$ rectangles in the $x$-$y$ plane

![[Screenshot 2026-11-11 at 2.11.28 PM.png]]


The sum of these box volumes is
$$
	2 \cdot (6.5 + 6 + 6 + 12 + 7.5 + 6) = 2 \cdot 44 = 88
$$
For an overestimate, we can follow the same procedure as before, except using the surface height at the bottom-left corners.