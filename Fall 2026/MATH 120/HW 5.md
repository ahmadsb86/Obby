Resources used: Desmos (only the tool mentioned in the question), Obsidian (for typesetting)
Collaborators: None


**Problem 1**

a)  Since we are given the velocity formula and need to find the position of the ball after a given amount of time, we can simply take the definite integral of the velocity formula between 0 and 5 seconds. The Desmos tool gives -27.84 as the result of that integration. Therefore, the ball is 27.84m below the cliff.
![[Screenshot 2026-10-28 at 2.39.00 PM.png|809]]

b) To answer the first question, we must find the point where the velocity is zero. Since we already have the velocity function, we simply need to solve for its roots (the inputs at which the function becomes zero).
$$
\begin{align}
v(t) = 120e^{ -\frac{t}{10} } - 100 &= 0\\
120 e^{ -\frac{t}{10} } &= 100 \\
e^{ -\frac{t}{10}} &= \frac{5}{6} \\
\frac{t}{10} &= -\ln\left( \frac{5}{6} \right) \\
t &= -10\ln\left( \frac{5}{6} \right) \\
&\approx 1.8232
\end{align}
$$
This roughly checks out with the graph in Desmos, since the velocity curve crosses the x-axis slightly to the left of $(2,0)$.

Taking the integral of the velocity function between $t=0$ and $t=1.8232$ will give us the displacement of the ball up until it reaches zero velocity (the peak in trajectory). This is essentially the height it covers. 

$$
\begin{align}
&\quad \int_{0}^{1.8232} 120e^{ -\frac{t}{10} }- 100 \, dt  \\ \\
&= \left[ -1200e^{ -\frac{t}{10} } - 100t \right]_{0}^{1.8232} \\
&= \left( -1200e^{ -0.18232 } - 100(1.8232) \right) - \left( -1200e^{ 0 } - 100(0) \right) \\
&= \left( -1200\left( \frac{5}{6} \right) - 182.32 \right) + 1200 \\
&= -1000 - 182.32 + 1200 \\
&\approx 17.678
\end{align}
$$

This is confirmed by the Desmos tool's integration result.

![[Screenshot 2026-10-28 at 3.14.32 PM.png]]


**Problem 2**:

a) First, we need to find a function in $y$ that represents our unit circle. We start by rearranging the equation of the unit circle to make $y$ the subject.
$$
\begin{align}
&x^{2}+y^{2}=1 \\
&y^{2}=1-x^{2} \\
&y=\pm \sqrt{ 1-x^{2} } \\
\end{align}
$$
The question only requires us to consider the part of the unit circle above the $x$-axis. This is represented by the positive square root in the above equation. Thus, we have
$$
	f(x) = \sqrt{ 1-x^{2} }
$$
We can now take the integral of this function between $-1$ and $1$ to find the area under the unit semi-circle. The Desmos tool shows this integral is $\approx1.5708$. This is half of $\pi$.

b) We need to find a value for $a$ such that when we take the area under the curve between $a$ and 1 of $f(x)$ as defined earlier, we get 1. In other words we are trying to find a lower limit of the integral such that the result is 1.
$$
	\int_{a}^{1} \sqrt{ 1-x^{2} } \, dx  = 1
$$
We can find this by solving for the antiderivative and then using the fundamental theorem of calculus to create an equation in $a$. However, it seems like solving this type of integral is outside the scope of what we have studied in class. Therefore, I approximated the value of $a$ by moving the slider for $a$ in the Desmos tool until I got an integral value close to $1$. I refined my approximations by repeatedly tightening the bounds on the slider for $a$, making it easier to get more fine-grained control on the values of $a$ I was trying out.

I found that setting $a=-0.2164$ resulted in the area under the curve being pretty close to 1.

![[Screenshot 2026-10-28 at 3.31.58 PM.png]]