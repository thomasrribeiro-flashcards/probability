+++
order = 8
tags = ["math", "probability", "joint", "marginal", "conditional", "independence", "iid"]
+++

# Probability — Joint Distributions

## 8.1 Why Joint Distributions?

Q: Why do we need joint distributions at all — isn't one random variable at a time enough?
A: Most real problems involve several quantities that vary together: height and weight, temperature and pressure, returns on two stocks. A single-variable distribution tells us about each one in isolation but hides how they co-vary. A joint distribution captures the full probabilistic behavior of several random variables simultaneously, which is the only way to answer questions like "given $X$ is large, what do we expect of $Y$?".

Q: Why can't we reconstruct a joint distribution from the two separate distributions of $X$ and $Y$?
A: Knowing the distribution of $X$ alone and the distribution of $Y$ alone fixes only how each behaves on its own. Many different joint distributions share the same individual (marginal) distributions but disagree about how $X$ and $Y$ are linked. The joint distribution carries extra information about dependence that the marginals cannot express.

C: A [joint distribution] of random variables $X$ and $Y$ specifies the probability of every event involving both $X$ and $Y$ simultaneously.

C: The individual distribution of a single random variable extracted from a joint distribution is called its [marginal] distribution.

## 8.2 Joint PMF (Discrete)

Q: Why is a joint PMF the natural tool for two discrete random variables?
A: For discrete variables, probability is concentrated at a countable set of points. A joint PMF assigns a nonnegative weight to each pair $(x, y)$, and any event involving $X$ and $Y$ is a union of such pairs. Summing the PMF over the pairs in an event gives its probability directly, so the PMF contains all the probabilistic information about $(X, Y)$.

C: The [joint probability mass function] of discrete random variables $X$ and $Y$ is the function $p_{X,Y}(x, y) = P(X = x,\ Y = y)$, giving the probability that $X$ takes value $x$ and $Y$ takes value $y$ simultaneously.

C: A valid joint PMF $p_{X,Y}(x, y)$ must satisfy $p_{X,Y}(x, y) \geq 0$ for all $(x, y)$ and $\sum_{x} \sum_{y} p_{X,Y}(x, y) = [1]$, where the double sum ranges over all possible value pairs.

Q: Given a joint PMF $p_{X,Y}$, how do you compute $P((X, Y) \in A)$ for a set $A$ of pairs?
A: Sum the PMF over every pair in $A$: $P((X,Y) \in A) = \sum_{(x,y) \in A} p_{X,Y}(x,y)$. This works because the events $\{X = x, Y = y\}$ for distinct pairs are disjoint and cover $A$.

C: If $X$ and $Y$ are discrete with joint PMF $p_{X,Y}$, then $P(X = 2,\ Y = 3) = [p_{X,Y}(2, 3)]$.

## 8.3 Joint PDF (Continuous)

Q: Why do continuous random variables use a joint PDF instead of a joint PMF?
A: For continuous variables, the probability of hitting any exact pair $(x, y)$ is zero, so a PMF would be useless. Instead we describe probability as a density spread over the plane, and probability of a region is the volume under the density over that region. The joint PDF is the two-dimensional analog of the single-variable PDF.

C: The [joint probability density function] of continuous random variables $X$ and $Y$ is a nonnegative function $f_{X,Y}(x, y)$ such that $P((X, Y) \in A) = \iint_{A} f_{X,Y}(x, y)\, dx\, dy$ for every region $A$ in the plane.

C: A valid joint PDF $f_{X,Y}(x, y)$ satisfies $f_{X,Y}(x, y) \geq 0$ for all $(x, y)$ and $\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f_{X,Y}(x, y)\, dx\, dy = [1]$.

Q: Why is it fine for a joint PDF to take values greater than 1?
A: A PDF is a density, not a probability. Probabilities come from integrating the density over a region, and that integral over all of $\mathbb{R}^2$ equals 1. The density can be arbitrarily large over a small region as long as its integral stays bounded.

Q: For a continuous joint distribution, what is $P(X = a,\ Y = b)$ for specific numbers $a, b$?
A: Zero. The event $\{X = a, Y = b\}$ is a single point in the plane, which has zero area, so integrating the density over it gives 0. Continuous joint distributions only assign positive probability to regions with positive area.

## 8.4 Joint CDF

Q: Why define a joint CDF when we already have joint PMFs and PDFs?
A: The joint CDF exists for every pair of random variables — discrete, continuous, or mixed — while PMFs and PDFs only exist in their respective settings. It also makes certain computations (like $P(X \leq x, Y \leq y)$) immediate, and it is the standard object for proving general theorems about joint behavior.

C: The [joint cumulative distribution function] of random variables $X$ and $Y$ is $F_{X,Y}(x, y) = P(X \leq x,\ Y \leq y)$, defined for all real $x, y$.

C: As $x \to \infty$ and $y \to \infty$, the joint CDF satisfies $F_{X,Y}(x, y) \to [1]$, since the event $\{X \leq x, Y \leq y\}$ eventually becomes certain.

C: As $x \to -\infty$ (with $y$ fixed), the joint CDF satisfies $F_{X,Y}(x, y) \to [0]$, since the event $\{X \leq x\}$ becomes impossible.

Q: How is the joint PDF recovered from the joint CDF when the CDF is smooth enough?
A: By mixed partial differentiation: $f_{X,Y}(x, y) = \dfrac{\partial^2 F_{X,Y}(x, y)}{\partial x\, \partial y}$, where $F_{X,Y}$ is the joint CDF. This mirrors the single-variable identity $f_X(x) = F_X'(x)$ and holds wherever the mixed partial exists.

Q: How do you compute $P(a < X \leq b,\ c < Y \leq d)$ from the joint CDF?
A: Use the inclusion-exclusion formula $F_{X,Y}(b, d) - F_{X,Y}(a, d) - F_{X,Y}(b, c) + F_{X,Y}(a, c)$, where $F_{X,Y}$ is the joint CDF. The four terms add and subtract the four corners of the rectangle so that only the probability of the rectangle remains.

## 8.5 Marginal Distributions

Q: Why do we "sum out" or "integrate out" a variable to get a marginal?
A: The marginal distribution of $X$ asks only about $X$, ignoring $Y$. The event $\{X = x\}$ (or $\{X \leq x\}$) is the union over all possible $y$ of $\{X = x, Y = y\}$. Summing or integrating the joint distribution over $y$ collects the total probability weight for each $x$ regardless of what $Y$ does.

C: For discrete $X, Y$ with joint PMF $p_{X,Y}$, the [marginal PMF] of $X$ is $p_X(x) = \sum_{y} p_{X,Y}(x, y)$, where the sum runs over every possible value of $Y$.

C: For continuous $X, Y$ with joint PDF $f_{X,Y}$, the [marginal PDF] of $X$ is $f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x, y)\, dy$, integrating out $y$ over all real values.

C: By symmetry, the marginal PDF of $Y$ from a joint PDF $f_{X,Y}$ is $f_Y(y) = \int_{-\infty}^{\infty} f_{X,Y}(x, y)\, [dx]$.

Q: Why can the same pair of marginals come from very different joints?
A: Marginals describe $X$ and $Y$ separately but say nothing about how they vary together. Infinitely many joint PDFs can yield the same two marginals — they differ in their dependence structure. This is why you cannot recover the joint from the marginals alone.

## 8.6 Conditional Distributions

Q: Why do we define conditional distributions in terms of the joint divided by the marginal?
A: Conditional probability is $P(B \mid A) = P(A \cap B) / P(A)$. For random variables, conditioning on $X = x$ uses the joint (which plays the role of $P(A \cap B)$) and normalizes by the marginal of $X$ (the role of $P(A)$). This keeps the total conditional probability equal to 1, giving a genuine distribution of $Y$ for each fixed $x$.

C: For discrete $X, Y$ with $p_X(x) > 0$, the [conditional PMF] of $Y$ given $X = x$ is $p_{Y \mid X}(y \mid x) = p_{X,Y}(x, y) / p_X(x)$.

C: For continuous $X, Y$ with $f_X(x) > 0$, the [conditional PDF] of $Y$ given $X = x$ is $f_{Y \mid X}(y \mid x) = f_{X,Y}(x, y) / f_X(x)$.

Q: Why is the conditional PDF $f_{Y \mid X}(y \mid x)$ well-defined at a specific $x$ even though $P(X = x) = 0$?
A: The definition is built from densities, not from conditioning on the zero-probability event $\{X = x\}$ directly. Dividing the joint density by the marginal density at $x$ produces a function of $y$ that integrates to 1 and behaves exactly like the limiting distribution of $Y$ given $X$ is near $x$.

Q: What is the "multiplication rule" for joint densities from conditional and marginal?
A: $f_{X,Y}(x, y) = f_{Y \mid X}(y \mid x)\, f_X(x)$, where $f_X$ is the marginal of $X$ and $f_{Y \mid X}$ is the conditional density of $Y$ given $X$. This rearrangement of the conditional definition lets you build joints from one marginal plus one conditional.

C: The integration-to-1 property for a conditional density is $\int_{-\infty}^{\infty} f_{Y \mid X}(y \mid x)\, dy = [1]$ for each fixed $x$ with $f_X(x) > 0$.

## 8.7 Independence of Random Variables

Q: Why does independence of $X$ and $Y$ translate into the joint factoring as a product of marginals?
A: Events involving $X$ and $Y$ are independent when $P(A \cap B) = P(A) P(B)$. Applying this to $\{X \leq x\}$ and $\{Y \leq y\}$ shows $F_{X,Y}(x, y) = F_X(x) F_Y(y)$. Differentiating (continuous case) or taking differences (discrete case) yields the corresponding factorization of the PMF or PDF.

C: Discrete $X$ and $Y$ are [independent] if and only if $p_{X,Y}(x, y) = p_X(x)\, p_Y(y)$ for every pair $(x, y)$.

C: Continuous $X$ and $Y$ are [independent] if and only if $f_{X,Y}(x, y) = f_X(x)\, f_Y(y)$ for (almost) every pair $(x, y)$.

C: $X$ and $Y$ are independent if and only if their joint CDF factors: $F_{X,Y}(x, y) = F_X(x)\, [F_Y(y)]$ for all $x, y$.

Q: If $X$ and $Y$ are independent, what does the conditional distribution of $Y$ given $X = x$ look like?
A: It equals the marginal distribution of $Y$: $f_{Y \mid X}(y \mid x) = f_Y(y)$. Intuitively, knowing $X$ provides no information about $Y$, so conditioning leaves $Y$'s distribution unchanged.

Q: Why is "$X$ and $Y$ have the same marginals" not enough for independence?
A: Independence is a statement about the joint, not the marginals. Two variables with identical marginals can still be tightly coupled (e.g., $Y = X$). Independence requires the joint to factor into the product of marginals at every point, which is a strictly stronger condition.

Q: What's a quick algebraic test for independence given a joint PDF $f_{X,Y}(x, y)$ on a rectangular region?
A: Check whether $f_{X,Y}(x, y)$ factors as $g(x)\, h(y)$ (a function of $x$ alone times a function of $y$ alone) AND whether the support is a product set (rectangle). If either condition fails, $X$ and $Y$ are not independent.

## 8.8 Computing Probabilities via Double Integrals

Q: Why are double integrals the workhorse for computing probabilities of joint events?
A: For continuous $X, Y$, probabilities are volumes under the joint density. Any event $\{(X, Y) \in A\}$ has probability equal to the integral of $f_{X,Y}$ over $A$, which is a double integral. Choosing integration order and limits that match the region $A$ makes the computation tractable.

C: For continuous $X, Y$ with joint PDF $f_{X,Y}$, $P(X \leq x,\ Y \leq y) = \int_{-\infty}^{y} \int_{-\infty}^{x} f_{X,Y}(s, t)\, ds\, [dt]$, where $s, t$ are integration variables.

Q: When computing $P(X + Y \leq 1)$ from a joint PDF on the unit square, how do you set up the double integral?
A: The event is the region below the line $x + y = 1$ inside the support. Integrate $f_{X,Y}(x, y)$ over that triangular region — e.g., $\int_{0}^{1} \int_{0}^{1-x} f_{X,Y}(x, y)\, dy\, dx$, where for each $x \in [0, 1]$, $y$ ranges from $0$ to $1 - x$.

P: Let $X$ and $Y$ be continuous random variables with joint PDF $f_{X,Y}(x, y) = 2$ on the triangle $0 \leq y \leq x \leq 1$ and $0$ elsewhere. Find $P(X + Y \leq 1)$.

S:
**IDENTIFY**: A probability of a joint event for a continuous pair, computed by integrating the joint PDF over the region where both the support condition ($0 \leq y \leq x \leq 1$) and the event ($x + y \leq 1$) hold.

**PLAN**:
- Sketch the support: the triangle with vertices $(0, 0)$, $(1, 0)$, $(1, 1)$.
- Intersect with $\{x + y \leq 1\}$: this clips by the line $y = 1 - x$.
- Set up a double integral of $f_{X,Y}$ over the intersection.

**EXECUTE**:
1. Support: $0 \leq y \leq x$ and $x \leq 1$. Event: $y \leq 1 - x$.
2. For each $x$, $y$ ranges from $0$ to $\min(x,\ 1 - x)$. This min equals $x$ when $x \leq 1/2$ and $1 - x$ when $x \geq 1/2$.
3. Split the integral:
$$P(X + Y \leq 1) = \int_{0}^{1/2} \int_{0}^{x} 2\, dy\, dx + \int_{1/2}^{1} \int_{0}^{1 - x} 2\, dy\, dx.$$
4. First piece: $\int_{0}^{1/2} 2x\, dx = x^2 \big|_0^{1/2} = 1/4$.
5. Second piece: $\int_{1/2}^{1} 2(1 - x)\, dx = -(1 - x)^2 \big|_{1/2}^{1} = 0 - (-1/4) = 1/4$.
6. Total: $1/4 + 1/4 = 1/2$.

**EVALUATE**:
- Answer: $P(X + Y \leq 1) = 1/2$.
- Sanity check: the full triangle has area $1/2$ and density $2$, so total probability is $1$ ✓. The line $x + y = 1$ cuts that triangle exactly in half through $(1/2, 1/2)$, so getting $1/2$ is geometrically plausible.

## 8.9 Joint Distributions of More Than Two Variables

Q: Why generalize joint distributions beyond two variables?
A: Real systems usually involve many interacting quantities — $n$ stock returns, $n$ sensor readings, an entire time series. To make probabilistic statements about them jointly, we need a single object that describes their combined behavior. Everything we did for two variables extends naturally to $n$.

C: The [joint PMF] of discrete $X_1, \ldots, X_n$ is $p_{X_1, \ldots, X_n}(x_1, \ldots, x_n) = P(X_1 = x_1, \ldots, X_n = x_n)$, summing to $1$ over all value tuples.

C: The [joint PDF] of continuous $X_1, \ldots, X_n$ is a nonnegative function $f_{X_1, \ldots, X_n}$ such that probabilities of regions in $\mathbb{R}^n$ are computed by $n$-fold integrals, with $\int_{\mathbb{R}^n} f_{X_1, \ldots, X_n} = [1]$.

C: To marginalize out one variable from an $n$-variable joint PDF, you [integrate] that variable out over $\mathbb{R}$, leaving a joint PDF of the remaining $n - 1$ variables.

Q: How does the multiplication rule look for three random variables?
A: Any joint can be chained as $f_{X,Y,Z}(x, y, z) = f_X(x)\, f_{Y \mid X}(y \mid x)\, f_{Z \mid X, Y}(z \mid x, y)$, where $f_{Y \mid X}$ and $f_{Z \mid X, Y}$ are the appropriate conditional densities. This lets you build complex joint distributions from simpler conditionals.

C: Random variables $X_1, \ldots, X_n$ are [mutually independent] if and only if their joint PMF/PDF factors as $p_{X_1}(x_1)\, p_{X_2}(x_2) \cdots p_{X_n}(x_n)$ (or the density analog) for every tuple.

Q: Why is pairwise independence weaker than mutual independence?
A: Pairwise independence means every pair $(X_i, X_j)$ factors, but the full $n$-way joint may still not factor into $n$ marginals. Classic counterexamples exist: three Bernoulli variables can be pairwise independent yet satisfy $X_3 = X_1 \oplus X_2$, making them tightly linked jointly.

## 8.10 Independent and Identically Distributed (iid)

Q: Why is the "iid" assumption so central to probability and statistics?
A: "Independent" makes the joint distribution factor, and "identically distributed" means each factor is the same marginal. Together they let us replace an $n$-dimensional joint by a single marginal distribution raised to the $n$-th power, making computations, laws of large numbers, and central limit theorems tractable. Most classical sampling theory assumes iid.

C: Random variables $X_1, \ldots, X_n$ are called [iid] (independent and identically distributed) if they are mutually independent AND share a common marginal distribution $F$.

C: For iid continuous $X_1, \ldots, X_n$ with common PDF $f$, the joint PDF is $f_{X_1, \ldots, X_n}(x_1, \ldots, x_n) = \prod_{i=1}^{n} [f(x_i)]$.

Q: If $X_1, \ldots, X_n$ are iid, what is $P(X_1 \leq x,\ X_2 \leq x, \ldots, X_n \leq x)$ in terms of the common CDF $F$?
A: $[F(x)]^n$, since independence lets the joint CDF factor into a product and identical distribution makes every factor equal to $F(x)$. This is the standard starting point for maximum-of-iid-sample arguments.

Q: Why does "identically distributed" not imply "independent"?
A: Two variables can share the same marginal yet be strongly dependent — for example, $Y = X$ with $X \sim \text{Uniform}(0, 1)$ gives identical marginals but perfect dependence. Identical distributions constrain marginals only; independence is a statement about the joint.

## 8.11 Multivariate Normal (Brief Introduction)

Q: Why is the multivariate normal the most important multivariate distribution?
A: It generalizes the one-dimensional normal in a way that preserves the structure we love: every marginal is normal, every conditional is normal, every linear combination is normal. Combined with the central limit theorem — which says sums of iid variables are approximately normal — it becomes the default model for correlated measurements, errors, and noise.

C: A random vector $\mathbf{X} = (X_1, \ldots, X_n)^\top$ has a [multivariate normal] distribution if every linear combination $a_1 X_1 + \cdots + a_n X_n$ is a (univariate) normal random variable.

C: The multivariate normal distribution is parameterized by a [mean vector] $\boldsymbol{\mu} \in \mathbb{R}^n$ and a covariance matrix $\Sigma \in \mathbb{R}^{n \times n}$, written $\mathbf{X} \sim \mathcal{N}(\boldsymbol{\mu}, \Sigma)$.

C: For a nondegenerate multivariate normal, the joint PDF is $f_{\mathbf{X}}(\mathbf{x}) = \dfrac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}} \exp\!\left(-\tfrac{1}{2} (\mathbf{x} - \boldsymbol{\mu})^\top [\Sigma^{-1}] (\mathbf{x} - \boldsymbol{\mu})\right)$, where $\boldsymbol{\mu}$ is the mean vector, $\Sigma$ is the covariance matrix, and $|\Sigma|$ is its determinant.

Q: For a bivariate normal $(X, Y)$, what special property do jointly normal variables have that other joint distributions don't?
A: Zero correlation implies independence. In general, uncorrelated random variables need not be independent, but for jointly normal variables the covariance matrix being diagonal is equivalent to the joint density factoring into marginals — so uncorrelated jointly normal variables are independent.

Q: Why does "each $X_i$ is normal" not imply "the vector $(X_1, \ldots, X_n)$ is multivariate normal"?
A: Multivariate normality requires every linear combination to be normal, which is strictly stronger than each coordinate being normal. Counterexamples exist where $X$ and $Y$ are each marginally normal but their joint is not — so the multivariate normal condition constrains the dependence structure, not just the marginals.

C: If $\mathbf{X} \sim \mathcal{N}(\boldsymbol{\mu}, \Sigma)$, then every marginal distribution of a subset of coordinates is also [multivariate normal], with mean and covariance obtained by picking the corresponding entries of $\boldsymbol{\mu}$ and $\Sigma$.

Q: Why is the covariance matrix $\Sigma$ always symmetric and positive semidefinite?
A: Symmetry follows because $\operatorname{Cov}(X_i, X_j) = \operatorname{Cov}(X_j, X_i)$. Positive semidefiniteness follows because for any vector $\mathbf{a}$, $\mathbf{a}^\top \Sigma \mathbf{a} = \operatorname{Var}(\mathbf{a}^\top \mathbf{X}) \geq 0$, since variances are nonnegative. These properties are what let $\Sigma^{-1}$ (when it exists) sit inside the quadratic form of the density.
