+++
order = 5
tags = ["math", "probability", "distributions", "bernoulli", "binomial", "geometric", "poisson", "hypergeometric"]
+++

# Probability — Common Discrete Distributions

## 5.1 Why Study Named Distributions?

Q: Why devote a chapter to specific named distributions rather than treating every problem from scratch?
A: A handful of random experiments — coin flips, waiting for successes, counting rare events, sampling without replacement — recur across nearly every application of probability. Named distributions package the PMF, expectation, and variance for each pattern once and for all, so that recognising the experiment's structure immediately gives you the answer. This turns modelling into pattern-matching rather than repeated derivation.

Q: Why is "recognising the distribution" more valuable than memorising the PMF?
A: The hard part of applied probability is translating a word problem into the right mathematical object. Once you identify the experiment as, say, "trials until the first success with fixed probability $p$", the formulas for $E$ and $\mathrm{Var}$ follow mechanically. Misidentifying the distribution — e.g. confusing binomial with hypergeometric — produces wrong answers even with perfect algebra.

C: A [named distribution] is a probability distribution with a standard parametric form that arises repeatedly in applications.

Q: What four ingredients specify a discrete distribution in this chapter?
A: (1) The sample space of values the random variable can take, (2) the PMF $P(X = k)$, (3) the expectation $E[X]$, and (4) the variance $\mathrm{Var}(X)$. Together these let you compute any probability and summarise the distribution's centre and spread.

## 5.2 Bernoulli Distribution

Q: Why is the Bernoulli distribution the foundation for almost all other discrete distributions in this chapter?
A: A Bernoulli random variable models a single trial with two outcomes (success or failure). Binomial, geometric, and negative binomial distributions are all built from sums or waiting times of independent Bernoulli trials. Understanding the Bernoulli case first means the others reduce to counting and combinatorics applied to a known atomic piece.

C: A [Bernoulli random variable] $X$ takes the value 1 (success) with probability $p$ and the value 0 (failure) with probability $1 - p$, where $p \in [0, 1]$ is the success parameter.

C: The PMF of a Bernoulli$(p)$ variable $X$ is $P(X = 1) = p$ and $P(X = 0) = [1 - p]$, where $p$ is the probability of success on a single trial.

C: The expectation of $X \sim \mathrm{Bernoulli}(p)$ is $E[X] = [p]$, where $p$ is the probability of success.

Q: Why does $E[X] = p$ for a Bernoulli$(p)$ variable?
A: By definition $E[X] = 1 \cdot P(X=1) + 0 \cdot P(X=0) = 1 \cdot p + 0 \cdot (1-p) = p$. The expectation of an indicator is just the probability of the event it indicates.

C: The variance of $X \sim \mathrm{Bernoulli}(p)$ is $\mathrm{Var}(X) = [p(1-p)]$, where $p$ is the success probability.

Q: Why is the variance of a Bernoulli random variable maximised at $p = 1/2$?
A: $\mathrm{Var}(X) = p(1-p)$ is a downward-opening parabola in $p$ with roots at $0$ and $1$, so it peaks at $p = 1/2$ with value $1/4$. Intuitively, a fair coin is the most uncertain trial; if $p$ is near 0 or 1 the outcome is nearly deterministic and variance shrinks.

Q: What is an indicator random variable, and how does it relate to Bernoulli?
A: An indicator $\mathbf{1}_A$ equals 1 if event $A$ occurs and 0 otherwise. It is exactly a Bernoulli variable with parameter $p = P(A)$, which is why indicators are the standard tool for converting event probabilities into expectations via linearity.

## 5.3 Binomial Distribution

Q: Why is the binomial distribution the natural next step after Bernoulli?
A: Many real experiments consist of repeating the same Bernoulli trial $n$ times independently and counting successes — think of $n$ coin flips or $n$ defective-item tests. The binomial distribution is literally the sum of $n$ i.i.d. Bernoulli$(p)$ variables, so it inherits its structure directly from the Bernoulli case.

C: A [binomial random variable] $X \sim \mathrm{Binomial}(n, p)$ counts the number of successes in $n$ independent Bernoulli$(p)$ trials, where $n \in \mathbb{N}$ is the number of trials and $p \in [0,1]$ is the per-trial success probability.

C: The PMF of $X \sim \mathrm{Binomial}(n, p)$ is $P(X = k) = [\binom{n}{k} p^k (1-p)^{n-k}]$ for $k \in \{0, 1, \ldots, n\}$, where $n$ is the number of trials, $p$ the success probability, and $k$ the number of successes.

Q: Why does the binomial PMF contain the factor $\binom{n}{k}$?
A: There are $\binom{n}{k}$ distinct sequences of $n$ trials that produce exactly $k$ successes (choosing which trials succeed). Each such sequence has probability $p^k (1-p)^{n-k}$ by independence, and the sequences are mutually exclusive, so we sum $\binom{n}{k}$ equal terms.

Q: Why is independence essential for the binomial formula?
A: The factorisation $p^k (1-p)^{n-k}$ assumes the joint probability of a specific success/failure pattern equals the product of the individual trial probabilities. Without independence, the joint probability can differ, so the PMF breaks.

C: The expectation of $X \sim \mathrm{Binomial}(n, p)$ is $E[X] = [np]$, where $n$ is the number of trials and $p$ the success probability.

Q: Why does $E[X] = np$ follow immediately from the Bernoulli case?
A: Write $X = Y_1 + Y_2 + \cdots + Y_n$ where each $Y_i \sim \mathrm{Bernoulli}(p)$. By linearity of expectation, $E[X] = \sum_{i=1}^n E[Y_i] = \sum_{i=1}^n p = np$. Linearity holds without needing independence.

C: The variance of $X \sim \mathrm{Binomial}(n, p)$ is $\mathrm{Var}(X) = [np(1-p)]$, where $n$ is the number of trials and $p$ the success probability.

Q: Why does $\mathrm{Var}(X) = np(1-p)$ require independence, unlike the expectation?
A: Variance of a sum equals the sum of variances only when the summands are uncorrelated. For $X = \sum Y_i$ with independent Bernoulli$(p)$ terms, $\mathrm{Var}(X) = \sum \mathrm{Var}(Y_i) = n \cdot p(1-p)$. If the trials were correlated, covariance terms would appear.

Q: If $X_1 \sim \mathrm{Binomial}(n_1, p)$ and $X_2 \sim \mathrm{Binomial}(n_2, p)$ are independent, what is the distribution of $X_1 + X_2$?
A: $X_1 + X_2 \sim \mathrm{Binomial}(n_1 + n_2, p)$. Each $X_i$ is a sum of $n_i$ independent Bernoulli$(p)$ trials, so their sum is a total of $n_1 + n_2$ independent Bernoulli$(p)$ trials. The common $p$ is essential.

## 5.4 Geometric Distribution

Q: Why do we need a separate distribution for "waiting for the first success"?
A: The binomial counts successes in a fixed number of trials, but many problems instead fix a target ("one success") and ask how many trials that requires — a random number. This "first-passage" viewpoint produces a distribution with infinite support and very different behaviour, including the memoryless property.

C: A [geometric random variable] $X \sim \mathrm{Geometric}(p)$ counts the number of independent Bernoulli$(p)$ trials up to and including the first success, where $p \in (0, 1]$.

C: The PMF of $X \sim \mathrm{Geometric}(p)$ is $P(X = k) = [(1-p)^{k-1} p]$ for $k \in \{1, 2, 3, \ldots\}$, where $p$ is the success probability and $k$ the trial on which the first success occurs.

Q: Why does the geometric PMF look like $(1-p)^{k-1} p$?
A: Getting the first success on trial $k$ requires $k-1$ failures, each with probability $1-p$, followed by a success with probability $p$. By independence the probabilities multiply, giving $(1-p)^{k-1} p$. There is only one such sequence, so no binomial coefficient appears.

C: The expectation of $X \sim \mathrm{Geometric}(p)$ is $E[X] = [1/p]$, where $p$ is the success probability.

Q: Why is $E[X] = 1/p$ intuitive for a geometric distribution?
A: If a trial succeeds with probability $p$, you expect roughly one success per $1/p$ trials — so the average wait for that one success is $1/p$ trials. For example, rolling a 6 on a fair die ($p = 1/6$) takes on average 6 rolls.

C: The variance of $X \sim \mathrm{Geometric}(p)$ is $\mathrm{Var}(X) = [(1-p)/p^2]$, where $p$ is the success probability.

Q: Why does the variance of a geometric variable blow up as $p \to 0$?
A: $\mathrm{Var}(X) = (1-p)/p^2$ diverges like $1/p^2$ as $p \to 0$. Rare-success waiting times are highly uncertain: you might get lucky early or wait enormously longer than the mean, and this spread dominates.

C: The geometric distribution has the [memoryless property]: $P(X > m + n \mid X > m) = P(X > n)$ for all non-negative integers $m, n$.

Q: Why is the geometric distribution memoryless?
A: Each trial is independent, so past failures give no information about when the next success will come. Given that you have already failed $m$ times, the remaining wait is a fresh geometric experiment — the "clock resets."

Q: Why is the geometric the only memoryless discrete distribution on $\{1, 2, 3, \ldots\}$?
A: Memorylessness forces the tail probabilities to satisfy $P(X > m + n) = P(X > m) P(X > n)$, a Cauchy-type functional equation whose only solutions in positive integers are $P(X > k) = (1-p)^k$. That tail uniquely determines the geometric PMF.

## 5.5 Negative Binomial Distribution

Q: Why generalise the geometric distribution to "waiting for the $r$-th success"?
A: Many processes have a success target greater than one — e.g. selling $r$ products, finding $r$ defective items, or completing $r$ milestones. The negative binomial captures the number of trials needed to achieve $r$ successes and reduces to the geometric when $r = 1$.

C: A [negative binomial random variable] $X \sim \mathrm{NegBin}(r, p)$ counts the number of independent Bernoulli$(p)$ trials up to and including the $r$-th success, where $r \in \mathbb{N}$ is the target number of successes and $p \in (0, 1]$.

C: The PMF of $X \sim \mathrm{NegBin}(r, p)$ is $P(X = k) = [\binom{k-1}{r-1} p^r (1-p)^{k-r}]$ for $k \in \{r, r+1, r+2, \ldots\}$, where $r$ is the target successes, $p$ the success probability, and $k$ the trial on which the $r$-th success occurs.

Q: Why does the negative binomial PMF include $\binom{k-1}{r-1}$ rather than $\binom{k}{r}$?
A: The $r$-th success must land on trial $k$ itself (fixed), so only the first $k-1$ trials are free to arrange the remaining $r-1$ successes. There are $\binom{k-1}{r-1}$ ways to place those successes among the first $k-1$ trials, giving the coefficient.

Q: Why can we write a negative binomial as a sum of geometric variables?
A: Waiting for $r$ successes is the same as waiting for the 1st, then the 2nd, ..., then the $r$-th. Each inter-success waiting time is an independent Geometric$(p)$ variable, and the total is their sum. This decomposition makes the expectation and variance immediate.

C: The expectation of $X \sim \mathrm{NegBin}(r, p)$ is $E[X] = [r/p]$, where $r$ is the target successes and $p$ the success probability.

Q: Why does $E[X] = r/p$ for the negative binomial?
A: Decompose $X = W_1 + W_2 + \cdots + W_r$ where each $W_i \sim \mathrm{Geometric}(p)$. By linearity, $E[X] = \sum_{i=1}^r E[W_i] = r \cdot (1/p) = r/p$.

C: The variance of $X \sim \mathrm{NegBin}(r, p)$ is $\mathrm{Var}(X) = [r(1-p)/p^2]$, where $r$ is the target successes and $p$ the success probability.

Q: Why does $\mathrm{Var}(X) = r(1-p)/p^2$ for the negative binomial?
A: The inter-success waits $W_i \sim \mathrm{Geometric}(p)$ are independent, so variances add: $\mathrm{Var}(X) = \sum_{i=1}^r \mathrm{Var}(W_i) = r \cdot (1-p)/p^2$.

Q: What does the negative binomial reduce to when $r = 1$, and why?
A: It reduces to the Geometric$(p)$ distribution. With $r = 1$, waiting for the "first success" is just waiting for a success, and the PMF collapses to $(1-p)^{k-1} p$ since $\binom{k-1}{0} = 1$.

## 5.6 Hypergeometric Distribution

Q: Why do we need a different distribution when sampling *without* replacement?
A: The binomial assumes each trial has the same success probability $p$, which requires replacement (or an infinite population). When you draw without replacement from a finite population, removing a success changes the remaining proportion, so trials are dependent and the binomial no longer applies.

C: A [hypergeometric random variable] $X \sim \mathrm{Hypergeometric}(N, K, n)$ counts successes in $n$ draws without replacement from a population of $N$ items containing exactly $K$ successes, where $N$ is population size, $K$ the number of successes in the population, and $n$ the sample size, with $0 \le n \le N$ and $0 \le K \le N$.

C: The PMF of $X \sim \mathrm{Hypergeometric}(N, K, n)$ is $P(X = k) = [\binom{K}{k} \binom{N-K}{n-k} / \binom{N}{n}]$, where $N$ is population size, $K$ the number of successes in the population, $n$ the sample size, and $k$ the observed number of successes.

Q: Why does the hypergeometric PMF use $\binom{K}{k} \binom{N-K}{n-k} / \binom{N}{n}$?
A: Treat it as a combinatorial probability: the number of ways to choose $k$ successes from the $K$ available and $n-k$ failures from the $N-K$ available, divided by the total number of ways to choose $n$ items from $N$. All samples of size $n$ are equally likely, so this ratio is exactly $P(X=k)$.

C: The expectation of $X \sim \mathrm{Hypergeometric}(N, K, n)$ is $E[X] = [n K / N]$, where $N$ is population size, $K$ the number of successes, and $n$ the sample size.

Q: Why does $E[X] = nK/N$ for the hypergeometric despite dependence between draws?
A: Use indicators $Y_i = 1$ if draw $i$ is a success. By symmetry each draw is equally likely to land on any item, so $P(Y_i = 1) = K/N$. Linearity of expectation does not require independence, giving $E[X] = n \cdot K/N$.

C: The variance of $X \sim \mathrm{Hypergeometric}(N, K, n)$ is $\mathrm{Var}(X) = [n \cdot \frac{K}{N} \cdot \frac{N-K}{N} \cdot \frac{N-n}{N-1}]$, where $N$ is population size, $K$ the number of successes, and $n$ the sample size.

C: In the hypergeometric variance, the extra factor $\frac{N-n}{N-1}$ compared to the binomial is called the [finite population correction].

Q: Why is the hypergeometric variance smaller than the corresponding binomial variance?
A: Sampling without replacement introduces negative correlation between draws: picking a success makes another success slightly less likely. This negative covariance reduces the variance, captured by the finite population correction factor $(N-n)/(N-1) \le 1$.

Q: Why does the hypergeometric distribution approach the binomial when $N$ is very large compared to $n$?
A: With $N \gg n$, removing $n$ items barely changes the population composition, so draws behave almost independently with $p \approx K/N$. Formally, $(N-n)/(N-1) \to 1$ and $\binom{K}{k}\binom{N-K}{n-k}/\binom{N}{n} \to \binom{n}{k} p^k (1-p)^{n-k}$.

## 5.7 Poisson Distribution

Q: Why do we need yet another distribution for "rare events"?
A: Many real counts — phone calls per hour, radioactive decays per second, typos per page — involve a large number of opportunities each with a tiny success probability. Neither the binomial (which needs a tractable $n$ and $p$) nor the geometric models this cleanly. The Poisson captures such counts with a single rate parameter $\lambda$.

C: A [Poisson random variable] $X \sim \mathrm{Poisson}(\lambda)$ takes values in $\{0, 1, 2, \ldots\}$ and models counts of events occurring at an average rate $\lambda > 0$ per unit of time, area, or opportunity.

C: The PMF of $X \sim \mathrm{Poisson}(\lambda)$ is $P(X = k) = [e^{-\lambda} \lambda^k / k!]$ for $k \in \{0, 1, 2, \ldots\}$, where $\lambda > 0$ is the mean rate and $k$ is the observed count.

Q: Why does the Poisson PMF sum to 1?
A: Summing over $k$: $\sum_{k=0}^\infty e^{-\lambda} \lambda^k / k! = e^{-\lambda} \sum_{k=0}^\infty \lambda^k / k! = e^{-\lambda} \cdot e^{\lambda} = 1$, using the Taylor series for $e^\lambda$. The factor $e^{-\lambda}$ is precisely the normalising constant that makes the probabilities total 1.

C: The expectation of $X \sim \mathrm{Poisson}(\lambda)$ is $E[X] = [\lambda]$, where $\lambda$ is the rate parameter.

C: The variance of $X \sim \mathrm{Poisson}(\lambda)$ is $\mathrm{Var}(X) = [\lambda]$, where $\lambda$ is the rate parameter.

Q: Why is the equality $E[X] = \mathrm{Var}(X) = \lambda$ distinctive of the Poisson?
A: Most distributions have expectation and variance governed by different parameters. In the Poisson a single parameter $\lambda$ controls both, so mean and variance are numerically equal. A sample mean much larger than the sample variance (or vice versa) is a common diagnostic that the data are not Poisson.

Q: If $X_1 \sim \mathrm{Poisson}(\lambda_1)$ and $X_2 \sim \mathrm{Poisson}(\lambda_2)$ are independent, what is the distribution of $X_1 + X_2$?
A: $X_1 + X_2 \sim \mathrm{Poisson}(\lambda_1 + \lambda_2)$. Independent Poisson counts over disjoint regions add, and the total rate is the sum of the individual rates. This is the "additivity" property of the Poisson.

## 5.8 Poisson as a Limit of Binomial

Q: Why does the Poisson distribution arise as a limit of binomial distributions?
A: If you imagine slicing a time interval into $n$ tiny slots, each with a small chance $p$ of containing an event, the total count is Binomial$(n, p)$. Taking $n \to \infty$ and $p \to 0$ with $np \to \lambda$ fixed (many opportunities, each rare, with stable average rate) produces the Poisson$(\lambda)$ distribution in the limit.

C: If $X_n \sim \mathrm{Binomial}(n, p_n)$ with $n \to \infty$ and $n p_n \to \lambda$, then $X_n$ converges in distribution to [$\mathrm{Poisson}(\lambda)$].

Q: Why does $\binom{n}{k} p^k (1-p)^{n-k} \to e^{-\lambda} \lambda^k / k!$ as $n \to \infty$ with $np \to \lambda$?
A: Substitute $p = \lambda/n$. Then $\binom{n}{k} (\lambda/n)^k \to \lambda^k / k!$ (since $n(n-1)\cdots(n-k+1)/n^k \to 1$), and $(1 - \lambda/n)^{n-k} \to e^{-\lambda}$. Multiplying gives the Poisson PMF.

Q: When is the Poisson approximation to the binomial a good rule of thumb?
A: When $n$ is large (say $n \ge 20$) and $p$ is small (say $p \le 0.05$), so that $np$ is a moderate number. In this regime the binomial PMF is numerically close to the Poisson PMF with $\lambda = np$, and Poisson formulas are far easier to work with.

Q: Why does the Poisson approximation fail when $p$ is close to $1/2$?
A: The derivation requires $p \to 0$ so that $(1-p)^{n-k}$ can be approximated by $e^{-\lambda}$. When $p$ is not small, this approximation is inaccurate and the binomial's finite-$n$ structure (bounded support, symmetric shape for $p=1/2$) differs sharply from the unbounded, right-skewed Poisson.

## 5.9 Discrete Uniform Distribution

Q: Why introduce the discrete uniform distribution?
A: It models situations with finitely many equally likely outcomes — rolling a fair die, drawing a card, selecting a random integer from a range. It is the baseline "no information favours any outcome" distribution and the starting point for combinatorial probability.

C: A [discrete uniform random variable] $X$ on $\{a, a+1, \ldots, b\}$ takes each of the $n = b - a + 1$ integer values with equal probability $1/n$, where $a$ and $b$ are integers with $a \le b$.

C: The PMF of a discrete uniform variable $X$ on $\{a, \ldots, b\}$ is $P(X = k) = [1/(b-a+1)]$ for each integer $k \in \{a, a+1, \ldots, b\}$.

C: The expectation of a discrete uniform variable $X$ on $\{a, \ldots, b\}$ is $E[X] = [(a+b)/2]$, where $a$ is the minimum value and $b$ the maximum.

Q: Why is $E[X] = (a+b)/2$ for the discrete uniform on $\{a, \ldots, b\}$?
A: By symmetry the distribution is balanced around its midpoint. Pair up the smallest and largest values ($a$ and $b$), the next pair ($a+1$ and $b-1$), and so on — each pair has average $(a+b)/2$. Since all values are equally likely, the overall mean is that same midpoint.

C: The variance of a discrete uniform variable $X$ on $\{a, \ldots, b\}$ with $n = b - a + 1$ values is $\mathrm{Var}(X) = [(n^2 - 1)/12]$, where $n$ is the number of equally likely values.

Q: Why does the variance of a discrete uniform grow with the number of values $n$?
A: Variance measures spread; adding more values on either side of the mean increases the typical squared deviation. The exact formula $(n^2-1)/12$ is quadratic in $n$, mirroring how the continuous uniform on an interval of length $L$ has variance $L^2/12$.

## 5.10 Choosing the Right Distribution

Q: What is the first question to ask when choosing a discrete distribution for a problem?
A: "Am I counting successes, or waiting for them?" Counting points to binomial, Poisson, or hypergeometric. Waiting points to geometric or negative binomial. Misreading this dichotomy is the most common modelling mistake.

Q: How do you decide between binomial and hypergeometric when counting successes?
A: Ask whether sampling is *with* or *without* replacement. With replacement (or an effectively infinite population) gives independent trials and the binomial. Without replacement from a finite population gives dependent trials and the hypergeometric.

Q: How do you decide between geometric and negative binomial when waiting for successes?
A: Ask how many successes you are waiting for. One success gives the geometric; $r > 1$ successes gives the negative binomial. The negative binomial reduces to geometric when $r = 1$.

Q: When should you reach for the Poisson distribution?
A: When counting rare events over a continuous interval (time, area, volume) where a single rate $\lambda$ summarises the average count. Also use it as an approximation to Binomial$(n, p)$ whenever $n$ is large, $p$ is small, and $np$ is moderate.

Q: When is the discrete uniform distribution the right model?
A: When all finitely many outcomes are equally likely by symmetry — e.g. a fair die, a well-shuffled card, a random integer drawn from a known range. If any outcome is favoured, the uniform is wrong.

P: A factory produces widgets, and each widget is independently defective with probability $p = 0.02$. In a random batch of $n = 150$ widgets, what distribution models the number of defective widgets, and what are its expectation and variance? Also estimate $P(X \le 2)$ using a suitable approximation.

S:
**IDENTIFY**: We count successes ("defective") in $n = 150$ independent trials with fixed probability $p = 0.02$ per trial. This is the binomial setup. Because $n$ is large and $p$ is small with $np = 3$ moderate, the Poisson approximation is appropriate.

**PLAN**:
- Step 1: Name the exact distribution of $X$ (defective count).
- Step 2: Compute $E[X]$ and $\mathrm{Var}(X)$ using binomial formulas.
- Step 3: Approximate by $\mathrm{Poisson}(\lambda)$ with $\lambda = np$ and compute $P(X \le 2)$.

**EXECUTE**:
1. $X \sim \mathrm{Binomial}(n, p) = \mathrm{Binomial}(150, 0.02)$.
2. $E[X] = np = 150 \cdot 0.02 = 3$. $\mathrm{Var}(X) = np(1-p) = 3 \cdot 0.98 = 2.94$.
3. Since $n = 150 \ge 20$ and $p = 0.02 \le 0.05$, approximate $X \approx \mathrm{Poisson}(\lambda)$ with $\lambda = np = 3$.
4. $P(X \le 2) = \sum_{k=0}^{2} e^{-3} 3^k / k! = e^{-3}(1 + 3 + 9/2) = e^{-3} \cdot 8.5 \approx 0.0498 \cdot 8.5 \approx 0.423$.

**EVALUATE**:
- Expected number of defectives is 3, so observing $\le 2$ should be slightly less than 50% probability — our $\approx 0.42$ is consistent.
- Binomial variance $2.94$ is slightly less than Poisson variance $3$; the difference $np^2 = 0.06$ is small, so the approximation is accurate.
- If we doubted independence (e.g. widgets produced in bursts of correlated defects), binomial would be wrong and we would need a different model.

P: A bag contains $N = 20$ marbles, of which $K = 6$ are red. You draw $n = 5$ marbles without replacement. Which distribution models the number of red marbles drawn, and what are its expectation and variance?

S:
**IDENTIFY**: Counting "successes" (red marbles) in a sample drawn *without replacement* from a finite population of fixed composition. This is the hypergeometric setup with $N = 20$, $K = 6$, $n = 5$.

**PLAN**:
- Step 1: Name the distribution.
- Step 2: Use $E[X] = nK/N$.
- Step 3: Use $\mathrm{Var}(X) = n \cdot \frac{K}{N} \cdot \frac{N-K}{N} \cdot \frac{N-n}{N-1}$.
- Step 4: Compare with the wrong "binomial" answer to see the finite-population correction.

**EXECUTE**:
1. $X \sim \mathrm{Hypergeometric}(N=20, K=6, n=5)$.
2. $E[X] = nK/N = 5 \cdot 6 / 20 = 1.5$.
3. $\mathrm{Var}(X) = 5 \cdot \frac{6}{20} \cdot \frac{14}{20} \cdot \frac{15}{19} = 5 \cdot 0.3 \cdot 0.7 \cdot (15/19) = 1.05 \cdot (15/19) \approx 0.829$.
4. If we had wrongly used Binomial$(5, 6/20)$, we would get $\mathrm{Var} = 5 \cdot 0.3 \cdot 0.7 = 1.05$ — larger, because it ignores the negative correlation from without-replacement sampling.

**EVALUATE**:
- $E[X] = 1.5$ agrees with intuition: on average you draw the population proportion $K/N = 30\%$ times the sample size $n = 5$.
- The finite population correction $(N-n)/(N-1) = 15/19 \approx 0.789$ shrinks the variance, matching the theoretical principle.
- With $n/N = 5/20 = 25\%$, the sample is not small relative to the population, so the hypergeometric (not binomial) is required for accuracy.

P: At a call centre, calls arrive independently at an average rate of $\lambda = 4$ per minute. Given a word problem like this, identify the distribution of the number of calls in the next minute, and compute $P(X = 0)$ and $P(X \ge 2)$.

S:
**IDENTIFY**: Counting events (calls) over a continuous time interval with a known average rate, no fixed upper bound, and independent arrivals. This is the classic Poisson setup with $\lambda = 4$ per minute.

**PLAN**:
- Step 1: Name the distribution.
- Step 2: Apply the Poisson PMF $P(X=k) = e^{-\lambda} \lambda^k / k!$.
- Step 3: Compute $P(X=0)$ directly.
- Step 4: Compute $P(X \ge 2) = 1 - P(X = 0) - P(X = 1)$.

**EXECUTE**:
1. $X \sim \mathrm{Poisson}(\lambda = 4)$, with $E[X] = \mathrm{Var}(X) = 4$.
2. $P(X = 0) = e^{-4} \cdot 4^0 / 0! = e^{-4} \approx 0.0183$.
3. $P(X = 1) = e^{-4} \cdot 4 / 1 = 4 e^{-4} \approx 0.0733$.
4. $P(X \ge 2) = 1 - P(X=0) - P(X=1) = 1 - 0.0183 - 0.0733 \approx 0.908$.

**EVALUATE**:
- With expected count 4, $P(X = 0)$ should be small (about 2%) and $P(X \ge 2)$ should be large — consistent with our answers.
- Using binomial here would require artificially choosing $n$ slots and $p$; Poisson is the natural continuous-time model.
- If the rate varied over time (e.g. calls spike at lunchtime), the homogeneous Poisson assumption would break and we would need a time-dependent intensity.

P: A basketball player sinks free throws independently with probability $p = 0.7$. Given a word problem asking for the distribution of the number of attempts up to and including their 3rd successful free throw, identify the distribution and compute $E[X]$ and $\mathrm{Var}(X)$.

S:
**IDENTIFY**: This is a "waiting for the $r$-th success" problem with $r = 3$ and per-trial success probability $p = 0.7$. Trials are independent and identically distributed Bernoulli$(p)$, so $X$ is negative binomial, not geometric (since $r > 1$) and not binomial (we are not counting successes in a fixed number of trials).

**PLAN**:
- Step 1: Name the distribution and parameters.
- Step 2: Apply $E[X] = r/p$.
- Step 3: Apply $\mathrm{Var}(X) = r(1-p)/p^2$.
- Step 4: Sanity-check by decomposing $X$ into geometric waits.

**EXECUTE**:
1. $X \sim \mathrm{NegBin}(r = 3, p = 0.7)$.
2. $E[X] = r/p = 3 / 0.7 \approx 4.29$ attempts.
3. $\mathrm{Var}(X) = r(1-p)/p^2 = 3 \cdot 0.3 / 0.49 \approx 1.84$.
4. Decomposition check: $X = W_1 + W_2 + W_3$ with each $W_i \sim \mathrm{Geometric}(0.7)$. Each $E[W_i] = 1/0.7$, each $\mathrm{Var}(W_i) = 0.3 / 0.49$. Summing three independent copies reproduces the answers above.

**EVALUATE**:
- The player makes 70% of shots, so they expect to need about $3/0.7 \approx 4.3$ attempts for 3 makes — reasonable.
- The minimum possible value of $X$ is 3 (all makes in a row), and the distribution has a long right tail, so the variance being moderate is consistent.
- If the shots were not independent (fatigue, streakiness), the negative binomial model would no longer apply.
