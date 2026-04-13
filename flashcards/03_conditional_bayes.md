+++
order = 3
tags = ["math", "probability", "conditional", "bayes", "independence", "total-probability"]
+++

# Probability — Conditional Probability and Bayes

## 3.1 Why Condition?

Q: Why do we need conditional probability at all?
A: In real problems we rarely stay in the dark — new information arrives and should change our beliefs. Conditioning is the mathematical rule for updating a probability in light of that new information. Without it, the axioms of probability can describe a sample space but cannot describe learning, inference, or evidence. Every statistical and predictive method ultimately rests on conditioning.

Q: What question does the conditional probability $P(A|B)$ answer?
A: Given that event $B$ has occurred, how likely is event $A$? It restricts attention to the part of the sample space where $B$ is true and asks what fraction of that restricted world also lies in $A$.

Q: Why is "information changes probability" the central theme of this chapter?
A: Probability is a numerical measure of belief or long-run frequency, and both change when the set of possible outcomes shrinks. Learning that $B$ occurred rules out every outcome outside $B$, so the remaining probabilities must be renormalized. Conditioning, independence, and Bayes' theorem are all tools for tracking that renormalization.

C: The probability $P(A|B)$ is read "the probability of $A$ [given] $B$" and represents updated belief in $A$ after learning $B$ has occurred.

Q: Anticipation: before seeing the definition, predict how $P(A|B)$ should depend on $P(A \cap B)$ and $P(B)$.
A: Since we are restricting the sample space to $B$, the numerator should measure "how much of $A$ is inside $B$" — namely $P(A \cap B)$ — and the denominator should be the total mass of the new sample space, $P(B)$. The ratio renormalizes the overlap against the reduced world.

## 3.2 Definition of Conditional Probability

C: For events $A, B$ with $P(B) > 0$, the [conditional probability] of $A$ given $B$ is defined as $P(A|B) = \dfrac{P(A \cap B)}{P(B)}$, where $P(A \cap B)$ is the probability that both events occur and $P(B)$ is the probability of the conditioning event.

Q: Why does the definition of $P(A|B)$ require $P(B) > 0$?
A: The formula divides by $P(B)$, so $P(B) = 0$ would make the ratio undefined. Intuitively, conditioning on an event that cannot happen has no meaning — there is no "given $B$" scenario to speak of.

Q: Why is $P(A \cap B)$ in the numerator of $P(A|B)$ rather than $P(A)$?
A: Once we know $B$ has occurred, only outcomes in $B$ are still possible. The favorable outcomes for $A$ in this reduced world are exactly those in both $A$ and $B$ — i.e., $A \cap B$. The full $P(A)$ would incorrectly count outcomes of $A$ outside $B$, which are no longer possible.

Q: Why does dividing by $P(B)$ in the definition make sense?
A: Restricting to $B$ changes the total probability of the new sample space from $1$ to $P(B)$. Dividing by $P(B)$ rescales probabilities so that $P(B|B) = 1$, preserving the axiom that the whole (conditional) sample space has probability $1$.

C: By the definition, $P(B|B) = [1]$ whenever $P(B) > 0$.

Q: If $A$ and $B$ are mutually exclusive with $P(B) > 0$, what is $P(A|B)$?
A: Zero. Since $A \cap B = \emptyset$, we have $P(A \cap B) = 0$, so $P(A|B) = 0 / P(B) = 0$. Learning that $B$ occurred rules out $A$ entirely.

Q: Does $P(A|B) = P(B|A)$ in general?
A: No. The two conditional probabilities share the numerator $P(A \cap B)$ but divide by different denominators ($P(B)$ vs. $P(A)$). Confusing them is the "prosecutor's fallacy" and a common source of error in probabilistic reasoning.

## 3.3 Multiplication Rule

C: The [multiplication rule] rearranges the definition of conditional probability: $P(A \cap B) = P(A|B)\,P(B)$, where $P(A|B)$ is the probability of $A$ given $B$ and $P(B)$ is the marginal probability of $B$.

Q: Why is the multiplication rule useful even though it is just a rearrangement?
A: In many problems we are told conditional information directly — e.g., "given the test is positive, the disease probability is..." — but we want the joint probability. The multiplication rule lets us combine a marginal and a conditional probability to compute the joint, which is often the quantity needed for further calculation.

C: By symmetry, the multiplication rule can also be written $P(A \cap B) = [P(B|A)\,P(A)]$, where $P(B|A)$ is the probability of $B$ given $A$ and $P(A)$ is the marginal probability of $A$.

Q: Why are both forms $P(A|B)P(B)$ and $P(B|A)P(A)$ valid expressions for $P(A \cap B)$?
A: Intersection is symmetric — $A \cap B = B \cap A$ — so the joint probability can be decomposed by conditioning on either event. Setting the two forms equal immediately gives Bayes' theorem.

## 3.4 Chain Rule for Multiple Events

Q: Why extend the multiplication rule to more than two events?
A: Sequential experiments (drawing cards without replacement, Markov chains, Bayesian networks) require joint probabilities of many events that depend on one another. A general "chain rule" lets us factor these joints into a product of conditional probabilities we can reason about one step at a time.

C: The [chain rule] for three events states $P(A \cap B \cap C) = P(A)\,P(B|A)\,P(C|A \cap B)$, where each factor conditions on the events named before it.

C: For $n$ events $A_1, \ldots, A_n$, the chain rule states $P(A_1 \cap \cdots \cap A_n) = [P(A_1) \cdot P(A_2|A_1) \cdot P(A_3|A_1 \cap A_2) \cdots P(A_n|A_1 \cap \cdots \cap A_{n-1})]$, where each factor is the conditional probability of the next event given all previous ones.

Q: Why does the chain rule resemble a "sequence of updates"?
A: Each factor tells you how to update the probability of the next event given everything learned so far. Reading the chain rule left to right mirrors how an experiment unfolds in time: first $A_1$ happens, then $A_2$ happens given $A_1$, and so on.

P: A standard deck has 52 cards. Using the chain rule, find the probability of drawing three aces in a row (without replacement).

S:
**IDENTIFY**: Joint probability of three dependent events — each draw changes the composition of the deck. Events: $A_i$ = "$i$-th card is an ace."

**PLAN**:
- Apply the chain rule: $P(A_1 \cap A_2 \cap A_3) = P(A_1)\,P(A_2|A_1)\,P(A_3|A_1 \cap A_2)$.
- Count aces and remaining cards after each draw.

**EXECUTE**:
1. $P(A_1) = 4/52$ (4 aces out of 52 cards).
2. $P(A_2|A_1) = 3/51$ (3 aces remain out of 51 cards).
3. $P(A_3|A_1 \cap A_2) = 2/50$ (2 aces remain out of 50 cards).
4. Multiply: $\dfrac{4}{52} \cdot \dfrac{3}{51} \cdot \dfrac{2}{50} = \dfrac{24}{132600} = \dfrac{1}{5525}$.

**EVALUATE**:
- About $0.000181$, or roughly 1 in 5525 — reassuringly small for such a rare event.
- Sanity check: probability must decrease with each draw (fewer aces left), which it does ($4/52 > 3/51 > 2/50$).

## 3.5 Independence of Two Events

Q: Why do we need a special name for the case when knowing $B$ doesn't change $P(A)$?
A: Independence captures the idea that two events carry no information about each other — learning one tells you nothing new about the other. This condition simplifies joint probabilities enormously (they factor) and is the foundation of most probabilistic modeling, from coin flips to random sampling.

C: Two events $A$ and $B$ are called [independent] if $P(A \cap B) = P(A)\,P(B)$, where $P(A)$ and $P(B)$ are the individual probabilities of each event.

Q: Why is $P(A \cap B) = P(A)P(B)$ the preferred definition of independence (over $P(A|B) = P(A)$)?
A: The product form is symmetric in $A$ and $B$ and makes sense even when $P(B) = 0$, where $P(A|B)$ is undefined. So the product definition is more general and does not distinguish "which event came first."

Q: Show that if $P(B) > 0$, then $P(A \cap B) = P(A)P(B)$ is equivalent to $P(A|B) = P(A)$.
A: Divide both sides of $P(A \cap B) = P(A)P(B)$ by $P(B)$: the left side becomes $P(A|B)$ and the right side becomes $P(A)$. Conversely, multiplying $P(A|B) = P(A)$ by $P(B)$ recovers the product form. So the two definitions agree whenever conditioning on $B$ is defined.

Q: Why is independence sometimes described as "information-free"?
A: If $A$ and $B$ are independent, then $P(A|B) = P(A)$: learning that $B$ occurred does not change the probability of $A$. Symmetrically, $P(B|A) = P(B)$. Neither event provides information about the other.

C: If $A$ and $B$ are independent, then $A$ and the complement $B^c$ are [also independent], since $P(A \cap B^c) = P(A) - P(A \cap B) = P(A) - P(A)P(B) = P(A)P(B^c)$.

Q: Why is "mutually exclusive" NOT the same as "independent"?
A: Mutually exclusive events cannot both occur ($P(A \cap B) = 0$), so knowing one occurred rules the other out completely — maximum information transfer. Independent events, by contrast, carry zero information about each other. The only way to be both is if at least one has probability zero, a trivial case.

## 3.6 Pairwise vs. Mutual Independence

Q: Why isn't pairwise independence enough for three or more events?
A: Three events can be independent in pairs and yet "conspire" so that knowing any two determines the third. The product $P(A)P(B)P(C)$ need not equal $P(A \cap B \cap C)$ even if every pair factors. We need an additional condition on the triple intersection to rule out such conspiracies.

C: Events $A, B, C$ are [pairwise independent] if $P(A \cap B) = P(A)P(B)$, $P(A \cap C) = P(A)P(C)$, and $P(B \cap C) = P(B)P(C)$ — i.e., each pair of events is independent.

C: Events $A, B, C$ are [mutually independent] (or jointly independent) if they are pairwise independent AND $P(A \cap B \cap C) = P(A)P(B)P(C)$.

Q: Give a classic example showing pairwise independence does not imply mutual independence.
A: Flip two fair coins. Let $A$ = "first is heads," $B$ = "second is heads," $C$ = "the two outcomes match." Each pair is independent (probability $1/4$ for each intersection, and each marginal is $1/2$), but $A \cap B \cap C$ = "both heads and they match" = "both heads," which has probability $1/4$, not $(1/2)^3 = 1/8$.

C: For $n$ events $A_1, \ldots, A_n$ to be [mutually independent], the probability of every intersection of any subcollection must equal the product of the individual probabilities: $P\!\left(\bigcap_{i \in S} A_i\right) = \prod_{i \in S} P(A_i)$ for every subset $S \subseteq \{1, \ldots, n\}$.

Q: Why does mutual independence of $n$ events require $2^n - n - 1$ equations, not just one?
A: You must check factorization for every subset of size $\geq 2$. There are $\binom{n}{2} + \binom{n}{3} + \cdots + \binom{n}{n} = 2^n - n - 1$ such subsets. Pairwise independence only covers the $\binom{n}{2}$ pairs.

## 3.7 Conditional Independence

Q: Why introduce "conditional independence" when we already have independence?
A: Two events may be dependent marginally yet become independent once a third event is known — or vice versa. Conditional independence captures this nuance and is the backbone of graphical models (Bayes nets, Markov chains), where complex dependencies are decomposed into simpler conditional ones.

C: Events $A$ and $B$ are [conditionally independent given $C$] (with $P(C) > 0$) if $P(A \cap B|C) = P(A|C)\,P(B|C)$, where each factor is the conditional probability of that event given $C$.

Q: Why doesn't conditional independence imply unconditional independence?
A: Conditioning on $C$ changes the sample space, and the factorization need only hold in that restricted world. Marginalizing out $C$ can reintroduce dependence — e.g., $A$ = "umbrella used," $B$ = "streets are wet" might be dependent unconditionally (both driven by rain) yet conditionally independent given "it rained."

Q: Give an example where $A$ and $B$ are dependent overall but independent given $C$.
A: Let $C$ = "it rained today," $A$ = "umbrellas were used," $B$ = "sidewalks are wet." Marginally, $A$ and $B$ are positively correlated (rain causes both). But given that it rained, umbrella use and wet sidewalks are essentially independent — both are nearly certain regardless of the other.

## 3.8 Law of Total Probability

C: A collection $\{B_1, B_2, \ldots, B_n\}$ is a [partition] of the sample space $S$ if the $B_i$ are pairwise disjoint ($B_i \cap B_j = \emptyset$ for $i \neq j$) and their union equals $S$.

Q: Why do partitions matter for probability calculations?
A: A partition splits the sample space into non-overlapping pieces that together cover every possibility. This lets us compute the probability of any event by summing its contributions from each piece — a "divide and conquer" strategy that turns hard global problems into easier conditional subproblems.

C: The [law of total probability] states: if $\{B_1, \ldots, B_n\}$ is a partition of the sample space with $P(B_i) > 0$ for all $i$, then $P(A) = \sum_{i=1}^{n} P(A|B_i)\,P(B_i)$, where $P(A|B_i)$ is the conditional probability of $A$ given $B_i$ and $P(B_i)$ is the probability of the $i$-th partition piece.

Q: Why does the law of total probability work — what is the underlying identity?
A: Since the $B_i$ partition $S$, we can write $A = \bigcup_i (A \cap B_i)$ as a disjoint union. By the additivity axiom, $P(A) = \sum_i P(A \cap B_i)$. Applying the multiplication rule $P(A \cap B_i) = P(A|B_i)P(B_i)$ to each term yields the formula.

C: The simplest form of the law of total probability (with $B$ and $B^c$) reads $P(A) = [P(A|B)P(B) + P(A|B^c)P(B^c)]$, where $B^c$ is the complement of $B$.

Q: When is the law of total probability most useful?
A: When the direct marginal $P(A)$ is hard to compute but the conditionals $P(A|B_i)$ are natural — e.g., $A$ = "defective product," and the $B_i$ are the factories that produced it, each with a known defect rate and production share.

## 3.9 Bayes' Theorem

Q: Anticipation: before seeing Bayes' theorem, predict how we should combine $P(A|B)$ and $P(B)$ to get $P(B|A)$.
A: Since $P(A \cap B) = P(A|B)P(B) = P(B|A)P(A)$, solving for $P(B|A)$ gives $P(B|A) = P(A|B)P(B) / P(A)$. The conditional flips by "reweighting" the known direction with the ratio of marginals.

Q: Derive Bayes' theorem from the multiplication rule.
A: The multiplication rule gives two expressions for $P(A \cap B)$: $P(A|B)P(B)$ and $P(B|A)P(A)$. Setting them equal and dividing by $P(A)$ (assumed positive) yields $P(B|A) = \dfrac{P(A|B)\,P(B)}{P(A)}$, which is Bayes' theorem.

C: [Bayes' theorem] states $P(B|A) = \dfrac{P(A|B)\,P(B)}{P(A)}$, where $P(B|A)$ is the posterior probability of $B$ given $A$, $P(A|B)$ is the likelihood of $A$ under $B$, $P(B)$ is the prior probability of $B$, and $P(A)$ is the marginal probability of $A$.

C: Combining Bayes' theorem with the law of total probability gives the [expanded form]: $P(B|A) = \dfrac{P(A|B)\,P(B)}{P(A|B)\,P(B) + P(A|B^c)\,P(B^c)}$, where $B^c$ is the complement of $B$.

Q: Why is Bayes' theorem often called "inverse probability"?
A: It inverts the direction of conditioning. We typically know $P(A|B)$ (the probability of observing evidence $A$ under hypothesis $B$), but we want $P(B|A)$ (the probability of the hypothesis given the evidence). Bayes' theorem performs that inversion.

Q: For a partition $\{B_1, \ldots, B_n\}$, what is the general form of Bayes' theorem?
A: $P(B_k|A) = \dfrac{P(A|B_k)\,P(B_k)}{\sum_{i=1}^n P(A|B_i)\,P(B_i)}$, where the denominator is $P(A)$ expanded via the law of total probability. Each numerator is the joint $P(A \cap B_k)$, and the denominator normalizes across all partition pieces.

## 3.10 Prior vs. Posterior

C: In Bayes' theorem, $P(B)$ is called the [prior] probability — belief about $B$ before observing evidence $A$.

C: In Bayes' theorem, $P(B|A)$ is called the [posterior] probability — updated belief about $B$ after observing evidence $A$.

C: In Bayes' theorem, $P(A|B)$ is called the [likelihood] — the probability of observing evidence $A$ if $B$ were true.

Q: Why is the distinction between prior and posterior central to Bayesian reasoning?
A: It makes explicit that probability assignments depend on the available information. The prior encodes what you knew before the evidence; the posterior encodes what you know after. Bayes' theorem is the rule for moving from the former to the latter in a mathematically consistent way.

Q: Why does the denominator $P(A)$ in Bayes' theorem sometimes get called a "normalizing constant"?
A: $P(A)$ does not depend on which hypothesis $B_k$ we are considering — it is the same for every $k$. Its role is simply to make the posteriors $P(B_k|A)$ sum to $1$. The qualitative comparison between hypotheses is driven entirely by the numerators $P(A|B_k)P(B_k)$.

Q: What does it mean to say posterior $\propto$ likelihood $\times$ prior?
A: Since $P(A)$ is a constant across hypotheses, the posterior is proportional to the product of likelihood and prior. Evidence reshapes belief by multiplying the prior by how well each hypothesis "predicts" the observed data, then renormalizing.

Q: How does the posterior change if the likelihood $P(A|B)$ is much larger than $P(A|B^c)$?
A: The posterior $P(B|A)$ increases toward $1$ — the evidence strongly favors $B$ over its alternative. The ratio $P(A|B)/P(A|B^c)$ is called the Bayes factor and measures the strength of the evidence.

## 3.11 Classic Examples

Q: In the "false positive" problem, why does a positive test result often leave disease probability low?
A: When a disease is rare (low prior), even a highly accurate test produces more false positives than true positives in the general population. Bayes' theorem combines the small prior with the likelihood to give a posterior that can be surprisingly modest, no matter how "accurate" the test sounds.

P: A disease affects 1% of the population. A test has 99% sensitivity ($P(+|D) = 0.99$) and 95% specificity ($P(-|D^c) = 0.95$, so $P(+|D^c) = 0.05$). Given a positive test, what is the probability the person has the disease?

S:
**IDENTIFY**: Bayesian inversion problem. Known: prior $P(D) = 0.01$, likelihood $P(+|D) = 0.99$, false positive rate $P(+|D^c) = 0.05$. Want: posterior $P(D|+)$.

**PLAN**:
- Use Bayes' theorem with the law of total probability.
- $P(D|+) = \dfrac{P(+|D)\,P(D)}{P(+|D)\,P(D) + P(+|D^c)\,P(D^c)}$.

**EXECUTE**:
1. Numerator: $P(+|D)\,P(D) = 0.99 \times 0.01 = 0.0099$.
2. Second term in denominator: $P(+|D^c)\,P(D^c) = 0.05 \times 0.99 = 0.0495$.
3. Full denominator: $P(+) = 0.0099 + 0.0495 = 0.0594$.
4. Posterior: $P(D|+) = 0.0099 / 0.0594 \approx 0.167$.

**EVALUATE**:
- Even after a positive test, disease probability is only about 16.7%, not 99%.
- The reason: false positives from the healthy 99% of the population ($\approx 4.95\%$) outnumber true positives from the diseased 1% ($\approx 0.99\%$) by about 5 to 1.
- Takeaway: base rates (priors) dominate when the prior is small.

Q: Why is the false-positive result counterintuitive to most people?
A: People tend to focus on the test's accuracy (99%) and ignore the prior (1%). This cognitive error is called "base rate neglect." Bayes' theorem shows that the rarity of the disease massively dilutes the informativeness of a positive test.

Q: In the Monty Hall problem, what is the setup?
A: Three doors hide one car and two goats. The contestant picks a door. The host, who knows where the car is, then opens one of the other two doors to reveal a goat. The contestant is offered the choice to stick with their original door or switch to the remaining unopened door.

Q: In Monty Hall, what is the probability of winning if you stick with your original choice?
A: $1/3$. The original choice was made when all three doors were equally likely, so its probability of hiding the car is fixed at $1/3$ regardless of what the host reveals afterward.

Q: In Monty Hall, what is the probability of winning if you switch?
A: $2/3$. The two non-chosen doors together had probability $2/3$ of containing the car. When the host reveals a goat behind one of them, that $2/3$ "collapses" onto the single remaining unopened door.

Q: Why does the host's choice not affect the probability of the originally chosen door?
A: The host is forced to open a door with a goat from among the non-chosen doors, and this action reveals no new information about the contestant's original pick — that probability was set at $1/3$ at the moment of the pick. The host's action only redistributes the remaining $2/3$ probability.

Q: Why does Monty Hall illustrate the importance of conditioning carefully?
A: Naive intuition says "two doors left, so 50/50," treating the revealed door as if it eliminated information symmetrically. In reality, the host's action is conditioned on the contestant's pick and on the car's location, so it updates probabilities asymmetrically. Applying Bayes' theorem formally gives $P(\text{car behind other door}|\text{host opens goat}) = 2/3$.

Q: What single lesson unites the false-positive and Monty Hall examples?
A: Human intuition about conditional probability is often wrong — we ignore base rates or mishandle how evidence updates beliefs. Bayes' theorem is the corrective: it gives the unique mathematically consistent update from prior to posterior given the likelihood.
