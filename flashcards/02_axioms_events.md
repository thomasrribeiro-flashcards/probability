+++
order = 2
tags = ["math", "probability", "axioms", "events", "sample-space", "inclusion-exclusion"]
+++

# Probability — Axioms and Events

## 2.1 Random Experiments

Q: Why do we begin probability theory with the notion of a random experiment?
A: Probability is a quantitative language for situations whose outcome is not known in advance but for which we can list the things that could happen. Fixing a precise description of "the experiment" — what is done and what could be observed — is the foundation on which sample spaces, events, and probabilities are all built. Without this anchor, the later axioms have nothing concrete to attach to.

C: A [random experiment] is a process whose outcome cannot be predicted with certainty in advance but whose set of possible outcomes is known.

C: A single performance of a random experiment is called a [trial], and its result is called an outcome.

Q: What two features must a process have to qualify as a random experiment?
A: First, the list of all possible outcomes must be specifiable before the experiment is performed. Second, which specific outcome occurs on a given trial cannot be predicted with certainty. Together these allow us to describe uncertainty without abandoning mathematical precision.

Q: Why must the set of possible outcomes be fixed before the experiment, rather than discovered afterwards?
A: Probabilities are defined on subsets of a pre-specified outcome set. If we let outcomes appear retroactively, the same physical process could support many incompatible probability assignments. Fixing the outcome set up front makes probability unambiguous.

## 2.2 Sample Space

C: The [sample space] of a random experiment, denoted $\Omega$, is the set of all possible outcomes of the experiment.

C: An element $\omega \in \Omega$ is called a [sample point] or elementary outcome, where $\Omega$ is the sample space.

Q: Why is the sample space the first object we define, before probabilities?
A: Probabilities are numbers assigned to subsets of the sample space. Until we have fixed what "all possible outcomes" means, there is nothing for probabilities to be attached to. The sample space is the universe inside which every later object — events, random variables, distributions — lives.

Q: For a single coin flip, what is the sample space $\Omega$?
A: $\Omega = \{H, T\}$, where $H$ denotes heads and $T$ denotes tails. Every other object we build for this experiment will be a subset of this two-element set.

Q: For rolling a standard six-sided die, what is the sample space $\Omega$?
A: $\Omega = \{1, 2, 3, 4, 5, 6\}$, where each number represents the face showing on top after the roll.

C: A sample space is called [discrete] if it is finite or countably infinite.

C: A sample space is called [continuous] if it is uncountable, such as $\Omega = [0, 1]$ for a uniform random number.

## 2.3 Events

C: An [event] is a subset $A \subseteq \Omega$ of the sample space, where $\Omega$ is the set of all possible outcomes.

C: An event $A$ is said to [occur] on a given trial if the realized outcome $\omega$ satisfies $\omega \in A$.

C: A [simple event] (or elementary event) is an event consisting of exactly one outcome, i.e., a singleton $\{\omega\} \subseteq \Omega$.

C: A [compound event] is an event that consists of more than one outcome, i.e., a subset of $\Omega$ with at least two elements.

Q: Why do we model events as subsets of $\Omega$ rather than as individual outcomes?
A: Real questions usually ask about collections of outcomes ("the die shows an even number", "the coin does not land heads") rather than a single result. Subsets let us group outcomes flexibly, and set operations then correspond exactly to logical operations on questions. This is what makes the whole theory clean.

Q: For a die roll, express the event "the result is even" as a subset of $\Omega = \{1,\ldots,6\}$.
A: $A = \{2, 4, 6\}$. The event occurs on a trial exactly when the realized face value belongs to this set.

C: The [certain event] is the whole sample space $\Omega$, which occurs on every trial.

C: The [impossible event] is the empty set $\emptyset$, which never occurs on any trial.

## 2.4 Set Operations on Events

Q: Why are set operations the natural tools for combining events?
A: Every English connective between events ("and", "or", "not", "but not") matches a set operation on their subsets ($\cap$, $\cup$, $^c$, $\setminus$). Translating words into sets lets us reason about events using the well-developed algebra of sets rather than re-deriving rules each time.

C: The [union] of events $A$ and $B$, written $A \cup B$, is the event that occurs when $A$ occurs, $B$ occurs, or both occur.

C: Formally, $A \cup B = \{\omega \in \Omega : \omega \in A \text{ or } \omega \in B\}$, where $\Omega$ is the sample space and $A, B$ are events. The union corresponds to the logical word [or].

C: The [intersection] of events $A$ and $B$, written $A \cap B$, is the event that occurs when both $A$ and $B$ occur on the same trial.

C: Formally, $A \cap B = \{\omega \in \Omega : \omega \in A \text{ and } \omega \in B\}$, where $\Omega$ is the sample space. The intersection corresponds to the logical word [and].

C: The [complement] of an event $A$, written $A^c$ (or $\bar{A}$), is defined as $A^c = \{\omega \in \Omega : \omega \notin A\}$, where $\Omega$ is the sample space.

C: The complement $A^c$ occurs exactly when the event $A$ [does not occur], i.e., the realized outcome is not in $A$.

C: The [difference] of events $A$ and $B$, written $A \setminus B$, is $A \setminus B = A \cap B^c = \{\omega \in \Omega : \omega \in A \text{ and } \omega \notin B\}$.

Q: Why is the difference $A \setminus B$ equal to $A \cap B^c$?
A: "$A$ but not $B$" means the outcome must lie in $A$ and simultaneously not lie in $B$. "Not in $B$" is $B^c$, and "and" is intersection, so the set of outcomes in $A$ but not $B$ is exactly $A \cap B^c$.

## 2.5 Mutually Exclusive Events

C: Two events $A$ and $B$ are called [mutually exclusive] (or disjoint) if $A \cap B = \emptyset$, meaning they cannot both occur on the same trial.

C: A collection of events $A_1, A_2, \ldots$ is called [pairwise disjoint] if $A_i \cap A_j = \emptyset$ for all $i \neq j$.

Q: Why does mutual exclusivity matter for probability?
A: When events cannot co-occur, the probability of their union is simply the sum of their individual probabilities — no double-counting is possible. This turns one of Kolmogorov's axioms (countable additivity) into a usable computational rule and is the reason we care about disjointness.

Q: Are the events $A = \{1,2\}$ and $B = \{2,3\}$ on a die roll mutually exclusive? Why or why not?
A: No. Their intersection is $A \cap B = \{2\}$, which is non-empty, so both events occur together when the die shows a 2. Mutual exclusivity requires an empty intersection.

Q: For a single die roll, give two events that ARE mutually exclusive and explain why.
A: $A = \{1, 2\}$ and $B = \{5, 6\}$. Their intersection $A \cap B = \emptyset$ because no face value belongs to both sets, so only one of the two events can occur on any given roll.

C: An event $A$ and its complement $A^c$ are always [mutually exclusive], since $A \cap A^c = \emptyset$ by definition of the complement.

## 2.6 De Morgan's Laws

Q: Why are De Morgan's laws useful in probability?
A: They let us rewrite "not (A or B)" and "not (A and B)" in a different form, which is essential when one form is easier to compute than the other. In particular, probabilities of complements are often easier to handle than probabilities of unions, so De Morgan's laws are the bridge between the two.

C: De Morgan's first law for two events: $(A \cup B)^c = [A^c \cap B^c]$, where $A^c$ denotes the complement of $A$ in the sample space $\Omega$.

C: De Morgan's second law for two events: $(A \cap B)^c = [A^c \cup B^c]$, where $A, B$ are events in $\Omega$.

Q: In words, what does $(A \cup B)^c = A^c \cap B^c$ say?
A: "Neither $A$ nor $B$ occurs" means the same as "$A$ does not occur and $B$ does not occur". The complement of a union is the intersection of complements.

Q: In words, what does $(A \cap B)^c = A^c \cup B^c$ say?
A: "It is not the case that both $A$ and $B$ occur" means the same as "$A$ does not occur or $B$ does not occur". The complement of an intersection is the union of complements.

C: The general form of De Morgan's law for any collection of events: $\left(\bigcup_i A_i\right)^c = [\bigcap_i A_i^c]$, where the $A_i$ are events in $\Omega$.

C: The dual general form: $\left(\bigcap_i A_i\right)^c = [\bigcup_i A_i^c]$, where the $A_i$ are events in $\Omega$.

## 2.7 Kolmogorov's Axioms

Q: Why do we need axioms for probability rather than just intuition?
A: Intuitive rules for probability contradict each other or become ambiguous in subtle cases (infinite sample spaces, conditional events, paradoxes). Kolmogorov's axioms give a minimal set of rules from which every valid property of probability can be derived rigorously, so disagreements reduce to checking the axioms. This is the same role that axioms play in geometry or arithmetic.

C: A [probability measure] $P$ assigns to each event $A \subseteq \Omega$ a real number $P(A)$ called the probability of $A$, where $\Omega$ is the sample space.

C: Kolmogorov's [first axiom] (non-negativity): for every event $A$, $P(A) \geq 0$, where $P$ is the probability measure.

C: Kolmogorov's [second axiom] (normalization): $P(\Omega) = 1$, where $\Omega$ is the sample space. The certain event has probability one.

C: Kolmogorov's [third axiom] (countable additivity): for any sequence of pairwise disjoint events $A_1, A_2, \ldots$, $P\!\left(\bigcup_{i=1}^{\infty} A_i\right) = \sum_{i=1}^{\infty} P(A_i)$.

Q: Why does the third axiom require the events to be pairwise disjoint?
A: If two events overlap, an outcome in the overlap would be counted in more than one $P(A_i)$, making the right-hand sum exceed the probability of the union. Disjointness rules out this double counting, so the sum of probabilities exactly equals the probability of the union.

Q: Why is countable additivity stated for infinitely many events, not just finitely many?
A: Many natural sample spaces (like the set of positive integers, or a continuous interval decomposed into countably many pieces) involve unions of infinitely many disjoint events. Restricting to finite additivity would leave important limits undefined and break the theory on countable sample spaces.

Q: Why is the bound $P(A) \geq 0$ part of the axioms but $P(A) \leq 1$ is not?
A: Non-negativity is an independent assumption — probabilities as "sizes" of events must never be negative. The upper bound $P(A) \leq 1$ is not axiomatic because it is a theorem derivable from the axioms: it follows from monotonicity applied to $A \subseteq \Omega$ together with $P(\Omega) = 1$.

## 2.8 Basic Consequences

Q: Why do we derive consequences of the axioms rather than stipulating them directly?
A: A small axiom set is easier to justify and check. Every familiar formula — complement, empty-set probability, monotonicity — can be proved from the three Kolmogorov axioms using set identities. Deriving them ensures they are automatically consistent with each other.

C: Probability of the complement: $P(A^c) = [1 - P(A)]$, where $A$ is any event in the sample space $\Omega$.

Q: Derive $P(A^c) = 1 - P(A)$ from the axioms.
A: The events $A$ and $A^c$ are disjoint and their union is $\Omega$. By additivity, $P(A) + P(A^c) = P(\Omega)$. By the normalization axiom, $P(\Omega) = 1$. Therefore $P(A^c) = 1 - P(A)$.

C: Probability of the impossible event: $P(\emptyset) = [0]$, derivable from the axioms.

Q: Derive $P(\emptyset) = 0$ from the axioms.
A: Since $\Omega^c = \emptyset$, by the complement rule $P(\emptyset) = 1 - P(\Omega) = 1 - 1 = 0$.

C: [Monotonicity]: if $A \subseteq B$, then $P(A) \leq P(B)$, where $A, B$ are events in $\Omega$.

Q: Derive monotonicity: if $A \subseteq B$, then $P(A) \leq P(B)$.
A: Write $B = A \cup (B \setminus A)$, where $A$ and $B \setminus A$ are disjoint. By additivity, $P(B) = P(A) + P(B \setminus A)$. By non-negativity, $P(B \setminus A) \geq 0$, so $P(B) \geq P(A)$.

C: Upper bound on probabilities: for every event $A \subseteq \Omega$, $P(A) \leq [1]$, derived from monotonicity applied to $A \subseteq \Omega$ and $P(\Omega) = 1$.

C: Probability of a difference: $P(B \setminus A) = P(B) - P(A \cap B)$, where $A, B$ are events in $\Omega$. In particular, if $A \subseteq B$, then $P(B \setminus A) = [P(B) - P(A)]$.

## 2.9 Inclusion-Exclusion Principle

Q: Why do we need inclusion-exclusion when events are not disjoint?
A: For disjoint events, probabilities simply add. When events overlap, naive addition counts the overlap twice, so the sum exceeds the true union probability. Inclusion-exclusion corrects this by subtracting the over-counted intersections, giving the exact probability of the union.

C: Inclusion-exclusion for two events: $P(A \cup B) = P(A) + P(B) - [P(A \cap B)]$, where $A, B$ are events in $\Omega$.

Q: Why do we subtract $P(A \cap B)$ in the two-event inclusion-exclusion formula?
A: Every outcome in $A \cap B$ is counted once in $P(A)$ and again in $P(B)$, so the sum $P(A) + P(B)$ counts the overlap twice. Subtracting $P(A \cap B)$ once removes the extra count, leaving each outcome in $A \cup B$ counted exactly once.

P: Given $P(A) = 0.6$, $P(B) = 0.5$, and $P(A \cap B) = 0.2$, find $P(A \cup B)$.

S:
**IDENTIFY**: Two-event inclusion-exclusion problem; events are not disjoint since $P(A \cap B) > 0$.

**PLAN**: Apply $P(A \cup B) = P(A) + P(B) - P(A \cap B)$.

**EXECUTE**:
1. Substitute: $P(A \cup B) = 0.6 + 0.5 - 0.2$
2. Compute: $P(A \cup B) = 0.9$

**EVALUATE**: Check $0 \leq 0.9 \leq 1$, consistent with the axioms. Also $P(A \cup B) \geq \max(P(A), P(B)) = 0.6$ by monotonicity, satisfied.

C: Inclusion-exclusion for three events: $P(A \cup B \cup C) = P(A) + P(B) + P(C) - P(A \cap B) - P(A \cap C) - P(B \cap C) + [P(A \cap B \cap C)]$.

Q: Why does the triple intersection $P(A \cap B \cap C)$ appear with a plus sign in three-event inclusion-exclusion?
A: An outcome in $A \cap B \cap C$ is counted three times in the singles $P(A) + P(B) + P(C)$, then subtracted three times (once in each pairwise intersection), leaving it counted zero times. Adding $P(A \cap B \cap C)$ back once restores the correct count of one.

Q: State the general inclusion-exclusion formula for $n$ events $A_1, \ldots, A_n$.
A: $P\!\left(\bigcup_{i=1}^n A_i\right) = \sum_{k=1}^{n} (-1)^{k+1} \sum_{1 \leq i_1 < \cdots < i_k \leq n} P(A_{i_1} \cap \cdots \cap A_{i_k})$, where the alternating signs correct for over- and under-counting as intersection size grows.

P: A card is drawn from a standard 52-card deck. Find $P(\text{heart or face card})$, where face cards are J, Q, K.

S:
**IDENTIFY**: Two-event union on a finite equally likely space; events overlap (heart face cards exist).

**PLAN**: Let $H$ = "heart" and $F$ = "face card". Use $P(H \cup F) = P(H) + P(F) - P(H \cap F)$ with classical probability $|A|/|\Omega|$.

**EXECUTE**:
1. $|\Omega| = 52$
2. $|H| = 13$, so $P(H) = 13/52$
3. $|F| = 12$ (3 face cards per suit $\times$ 4 suits), so $P(F) = 12/52$
4. $|H \cap F| = 3$ (J, Q, K of hearts), so $P(H \cap F) = 3/52$
5. $P(H \cup F) = 13/52 + 12/52 - 3/52 = 22/52 = 11/26$

**EVALUATE**: $0 \leq 11/26 \approx 0.423 \leq 1$; also $P(H \cup F) \geq P(H) = 1/4$ by monotonicity. Both sanity checks pass.

## 2.10 Equally Likely Outcomes and Classical Probability

Q: Why is the equally-likely-outcomes model the historical starting point of probability?
A: Games of chance (coins, dice, cards) motivated probability theory, and in these games each outcome is by construction equally likely. This makes probabilities reducible to counting, which is intuitive and computable. The classical model still underlies combinatorial probability today.

C: [Classical probability] applies when $\Omega$ is finite and every outcome is equally likely; for any event $A$, $P(A) = [|A| / |\Omega|]$, where $|A|$ is the number of outcomes in $A$ and $|\Omega|$ is the total number of outcomes.

Q: Why must the sample space be finite for the classical definition $P(A) = |A|/|\Omega|$ to make sense?
A: The formula divides the count of favorable outcomes by the count of total outcomes. If $|\Omega|$ is infinite, this ratio is not well-defined (infinity divided by infinity), so a different construction — a density or measure — is required. Equal likelihood is meaningful only when outcomes can be counted.

Q: Verify that the classical definition $P(A) = |A|/|\Omega|$ satisfies Kolmogorov's axioms.
A: Non-negativity: $|A| \geq 0$ and $|\Omega| > 0$, so $P(A) \geq 0$. Normalization: $P(\Omega) = |\Omega|/|\Omega| = 1$. Additivity: for disjoint $A$ and $B$, $|A \cup B| = |A| + |B|$, so $P(A \cup B) = (|A| + |B|)/|\Omega| = P(A) + P(B)$. All three axioms hold.

P: A fair six-sided die is rolled once. Find the probability that the result is a prime number.

S:
**IDENTIFY**: Classical probability problem on the finite equally likely space $\Omega = \{1,2,3,4,5,6\}$.

**PLAN**: List the favorable outcomes (primes on a die), then compute $P(A) = |A|/|\Omega|$.

**EXECUTE**:
1. $\Omega = \{1,2,3,4,5,6\}$, so $|\Omega| = 6$
2. Primes in $\Omega$: $A = \{2, 3, 5\}$, so $|A| = 3$
3. $P(A) = 3/6 = 1/2$

**EVALUATE**: $0 \leq 1/2 \leq 1$; exactly half of the faces are prime, which matches the count directly.

P: Two fair coins are flipped. Find the probability of getting at least one head.

S:
**IDENTIFY**: Classical probability; "at least one" suggests using the complement rule for efficiency.

**PLAN**: Let $A$ = "at least one head". Then $A^c$ = "no heads" = "both tails". Compute $P(A) = 1 - P(A^c)$.

**EXECUTE**:
1. $\Omega = \{HH, HT, TH, TT\}$, so $|\Omega| = 4$
2. $A^c = \{TT\}$, so $|A^c| = 1$ and $P(A^c) = 1/4$
3. $P(A) = 1 - 1/4 = 3/4$

**EVALUATE**: Direct count gives $A = \{HH, HT, TH\}$, $|A| = 3$, $P(A) = 3/4$. The two methods agree.

Q: When is using the complement $P(A) = 1 - P(A^c)$ more efficient than counting $A$ directly?
A: When $A^c$ has far fewer outcomes to enumerate, typically for "at least one" events. The complement "none" is usually a single simple condition, while "at least one" splits into many cases. Counting the single case and subtracting from 1 is faster and less error-prone.
