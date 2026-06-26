---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: lecture_slides
raw_path: Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
created: 2026-06-09
updated: 2026-06-09
---

# VL03 — Goodness-of-fit

> Reading (from [[ReadingList-VL2-5.pdf|reading list]]): Farrell & Lewandowsky (2018),
> chapter 10 (skip the KL-distance maths, pp. 256–258). Supplementary:
> StatQuest "Cross Validation" video; Hastie et al. (2009) §7.10 (optional,
> "beyond this course" — see [[Hastie et al 2009 Elements of Statistical Learning]]);
> the regularisation example is from Bishop (2006) §1.1
> ([[Bishop 2006 Pattern Recognition and Machine Learning]]). User note:
> [[Farrell and Lewandowsky Chap 10]].

## Summary

Step two of the recipe: once we can *measure* discrepancy (VL2), how do we
*evaluate* it? The lecture's core lesson is that **goodness-of-fit alone cannot
prevent over-fitting**. A more complex (more flexible) model will always fit the
training data better — but in doing so it fits *noise* as well as *signal*, and
so predicts new data worse. The lecture builds the conceptual machinery for
trading fit against complexity: the **bias–variance trade-off**, the distinction
between **fit (past data) and prediction (future data)**, **deviance** and the
**likelihood-ratio test**, the penalty-based criteria **AIC** and **BIC**, and
the simulation-based alternatives **cross-validation** and **regularisation**.
It closes with two structural model properties: **identifiability** and
**testability**.

## Key points

- **Goodness-of-fit vs over-fitting.** GoF is a discrepancy measure (smaller =
  better). Over-fitting is using a model so flexible it "chases" noise. A
  *worse* fit can be a *better* model if it captures the generating process and
  ignores the noise.
- **Three drivers of model complexity/flexibility:** (1) number of free
  parameters, (2) functional form, (3) extension of the parameter space (the
  bounds). Counting parameters alone does not capture complexity.
- **Bias–variance trade-off.** Simple models → high bias (systematic
  mis-prediction), low variance. Complex models → low bias, high variance (fits
  swing wildly across noisy samples). Total error is minimised at the complexity
  matching the *true* generating process.
- **Fit vs prediction.** Training error decreases monotonically with complexity;
  test (out-of-sample) error first falls then rises — the U-shape that defines
  the sweet spot.
- **Deviance** solves the problem that raw (log-)likelihood values are
  meaningless (they depend on $n$ and on the distribution): it scales your
  model's likelihood against the *saturated* model (a perfect-fit model with one
  parameter per data point).
- **Penalised criteria.** AIC and BIC add a complexity penalty to $-2\ln L$;
  BIC's penalty grows with $\ln n$, so it punishes complexity harder for large
  samples. MDL and NML go further by accounting for functional form.
- **Cross-validation** estimates prediction error by holding out data; it
  *evaluates* models. **Regularisation** adds a complexity penalty *inside* the
  fitting and *changes* how the model is fit.
- **Identifiability vs testability** are properties of the model *before* you
  trust any fit (see [[Parameter Identifiability and Model Testability]]).

## Equations or formal definitions

**Deviance** (scaled log-likelihood ratio against the saturated model):

$$D = 2\ln\!\left(\frac{L(\theta_{\max}; y)}{L(\hat\theta; y)}\right) = 2\big(\ell(\theta_{\max}; y) - \ell(\hat\theta; y)\big)$$

- $\hat\theta$: your fitted parameters; $\theta_{\max}$: the saturated model
  (perfect fit, one free parameter per data point). $D$ asymptotically follows a
  $\chi^2$ distribution with $n-K$ degrees of freedom ($K$ = free parameters).
  For **nested** models, the *difference* in $D$ is $\chi^2$ with df = the
  difference in number of parameters — this is the **likelihood-ratio test**.

**AIC and BIC:**

$$\mathrm{AIC} = -2\ln L(\hat\theta; y) + 2K, \qquad \mathrm{BIC} = -2\ln L(\hat\theta; y) + K\ln(n)$$

- $-2\ln L$ rewards fit (smaller is better); $+2K$ or $+K\ln n$ penalises
  complexity. Lower AIC/BIC = preferred model. AIC estimates Kullback–Leibler
  distance; BIC approximates the model with highest posterior probability.

**Regularisation** (add the weighted norm of the parameters to the error):

$$\text{Error} = \text{GoF} + \lambda\lVert\alpha\rVert_p, \qquad \lVert\alpha\rVert_p = \Big(\sum_{i=1}^{N}|\alpha_i|^p\Big)^{1/p}$$

- $\lambda$ controls the strength of the penalty (a *hyperparameter*, tuned by
  cross-validation). $p=2$ → L2/ridge; $p=1$ → L1/lasso. Larger $\lambda$ → more
  bias, less variance.

## Methods, models, or theories

- **Likelihood-ratio test** for nested models (deviance difference, $\chi^2$).
- **AIC / BIC / MDL / NML** — penalty-based selection (see [[Model Selection Criteria (Deviance, AIC, BIC)]]).
- **Cross-validation** (LOO, K-fold) and **regularisation** (ridge/lasso, with
  nested CV to set $\lambda$) — see [[Cross-Validation and Regularisation]].
- **Bishop's polynomial curve-fitting** worked example (orders M=0,1,3,9;
  RMS train vs test; "more data helps"; regularisation with $\ln\lambda$) —
  from [[Bishop 2006 Pattern Recognition and Machine Learning]].

## Local relevance

Step 2 of [[The Three-Step Recipe for Modeling Data]]. Deviance/AIC/BIC reappear
as the $G^2$ statistic and BIC comparison in [[VL08 Model Comparison Example]];
identifiability/testability is revisited by Butz with the Jacobian-rank
treatment in [[VL07 Interpreting Modeling]].

## Exam or project relevance

Very high. Be able to: explain why GoF cannot prevent over-fitting; state the
three complexity drivers; explain bias–variance and *why the trade-off plot is
impossible in practice* (you'd need to know the true model); define the
saturated model and compute deviance; write and interpret AIC and BIC; explain
how CV and regularisation trade off fit vs complexity and how they differ; and
give examples of non-identifiable and non-testable models.

## Links to global concepts

- [[Overfitting and the Bias-Variance Trade-off]] (global)
- [[Model Selection: AIC and BIC]] (global)
- [[Cross-Validation]] (global)
- [[Regularisation]] (global)

## Open questions

- Bias–variance figures (10.3–10.5) and Bishop's polynomial figures are
  high-value; user already holds Bias-Variance and Training-Error PNGs in
  [[Farrell and Lewandowsky Chap 10]].
