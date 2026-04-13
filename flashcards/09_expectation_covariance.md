+++
order = 9
tags = ["math", "probability", "expectation", "variance", "covariance", "correlation"]
+++

# Probability — Expectation, Covariance, Correlation

## 9.1 Why develop more expectation theory?

Q: Why do we need more expectation theory beyond the basic definition $E[X] = \sum x\,p(x)$ or $\int x\,f(x)\,dx$?
A: Real problems involve multiple interacting random variables — sums, products, and combinations. Computing $E[X+Y]$ or $\mathrm{Var}(X+Y)$ directly from joint densities is often painful or impossible when the distribution of the sum is unknown. Linearity of expectation and covariance identities let us bypass the joint distribution entirely and compute key quantities from marginal moments alone.

Q: Why is it useful that linearity of expectation holds even without independence?
A: Independence is a strong and often unverifiable assumption. The fact that $E[X+Y] = E[X] + E[Y]$ holds for any random variables — even dependent ones — makes expectation one of the most powerful general-purpose tools in probability. It lets us compute averages of sums without ever solving the harder joint-distribution problem.

Q: Why introduce covariance and correlation at all?
A: Variance of a sum depends on how the summands move together, not just on their individual variances. Covariance measures the "co-movement" of two random variables, and correlation standardizes it to a dimensionless number in $[-1, 1]$ so we can compare relationships across different scales and units.

## 9.2 Linearity of expectation

Q: State the linearity of expectation for two random variables.
A: For any random variables $X$ and $Y$ with finite expectations and any constants $a, b \in \mathbb{R}$, $E[aX + bY] = a\,E[X] + b\,E[Y]$. No independence assumption is needed — this holds even when $X$ and $Y$ are strongly dependent.

C: [Linearity of expectation] states that $E[aX + bY] = a\,E[X] + b\,E[Y]$ for any random variables $X, Y$ and constants $a, b$, with no independence required.

Q: Why does linearity of expectation hold without independence?
A: Expectation is an integral (or sum) weighted by the joint distribution, and integration is a linear operation: $\int (ax + by)\,f(x,y)\,dx\,dy = a\int x\,f + b\int y\,f$. The joint density $f(x,y)$ may encode arbitrary dependence, but that dependence cancels out when we split the linear integrand.

C: For any constant $c$, $E[c] = [c]$ — the expectation of a constant equals the constant itself.

C: For any random variable $X$ and constant $c$, $E[cX] = [c\,E[X]]$.

Q: Generalize linearity to $n$ random variables.
A: For any random variables $X_1, \ldots, X_n$ with finite expectations and any constants $a_1, \ldots, a_n$, $E\!\left[\sum_{i=1}^n a_i X_i\right] = \sum_{i=1}^n a_i\,E[X_i]$. Dependence among the $X_i$ is irrelevant.

Q: If $X$ and $Y$ are dependent, is $E[X + Y] = E[X] + E[Y]$ still true?
A: Yes. Linearity of expectation requires no independence assumption whatsoever; it follows purely from linearity of integration/summation. Only variance (and higher moments) of sums depend on independence.

## 9.3 Expectation of a product for independent RVs

Q: For independent random variables $X$ and $Y$, what is $E[XY]$?
A: $E[XY] = E[X]\,E[Y]$. The expectation of the product factors into the product of expectations precisely because independence lets the joint density factor as $f(x,y) = f_X(x) f_Y(y)$.

C: If $X$ and $Y$ are independent, then $E[XY] = [E[X]\,E[Y]]$.

Q: Why does $E[XY] = E[X]E[Y]$ require independence, while $E[X+Y] = E[X]+E[Y]$ does not?
A: The sum $X+Y$ is a linear function, so linearity of the expectation operator suffices. The product $XY$ is nonlinear, and splitting $E[XY]$ into $E[X]E[Y]$ requires the joint density to factor — which is exactly what independence gives: $f_{X,Y}(x,y) = f_X(x) f_Y(y)$.

Q: Is $E[XY] = E[X]E[Y]$ sufficient for $X$ and $Y$ to be independent?
A: No. The equality $E[XY] = E[X]E[Y]$ defines "uncorrelated," a strictly weaker condition. Independence requires $f_{X,Y}(x,y) = f_X(x) f_Y(y)$ everywhere, which constrains all joint probabilities — not just one expectation.

Q: If $X$ and $Y$ are independent, what is $E[g(X)\,h(Y)]$ for functions $g, h$?
A: $E[g(X)\,h(Y)] = E[g(X)]\,E[h(Y)]$. Independence of $X$ and $Y$ implies independence of any functions of them separately, so the factoring extends to arbitrary transformations.

## 9.4 Variance of a sum

C: The variance of a sum of two random variables satisfies $\mathrm{Var}(X+Y) = [\mathrm{Var}(X) + \mathrm{Var}(Y) + 2\,\mathrm{Cov}(X,Y)]$, where $\mathrm{Cov}(X,Y)$ measures how $X$ and $Y$ co-vary.

Q: Why does $\mathrm{Var}(X+Y)$ depend on a covariance term, unlike $E[X+Y]$?
A: Variance measures squared deviation from the mean: $\mathrm{Var}(X+Y) = E[((X-\mu_X) + (Y-\mu_Y))^2]$. Expanding the square produces the two individual variance terms plus a cross term $2\,E[(X-\mu_X)(Y-\mu_Y)]$ — which is exactly $2\,\mathrm{Cov}(X,Y)$. This cross term captures how the deviations of $X$ and $Y$ move together.

Q: Derive $\mathrm{Var}(X+Y) = \mathrm{Var}(X) + \mathrm{Var}(Y) + 2\,\mathrm{Cov}(X,Y)$.
A: Let $\mu_X = E[X]$, $\mu_Y = E[Y]$. Then $\mathrm{Var}(X+Y) = E[(X+Y - \mu_X - \mu_Y)^2] = E[((X-\mu_X) + (Y-\mu_Y))^2]$. Expanding the square: $E[(X-\mu_X)^2] + E[(Y-\mu_Y)^2] + 2\,E[(X-\mu_X)(Y-\mu_Y)] = \mathrm{Var}(X) + \mathrm{Var}(Y) + 2\,\mathrm{Cov}(X,Y)$.

Q: When does $\mathrm{Var}(X+Y) = \mathrm{Var}(X) + \mathrm{Var}(Y)$?
A: When $\mathrm{Cov}(X,Y) = 0$ — i.e., when $X$ and $Y$ are uncorrelated. Independence implies zero covariance, so independence is a sufficient (but not necessary) condition for the variances to simply add.

C: If $X$ and $Y$ are independent, then $\mathrm{Var}(X+Y) = [\mathrm{Var}(X) + \mathrm{Var}(Y)]$.

Q: What is $\mathrm{Var}(X - Y)$ in terms of variances and covariance?
A: $\mathrm{Var}(X-Y) = \mathrm{Var}(X) + \mathrm{Var}(Y) - 2\,\mathrm{Cov}(X,Y)$. The minus sign on $Y$ flips the sign of the cross term but not the $\mathrm{Var}(Y)$ term, because $\mathrm{Var}(-Y) = \mathrm{Var}(Y)$.

Q: Why is $\mathrm{Var}(X - Y) = \mathrm{Var}(X) + \mathrm{Var}(Y)$ (not minus) when $X, Y$ are independent?
A: Variance is always nonnegative and invariant under sign flips: $\mathrm{Var}(-Y) = (-1)^2 \mathrm{Var}(Y) = \mathrm{Var}(Y)$. So independent subtraction still adds variances — the uncertainties compound rather than cancel.

## 9.5 Definition of covariance

C: The [covariance] of random variables $X$ and $Y$ is defined as $\mathrm{Cov}(X,Y) = E[(X - \mu_X)(Y - \mu_Y)]$, where $\mu_X = E[X]$ and $\mu_Y = E[Y]$.

C: The computational formula for covariance is $\mathrm{Cov}(X,Y) = [E[XY] - E[X]\,E[Y]]$, where $E[XY]$ is the expectation of the product.

Q: Derive the computational formula $\mathrm{Cov}(X,Y) = E[XY] - E[X]E[Y]$.
A: Expand the definition: $\mathrm{Cov}(X,Y) = E[(X-\mu_X)(Y-\mu_Y)] = E[XY - \mu_X Y - \mu_Y X + \mu_X \mu_Y]$. By linearity of expectation, this equals $E[XY] - \mu_X E[Y] - \mu_Y E[X] + \mu_X \mu_Y = E[XY] - \mu_X \mu_Y - \mu_Y \mu_X + \mu_X \mu_Y = E[XY] - E[X]E[Y]$.

Q: What does the sign of $\mathrm{Cov}(X,Y)$ tell you intuitively?
A: Positive covariance means $X$ and $Y$ tend to deviate from their means in the same direction (both above or both below). Negative covariance means they deviate in opposite directions. Zero covariance means deviations have no consistent linear relationship.

Q: Why do we subtract the means in the covariance definition?
A: Subtracting $\mu_X$ and $\mu_Y$ centers the variables at zero, so the product $(X-\mu_X)(Y-\mu_Y)$ is positive exactly when $X$ and $Y$ are on the same side of their means. Without centering, $E[XY]$ would conflate mean location with co-movement, making the quantity uninformative about dependence.

C: Covariance has units of [the product of the units of $X$ and $Y$] (e.g., $\text{meters} \cdot \text{seconds}$ if $X$ is a length and $Y$ a time).

## 9.6 Properties of covariance

C: Covariance is [symmetric]: $\mathrm{Cov}(X,Y) = \mathrm{Cov}(Y,X)$.

C: The covariance of a random variable with itself is its variance: $\mathrm{Cov}(X,X) = [\mathrm{Var}(X)]$.

Q: Why is $\mathrm{Cov}(X,X) = \mathrm{Var}(X)$?
A: From the definition, $\mathrm{Cov}(X,X) = E[(X-\mu_X)(X-\mu_X)] = E[(X-\mu_X)^2]$, which is precisely the definition of variance. So variance is a special case of covariance.

C: Covariance is [bilinear]: $\mathrm{Cov}(aX + bY,\, Z) = a\,\mathrm{Cov}(X,Z) + b\,\mathrm{Cov}(Y,Z)$ for constants $a, b$.

Q: State the full bilinearity property of covariance.
A: For constants $a, b, c, d$ and random variables $X, Y, Z, W$: $\mathrm{Cov}(aX + bY,\, cZ + dW) = ac\,\mathrm{Cov}(X,Z) + ad\,\mathrm{Cov}(X,W) + bc\,\mathrm{Cov}(Y,Z) + bd\,\mathrm{Cov}(Y,W)$. Covariance is linear in each argument separately.

Q: What is $\mathrm{Cov}(X, c)$ where $c$ is a constant?
A: Zero. A constant has no deviation from its mean ($c - E[c] = c - c = 0$), so $\mathrm{Cov}(X, c) = E[(X-\mu_X)(c-c)] = E[0] = 0$.

C: For any constant $c$ and random variable $X$, $\mathrm{Cov}(X + c,\, Y) = [\mathrm{Cov}(X, Y)]$ — adding a constant shifts $X$ but leaves its covariance with $Y$ unchanged.

Q: Why is covariance unchanged when you add a constant to one of the variables?
A: Adding a constant shifts the variable's mean by the same amount, so the deviation $X - \mu_X$ is unaffected: $(X + c) - (\mu_X + c) = X - \mu_X$. Covariance depends only on deviations from the mean, so constant shifts cancel out.

C: For constants $a, b$, $\mathrm{Cov}(aX, bY) = [ab\,\mathrm{Cov}(X,Y)]$.

## 9.7 Independence and zero covariance

Q: If $X$ and $Y$ are independent, what is $\mathrm{Cov}(X,Y)$?
A: Zero. Independence gives $E[XY] = E[X]E[Y]$, so $\mathrm{Cov}(X,Y) = E[XY] - E[X]E[Y] = 0$. Independent variables are always uncorrelated.

C: [Independence implies zero covariance]: if $X$ and $Y$ are independent, then $\mathrm{Cov}(X,Y) = 0$.

Q: Does zero covariance imply independence?
A: No — this is the most important subtlety in the whole chapter. Zero covariance only says $X$ and $Y$ have no linear relationship. They can still be strongly dependent through nonlinear relationships (e.g., $Y = X^2$ with $X$ symmetric about zero gives $\mathrm{Cov}(X,Y) = 0$ yet $Y$ is a deterministic function of $X$).

Q: Give an example where $\mathrm{Cov}(X,Y) = 0$ but $X$ and $Y$ are dependent.
A: Let $X$ be uniform on $\{-1, 0, 1\}$ and $Y = X^2$. Then $E[X] = 0$ and $E[XY] = E[X \cdot X^2] = E[X^3] = 0$ (odd function, symmetric distribution), so $\mathrm{Cov}(X,Y) = 0$. But $Y$ is completely determined by $X$, so they are maximally dependent.

Q: Why does zero covariance fail to imply independence?
A: Covariance captures only the linear component of the relationship between $X$ and $Y$. A symmetric nonlinear relationship (like $Y = X^2$ with $X$ symmetric) can have deviations $X - \mu_X$ and $Y - \mu_Y$ that multiply to a product whose expectation cancels to zero, even though $Y$ is perfectly determined by $X$.

C: Two random variables $X$ and $Y$ are called [uncorrelated] if $\mathrm{Cov}(X,Y) = 0$, which is equivalent to $E[XY] = E[X]E[Y]$.

Q: What is the logical relationship between "independent" and "uncorrelated"?
A: Independent $\Rightarrow$ uncorrelated, but uncorrelated $\not\Rightarrow$ independent. Independence is strictly stronger: it requires $f_{X,Y} = f_X f_Y$ for all outcomes, while uncorrelatedness only constrains one scalar (the covariance) to be zero.

## 9.8 Correlation

C: The [correlation coefficient] of $X$ and $Y$ is $\rho_{X,Y} = \dfrac{\mathrm{Cov}(X,Y)}{\sigma_X \sigma_Y}$, where $\sigma_X = \sqrt{\mathrm{Var}(X)}$ and $\sigma_Y = \sqrt{\mathrm{Var}(Y)}$ are the standard deviations.

Q: Why standardize covariance into correlation?
A: Covariance has units (product of the units of $X$ and $Y$) and its magnitude depends on the scales of the variables. Dividing by $\sigma_X \sigma_Y$ produces a dimensionless quantity in $[-1, 1]$, so correlations are comparable across different variables and units.

C: The correlation coefficient is bounded: $|\rho_{X,Y}| \leq [1]$.

Q: What does $\rho_{X,Y} = 1$ mean?
A: $X$ and $Y$ are perfectly positively linearly related: $Y = aX + b$ for some constants $a > 0$ and $b$. Every increase in $X$ by a standard deviation corresponds to an increase in $Y$ by its standard deviation.

Q: What does $\rho_{X,Y} = -1$ mean?
A: $X$ and $Y$ are perfectly negatively linearly related: $Y = aX + b$ for some $a < 0$ and $b$. The variables move in exactly opposite directions along a line.

Q: What does $\rho_{X,Y} = 0$ mean?
A: $X$ and $Y$ are uncorrelated — they have no linear relationship. They may still be nonlinearly dependent (as in the $Y = X^2$ example), so $\rho = 0$ is not the same as independence.

Q: Why is correlation invariant under positive linear transformations of $X$ and $Y$?
A: Let $X' = aX + b$ and $Y' = cY + d$ with $a, c > 0$. Then $\mathrm{Cov}(X', Y') = ac\,\mathrm{Cov}(X,Y)$ and $\sigma_{X'} \sigma_{Y'} = |a||c|\sigma_X \sigma_Y = ac\,\sigma_X \sigma_Y$. The $ac$ factors cancel, so $\rho_{X',Y'} = \rho_{X,Y}$. This scale invariance is exactly why correlation is useful across different units.

## 9.9 Cauchy–Schwarz inequality for expectations

C: The [Cauchy–Schwarz inequality] for expectations states that $(E[XY])^2 \leq E[X^2]\,E[Y^2]$, with equality if and only if $Y = cX$ almost surely for some constant $c$ (or one of them is zero).

Q: How does the Cauchy–Schwarz inequality prove $|\rho_{X,Y}| \leq 1$?
A: Apply Cauchy–Schwarz to the centered variables $X' = X - \mu_X$ and $Y' = Y - \mu_Y$: $(E[X'Y'])^2 \leq E[X'^2]\,E[Y'^2]$, i.e., $\mathrm{Cov}(X,Y)^2 \leq \mathrm{Var}(X)\,\mathrm{Var}(Y)$. Dividing both sides by $\mathrm{Var}(X)\mathrm{Var}(Y)$ gives $\rho^2 \leq 1$, so $|\rho| \leq 1$.

Q: When does $|\rho_{X,Y}| = 1$?
A: When Cauchy–Schwarz becomes an equality, i.e., when $Y - \mu_Y = c(X - \mu_X)$ almost surely for some constant $c \neq 0$. Equivalently, $Y$ is an exact linear function of $X$: $Y = aX + b$ for some $a, b$.

Q: Why does equality in Cauchy–Schwarz correspond to a perfect linear relationship?
A: Cauchy–Schwarz is saturated only when the two "vectors" (here, the centered random variables viewed in the inner-product space $L^2$) are scalar multiples of each other. "$Y' = cX'$ almost surely" is exactly the statement that $Y$ is a deterministic linear function of $X$ — no random scatter remains.

## 9.10 Variance of a linear combination

C: For random variables $X_1, \ldots, X_n$ and constants $a_1, \ldots, a_n$, $\mathrm{Var}\!\left(\sum_{i=1}^n a_i X_i\right) = [\sum_{i=1}^n a_i^2 \mathrm{Var}(X_i) + 2\sum_{i<j} a_i a_j \mathrm{Cov}(X_i, X_j)]$.

Q: Derive the variance formula for a linear combination $\sum a_i X_i$.
A: $\mathrm{Var}(\sum a_i X_i) = \mathrm{Cov}(\sum a_i X_i, \sum a_j X_j)$ by the $\mathrm{Cov}(X,X) = \mathrm{Var}(X)$ identity. By bilinearity, this expands to $\sum_i \sum_j a_i a_j \mathrm{Cov}(X_i, X_j)$. Separating diagonal terms ($i=j$, giving $a_i^2 \mathrm{Var}(X_i)$) from off-diagonal pairs (which appear twice by symmetry, giving $2 a_i a_j \mathrm{Cov}(X_i, X_j)$ for $i < j$) produces the stated formula.

Q: If $X_1, \ldots, X_n$ are pairwise uncorrelated, what is $\mathrm{Var}(\sum a_i X_i)$?
A: $\mathrm{Var}(\sum a_i X_i) = \sum_{i=1}^n a_i^2 \mathrm{Var}(X_i)$. All covariance cross terms vanish, so only the diagonal contributions survive. Pairwise uncorrelatedness is sufficient — full mutual independence is not required.

Q: What is $\mathrm{Var}(aX + b)$ for constants $a, b$ and random variable $X$?
A: $\mathrm{Var}(aX + b) = a^2\,\mathrm{Var}(X)$. The constant $b$ contributes nothing (adding a constant doesn't change spread), and the scaling $a$ gets squared because variance is a squared quantity.

C: For a constant $b$, $\mathrm{Var}(X + b) = [\mathrm{Var}(X)]$ — additive shifts leave variance unchanged.

Q: Why does $\mathrm{Var}(aX) = a^2\mathrm{Var}(X)$ instead of $|a|\mathrm{Var}(X)$?
A: Variance is defined as the expectation of a squared deviation: $\mathrm{Var}(aX) = E[(aX - a\mu_X)^2] = E[a^2(X - \mu_X)^2] = a^2 \mathrm{Var}(X)$. The square guarantees the $a$ is squared, which is also why standard deviation (the square root) scales by $|a|$.

## 9.11 Sample mean of iid RVs

C: Let $X_1, \ldots, X_n$ be independent and identically distributed (iid) with $E[X_i] = \mu$ and $\mathrm{Var}(X_i) = \sigma^2$. The [sample mean] is defined as $\bar{X}_n = \frac{1}{n}\sum_{i=1}^n X_i$.

Q: What is $E[\bar{X}_n]$ for iid random variables with mean $\mu$?
A: $E[\bar{X}_n] = \mu$. By linearity of expectation, $E[\frac{1}{n}\sum X_i] = \frac{1}{n}\sum E[X_i] = \frac{1}{n} \cdot n\mu = \mu$. The sample mean is an unbiased estimator of the population mean.

Q: What is $\mathrm{Var}(\bar{X}_n)$ for iid random variables with variance $\sigma^2$?
A: $\mathrm{Var}(\bar{X}_n) = \sigma^2 / n$. Since the $X_i$ are independent, $\mathrm{Var}(\sum X_i) = n\sigma^2$, and $\mathrm{Var}(\frac{1}{n}\sum X_i) = \frac{1}{n^2} \cdot n\sigma^2 = \sigma^2/n$.

Q: Derive $\mathrm{Var}(\bar{X}_n) = \sigma^2/n$ from the linear-combination variance formula.
A: Write $\bar{X}_n = \sum_{i=1}^n \frac{1}{n} X_i$, a linear combination with $a_i = 1/n$. By independence, all covariance terms vanish: $\mathrm{Var}(\bar{X}_n) = \sum_{i=1}^n (1/n)^2 \mathrm{Var}(X_i) = \frac{1}{n^2} \cdot n\sigma^2 = \sigma^2/n$.

C: For iid $X_1, \ldots, X_n$ with variance $\sigma^2$, the standard deviation of the sample mean is $\sigma_{\bar{X}_n} = [\sigma/\sqrt{n}]$.

Q: Why does the standard deviation of the sample mean shrink like $1/\sqrt{n}$ rather than $1/n$?
A: Variance of the sum grows linearly in $n$ (as $n\sigma^2$), so dividing by $n$ in the mean yields $\sigma^2/n$ for the variance. Taking the square root to get standard deviation produces $\sigma/\sqrt{n}$. This $\sqrt{n}$ scaling is the foundation of the central limit theorem and why quadrupling sample size only halves the standard error.

Q: Why does iid-ness (rather than just identical distribution) matter for $\mathrm{Var}(\bar{X}_n) = \sigma^2/n$?
A: Without independence, the covariance cross terms $\mathrm{Cov}(X_i, X_j)$ may be nonzero and contribute to $\mathrm{Var}(\bar{X}_n)$. For example, if all $X_i$ are perfectly correlated ($X_i = X_1$), then $\mathrm{Var}(\bar{X}_n) = \mathrm{Var}(X_1) = \sigma^2$, with no $1/n$ shrinkage at all.

P: Let $X$ and $Y$ be random variables with $E[X] = 2$, $E[Y] = -1$, $\mathrm{Var}(X) = 4$, $\mathrm{Var}(Y) = 9$, and $\mathrm{Cov}(X, Y) = -3$. Compute $E[3X - 2Y + 5]$, $\mathrm{Var}(3X - 2Y + 5)$, and $\rho_{X,Y}$.

S:
**IDENTIFY**: Linear combination of two correlated random variables — need linearity of expectation, the variance-of-linear-combination formula, and the correlation definition.

**PLAN**:
- Apply $E[aX + bY + c] = a\,E[X] + b\,E[Y] + c$.
- Apply $\mathrm{Var}(aX + bY + c) = a^2\mathrm{Var}(X) + b^2\mathrm{Var}(Y) + 2ab\,\mathrm{Cov}(X,Y)$ (the constant $c$ drops out).
- Apply $\rho_{X,Y} = \mathrm{Cov}(X,Y)/(\sigma_X \sigma_Y)$.

**EXECUTE**:
1. Expectation: $E[3X - 2Y + 5] = 3(2) - 2(-1) + 5 = 6 + 2 + 5 = 13$.
2. Variance: with $a = 3$, $b = -2$, $\mathrm{Var}(3X - 2Y + 5) = 9 \cdot 4 + 4 \cdot 9 + 2(3)(-2)(-3) = 36 + 36 + 36 = 108$.
3. Correlation: $\sigma_X = 2$, $\sigma_Y = 3$, so $\rho_{X,Y} = -3/(2 \cdot 3) = -1/2$.

**EVALUATE**:
- $E = 13$, $\mathrm{Var} = 108$, $\rho = -0.5$.
- The constant $+5$ shifted the expectation but did not affect the variance, as expected.
- $|\rho| = 0.5 \leq 1$, consistent with the Cauchy–Schwarz bound.
- The cross-term $2ab\,\mathrm{Cov}$ was positive ($+36$) because both $ab = -6$ and $\mathrm{Cov} = -3$ are negative; negative correlation with opposite-sign coefficients increases the variance of the combination.

P: Let $X_1, \ldots, X_{100}$ be iid with $E[X_i] = 10$ and $\mathrm{Var}(X_i) = 25$. Find $E[\bar{X}_{100}]$ and $\mathrm{Var}(\bar{X}_{100})$, and compare the standard deviation of $\bar{X}_{100}$ to that of a single $X_i$.

S:
**IDENTIFY**: Expectation and variance of a sample mean of iid random variables.

**PLAN**:
- Use $E[\bar{X}_n] = \mu$ (linearity of expectation, no independence needed).
- Use $\mathrm{Var}(\bar{X}_n) = \sigma^2/n$ (requires independence so covariance terms vanish).
- Compare $\sigma_{\bar{X}_n} = \sigma/\sqrt{n}$ to $\sigma$.

**EXECUTE**:
1. $E[\bar{X}_{100}] = 10$.
2. $\mathrm{Var}(\bar{X}_{100}) = 25/100 = 0.25$.
3. $\sigma_{\bar{X}_{100}} = \sqrt{0.25} = 0.5$, while $\sigma_{X_i} = \sqrt{25} = 5$.

**EVALUATE**:
- The sample mean has the same center ($\mu = 10$) as each $X_i$.
- The spread is $10\times$ smaller: $\sigma_{\bar{X}} = 0.5$ vs $\sigma_{X_i} = 5$, matching the $1/\sqrt{100} = 1/10$ reduction.
- This illustrates why averaging reduces uncertainty: the mean of 100 iid samples is 10 times more concentrated than a single sample.
