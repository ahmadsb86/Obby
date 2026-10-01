# Problem 1 - Part A
$$
	\frac{ \partial f }{ \partial x } (1,-1) \approx \frac{0.04-0.06}{0.4} = -0.05
$$
By visually observing the contour plot, we can see that the point $(1,-1)$ lies on the contour line of 0.06. Therefore I estimate the value of $f(x,y)$ to be 0.06 at that point. I then look at the point 0.04 units to the right at $(1.4,-1)$. This point seems to fall on the contour line of 0.04. I know that the value of a partial derivative $\frac{ \partial f }{ \partial x }$ can be estimated by dividing a small resulting change in the value of $f(x,y)$ by a small change in the value of $x$. Here, the change in x was 0.04, and the resulting change in $f(x,y)$ was $0.04-0.06=0.02$. I divide these two numbers to get my estimate for $\frac{ \partial f }{ \partial x }$

$$
		\frac{ \partial f }{ \partial y } (1,-1) \approx \frac{0.08-0.06}{0.4} = 0.05
$$

For the partial derivative, $\frac{ \partial f }{ \partial y }$ I use the exact same procedure. I observe $f(x,y)$ is approximately 0.06 at $(1,-1)$ but 0.08 at the point 0.4 units upwards. I divide the change in $f(x,y)$ from 0.4 to get my answer.

# Problem 1 - Part B

![[Pasted image 20260924205533.png|303]]

Here I use implicitly use the chain rule. I use the rule for derivating exponents of $e$ where you take the derivative of x within the exponent and multiply it by the original function. 

# Problem 1 - Part C

![[Pasted image 20260924205610.png|372]]

Intuitively, I can observe from the contour plot that any point that lies on the x-axis should have a $\frac{ \partial f }{ \partial y }$ of 0 since the tangents of the circles seem to point directly upwards. Therefore, I try point $(1,0)$ and plug it into the equation for $\frac{ \partial f }{ \partial y }$ which I found using the exact same procedure used in part (b). 

# Problem 1 - Part D

A paraboloid's contour lines form circles that, as you go outwards from the center of the circles, appear closer and closer together (of course, this only applies if the contour lines represent equidistant values of $f(x,y)$). This is because the value of any function $f(x,y) = ax^{2}+by^{2}+c$ clearly does not grow linearly with respect to either $x$ or $y$. At more extreme values of $x$ or $y$, the value of $f(x,y)$ changes more dramatically (and thus the contour lines appear closer) by the nature of the squaring operation on both $x$ and $y$.  The same is true for a hemisphere. As your go outwards from the center of the circles on the contour line plot, the circles appear closer and closer. However, in the contours of this function do not follow the same pattern. As you go further from the center of the contours, they appear to become more and more distant from each other. This shows that the underlying function is not a hemisphere or a paraboloid, but a kind of surface that flattens out towards the extremes.

# Problem 2 - Part A

![[Pasted image 20260924211423.png|444]]

Similar to Q1A, I estimate the value of the partial derivatives by looking at the value at $(40000,30)$ and seeing how it changes when I look one box below or to the left. I divide that change in value by the change in either $I$ or $Y$.

# Problem 2 - Part B

The first result, estimating $\frac{ \partial S }{ \partial I }$, shows that near a current salary of $40,000 and 30 years to retirement, every extra dollar you earn in current salary will get you 25 cents more of Social Security annual income.

The second result, estimating $\frac{ \partial S }{ \partial Y }$, shows that near a current salary of $40,000 and 30 years to retirement, every extra year you have left until retirement will get you $500 more of Social Security annual income.


# Problem 3 - Part A

![[Pasted image 20260924214703.png|406]]

For this question, I used the formula for the tangent plane equation at $(a,b)$: 
$$z = \frac{\partial f}{\partial x} (a,b)(x-a) + \frac{\partial f}{\partial y}(a,b)(y-b) + f(a,b)$$
I evaluated each of the parts of this formula separately. For the partial derivatives, I only used the power rule.

# Problem 3 - Part B

![[Pasted image 20260924215419.png|335]]
![[Pasted image 20260924215518.png|336]]

# Problem 3 - Part C

![[Pasted image 20260924215755.png|478]]

# Problem 3 - Part D

Both of the second partial derivatives are negative which shows that the value of the partial derivatives is decreasing. The partial derivative with respect to y is negative anyways, so this must mean that the partial derivative in the y direction is getting more negative (more steep). This is shown by the surface sloping downwards, more and more steeply, in the y-direction away from (1,1). If a ball were to be constrained in the y-direction on the slope, it would roll downwards as its y-value increased. Additionally it would roll down faster and faster (accelerating much faster than it would on a flat ramp because the slope is getting steeper and steeper). 

Another way to view it is the following. If the partial derivative with respect to y at (1,1) is decreasing and is already negative at (1,1), it must be zero at some point before (1,1) in the y-direction. That is to say, it must be zero at some point along $x=1$ with a smaller y-value that 1.  There is indeed such a peak that can be seen in the surface plot at a point with a slightly lesser y-value than 1.

The partial derivative with respect to x is positive, but is decreasing because the second order partial derivative is negative. This is shown by how the surface at (1,1) gains elevation as you move towards positive x, but reaches a peak very soon (at this point the partial derivative with respect to x is zero). The peak on the positive x side of the point (1,1) is a result of the fact that the slope in the positive x direction becomes less and less steep until it is zero. 

In short, the fact that both second partial derivatives are negative shows that the surface is more so hill-shaped than bowl-shaped