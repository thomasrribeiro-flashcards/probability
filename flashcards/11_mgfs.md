+++
order = 11
tags = ["math", "probability", "mgf", "moments", "sums", "characteristic-function"]
+++

# Probability — Moment Generating Functions

## 11.1 Why MGFs?

Q: Why introduce moment generating functions at all, after already having PMFs, PDFs, and CDFs?
A: MGFs package all moments of a random variable into a single function, turn sums of independent random variables into products (which are much easier to manipulate), and uniquely identify a distribution. Each of these three uses — computing moments, analyzing sums, and identifying distributions — would justify the tool on its own.

Q: What are the three main uses of moment generating functions?
A: (1) Generating moments $E[X^n]$ via derivatives at $0$; (2) finding the distribution of a sum of independent random variables by multiplying their MGFs; (3) identifying a distribution because the MGF (when it exists in a neighborhood of $0$) determines the distribution uniquely.

Q: Before seeing the definition, predict: why might taking expectations of $e^{tX}$ be useful for extracting moments of $X$?
A: The exponential $e^{tX}$ has the Taylor expansion $1 + tX + \tfrac{(tX)^2}{2!} + \cdots$, so $E[e^{tX}] = 1 + tE[X] + \tfrac{t^2}{2!}E[X^2] + \cdots$ packages every moment $E[X^n]$ as a coefficient in $t$. Differentiating in $t$ and evaluating at $0$ picks out individual moments.

## 11.2 Definition

C: The [moment generating function] of a random variable $X$ is defined as $M_X(t) = E[e^{tX}]$, provided the expectation exists (is finite) for $t$ in some open interval containing $0$.

C: For a discrete random variable $X$ with PMF $p_X$, the MGF is $M_X(t) = [\sum_x e^{tx} p_X(x)]$, where the sum is over all values $x$ in the support of $X$.

C: For a continuous random variable $X$ with PDF $f_X$, the MGF is $M_X(t) = [\int_{-\infty}^{\infty} e^{tx} f_X(x)\, dx]$, where $f_X$ is the density of $X$.

Q: What is $M_X(0)$ for any random variable $X$?
A: $M_X(0) = E[e^{0 \cdot X}] = E[1] = 1$. Every MGF equals $1$ at $t = 0$.

Q: Why does the definition of the MGF require $E[e^{tX}]$ to exist in an open interval around $0$, not just at $t = 0$?
A: At $t = 0$ the expectation is always $1$, which gives no information. To differentiate in $t$ and extract moments, $M_X$ must be defined (and smooth) on a neighborhood of $0$. Some distributions (like the Cauchy) fail this and have no MGF in the usual sense.

## 11.3 Moments from Derivatives

Q: Why does differentiating $M_X(t)$ and evaluating at $0$ produce moments of $X$?
A: Differentiating under the expectation gives $M_X^{(n)}(t) = E[X^n e^{tX}]$. Setting $t = 0$ makes $e^{tX} = 1$, leaving $M_X^{(n)}(0) = E[X^n]$. So each moment is the corresponding derivative at the origin.

C: If the MGF $M_X$ exists in a neighborhood of $0$, then $E[X^n] = [M_X^{(n)}(0)]$, the $n$-th derivative of $M_X$ evaluated at $t = 0$.

C: In particular, $E[X] = [M_X'(0)]$ and $E[X^2] = M_X''(0)$, so the variance can be computed as $\operatorname{Var}(X) = M_X''(0) - (M_X'(0))^2$.

P: Given $M_X(t) = e^{t + t^2/2}$, find $E[X]$ and $\operatorname{Var}(X)$.

S:
**IDENTIFY**: MGF given; recover first two moments via derivatives at $0$, then compute variance.

**PLAN**:
- Compute $M_X'(t)$ and evaluate at $t = 0$ to get $E[X]$.
- Compute $M_X''(t)$ and evaluate at $t = 0$ to get $E[X^2]$.
- Use $\operatorname{Var}(X) = E[X^2] - (E[X])^2$.

**EXECUTE**:
1. Let $g(t) = t + t^2/2$, so $M_X(t) = e^{g(t)}$ with $g'(t) = 1 + t$ and $g''(t) = 1$.
2. $M_X'(t) = g'(t) e^{g(t)} = (1 + t) e^{t + t^2/2}$, so $M_X'(0) = 1 \cdot 1 = 1$. Thus $E[X] = 1$.
3. $M_X''(t) = g''(t) e^{g(t)} + (g'(t))^2 e^{g(t)} = \big(1 + (1 + t)^2\big) e^{t + t^2/2}$, so $M_X''(0) = 1 + 1 = 2$. Thus $E[X^2] = 2$.
4. $\operatorname{Var}(X) = E[X^2] - (E[X])^2 = 2 - 1 = 1$.

**EVALUATE**: $E[X] = 1$, $\operatorname{Var}(X) = 1$. (This MGF is in fact $N(1, 1)$, matching the result.)

## 11.4 Uniqueness Theorem

Q: Why is the uniqueness theorem for MGFs the key reason MGFs are useful for identifying distributions?
A: If we can compute the MGF of some unknown distribution and recognize it as the MGF of a known distribution, uniqueness tells us the two distributions are the same. Without uniqueness, matching MGFs would only give partial information.

C: [Uniqueness theorem for MGFs]: if two random variables $X$ and $Y$ have the same MGF on some open interval containing $0$, i.e. $M_X(t) = M_Y(t)$ there, then $X$ and $Y$ have the same distribution.

Q: What is the practical recipe for using the uniqueness theorem?
A: (1) Compute the MGF $M_Z(t)$ of a random variable $Z$ whose distribution is unknown; (2) recognize $M_Z(t)$ as the MGF of a known distribution; (3) conclude $Z$ has that known distribution.

Q: Why does the uniqueness theorem require the MGF to exist on a neighborhood of $0$, not just at a single point?
A: Two different distributions can agree at isolated values of $t$, so pointwise equality is not enough. Equality on an open interval pins down the analytic continuation and, ultimately, the distribution itself.

## 11.5 MGFs of Standard Distributions

C: If $X \sim \operatorname{Bernoulli}(p)$ with $P(X=1) = p$ and $P(X=0) = 1 - p$, then $M_X(t) = [1 - p + p e^{t}]$.

C: If $X \sim \operatorname{Binomial}(n, p)$ (sum of $n$ iid Bernoulli$(p)$ trials), then $M_X(t) = [(1 - p + p e^{t})^n]$.

C: If $X \sim \operatorname{Geometric}(p)$ counting trials until first success ($X \in \{1, 2, \ldots\}$ with $P(X=k) = (1-p)^{k-1} p$), then $M_X(t) = \dfrac{p e^{t}}{1 - (1-p) e^{t}}$ for $t$ such that $[(1-p) e^{t} < 1]$.

C: If $X \sim \operatorname{Poisson}(\lambda)$ with rate $\lambda > 0$, then $M_X(t) = [e^{\lambda(e^{t} - 1)}]$ for all $t \in \mathbb{R}$.

C: If $X \sim \operatorname{Uniform}(a, b)$ on the interval $[a, b]$, then $M_X(t) = \dfrac{e^{tb} - e^{ta}}{t(b-a)}$ for $t \neq 0$, with $M_X(0) = [1]$.

C: If $X \sim \operatorname{Exponential}(\lambda)$ with rate $\lambda > 0$, then $M_X(t) = \dfrac{\lambda}{\lambda - t}$ for $[t < \lambda]$.

C: If $X \sim N(\mu, \sigma^2)$ with mean $\mu$ and variance $\sigma^2$, then $M_X(t) = [e^{\mu t + \sigma^2 t^2 / 2}]$ for all $t \in \mathbb{R}$.

Q: Why does the binomial MGF equal the Bernoulli MGF raised to the $n$-th power?
A: A Binomial$(n, p)$ random variable is the sum of $n$ independent Bernoulli$(p)$ random variables. The MGF of a sum of independent random variables is the product of their MGFs, and all $n$ Bernoullis have the same MGF $1 - p + p e^{t}$, so the product is $(1 - p + p e^{t})^n$.

Q: Why does the exponential MGF $M_X(t) = \lambda / (\lambda - t)$ only exist for $t < \lambda$?
A: The integral $\int_0^{\infty} e^{tx} \lambda e^{-\lambda x}\, dx = \lambda \int_0^{\infty} e^{-(\lambda - t)x}\, dx$ converges only when $\lambda - t > 0$, i.e. $t < \lambda$. For $t \geq \lambda$ the integrand fails to decay and the expectation is infinite.

P: Derive the MGF of $X \sim \operatorname{Poisson}(\lambda)$ from the definition.

S:
**IDENTIFY**: Compute $M_X(t) = E[e^{tX}]$ for $X \sim \operatorname{Poisson}(\lambda)$ directly from the PMF $P(X = k) = e^{-\lambda} \lambda^k / k!$ for $k = 0, 1, 2, \ldots$.

**PLAN**:
- Write the sum $\sum_{k=0}^{\infty} e^{tk} P(X=k)$.
- Recognize the remaining sum as the Taylor series for $e^{\lambda e^t}$.

**EXECUTE**:
1. $M_X(t) = \sum_{k=0}^{\infty} e^{tk}\, e^{-\lambda} \frac{\lambda^k}{k!} = e^{-\lambda} \sum_{k=0}^{\infty} \frac{(\lambda e^t)^k}{k!}$.
2. The inner sum equals $e^{\lambda e^t}$ (exponential series at $\lambda e^t$).
3. So $M_X(t) = e^{-\lambda} \cdot e^{\lambda e^t} = e^{\lambda(e^t - 1)}$.

**EVALUATE**: Valid for all $t \in \mathbb{R}$, since the series converges everywhere. Checking moments: $M_X'(t) = \lambda e^t e^{\lambda(e^t-1)}$, so $M_X'(0) = \lambda = E[X]$ ✓.

## 11.6 MGF of a Linear Transformation

Q: Before deriving it, predict: if $Y = aX + b$ for constants $a, b$, how should $M_Y(t)$ relate to $M_X(t)$?
A: The constant shift $b$ should contribute a factor $e^{tb}$ (it only rescales $e^{tY}$), and the scale $a$ should appear by reading $M_X$ at the rescaled argument $at$. So we expect $M_Y(t) = e^{tb} M_X(at)$.

C: If $Y = aX + b$ for constants $a, b \in \mathbb{R}$, then $M_Y(t) = [e^{tb} M_X(at)]$, where $M_X$ is the MGF of $X$.

Q: Why does $Y = aX + b$ give $M_Y(t) = e^{tb} M_X(at)$?
A: By definition $M_Y(t) = E[e^{t(aX+b)}] = E[e^{tb} e^{(at)X}] = e^{tb} E[e^{(at)X}] = e^{tb} M_X(at)$, since $e^{tb}$ is a constant and pulls out of the expectation.

P: Given $X \sim N(0, 1)$ with MGF $M_X(t) = e^{t^2/2}$, use the linear-transformation rule to find the MGF of $Y = \sigma X + \mu$, where $\mu \in \mathbb{R}$ and $\sigma > 0$ are constants.

S:
**IDENTIFY**: Linear transformation of a random variable with known MGF.

**PLAN**: Apply $M_Y(t) = e^{tb} M_X(at)$ with $a = \sigma$ and $b = \mu$.

**EXECUTE**:
1. $M_Y(t) = e^{t\mu} M_X(\sigma t) = e^{t\mu} e^{(\sigma t)^2/2} = e^{\mu t + \sigma^2 t^2 / 2}$.

**EVALUATE**: This matches the MGF of $N(\mu, \sigma^2)$ stated in 11.5. By uniqueness, $Y \sim N(\mu, \sigma^2)$ — confirming that an affine transformation of a standard normal is normal.

## 11.7 MGF of a Sum of Independent Random Variables

Q: Why is the MGF so useful for sums of independent random variables?
A: Convolving PMFs or PDFs to find the distribution of $X + Y$ is typically a messy integral. Taking MGFs turns the sum into a product: $M_{X+Y}(t) = M_X(t) M_Y(t)$. Multiplication of simple functions is much easier than convolution, and uniqueness then identifies the resulting distribution.

C: If $X$ and $Y$ are [independent] random variables, then $M_{X+Y}(t) = M_X(t) M_Y(t)$ wherever both MGFs exist.

Q: Why does independence of $X$ and $Y$ imply $M_{X+Y}(t) = M_X(t) M_Y(t)$?
A: $M_{X+Y}(t) = E[e^{t(X+Y)}] = E[e^{tX} e^{tY}]$. Since $X$ and $Y$ are independent, so are $e^{tX}$ and $e^{tY}$, and the expectation of a product of independent random variables is the product of expectations: $E[e^{tX}] E[e^{tY}] = M_X(t) M_Y(t)$.

C: If $X_1, \ldots, X_n$ are independent, then $M_{X_1 + \cdots + X_n}(t) = [\prod_{i=1}^{n} M_{X_i}(t)]$, the product of the individual MGFs.

Q: If $X_1, \ldots, X_n$ are iid with common MGF $M(t)$, what is the MGF of $S_n = X_1 + \cdots + X_n$?
A: $M_{S_n}(t) = (M(t))^n$. All $n$ variables have the same MGF, and independence turns the sum into a product of $n$ identical factors.

## 11.8 Application: Sum of Independent Normals

Q: Before deriving it, predict what distribution the sum of two independent normal random variables should have, and why.
A: It should also be normal, with mean equal to the sum of the means and variance equal to the sum of the variances — means and variances add for sums of independent random variables, and the MGF product rule preserves the $e^{\mu t + \sigma^2 t^2 / 2}$ form.

P: Let $X \sim N(\mu_1, \sigma_1^2)$ and $Y \sim N(\mu_2, \sigma_2^2)$ be independent. Show that $X + Y \sim N(\mu_1 + \mu_2, \sigma_1^2 + \sigma_2^2)$ using MGFs.

S:
**IDENTIFY**: Identify the distribution of a sum of independent normals via MGFs and the uniqueness theorem.

**PLAN**:
- Write $M_X$ and $M_Y$ using the normal MGF.
- Multiply to get $M_{X+Y}$.
- Recognize the product as a normal MGF; apply uniqueness.

**EXECUTE**:
1. $M_X(t) = e^{\mu_1 t + \sigma_1^2 t^2 / 2}$, $M_Y(t) = e^{\mu_2 t + \sigma_2^2 t^2 / 2}$.
2. By independence, $M_{X+Y}(t) = M_X(t) M_Y(t) = e^{(\mu_1 + \mu_2) t + (\sigma_1^2 + \sigma_2^2) t^2 / 2}$.
3. This is exactly the MGF of $N(\mu_1 + \mu_2,\; \sigma_1^2 + \sigma_2^2)$.

**EVALUATE**: By uniqueness, $X + Y \sim N(\mu_1 + \mu_2, \sigma_1^2 + \sigma_2^2)$. Means and variances add, as expected.

C: If $X_1, \ldots, X_n$ are independent with $X_i \sim N(\mu_i, \sigma_i^2)$, then $\sum_{i=1}^{n} X_i \sim N\big([\sum \mu_i,\; \sum \sigma_i^2]\big)$.

## 11.9 Application: Sum of Independent Poissons

P: Let $X \sim \operatorname{Poisson}(\lambda_1)$ and $Y \sim \operatorname{Poisson}(\lambda_2)$ be independent. Show that $X + Y \sim \operatorname{Poisson}(\lambda_1 + \lambda_2)$ using MGFs.

S:
**IDENTIFY**: Identify the distribution of a sum of independent Poisson random variables via MGFs.

**PLAN**:
- Use the Poisson MGF $M(t) = e^{\lambda(e^t - 1)}$ for each.
- Multiply; match the result to a Poisson MGF.

**EXECUTE**:
1. $M_X(t) = e^{\lambda_1 (e^t - 1)}$, $M_Y(t) = e^{\lambda_2 (e^t - 1)}$.
2. By independence, $M_{X+Y}(t) = M_X(t) M_Y(t) = e^{(\lambda_1 + \lambda_2)(e^t - 1)}$.
3. This is the MGF of $\operatorname{Poisson}(\lambda_1 + \lambda_2)$.

**EVALUATE**: By uniqueness, $X + Y \sim \operatorname{Poisson}(\lambda_1 + \lambda_2)$. Rates add — consistent with Poisson processes merging.

C: If $X_1, \ldots, X_n$ are independent with $X_i \sim \operatorname{Poisson}(\lambda_i)$, then $\sum_{i=1}^{n} X_i \sim \operatorname{Poisson}\big([\sum_{i=1}^{n} \lambda_i]\big)$.

Q: What common property do the normal and Poisson families share that makes MGF analysis clean for their sums?
A: Both families are closed under addition of independent members — summing keeps you in the family and just adds the parameters (means and variances for normals, rates for Poissons). This closure manifests as a simple multiplicative structure of their MGFs.

## 11.10 Characteristic Functions

Q: Why do we sometimes replace $e^{tX}$ by $e^{itX}$ (where $i = \sqrt{-1}$) when defining the generating function?
A: The expectation $E[e^{tX}]$ can be infinite for heavy-tailed distributions (e.g., Cauchy), so the MGF may fail to exist. Replacing $t$ with $it$ makes the integrand $e^{itX}$ have modulus $1$, so the expectation always converges. The resulting object — the characteristic function — exists for every distribution.

C: The [characteristic function] of a random variable $X$ is $\varphi_X(t) = E[e^{itX}]$, where $i = \sqrt{-1}$ and $t \in \mathbb{R}$.

C: Unlike the MGF, the characteristic function $\varphi_X$ exists (and is finite) for [every] random variable, because $|e^{itX}| = 1$ so the expectation always converges.

Q: Which distribution fails to have an MGF but still has a perfectly well-defined characteristic function?
A: The standard Cauchy distribution. Its tails are too heavy for $E[e^{tX}]$ to be finite for any $t \neq 0$, but $\varphi(t) = e^{-|t|}$ is well defined because $|e^{itX}| = 1$.

## 11.11 Probability Generating Functions

Q: When is the probability generating function preferred over the MGF?
A: When $X$ takes values in the nonnegative integers $\{0, 1, 2, \ldots\}$. The PGF $G_X(z) = E[z^X]$ encodes the PMF as coefficients of a power series in $z$, making it especially convenient for discrete problems like branching processes and combinatorial identities.

C: The [probability generating function] (PGF) of a nonnegative integer-valued random variable $X$ is $G_X(z) = E[z^X] = \sum_{k=0}^{\infty} z^k P(X = k)$, defined at least for $|z| \leq 1$.

C: The MGF and PGF are related by $M_X(t) = [G_X(e^t)]$, so one can be recovered from the other whenever both exist.

Q: Why does $G_X(1) = 1$ for every nonnegative integer-valued random variable $X$?
A: $G_X(1) = \sum_{k=0}^{\infty} 1^k P(X=k) = \sum_{k=0}^{\infty} P(X=k) = 1$, since the probabilities sum to $1$ over the support.

Q: How do you recover $P(X = k)$ from the PGF $G_X$?
A: $P(X = k) = G_X^{(k)}(0) / k!$, the $k$-th Taylor coefficient of $G_X$ at $z = 0$. The PGF is literally the generating function of the PMF.
