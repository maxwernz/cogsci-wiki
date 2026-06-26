---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_02_RMSD-ML.pdf
  - Classes/Cognitive Modeling/raw/Computational Modeling of Cognition and Behavior/09.1_pp_47_71_Basic_Parameter_Estimation_Techniques.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Least-Squares Estimation in Cognitive Modeling

## Short definition

Least-squares estimation finds the parameters that make a model's predictions as
close as possible to the data, by minimising the sum of squared vertical
distances (residuals) between data points and the model curve.

## Intuition

Imagine the model as a curve and your data as dots scattered around it. For each
dot, drop a vertical line to the curve — that gap is the *residual*. Least
squares slides and bends the curve (by tuning its parameters) until the *total
squared gap* is as small as possible. Squaring means a few big misses hurt much
more than many tiny ones, so the fit is pulled hard toward the worst-fitting
points.

## Explanation

A **discrepancy function** (also called error, cost, or objective function)
condenses the mismatch between model and data into one number, so that fitting
becomes minimisation. Least squares is the most intuitive choice: it literally
minimises how far the predictions sit from the observations.

Crucially, the discrepancy is measured **vertically**, at the same value of the
independent variable. A data point can look visually close to the curve and yet
have a large residual, because what counts is the vertical gap at that x-value,
not the shortest distance to the curve.

Three named quantities all rest on the squared residuals — sum of squared errors
(SSE), mean squared error (MSE), and root mean squared deviation (RMSD/RMSE).
They differ only by dividing by $n$ and/or taking a square root, so **they are
all minimised by the same parameters**. RMSD is usually *reported* because it is
in the same units as the data. Two non-squared cousins exist: the mean error
(ME), which can reveal systematic **bias** (over- or under-prediction), and the
mean absolute error (MAE).

Why squared rather than absolute or signed deviations? Two reasons. (1) The
squared error is smooth and differentiable everywhere, which makes the
optimisation mathematically convenient (you can take derivatives and the surface
has no kinks). (2) Squaring penalises large residuals disproportionately, so the
fit cannot be "good on average" while badly missing a few points. The signed ME
would be useless as a fit criterion because positive and negative misses cancel.

The decisive limitation: **least squares has no known statistical properties.**
You cannot say whether a given RMSD is "good" or "bad" (is 0.026 chance-level or
damning?), you cannot make a *statistical* comparison between two models'
fits, and the parameter estimates come with no confidence intervals and no way
to predict how a replication would turn out. Whenever those statistical
guarantees matter, you need [[Maximum Likelihood Estimation in Cognitive Modeling]] instead. Least squares remains useful as a simple *descriptive*
summary and requires no (or minimal) distributional assumptions.

## Worked example

Suppose you fit a power function of forgetting, $f(t)=a\,(b t + 1)^{-c}$, to
retention data (Farrell & Lewandowsky's Carpenter et al. example). With
best-fitting $a=0.95, b=0.13, c=0.58$ you get residuals $\Delta_i$ at each
retention interval. If the residuals are, say, $-0.02, 0.03, -0.01, 0.04$, then

$$\mathrm{SSE}=(-0.02)^2+0.03^2+(-0.01)^2+0.04^2 = 0.0030,\quad \mathrm{RMSD}=\sqrt{0.0030/4}\approx 0.027.$$

Switching to MSE or SSE would change the *number* but not the *parameters* that
minimise it. Note you cannot tell from 0.027 alone whether the model is adequate
— that judgement needs the goodness-of-fit machinery of VL3.

## Formal definition / equations

Residual, SSE, MSE, RMSD:

$$\Delta_i = y_i - f(x_i,\theta),\qquad \mathrm{SSE}=\sum_{i=1}^{n}\Delta_i^2,\qquad \mathrm{MSE}=\frac1n\sum_{i=1}^{n}\Delta_i^2,\qquad \mathrm{RMSD}=\sqrt{\mathrm{MSE}}.$$

- $y_i$: observed value at the $i$-th x; $f(x_i,\theta)$: model prediction;
  $\theta$: parameter vector; $n$: number of points. We choose $\hat\theta =
  \arg\min_\theta \mathrm{SSE}(\theta)$.

## Role in this class or project

Step 1 of the modeling recipe in [[VL02 RMSD and ML]] and the simpler of the two
estimation philosophies. It reappears wherever a quick descriptive fit is enough
and statistical inference is not needed (e.g. the qualitative/RMSD fits in
[[VL06 Modeling Visual Cognition]]).

## Exam, assignment, or project relevance

Define a discrepancy function; explain why SSE/MSE/RMSD share the same optimum;
justify squaring over absolute/signed deviations; and explain *why* least squares
lacks statistical properties (no GoF test, no model comparison, no CIs). There
are analytic pen-and-paper exercises on LMSE.

## Related global concepts

- [[Least-Squares Estimation]] (general method)
- [[Maximum Likelihood Estimation]]
- [[Overfitting and the Bias-Variance Trade-off]]

## Related local pages

- [[Maximum Likelihood Estimation in Cognitive Modeling]]
- [[Numerical Optimisation for Model Fitting]]
- [[The Three-Step Recipe for Modeling Data]]

## Common confusions

- **"The residual is the shortest distance to the curve."** No — it is the
  *vertical* distance at the same x-value.
- **"RMSD tells me if the model is good."** No — it is unitful and uncalibrated;
  you cannot judge adequacy without a goodness-of-fit test.
- **SSE vs MSE vs RMSD give different fits.** They give the same $\hat\theta$;
  only the reported number differs.

## Sources

- [[VL02 RMSD and ML]]
- [[Farrell and Lewandowsky Chap 3.1-3.6 + Chap 4]] (user note)
