# Multivariable Functions
For single var functions we usually visualize w/ 2D graph. Two var funcs --> 3D graph
Pos axis convention right hand rule: put fingers to pos x, curl towards pos y, then thumb points pos z
**Parabaloid**: hill shaped surface with general formula $z=C-Ax^{2}-By^{2}$ (w/ +ve signs, bowl shape forms)
Contours of a paraboloid are always circular/elliptical as can be proved by setting $z$ to a const and gettnig eq of a circle
A trace is a contour w/ x or y const 

# Vectors
vec addition commutative
magnitude is $\sqrt{ x_{0}^{2}+x_{1}^{2}+\dots}$

# Dot products
Given $v_{1} = < a_{1},b_{1}>$ and $v_{2}= <a_{2},b_{2}>$, then the dot product $v_{1} \cdot v_{2} = a_{1}a_{2} + b_{1}b_{2}$ 
$$\cos \theta = \frac{v_{1} \cdot v_{2}}{|v_{1}| |v_{2}|}$$
$$
	v_{1} \cdot v_{2} = 0 \iff v_{1} \perp v_{2}
$$
For two **unit vectors** $v_{1},v_{2}$
$$
	v_{1} \cdot v_{2} = 1 \iff v_{1} \parallel v_{2}
$$
... and for anti-parallel (pointing in exact opposite directions), $v_{1} \cdot v_{2} = -1$

$$
	|v| = \sqrt{ v \cdot v }
$$
Proof:
$$
	\sqrt{ v \cdot v } = \sqrt{ <a,b> \cdot <a,b> } = \sqrt{ a^{2} + b^{2} } = |v|
$$

# Projections
$$
	\text{vector proj of b onto a} = \frac{b \cdot a}{|a|^2} a
$$
$$
	\text{scalar proj of b onto a = } \frac{b \cdot a}{|a|} = |b| \cos \theta
$$
# Planes
Equation of plane always of the form $x + 2y + 3z = 0$ 
Plane can be expressed as a dot product equation $<1,2,3> \cdot <x,y,z> = 0$. Here $<1,2,3>$ is the vector perp to plane
A plane goes through $(0,0,0) \iff$ plane equation of form $z = Ax + By$ OR $ax + by + cz = 0$
All normal vectors of a plane are scalar multiples of eo
![[Pasted image 20260914114104.png|332]]
Given $<a,b,c>$ normal vector and point $(x_{0},y_{0},z_{0})$ on the plane, equation is 
$$
	a(x-x_{0}) + b(y-y_{0}) + c(z-z_{0}) = 0
$$
This is very similar to point slope formula but in 3D. Comes from 
$$
	<x-x_{0},y-y_{0},z-z_{0}> \cdot <a,b,c> = 0
$$
which is basically saying that the vector between fixed point $x_{0},y_{0},z_{0}$ and any point on plane $x,y,z$ must be perp to normal vector, $<a,b,c>$

# Partial Derivatives
To take the partial derivative w.r.t some variable, treat all other variables as constant and derivate normally.


# Tangent Planes
Plane equations roughly look like $z=Ax+By+C$
The tangent plane to $z=f(x,y)$ at the point $(a,b)$ is $z = \frac{\partial f}{\partial x} (a,b)(x-a) + \frac{\partial f}{\partial x}(a,b)(y-b) + f(a,b)$

# Multi-variable Chain Rule: 
We first create a dependency tree and observe all paths from the variable we are differentiating to the the variable we are differentiating with respect to. Then we use the simple single-variable chain rule and sum up all those paths

![[Pasted image 20260923115005.png|175]]
$$
	\frac{\partial f}{\partial t} = \frac{\partial f}{\partial x} \cdot \frac{\partial x}{\partial t} + \frac{\partial f}{\partial y} \cdot \frac{\partial y}{\partial t}
$$
das