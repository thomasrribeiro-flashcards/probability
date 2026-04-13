+++
order = 7
tags = ["math", "probability", "distributions", "uniform", "exponential", "normal", "gamma", "beta"]
+++

# Probability — Common Continuous Distributions

## 7.1 Why study named continuous distributions?

Q: Why do we bother naming specific continuous distributions like uniform, exponential, and normal?
A: A handful of distributions arise repeatedly in models of real phenomena (waiting times, measurement error, proportions), so naming them lets us recycle derived formulas for their PDFs, CDFs, means, and variances instead of redoing integrals each time. They also serve as building blocks: many richer distributions are defined as transformations or sums of these basic ones.

Q: Why should we memorize the mean and variance of each named distribution?
A: When a model uses, say, an exponential arrival time, the mean and variance immediately tell you the expected wait and its spread without computing any integrals. This turns modeling questions into parameter-matching exercises: pick the distribution whose shape fits, then use its known moments.

Q: Why is knowing a distribution's family more useful than just knowing a single PDF?
A: A family (indexed by parameters like $\lambda$ or $\mu, \sigma$) covers a whole range of shapes with one formula. You can fit the parameters to data, compare within a family, and exploit shared properties (e.g. every exponential is memoryless, every normal is closed under linear combinations).

C: A [parametric family] of distributions is a collection of distributions indexed by one or more real parameters, such as $\mathrm{Exp}(\lambda)$ for $\lambda > 0$.

## 7.2 Uniform $U(a,b)$

Q: Why is the uniform distribution on $[a,b]$ the natural model for "complete ignorance" on a bounded interval?
A: If we have no reason to prefer any point in $[a,b]$ over another, the only density consistent with that symmetry is the constant density — every sub-interval of equal length has equal probability. Anything else would privilege some region, contradicting the ignorance assumption.

C: A random variable $X$ has the [uniform distribution] on $[a,b]$, written $X \sim U(a,b)$, if its PDF is constant on $[a,b]$ and zero elsewhere, where $a < b$ are the interval endpoints.

C: The PDF of $X \sim U(a,b)$ is $f(x) = [\tfrac{1}{b-a}]$ for $x \in [a,b]$ and $0$ otherwise, where $a$ and $b$ are the endpoints of the support.

Q: Why does the uniform PDF on $[a,b]$ equal $1/(b-a)$ specifically?
A: A PDF must integrate to $1$ over its support. If $f$ is a constant $c$ on an interval of length $b-a$, then $\int_a^b c\,dx = c(b-a)$, which equals $1$ only when $c = 1/(b-a)$.

C: The CDF of $X \sim U(a,b)$ is $F(x) = [\tfrac{x-a}{b-a}]$ for $x \in [a,b]$, where $a$ and $b$ are the endpoints of the support.

Q: Why is the CDF of a uniform random variable linear on its support?
A: The CDF is the integral of a constant PDF, and the integral of a constant is a linear function. Geometrically, $F(x)$ is the area of a rectangle of height $1/(b-a)$ and width $x-a$.

C: If $X \sim U(a,b)$, then $E[X] = [\tfrac{a+b}{2}]$, where $a$ and $b$ are the interval endpoints.

Q: Why does $E[X] = (a+b)/2$ for $X \sim U(a,b)$ without any calculation?
A: The uniform PDF is symmetric about the midpoint of $[a,b]$. For any symmetric distribution on a bounded interval, the mean equals the center of symmetry, which is $(a+b)/2$.

C: If $X \sim U(a,b)$, then $\mathrm{Var}(X) = [\tfrac{(b-a)^2}{12}]$, where $b-a$ is the length of the support.

Q: Why does the variance of $U(a,b)$ scale as $(b-a)^2$ rather than $(b-a)$?
A: Variance has units of (value)$^2$, so it must scale as the square of any length applied to $X$. Doubling the interval doubles $X - E[X]$ pointwise, which quadruples the squared deviations and hence the variance.

P: Compute $E[X]$ and $\mathrm{Var}(X)$ directly for $X \sim U(0,1)$ using the definitions.

S:
**IDENTIFY**: Compute the first two moments of a uniform random variable from its PDF, $f(x)=1$ on $[0,1]$.

**PLAN**:
- Use $E[X] = \int x f(x)\,dx$.
- Use $\mathrm{Var}(X) = E[X^2] - E[X]^2$ with $E[X^2] = \int x^2 f(x)\,dx$.

**EXECUTE**:
1. $E[X] = \int_0^1 x\,dx = \tfrac{1}{2}$.
2. $E[X^2] = \int_0^1 x^2\,dx = \tfrac{1}{3}$.
3. $\mathrm{Var}(X) = \tfrac{1}{3} - (\tfrac{1}{2})^2 = \tfrac{1}{3} - \tfrac{1}{4} = \tfrac{1}{12}$.

**EVALUATE**:
- Matches the general formula with $a = 0, b = 1$: mean $(a+b)/2 = 1/2$, variance $(b-a)^2/12 = 1/12$. ✓

## 7.3 Exponential $\mathrm{Exp}(\lambda)$

Q: Why is the exponential distribution the standard model for waiting times?
A: It describes the time until the first occurrence of an event that happens at a constant average rate and is independent of the past. Radioactive decay, customer arrivals to a Poisson-rate process, and failure times of "ageless" components all fit this assumption naturally.

C: A random variable $T \geq 0$ has the [exponential distribution] with rate $\lambda > 0$, written $T \sim \mathrm{Exp}(\lambda)$, if its PDF is $f(t) = \lambda e^{-\lambda t}$ for $t \geq 0$, where $\lambda$ is the rate parameter.

C: The PDF of $T \sim \mathrm{Exp}(\lambda)$ is $f(t) = [\lambda e^{-\lambda t}]$ for $t \geq 0$, where $\lambda > 0$ is the rate parameter and $t$ is the elapsed time.

Q: What units does the rate parameter $\lambda$ of an exponential distribution have?
A: Inverse time (e.g. events per second). Since $\lambda t$ must be dimensionless in $e^{-\lambda t}$, and $t$ is a time, $\lambda$ must have units of $1/\text{time}$ — it is a frequency.

C: The CDF of $T \sim \mathrm{Exp}(\lambda)$ is $F(t) = [1 - e^{-\lambda t}]$ for $t \geq 0$, where $\lambda > 0$ is the rate parameter.

Q: Why does the exponential CDF have the form $1 - e^{-\lambda t}$?
A: Integrating $\lambda e^{-\lambda s}$ from $0$ to $t$ gives $[-e^{-\lambda s}]_0^t = 1 - e^{-\lambda t}$. The survival probability $P(T > t) = e^{-\lambda t}$ captures "no event has occurred by time $t$" and decays exponentially at rate $\lambda$.

C: For $T \sim \mathrm{Exp}(\lambda)$, the survival function is $P(T > t) = [e^{-\lambda t}]$, where $\lambda$ is the rate and $t \geq 0$.

C: If $T \sim \mathrm{Exp}(\lambda)$, then $E[T] = [1/\lambda]$, where $\lambda$ is the rate parameter.

Q: Why does $E[T] = 1/\lambda$ for $T \sim \mathrm{Exp}(\lambda)$ make intuitive sense?
A: The parameter $\lambda$ is the average number of events per unit time. If events happen on average $\lambda$ times per second, the average time between events is $1/\lambda$ seconds — rate and mean waiting time are reciprocals.

C: If $T \sim \mathrm{Exp}(\lambda)$, then $\mathrm{Var}(T) = [1/\lambda^2]$, where $\lambda$ is the rate parameter.

Q: Why does the exponential distribution have $\mathrm{Var}(T) = 1/\lambda^2$ equal to the square of its mean?
A: The exponential is a one-parameter family: $\lambda$ sets both a location scale ($1/\lambda$) and a variability scale. Since variance has units of time$^2$ and the only time scale available is $1/\lambda$, dimensional reasoning forces $\mathrm{Var}(T) \propto 1/\lambda^2$; the constant of proportionality happens to be $1$.

## 7.4 Memoryless property of exponential

Q: What does it mean for a distribution to be "memoryless"?
A: Given that the event hasn't happened by time $s$, the remaining waiting time has the same distribution as a fresh start — the past is forgotten. Formally, $P(T > s + t \mid T > s) = P(T > t)$ for all $s, t \geq 0$.

C: A nonnegative random variable $T$ is called [memoryless] if $P(T > s + t \mid T > s) = P(T > t)$ for all $s, t \geq 0$.

Q: Why is the exponential the only continuous distribution on $[0, \infty)$ that is memoryless?
A: The memoryless condition $P(T > s+t) = P(T > s)\,P(T > t)$ is Cauchy's multiplicative functional equation on the survival function, whose only continuous solutions are exponentials $e^{-\lambda t}$. So any continuous memoryless waiting time must be $\mathrm{Exp}(\lambda)$ for some $\lambda > 0$.

P: Show that if $T \sim \mathrm{Exp}(\lambda)$, then $P(T > s + t \mid T > s) = P(T > t)$.

S:
**IDENTIFY**: Prove the memoryless property of the exponential distribution.

**PLAN**:
- Use the definition of conditional probability.
- Use the survival function $P(T > t) = e^{-\lambda t}$.

**EXECUTE**:
1. $P(T > s+t \mid T > s) = \dfrac{P(T > s+t \text{ and } T > s)}{P(T > s)}$.
2. Since $s + t \geq s$, the event $\{T > s+t\}$ is contained in $\{T > s\}$, so the numerator is $P(T > s+t) = e^{-\lambda(s+t)}$.
3. Denominator: $P(T > s) = e^{-\lambda s}$.
4. Ratio: $e^{-\lambda(s+t)}/e^{-\lambda s} = e^{-\lambda t} = P(T > t)$.

**EVALUATE**:
- The conditional survival probability equals the unconditional one, so the exponential is memoryless. ✓
- Intuition: conditioning on "no event by $s$" and restarting the clock gives a fresh exponential.

Q: Why does the memoryless property make the exponential a poor model for human lifetimes?
A: For humans, the probability of surviving another year depends strongly on current age — a 90-year-old is less likely to survive another year than a 20-year-old. The exponential forgets the past, so it predicts the same residual life at every age, which contradicts aging.

## 7.5 Exponential as continuous analog of geometric

Q: How does the exponential distribution relate to the geometric distribution?
A: The geometric counts the number of Bernoulli trials until the first success; the exponential measures the continuous time until the first event of a Poisson process. Both model "waiting for the first success" and both are the unique memoryless distributions on their respective supports ($\mathbb{N}$ vs $[0,\infty)$).

C: The exponential distribution is the continuous analog of the [geometric] distribution, both being the unique memoryless distributions on their supports.

Q: Why do exponential interarrival times characterize a Poisson process?
A: If events occur at a constant rate $\lambda$ and independently of history, the time between successive events must be memoryless and hence exponential with rate $\lambda$. Conversely, iid $\mathrm{Exp}(\lambda)$ interarrival times generate counts that are $\mathrm{Poisson}(\lambda t)$ on any interval of length $t$.

C: In a Poisson process of rate $\lambda$, the times between consecutive events ([interarrival times]) are iid $\mathrm{Exp}(\lambda)$, where $\lambda$ is the event rate.

Q: If buses arrive as a Poisson process at rate $\lambda = 1/10$ per minute, what is the expected wait for the next bus?
A: $1/\lambda = 10$ minutes. By memorylessness, this holds no matter how long you've already been waiting — a notorious counterintuitive feature of Poisson-arrival systems.

## 7.6 Normal (Gaussian) $N(\mu, \sigma^2)$

Q: Why is the normal distribution so ubiquitous in probability and statistics?
A: The Central Limit Theorem says that sums of many independent, finite-variance contributions converge to a normal distribution regardless of the individual components' shapes. Measurement errors, aggregated noise, and averages therefore tend to be approximately normal in a huge range of applications.

C: A random variable $X$ has the [normal distribution] with mean $\mu$ and variance $\sigma^2$, written $X \sim N(\mu, \sigma^2)$, if its PDF is $f(x) = \tfrac{1}{\sigma\sqrt{2\pi}} e^{-(x-\mu)^2/(2\sigma^2)}$, where $\mu$ is the mean and $\sigma > 0$ is the standard deviation.

C: The PDF of $X \sim N(\mu, \sigma^2)$ is $f(x) = [\tfrac{1}{\sigma\sqrt{2\pi}} e^{-(x-\mu)^2/(2\sigma^2)}]$, where $\mu$ is the mean and $\sigma$ is the standard deviation.

Q: What role does each parameter ($\mu$ and $\sigma$) play in the shape of the normal PDF?
A: $\mu$ shifts the bell curve horizontally — it is both the mean and the axis of symmetry. $\sigma$ controls the spread: larger $\sigma$ gives a shorter, wider bell; smaller $\sigma$ gives a taller, narrower bell. Area under the curve is always $1$.

Q: Why is the normal PDF symmetric about $\mu$?
A: The PDF depends on $x$ only through $(x-\mu)^2$, which is unchanged when $x$ is replaced by $2\mu - x$ (reflection through $\mu$). Hence $f(\mu + h) = f(\mu - h)$ for all $h$, which is exactly the definition of symmetry about $\mu$.

C: If $X \sim N(\mu, \sigma^2)$, then $E[X] = [\mu]$, where $\mu$ is the mean parameter.

C: If $X \sim N(\mu, \sigma^2)$, then $\mathrm{Var}(X) = [\sigma^2]$, where $\sigma$ is the standard deviation parameter.

Q: Why is the normal family closed under affine transformations?
A: If $X \sim N(\mu, \sigma^2)$ and $Y = aX + b$ with $a \neq 0$, then $Y$ has a PDF that, after substitution, is again Gaussian — specifically $Y \sim N(a\mu + b, a^2 \sigma^2)$. Shifts and rescalings of a bell curve are still bell curves.

C: If $X \sim N(\mu, \sigma^2)$ and $Y = aX + b$ with $a \neq 0$, then $Y \sim [N(a\mu + b, a^2\sigma^2)]$, where $a, b$ are real constants.

Q: Predict before the formula: if $X$ has mean $\mu$ and standard deviation $\sigma$, what linear transformation would produce a variable with mean $0$ and standard deviation $1$?
A: Subtract $\mu$ to center at zero, then divide by $\sigma$ to rescale the spread to $1$. That is, $Z = (X - \mu)/\sigma$.

C: The [standardization] of $X \sim N(\mu, \sigma^2)$ is $Z = (X-\mu)/\sigma$, where $\mu$ is the mean and $\sigma$ is the standard deviation.

Q: Why does standardization turn any normal variable into $N(0,1)$?
A: Affine transformations of a normal are normal. Subtracting $\mu$ gives mean $0$; dividing by $\sigma$ gives variance $\sigma^2/\sigma^2 = 1$. So $Z = (X-\mu)/\sigma \sim N(0,1)$ regardless of the original $\mu, \sigma$.

P: Given $X \sim N(100, 225)$, compute $P(X \leq 130)$ using standardization.

S:
**IDENTIFY**: Compute a probability for a general normal using the standard normal CDF $\Phi$.

**PLAN**:
- Read off $\mu = 100$, $\sigma = \sqrt{225} = 15$.
- Standardize: $Z = (X - \mu)/\sigma$.
- Express the target event in terms of $Z$ and evaluate $\Phi$.

**EXECUTE**:
1. $P(X \leq 130) = P\!\left(\dfrac{X - 100}{15} \leq \dfrac{130 - 100}{15}\right) = P(Z \leq 2)$.
2. From a $\Phi$ table, $\Phi(2) \approx 0.9772$.

**EVALUATE**:
- $130$ is two standard deviations above the mean; by the 68-95-99.7 rule, about $97.5\%$ of mass lies below $\mu + 2\sigma$, matching $\Phi(2) \approx 0.9772$. ✓

## 7.7 Standard normal $\Phi(z)$

C: The [standard normal distribution] is $N(0,1)$, with PDF $\varphi(z) = \tfrac{1}{\sqrt{2\pi}} e^{-z^2/2}$ for $z \in \mathbb{R}$.

C: The CDF of the standard normal is denoted $[\Phi(z)] = P(Z \leq z)$ where $Z \sim N(0,1)$.

Q: Why is there no closed-form expression for $\Phi(z)$ in terms of elementary functions?
A: The integrand $e^{-z^2/2}$ has no antiderivative expressible with elementary functions. $\Phi$ is therefore defined only via its integral (or equivalently the error function), and practical values come from tables or numerical approximations.

C: By symmetry of the standard normal about $0$, $\Phi(-z) = [1 - \Phi(z)]$, where $z$ is any real number.

Q: Why does $\Phi(-z) = 1 - \Phi(z)$ hold for the standard normal?
A: The PDF $\varphi$ is even, so $P(Z \leq -z) = P(Z \geq z) = 1 - P(Z \leq z) = 1 - \Phi(z)$. The identity just expresses that the two tails beyond $\pm z$ have equal mass.

C: The [68-95-99.7 rule] states that if $X \sim N(\mu, \sigma^2)$, then approximately $68\%$ of the mass lies in $\mu \pm \sigma$, $95\%$ in $\mu \pm 2\sigma$, and $[99.7\%]$ in $\mu \pm 3\sigma$.

Q: Why is the 68-95-99.7 rule worth memorizing rather than just looking up $\Phi$?
A: It lets you do normal probability estimates in your head. Seeing that an observation is "three standard deviations away" immediately flags it as extremely unlikely ($< 0.3\%$), without opening a table or calling a library.

Q: Using the 68-95-99.7 rule, what fraction of a normal distribution lies more than $2\sigma$ above the mean?
A: About $2.5\%$. $95\%$ is inside $\mu \pm 2\sigma$, so $5\%$ is outside, split equally between the two tails by symmetry.

## 7.8 Gamma distribution

Q: Why introduce the gamma distribution when we already have the exponential?
A: The exponential models the time to one event; summing $k$ independent $\mathrm{Exp}(\lambda)$ times (the time to the $k$-th event of a Poisson process) gives a new distribution with a flexible shape. The gamma family generalizes this to a continuous shape parameter $\alpha > 0$, covering many waiting-time and positive-valued models.

C: A random variable $X > 0$ has the [gamma distribution] with shape $\alpha > 0$ and rate $\beta > 0$, written $X \sim \mathrm{Gamma}(\alpha, \beta)$, where $\alpha$ controls the shape and $\beta$ is the rate parameter.

C: The PDF of $X \sim \mathrm{Gamma}(\alpha, \beta)$ is $f(x) = [\tfrac{\beta^\alpha}{\Gamma(\alpha)} x^{\alpha - 1} e^{-\beta x}]$ for $x > 0$, where $\alpha$ is shape, $\beta$ is rate, and $\Gamma$ is the gamma function.

C: The [gamma function] is defined by $\Gamma(\alpha) = \int_0^\infty t^{\alpha - 1} e^{-t}\,dt$ for $\alpha > 0$ and satisfies $\Gamma(n) = (n-1)!$ for positive integers $n$.

Q: Why does $\Gamma(\alpha)$ appear as a normalizing constant in the gamma PDF?
A: The unnormalized density $x^{\alpha-1} e^{-\beta x}$ integrates (after substituting $t = \beta x$) to $\Gamma(\alpha)/\beta^\alpha$. Dividing by this gives a proper PDF, so $\beta^\alpha / \Gamma(\alpha)$ is exactly the constant that makes the total probability equal $1$.

C: If $X \sim \mathrm{Gamma}(\alpha, \beta)$, then $E[X] = [\alpha/\beta]$, where $\alpha$ is the shape and $\beta$ is the rate.

C: If $X \sim \mathrm{Gamma}(\alpha, \beta)$, then $\mathrm{Var}(X) = [\alpha/\beta^2]$, where $\alpha$ is the shape and $\beta$ is the rate.

Q: Why are the gamma moments $E[X] = \alpha/\beta$ and $\mathrm{Var}(X) = \alpha/\beta^2$ consistent with the exponential case?
A: An $\mathrm{Exp}(\lambda)$ is a $\mathrm{Gamma}(1, \lambda)$: shape $\alpha = 1$, rate $\beta = \lambda$. Then $E[X] = 1/\lambda$ and $\mathrm{Var}(X) = 1/\lambda^2$, recovering exactly the exponential formulas.

Q: If $X_1, \ldots, X_k$ are iid $\mathrm{Exp}(\lambda)$, what is the distribution of $S = X_1 + \cdots + X_k$?
A: $S \sim \mathrm{Gamma}(k, \lambda)$ — a gamma with integer shape, also known as the Erlang distribution. Intuition: $S$ is the time to the $k$-th event of a Poisson process of rate $\lambda$.

C: The sum of $k$ independent $\mathrm{Exp}(\lambda)$ random variables is [$\mathrm{Gamma}(k, \lambda)$], the Erlang distribution with shape $k$ and rate $\lambda$.

## 7.9 Chi-square as special case of gamma

Q: Why does the chi-square distribution appear so often in statistics?
A: Sums of squared independent standard normals are chi-square distributed, and many standard test statistics (sample variances, goodness-of-fit statistics, likelihood ratios) reduce to such sums. So chi-square is the natural distribution of "squared-error" quantities under normal assumptions.

C: A random variable $X$ has the [chi-square distribution] with $k$ degrees of freedom, written $X \sim \chi^2_k$, if it has the same distribution as $Z_1^2 + \cdots + Z_k^2$ where the $Z_i$ are iid $N(0,1)$.

C: The chi-square distribution with $k$ degrees of freedom equals [$\mathrm{Gamma}(k/2, 1/2)$], i.e. shape $\alpha = k/2$ and rate $\beta = 1/2$.

Q: Why does $\chi^2_k = \mathrm{Gamma}(k/2, 1/2)$?
A: The square of a single $N(0,1)$ is $\mathrm{Gamma}(1/2, 1/2)$ (a direct change-of-variables calculation). Independent gammas with the same rate add their shape parameters, so $k$ iid copies sum to $\mathrm{Gamma}(k/2, 1/2)$, which is $\chi^2_k$ by definition.

C: If $X \sim \chi^2_k$, then $E[X] = [k]$ and $\mathrm{Var}(X) = 2k$, where $k$ is the number of degrees of freedom.

Q: Why is $E[\chi^2_k] = k$ intuitive?
A: $\chi^2_k$ is the sum of $k$ iid squares of $N(0,1)$ variables. Each $Z_i^2$ has mean $\mathrm{Var}(Z_i) = 1$, so the total expected value is $k \cdot 1 = k$ by linearity of expectation.

## 7.10 Beta distribution on $[0,1]$

Q: Why do we need a distribution supported on $[0,1]$?
A: Many quantities are naturally proportions or probabilities — rates, fractions, Bayesian posterior probabilities — and these live in $[0,1]$. The beta family gives a flexible, two-parameter toolbox of shapes on $[0,1]$, from uniform to U-shaped to peaked.

C: A random variable $X \in [0,1]$ has the [beta distribution] with shape parameters $\alpha > 0$ and $\beta > 0$, written $X \sim \mathrm{Beta}(\alpha, \beta)$, where both parameters control the shape on $[0,1]$.

C: The PDF of $X \sim \mathrm{Beta}(\alpha, \beta)$ is $f(x) = [\tfrac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha, \beta)}]$ for $x \in [0,1]$, where $B(\alpha,\beta) = \Gamma(\alpha)\Gamma(\beta)/\Gamma(\alpha+\beta)$ is the beta function.

Q: What qualitative shape does the beta PDF take for different $(\alpha, \beta)$?
A: $\alpha = \beta = 1$ gives uniform; $\alpha, \beta > 1$ gives a unimodal bump whose peak shifts toward $\alpha/(\alpha+\beta)$; $\alpha, \beta < 1$ gives a U-shape (mass piled near $0$ and $1$); $\alpha \neq \beta$ gives asymmetry.

C: If $X \sim \mathrm{Beta}(\alpha, \beta)$, then $E[X] = [\tfrac{\alpha}{\alpha + \beta}]$, where $\alpha, \beta$ are the two shape parameters.

Q: Why is $E[X] = \alpha/(\alpha + \beta)$ a sensible formula for a beta mean?
A: In the Bayesian "successes and failures" interpretation, $\alpha$ counts successes (including a prior) and $\beta$ counts failures. The expected proportion of successes is then successes/total = $\alpha/(\alpha + \beta)$, exactly mirroring a sample proportion.

C: The $\mathrm{Beta}(1,1)$ distribution is identical to the [uniform] distribution on $[0,1]$.

Q: Why is $\mathrm{Beta}(1,1) = U(0,1)$?
A: With $\alpha = \beta = 1$, the PDF is $x^0 (1-x)^0 / B(1,1) = 1/1 = 1$ on $[0,1]$ — the constant density, which is exactly the uniform distribution.

Q: What does it mean for the beta distribution to be a "conjugate prior" for the Bernoulli/binomial likelihood?
A: If the prior on a success probability $p$ is $\mathrm{Beta}(\alpha, \beta)$ and the data are Bernoulli/binomial with $s$ successes and $f$ failures, the posterior is $\mathrm{Beta}(\alpha + s, \beta + f)$ — same family, parameters updated by counts. This closure under Bayesian updating makes calculations tractable.

C: The beta distribution is the [conjugate prior] for the Bernoulli/binomial likelihood, with posterior $\mathrm{Beta}(\alpha + s, \beta + f)$ given $s$ successes and $f$ failures.

P: You observe 7 heads in 10 flips of a coin. Using a $\mathrm{Beta}(1,1)$ prior on the head probability $p$, find the posterior distribution and the posterior mean of $p$.

S:
**IDENTIFY**: Bayesian update with a beta prior and binomial likelihood.

**PLAN**:
- Use conjugacy: prior $\mathrm{Beta}(\alpha, \beta)$ with $s$ successes and $f$ failures gives posterior $\mathrm{Beta}(\alpha + s, \beta + f)$.
- Use $E[X] = \alpha/(\alpha+\beta)$ for the posterior mean.

**EXECUTE**:
1. Prior parameters: $\alpha = 1$, $\beta = 1$.
2. Data: $s = 7$ heads, $f = 3$ tails.
3. Posterior: $\mathrm{Beta}(1 + 7, 1 + 3) = \mathrm{Beta}(8, 4)$.
4. Posterior mean: $8/(8 + 4) = 8/12 = 2/3$.

**EVALUATE**:
- The uniform prior is equivalent to "$1$ pseudo-head and $1$ pseudo-tail." After data, we have effectively $8$ heads and $4$ tails, so the posterior mean $2/3$ is a mild shrinkage of the raw estimate $7/10 = 0.7$ toward $1/2$. ✓

## 7.11 Relationships between distributions

Q: Why is it useful to know the relationships between named distributions?
A: Knowing that one distribution is a special case or a transformation of another lets you reuse formulas, derive properties quickly, and recognize familiar structure in unfamiliar problems. It also reveals the unity behind an otherwise long list of definitions.

C: The exponential distribution is the special case [$\mathrm{Gamma}(1, \lambda)$] of the gamma family, with shape $\alpha = 1$ and rate $\beta = \lambda$.

C: The sum of $k$ iid $\mathrm{Exp}(\lambda)$ random variables is $\mathrm{Gamma}(k, \lambda)$, linking exponential to [gamma] via convolution.

C: The chi-square distribution $\chi^2_k$ is the special case [$\mathrm{Gamma}(k/2, 1/2)$] of gamma, arising as a sum of squares of $k$ iid $N(0,1)$ variables.

C: The uniform distribution $U(0,1)$ is the special case [$\mathrm{Beta}(1,1)$] of the beta family.

Q: Why can we view normal → chi-square as "squaring standard normals"?
A: $Z^2$ for $Z \sim N(0,1)$ is $\chi^2_1$ by definition (and equivalently $\mathrm{Gamma}(1/2, 1/2)$). Summing $k$ independent such squares gives $\chi^2_k$. So chi-square is literally the distribution of squared-error sums from normal data.

Q: Why can we view uniform → beta as a generalization of a flat density?
A: $\mathrm{Beta}(1,1)$ has constant PDF equal to $1$ on $[0,1]$ — the uniform. Moving $\alpha, \beta$ away from $1$ bends the constant density into unimodal or U-shaped curves while keeping the support $[0,1]$, so beta is a one-step generalization of uniform.

Q: In one sentence each, when would you reach for each of uniform, exponential, normal, gamma, beta?
A: Uniform — complete ignorance on a bounded interval; exponential — memoryless waiting times / Poisson-process gaps; normal — sums/averages, measurement error, the CLT limit; gamma — times to the $k$-th event or other positive continuous data with flexible shape; beta — proportions and Bayesian priors on probabilities.

C: The table of conjugate relationships: [beta] is conjugate to Bernoulli/binomial, and gamma is conjugate to Poisson rate and exponential rate.

Q: Why do we say the gamma distribution is the conjugate prior for the rate $\lambda$ of an exponential likelihood?
A: If $\lambda \sim \mathrm{Gamma}(\alpha, \beta)$ a priori and we observe $n$ iid exponential waiting times summing to $T$, the posterior is $\mathrm{Gamma}(\alpha + n, \beta + T)$ — the same family, with updated parameters. This parallels the beta/Bernoulli conjugacy and makes sequential updating trivial.
