---
type: method
status: active
scope: global
classes: [Cognitive Modeling]
projects:
domains: [statistics, modeling, machine learning]
sources:
created: 2026-06-17
updated: 2026-06-17
---

# Least-Squares Estimation

## Short definition

Least-squares estimation finds the parameters that make a model's predictions as
close as possible to the data by minimising the sum of squared vertical distances
(residuals) between data points and the model.

## General explanation

A **discrepancy (cost, error, objective) function** condenses the mismatch
between model and data into one number, so that fitting becomes minimisation.
Least squares is the most intuitive choice: it minimises how far the predictions
sit from the observations. Crucially the discrepancy is measured **vertically**,
at the same value of the independent variable — a point can look visually close
to the curve yet have a large residual, because what counts is the vertical gap
at that $x$, not the shortest distance to the curve.

Several named quantities all rest on the squared residuals — sum of squared
errors (SSE), mean squared error (MSE), and root mean squared deviation
(RMSD/RMSE). They differ only by dividing by $n$ and/or a square root, so **they
are all minimised by the same parameters**; RMSD is usually *reported* because it
is in the data's units. Two non-squared cousins are the mean error (ME), which
reveals systematic **bias** (over/under-prediction), and the mean absolute error
(MAE).

Why squared rather than absolute or signed deviations? (1) The squared error is
smooth and differentiable everywhere, which makes optimisation convenient (you
can take derivatives, and the surface has no kinks). (2) Squaring penalises large
residuals disproportionately, so the fit cannot be "good on average" while badly
missing a few points. Signed deviations would be useless as a criterion because
positive and negative misses cancel.

For models that are **linear in the parameters**, least squares has a unique
closed-form solution (the normal equations / linear regression). For nonlinear
models it becomes a [[Numerical Optimisation]] problem. A key conceptual
limitation: plain least squares has **no built-in statistical properties** —
on its own it gives no significance test, no principled model comparison, and no
confidence intervals. When those guarantees matter you turn to
[[Maximum Likelihood Estimation]] (least squares is in fact the MLE under
independent Gaussian noise of constant variance).

## Intuition

Imagine the model as a curve and your data as dots scattered around it. For each
dot, drop a vertical line to the curve — that gap is the *residual*. Least
squares slides and bends the curve (by tuning its parameters) until the *total
squared gap* is as small as possible. Squaring means a few big misses hurt much
more than many tiny ones, so the fit is pulled hard toward the worst-fitting
points.

## Formal definition

$$\Delta_i=y_i-f(x_i,\theta),\qquad \mathrm{SSE}=\sum_{i=1}^n\Delta_i^2,\qquad
\mathrm{MSE}=\tfrac1n\sum_{i=1}^n\Delta_i^2,\qquad \mathrm{RMSD}=\sqrt{\mathrm{MSE}}.$$

Symbols: $y_i$ observed value at the $i$-th $x$; $f(x_i,\theta)$ model
prediction; $\theta$ parameter vector; $n$ number of points. The estimate is
$\hat\theta=\arg\min_\theta \mathrm{SSE}(\theta)$.

## Worked example

Fit a power function of forgetting $f(t)=a\,(bt+1)^{-c}$ to retention data. With
best-fitting parameters you obtain residuals at each interval, say
$-0.02, 0.03, -0.01, 0.04$. Then
$\mathrm{SSE}=(-0.02)^2+0.03^2+(-0.01)^2+0.04^2=0.0030$ and
$\mathrm{RMSD}=\sqrt{0.0030/4}\approx0.027$. Switching to MSE or SSE changes the
*number* but not the *parameters* that minimise it — and 0.027 alone does not
tell you whether the model is adequate; that needs a goodness-of-fit judgement.

## Why it matters

Least squares is the most widely used estimation principle in science: the basis
of linear regression, curve fitting, and a default objective across statistics
and machine learning. It is simple, assumption-light, and the natural first tool
for a descriptive fit.

## Used in

- [[Least-Squares Estimation in Cognitive Modeling]] (the simpler of two
  estimation philosophies; SSE/MSE/RMSD; why it lacks statistical properties)
- [[Numerical Optimisation]] (how the minimum is found for nonlinear models)

## Related concepts

- [[Maximum Likelihood Estimation]]
- [[Numerical Optimisation]]
- [[Overfitting and the Bias-Variance Trade-off]]

## Common confusions

- **"The residual is the shortest distance to the curve."** No — it is the
  *vertical* distance at the same $x$.
- **"RMSD tells me if the model is good."** No — it is unitful and uncalibrated;
  adequacy needs a goodness-of-fit test.
- **SSE vs MSE vs RMSD give different fits.** They give the same $\hat\theta$;
  only the reported number differs.

## Sources

- Farrell & Lewandowsky, *Computational Modeling of Cognition and Behavior*;
  standard regression texts.
