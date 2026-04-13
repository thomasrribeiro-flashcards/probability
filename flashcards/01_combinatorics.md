+++
name = "Probability"
subject = "Math"
order = 1
tags = ["math", "probability", "combinatorics", "counting", "permutations", "combinations"]
+++

# Probability — Combinatorics and Counting

## 1.1 Motivation

Q: Why do we start a probability course with combinatorics?
A: Many probabilities reduce to a ratio "favorable outcomes / total outcomes", so computing a probability often means counting two sets. Combinatorics provides the tools to count large finite sets without enumerating them. Before we can compute $P(A) = |A|/|\Omega|$ in any serious example, we need reliable ways to find $|A|$ and $|\Omega|$, where $\Omega$ is the sample space and $A$ is the event of interest.

Q: Why is direct enumeration usually not enough for counting problems?
A: The number of outcomes grows explosively — dealing 5 cards from a 52-card deck already gives over 2.5 million hands. Listing them by hand is infeasible, so we need structural rules (multiplication, addition, permutations, combinations) that produce counts from small inputs.

C: In a finite equally-likely model, the probability of event $A$ is $P(A) = [|A|/|\Omega|]$, where $|A|$ is the number of favorable outcomes and $|\Omega|$ is the total number of outcomes.

C: Combinatorics is the branch of mathematics concerned with [counting], arranging, and selecting objects from finite sets.

Q: Why does combinatorics care about the difference between ordered and unordered selections?
A: "How many ways can three runners finish 1st, 2nd, 3rd?" and "How many groups of three runners can I pick?" have different answers because order matters in the first but not the second. Getting probability right depends on matching the counting method (ordered vs. unordered) to how the outcomes are actually distinguished.

## 1.2 Multiplication (Product) Rule

Q: Why does the multiplication rule work?
A: If a task is built from independent stages, every choice at one stage can be paired with every choice at the next. So the total number of outcomes is the product of the number of choices at each stage — the "branches of a decision tree" multiply rather than add.

C: [Multiplication rule]: if a procedure has $k$ stages with $n_1, n_2, \ldots, n_k$ choices at each stage (choices at later stages not depending on earlier ones), the total number of outcomes is $n_1 \cdot n_2 \cdots n_k$.

Q: If a menu offers 4 starters, 5 mains, and 3 desserts, how many three-course meals are possible, and why?
A: $4 \cdot 5 \cdot 3 = 60$. Each starter can be paired with each main (giving $4 \cdot 5 = 20$ two-course combinations), and each of those with each dessert, multiplying by 3 more.

C: The number of binary strings of length $n$ is $[2^n]$, because each of the $n$ positions independently has 2 choices.

C: The number of functions from a set of size $k$ to a set of size $n$ is $[n^k]$, because each of the $k$ inputs independently maps to one of $n$ outputs.

Q: When does the multiplication rule fail?
A: When later choices depend on earlier ones in a way that changes how many options remain, and that dependency isn't captured by a single fixed count per stage. You can still use it if you can describe the number of choices at each stage as a function of the stage number alone (e.g. permutations).

## 1.3 Addition Rule for Disjoint Cases

Q: Why is the addition rule restricted to disjoint cases?
A: If the cases overlap, outcomes in the overlap get counted more than once. Adding counts only gives the correct total when no outcome belongs to two cases at the same time, so the cases must be mutually exclusive (disjoint).

C: [Addition rule]: if a task can be done in one of $k$ mutually exclusive ways with $n_1, \ldots, n_k$ options in each, the total number of ways is $n_1 + n_2 + \cdots + n_k$.

Q: How do you decide whether to add or multiply when counting?
A: Multiply when outcomes are built by completing several stages in sequence ("and"), and add when outcomes are split into disjoint cases and exactly one case occurs ("or, but not both"). Most real problems combine both: split into disjoint cases, multiply within each case, then add the totals.

C: If two sets $A$ and $B$ are disjoint, then $|A \cup B| = [|A| + |B|]$.

Q: Why must we be careful with "or" in counting?
A: Everyday "or" is ambiguous, but counting needs the exclusive version (disjoint cases). If cases overlap we need the inclusion-exclusion principle, $|A \cup B| = |A| + |B| - |A \cap B|$, not simple addition.

## 1.4 Permutations and Factorials

Q: Why does ordering $n$ distinct objects give $n!$ arrangements?
A: The first position has $n$ choices, the second has $n-1$ (one object is used up), the third has $n-2$, and so on down to 1. By the multiplication rule the total is $n \cdot (n-1) \cdots 2 \cdot 1 = n!$.

C: A [permutation] of a set of objects is an ordered arrangement of those objects.

C: The [factorial] of a non-negative integer $n$, written $n!$, is defined by $n! = n \cdot (n-1) \cdot (n-2) \cdots 2 \cdot 1$ for $n \geq 1$, and $0! = 1$ by convention.

Q: Why do we define $0! = 1$?
A: It's the empty product, and it makes formulas like $P(n,k) = n!/(n-k)!$ and $\binom{n}{k} = n!/(k!(n-k)!)$ work at the boundary cases (e.g. $\binom{n}{0} = 1$). There is exactly one way to arrange zero objects — do nothing — so $0! = 1$ also matches the combinatorial meaning.

C: The number of permutations of $n$ distinct objects is $[n!]$.

C: $5! = [120]$.

Q: Roughly how fast does $n!$ grow?
A: Faster than any exponential $c^n$. For reference, $10! = 3{,}628{,}800$ and $20!$ is about $2.4 \times 10^{18}$. This is why direct enumeration fails quickly and we need compact formulas.

## 1.5 Permutations of n Objects Taken k at a Time

Q: Why do we need a formula for $P(n,k)$ separate from $n!$?
A: Often we arrange only some of the available objects — e.g. picking 1st, 2nd, 3rd place from 8 runners. We want the number of ordered selections of size $k$ from $n$ distinct objects, not all $n!$ full arrangements.

C: $P(n,k)$, the number of [permutations of $n$ distinct objects taken $k$ at a time], counts ordered selections of $k$ objects from $n$ where order matters and no object is repeated.

C: The formula for permutations is $P(n,k) = [n!/(n-k)!]$, where $n$ is the number of available distinct objects and $k$ is the number chosen (with $0 \leq k \leq n$).

Q: Why is $P(n,k) = n!/(n-k)!$ rather than just $n!$?
A: Arranging all $n$ objects overcounts ordered $k$-selections because it also orders the $n-k$ objects we didn't pick. Dividing by $(n-k)!$ collapses those irrelevant orderings, leaving only the orderings of the $k$ chosen objects.

Q: Derive $P(n,k)$ directly from the multiplication rule.
A: The first chosen object has $n$ options, the second has $n-1$, down to the $k$-th which has $n-k+1$. Multiplying: $P(n,k) = n(n-1)\cdots(n-k+1)$, and multiplying and dividing by $(n-k)!$ rewrites this as $n!/(n-k)!$.

C: $P(n,n) = [n!]$, because taking all $n$ objects in order is just a full permutation.

C: $P(n,0) = [1]$, because there is exactly one ordered selection of zero objects — the empty arrangement.

P: How many ways can 8 sprinters finish 1st, 2nd, and 3rd?

S:
**IDENTIFY**: Ordered selection of $k=3$ from $n=8$ distinct objects (order matters: gold, silver, bronze are different).

**PLAN**: Apply the permutation formula $P(n,k) = n!/(n-k)!$ with $n=8$, $k=3$.

**EXECUTE**:
1. $P(8,3) = 8!/(8-3)! = 8!/5!$.
2. Cancel: $8!/5! = 8 \cdot 7 \cdot 6$.
3. Compute: $8 \cdot 7 = 56$, then $56 \cdot 6 = 336$.

**EVALUATE**: 336 possible podiums. Check by multiplication rule: 8 choices for gold, 7 for silver, 6 for bronze, $8 \cdot 7 \cdot 6 = 336$. ✓

## 1.6 Combinations

Q: Why do we need combinations in addition to permutations?
A: Many questions ask how many groups can be formed regardless of order — e.g. how many 5-card poker hands exist. Permutations overcount every group by the number of ways to order it, so we need a formula that divides that overcount out.

C: A [combination] of $n$ distinct objects taken $k$ at a time is an unordered selection of $k$ objects from the $n$, with no object repeated.

C: The number of combinations of $n$ objects taken $k$ at a time is $\binom{n}{k} = [n!/(k!(n-k)!)]$, where $n$ is the size of the pool and $k$ is the size of the selected subset ($0 \leq k \leq n$).

Q: Why is the combination formula $\binom{n}{k} = P(n,k)/k!$?
A: Each unordered $k$-subset can be arranged in $k!$ different orders, and $P(n,k)$ counts each ordering separately. Dividing $P(n,k)$ by $k!$ identifies all these equivalent orderings, leaving one count per subset.

C: $\binom{n}{k}$ is read "[n choose k]" and equals the number of $k$-element subsets of an $n$-element set.

C: $\binom{n}{0} = [1]$, because the empty subset is the only way to choose 0 objects.

C: $\binom{n}{n} = [1]$, because there is exactly one way to choose all $n$ objects.

Q: Why does $\binom{n}{k} = \binom{n}{n-k}$?
A: Choosing which $k$ objects to include is equivalent to choosing which $n-k$ objects to exclude — the two sets are in one-to-one correspondence. So the counts must be equal.

C: The symmetry identity $\binom{n}{k} = \binom{n}{n-k}$ follows because choosing a subset of size $k$ is equivalent to choosing its [complement] of size $n-k$.

P: How many 5-card hands can be dealt from a standard 52-card deck?

S:
**IDENTIFY**: Unordered selection of $k=5$ from $n=52$ (a hand is unordered).

**PLAN**: Apply the combination formula $\binom{n}{k} = n!/(k!(n-k)!)$ with $n=52$, $k=5$.

**EXECUTE**:
1. $\binom{52}{5} = \frac{52!}{5!\,47!} = \frac{52 \cdot 51 \cdot 50 \cdot 49 \cdot 48}{5!}$.
2. Numerator: $52 \cdot 51 \cdot 50 \cdot 49 \cdot 48 = 311{,}875{,}200$.
3. Denominator: $5! = 120$.
4. Divide: $311{,}875{,}200 / 120 = 2{,}598{,}960$.

**EVALUATE**: 2,598,960 hands. Sanity check: $\binom{52}{5}$ must be much smaller than $P(52,5) = 311{,}875{,}200$ (ordered), and larger than $\binom{52}{1} = 52$. Our value is between them and matches the standard poker count. ✓

## 1.7 Binomial Theorem and Pascal's Identity

Q: Why are $\binom{n}{k}$ called binomial coefficients?
A: They appear as the coefficients when the binomial $(x+y)^n$ is expanded. Each term in the expansion corresponds to choosing $k$ of the $n$ factors to contribute a $y$ (and the remaining $n-k$ to contribute an $x$), and there are $\binom{n}{k}$ such choices.

C: The [binomial theorem] states that $(x+y)^n = \sum_{k=0}^{n} \binom{n}{k} x^{n-k} y^k$, where $n$ is a non-negative integer and $x, y$ are any numbers.

Q: In the expansion of $(x+y)^n$, what is the coefficient of $x^{n-k} y^k$, and why?
A: The coefficient is $\binom{n}{k}$. To produce $x^{n-k} y^k$, we pick which $k$ of the $n$ parenthesized $(x+y)$ factors will contribute a $y$; there are $\binom{n}{k}$ such choices.

C: In the expansion $(x+y)^n$, the coefficient of the term $x^{n-k} y^k$ is $[\binom{n}{k}]$.

Q: Why does $\sum_{k=0}^{n} \binom{n}{k} = 2^n$?
A: Setting $x = y = 1$ in the binomial theorem gives $(1+1)^n = \sum_{k=0}^{n} \binom{n}{k}$, i.e. $2^n$. Combinatorially, the left side counts all subsets of an $n$-set (each element is in or out, giving $2^n$), and the right side counts them by size.

C: The total number of subsets of an $n$-element set is $[2^n] = \sum_{k=0}^{n}\binom{n}{k}$.

C: [Pascal's identity]: $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$ for integers $1 \leq k \leq n-1$.

Q: Give a combinatorial proof of Pascal's identity.
A: Fix one particular element $x$ of the $n$-set. Every $k$-subset either contains $x$ (then we pick the remaining $k-1$ from the other $n-1$ elements: $\binom{n-1}{k-1}$ ways) or does not contain $x$ (pick all $k$ from the other $n-1$: $\binom{n-1}{k}$ ways). These cases are disjoint and exhaustive, so they add to $\binom{n}{k}$.

C: Pascal's triangle builds each row by adding [adjacent entries] from the previous row, which is exactly Pascal's identity in visual form.

## 1.8 Multinomial Coefficients and the Multinomial Theorem

Q: Why do we generalize binomial coefficients to multinomial coefficients?
A: Binomial coefficients handle splitting $n$ objects into 2 groups. Many problems split into more than 2 groups — e.g. dealing $n$ cards into 4 hands. Multinomial coefficients count the number of ways to partition $n$ distinct objects into $r$ groups of specified sizes.

C: The [multinomial coefficient] $\binom{n}{n_1,\,n_2,\,\ldots,\,n_r} = \dfrac{n!}{n_1!\,n_2!\cdots n_r!}$ counts the number of ways to partition $n$ distinct objects into $r$ ordered groups of sizes $n_1, n_2, \ldots, n_r$, where $n_1 + n_2 + \cdots + n_r = n$.

Q: Why is the multinomial coefficient $n!/(n_1! n_2! \cdots n_r!)$?
A: Order all $n$ objects in a row ($n!$ ways), then assign the first $n_1$ to group 1, the next $n_2$ to group 2, and so on. Reorderings within each group produce the same partition, so divide by $n_1! n_2! \cdots n_r!$.

C: When $r=2$, the multinomial coefficient $\binom{n}{k,\,n-k}$ reduces to the binomial coefficient $[\binom{n}{k}]$.

C: The [multinomial theorem]: $(x_1 + x_2 + \cdots + x_r)^n = \sum \binom{n}{n_1,\ldots,n_r} x_1^{n_1} x_2^{n_2} \cdots x_r^{n_r}$, summed over all non-negative integers $n_1, \ldots, n_r$ with $n_1 + \cdots + n_r = n$.

P: How many distinct arrangements are there of the letters in MISSISSIPPI?

S:
**IDENTIFY**: Arranging $n=11$ letters where letters repeat: 1 M, 4 I's, 4 S's, 2 P's. This is a multinomial (permutation-with-repetition) problem.

**PLAN**: Use $n!/(n_1!\,n_2!\cdots n_r!)$ with $n=11$ and group sizes $1, 4, 4, 2$.

**EXECUTE**:
1. Total arrangements if all letters were distinct: $11! = 39{,}916{,}800$.
2. Divide by overcounts: $1! \cdot 4! \cdot 4! \cdot 2! = 1 \cdot 24 \cdot 24 \cdot 2 = 1152$.
3. $11! / 1152 = 39{,}916{,}800 / 1152 = 34{,}650$.

**EVALUATE**: 34,650 distinct arrangements. Sanity check: the answer is much smaller than $11!$ (expected, because of repeats) but far larger than $11$ (expected, because there are many distinct permutations). ✓

## 1.9 Distinguishable vs Indistinguishable Objects

Q: Why does indistinguishability reduce the number of arrangements?
A: Swapping two identical objects leaves the arrangement looking the same. If we count all $n!$ orderings, every truly distinct arrangement is counted multiple times — once for every reordering of the identical objects. Dividing by those reorderings corrects the overcount.

C: The number of distinguishable permutations of $n$ objects where there are $n_1$ of type 1, $n_2$ of type 2, ..., $n_r$ of type $r$ (with $n_1 + \cdots + n_r = n$) is $[n!/(n_1!\,n_2!\cdots n_r!)]$.

Q: Why is "permutation with repetition" the same formula as the multinomial coefficient?
A: Arranging letters with repeats is equivalent to partitioning the $n$ positions into groups by letter type — positions get "letter 1" ($n_1$ of them), "letter 2" ($n_2$), etc. That partition count is exactly $n!/(n_1! \cdots n_r!)$.

Q: How many distinct arrangements of the word BANANA are there, and why?
A: $6!/(1! \cdot 3! \cdot 2!) = 720/12 = 60$. There are 6 letters total (1 B, 3 A's, 2 N's); dividing $6!$ by $3!$ removes duplicate orderings of the three A's, and by $2!$ removes duplicate orderings of the two N's.

C: If all $n$ objects are distinguishable, the number of arrangements reduces to $[n!]$, because each $n_i = 1$ and every factorial in the denominator equals 1.

## 1.10 Stars and Bars (Combinations with Repetition)

Q: Why do we need a new formula for combinations with repetition?
A: The usual $\binom{n}{k}$ counts choices where each object is picked at most once. But sometimes we pick $k$ items from $n$ types where repeats are allowed — e.g. buying 10 donuts from 5 varieties. The objects in the selection aren't distinct, so neither ordering nor exclusion arguments apply directly.

C: The number of ways to choose $k$ objects from $n$ types with [repetition allowed] and order ignored is $\binom{n+k-1}{k}$, where $n$ is the number of types and $k$ is the number of objects chosen.

Q: Why is the stars-and-bars formula $\binom{n+k-1}{k}$?
A: Represent a selection as $k$ stars (the objects) separated by $n-1$ bars (between the $n$ type-bins). Any arrangement of $k$ stars and $n-1$ bars in a row of length $n+k-1$ determines a unique selection, and every selection corresponds to one arrangement. Choose the $k$ star positions from $n+k-1$ slots: $\binom{n+k-1}{k}$.

C: The number of non-negative integer solutions to $x_1 + x_2 + \cdots + x_n = k$ is $[\binom{n+k-1}{k}]$, where each $x_i \geq 0$ represents the count in type $i$.

Q: Why does counting solutions to $x_1 + \cdots + x_n = k$ use the same formula?
A: Each solution assigns a non-negative count $x_i$ to each of $n$ types so that the counts total $k$ — exactly the same data as picking $k$ items from $n$ types with repetition. The star-and-bar diagram maps one to one with both interpretations.

C: In the stars-and-bars diagram, [stars] represent the objects being chosen and [bars] separate the different types (using only 1 cloze here: the stars).

Q: How many ways can you distribute 10 identical donuts among 5 varieties (any variety can be chosen any number of times, including zero)?
A: $\binom{5+10-1}{10} = \binom{14}{10} = \binom{14}{4} = 1001$. Each distribution is a non-negative integer solution to $x_1 + x_2 + x_3 + x_4 + x_5 = 10$, where $x_i$ is the number of donuts of variety $i$.

C: If each type must be chosen at least once (i.e. $x_i \geq 1$), substitute $y_i = x_i - 1$ to reduce to the non-negative case, giving $[\binom{k-1}{n-1}]$ solutions for $x_1 + \cdots + x_n = k$ with $x_i \geq 1$.

Q: Summarize: when picking $k$ items from $n$, which of the four counting formulas applies?
A: Ordered, no repetition: $P(n,k) = n!/(n-k)!$. Ordered, with repetition: $n^k$. Unordered, no repetition: $\binom{n}{k}$. Unordered, with repetition: $\binom{n+k-1}{k}$. Choose by first asking "does order matter?" then "are repeats allowed?".

C: Ordered selection of $k$ from $n$ with repetition allowed has $[n^k]$ outcomes, because each of the $k$ positions independently has $n$ choices.

C: Unordered selection of $k$ from $n$ without repetition has $[\binom{n}{k}]$ outcomes.
