# Problem 0

No colloborators. Resources: Desmos

# Problem 1

a) Firstly, the expression for $z$ can be re-written in polar form as $4+r^2$ since we know that $r=x^{2}+y^{2}$. Since we are integrating over the quarter circle of radius 2, our radius will span from 0 to 2. Since we also want to constrain our integral to the first integral, our $\theta$ bounds will be from $0$ to $\frac{\pi}{2}$. 

From this, we have:
$$
	\int_{0}^{\pi/2} \int_{0}^{2} (4+r^{2}) (r) \, dr  \, d\theta 
$$
Note that we also had to include an $r$ factor when deriving a cylindrical integral from Cartesian expressions.

b) Now we can solve this

$$
	\begin{align}
	& \int_{0}^{\pi/2} \int_{0}^{2} 4r + r^{3} \, dr  \, d\theta  \\
	& \int_{0}^{\pi/2} \left[ \frac{4r^{2}}{2} + \frac{r^{4}}{4} \right]_{0}^2 \, d\theta \\
	& \int_{0}^{\pi/2} \left( \frac{16}{2} + \frac{16}{4} \right) \, d\theta  \\
	& \int_{0}^{\pi/2} 12 \, d\theta \\
	& \left[ 12\theta \right]_{0}^{\pi/2}   \\
	&  12 \cdot \frac{\pi}{2} \\
	&  6\pi
	\end{align}
$$

# Problem 2
![[Screenshot 2026-11-19 at 5.14.19 PM.png|196]]

From the Desmos visualization it becomes clear that our lower z bound must be the sphere while the upper z bound must be the parabola. The r bounds would have to span from 0 (since the parabola touches the origin) and the radius at which the parabola/sphere intersect. We can solve for that 
$$
	\begin{align}
	 & z = r^2 \\
	 & z = \sqrt{ 6 - r^{2} } \\
	 & r^{4} = 6 - r^{2} \\
	 & r^{4} + r^{2} = 6 \\
	 & r = \sqrt{ 2 }
	\end{align}
$$
The $\theta$ bound would just be $0$ to $2\pi$, since we do not want to constrain our integral over any specific angle range

Thus, our integral becomes,
$$
		\int_{0}^{2\pi} \int_{0}^{\sqrt{ 2 }} \left[ \sqrt{ 6-r^{2} } -  {r^{2}}   \right] r  \, dr  \, d\theta 
$$

Desmos shows that the value of this integral is about 7.74284979756

![[Screenshot 2026-11-19 at 5.24.50 PM.png|274]]

# Problem 3
