+++
order = 13
tags = ["math", "probability", "conditional-expectation", "tower-property", "markov-chains"]
+++

# Probability — Conditional Expectation and Markov Chains

## 13.1 Why Conditional Expectation as an RV?

Q: Why upgrade from plain conditional probability $P(A \mid B)$ to conditional expectation $E[Y \mid X]$?
A: Plain conditional probability answers "what is the chance of event $A$ given event $B$?" — a single number. Conditional expectation answers "what is the best prediction of a numerical quantity $Y$ given information about another quantity $X$?" — a whole function of $X$. It handles continuous random variables, captures both mean and variability, and supports chained predictions (tower property) that pure probabilities cannot.

Q: Why is $E[Y \mid X]$ itself a random variable rather than a number?
A: Because we have not fixed a particular outcome of $X$ yet. Each possible value $x$ of $X$ produces a possibly different conditional mean $E[Y \mid X = x]$. Bundling all those numbers into a single object — a function of $X$ — yields a random variable whose randomness is inherited from $X$.

Q: Why is $E[Y \mid X = x]$ (with $X$ fixed at value $x$) a number, but $E[Y \mid X]$ a random variable?
A: Fixing $X = x$ collapses the randomness in $X$, leaving a deterministic average over $Y$ — a single number. Leaving $X$ symbolic means its value has not been realized, so the conditional mean varies with the (still random) outcome of $X$.

Q: Why is conditional expectation more useful than conditional probability for regression problems?
A: Regression asks "given $X$, what value of $Y$ should I predict?" The answer is a number (or function), not a probability. $E[Y \mid X]$ directly produces that prediction for every $x$, while conditional probabilities only describe event chances.

## 13.2 Conditional Expectation $E[Y \mid X = x]$

C: The [conditional expectation] of $Y$ given $X = x$ is defined (discrete case) as $E[Y \mid X = x] = \sum_y y \, P(Y = y \mid X = x)$, where the sum runs over all possible values $y$ of $Y$ and $P(Y = y \mid X = x)$ is the conditional pmf.

C: For continuous random variables with joint density $f_{X,Y}(x,y)$, the conditional expectation is $E[Y \mid X = x] = \int_{-\infty}^{\infty} y \, f_{Y \mid X}(y \mid x) \, dy$, where $f_{Y \mid X}(y \mid x) = f_{X,Y}(x,y) / f_X(x)$ is the [conditional density] of $Y$ given $X = x$.

Q: In the formula $f_{Y \mid X}(y \mid x) = f_{X,Y}(x,y) / f_X(x)$, what does each symbol mean and what must hold for the formula to be valid?
A: $f_{X,Y}(x,y)$ is the joint density of $(X,Y)$, $f_X(x)$ is the marginal density of $X$ at value $x$, and $f_{Y \mid X}(y \mid x)$ is the conditional density of $Y$ given $X = x$. The formula requires $f_X(x) > 0$ (dividing by zero is undefined, matching the fact that conditioning on an impossible value makes no sense).

Q: Why does the formula $E[Y \mid X = x] = \sum_y y \, P(Y = y \mid X = x)$ mirror the unconditional formula $E[Y] = \sum_y y \, P(Y = y)$?
A: Conditional expectation is an ordinary expectation, but taken with respect to the conditional distribution instead of the marginal. Replacing $P(Y = y)$ by $P(Y = y \mid X = x)$ reweights outcomes by the knowledge that $X = x$; everything else about the averaging is identical.

C: If $X$ and $Y$ are independent, then $E[Y \mid X = x] = [E[Y]]$ for every $x$ in the support of $X$.

Q: Why does independence force $E[Y \mid X = x] = E[Y]$?
A: Independence means the conditional distribution of $Y$ given $X = x$ equals the marginal distribution of $Y$. Averaging $Y$ against the same distribution always yields the same number, so conditioning on $X$ provides no new information.

P: Let $(X,Y)$ be discrete with joint pmf $P(X=1,Y=1)=0.2$, $P(X=1,Y=2)=0.3$, $P(X=2,Y=1)=0.1$, $P(X=2,Y=2)=0.4$. Compute $E[Y \mid X = 1]$.

S:
**IDENTIFY**: Discrete conditional expectation — apply $E[Y \mid X = x] = \sum_y y \, P(Y = y \mid X = x)$ at $x = 1$.

**PLAN**:
- Compute the marginal $P(X = 1)$ by summing over $y$.
- Compute conditional pmf $P(Y = y \mid X = 1) = P(X = 1, Y = y)/P(X = 1)$.
- Sum $y \cdot P(Y = y \mid X = 1)$ over $y \in \{1, 2\}$.

**EXECUTE**:
1. $P(X = 1) = 0.2 + 0.3 = 0.5$.
2. $P(Y = 1 \mid X = 1) = 0.2 / 0.5 = 0.4$; $P(Y = 2 \mid X = 1) = 0.3 / 0.5 = 0.6$.
3. $E[Y \mid X = 1] = 1 \cdot 0.4 + 2 \cdot 0.6 = 0.4 + 1.2 = 1.6$.

**EVALUATE**: The conditional pmf sums to $0.4 + 0.6 = 1$ ✓. The answer $1.6$ lies in $[1,2]$, the support of $Y$, as it must for a weighted average.

## 13.3 Conditional Expectation as a Random Variable $E[Y \mid X]$

C: The [conditional expectation random variable] $E[Y \mid X]$ is the random variable obtained by applying the function $g(x) = E[Y \mid X = x]$ to $X$; that is, $E[Y \mid X] = g(X)$.

Q: If $g(x) = E[Y \mid X = x]$, why is $E[Y \mid X]$ equal to $g(X)$ and not to $g(x)$?
A: $g(x)$ is a number (or deterministic function evaluated at a specific $x$). $E[Y \mid X]$ is a random variable, so we must plug the random $X$ (not a fixed $x$) into $g$. The randomness of $X$ then makes $g(X)$ random too.

Q: What is the probability distribution of $E[Y \mid X]$ determined by?
A: By the distribution of $X$ alone: each value $x$ occurs with probability $P(X = x)$ (or density $f_X(x)$), and $E[Y \mid X]$ takes the value $g(x) = E[Y \mid X = x]$ there. So $E[Y \mid X]$ is a deterministic transformation of $X$.

C: $E[Y \mid X]$ is a function of $X$, meaning it is [$\sigma(X)$-measurable] — its value is completely determined once the value of $X$ is known.

Q: Why can $E[Y \mid X]$ be described as "the best guess of $Y$ from knowing $X$"?
A: It is computed by averaging $Y$ over exactly those outcomes consistent with each observed value of $X$. Once $X$ is observed, no finer information about $Y$ is available, so the conditional mean is the best single-number summary of $Y$ that uses only knowledge of $X$.

## 13.4 Tower Property (Law of Total Expectation)

C: The [tower property] (law of total expectation) states $E[Y] = E[E[Y \mid X]]$, where the outer expectation is taken over the distribution of $X$ and the inner expectation is over $Y$ given $X$.

Q: In the tower property $E[Y] = E[E[Y \mid X]]$, which variable does each expectation average over?
A: The inner $E[Y \mid X]$ averages $Y$ while holding $X$ fixed, producing a function of $X$. The outer $E[\cdot]$ then averages that function over the distribution of $X$. Together they recover the full unconditional mean of $Y$.

Q: Why does the tower property $E[Y] = E[E[Y \mid X]]$ make intuitive sense?
A: To find the overall average of $Y$, first find the average of $Y$ within each "slice" where $X = x$, then take a weighted average of those slice-averages using the probabilities of $X$. This is the discrete formula $E[Y] = \sum_x E[Y \mid X = x] P(X = x)$ in disguise.

C: The discrete form of the tower property is $E[Y] = \sum_x E[Y \mid X = x] \, P(X = x)$, where the sum runs over all values $x$ of $X$ and $[P(X = x)]$ is the marginal pmf of $X$.

P: An insurance company has two customer classes. Class 1 (probability $0.7$) has mean claim $\$500$; Class 2 (probability $0.3$) has mean claim $\$1500$. Find the overall mean claim $E[Y]$ using the tower property.

S:
**IDENTIFY**: Apply law of total expectation $E[Y] = \sum_x E[Y \mid X = x] \, P(X = x)$, where $X$ is the class indicator and $Y$ is the claim amount.

**PLAN**:
- Identify the two conditional means: $E[Y \mid X=1] = 500$, $E[Y \mid X=2] = 1500$.
- Multiply each by its class probability and sum.

**EXECUTE**:
1. $E[Y] = E[Y \mid X = 1] P(X = 1) + E[Y \mid X = 2] P(X = 2)$.
2. $E[Y] = 500 \cdot 0.7 + 1500 \cdot 0.3 = 350 + 450 = 800$.

**EVALUATE**: The result $\$800$ lies between $500$ and $1500$ as any weighted average must ✓. It is closer to $500$ since Class 1 is the more common class, matching intuition.

## 13.5 Conditional Variance $\mathrm{Var}(Y \mid X)$

C: The [conditional variance] of $Y$ given $X = x$ is $\mathrm{Var}(Y \mid X = x) = E[(Y - E[Y \mid X = x])^2 \mid X = x]$, the variance of $Y$ taken under the conditional distribution of $Y$ given $X = x$.

C: The computational form of conditional variance is $\mathrm{Var}(Y \mid X) = E[Y^2 \mid X] - (E[Y \mid X])^2$, the conditional analogue of $[\mathrm{Var}(Y) = E[Y^2] - (E[Y])^2]$.

Q: Why, like $E[Y \mid X]$, is $\mathrm{Var}(Y \mid X)$ a random variable rather than a number?
A: Each value $x$ of $X$ yields its own conditional variance $\mathrm{Var}(Y \mid X = x)$, a number describing spread of $Y$ within that slice. Since $X$ is random, which slice we land in is random, so $\mathrm{Var}(Y \mid X)$ inherits that randomness.

Q: What does $\mathrm{Var}(Y \mid X)$ intuitively measure?
A: The residual uncertainty about $Y$ after we observe $X$. If $X$ determines $Y$ exactly, $\mathrm{Var}(Y \mid X) = 0$. If $X$ gives no information, $\mathrm{Var}(Y \mid X) = \mathrm{Var}(Y)$.

## 13.6 Law of Total Variance

C: The [law of total variance] decomposes $\mathrm{Var}(Y)$ as $\mathrm{Var}(Y) = E[\mathrm{Var}(Y \mid X)] + \mathrm{Var}(E[Y \mid X])$, where the first term is the average within-group variance and the second is the variance between group means.

Q: In $\mathrm{Var}(Y) = E[\mathrm{Var}(Y \mid X)] + \mathrm{Var}(E[Y \mid X])$, what does each of the two terms represent?
A: $E[\mathrm{Var}(Y \mid X)]$ is the expected "within-group" spread — how much $Y$ still varies once $X$ is known, averaged across groups. $\mathrm{Var}(E[Y \mid X])$ is the "between-group" spread — how much the conditional mean itself varies across different values of $X$.

Q: Why must total variance equal within-group variance plus between-group variance?
A: Variability of $Y$ comes from two independent sources: ($i$) differences between the slices defined by $X$ (captured by how the conditional means spread out), and ($ii$) residual variability inside each slice (captured by conditional variances). Neither source is double-counted, so they sum exactly to $\mathrm{Var}(Y)$.

Q: If $X$ and $Y$ are independent, what do the two terms of the law of total variance reduce to?
A: $E[Y \mid X] = E[Y]$ is constant, so $\mathrm{Var}(E[Y \mid X]) = 0$. And $\mathrm{Var}(Y \mid X) = \mathrm{Var}(Y)$ is constant, so $E[\mathrm{Var}(Y \mid X)] = \mathrm{Var}(Y)$. The sum is still $\mathrm{Var}(Y)$ ✓.

P: Let $X$ be Class 1 ($P=0.7$, $Y \mid X=1$ has mean $500$, var $100^2$) or Class 2 ($P=0.3$, $Y \mid X=2$ has mean $1500$, var $300^2$). Find $\mathrm{Var}(Y)$.

S:
**IDENTIFY**: Two-level mixture; apply $\mathrm{Var}(Y) = E[\mathrm{Var}(Y \mid X)] + \mathrm{Var}(E[Y \mid X])$.

**PLAN**:
- Compute $E[\mathrm{Var}(Y \mid X)] = 0.7 \cdot 100^2 + 0.3 \cdot 300^2$.
- Compute $E[E[Y \mid X]] = 0.7 \cdot 500 + 0.3 \cdot 1500 = 800$ (from prior problem).
- Compute $\mathrm{Var}(E[Y \mid X]) = 0.7 (500 - 800)^2 + 0.3 (1500 - 800)^2$.
- Sum the two.

**EXECUTE**:
1. $E[\mathrm{Var}(Y \mid X)] = 0.7 \cdot 10000 + 0.3 \cdot 90000 = 7000 + 27000 = 34000$.
2. $\mathrm{Var}(E[Y \mid X]) = 0.7 \cdot 90000 + 0.3 \cdot 490000 = 63000 + 147000 = 210000$.
3. $\mathrm{Var}(Y) = 34000 + 210000 = 244000$.

**EVALUATE**: Standard deviation $\approx \sqrt{244000} \approx 494$. This exceeds each class's own standard deviation ($100$ and $300$), as expected: overall spread includes both within-class noise and the large gap between class means.

## 13.7 Best Predictor Interpretation (MMSE)

Q: Among all functions $g(X)$, which one minimizes the mean squared error $E[(Y - g(X))^2]$?
A: The conditional expectation $g^*(X) = E[Y \mid X]$. No other function of $X$ achieves a smaller expected squared prediction error.

C: The [minimum mean squared error] (MMSE) predictor of $Y$ from $X$ is $g^*(X) = E[Y \mid X]$.

Q: Why is $E[Y \mid X]$ the MMSE predictor intuitively?
A: For each fixed value $x$, the number that minimizes $E[(Y - c)^2 \mid X = x]$ is $c = E[Y \mid X = x]$ (the mean minimizes squared deviation). Doing this optimization separately inside every slice and gluing the results together gives the function $E[Y \mid X]$.

Q: What is the MMSE achieved by the predictor $E[Y \mid X]$, expressed in terms of conditional variance?
A: $E[(Y - E[Y \mid X])^2] = E[\mathrm{Var}(Y \mid X)]$ — the expected within-slice variance. By the law of total variance this is also $\mathrm{Var}(Y) - \mathrm{Var}(E[Y \mid X])$.

Q: Why does the best linear predictor generally differ from $E[Y \mid X]$?
A: $E[Y \mid X]$ may be a nonlinear function of $X$. The best linear predictor is restricted to the form $aX + b$, which can only match $E[Y \mid X]$ exactly when the conditional mean happens to be linear (as in jointly Gaussian $(X,Y)$).

## 13.8 Markov Chains — Definition, State Space, Transition Matrix

C: A [Markov chain] is a sequence of random variables $X_0, X_1, X_2, \ldots$ taking values in a set $S$ such that the distribution of $X_{n+1}$ given the entire past depends only on $X_n$.

C: The set $S$ of all possible values of the chain is called the [state space]; each element of $S$ is a state.

C: For a Markov chain on a finite or countable state space $S$, the [transition probability] $p_{ij} = P(X_{n+1} = j \mid X_n = i)$ gives the chance of jumping from state $i$ to state $j$ in one step.

C: A Markov chain is called [time-homogeneous] if the transition probabilities $p_{ij}$ do not depend on the time index $n$.

C: For a time-homogeneous chain on finite state space $S = \{1, \ldots, N\}$, the [transition matrix] $P$ is the $N \times N$ matrix with entries $P_{ij} = p_{ij}$.

Q: Why must each row of a transition matrix $P$ sum to $1$?
A: Row $i$ lists $P(X_{n+1} = j \mid X_n = i)$ for all $j \in S$. Since from state $i$ the chain must move to some state, these conditional probabilities are a probability distribution over $S$, which sums to $1$.

C: A square matrix with nonnegative entries whose rows each sum to $1$ is called a [stochastic matrix] (or row-stochastic matrix).

Q: Given states $\{A, B\}$ with $P(A \to A) = 0.8$, $P(A \to B) = 0.2$, $P(B \to A) = 0.5$, $P(B \to B) = 0.5$, what is the transition matrix?
A: $P = \begin{pmatrix} 0.8 & 0.2 \\ 0.5 & 0.5 \end{pmatrix}$, with rows indexed by the current state ($A$ then $B$) and columns indexed by the next state. Each row sums to $1$ ✓.

## 13.9 Markov Property (Memoryless)

C: The [Markov property] states $P(X_{n+1} = j \mid X_n = i, X_{n-1} = i_{n-1}, \ldots, X_0 = i_0) = P(X_{n+1} = j \mid X_n = i)$ — the future depends on the past only through the present.

Q: Why is the Markov property called "memoryless"?
A: Once the current state $X_n$ is known, no additional information about earlier states $X_{n-1}, \ldots, X_0$ changes the prediction of $X_{n+1}$. The chain effectively "forgets" its history beyond the current state.

Q: Why doesn't "memoryless" mean the past is irrelevant in every sense?
A: The past is already summarized in the current state. Knowing $X_n$ captures everything that matters for the future; separately, the past still correlates with the present (and hence with the future) through $X_n$ itself.

Q: Give a non-Markov example where knowing only the current state is insufficient.
A: A car's next position depends on its current position AND its current velocity. If the state is just position, the process is not Markov (two trajectories at the same position with different velocities evolve differently). Adding velocity to the state restores the Markov property.

Q: Why does the Markov property make transition matrices so powerful?
A: The full law of the process is captured by the initial distribution and one-step transitions. Future-distribution computations reduce to matrix algebra, rather than requiring joint distributions of arbitrary-length histories.

## 13.10 Multi-Step Transitions $P^{(n)}$

C: The [$n$-step transition probability] $p_{ij}^{(n)} = P(X_{n} = j \mid X_0 = i)$ gives the chance of going from state $i$ to state $j$ in exactly $n$ steps.

C: For a time-homogeneous chain with one-step transition matrix $P$, the $n$-step transition matrix is $P^{(n)} = [P^n]$, the ordinary $n$-th matrix power of $P$.

Q: Why does $P^{(n)} = P^n$ (matrix power) give the $n$-step transitions?
A: Applying the Markov property at each step, $p_{ij}^{(2)} = \sum_k p_{ik} p_{kj}$, which is exactly the $(i,j)$ entry of $P \cdot P = P^2$. Iterating this argument gives $p_{ij}^{(n)} = (P^n)_{ij}$.

C: The [Chapman-Kolmogorov equation] states $p_{ij}^{(m+n)} = \sum_k p_{ik}^{(m)} p_{kj}^{(n)}$, equivalent to the matrix identity $P^{m+n} = P^m P^n$.

Q: Why does Chapman-Kolmogorov make intuitive sense?
A: To go from $i$ to $j$ in $m + n$ steps, the chain must pass through some intermediate state $k$ at time $m$. Summing over all possible $k$'s, weighted by the probability of reaching $k$ in $m$ steps and then $j$ in $n$ more, accounts for every path.

C: If $\vec{\pi}_n$ is the row-vector distribution of $X_n$ (so $(\vec{\pi}_n)_i = P(X_n = i)$), then $\vec{\pi}_{n+1} = \vec{\pi}_n P$, and more generally $[\vec{\pi}_n = \vec{\pi}_0 P^n]$, where $\vec{\pi}_0$ is the initial distribution.

P: For $P = \begin{pmatrix} 0.8 & 0.2 \\ 0.5 & 0.5 \end{pmatrix}$ with states $\{A, B\}$ and $X_0 = A$, find $P(X_2 = A)$.

S:
**IDENTIFY**: Two-step transition probability — compute entry $(A, A)$ of $P^2$.

**PLAN**:
- Compute $P^2 = P \cdot P$.
- Read off the $(A, A)$ entry.

**EXECUTE**:
1. $(P^2)_{AA} = P_{AA} P_{AA} + P_{AB} P_{BA} = 0.8 \cdot 0.8 + 0.2 \cdot 0.5 = 0.64 + 0.10 = 0.74$.

**EVALUATE**: $P(X_2 = A \mid X_0 = A) = 0.74$. Sanity check: $P(X_2 = B \mid X_0 = A) = 0.8 \cdot 0.2 + 0.2 \cdot 0.5 = 0.16 + 0.10 = 0.26$, and $0.74 + 0.26 = 1$ ✓.

## 13.11 Stationary Distribution (Brief)

C: A probability row-vector $\vec{\pi}$ on the state space is a [stationary distribution] of the chain with transition matrix $P$ if $\vec{\pi} P = \vec{\pi}$, meaning starting in distribution $\vec{\pi}$ leaves the distribution unchanged after one step.

Q: In the defining equation $\vec{\pi} P = \vec{\pi}$, what are $\vec{\pi}$ and $P$, and what additional constraint must $\vec{\pi}$ satisfy?
A: $\vec{\pi}$ is a row vector whose entries $\pi_i$ give a probability distribution over states ($\pi_i \ge 0$), $P$ is the transition matrix. In addition to $\vec{\pi} P = \vec{\pi}$, we require $\sum_i \pi_i = 1$ so that $\vec{\pi}$ is actually a probability distribution.

Q: Why is a stationary distribution an eigenvector of $P$?
A: The equation $\vec{\pi} P = \vec{\pi}$ says $\vec{\pi}$ is a left eigenvector of $P$ with eigenvalue $1$. Every stochastic matrix has $1$ as an eigenvalue (row sums equal $1$), so such a vector always exists on a finite state space.

Q: Under suitable conditions (irreducible + aperiodic finite chain), what is the long-run behavior of the distribution $\vec{\pi}_n$?
A: $\vec{\pi}_n \to \vec{\pi}$ as $n \to \infty$, where $\vec{\pi}$ is the unique stationary distribution. The chain "forgets" its initial distribution and settles into $\vec{\pi}$.

P: Find the stationary distribution of $P = \begin{pmatrix} 0.8 & 0.2 \\ 0.5 & 0.5 \end{pmatrix}$.

S:
**IDENTIFY**: Solve $\vec{\pi} P = \vec{\pi}$ with $\pi_A + \pi_B = 1$, $\pi_A, \pi_B \ge 0$.

**PLAN**:
- Write the two scalar equations from $(\pi_A, \pi_B) P = (\pi_A, \pi_B)$.
- Use the normalization $\pi_A + \pi_B = 1$ to close the system.

**EXECUTE**:
1. First component: $0.8 \pi_A + 0.5 \pi_B = \pi_A \Rightarrow 0.5 \pi_B = 0.2 \pi_A \Rightarrow \pi_B = 0.4 \pi_A$.
2. Normalize: $\pi_A + 0.4 \pi_A = 1 \Rightarrow 1.4 \pi_A = 1 \Rightarrow \pi_A = 5/7$.
3. Then $\pi_B = 2/7$.

**EVALUATE**: $\vec{\pi} = (5/7, 2/7)$. Check: $(5/7)(0.8) + (2/7)(0.5) = 4/7 + 1/7 = 5/7$ ✓; entries nonnegative and sum to $1$ ✓.

## 13.12 Random Walks as Markov Chains

C: A [simple random walk] on $\mathbb{Z}$ is the Markov chain $X_0, X_1, \ldots$ with $X_{n+1} = X_n + Z_{n+1}$, where $Z_1, Z_2, \ldots$ are i.i.d. with $P(Z = +1) = p$ and $P(Z = -1) = 1 - p$.

Q: Why does the simple random walk on $\mathbb{Z}$ satisfy the Markov property?
A: $X_{n+1} = X_n + Z_{n+1}$ with $Z_{n+1}$ independent of $X_0, \ldots, X_{n-1}$ given $X_n$. So given the current position $X_n$, the next position depends only on an independent fresh increment, never on the earlier history.

C: The simple random walk is called [symmetric] when $p = 1/2$, so $P(Z = +1) = P(Z = -1) = 1/2$.

Q: What are the one-step transition probabilities $p_{ij}$ for the simple random walk on $\mathbb{Z}$?
A: $p_{i, i+1} = p$, $p_{i, i-1} = 1 - p$, and $p_{ij} = 0$ for $|i - j| \ne 1$. Only the two neighbors of $i$ are reachable in one step.

Q: For the symmetric random walk starting at $X_0 = 0$, what is $E[X_n]$?
A: $E[X_n] = 0$ for all $n$. Each step has mean $E[Z] = (+1)(1/2) + (-1)(1/2) = 0$, and $E[X_n] = E[X_0] + n E[Z] = 0$.

Q: For the simple random walk with step distribution $P(Z = +1) = p$, $P(Z = -1) = 1 - p$, what is $\mathrm{Var}(X_n)$ given $X_0 = 0$?
A: $\mathrm{Var}(X_n) = n \, \mathrm{Var}(Z) = n [1 - (2p - 1)^2] = 4 n p (1 - p)$, using independence of the increments to add variances. For $p = 1/2$ this simplifies to $\mathrm{Var}(X_n) = n$.

Q: Why is a random walk often described as "diffusive"?
A: Its standard deviation grows like $\sqrt{n}$ (since $\mathrm{Var}(X_n) \propto n$), matching how a diffusing particle spreads. Typical displacement after $n$ steps is on the order of $\sqrt{n}$, not $n$.
