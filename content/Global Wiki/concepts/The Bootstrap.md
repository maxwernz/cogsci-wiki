---
type: method
status: active
scope: global
classes: [Cognitive Modeling, Data Literacy, Neural Coding]
projects:
domains: [statistics, resampling, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_04_CIs.pdf
created: 2026-06-09
updated: 2026-06-09
---

# The Bootstrap

## Short definition

The bootstrap estimates the sampling variability of a statistic by repeatedly
resampling — from the data or from a fitted model — and recomputing the statistic
each time, using only the single sample you actually have.

## General explanation

A point estimate carries no information about how much it would vary on
replication. The bootstrap (Efron, 1979) builds an approximate sampling
distribution from one sample, and belongs to the **resampling / Monte Carlo**
family (with the jackknife and permutation tests). Two variants:

- **Non-parametric bootstrap:** draw, with replacement, new datasets of the same
  size $N$ from the observed data, recompute the statistic, repeat ~1,000–10,000
  times. The sample stands in for the population. Answers: *how much would my
  estimate vary across fresh data samples?*
- **Parametric bootstrap:** simulate datasets from a *fitted model* (using
  $\hat\theta$), refit each, and look at the spread of refit estimates. Answers:
  *if this model were true, how variable would the refit parameters be?*

Confidence intervals come from the bootstrap distribution: the **percentile**
method uses its quantiles directly; **BCa** corrects for bias and skewness. A
caveat for the parametric bootstrap is the **bridging assumption** — it treats
$\hat\theta$ as if it were the true parameter, which should be checked by
sensitivity analysis across nearby generating values.

## Intuition

You only ran the study once, so you can't see how the result would jitter on
repetition. The bootstrap fakes repetition by re-drawing from your one sample
(treating it as the population), and the jitter across those re-draws estimates
the real jitter — pulling a sampling distribution out of a single dataset.

## Formal definition

Parametric bootstrap variance of an estimator $\hat\theta$:

$$\widehat{\mathrm{Var}}(\hat\theta)\approx\frac{1}{T-1}\sum_{k=1}^{T}\big(\hat\theta^{b}_k-\bar{\hat\theta^{b}}\big)^2,\quad y^{b}_k\sim f(x;\hat\theta),\ \hat\theta^{b}_k=\text{fit}(y^{b}_k).$$

- $T$: number of bootstrap samples; $y^{b}_k$: $k$-th simulated dataset (size
  $N$); $\hat\theta^{b}_k$: refit estimate.

## Worked example

For a mean: from a size-6 sample, draw 6 with replacement, take the mean, repeat
10,000 times; the histogram's 2.5/97.5 percentiles give a 95% CI. For a model
parameter: fit, simulate many datasets from the fit, refit each, and the scatter
of refit parameters gives the confidence region.

## Why it matters

The bootstrap provides error bars and confidence intervals when analytic formulas
are unavailable — which is the common case for realistic models in cognitive
science, neuroscience and applied statistics.

## Used in

- [[The Bootstrap]] (Cognitive Modeling, VL4)
- [[VL07 Interpreting Modeling]] (parameter confidences, model recovery)
- [[VL08 Model Comparison Example]] ($G^2$ distribution)

## Related concepts

- [[Maximum Likelihood Estimation]]
- [[Bayesian Inference]] (posterior/credible intervals as the alternative)

## Common confusions

- The bootstrap creates no new information; it re-uses one sample to estimate
  variability.
- Non-parametric resamples the *data*; parametric resamples from the *fitted
  model*.
- Percentile CIs can be biased/skewed (use BCa); parametric CIs rely on the
  bridging assumption.

## Sources

- [[VL04 Assessing variability]]
- [[Wichmann and Hill (2001b)]]
