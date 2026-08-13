## Inverse Hyperbolic Functions — ± Rule

**Rule:** Only **cosh** and **sech** give ± when solving. All others give one solution.

**Why:** cosh and sech are even (U-shape / bell-shape) → two x-values per y-value. The rest are one-to-one → one solution.

**Inverse formulas (always just +):**
- $\sinh^{-1}(x) = \ln(x + \sqrt{x^2+1})$
- $\cosh^{-1}(x) = \ln(x + \sqrt{x^2-1})$, $x \geq 1$
- $\tanh^{-1}(x) = \frac{1}{2}\ln\left(\frac{1+x}{1-x}\right)$, $-1 < x < 1$
- $\text{sech}^{-1}(x) = \ln\left(\frac{1 + \sqrt{1-x^2}}{x}\right)$, $0 < x \leq 1$
- $\text{cosech}^{-1}(x) = \ln\left(\frac{1 + \sqrt{1+x^2}}{x}\right)$, $x > 0$
- $\coth^{-1}(x) = \frac{1}{2}\ln\left(\frac{x+1}{x-1}\right)$, $x > 1$

**Solving $\cosh(x) = k$:**
1. $x = \pm\cosh^{-1}(k)$
2. $x = \ln(k \pm \sqrt{k^2-1})$ ← ± absorbed via $-\ln(a) = \ln(1/a)$

**Solving $\text{sech}(x) = k$:**
1. $x = \pm\text{sech}^{-1}(k)$
2. $x = \ln\left(\frac{1 \pm \sqrt{1-k^2}}{k}\right)$ ← same absorption trick