+++
order = 4
tags = ["math", "probability", "random-variables", "discrete", "pmf", "expectation", "variance"]
+++

# Probability — Discrete Random Variables

## 4.1 Why Random Variables?

Q: Why do we introduce random variables at all, given that we already have sample spaces and events?
A: Sample spaces can contain arbitrary outcomes (coin faces, colored balls, people, molecules) that are awkward to compute with directly. A random variable maps each outcome to a number, so we can apply arithmetic: averaging, summing, comparing, and integrating. This numerical representation is what lets probability become a quantitative science instead of just a bookkeeping of events.

Q: Why is mapping outcomes to numbers more powerful than working with outcomes directly?
A: Numbers admit operations that raw outcomes don't. Once outcomes become numbers, we can ask about the "average" outcome, the spread, or the probability that the outcome exceeds some threshold. All the machinery of calculus and algebra becomes available, which would be meaningless on a set of abstract labels.

Q: What kind of question does a random variable let us answer that an event alone cannot?
A: Events answer yes/no questions ("did at least one head appear?"). Random variables answer quantitative questions ("how many heads appeared on average?", "how far from the mean is the outcome likely to be?"). The shift from events to random variables is the shift from classifying outcomes to measuring them.

## 4.2 Definition of a Random Variable

C: A [random variable] on a sample space $\Omega$ is a function $X : \Omega \to \mathbb{R}$ that assigns a real number to each outcome.

C: In the notation $X : \Omega \to \mathbb{R}$, $\Omega$ is the [sample space] (the set of all possible outcomes of the random experiment).

C: In the notation $X : \Omega \to \mathbb{R}$, $\mathbb{R}$ is the set of [real numbers], the codomain into which outcomes are mapped.

Q: Why is a random variable formally a function rather than a "variable that is random"?
A: The outcome $\omega \in \Omega$ is what's random; $X$ itself is a deterministic rule that assigns a number to each outcome. Once $\omega$ is drawn, $X(\omega)$ is completely determined. Calling $X$ a function clarifies that the randomness lives in $\Omega$, and $X$ just reads off a number.

Q: If you flip a coin twice, and $X$ counts the number of heads, what are $X(HH)$, $X(HT)$, $X(TH)$, and $X(TT)$?
A: $X(HH) = 2$, $X(HT) = 1$, $X(TH) = 1$, and $X(TT) = 0$. The function $X$ sends each outcome in $\Omega = \{HH, HT, TH, TT\}$ to a number in $\mathbb{R}$.

C: We write $\{X = x\}$ as shorthand for the [event] $\{\omega \in \Omega : X(\omega) = x\}$, the set of outcomes mapped to the value $x$.

Q: Why is $\{X = x\}$ called an event?
A: It is a subset of $\Omega$ (the preimage of $x$ under $X$), and events in probability are exactly subsets of the sample space. This identification is what lets us assign a probability $P(X = x)$ to the numerical value $x$.

## 4.3 Discrete Random Variables

C: A random variable $X$ is called [discrete] if its range (the set of values it can take) is finite or countably infinite.

C: The [range] of a random variable $X$ is the set $\{X(\omega) : \omega \in \Omega\}$, i.e., every value $X$ can actually take.

Q: Why does "countable range" capture the essential feature of a discrete random variable?
A: A countable range means the values can be listed $x_1, x_2, x_3, \ldots$ and each listed value can carry its own positive probability. Uncountable ranges (like an interval of reals) force individual values to have probability zero, which breaks the "sum over values" approach and demands integrals instead.

Q: Give an example of a discrete random variable with finite range, and one with countably infinite range.
A: Finite: the number of heads in 10 coin flips has range $\{0, 1, \ldots, 10\}$. Countably infinite: the number of flips until the first head has range $\{1, 2, 3, \ldots\}$, which is infinite but still listable.

Q: Is the exact height of a randomly selected person a discrete random variable?
A: No. Height can in principle take any real value in some interval, which is uncountable. It is a continuous random variable, and its distribution is described by a density rather than a mass function.

## 4.4 Probability Mass Function

C: The [probability mass function] (PMF) of a discrete random variable $X$ is the function $p_X(x) = P(X = x)$, giving the probability that $X$ takes each particular value $x$.

C: In the PMF $p_X(x) = P(X = x)$, $X$ is the [random variable] and $x$ is a specific real number at which we evaluate the probability.

Q: Why do we use $p_X$ (with subscript) rather than just $p$ for the PMF?
A: When several random variables appear in the same problem, their PMFs need to be distinguished. The subscript $X$ reminds you whose PMF it is, so $p_X(3)$ and $p_Y(3)$ can coexist without confusion.

Q: Why is the PMF defined only for discrete random variables?
A: It assigns a positive probability to individual values. For a continuous random variable, each single value has probability zero, so $P(X = x)$ is uninformative and we describe distributions with densities instead.

C: If $X$ is the number of heads in two fair coin flips, then $p_X(0) = [1/4]$, $p_X(1) = 1/2$, and $p_X(2) = 1/4$.

## 4.5 Properties of a Valid PMF

Q: What two conditions must a function $p_X$ satisfy to be a valid probability mass function?
A: First, nonnegativity: $p_X(x) \geq 0$ for every real $x$. Second, it must sum to 1 over all values in the range: $\sum_{x} p_X(x) = 1$. These two conditions are the discrete versions of the probability axioms.

C: A valid PMF satisfies [nonnegativity]: $p_X(x) \geq 0$ for all $x \in \mathbb{R}$.

C: A valid PMF satisfies the [normalization] condition: $\sum_{x} p_X(x) = 1$, where the sum runs over all values in the range of $X$.

Q: Why must a valid PMF sum to exactly 1?
A: The events $\{X = x\}$ for different values of $x$ are disjoint (a single outcome $\omega$ maps to exactly one number), and their union is the entire sample space $\Omega$. Since $P(\Omega) = 1$, countable additivity forces the probabilities of the pieces to sum to 1.

Q: Why must a PMF be nonnegative everywhere?
A: Each value $p_X(x) = P(X = x)$ is the probability of an event, and probabilities can never be negative by the axioms. Nonnegativity of the PMF is just a restatement of the nonnegativity axiom of probability.

C: If $p_X(x) = P(X = x)$ and $B \subseteq \mathbb{R}$, then $P(X \in B) = [\sum_{x \in B} p_X(x)]$.

Q: Why does $P(X \in B) = \sum_{x \in B} p_X(x)$ follow from the PMF?
A: The event $\{X \in B\}$ is the disjoint union of the events $\{X = x\}$ over $x \in B$. Countable additivity then lets us add their individual probabilities, each of which is $p_X(x)$ by definition.

## 4.6 Cumulative Distribution Function

C: The [cumulative distribution function] (CDF) of a random variable $X$ is $F_X(x) = P(X \leq x)$, the probability that $X$ takes a value at most $x$.

C: In the CDF $F_X(x) = P(X \leq x)$, the input $x$ is any [real number] (not just a value in the range of $X$).

Q: Why is the CDF defined for every real $x$, even values $X$ can never take?
A: The event $\{X \leq x\}$ makes sense for every real threshold $x$, regardless of whether $X$ itself hits $x$. This lets the CDF describe the whole distribution with a single function defined on all of $\mathbb{R}$, which is especially useful for comparing discrete and continuous random variables in a unified way.

Q: For a discrete random variable, how do you compute $F_X(x)$ from the PMF?
A: Sum the PMF over every value in the range that is $\leq x$: $F_X(x) = \sum_{x_i \leq x} p_X(x_i)$. The CDF is a running total of the PMF.

Q: Why does the CDF of a discrete random variable look like a step function?
A: Between consecutive values in the range, no new probability mass is added, so $F_X$ stays flat. At each value $x_i$ in the range, the CDF jumps up by exactly $p_X(x_i)$. The result is piecewise constant with jump discontinuities at the mass points.

## 4.7 Properties of the CDF

Q: What are the four defining properties of any cumulative distribution function?
A: (1) Monotone nondecreasing: $x \leq y$ implies $F_X(x) \leq F_X(y)$. (2) Right-continuous: $\lim_{y \to x^+} F_X(y) = F_X(x)$. (3) $\lim_{x \to -\infty} F_X(x) = 0$. (4) $\lim_{x \to +\infty} F_X(x) = 1$.

C: The CDF is [monotone nondecreasing]: if $x \leq y$, then $F_X(x) \leq F_X(y)$.

Q: Why is the CDF monotone nondecreasing?
A: If $x \leq y$, then $\{X \leq x\} \subseteq \{X \leq y\}$. By monotonicity of probability on nested events, $P(X \leq x) \leq P(X \leq y)$, i.e., $F_X(x) \leq F_X(y)$.

C: The CDF is [right-continuous]: $\lim_{y \to x^+} F_X(y) = F_X(x)$.

Q: Why is the CDF right-continuous rather than left-continuous?
A: The definition $F_X(x) = P(X \leq x)$ includes the point $x$. Approaching $x$ from the right, we keep including $x$, so the limit equals $F_X(x)$. Approaching from the left excludes $x$, so we miss the probability mass at $x$ and the left limit equals $F_X(x) - p_X(x)$.

C: The left limit of the CDF satisfies $\lim_{y \to x^-} F_X(y) = P(X < x) = F_X(x) - [p_X(x)]$.

Q: Why does $\lim_{x \to -\infty} F_X(x) = 0$?
A: As $x \to -\infty$, the event $\{X \leq x\}$ shrinks to the empty set because no outcome produces arbitrarily negative values in the limit. Continuity of probability from above gives $F_X(x) \to P(\emptyset) = 0$.

Q: Why does $\lim_{x \to +\infty} F_X(x) = 1$?
A: As $x \to +\infty$, the event $\{X \leq x\}$ grows to cover every possible value of $X$, i.e., the full sample space $\Omega$. Continuity from below gives $F_X(x) \to P(\Omega) = 1$.

Q: How do you recover $p_X(x)$ from the CDF of a discrete random variable?
A: $p_X(x) = F_X(x) - \lim_{y \to x^-} F_X(y)$. In other words, the jump of the CDF at $x$ equals the probability mass at $x$. Where the CDF is continuous, the mass is zero.

## 4.8 Expectation

Q: Why do we need a single number to summarize a random variable instead of reporting the whole PMF?
A: The PMF carries complete information but is bulky and hard to compare across distributions. A single "typical value" — the expectation — lets us rank distributions, build intuition, and prove theorems like the law of large numbers. It is the first and most important summary statistic of a random variable.

C: The [expectation] (expected value, mean) of a discrete random variable $X$ is $E[X] = \sum_{x} x \, p_X(x)$, where the sum runs over all values $x$ in the range of $X$.

C: In the expectation formula $E[X] = \sum_x x \, p_X(x)$, the value $x$ is a possible outcome of $X$ and $p_X(x) = P(X = x)$ is the [probability] of that outcome.

Q: Why is expectation a weighted average rather than a plain average of the possible values?
A: Not every value is equally likely. Weighting each value $x$ by its probability $p_X(x)$ reflects how often it actually occurs, so rare large values contribute less and frequent values contribute more. A plain average would treat unlikely outcomes as importantly as likely ones, which misrepresents the distribution.

Q: What is $E[X]$ for $X$ equal to the number showing on a fair six-sided die?
A: $E[X] = \sum_{x=1}^{6} x \cdot \frac{1}{6} = \frac{1 + 2 + 3 + 4 + 5 + 6}{6} = \frac{21}{6} = 3.5$. Note that $E[X]$ need not itself be a value in the range of $X$.

Q: Can the expectation of a random variable fail to exist?
A: Yes. If the range is countably infinite and $\sum_{x} |x| \, p_X(x) = \infty$, the sum $\sum_x x \, p_X(x)$ does not converge absolutely, and $E[X]$ is undefined. Absolute convergence is required so the expectation is independent of the summation order.

## 4.9 Law of the Unconscious Statistician

Q: Why do we need a special formula for $E[g(X)]$ instead of just using the definition?
A: The definition of expectation requires the PMF of $g(X)$, which could be painful to compute (you'd need to find $P(g(X) = y)$ for every $y$). The LOTUS formula lets us compute $E[g(X)]$ directly from the PMF of $X$ alone, without ever deriving the distribution of $g(X)$.

C: The [law of the unconscious statistician] (LOTUS) states that for a discrete random variable $X$ and any function $g : \mathbb{R} \to \mathbb{R}$, $E[g(X)] = \sum_{x} g(x) \, p_X(x)$.

Q: Why is LOTUS called the "law of the unconscious statistician"?
A: Many people instinctively compute $E[g(X)]$ this way without realizing it requires proof — as if "unconsciously." The formula looks like a plain substitution, but it actually needs the fact that $\{g(X) = y\}$ decomposes into disjoint pieces $\{X = x\}$ over all $x$ with $g(x) = y$.

P: Let $X$ be the number on a fair six-sided die. Compute $E[X^2]$ using LOTUS.

S:
**IDENTIFY**: Expectation of a function $g(X) = X^2$ of a discrete random variable.

**PLAN**:
- Apply LOTUS: $E[g(X)] = \sum_x g(x) \, p_X(x)$.
- Here $g(x) = x^2$ and $p_X(x) = 1/6$ for $x \in \{1, \ldots, 6\}$.

**EXECUTE**:
1. $E[X^2] = \sum_{x=1}^{6} x^2 \cdot \frac{1}{6}$.
2. $1^2 + 2^2 + 3^2 + 4^2 + 5^2 + 6^2 = 1 + 4 + 9 + 16 + 25 + 36 = 91$.
3. $E[X^2] = 91/6 \approx 15.17$.

**EVALUATE**:
- Sanity check: values range from $1$ to $36$, and $91/6 \approx 15.17$ sits between them, closer to the lower end (since small squares are more numerous per unit interval) — plausible.
- Note $E[X^2] = 91/6 \neq (E[X])^2 = 3.5^2 = 12.25$. They differ, which is exactly what variance will measure.

## 4.10 Variance

Q: Why isn't the expectation alone enough to describe a distribution?
A: Two distributions can share the same mean but differ enormously in how tightly they cluster around it. A constant equal to $0$ and a random variable that is $\pm 10^6$ with equal probability both have mean $0$, but one is predictable and the other wild. We need a second number — the variance — to capture spread.

Q: Why use $E[(X - \mu)^2]$ rather than $E[X - \mu]$ to measure spread?
A: $E[X - \mu] = 0$ always: positive and negative deviations cancel, making that quantity useless. Squaring makes every deviation nonnegative, so cancellation is impossible and the result genuinely measures how far $X$ strays from $\mu$ on average.

C: The [variance] of a discrete random variable $X$ with mean $\mu = E[X]$ is $\mathrm{Var}(X) = E[(X - \mu)^2]$, the expected squared deviation from the mean.

C: In the variance definition $\mathrm{Var}(X) = E[(X-\mu)^2]$, $\mu = E[X]$ is the [mean] of $X$ and the random variable $(X-\mu)^2$ measures squared deviation.

Q: Why is variance always nonnegative?
A: The random variable $(X - \mu)^2$ is nonnegative for every outcome, so its expectation is a sum of nonnegative terms weighted by probabilities, which cannot be negative.

C: The [computational formula] for variance is $\mathrm{Var}(X) = E[X^2] - (E[X])^2$.

Q: Why does $\mathrm{Var}(X) = E[X^2] - (E[X])^2$ follow from the definition?
A: Expand: $E[(X - \mu)^2] = E[X^2 - 2\mu X + \mu^2] = E[X^2] - 2\mu E[X] + \mu^2 = E[X^2] - 2\mu^2 + \mu^2 = E[X^2] - \mu^2$. This uses linearity of expectation and the fact that $\mu = E[X]$ is a constant.

Q: When is the computational formula $\mathrm{Var}(X) = E[X^2] - (E[X])^2$ preferable to the definition?
A: In calculations. Computing $E[(X-\mu)^2]$ directly requires first finding $\mu$ and then summing over $(x - \mu)^2 p_X(x)$. The computational formula needs only $E[X^2]$ (via LOTUS) and $E[X]$, avoiding the subtraction inside the sum.

P: Let $X$ be the number on a fair six-sided die. Compute $\mathrm{Var}(X)$.

S:
**IDENTIFY**: Variance of a discrete uniform random variable on $\{1, \ldots, 6\}$.

**PLAN**:
- Use the computational formula $\mathrm{Var}(X) = E[X^2] - (E[X])^2$.
- Compute $E[X]$ and $E[X^2]$ via LOTUS.

**EXECUTE**:
1. $E[X] = 3.5$ (computed earlier).
2. $E[X^2] = 91/6$ (computed earlier via LOTUS).
3. $\mathrm{Var}(X) = 91/6 - (7/2)^2 = 91/6 - 49/4$.
4. Common denominator $12$: $91/6 = 182/12$ and $49/4 = 147/12$, so $\mathrm{Var}(X) = 35/12 \approx 2.917$.

**EVALUATE**:
- Positive, as variance must be.
- Die values range over $6$ units; a variance of $\approx 2.9$ gives a standard deviation of $\approx 1.7$, which is roughly the typical distance from $3.5$ to a random face — plausible.

## 4.11 Standard Deviation

Q: Why do we bother defining the standard deviation in addition to the variance?
A: Variance has units of the square of $X$'s units (e.g., $\text{meters}^2$), which is hard to interpret. The standard deviation $\sigma = \sqrt{\mathrm{Var}(X)}$ has the same units as $X$ itself, so it can be compared directly to the mean and to typical values of $X$.

C: The [standard deviation] of $X$ is $\sigma_X = \sqrt{\mathrm{Var}(X)}$, the positive square root of the variance.

C: The standard deviation $\sigma_X$ has the [same units] as $X$, whereas the variance has squared units.

Q: Why is the standard deviation always nonnegative?
A: It is defined as the positive (principal) square root of the variance. Since variance is nonnegative, its square root is real and we choose the nonnegative root by convention.

Q: If $\mathrm{Var}(X) = 35/12$, what is the standard deviation of $X$?
A: $\sigma_X = \sqrt{35/12} \approx 1.708$. It carries the same units as $X$ and roughly represents the typical deviation from the mean.

## 4.12 Linearity of Expectation and Variance Scaling

Q: Why is $E[aX + b] = aE[X] + b$ for constants $a, b$?
A: Apply LOTUS with $g(x) = ax + b$: $E[aX + b] = \sum_x (ax + b) p_X(x) = a \sum_x x p_X(x) + b \sum_x p_X(x) = a E[X] + b \cdot 1$. The linearity of the summation carries over directly to expectation.

C: [Linearity of expectation] (single variable): for constants $a, b \in \mathbb{R}$, $E[aX + b] = a E[X] + b$.

Q: Why does the $+b$ in $aX + b$ add to the expectation without modification?
A: Adding a constant $b$ shifts every value of $X$ by the same amount, so the average shifts by exactly $b$. No weighting or scaling affects it, because $b$ does not depend on the outcome.

C: [Variance under affine transformation]: for constants $a, b \in \mathbb{R}$, $\mathrm{Var}(aX + b) = a^2 \, \mathrm{Var}(X)$.

Q: Why does the constant $b$ disappear from $\mathrm{Var}(aX + b)$?
A: Shifting every value by $b$ also shifts the mean by $b$, so the deviation $(aX + b) - (a\mu + b) = a(X - \mu)$ doesn't involve $b$ at all. Variance measures spread around the mean, and translation does not change spread.

Q: Why does the scalar $a$ appear squared in $\mathrm{Var}(aX + b) = a^2 \mathrm{Var}(X)$?
A: Scaling $X$ by $a$ scales each deviation $(X - \mu)$ by $a$, so the squared deviation $(X - \mu)^2$ gets multiplied by $a^2$. Expectation then inherits that factor, giving $a^2 \mathrm{Var}(X)$. The absolute value $|a|$ appears (once) in standard deviation: $\sigma_{aX+b} = |a| \sigma_X$.

Q: If $E[X] = 3.5$ and $\mathrm{Var}(X) = 35/12$, what are $E[2X - 1]$ and $\mathrm{Var}(2X - 1)$?
A: $E[2X - 1] = 2 \cdot 3.5 - 1 = 6$ and $\mathrm{Var}(2X - 1) = 2^2 \cdot 35/12 = 35/3 \approx 11.67$. The constant $-1$ shifts the mean but leaves the variance unchanged, and the factor $2$ scales the variance by $4$.

P: A random variable $X$ has $E[X] = 10$ and $\mathrm{Var}(X) = 4$. Define $Y = -3X + 7$. Find $E[Y]$, $\mathrm{Var}(Y)$, and $\sigma_Y$.

S:
**IDENTIFY**: Affine transformation of a random variable; compute mean, variance, and standard deviation of $Y = aX + b$ with $a = -3$, $b = 7$.

**PLAN**:
- Apply linearity of expectation: $E[aX + b] = a E[X] + b$.
- Apply variance scaling: $\mathrm{Var}(aX + b) = a^2 \mathrm{Var}(X)$.
- Take the positive square root for $\sigma_Y$.

**EXECUTE**:
1. $E[Y] = -3 \cdot 10 + 7 = -30 + 7 = -23$.
2. $\mathrm{Var}(Y) = (-3)^2 \cdot 4 = 9 \cdot 4 = 36$.
3. $\sigma_Y = \sqrt{36} = 6$.

**EVALUATE**:
- The constant $+7$ affected the mean but not the variance — as expected.
- The negative sign on $a = -3$ vanished in the variance because $a$ is squared, but $\sigma_Y = |a| \sigma_X = 3 \cdot 2 = 6$ still uses the absolute value.
- Sanity: $\sigma_X = \sqrt{4} = 2$, and scaling $X$ by $3$ in magnitude should triple the spread, giving $\sigma_Y = 6$. ✓
