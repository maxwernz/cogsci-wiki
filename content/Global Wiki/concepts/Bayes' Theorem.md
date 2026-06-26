---
type: concept
status: active
scope: global
classes: [Cognitive Modeling, Neural Coding]
projects:
domains: [statistics, probability, Bayesian]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_05_Bayes.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Bayes' Theorem

## Short definition

Bayes' theorem is the rule for inverting conditional probabilities: it computes
the probability of a hypothesis given evidence from the probability of the
evidence given the hypothesis.

## General explanation

Bayes' theorem rewrites $p(H\mid E)$ in terms of $p(E\mid H)$, the prior $p(H)$,
and the evidence $p(E)$. It is a mathematical identity — *uncontroversial and
accepted by every statistician*, Bayesian or frequentist alike. The controversy
attached to "Bayes" concerns the *interpretation* of probability (degrees of
belief vs frequencies) and the *use* of Bayes' theorem for inference with
subjective priors (see [[Bayesian Inference]]), not the theorem itself.

In modeling, the hypothesis is usually a parameter value $\theta$ and the evidence
is the data $x$: the theorem turns the likelihood $p(x\mid\theta)$ and a prior
$p(\theta)$ into a posterior $p(\theta\mid x)$. The denominator $p(x)$ is a
normalising constant (the "evidence" or marginal likelihood), often dropped when
only relative posterior values are needed.

## Intuition

You know how probable the evidence is *under* each hypothesis (forward
direction); Bayes flips this to tell you how probable each hypothesis is *given*
the evidence (inverse direction). A positive medical test is evidence; Bayes
combines the test's accuracy with the disease's base rate to give the probability
you actually have the disease.

## Formal definition

$$p(H\mid E)=\frac{p(E\mid H)\,p(H)}{p(E)},\qquad p(E)=\sum_{H'} p(E\mid H')\,p(H').$$

- $p(H)$: prior; $p(E\mid H)$: likelihood; $p(E)$: evidence/normaliser;
  $p(H\mid E)$: posterior. In modeling form: $p(\theta\mid x)\propto p(x\mid\theta)\,p(\theta)$.

## Worked example

A disease affects 1% of people; a test is 99% sensitive and 95% specific. For a
positive test: $p(\text{disease}\mid +)=\dfrac{0.99\times0.01}{0.99\times0.01+0.05\times0.99}=\dfrac{0.0099}{0.0099+0.0495}\approx 0.167$.
Despite the "99% accurate" test, only ~17% of positives truly have the disease —
because the base rate (prior) is low. This base-rate effect is the classic Bayes'
theorem lesson.

## Why it matters

Bayes' theorem is the backbone of all Bayesian statistics and modeling, of optimal
decoding in neuroscience, of medical/diagnostic reasoning, and of the
"Bayesian brain" hypothesis in perception and cognition.

## Used in

- [[Bayesian Inference in Cognitive Modeling]] (VL5)
- [[Encoding and Decoding]] (Bayesian decoding of neural activity)

## Related concepts

- [[Bayesian Inference]]
- [[Maximum Likelihood Estimation]]
- [[Marr's Levels of Analysis]]

## Common confusions

- The theorem is not controversial; the interpretation of probability and the use
  of subjective priors are.
- $p(H\mid E)\ne p(E\mid H)$ — confusing them is the "prosecutor's fallacy".
- Base rates (the prior) matter: a highly accurate test can still yield mostly
  false positives for a rare condition.

## Sources

- [[VL05 Bayes]]
