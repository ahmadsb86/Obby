# Problem 0

Resources used: Desmos, standard scientific calculator
Collaborators: None

# Problem 1

For an underestimate, we can construct imaginary rectangular prisms over the region. The base of each prism is a $2 \text{x} 2$ rectangle in the $x$-$y$ plane, and its height is the approximate height of the surface at the bottom-left corner of that rectangle (toward negative $x$, negative $y$). Because there is a peak near the middle of $R$, some boxes underestimate while others overestimate. Boxes to the left/bottom of the peak underestimate, while xoxes to the right/top of the peak overestimate. The underestimating boxes outweigh the overestimating ones, so the sum of these boxes is an underestimate.

In the screenshot below, my estimates for the surface height at those bottom-left corners are written in black text. The black lines outline the $2 \text{x} 2$ rectangles in the $x$-$y$ plane.

![[Screenshot 2026-11-11 at 2.39.31 PM.png]]

The sum of these box volumes is

$$4 \cdot (3.5 + 12 + 7.5 + 2 + 6.5 + 6) = 4 \cdot 37.5 = 150$$

For an overestimate, we can follow the same procedure, except using the surface height at the top-right corners. This time, the overestimating boxes outweigh the underestimating ones, so this sum is an overestimate.

![[Screenshot 2026-11-11 at 2.11.28 PM.png]]

Now the sum is

$$4 \cdot (6.5 + 6 + 6 + 12 + 7.5 + 6) = 4 \cdot 44 = 176$$

So the volume lies roughly between $150$ and $176$. A good estimate of the true integrated volume would be the average which comes out to be 163.
$$
 \frac{150+176}{2} = 163
$$

# Problem 2

Plotting the region, it is clear that the region $R$ spans $-2 \leq x \leq 6$ as well as $0 \leq y \leq 9$



![[Screenshot 2026-11-11 at 2.53.06 PM.png|616]]

I will construct an iterated integral such that the outer integral is w.r.t $x$. Therefore $x$ will be treated as a constant for the inner integral. We can see from the Desmos graph that for a certain value of $x$, the $y$-integral should sweep from the lower parabolic curve to the upper straight line. Therefore, the inner integral should look like
$$
	\int_{\frac{x^{2}}{4}}^{x+3} (x+2) \, dy 
$$
The outer integral should sweep from $x=-2$ to $x=6$. This is obvious from the plot, but we can compute these points by solving the two equations simultaneously to find intersection points.

$$
	\begin{align}
		& x+3 = \frac{x^{2}}{4} \\
		& 4x + 12 = x^{2} \\
		& x^{2} - 4x - 12 = 0 \\
		& x^{2} -4x +4 - 16 =0 \\
		& (x-2)^{2} - 16 = 0 \\
		& x - 2 = \pm4 \\
		& x = -2, 6
	\end{align}
$$
Thus, the complete iterated integral should be
$$
	\int_{-2}^{6} \int_{\frac{x^{2}}{4}}^{x+3} (x+2) \, dy  \, dx  = 85.333
$$
The numerical result of the integral was found by plugging in the whole iterated integral into Desmos.

# Problem 3

Essentially, the problem asks us to take the integral of the surface $z=y$ over the area between  $y=a^{2} - x^{2}$ and $y=0$. This integral is easier to set up if we start constructing an inner integral for a constant value of $x$. We know the integral must sweep from $y=0$ to $y=a^{2}-x^{2}$ for any value of $x$. Therefore, the inner integral must look like
$$
	\int_{0}^{a^{2}-x^{2}} (y) \, dy 
$$
The outer integral should just sweep the values of $x$ between the two roots of $a^{2}-x^{2}$, because those two points would bound the sides of the wedge. We can find these roots algebraiclly.
$$
\begin{align}
 & a^{2}-x^{2} = 0\\
 & x ^{2} = a^{2} \\
 & x = \pm a
\end{align}
$$
Hence, the outer integral should have bounds $a, -a$. Finally, we have
$$
	\int_{-a}^{a} \int_{0}^{a^{2}-x^{2}} (y) \, dy  \, dx
$$
To solve this, first I will compute the inner integral keeping $x$ as constant
$$
\begin{align}
& \int_{0}^{a^{2}-x^{2}} y \, dy  \\
=& \left[ \frac{y^{2}}{2} \right]_{0}^{a^{2}-x^{2}} \\
=&\left[ \frac{\left( a^{2}-x^{2}  \right)^{2} }{2}  \right]   - \left[ \frac{0^{2}}{2} \right]  \\
=& \frac{\left( a^{2}-x^{2}  \right)^{2}}{2}
\end{align}
$$
Now, we can subsitute the inner integral for this expression, and solve the full iterated integral
$$
\begin{align} \\
&\int_{-a}^{a}\frac{(a^2-x^2)^2}{2} \, dx  \\
=& \frac{1}{2}  \int_{-a}^a \left(a^4-2a^2x^2+x^4\right)dx \\
=& \frac{1}{2} \left[ a^{4}x - \frac{2a^{2}x^{3}}{3} + \frac{x^{5}}{5} \right]_{-a}^{a} \\
=& \frac{1}{2} \left[ a^{5} - \frac{2a^{5}}{3} + \frac{a^{5}}{5} \right] - \frac{1}{2}\left[ -a^{5}+\frac{2a^{5}}{3}-\frac{a^{5}}{5} \right]  \\
=& \, a ^{5} - \frac{2a^{5}}{3} + \frac{a^{5}}{5}  \\
=& \frac{8}{15}a^{5}
\end{align}
$$
