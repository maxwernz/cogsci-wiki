---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: lecture_slides
raw_path: Classes/Cognitive Modeling/raw/Slides/VLCogMod_04_CIs.pdf
created: 2026-06-09
updated: 2026-06-09
---

# VL04 — Assessing variability

> Reading (from [[ReadingList-VL2-5.pdf|reading list]]): Farrell & Lewandowsky (2018)
> §3.5 (pp. 65–70) and Wichmann & Hill (2001b) — the bootstrap-and-confidence-
> intervals companion paper ([[Wichmann and Hill (2001b)]]). Optional companion:
> Wichmann & Hill (2001a) ([[Wichmann and Hill 2001a Psychometric Function I]]).
> User note: [[VL4 Assessing variability]].

## Summary

Step three of the recipe: a point estimate $\hat\theta$ is not enough — we need
**error bars** (confidence intervals) on the fitted parameters. Without them we
cannot tell whether two conditions truly differ, or whether the data even
constrain the parameters. Analytic variability estimates are usually impossible
for realistic cognitive models, so the lecture introduces the **bootstrap**: a
resampling (Monte Carlo) method that constructs a sampling distribution from a
single dataset. It contrasts the **non-parametric** bootstrap (resample the
data) with the **parametric** bootstrap (resample from the fitted model), and
uses Wichmann & Hill (2001b) to surface real-world subtleties: the **bootstrap
bridging assumption**, a parametric-bootstrap failure mode, and which
sensitivities are "features" vs "bugs". It closes by stating the **three-step
recipe** explicitly (parameters → error bars → goodness-of-fit), warning against
"chi-by-eye".

## Key points

- **Why variability?** (1) To compare parameters across conditions you need to
  know if a numerical difference is meaningful. (2) Very wide CIs reveal that the
  data do not constrain the parameters (too little/wrong data or wrong model).
- **The bootstrap idea** (Efron, 1979): the empirical sample stands in for the
  population; resampling *with replacement* mimics drawing fresh samples, so the
  spread of the resampled estimates approximates the sampling distribution.
  Tukey: "an approximate answer to the right question" beats an exact answer to
  the wrong one.
- **Non-parametric bootstrap:** resample the observed data points with
  replacement (each resample size $N$), refit, repeat ~1,000–10,000 times.
  Answers: *if I got new samples of data, how much would my fits vary?*
- **Parametric bootstrap:** simulate $T$ datasets *from the fitted model* (using
  $\hat\theta$, each of size $N$), refit each, and look at the spread. Answers:
  *if this were the true model, what data would we expect?*
- **Confidence intervals:** percentile method (use the bootstrap distribution's
  percentiles directly) vs BCa (corrects for bias and skewness).
- **Bootstrap bridging assumption** (Wichmann & Hill, 2001b): the parametric
  bootstrap resamples from $\hat\theta$ *as if* it were the true generating
  parameter. This "bridge" from estimate to truth must be checked (via
  sensitivity analysis across nearby generating parameters) — otherwise CIs can
  be misleading.
- **Features vs bugs.** Sensible (feature) dependencies of CI width: the sample
  points $x$, total observations $N$, the sampling scheme $s$. Problematic (bug)
  dependencies: dependence on the (non-essential) distribution function $F$, and
  sensitivity to initial conditions.

## Equations or formal definitions

Non-parametric bootstrap resamples directly from the data; the parametric
bootstrap samples from the fitted probabilities

$$p = f(x; \hat\theta),$$

then refits to obtain bootstrap estimates $\hat\theta^{b}_{1},\dots,\hat\theta^{b}_{T}$,
whose spread estimates the parameter variability (Figure 3.6 in the book).

- $\hat\theta$: parameters fit to the original data; $f(x;\hat\theta)$: the
  fitted model's predicted probabilities; $T$: number of bootstrap samples;
  $N$: size of each bootstrap dataset (= original $N$). The variance across the
  $\hat\theta^{b}_{k}$ gives the error bars.

## Methods, models, or theories

- **The bootstrap** (parametric and non-parametric), percentile and BCa CIs —
  developed in [[The Bootstrap]].
- **Resampling family:** bootstrap, jackknife, permutation tests (Monte Carlo
  methods that "simulate the answer" instead of relying on asymptotic theory).
- **The psychometric function** is the worked vehicle (Wichmann & Hill) but is
  explicitly only a *descriptive* model — do not get lost in its details.

## Local relevance

Step 3 of [[The Three-Step Recipe for Modeling Data]]. The bootstrap is reused
by Butz for parameter confidences and the **model-recovery procedure** in
[[VL07 Interpreting Modeling]] and for the $G^2$-distribution bootstrap in
[[VL08 Model Comparison Example]]. The "error bars on spatial-vision parameters"
are flagged as still-in-progress work in [[VL06 Modeling Visual Cognition]].

## Exam or project relevance

Very high. Be able to: say why variability estimates are essential and why they
are usually analytically intractable; describe how the bootstrap works;
distinguish non-parametric from parametric bootstrap and say when each is
appropriate; explain the bootstrap bridging assumption and why/when it must be
tested; and classify the CI-width dependencies as features vs bugs.

## Links to global concepts

- [[The Bootstrap]] (global)

## Open questions

- Wichmann & Hill Figure 1 (bridging assumption) and Figure 6 (parametric
  bootstrap failure) are key visuals; not yet extracted.
