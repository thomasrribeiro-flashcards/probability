+++
order = 6
tags = ["math", "probability", "continuous", "pdf", "cdf", "expectation", "quantiles"]
+++

# Probability — Continuous Random Variables

## 6.1 Why Continuous Random Variables?

Q: Why do we need continuous random variables when discrete ones already exist?
A: Many natural quantities — heights, waiting times, temperatures, particle positions — take values on a continuum, where listing outcomes one by one is impossible. Discrete distributions assign positive probability to each outcome, but a continuum has uncountably many outcomes, so that approach breaks down. Continuous random variables replace "probability at a point" with "probability density over a region," letting us model real-valued measurements consistently.

Q: Why can't we just use a very fine discrete approximation instead of a continuous random variable?
A: Finer and finer discretizations require shrinking the probability at each point, and in the limit every individual point carries zero probability. Working directly with the continuous limit is cleaner: densities and integrals replace probabilities and sums, giving exact formulas rather than approximations whose accuracy depends on bin width.

C: A random variable $X$ is called [continuous] if its set of possible values is uncountable (e.g., an interval of $\mathbb{R}$) and $P(X = x) = 0$ for every single $x$.

Q: What kind of real-world quantities are naturally modeled as continuous random variables?
A: Measurements on a continuous scale — lengths, masses, times, voltages, temperatures — where the resolution of the scale is limited only by the measuring instrument, not by the underlying quantity.

Q: Why is the distinction between "countably infinite" and "uncountably infinite" important for probability?
A: For countably many outcomes we can still assign each a positive probability that sums to $1$ (e.g., geometric distribution). For uncountably many outcomes no such assignment is possible — an uncountable sum of positive numbers cannot equal $1$ — so we must abandon pointwise probability and work with densities instead.

## 6.2 Why $P(X=x) = 0$ for Continuous RVs

Q: Before we prove it, predict: for a continuous random variable $X$ with values in $[0,1]$, what do you expect $P(X = 0.5)$ to equal, and why?
A: Intuition says "very small," but in fact it equals exactly $0$. There are uncountably many points in $[0,1]$, and if any individual point had positive probability $p$, then adding up the probabilities of even countably many such points would exceed $1$, contradicting the total probability axiom.

Q: Why does $P(X = x) = 0$ hold for every $x$ when $X$ is continuous?
A: If $P(X = x) > 0$ held for even one point, a consistency argument using the continuum of nearby points would force the total probability to exceed $1$. More formally, $P(X = x)$ is the integral of the density over the single point $\{x\}$, and the integral of any function over a single point is $0$.

Q: Does $P(X = x) = 0$ mean that the outcome $X = x$ is impossible?
A: No. Impossibility is a stronger notion than probability zero for continuous random variables. Every realization of $X$ lands on some specific value $x$, yet each specific value had probability zero ahead of time. "Probability zero" here means "negligible in the sense of integration," not "cannot occur."

Q: Why, for a continuous $X$, is $P(a \leq X \leq b) = P(a < X < b)$?
A: The two events differ only by the endpoints $\{X = a\}$ and $\{X = b\}$, which each have probability zero for a continuous $X$. Adding or removing probability-zero events does not change the probability, so inclusive and exclusive inequalities yield the same value.

C: For a continuous random variable, $P(X = x) = [0]$ for every real $x$.

C: For a continuous $X$ and real numbers $a < b$, $P(a \leq X \leq b) = P(a < X < b)$ because the [endpoints] contribute zero probability.

## 6.3 Probability Density Function (PDF)

Q: Why replace the probability mass function of discrete RVs with a probability density function for continuous ones?
A: A pmf assigns a positive number to each outcome, but for continuous RVs every outcome has probability zero, so a pmf would be uniformly zero and useless. A pdf instead describes how probability is distributed per unit length: probability of a region is obtained by integrating the density over that region, which remains finite and informative.

C: The [probability density function] (pdf) of a continuous random variable $X$ is a function $f_X : \mathbb{R} \to \mathbb{R}$ such that $P(a \leq X \leq b) = \int_a^b f_X(x)\,dx$ for all $a \leq b$.

C: A pdf $f_X$ must satisfy $f_X(x) \geq [0]$ for every $x \in \mathbb{R}$.

C: A pdf $f_X$ must satisfy $\int_{-\infty}^{\infty} f_X(x)\,dx = [1]$, the total probability axiom.

Q: Can the value of a pdf $f_X(x)$ be larger than $1$?
A: Yes. The pdf is a density (probability per unit length), not a probability. For example, the uniform pdf on $[0, 0.1]$ equals $10$ on that interval. What must stay between $0$ and $1$ are probabilities, obtained by integrating the pdf over an interval.

Q: What does the value $f_X(x_0)$ physically represent?
A: It represents the probability per unit length near $x_0$: for a small interval of width $dx$ around $x_0$, $P(x_0 \leq X \leq x_0 + dx) \approx f_X(x_0)\,dx$. Higher density at $x_0$ means values near $x_0$ are more likely than values where the density is lower.

Q: Why must a pdf be nonnegative?
A: Probabilities of events must be nonnegative, and $P(a \leq X \leq b) = \int_a^b f_X(x)\,dx$. If $f_X$ were negative on some interval, we could choose $a,b$ to make this integral negative, producing a negative probability — a contradiction.

Q: Why must a pdf integrate to $1$ over all of $\mathbb{R}$?
A: The event $-\infty < X < \infty$ is certain, so its probability is $1$. By definition of the pdf, that probability equals $\int_{-\infty}^{\infty} f_X(x)\,dx$, which therefore must equal $1$.

C: If $g$ is nonnegative and $\int_{-\infty}^{\infty} g(x)\,dx = c$ with $0 < c < \infty$, then $f(x) = g(x)/c$ is a valid pdf, obtained by [normalizing] $g$.

## 6.4 Computing Probabilities via Integration

C: For a continuous RV $X$ with pdf $f_X$, $P(a \leq X \leq b) = \int_a^b [f_X(x)\,dx]$.

Q: Why is the probability of a region given by an integral rather than a sum?
A: An integral is the continuous analog of a sum. For discrete RVs we add pmf values over outcomes in an event; for continuous RVs we add density values times infinitesimal widths over the region, which is precisely integration. The pdf times $dx$ plays the role of the pmf value.

Q: For continuous $X$, how do $P(X \leq b)$ and $P(X < b)$ compare?
A: They are equal, because $P(X = b) = 0$. The event $\{X \leq b\}$ differs from $\{X < b\}$ only by the single point $\{X = b\}$, which contributes zero probability.

P: Let $X$ have pdf $f_X(x) = 3x^2$ on $[0,1]$ and $0$ elsewhere. Find $P(0.2 \leq X \leq 0.5)$.

S:
**IDENTIFY**: Probability of an interval for a continuous RV — requires integrating the pdf over the interval.

**PLAN**:
- Confirm $f_X$ is a valid pdf (nonnegative and integrates to $1$).
- Compute $P(0.2 \leq X \leq 0.5) = \int_{0.2}^{0.5} f_X(x)\,dx$.

**EXECUTE**:
1. Check total: $\int_0^1 3x^2\,dx = x^3 \big|_0^1 = 1$ ✓.
2. $P(0.2 \leq X \leq 0.5) = \int_{0.2}^{0.5} 3x^2\,dx = x^3 \big|_{0.2}^{0.5} = 0.125 - 0.008 = 0.117$.

**EVALUATE**:
- Result is between $0$ and $1$ ✓.
- The pdf is larger near $x=1$, so most probability sits to the right; $0.117$ on $[0.2, 0.5]$ is plausibly smaller than $P(0.5 \leq X \leq 1) = 1 - 0.125 = 0.875$.

## 6.5 Cumulative Distribution Function (CDF)

C: The [cumulative distribution function] (CDF) of a random variable $X$ is $F_X(x) = P(X \leq x)$, defined for every real $x$.

C: For a continuous $X$ with pdf $f_X$, $F_X(x) = \int_{-\infty}^{x} [f_X(t)]\,dt$, where $t$ is the dummy variable of integration.

Q: Why does the CDF use a different dummy variable ($t$) inside the integral?
A: The upper limit $x$ is the input to $F_X$, so it must not also be used as the integration variable. Using $t$ as the dummy keeps the roles separate: $x$ is fixed for the evaluation, while $t$ ranges from $-\infty$ up to $x$.

Q: Why is the CDF often more convenient than the pdf for computing probabilities?
A: The CDF directly gives $P(X \leq x)$ for any $x$, and differences of CDF values give interval probabilities: $P(a < X \leq b) = F_X(b) - F_X(a)$. Looking up or computing two CDF values is often faster than integrating the pdf from scratch for each new interval.

C: For continuous $X$, $P(a \leq X \leq b) = F_X(b) - [F_X(a)]$.

Q: Why does the formula $P(a \leq X \leq b) = F_X(b) - F_X(a)$ use the SAME expression for inclusive and exclusive endpoints when $X$ is continuous?
A: Because $P(X = a) = P(X = b) = 0$, swapping $\leq$ for $<$ at either endpoint changes the probability by $0$. The formula works identically for $P(a < X < b)$, $P(a \leq X < b)$, etc.

## 6.6 PDF as Derivative of CDF

C: At every point where $F_X$ is differentiable, $f_X(x) = [F_X'(x)]$.

Q: Why is the pdf the derivative of the CDF?
A: The CDF $F_X(x) = \int_{-\infty}^x f_X(t)\,dt$ is the integral of $f_X$ from $-\infty$ to $x$, so by the fundamental theorem of calculus its derivative with respect to $x$ equals the integrand $f_X(x)$ (at every point where $f_X$ is continuous).

Q: Why are pdf and CDF two equivalent ways of describing a continuous distribution?
A: Given the pdf, integrating yields the CDF; given the CDF, differentiating yields the pdf. Both encode the same information about how probability is distributed, but in different forms — the pdf emphasizes local density, the CDF emphasizes cumulative probability up to a point.

P: Suppose $F_X(x) = 1 - e^{-\lambda x}$ for $x \geq 0$ (and $0$ otherwise), with $\lambda > 0$. Find the pdf $f_X$.

S:
**IDENTIFY**: Recover the pdf from a given CDF — differentiate.

**PLAN**:
- Use $f_X(x) = F_X'(x)$ on the region where $F_X$ is smooth.
- State the pdf as zero outside that region.

**EXECUTE**:
1. For $x \geq 0$: $f_X(x) = \frac{d}{dx}(1 - e^{-\lambda x}) = \lambda e^{-\lambda x}$.
2. For $x < 0$: $F_X$ is constant at $0$, so $f_X(x) = 0$.

**EVALUATE**:
- $f_X(x) \geq 0$ everywhere ✓.
- $\int_0^\infty \lambda e^{-\lambda x}\,dx = 1$ ✓.
- This is the Exponential($\lambda$) pdf, consistent with the Exponential CDF we started from.

## 6.7 Properties of the CDF

Q: Why is the CDF always monotone non-decreasing?
A: If $a \leq b$, then $\{X \leq a\} \subseteq \{X \leq b\}$. Probabilities of subsets are no larger than probabilities of supersets, so $F_X(a) = P(X \leq a) \leq P(X \leq b) = F_X(b)$.

C: Every CDF satisfies $\lim_{x \to -\infty} F_X(x) = [0]$ because events of the form $\{X \leq x\}$ shrink to the impossible event as $x \to -\infty$.

C: Every CDF satisfies $\lim_{x \to \infty} F_X(x) = [1]$ because events of the form $\{X \leq x\}$ grow to the certain event as $x \to \infty$.

Q: Why is the CDF of a continuous RV continuous (no jumps)?
A: A jump of size $p$ at $x = x_0$ in the CDF would mean $P(X = x_0) = p > 0$. Since $P(X = x) = 0$ for every $x$ when $X$ is continuous, no such jump can occur, and $F_X$ is everywhere continuous.

Q: What does a jump discontinuity in a CDF at $x = x_0$ indicate?
A: That $P(X = x_0)$ equals the size of the jump — the RV places positive probability mass at $x_0$. Jumps therefore occur exactly at atoms of the distribution; a purely continuous RV has a jump-free CDF.

C: For any random variable, the CDF $F_X$ is [right-continuous].

Q: Why do we evaluate probabilities with $F_X(b) - F_X(a)$ rather than $F_X(a) - F_X(b)$?
A: $F_X$ is non-decreasing, so $F_X(b) \geq F_X(a)$ for $a \leq b$, and the positive difference $F_X(b) - F_X(a)$ equals $P(a < X \leq b) \geq 0$. Reversing would yield a non-positive number, inconsistent with a probability.

## 6.8 Expectation of a Continuous RV

Q: Why does the expectation formula switch from a sum (discrete) to an integral (continuous)?
A: Expectation weights each possible value by its probability. For discrete RVs that's $\sum x \cdot P(X=x)$; for continuous RVs the probability at a point is zero, so we instead weight each value by its probability density and integrate, giving $\int x f_X(x)\,dx$ — the continuous analog of the weighted sum.

C: The [expectation] of a continuous RV $X$ with pdf $f_X$ is $E[X] = \int_{-\infty}^{\infty} x f_X(x)\,dx$, provided the integral converges absolutely.

Q: What does $E[X]$ represent geometrically when $f_X$ is viewed as a mass distribution?
A: The center of mass (centroid) of the density $f_X$. If you imagine the pdf as a mass distribution on the real line with total mass $1$, $E[X]$ is the balance point where the distribution would balance on a pivot.

Q: Why might $E[X]$ fail to exist for some continuous distributions?
A: The defining integral $\int x f_X(x)\,dx$ can diverge if the tails of $f_X$ are too heavy. For example, the Cauchy distribution has $f_X(x) = \frac{1}{\pi(1+x^2)}$, whose expectation integral diverges, so $E[X]$ is undefined.

C: A continuous RV has expectation $E[X]$ exactly when $\int_{-\infty}^{\infty} [|x|] f_X(x)\,dx < \infty$ (absolute integrability).

## 6.9 Law of the Unconscious Statistician (LOTUS)

Q: Why is LOTUS called "unconscious"? What does it let us avoid?
A: To compute $E[g(X)]$ you'd normally need the distribution of $Y = g(X)$ first, then integrate $y f_Y(y)\,dy$. LOTUS lets you skip finding $f_Y$ entirely — you "unconsciously" use the original density $f_X$ and just weight $g(x)$ by it. This shortcut is valid because the total probability assigned by $f_X$ to each region matches the probability $Y$ assigns to the image of that region.

C: [LOTUS] for continuous RVs: $E[g(X)] = \int_{-\infty}^{\infty} g(x) f_X(x)\,dx$, where $g$ is any function for which the integral converges absolutely.

Q: What special case of LOTUS gives $E[X^2]$?
A: Take $g(x) = x^2$. Then $E[X^2] = \int_{-\infty}^{\infty} x^2 f_X(x)\,dx$. This is the "second moment" of $X$ and appears in the variance formula.

Q: Why does linearity of expectation still hold for continuous RVs?
A: Linearity follows from linearity of integration: $E[aX + b] = \int (ax + b) f_X(x)\,dx = a \int x f_X(x)\,dx + b \int f_X(x)\,dx = a E[X] + b$. So constants pull out and additive constants shift the mean, just as in the discrete case.

C: For continuous $X$ and constants $a, b$, $E[aX + b] = a E[X] + [b]$.

## 6.10 Variance

Q: Why does the definition of variance stay the same when moving from discrete to continuous RVs?
A: Variance is defined by an expectation — $\text{Var}(X) = E[(X - E[X])^2]$ — and expectation has both discrete (sum) and continuous (integral) forms. The definition is expressed in terms of $E$, so it transfers verbatim; only the way we compute the underlying expectation changes.

C: The [variance] of a continuous RV $X$ is $\text{Var}(X) = E[(X - \mu)^2] = \int_{-\infty}^{\infty} (x - \mu)^2 f_X(x)\,dx$, where $\mu = E[X]$ is the mean.

C: The [computational formula] for variance still holds: $\text{Var}(X) = E[X^2] - (E[X])^2$.

Q: Why is $\text{Var}(X) = E[X^2] - (E[X])^2$ usually easier to use than the definition?
A: The definition requires first computing $\mu = E[X]$, then integrating $(x - \mu)^2 f_X(x)$, which expands into a messy polynomial. The computational formula only needs two integrals — $\int x f_X(x)\,dx$ and $\int x^2 f_X(x)\,dx$ — each of which is a raw moment and usually simpler to evaluate.

C: The [standard deviation] of $X$ is $\sigma_X = \sqrt{\text{Var}(X)}$, measured in the same units as $X$ itself.

Q: Why is variance always nonnegative for continuous RVs?
A: Variance is the expectation of the nonnegative quantity $(X - \mu)^2$. The integral of a nonnegative function against a nonnegative density is nonnegative, so $\text{Var}(X) \geq 0$ always, with equality only if $X$ is constant almost surely.

Q: For constants $a, b$, how does $\text{Var}(aX + b)$ depend on $a$ and $b$?
A: $\text{Var}(aX + b) = a^2 \text{Var}(X)$. The shift $b$ does not affect spread (every value moves by the same amount), while scaling by $a$ stretches deviations by $|a|$, squaring in the variance.

P: Let $X \sim \text{Uniform}[0,1]$, so $f_X(x) = 1$ on $[0,1]$ and $0$ elsewhere. Compute $E[X]$ and $\text{Var}(X)$.

S:
**IDENTIFY**: Mean and variance of a continuous uniform RV — direct integration plus the computational formula.

**PLAN**:
- Compute $E[X] = \int_0^1 x \cdot 1\,dx$.
- Compute $E[X^2] = \int_0^1 x^2 \cdot 1\,dx$ using LOTUS.
- Apply $\text{Var}(X) = E[X^2] - (E[X])^2$.

**EXECUTE**:
1. $E[X] = \int_0^1 x\,dx = \frac{1}{2}$.
2. $E[X^2] = \int_0^1 x^2\,dx = \frac{1}{3}$.
3. $\text{Var}(X) = \frac{1}{3} - \left(\frac{1}{2}\right)^2 = \frac{1}{3} - \frac{1}{4} = \frac{1}{12}$.

**EVALUATE**:
- Mean $\frac{1}{2}$ is the midpoint of $[0,1]$, as expected by symmetry ✓.
- Variance $\frac{1}{12} \approx 0.083$, giving $\sigma_X \approx 0.289$, which is a reasonable spread for a distribution confined to a unit interval ✓.

## 6.11 Quantiles and the Median

Q: Why are quantiles useful summaries of a continuous distribution?
A: They describe location in terms of probability rather than raw value: the $p$-th quantile is the threshold below which a fraction $p$ of probability lies. This makes quantiles robust to outliers and meaningful even when $E[X]$ is undefined (e.g., Cauchy), where the mean fails as a summary.

C: For $p \in (0,1)$, the [$p$-th quantile] of $X$ is any value $q_p$ satisfying $F_X(q_p) = p$, i.e., $P(X \leq q_p) = p$.

Q: Why is the quantile uniquely defined when the CDF is strictly increasing and continuous?
A: A strictly increasing continuous CDF is a bijection from its support to $(0,1)$, so for every $p \in (0,1)$ there is exactly one $x$ with $F_X(x) = p$. Plateaus in $F_X$ (flat regions) or jumps would break uniqueness, but those do not occur for a strictly increasing continuous CDF.

C: The [median] of $X$ is the $0.5$-quantile: a value $m$ with $F_X(m) = 0.5$, so that $P(X \leq m) = P(X \geq m) = \frac{1}{2}$.

Q: Why can the median and the mean of a continuous distribution differ?
A: The mean is sensitive to how far values lie from the center (it integrates $x f_X(x)$), while the median only cares about how much probability lies on each side. A skewed density moves the mean toward the heavy tail but leaves the median near the bulk of the mass, so the two diverge whenever the distribution is asymmetric.

Q: For a symmetric continuous distribution with finite mean, why are the mean and the median equal?
A: Symmetry about a point $c$ means $f_X(c + t) = f_X(c - t)$, so probability is balanced on both sides of $c$, giving $F_X(c) = 0.5$ (median is $c$) and $E[X] = c$ by a change-of-variable argument. Both summaries coincide at the axis of symmetry.

C: The first [quartile] $Q_1$ is the $0.25$-quantile, and the third quartile $Q_3$ is the $0.75$-quantile.

C: The [interquartile range] (IQR) of $X$ is $Q_3 - Q_1$, a spread measure robust to heavy tails.

P: Let $X$ have CDF $F_X(x) = 1 - e^{-\lambda x}$ for $x \geq 0$ (Exponential$(\lambda)$). Find the median.

S:
**IDENTIFY**: Median of a continuous RV — solve $F_X(m) = 1/2$.

**PLAN**:
- Set $F_X(m) = 0.5$ and solve for $m$.

**EXECUTE**:
1. $1 - e^{-\lambda m} = 0.5$ so $e^{-\lambda m} = 0.5$.
2. $-\lambda m = \ln(0.5) = -\ln 2$.
3. $m = \frac{\ln 2}{\lambda}$.

**EVALUATE**:
- $m > 0$, as required for a distribution supported on $[0, \infty)$ ✓.
- Median $\frac{\ln 2}{\lambda} \approx \frac{0.693}{\lambda}$ is less than the mean $\frac{1}{\lambda}$, reflecting the right-skew of the Exponential distribution — consistent with "mean > median for right-skewed distributions."

## 6.12 Mixed Random Variables

Q: Why do some random variables fail to be purely discrete or purely continuous?
A: A variable can simultaneously assign positive probability to a specific value (an atom) and spread probability continuously elsewhere. Examples include insurance claim amounts (mass at $0$ for "no claim," continuous density for positive claims) or censored measurements. Neither a pmf alone nor a pdf alone captures both behaviors.

C: A [mixed random variable] has a CDF with both jump discontinuities (discrete atoms) and regions of continuous increase (continuous part).

Q: What do jumps and smooth increases in a CDF correspond to for a mixed RV?
A: A jump of size $p$ at $x_0$ corresponds to a point mass $P(X = x_0) = p$, like a discrete atom. A smooth increase over an interval corresponds to a continuous density contribution, integrated as a pdf would be. Mixed RVs combine both phenomena in a single CDF.

Q: For a mixed RV, why is the CDF still the correct unified description?
A: The CDF is defined as $F_X(x) = P(X \leq x)$ for any random variable — discrete, continuous, or mixed. It always exists, captures all atoms as jumps and all continuous parts as smooth increases, and lets us compute probabilities by differences $F_X(b) - F_X(a)$ regardless of the RV's type.
