---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, modeling, machine learning]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
  - Classes/Cognitive Modeling/raw/Computational Modeling of Cognition and Behavior/10.1_pp_241_272_Model_Comparison.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Cross-Validation and Regularisation

## Short definition

Two simulation/optimisation-based ways to fight over-fitting: cross-validation
*evaluates* models by testing them on data they were not fit to; regularisation
*changes the fitting* by adding a complexity penalty to the objective.

## Intuition

Both ask the same question as AIC/BIC — "is this extra complexity worth it?" —
but answer it empirically. Cross-validation hides part of your data, fits on the
rest, and checks how well the model predicts the hidden part: an over-fit model
aces the data it saw but flunks the hidden data. Regularisation instead leans on
the fit from the start, adding a "complexity tax" so the optimiser is reluctant
to use large/many parameters unless the data really demand it.

## Explanation

### Cross-validation (CV)

CV estimates a model's **prediction error** on unseen data. The simplest version
fits on a training set and evaluates on a separate test set; but holding out a
fixed test set wastes data. CV reuses data more efficiently:

- **Leave-one-out (LOO):** each data point is left out in turn, the model is fit
  to the other $n-1$, and tested on the held-out point.
- **K-fold:** split the data into $K$ folds; each fold serves once as the test
  set while the other $K-1$ folds train. Hastie et al. (2009) show K-fold gives
  a reasonable estimate of the expected prediction error across training sets.

CV trades fit against complexity *automatically*: an over-fit model has low
training error but high test error, so picking the model with the lowest
*test/validation* error lands on the sweet-spot complexity. Its strengths: it is
pragmatic, hugely successful in machine learning, and **works with least-squares
methods** (so even LSE, which lacks statistical properties, can be used for model
selection via CV). Its weaknesses: there are usually **no proofs** that it works,
and many choices are unprincipled — 2-fold vs 5-fold vs 10-fold, what to do when
different $K$ disagree, or when models predict almost equally well. A
**generalization** variant (Butz, VL7) splits the data *systematically* rather
than randomly to test interpolation/extrapolation.

### Regularisation

Regularisation adds a penalty for complexity *inside* the objective function, so
it does not merely evaluate models — it **changes how the model is fit**:

$$\text{Error} = \text{GoF} + \lambda\lVert\alpha\rVert_p.$$

The penalty is the (weighted) **norm** of the parameter vector: the more
parameters, and the larger their values, the bigger the penalty. Common choices:
the **L2 / Euclidean** norm ($p=2$), giving **ridge regression**, and the
**L1 / taxicab** norm ($p=1$), giving **lasso regression** (which can drive
coefficients exactly to zero). Regularisation **increases bias but decreases
variance**, yielding simpler, more stable models; for an appropriately chosen
$\lambda$ the *total* error is lower.

The strength $\lambda$ is a **hyperparameter**: large $\lambda$ → heavy penalty
(useful when data are scarce). Choosing $\lambda$ well is itself a model-selection
problem, solved by CV. To both *tune* $\lambda$ and *honestly assess* the final
model you need **nested cross-validation**: an inner loop picks $\lambda$ (and the
parameters) on training+validation data, and an independent outer loop estimates
generalisation error on a held-out test set. This needs a three-way split
(train/validation/test) and is computationally expensive.

### How they relate

CV is **discrete** — it can only rank the models you actually have — and it
*evaluates*, never modifies, them. Regularisation offers **smooth, continuous**
control of effective complexity via $\lambda$, stabilises solutions by penalising
parameter *magnitude* (not just count, unlike AIC/BIC), and *changes* the fit. The
two are complementary: regularisation reshapes the model; CV picks its
hyperparameter and judges the result. Regularisation is also closely related to a
**Bayesian prior** ([[Bayesian Inference in Cognitive Modeling]]): the penalty
$\lambda R(f)$ plays the role of a prior that disfavours complex models — the key
difference being that in regularisation the fit–complexity trade-off is tuned by
$\lambda$ via CV rather than fixed by a prior.

## Worked example

Bishop's $M=9$ polynomial over-fits 10 noisy points. Adding an L2 penalty
$\lambda\lVert\alpha\rVert^2$ and choosing $\ln\lambda$ by cross-validation tames
the oscillations *without* lowering the polynomial order: the coefficients shrink,
bias rises slightly, variance drops sharply, and out-of-sample error improves.
The right $\lambda$ is found by trying several values and keeping the one with the
best validation error.

## Formal definition / equations

Regularised objective and the $L_p$ norm:

$$E(\alpha) = \underbrace{\sum_{i=1}^{N}\{y_i - f(x_i,\alpha)\}^2}_{\text{goodness-of-fit}} + \lambda\lVert\alpha\rVert_p,\qquad \lVert\alpha\rVert_p = \Big(\sum_{i=1}^{N}|\alpha_i|^p\Big)^{1/p}.$$

- $\lambda\ge 0$: regularisation strength (hyperparameter, tuned by CV); $p=2$ →
  ridge, $p=1$ → lasso; larger $\lambda$ → smaller coefficients → simpler model.

## Role in this class or project

The empirical, simulation-based half of step 2 ([[VL03 Goodness-of-fit]]),
complementing the analytic AIC/BIC criteria. Cross-validation/generalization is
the comparison method Butz applies in [[VL07 Interpreting Modeling]] and
[[VL08 Model Comparison Example]].

## Exam, assignment, or project relevance

Explain how CV trades off fit vs complexity; describe LOO and K-fold; list
advantages of CV over AIC/BIC/MDL/NML (works with LSE, pragmatic, makes few
assumptions) and its problems (no proofs, arbitrary $K$); write the regularised
objective; distinguish ridge (L2) from lasso (L1); explain why $\lambda$ needs
(nested) CV; and state how CV and regularisation differ (evaluate vs modify;
discrete vs continuous).

## Related global concepts

- [[Cross-Validation]]
- [[Regularisation]]
- [[Overfitting and the Bias-Variance Trade-off]]

## Related local pages

- [[Goodness-of-Fit and Overfitting]]
- [[Model Selection Criteria (Deviance, AIC, BIC)]]
- [[Bayesian Inference in Cognitive Modeling]]

## Common confusions

- **"Cross-validation changes the model."** No — it only *evaluates*;
  regularisation changes the fit.
- **"Regularisation just removes parameters."** It shrinks parameter *magnitudes*
  (L1 can zero some out); it penalises size, not just count.
- **"You can tune $\lambda$ and report its CV error as generalisation."** That
  double-uses data; you need *nested* CV with a separate outer test set.

## Sources

- [[VL03 Goodness-of-fit]]
- [[Farrell and Lewandowsky Chap 10]] (user note)
- [[Bishop 2006 Pattern Recognition and Machine Learning]]
- [[Hastie et al 2009 Elements of Statistical Learning]]
