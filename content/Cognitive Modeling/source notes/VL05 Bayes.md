---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: lecture_slides
raw_path: Classes/Cognitive Modeling/raw/Slides/VLCogMod_05_Bayes.pdf
created: 2026-06-09
updated: 2026-06-09
---

# VL05 — Bayes

> Reading (from [[ReadingList-VL2-5.pdf|reading list]]): *no compulsory reading.*
> Suggested further reading cited on the slides: Dienes (2008), Etz &
> Vandekerckhove (2018), Sivia (2006), Lee & Wagenmakers (2013), Schütt et al.
> (2016) ([[Schutt et al 2016 Bayesian Psychometric Functions]]), Wagenmakers et
> al. (2018), Griffiths et al. (2010), Zednik & Jäkel (2016); sceptical: Bowers &
> Davis (2012), Jones & Love (2011).

## Summary

The final fundamentals lecture clarifies what "Bayes" actually means, because
the word is used for at least five distinct things. The lecture's organising
device is **"the many faces of Bayes"**: (1) **Bayes' theorem** — pure maths,
uncontroversial; (2) **Bayesian probability** — the philosophical claim that
probabilities are degrees of belief (contentious); (3) **Bayesian statistics** —
inference via Bayes factors instead of p-values (touched only briefly); (4)
**Bayesian modeling** — using priors+likelihood to get a posterior *distribution*
over parameters, an alternative to the frequentist MLE of VL2–4; and (5) the
**Bayesian mind/brain** — the empirical hypothesis that the brain itself
computes like a Bayesian (most contentious). David Marr's **levels of analysis**
are introduced as the tool for keeping these claims straight.

## Key points

- **Bayes' theorem** is just a rule for inverting conditional probabilities
  ("the probability of a cause given its effect"). *Everyone* — frequentist or
  Bayesian — accepts it.
- **Frequentist vs Bayesian probability.** Frequentist (classical/orthodox):
  probabilities are long-run relative frequencies, measurable by counting; apply
  only to repeatable events. Bayesian (subjective/epistemic): probabilities are
  degrees of belief, applicable to single events ("60% chance I pass the exam").
- **Subjective ≠ arbitrary.** Cox (1946) showed that any consistent,
  transitive system of graded beliefs must obey the probability axioms; rational
  agents' beliefs converge as data accumulate; you should be willing to bet at
  your stated odds. The *arithmetic* is identical either way.
- **Bayesian modeling vs frequentist modeling.** Frequentist: θ is a fixed
  unknown, the *data* are the random variable; estimate θ, use the bootstrap to
  judge variability. Bayesian: θ is *also* a random variable; combine a prior
  over θ with the likelihood to get a *posterior distribution*, often via MCMC
  (computationally expensive). The controversy is about the **subjectivity of
  priors**.
- **Bayesian mind/brain** can be claimed at any of Marr's three levels:
  computational (rational/ideal-observer analysis), algorithmic (people combine
  prior+data via Bayes' rule), implementational (neurons code probabilities —
  "Bayesian realism", not yet convincingly evidenced).
- **Critiques.** "Bayesian Fundamentalism" (Jones & Love, 2011): too much
  rational analysis at the computational level, ignoring process and mechanism.
  Priors can be chosen post-hoc to make a poor model fit. Full Bayesian
  inference may be computationally implausible as a brain algorithm.

## Equations or formal definitions

Bayes' theorem in the modeling form:

$$\underbrace{p(\theta\mid x)}_{\text{posterior}} = \frac{\overbrace{p(x\mid\theta)}^{\text{likelihood}}\;\overbrace{p(\theta)}^{\text{prior}}}{\underbrace{p(x)}_{\text{evidence}}}$$

- $p(\theta)$: prior belief over parameters before data; $p(x\mid\theta)$:
  likelihood (how probable the data are under θ); $p(x)$: evidence /
  normalising constant; $p(\theta\mid x)$: posterior, the updated belief.

Bayesian perception (Helmholtz's "unconscious inference"), often with the
normaliser dropped:

$$p(S\mid I) \propto p(S)\,p(I\mid S)$$

- $S$: scene/cause in the world; $I$: retinal input/image. The prior $p(S)$
  says how probable scenes are; $p(I\mid S)$ is the likelihood of the image
  given a scene; the posterior $p(S\mid I)$ is the inferred scene.

## Methods, models, or theories

- **Bayesian inference / modeling** — see [[Bayesian Inference in Cognitive Modeling]].
- **Marr's three levels of analysis** (computational / algorithmic /
  implementational), illustrated with how a fly measures visual motion
  (computation: optic-flow goal; algorithm: Hassenstein–Reichardt detector;
  implementation: medulla circuitry) — see [[Marr's Levels of Analysis]].
- **Ideal-observer / rational analysis** as the computational-level formalism.

## Local relevance

Bayes is the conceptual counterpart to the frequentist machinery of VL2–4: it
re-frames "estimate θ + error bars" as "compute a posterior over θ". The
prior–penalty analogy connects back to [[Regularisation]] (VL3): a regulariser
plays a role analogous to a Bayesian prior. Marr's levels recur throughout the
Butz lectures and are broadly reusable.

## Exam or project relevance

Be able to: write Bayes' theorem and name each term; contrast frequentist and
Bayesian *probability* and *modeling*; explain why priors are the locus of
controversy; lay out Marr's three levels and place a "Bayesian brain" claim at
the right level; and summarise the Fundamentalism critique. (No compulsory
reading, but the conceptual distinctions are fair game.)

## Links to global concepts

- [[Bayes' Theorem]] (global)
- [[Bayesian Inference]] (global)
- [[Marr's Levels of Analysis]] (global)

## Open questions

- How exactly a regulariser corresponds to a specific prior (MAP estimation) is
  asserted but not derived in the lecture.
