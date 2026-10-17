To find the function representing the total cost of shipping to all three cities, we can sum the cost of shipping to each of the three cities. The cost to shipping to any city at $(a,b)$ from a location $(x,y)$ is equal to the distance to that city, $\sqrt{ (x-a)^{2} + (x-b)^{2}}$, multiplied by the unit cost of shipping (how much it costs to ship across one Snorg).

The following expressions represent the costs to each of the three cities:
- Arctangent: $2 \cdot \sqrt{ (x-0)^{2}+(y-0)^{2}} = 2\sqrt{ x^{2}+y^{2} }$
- Bohm: $1 \cdot \sqrt{ (x-0)^{2}+(y-2.8)^{2}} =  \sqrt{ x^{2} + (y-2.8)^{2} }$
- Cooper: $2.5 \cdot \sqrt{ (x-3.8)^{2}+(y-0)^{2}} = 2.5 \sqrt{ (x-3.8)^{2} + y^{2}}$

By summing these three expressions, we get our total cost function
$$
	f(x,y) = 2\sqrt{ x^{2}+y^{2} }+ \sqrt{ x^{2} + (y-2.8)^{2} } + 2.5\sqrt{ (x-3.8)^{2} + y^{2} }
$$

Finding the minimum of this function requires first finding the critical point of this function. This can be done by finding the partial derivatives with respect to x and y, and equating both to zero. Then we can solve this system of simultaneous equations to find the critical points.

$$
\begin{align}
\frac{ \partial f }{ \partial x } = \text{something}  \\
\frac{ \partial f }{ \partial y } = \text{something}
\end{align}
$$

