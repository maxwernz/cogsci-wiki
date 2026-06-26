---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, Bayesian, modeling, cognitive science]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_05_Bayes.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Bayesian Inference in Cognitive Modeling

## Short definition

Bayesian inference updates a probability distribution over a model's parameters
(or hypotheses) in light of data, by combining a prior with the likelihood to get
a posterior — and, in cognitive science, is also a *hypothesis about how the mind
works*.

## Intuition

Instead of returning a single best parameter value (like MLE), Bayesian inference
returns a whole *distribution* of plausible values, weighted by how much you
believe each one after seeing the data. You start with a prior belief, the data
reshape it through the likelihood, and out comes a posterior belief. The word
"Bayes" hides several distinct ideas, and most arguments about Bayes are really
arguments about *which* of those ideas you mean.

## Explanation

VL5 untangles **five "faces of Bayes"**, ordered from uncontroversial to
contentious:

1. **Bayes' theorem** — a mathematical rule for inverting conditional
   probabilities (probability of a cause given its effect). *Everyone* accepts
   it; it is just arithmetic.
2. **Bayesian probability** — the philosophical claim that probabilities are
   *degrees of belief* (subjective/epistemic), as opposed to the **frequentist**
   view that they are long-run relative frequencies of repeatable events. This is
   genuinely contested. But subjective ≠ arbitrary: Cox (1946) showed any
   consistent, transitive system of graded beliefs must obey the probability
   axioms; rational agents converge as data accumulate; and you should bet at
   your stated odds. The arithmetic is identical either way.
3. **Bayesian statistics** — using Bayes factors for hypothesis testing instead
   of $p$-values (covered only in passing here).
4. **Bayesian modeling** — the modeling counterpart to MLE: combine a prior over
   parameters with the likelihood to obtain a posterior *distribution*.
5. **Bayesian mind/brain** — the empirical hypothesis that the brain itself
   computes (approximately) like a Bayesian — the most contentious face.

**Bayesian vs frequentist modeling** (the VL2–4 contrast made explicit):

- *Frequentist:* there is a true, fixed parameter $\theta$; the **data** are the
  random variable; you estimate $\theta$ (MLE) and use the **bootstrap** to gauge
  its variability.
- *Bayesian:* $\theta$ is *also* treated as a random variable; you place a prior
  over it and compute a **posterior** that quantifies remaining uncertainty,
  often via **MCMC** (computationally expensive). Once data are observed they are
  fixed; uncertainty lives in the posterior over $\theta$.

The locus of controversy is the **subjectivity of the prior**. A well-justified,
objective prior makes Bayesian inference uncontroversial (medicine, engineering,
law). But in cognitive science priors are often chosen by the researcher, and a
"poor model + conveniently chosen prior" can be made to fit. Note the link to
[[Cross-Validation and Regularisation]]: a **regulariser is analogous to a
prior** that disfavours complex models — the difference is that regularisation
tunes the trade-off via $\lambda$ (by cross-validation) rather than fixing it by a
prior.

**The Bayesian brain** can be asserted at any of [[Marr's Levels of Analysis]]:
computational (an *ideal-observer / rational analysis* specifying the optimal
solution), algorithmic (people actually combine prior + data via Bayes' rule), or
implementational (neurons code probability distributions — "Bayesian realism",
not yet convincingly evidenced). Critiques: **Bayesian Fundamentalism** (Jones &
Love, 2011) — too much rational analysis at the computational level with no
attention to process or mechanism; post-hoc priors; and the computational
implausibility of full Bayesian inference as a brain algorithm.

## Worked example

Bayesian perception as Helmholtz's "unconscious inference": infer the scene $S$
from retinal input $I$ via $p(S\mid I)\propto p(S)\,p(I\mid S)$. The prior $p(S)$
encodes how probable scenes are (e.g. light usually comes from above); the
likelihood $p(I\mid S)$ says how probable the image is given a scene; the
posterior $p(S\mid I)$ is the perceived scene. This is a *computational-level*
(ideal-observer) claim — it does not require that neurons explicitly represent or
apply Bayes' rule (Griffiths et al., 2010).

## Formal definition / equations

Bayes' theorem in modeling form:

$$p(\theta\mid x) = \frac{p(x\mid\theta)\,p(\theta)}{p(x)},\qquad p(x)=\int p(x\mid\theta)\,p(\theta)\,\mathrm{d}\theta.$$

- $p(\theta)$: prior; $p(x\mid\theta)$: likelihood; $p(x)$: evidence
  (normaliser); $p(\theta\mid x)$: posterior. For inference about a scene/cause
  the proportional form $p(S\mid I)\propto p(S)\,p(I\mid S)$ drops the normaliser.

## Role in this class or project

The fifth fundamentals lecture ([[VL05 Bayes]]) and the conceptual alternative to
the frequentist machinery of VL2–4. It also frames the "Bayesian utility model"
in [[VL08 Model Comparison Example]] and connects to regularisation (VL3) and
Marr's levels (used throughout the Butz lectures).

## Exam, assignment, or project relevance

Write Bayes' theorem and name each term; distinguish the five faces of Bayes;
contrast frequentist vs Bayesian *probability* and *modeling*; explain why priors
are the locus of controversy; relate priors to regularisation; and place a
"Bayesian brain" claim at the correct Marr level, including the Fundamentalism
critique. (No compulsory reading, but the conceptual distinctions are examinable.)

## Related global concepts

- [[Bayes' Theorem]]
- [[Bayesian Inference]]
- [[Marr's Levels of Analysis]]
- [[Maximum Likelihood Estimation]]

## Related local pages

- [[Marr's Levels of Analysis]]
- [[Cross-Validation and Regularisation]]
- [[Maximum Likelihood Estimation in Cognitive Modeling]]

## Common confusions

- **"Bayesian = subjective/arbitrary."** Subjective priors are constrained by the
  probability axioms and converge with data; the maths is shared with
  frequentism.
- **"A Bayesian model of behaviour means the brain runs Bayes' rule."** Only if
  the claim is made at the algorithmic/implementational level; a computational-
  level (ideal-observer) claim does not require explicit Bayesian computation.
- **"Bayes' theorem is controversial."** The theorem is not; the *interpretation
  of probability* and the *Bayesian brain* are.

## Sources

- [[VL05 Bayes]]
- [[Schutt et al 2016 Bayesian Psychometric Functions]]
