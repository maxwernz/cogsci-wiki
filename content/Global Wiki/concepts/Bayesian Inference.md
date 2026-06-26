---
type: method
status: active
scope: global
classes: [Cognitive Modeling, Neural Coding]
projects:
domains: [statistics, Bayesian, modeling, cognitive science]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_05_Bayes.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Bayesian Inference

## Short definition

Bayesian inference updates a probability distribution over unknowns (parameters or
hypotheses) by combining a prior with the likelihood of observed data to produce a
posterior distribution.

## General explanation

Where [[Maximum Likelihood Estimation]] returns a single best parameter value,
Bayesian inference treats the parameter as a random variable and returns a whole
**posterior distribution**, quantifying remaining uncertainty. You start with a
**prior** $p(\theta)$, observe data, and reshape it through the **likelihood**
$p(x\mid\theta)$ via [[Bayes' Theorem]] into the **posterior** $p(\theta\mid x)$.
Point summaries (posterior mean/mode) and **credible intervals** are read off the
posterior.

Two contrasts matter. (1) **Frequentist vs Bayesian probability:** frequentists
read probability as long-run frequency of repeatable events; Bayesians read it as
degree of belief, applicable to single events. Subjective ≠ arbitrary — Cox (1946)
showed consistent graded beliefs must obey the probability axioms, and rational
agents converge as data accumulate. (2) **Frequentist vs Bayesian modeling:**
frequentists estimate a fixed $\theta$ and use the [[The Bootstrap|bootstrap]] for
variability; Bayesians compute a posterior, often via **MCMC** (computationally
expensive). The locus of controversy is the **subjectivity of the prior**. A
**regulariser** is the frequentist analogue of a complexity-disfavouring prior
([[Regularisation]]).

In cognitive science, Bayesian inference is also a *hypothesis about the mind* —
the "Bayesian brain" — which can be asserted at any of [[Marr's Levels of Analysis]] (computational/ideal-observer, algorithmic, implementational), and is
critiqued as "Bayesian Fundamentalism" when rational analysis is taken to imply
mechanism without evidence.

## Intuition

You hold a belief about the world, see some evidence, and revise the belief in
proportion to how well each possibility predicted that evidence. The output is not
"the answer" but a *distribution* of how plausible each answer now is.

## Formal definition

$$p(\theta\mid x)=\frac{p(x\mid\theta)\,p(\theta)}{p(x)},\qquad p(x)=\int p(x\mid\theta)\,p(\theta)\,\mathrm{d}\theta.$$

- $p(\theta)$: prior; $p(x\mid\theta)$: likelihood; $p(x)$: evidence; $p(\theta\mid
  x)$: posterior. Sequential updating uses each posterior as the next prior.

## Worked example

Estimating a coin's bias $p$ from $k=8$ heads in $n=10$ tosses with a uniform
prior Beta(1,1): the posterior is Beta($1+8, 1+2$) = Beta(9,3), with posterior
mean $9/12=0.75$ and a credible interval read from the Beta distribution — a full
distribution over $p$, not just a point estimate.

## Why it matters

Bayesian inference underpins modern statistics, probabilistic machine learning,
optimal neural decoding, and a dominant (if contested) theoretical framework for
perception and cognition.

## Used in

- [[Bayesian Inference in Cognitive Modeling]] (VL5)
- [[Schutt et al 2016 Bayesian Psychometric Functions]] (credible intervals)
- [[Encoding and Decoding]] (Bayesian decoding)

## Related concepts

- [[Bayes' Theorem]]
- [[Maximum Likelihood Estimation]]
- [[Marr's Levels of Analysis]]
- [[Regularisation]]
- [[The Bootstrap]]

## Common confusions

- Bayesian ≠ arbitrary: priors are constrained by the axioms and converge with
  data.
- A Bayesian model of behaviour implies the brain runs Bayes' rule only if claimed
  at the algorithmic/implementational level, not the computational level.
- Posterior credible intervals are not the same as frequentist confidence
  intervals (different interpretations).

## Sources

- [[VL05 Bayes]]
