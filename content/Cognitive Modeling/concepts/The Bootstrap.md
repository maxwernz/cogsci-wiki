---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, resampling, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_04_CIs.pdf
  - Classes/Cognitive Modeling/raw/Computational Modeling of Cognition and Behavior/09.1_pp_47_71_Basic_Parameter_Estimation_Techniques.pdf
created: 2026-06-09
updated: 2026-06-09
---

# The Bootstrap

## Short definition

The bootstrap estimates the variability of a fitted statistic (e.g. a model
parameter) by repeatedly resampling — either the data, or the fitted model — and
re-computing the statistic each time, building up its sampling distribution from a
single dataset.

## Intuition

You only ran the experiment once, so you have one estimate and no idea how much it
would wobble if you ran it again. The bootstrap fakes "running it again" by
treating your one sample as a stand-in for the whole population and drawing new
pretend-samples from it. The spread of estimates across those pretend-samples
approximates how much your real estimate would vary across real replications. As
Münchhausen pulled himself out of the swamp by his own hair, you "pull" a sampling
distribution out of a single sample.

## Explanation

Point estimates from least squares or ML give a best guess but **no error bars**.
Error bars matter for two reasons (VL4): to judge whether parameters truly differ
across conditions (is a numerical difference statistically meaningful?), and to
detect when the data **fail to constrain** a parameter (a very wide interval means
too little/wrong data or the wrong model). Analytic variability formulas are
usually unavailable for realistic cognitive models, so we resample.

The bootstrap (Efron, 1979) belongs to the **resampling / Monte Carlo** family
(alongside the jackknife and permutation tests). These avoid asymptotic
mathematics by simulating the answer to "what would happen if we sampled many
times under the same conditions?". There are two flavours:

**Non-parametric bootstrap.** Resample *the data*: draw, with replacement, a new
dataset of the same size $N$ from the observed data points, refit, and repeat
~1,000–10,000 times. The empirical sample is the "population"; sampling with
replacement mimics drawing fresh samples from that population. It answers: *if I
got new samples of data, how much would my fits vary?* Use it when you do **not**
want to lean on a parametric model's assumptions, or want a model-agnostic sense
of data variability.

**Parametric bootstrap.** Resample *from the fitted model*: using $\hat\theta$,
simulate $T$ synthetic datasets (each of size $N$) from the model's probabilities
$p=f(x;\hat\theta)$, refit each, and look at the spread of the resulting
$\hat\theta^{b}_{1},\dots,\hat\theta^{b}_{T}$ (Figure 3.6). It answers: *if this
were the true model, what data would we expect, and how variable would the
re-fitted parameters be?* Use it to put confidence limits on model parameters
when you are willing to trust the model's form.

**Confidence intervals** are read off the bootstrap distribution: the
**percentile method** uses its percentiles directly (e.g. the 2.5th and 97.5th
for a 95% CI); the **BCa method** adjusts those percentiles to correct for bias
and skewness.

**Subtleties (Wichmann & Hill, 2001b).** The parametric bootstrap rests on a
**bridging assumption**: it resamples from $\hat\theta$ *as if* the estimate were
the true generating parameter. This "bridge" from estimate to truth should be
*tested* — via a sensitivity analysis that regenerates the bootstrap from several
nearby generating parameters — because if the CI changes a lot across plausible
truths, the bootstrap CI is unreliable. The paper also classifies what the CI
width depends on into **features** (legitimate, expected dependencies: the sample
points $x$, the number of observations $N$, the sampling scheme $s$) and **bugs**
(problematic dependencies: sensitivity to the non-essential distribution function
$F$, and sensitivity to initial conditions of the fit).

## Worked example

Non-parametric, for a mean: from a sample of 6 values, draw 6 with replacement
(so some repeat, some drop out), compute the mean; repeat 10,000 times; the
histogram of those means estimates the sampling distribution of the mean, and its
2.5/97.5 percentiles give a 95% CI. Parametric, for a model parameter: fit a
psychometric function to get $\hat\theta$, simulate 2,000 datasets from it, refit
each, and the scatter of the 2,000 re-estimated parameter pairs (Wichmann & Hill
Fig. 1) gives the confidence region — whose width depends sensibly on $N$ and the
sampling scheme.

## Formal definition / equations

Parametric bootstrap (per Figure 3.6): fit to data $y$ to get $\hat\theta$;
generate $y^{b}_{k}\sim f(x;\hat\theta)$ for $k=1,\dots,T$ (each of size $N$);
refit to get $\hat\theta^{b}_{k}$; then

$$\widehat{\mathrm{Var}}(\hat\theta) \approx \frac{1}{T-1}\sum_{k=1}^{T}\big(\hat\theta^{b}_{k}-\bar{\hat\theta^{b}}\big)^2.$$

- $\hat\theta$: parameters fit to the real data; $y^{b}_{k}$: $k$-th simulated
  dataset; $\hat\theta^{b}_{k}$: parameters refit to it; $T$: number of bootstrap
  samples; $N$: size of each (= original $N$).

## Role in this class or project

Step 3 of the recipe ([[VL04 Assessing variability]]). Reused for parameter
confidences and the model-recovery procedure in [[VL07 Interpreting Modeling]],
and to bootstrap the $G^2$ distribution for significance tests in [[VL08 Model Comparison Example]].

## Exam, assignment, or project relevance

Very high. Explain why variability estimates are needed and why analytic ones are
usually impossible; describe how the bootstrap works; contrast non-parametric vs
parametric and say when to use each; explain the bridging assumption and why/when
it must be tested; and classify CI-width dependencies as features vs bugs.

## Related global concepts

- [[The Bootstrap]]
- [[Maximum Likelihood Estimation]]

## Related local pages

- [[The Three-Step Recipe for Modeling Data]]
- [[Maximum Likelihood Estimation in Cognitive Modeling]]
- [[Model Interpretation: Necessity and Sufficiency]]

## Common confusions

- **"Bootstrapping creates new information."** It cannot — it only re-uses the
  one sample to estimate variability; it is "an approximate answer to the right
  question" (Tukey), not magic.
- **Non-parametric vs parametric.** Non-parametric resamples the *data*;
  parametric resamples from the *fitted model*.
- **"Percentile CIs are always fine."** They can be biased/skewed; BCa corrects
  for that, and the bridging assumption must hold for parametric CIs.

## Sources

- [[VL04 Assessing variability]]
- [[Wichmann and Hill (2001b)]] (user note)
- [[VL4 Assessing variability]] (user note)
