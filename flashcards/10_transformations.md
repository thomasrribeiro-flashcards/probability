+++
order = 10
tags = ["math", "probability", "transformations", "jacobian", "convolution", "order-statistics"]
+++

# Probability — Transformations of Random Variables

## 10.1 Why Transform?

Q: Why do we study transformations of random variables?
A: Real problems rarely hand us the random quantity we actually care about. We often know the distribution of some raw variable $X$ but need the distribution of a derived quantity $Y = g(X)$ (e.g., $X$ is a radius and we want the area $Y = \pi X^2$). Transformation techniques turn a known distribution into the unknown one we need.

Q: Before learning the formulas, predict: if $X$ is uniform on $[0,1]$, what do you expect the distribution of $Y = X^2$ to look like?
A: It should be concentrated near 0 (since squaring pushes values in $[0,1]$ toward 0) with a density that blows up at $y = 0$ and decreases toward $y = 1$.

C: If $X$ is a random variable and $g$ is a function, then $Y = g(X)$ is called a [transformation] (or function) of $X$.

C: The central problem of this chapter: given the distribution of $X$, find the [distribution of $Y = g(X)$].

Q: Name three real situations where you need the distribution of a transformed variable.
A: (1) Physics: kinetic energy $Y = \tfrac{1}{2}mX^2$ from velocity $X$. (2) Finance: log-return $Y = \ln(X)$ from price ratio $X$. (3) Engineering: area $Y = \pi X^2$ from radius $X$.

## 10.2 CDF Method for Discrete $Y = g(X)$

Q: If $X$ is discrete with pmf $p_X$, how do you find the pmf of $Y = g(X)$?
A: For each possible value $y$ of $Y$, collect every $x$ with $g(x) = y$ and sum their probabilities: $p_Y(y) = \sum_{x : g(x) = y} p_X(x)$, where $p_X(x) = P(X = x)$.

C: For a discrete transformation, $p_Y(y) = \sum_{x : g(x) = y} p_X(x)$, which sums the pmf of $X$ over the [preimage] $g^{-1}(y) = \{x : g(x) = y\}$.

Q: If $X$ takes values $\{-1, 0, 1\}$ each with probability $1/3$, what is the pmf of $Y = X^2$?
A: $Y$ takes value $0$ when $X=0$ (prob $1/3$) and value $1$ when $X \in \{-1, 1\}$ (prob $2/3$). So $p_Y(0) = 1/3$ and $p_Y(1) = 2/3$.

Q: When $g$ is not one-to-one on the support of discrete $X$, what changes in computing $p_Y$?
A: Multiple $x$-values map to the same $y$, so $p_Y(y)$ is a sum of several $p_X(x)$ values rather than a single probability. This is the discrete analog of "summing over branches."

## 10.3 CDF Method for Continuous $Y = g(X)$

Q: Why use the CDF method instead of trying to write down $f_Y$ directly?
A: The CDF $F_Y(y) = P(Y \le y)$ is always well-defined as a probability, even when $g$ is complicated, non-monotone, or has flat regions. Densities can be subtle, but probabilities of events like $\{g(X) \le y\}$ can always be written as an integral of $f_X$ over a region.

C: The [CDF method] for continuous transformations: compute $F_Y(y) = P(g(X) \le y)$ by rewriting the event $\{g(X) \le y\}$ in terms of $X$, then differentiate to get $f_Y$.

Q: Write the general formula for $F_Y(y)$ when $Y = g(X)$ and $X$ has density $f_X$.
A: $F_Y(y) = P(g(X) \le y) = \int_{\{x : g(x) \le y\}} f_X(x)\, dx$, where the integration region is the preimage of $(-\infty, y]$ under $g$.

P: Use the CDF method to find the density of $Y = X^2$ when $X \sim \text{Uniform}(0,1)$.

S:
**IDENTIFY**: Continuous transformation $Y = g(X) = X^2$; $X$ has density $f_X(x) = 1$ on $[0,1]$, else $0$. Want $f_Y$.

**PLAN**:
- Determine range of $Y$: since $X \in [0,1]$, $Y = X^2 \in [0,1]$.
- Compute $F_Y(y) = P(X^2 \le y)$ for $y \in [0,1]$.
- Differentiate $F_Y$ to get $f_Y$.

**EXECUTE**:
1. For $y \in [0,1]$: $F_Y(y) = P(X^2 \le y) = P(-\sqrt{y} \le X \le \sqrt{y})$.
2. Since $X \ge 0$: $F_Y(y) = P(0 \le X \le \sqrt{y}) = \sqrt{y}$.
3. Differentiate: $f_Y(y) = \dfrac{d}{dy}\sqrt{y} = \dfrac{1}{2\sqrt{y}}$ on $(0,1]$, else $0$.

**EVALUATE**:
- Density blows up at $y = 0^+$ — matches the intuition that squaring concentrates mass near 0.
- Check $\int_0^1 \tfrac{1}{2\sqrt{y}}\, dy = [\sqrt{y}]_0^1 = 1$ ✓.

## 10.4 PDF via Differentiation

Q: Why do we differentiate the CDF to get the pdf?
A: By definition, $f_Y(y) = F_Y'(y)$ wherever $F_Y$ is differentiable, with $F_Y(y) = P(Y \le y)$. So once we have the CDF in closed form, differentiation is a mechanical step that extracts the density.

C: If $F_Y(y) = P(Y \le y)$ is differentiable at $y$, then $f_Y(y) = [F_Y'(y)]$, where $f_Y$ is the pdf of $Y$.

Q: What can go wrong when differentiating $F_Y$ to get $f_Y$?
A: $F_Y$ may fail to be differentiable at boundary points of the support, or at values where $g$ has critical points (e.g., $y=0$ for $Y = X^2$). At those points, define $f_Y$ by taking appropriate left/right limits or just declare $f_Y$ only on the interior — a single-point mismatch doesn't affect probabilities.

## 10.5 Change-of-Variables Formula (Monotone Case)

Q: Why do we need a formula specifically for monotone transformations?
A: Monotonicity guarantees that $g$ is invertible and that the event $\{g(X) \le y\}$ corresponds cleanly to a single interval in $X$. This collapses the CDF method into a one-line formula involving only $f_X$, $g^{-1}$, and a derivative.

C: If $g$ is strictly increasing and differentiable, then $Y = g(X) \le y$ iff $X \le g^{-1}(y)$, so $F_Y(y) = [F_X(g^{-1}(y))]$, where $F_X$ is the CDF of $X$.

C: If $g$ is strictly decreasing and differentiable, then $Y = g(X) \le y$ iff $X \ge g^{-1}(y)$, so $F_Y(y) = [1 - F_X(g^{-1}(y))]$, where $F_X$ is the CDF of $X$.

C: [Change-of-variables formula] (monotone $g$): $f_Y(y) = f_X(g^{-1}(y))\,\left|\dfrac{dg^{-1}}{dy}(y)\right|$, where $f_X$ is the pdf of $X$ and $g^{-1}$ is the inverse of $g$.

Q: Where does the absolute value of the derivative come from in the change-of-variables formula?
A: For increasing $g$, $(g^{-1})' > 0$ and differentiating $F_X(g^{-1}(y))$ gives a $+$ sign. For decreasing $g$, $(g^{-1})' < 0$ and differentiating $1 - F_X(g^{-1}(y))$ gives a $-$ sign that cancels the negative derivative. The absolute value handles both cases in one formula.

P: Let $X \sim \text{Exp}(\lambda)$ with pdf $f_X(x) = \lambda e^{-\lambda x}$ for $x \ge 0$. Use the change-of-variables formula to find the pdf of $Y = \sqrt{X}$.

S:
**IDENTIFY**: Monotone transformation ($g(x) = \sqrt{x}$ is strictly increasing on $[0,\infty)$). Goal: $f_Y$.

**PLAN**:
- Compute $g^{-1}(y) = y^2$.
- Compute $\dfrac{dg^{-1}}{dy} = 2y$.
- Apply $f_Y(y) = f_X(g^{-1}(y))\,|(g^{-1})'(y)|$.

**EXECUTE**:
1. Support: $X \ge 0 \Rightarrow Y \ge 0$.
2. $g^{-1}(y) = y^2$, $(g^{-1})'(y) = 2y$.
3. $f_Y(y) = \lambda e^{-\lambda y^2} \cdot 2y = 2\lambda y\, e^{-\lambda y^2}$ for $y \ge 0$.

**EVALUATE**:
- This is the Rayleigh-style distribution.
- Check: $\int_0^\infty 2\lambda y\, e^{-\lambda y^2}\, dy = [-e^{-\lambda y^2}]_0^\infty = 1$ ✓.

## 10.6 Non-Monotone Transformations

Q: Why does the single-branch change-of-variables formula fail when $g$ is not monotone?
A: When $g$ is not monotone, the event $\{g(X) \le y\}$ can correspond to multiple disjoint intervals in $X$, and a single $y$ has multiple preimages $x_1, x_2, \ldots$. The density must account for probability mass contributed by every branch.

C: For non-monotone differentiable $g$ with finitely many preimages $x_1(y), \ldots, x_k(y)$ of $y$, the pdf of $Y = g(X)$ is $f_Y(y) = \sum_{i=1}^{k} f_X(x_i(y))\,\left|\dfrac{[dx_i]}{dy}\right|$, where $x_i(y) = g_i^{-1}(y)$ is the inverse of $g$ restricted to the $i$-th monotone branch.

Q: Derive the pdf of $Y = X^2$ when $X$ has pdf $f_X$ (not necessarily symmetric), using the multi-branch formula.
A: The two branches give preimages $x_1(y) = \sqrt{y}$ and $x_2(y) = -\sqrt{y}$, each with $|dx/dy| = \tfrac{1}{2\sqrt{y}}$. So $f_Y(y) = \dfrac{1}{2\sqrt{y}}\left[f_X(\sqrt{y}) + f_X(-\sqrt{y})\right]$ for $y > 0$.

Q: If $X \sim \mathcal{N}(0,1)$ and $Y = X^2$, what distribution does $Y$ follow, and what is its pdf?
A: $Y \sim \chi^2_1$ (chi-squared with 1 degree of freedom). Using both branches: $f_Y(y) = \dfrac{1}{2\sqrt{y}}\cdot 2 \cdot \dfrac{1}{\sqrt{2\pi}} e^{-y/2} = \dfrac{1}{\sqrt{2\pi y}} e^{-y/2}$ for $y > 0$.

P: Find the pdf of $Y = X^2$ when $X \sim \text{Uniform}(-1, 2)$ (so $f_X(x) = 1/3$ on $[-1,2]$).

S:
**IDENTIFY**: Non-monotone transformation $g(x) = x^2$ on an asymmetric support.

**PLAN**:
- Determine range of $Y$: $X \in [-1,2] \Rightarrow Y \in [0,4]$.
- Split into regions based on which branches are active.
- Apply the multi-branch formula where both branches contribute; the single-branch formula where only one does.

**EXECUTE**:
1. For $y \in [0,1]$: both $\sqrt{y} \in [0,1] \subset [-1,2]$ and $-\sqrt{y} \in [-1,0] \subset [-1,2]$ are in the support. So $f_Y(y) = \tfrac{1}{2\sqrt{y}}[f_X(\sqrt{y}) + f_X(-\sqrt{y})] = \tfrac{1}{2\sqrt{y}} \cdot \tfrac{2}{3} = \tfrac{1}{3\sqrt{y}}$.
2. For $y \in (1,4]$: only $\sqrt{y} \in (1,2]$ is in the support; $-\sqrt{y} \notin [-1,2]$. So $f_Y(y) = \tfrac{1}{2\sqrt{y}} \cdot \tfrac{1}{3} = \tfrac{1}{6\sqrt{y}}$.

**EVALUATE**:
- Check total: $\int_0^1 \tfrac{1}{3\sqrt{y}}\, dy + \int_1^4 \tfrac{1}{6\sqrt{y}}\, dy = \tfrac{2}{3} + \tfrac{1}{3} = 1$ ✓.
- The density is larger on $[0,1]$ because both branches contribute there.

## 10.7 Linear Transformation $Y = aX + b$

Q: Why is $Y = aX + b$ the most important transformation in practice?
A: Linear transformations appear constantly (unit changes, standardization, affine rescaling of measurements) and yield a clean closed-form density. Standardization $Z = (X - \mu)/\sigma$ is a special case that underlies the entire framework of z-scores.

C: If $Y = aX + b$ with $a \neq 0$, then $f_Y(y) = [\dfrac{1}{|a|}\, f_X\!\left(\dfrac{y - b}{a}\right)]$, where $f_X$ is the pdf of $X$.

Q: Why does the factor $1/|a|$ appear in the pdf of $Y = aX + b$?
A: Stretching the $x$-axis by factor $|a|$ spreads the same total probability over a wider interval, so the density must shrink by $1/|a|$ to keep the total area equal to 1. The absolute value handles negative $a$ (reflection).

Q: If $X \sim \mathcal{N}(\mu, \sigma^2)$ and $Y = aX + b$ with $a \neq 0$, what is the distribution of $Y$?
A: $Y \sim \mathcal{N}(a\mu + b,\; a^2\sigma^2)$. Linear transformations preserve normality; the mean shifts by the linear map and the variance scales by $a^2$.

C: If $X \sim \mathcal{N}(\mu, \sigma^2)$, then $Z = (X - \mu)/\sigma$ is called the [standard score] (or z-score) and has distribution $\mathcal{N}(0,1)$.

## 10.8 Joint Transformations — Jacobian Method

Q: Why do we need a Jacobian when transforming two random variables jointly?
A: A map $(X,Y) \mapsto (U,V)$ can stretch or compress areas differently in different directions. The Jacobian determinant measures the local area scaling factor, playing the same role for joint densities that $|g^{-1\prime}(y)|$ plays for a single variable.

C: For a differentiable invertible map $(x, y) = T^{-1}(u, v)$, the [Jacobian matrix] is $J = \begin{pmatrix} \partial x/\partial u & \partial x/\partial v \\ \partial y/\partial u & \partial y/\partial v \end{pmatrix}$, where $(u,v) = T(x,y)$ defines the new variables.

C: The [Jacobian determinant] $|J|$ of $T^{-1}$ at $(u,v)$ is $|\det J|$, representing the local area scaling factor of the inverse map at $(u,v)$.

C: [Jacobian method] for joint transformations: if $(U,V) = T(X,Y)$ is invertible and differentiable, then $f_{U,V}(u,v) = f_{X,Y}(x(u,v),\, y(u,v))\,|J|$, where $|J|$ is the Jacobian determinant of $T^{-1}$.

P: Let $X, Y$ be independent with joint density $f_{X,Y}(x,y) = e^{-(x+y)}$ on $x,y \ge 0$. Find the joint density of $U = X + Y$, $V = X/(X+Y)$.

S:
**IDENTIFY**: Joint transformation of two RVs; use the Jacobian method.

**PLAN**:
- Solve for $(x,y)$ in terms of $(u,v)$.
- Compute the Jacobian determinant of $T^{-1}$.
- Apply $f_{U,V}(u,v) = f_{X,Y}(x,y)\,|J|$.

**EXECUTE**:
1. $u = x + y$, $v = x/(x+y) \Rightarrow x = uv$, $y = u(1-v)$.
2. Jacobian: $J = \begin{pmatrix} v & u \\ 1 - v & -u \end{pmatrix}$, $\det J = -uv - u(1-v) = -u$, so $|J| = u$.
3. Support: $x,y \ge 0 \Rightarrow u \ge 0$, $v \in [0,1]$.
4. $f_{U,V}(u,v) = e^{-(uv + u(1-v))}\cdot u = u\, e^{-u}$ for $u \ge 0$, $v \in [0,1]$.

**EVALUATE**:
- The density factors: $f_{U,V}(u,v) = (u e^{-u}) \cdot 1$, so $U \sim \text{Gamma}(2,1)$ and $V \sim \text{Uniform}(0,1)$, and they are independent.
- This is the well-known beta–gamma decomposition.

Q: In the Jacobian method, why must $T$ be invertible on the support?
A: The change-of-variables formula expresses $f_{U,V}$ using the inverse map $T^{-1}$. If $T$ is not invertible, a single $(u,v)$ has multiple preimages and we need a branches-style formula analogous to the non-monotone 1D case.

## 10.9 Sums of Independent Random Variables — Convolution

Q: Why does adding independent random variables convolve their densities?
A: For independent $X, Y$, computing $P(X + Y \le z)$ requires integrating the joint pdf $f_X(x)f_Y(y)$ over the half-plane $\{x + y \le z\}$. Slicing this region parallel to the $y$-axis leads to an integral of the form $\int f_X(x) f_Y(z - x)\, dx$, which is the convolution.

C: If $X$ and $Y$ are independent continuous RVs with pdfs $f_X$ and $f_Y$, then $Z = X + Y$ has pdf $f_Z(z) = [\int_{-\infty}^{\infty} f_X(x)\, f_Y(z - x)\, dx]$, called the convolution $f_X * f_Y$.

Q: Derive the convolution formula starting from $F_Z(z) = P(X + Y \le z)$.
A: $F_Z(z) = \iint_{x + y \le z} f_X(x) f_Y(y)\, dx\, dy = \int_{-\infty}^{\infty} f_X(x) \int_{-\infty}^{z - x} f_Y(y)\, dy\, dx = \int_{-\infty}^{\infty} f_X(x)\, F_Y(z - x)\, dx$. Differentiating under the integral gives $f_Z(z) = \int_{-\infty}^{\infty} f_X(x)\, f_Y(z - x)\, dx$.

Q: Why does independence matter in the convolution formula?
A: The derivation uses $f_{X,Y}(x,y) = f_X(x) f_Y(y)$, which requires independence. Without it, we would need to integrate the full joint density $f_{X,Y}(x, z-x)$ and no simple product form exists.

P: Let $X, Y \stackrel{iid}{\sim} \text{Exp}(\lambda)$. Find the pdf of $Z = X + Y$ using convolution.

S:
**IDENTIFY**: Sum of two independent exponentials; use the convolution formula.

**PLAN**:
- Write $f_Z(z) = \int f_X(x) f_Y(z - x)\, dx$.
- Integrate only over the region where both $f_X(x)$ and $f_Y(z - x)$ are nonzero, i.e., $x \ge 0$ and $z - x \ge 0 \Rightarrow 0 \le x \le z$.

**EXECUTE**:
1. $f_Z(z) = \int_0^z \lambda e^{-\lambda x}\, \lambda e^{-\lambda(z - x)}\, dx$ for $z \ge 0$.
2. The exponents combine: $e^{-\lambda x - \lambda z + \lambda x} = e^{-\lambda z}$.
3. $f_Z(z) = \lambda^2 e^{-\lambda z} \int_0^z 1\, dx = \lambda^2 z\, e^{-\lambda z}$.

**EVALUATE**:
- $Z \sim \text{Gamma}(2, \lambda)$ — sum of $n$ iid exponentials is Gamma$(n, \lambda)$.
- Check: $\int_0^\infty \lambda^2 z\, e^{-\lambda z}\, dz = 1$ ✓ (Gamma function identity).

Q: If $X \sim \mathcal{N}(\mu_X, \sigma_X^2)$ and $Y \sim \mathcal{N}(\mu_Y, \sigma_Y^2)$ are independent, what is the distribution of $X + Y$?
A: $X + Y \sim \mathcal{N}(\mu_X + \mu_Y,\; \sigma_X^2 + \sigma_Y^2)$. The sum is normal with means adding and variances adding; this can be shown by convolution or more cleanly via moment generating functions.

## 10.10 Order Statistics

Q: Why study order statistics?
A: Many statistics (sample min, sample max, median, range) are functions of the sorted sample, not the original order of observations. Their distributions underlie reliability analysis (weakest link = minimum), extreme-value theory (maximum), and nonparametric methods.

C: Given iid RVs $X_1, \ldots, X_n$, the [$k$-th order statistic] $X_{(k)}$ is the $k$-th smallest value: $X_{(1)} \le X_{(2)} \le \cdots \le X_{(n)}$.

C: The sample minimum is $X_{(1)}$, and the sample maximum is $[X_{(n)}]$.

Q: For iid $X_1, \ldots, X_n$ with CDF $F$, derive the CDF of the maximum $X_{(n)}$.
A: $F_{X_{(n)}}(x) = P(\max_i X_i \le x) = P(\text{every } X_i \le x) = \prod_i P(X_i \le x) = [F(x)]^n$, using independence and the fact that the maximum is $\le x$ iff every $X_i$ is $\le x$.

Q: For iid $X_1, \ldots, X_n$ with CDF $F$, derive the CDF of the minimum $X_{(1)}$.
A: $F_{X_{(1)}}(x) = P(X_{(1)} \le x) = 1 - P(\min_i X_i > x) = 1 - P(\text{every } X_i > x) = 1 - [1 - F(x)]^n$.

C: For iid $X_1,\ldots,X_n$ with pdf $f$, the pdf of the maximum is $f_{X_{(n)}}(x) = [n\, f(x)\, [F(x)]^{n-1}]$.

C: For iid $X_1,\ldots,X_n$ with pdf $f$, the pdf of the minimum is $f_{X_{(1)}}(x) = [n\, f(x)\, [1 - F(x)]^{n-1}]$.

C: For iid $X_1,\ldots,X_n$ with pdf $f$ and CDF $F$, the pdf of the $k$-th order statistic is $f_{X_{(k)}}(x) = \dfrac{n!}{(k-1)!\,(n-k)!}\,[F(x)]^{k-1}\,[1 - F(x)]^{n-k}\,f(x)$, where the [combinatorial factor] counts arrangements of $k-1$ values below $x$, one at $x$, and $n-k$ above.

Q: Intuitively, why does the $k$-th order statistic pdf contain the factor $[F(x)]^{k-1}[1-F(x)]^{n-k} f(x)$?
A: For $X_{(k)}$ to be near $x$, we need exactly one observation at $x$ (contributes $f(x)\,dx$), $k-1$ observations below $x$ (each contributes factor $F(x)$), and $n - k$ observations above $x$ (each contributes $1 - F(x)$). The multinomial coefficient counts the ways to assign labels.

P: Let $X_1, \ldots, X_n \stackrel{iid}{\sim} \text{Uniform}(0,1)$. Find the pdf of the sample maximum $X_{(n)}$.

S:
**IDENTIFY**: Order statistic for uniform sample; use the max pdf formula.

**PLAN**:
- $f(x) = 1$ and $F(x) = x$ on $[0,1]$.
- Apply $f_{X_{(n)}}(x) = n f(x) [F(x)]^{n-1}$.

**EXECUTE**:
1. $f_{X_{(n)}}(x) = n \cdot 1 \cdot x^{n-1} = n\, x^{n-1}$ for $x \in [0,1]$.

**EVALUATE**:
- This is the $\text{Beta}(n, 1)$ density.
- Expected max: $E[X_{(n)}] = \int_0^1 x \cdot n x^{n-1}\, dx = \tfrac{n}{n+1} \to 1$ as $n \to \infty$ ✓ (intuitive: more samples push the max closer to 1).

## 10.11 Simulation by Inverse CDF Method

Q: Why is the inverse CDF method the foundational simulation technique?
A: Every computer can generate uniform$(0,1)$ random numbers easily. The inverse CDF method transforms those uniforms into samples from any continuous distribution whose CDF we can invert — turning one generator into infinitely many.

C: [Inverse CDF method] (probability integral transform): if $U \sim \text{Uniform}(0,1)$ and $F$ is a continuous strictly increasing CDF, then $X = F^{-1}(U)$ has distribution $F$.

Q: Prove that $X = F^{-1}(U)$ has CDF $F$ when $U \sim \text{Uniform}(0,1)$ and $F$ is continuous and strictly increasing.
A: $P(X \le x) = P(F^{-1}(U) \le x) = P(U \le F(x)) = F(x)$, using that $F$ is strictly increasing (so $F^{-1}(U) \le x \iff U \le F(x)$) and that $U$ is uniform (so $P(U \le u) = u$).

Q: Conversely, if $X$ has continuous strictly increasing CDF $F$, what is the distribution of $F(X)$?
A: $F(X) \sim \text{Uniform}(0,1)$. This is the probability integral transform: applying a continuous CDF to its own random variable yields a uniform — the basis of p-values and goodness-of-fit tests.

P: Show how to simulate $X \sim \text{Exp}(\lambda)$ from $U \sim \text{Uniform}(0,1)$.

S:
**IDENTIFY**: Simulation problem; apply the inverse CDF method to the exponential.

**PLAN**:
- Write down CDF $F$ of $\text{Exp}(\lambda)$.
- Invert to obtain $F^{-1}$.
- Set $X = F^{-1}(U)$.

**EXECUTE**:
1. CDF: $F(x) = 1 - e^{-\lambda x}$ for $x \ge 0$.
2. Solve $u = 1 - e^{-\lambda x}$ for $x$: $e^{-\lambda x} = 1 - u \Rightarrow x = -\tfrac{1}{\lambda}\ln(1 - u)$.
3. So $X = -\tfrac{1}{\lambda}\ln(1 - U)$. Equivalently, $X = -\tfrac{1}{\lambda}\ln U$ since $1 - U \sim \text{Uniform}(0,1)$ as well.

**EVALUATE**:
- Verify: $P(X \le x) = P(-\tfrac{1}{\lambda}\ln U \le x) = P(\ln U \ge -\lambda x) = P(U \ge e^{-\lambda x}) = 1 - e^{-\lambda x}$ ✓.
- This one-liner is how exponential samples are generated in most numerical libraries.

Q: When does the inverse CDF method fail or become impractical?
A: When $F$ cannot be inverted in closed form (e.g., the standard normal, whose CDF is $\Phi$ has no elementary inverse). In practice we use numerical inversion or specialized algorithms (Box–Muller, rejection sampling) for such distributions.
