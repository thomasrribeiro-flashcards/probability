+++
order = 12
tags = ["math", "probability", "limit-theorems", "lln", "clt", "convergence", "inequalities"]
+++

# Probability — Limit Theorems

## 12.1 Why Limit Theorems?

Q: Why do we study limit theorems in probability?
A: Single outcomes of random experiments are unpredictable, but averages and sums of many independent trials behave in predictable, often deterministic, ways. Limit theorems describe this regularity — they tell us what happens as the sample size grows large, which is exactly the regime where statistics, simulation, and real-world inference live.

Q: Before reading the formal theorems, predict: what should happen to the sample mean $\bar{X}_n = \frac{1}{n}\sum_{i=1}^n X_i$ as $n \to \infty$ if each $X_i$ is iid with mean $\mu$?
A: It should approach $\mu$ — averages of many independent trials "wash out" randomness. The law of large numbers makes this precise; the central limit theorem then describes the fluctuations around $\mu$.

C: The [law of large numbers] describes the behavior of the sample mean as the sample size grows, while the [central limit theorem] describes the distribution of its fluctuations.

Q: What two distinct questions do the LLN and CLT answer about $\bar{X}_n$?
A: The LLN answers "where does $\bar{X}_n$ go?" — it converges to the mean $\mu$. The CLT answers "how fast, and with what distribution, does it fluctuate around $\mu$?" — the scaled deviation $\sqrt{n}(\bar{X}_n - \mu)$ is approximately normal.

## 12.2 Markov's Inequality

Q: Why do we want tail bounds like Markov's inequality?
A: Exact tail probabilities $P(X \geq a)$ are often hard to compute, yet we frequently only need an upper bound — enough to know the tail is small. Markov's inequality gives such a bound using only the mean, no other information about the distribution.

C: [Markov's inequality] states that for a nonnegative random variable $X$ and any $a > 0$, $P(X \geq a) \leq \frac{E[X]}{a}$, where $E[X]$ is the mean of $X$ and $a$ is the threshold.

Q: What assumption on $X$ is required for Markov's inequality?
A: $X$ must be nonnegative ($X \geq 0$ almost surely). Without this, the bound can fail because large negative values can inflate $P(X \geq a)$ without increasing $E[X]$ proportionally.

Q: Why is Markov's inequality considered a "weak" bound?
A: It uses only the mean — one piece of information about the distribution — so it cannot exploit additional structure (variance, higher moments, shape). Tighter bounds like Chebyshev use more information and are usually sharper.

P: Use Markov's inequality to bound $P(X \geq 10)$ for a nonnegative random variable $X$ with $E[X] = 2$.

S:
**IDENTIFY**: Tail bound problem for a nonnegative random variable using only the mean.

**PLAN**:
- Check nonnegativity assumption: given.
- Apply Markov: $P(X \geq a) \leq E[X]/a$ with $a = 10$, $E[X] = 2$.

**EXECUTE**:
1. $P(X \geq 10) \leq \frac{E[X]}{10} = \frac{2}{10} = 0.2$.

**EVALUATE**:
- The bound says at most 20% of the mass sits at or above 10.
- Sanity check: if $E[X] = 2$ and $P(X \geq 10) > 0.2$, then even setting all other mass to 0 would force $E[X] > 10 \cdot 0.2 = 2$, a contradiction. The bound is tight when $X$ is $10$ with probability $0.2$ and $0$ otherwise.

## 12.3 Chebyshev's Inequality

Q: Why do we need Chebyshev's inequality when we already have Markov's?
A: Markov uses only the mean and ignores how spread out $X$ is. Chebyshev uses the variance too, so it gives much tighter bounds whenever the variance is finite — particularly for deviations from the mean, which Markov cannot handle directly.

C: [Chebyshev's inequality] states that for a random variable $X$ with mean $\mu = E[X]$ and variance $\sigma^2 = \mathrm{Var}(X) < \infty$, $P(|X - \mu| \geq k\sigma) \leq \frac{1}{k^2}$ for any $k > 0$.

Q: In Chebyshev's inequality $P(|X - \mu| \geq k\sigma) \leq 1/k^2$, what does each symbol mean?
A: $X$ is the random variable, $\mu$ is its mean, $\sigma$ is its standard deviation, and $k$ is the number of standard deviations away from $\mu$. The right side $1/k^2$ is the upper bound on the probability of being at least $k$ SDs away.

Q: How is Chebyshev's inequality derived from Markov's inequality?
A: Apply Markov to the nonnegative random variable $Y = (X - \mu)^2$ with threshold $a = k^2\sigma^2$. Since $E[Y] = \sigma^2$, Markov gives $P((X-\mu)^2 \geq k^2\sigma^2) \leq \sigma^2/(k^2\sigma^2) = 1/k^2$, and the event equals $|X - \mu| \geq k\sigma$.

Q: According to Chebyshev, at least what fraction of the distribution lies within $k$ standard deviations of the mean?
A: At least $1 - 1/k^2$. For $k=2$: at least $75\%$. For $k=3$: at least $\approx 88.9\%$. This holds for any distribution with finite variance.

Q: Why does Chebyshev give trivial information for $k \leq 1$?
A: For $k = 1$, the bound is $1/k^2 = 1$, which is always true (all probabilities are $\leq 1$). For $k < 1$ it exceeds 1, which is even less informative. Chebyshev is useful only for $k > 1$.

P: A random variable $X$ has $\mu = 50$ and $\sigma = 5$. Bound $P(|X - 50| \geq 15)$ using Chebyshev.

S:
**IDENTIFY**: Tail bound for deviation from the mean, variance known.

**PLAN**:
- Express the threshold as $k\sigma$: $15 = k \cdot 5$, so $k = 3$.
- Apply Chebyshev: $P(|X - \mu| \geq k\sigma) \leq 1/k^2$.

**EXECUTE**:
1. $k = 15/5 = 3$.
2. $P(|X - 50| \geq 15) \leq 1/9 \approx 0.111$.

**EVALUATE**:
- At most about $11.1\%$ of the mass lies more than 3 SDs from the mean.
- The bound is distribution-free; specific distributions (e.g., normal) have much smaller actual tail probabilities ($\approx 0.0027$ for 3 SDs).

## 12.4 Convergence in Probability

Q: Why do we need a notion of convergence for random variables rather than just for numbers?
A: A sequence of random variables $X_1, X_2, \ldots$ doesn't have single numerical values that could converge — each $X_n$ is a whole distribution. "Convergence" of random variables must be phrased probabilistically: either the probability of large deviations shrinks, or individual sample paths settle down.

C: A sequence $X_n$ [converges in probability] to $X$, written $X_n \xrightarrow{P} X$, if for every $\epsilon > 0$, $\lim_{n \to \infty} P(|X_n - X| \geq \epsilon) = 0$, where $\epsilon$ is the tolerance and $X$ is the limiting random variable (often a constant).

Q: In plain words, what does $X_n \xrightarrow{P} X$ mean?
A: For any tolerance $\epsilon$, no matter how small, the probability that $X_n$ differs from $X$ by more than $\epsilon$ eventually becomes arbitrarily small as $n$ grows. Individual sample paths can still misbehave, but such misbehavior becomes increasingly rare.

Q: Why is the tolerance $\epsilon$ necessary in the definition of convergence in probability?
A: Without $\epsilon$, the event $|X_n - X| = 0$ typically has probability zero for continuous distributions, so the definition would trivially fail. Allowing any $\epsilon > 0$ captures "eventually close" rather than "eventually equal."

## 12.5 Almost Sure Convergence

C: A sequence $X_n$ [converges almost surely] to $X$, written $X_n \xrightarrow{a.s.} X$, if $P\!\left(\lim_{n \to \infty} X_n = X\right) = 1$, where the limit is taken pointwise on sample paths.

Q: Intuitively, what does almost sure convergence mean?
A: If you fix an outcome $\omega$ (a whole sample path) and watch the sequence $X_1(\omega), X_2(\omega), \ldots$ as numbers, that numerical sequence converges to $X(\omega)$. This happens for essentially every outcome — only a measure-zero set of "bad" paths is excluded.

Q: Why is almost sure convergence stronger than convergence in probability?
A: Almost sure convergence requires that nearly every individual sample path converges as a deterministic sequence. Convergence in probability only requires the probability of being far from the limit to shrink — it allows individual paths to keep jumping, as long as those jumps become rare.

C: Almost sure convergence is about the behavior of [individual sample paths], while convergence in probability is about the behavior of [probabilities of deviation].

## 12.6 Convergence in Distribution

C: A sequence $X_n$ [converges in distribution] to $X$, written $X_n \xrightarrow{d} X$, if $\lim_{n \to \infty} F_{X_n}(x) = F_X(x)$ at every point $x$ where $F_X$ is continuous, where $F_{X_n}$ and $F_X$ are the CDFs of $X_n$ and $X$.

Q: Why does the definition of convergence in distribution only require agreement at continuity points of $F_X$?
A: CDFs of discrete or mixed limits have jumps, and a small perturbation in $X_n$ could shift a jump location without changing the underlying distribution meaningfully. Requiring convergence at jump points would make many natural examples fail; restricting to continuity points fixes this while preserving the essential meaning.

Q: In plain words, what does $X_n \xrightarrow{d} X$ mean?
A: The distribution of $X_n$ — its CDF, its histogram shape — looks more and more like the distribution of $X$ as $n$ grows. The random variables themselves need not be close; only their distributions do.

Q: Why is convergence in distribution the weakest of the three modes?
A: It only constrains distributions, not the random variables themselves. Two sequences can converge in distribution to the same limit while being very different as functions on the sample space — they need not even be defined on the same probability space.

## 12.7 Relationships Among Modes of Convergence

C: Almost sure convergence implies [convergence in probability], which in turn implies [convergence in distribution].

Q: Write the chain of implications among the three modes of convergence.
A: $X_n \xrightarrow{a.s.} X \;\Longrightarrow\; X_n \xrightarrow{P} X \;\Longrightarrow\; X_n \xrightarrow{d} X$. None of the reverse implications hold in general.

Q: Why does convergence in probability NOT imply almost sure convergence?
A: Convergence in probability allows the "bad" event $|X_n - X| \geq \epsilon$ to occur infinitely often, as long as its probability shrinks with $n$. Individual sample paths can therefore keep failing to converge, violating the pathwise requirement of a.s. convergence.

Q: Under what special condition does convergence in distribution imply convergence in probability?
A: When the limit $X$ is a constant. If $X_n \xrightarrow{d} c$ for a constant $c$, then $X_n \xrightarrow{P} c$ as well. This matters because the WLLN's limit is the constant $\mu$.

## 12.8 Weak Law of Large Numbers (WLLN)

C: The [weak law of large numbers] states that if $X_1, X_2, \ldots$ are iid with finite mean $\mu = E[X_i]$, then the sample mean $\bar{X}_n = \frac{1}{n}\sum_{i=1}^n X_i$ satisfies $\bar{X}_n \xrightarrow{P} \mu$, where $\bar{X}_n$ is the sample mean of the first $n$ observations.

Q: What does the WLLN say in plain words?
A: If you average a large number of independent copies of the same random variable, the average is likely to be close to the true mean. The probability of a deviation greater than any fixed $\epsilon$ shrinks to zero as the sample size grows.

Q: How is the WLLN proved using Chebyshev's inequality (assuming finite variance)?
A: For iid $X_i$ with variance $\sigma^2$, $\mathrm{Var}(\bar{X}_n) = \sigma^2/n$. Apply Chebyshev: $P(|\bar{X}_n - \mu| \geq \epsilon) \leq \sigma^2/(n\epsilon^2) \to 0$ as $n \to \infty$. So $\bar{X}_n \xrightarrow{P} \mu$.

Q: Why does the WLLN justify the frequentist definition of probability?
A: If $X_i = \mathbb{1}\{A \text{ occurs on trial } i\}$, then $\bar{X}_n$ is the observed relative frequency of event $A$. The WLLN gives $\bar{X}_n \xrightarrow{P} E[X_i] = P(A)$, so long-run relative frequency converges to probability.

## 12.9 Strong Law of Large Numbers (SLLN)

C: The [strong law of large numbers] states that if $X_1, X_2, \ldots$ are iid with finite mean $\mu$, then $\bar{X}_n \xrightarrow{a.s.} \mu$, where $\bar{X}_n = \frac{1}{n}\sum_{i=1}^n X_i$ is the sample mean.

Q: What does "strong" mean in the strong law of large numbers?
A: "Strong" refers to the mode of convergence: almost surely, rather than merely in probability. The SLLN guarantees that for nearly every infinite sequence of outcomes, the running average actually converges as a numerical sequence to $\mu$.

Q: Why does the SLLN imply the WLLN but not vice versa?
A: Almost sure convergence implies convergence in probability. So whenever the SLLN holds, the WLLN automatically holds. The reverse fails because convergence in probability is a strictly weaker condition.

Q: Practically, why does it matter that the LLN is "strong" rather than just "weak"?
A: The SLLN justifies Monte Carlo simulation: a single long run of simulations is guaranteed (with probability one) to produce an average converging to the true expectation. The WLLN only says a single run is "likely" close — not that it actually converges.

## 12.10 Central Limit Theorem (CLT)

Q: Before stating the CLT, anticipate: if $\bar{X}_n \to \mu$ by the LLN, what should the fluctuations $\bar{X}_n - \mu$ look like as $n$ grows?
A: They shrink to zero, so to see nontrivial behavior we must zoom in — multiply by some increasing factor. The right scaling turns out to be $\sqrt{n}$, and the limiting distribution is the standard normal.

C: The [central limit theorem] states that if $X_1, X_2, \ldots$ are iid with mean $\mu$ and finite variance $\sigma^2 > 0$, then $\frac{\bar{X}_n - \mu}{\sigma/\sqrt{n}} \xrightarrow{d} Z$, where $Z \sim N(0,1)$ is standard normal and $\bar{X}_n$ is the sample mean of $n$ observations.

Q: In the CLT expression $\frac{\bar{X}_n - \mu}{\sigma/\sqrt{n}}$, what does each piece represent?
A: $\bar{X}_n$ is the sample mean; $\mu$ is the population mean; $\sigma$ is the population standard deviation; $\sigma/\sqrt{n}$ is the standard deviation of $\bar{X}_n$. The whole ratio is the standardized sample mean, which approaches $N(0,1)$.

Q: State the CLT in terms of the sum $S_n = \sum_{i=1}^n X_i$ rather than the sample mean.
A: $\frac{S_n - n\mu}{\sigma\sqrt{n}} \xrightarrow{d} N(0,1)$, where $S_n$ is the sum of $n$ iid random variables with mean $\mu$ and variance $\sigma^2$. Equivalently, $S_n$ is approximately $N(n\mu, n\sigma^2)$ for large $n$.

Q: Why is $\sqrt{n}$ the correct scaling factor in the CLT?
A: $\mathrm{Var}(\bar{X}_n) = \sigma^2/n$, so the standard deviation of $\bar{X}_n$ is $\sigma/\sqrt{n}$. Dividing by this quantity standardizes the fluctuation to unit variance, which is exactly what is needed to get a nondegenerate limit.

Q: What assumptions does the classical CLT require?
A: Three conditions: (1) the $X_i$ are independent, (2) they are identically distributed, and (3) they have finite variance $\sigma^2 > 0$. Finite mean follows from finite variance, so it's implicit.

Q: Why is the CLT such a remarkable result?
A: Regardless of the original distribution of $X_i$ — skewed, discrete, bimodal, anything with finite variance — the standardized sum approaches the same universal normal distribution. This explains why the normal appears everywhere in nature and statistics.

## 12.11 CLT Applications: Normal Approximation to Binomial

Q: Why does a binomial $\mathrm{Binomial}(n, p)$ become approximately normal for large $n$?
A: A $\mathrm{Binomial}(n, p)$ variable is the sum of $n$ iid Bernoulli($p$) indicators. Each Bernoulli has finite mean $p$ and variance $p(1-p)$, so the CLT applies and the standardized sum approaches $N(0, 1)$.

C: For $X \sim \mathrm{Binomial}(n, p)$ with $n$ large, $X$ is approximately $[N(np, np(1-p))]$, where $np$ is the mean and $np(1-p)$ is the variance of the binomial.

Q: What is a common rule of thumb for when the normal approximation to the binomial is reasonable?
A: Both $np \geq 10$ and $n(1-p) \geq 10$ (sometimes stated as $np \geq 5$ and $n(1-p) \geq 5$). This ensures the binomial has enough mass away from the boundaries 0 and $n$ for the normal shape to fit well.

Q: Why do we apply a continuity correction when approximating a discrete distribution with a continuous one?
A: The binomial is discrete (integer-valued), while the normal is continuous. Naively computing $P(X \leq k)$ as $P(N \leq k)$ mismatches at boundaries. Shifting by $\pm 0.5$ accounts for the fact that each integer $k$ "owns" the interval $[k-0.5, k+0.5]$ under the continuous approximation.

C: Using the [continuity correction], $P(X \leq k) \approx P(Y \leq k + 0.5)$ and $P(X \geq k) \approx P(Y \geq k - 0.5)$, where $X$ is the discrete variable and $Y$ is its continuous normal approximation.

P: Let $X \sim \mathrm{Binomial}(100, 0.5)$. Approximate $P(X \leq 60)$ using the normal approximation with continuity correction.

S:
**IDENTIFY**: Binomial tail probability, normal approximation via CLT, discrete variable so use continuity correction.

**PLAN**:
- Compute mean $\mu = np$ and variance $\sigma^2 = np(1-p)$.
- Apply continuity correction: $P(X \leq 60) \approx P(Y \leq 60.5)$ where $Y \sim N(\mu, \sigma^2)$.
- Standardize: $z = (60.5 - \mu)/\sigma$ and look up $\Phi(z)$.

**EXECUTE**:
1. $\mu = 100 \cdot 0.5 = 50$; $\sigma^2 = 100 \cdot 0.5 \cdot 0.5 = 25$; $\sigma = 5$.
2. Continuity-corrected bound: $60.5$.
3. $z = (60.5 - 50)/5 = 2.1$.
4. $P(X \leq 60) \approx \Phi(2.1) \approx 0.9821$.

**EVALUATE**:
- The approximation is good because $np = 50 \geq 10$ and $n(1-p) = 50 \geq 10$.
- Without continuity correction: $z = (60 - 50)/5 = 2$, giving $\Phi(2) \approx 0.9772$ — a noticeable underestimate.
- The corrected value $0.9821$ is closer to the exact binomial probability $\approx 0.9824$.

## 12.12 The Delta Method

Q: Why do we need the delta method beyond the CLT itself?
A: The CLT gives the asymptotic distribution of $\bar{X}_n$, but we often want the asymptotic distribution of a smooth function $g(\bar{X}_n)$ — for example, a log-odds, a ratio, or a variance estimator. The delta method transfers the CLT through such a function using a linear (Taylor) approximation.

C: The [delta method] states that if $\sqrt{n}(T_n - \theta) \xrightarrow{d} N(0, \sigma^2)$ and $g$ is differentiable at $\theta$ with $g'(\theta) \neq 0$, then $\sqrt{n}(g(T_n) - g(\theta)) \xrightarrow{d} N\!\left(0,\; [g'(\theta)]^2 \sigma^2\right)$, where $g'(\theta)$ is the derivative of $g$ at the true parameter $\theta$.

Q: What is the intuition behind the delta method?
A: Near $\theta$, the function $g$ is approximately linear: $g(T_n) \approx g(\theta) + g'(\theta)(T_n - \theta)$. A linear transformation of an asymptotically normal variable is also asymptotically normal, with variance scaled by $[g'(\theta)]^2$.

Q: What requirement on $g'(\theta)$ is essential for the standard delta method?
A: $g'(\theta) \neq 0$. If $g'(\theta) = 0$, the first-order linearization is zero and gives a degenerate limit; a second-order ("higher-order delta method") expansion involving $g''(\theta)$ and a chi-squared limit is then needed.

P: Given $\sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} N(0, \sigma^2)$, find the asymptotic distribution of $\sqrt{n}(\bar{X}_n^2 - \mu^2)$ using the delta method (assume $\mu \neq 0$).

S:
**IDENTIFY**: Transform an asymptotically normal statistic through a smooth function $g(x) = x^2$.

**PLAN**:
- Compute $g'(x) = 2x$, so $g'(\mu) = 2\mu$.
- Check $g'(\mu) = 2\mu \neq 0$ (given $\mu \neq 0$).
- Apply delta method: limit variance is $[g'(\mu)]^2 \sigma^2$.

**EXECUTE**:
1. $g(x) = x^2$, $g'(x) = 2x$, $g'(\mu) = 2\mu$.
2. $[g'(\mu)]^2 \sigma^2 = 4\mu^2 \sigma^2$.
3. $\sqrt{n}(\bar{X}_n^2 - \mu^2) \xrightarrow{d} N(0,\; 4\mu^2 \sigma^2)$.

**EVALUATE**:
- The variance scales with $\mu^2$: the further $\mu$ is from zero, the more sensitive $g(\bar{X}_n)$ is to fluctuations in $\bar{X}_n$.
- If $\mu = 0$, the method breaks down ($g'(0) = 0$) and a second-order expansion would yield a chi-squared limit instead.
