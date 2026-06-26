---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: lecture_slides
raw_path: Classes/Cognitive Modeling/raw/Slides/VLCogMod_02_RMSD-ML.pdf
created: 2026-06-09
updated: 2026-06-09
---

# VL02 — RMSD and ML

> Reading (from [[ReadingList-VL2-5.pdf|reading list]]): Farrell & Lewandowsky (2018),
> chapter 3 §3.1–3.4 and §3.6, and all of chapter 4. See the user note
> [[Farrell and Lewandowsky Chap 3.1-3.6 + Chap 4]].

## Summary

This is the first of three lectures on the *fundamentals of fitting a model to
data*. It answers step one of the modeling recipe: **how do we measure the
discrepancy between a model and the data?** Two discrepancy ("error", "cost",
"objective") functions dominate: **least-squares** (SSE/MSE/RMSD) and
**maximum likelihood (ML)**. Least squares is intuitive but statistically
"blind"; ML rests on a probabilistic model and so unlocks goodness-of-fit tests,
model comparison, and confidence intervals (the topics of VL3–VL4). The lecture
also covers *how* the best parameters are found in practice — numerical
optimisation (simplex, simulated annealing) — and the key statistical properties
of the ML estimator (sufficiency, consistency, (a)bias, parameterisation
invariance).

A recurring framing comes from George Box: models are "wrong but useful"
approximations; we never claim the normal distribution or a straight line is
*true*, only that it gives results matching reality "to a useful approximation".

## Key points

- **Discrepancy function.** Parameter estimation reframes "maximise agreement
  between model and data" as "minimise a single number, the discrepancy"
  (Farrell & Lewandowsky, 2018, p. 47). The discrepancy Δ is measured
  *vertically* (at the same x-value): a point can look visually close to the
  curve yet have a large vertical residual.
- **Least squares.** Residual $\Delta_i = y_i - f(x_i,\theta)$. SSE, MSE and
  RMSD all minimise the *same* squared residuals and therefore return the
  *identical* optimal parameters $\hat\theta$. ME and MAE are alternatives.
- **Why squared, not absolute/signed?** Squaring is differentiable everywhere
  (analytically convenient) and penalises large residuals more heavily; the
  signed mean error (ME) would let positive and negative misses cancel.
- **Least squares is statistically blind.** It has no known statistical
  properties: you cannot say whether an RMSD of 0.026 is "good" or "bad",
  cannot statistically compare two models, and get no confidence intervals.
- **Maximum likelihood needs a probabilistic model.** Unlike LSE, MLE assumes
  the data come from a specific probability distribution; you then pick the
  parameters that make the observed data most probable.
- **Probability vs likelihood** — the central conceptual shift: probability
  fixes the parameters and varies the data (and integrates to 1); likelihood
  fixes the data and varies the parameters (and does *not* integrate to 1).
- **Estimator properties:** the ML estimator is *minimally sufficient* (captures
  all information the sample carries about θ), *asymptotically consistent*
  (converges to the truth as n→∞), invariant to reparameterisation, but *not
  necessarily unbiased* for finite samples.

## Methods, models, or theories

**Numerical optimisation.** Optimal parameters usually cannot be found
analytically and must be located numerically. Farrell & Lewandowsky discuss the
**simplex** (Nelder–Mead, §3.4.1) and **simulated annealing** (§3.4.2). The key
hazard is **local minima**: a greedy downhill method (simplex) can settle in a
shallow valley that is not the global optimum. Simulated annealing accepts
occasional *uphill* moves (with a probability set by a falling "temperature"), so
it can escape local minima. See [[Numerical Optimisation for Model Fitting]].

**The two estimation philosophies** are detailed in
[[Least-Squares Estimation in Cognitive Modeling]] and
[[Maximum Likelihood Estimation in Cognitive Modeling]].

## Equations or formal definitions

Residual and sum of squared errors:

$$\Delta_i = y_i - f(x_i,\theta), \qquad \mathrm{SSE} = \sum_{i=1}^{n}\Delta_i^2 = \sum_{i=1}^{n}\big[y_i - f(x_i,\theta)\big]^2$$

Root mean squared deviation (the reported "error bar" on fit quality):

$$\mathrm{RMSD} = \sqrt{\frac{1}{n}\sum_{i=1}^{n}\Delta_i^2}$$

- $y_i$: observed value at the $i$-th x-value; $f(x_i,\theta)$: model prediction
  there; $\theta$: the parameter vector; $n$: number of data points.
- In words: SSE adds up the squared vertical misses; MSE averages them; RMSD
  takes the square root to return to the units of $y$. All three are minimised
  by the same $\hat\theta$.

The likelihood of parameters given data, for independent observations:

$$L(\theta; x) = \prod_{i=1}^{n} f(x_i,\theta), \qquad \ell(\theta;x) = \sum_{i=1}^{n}\ln f(x_i,\theta)$$

- We maximise $\ell$ (the log-likelihood) for numerical stability. Note the
  shift of viewpoint: here $x$ is fixed (the observed data) and $\theta$ varies.

## Local relevance

This lecture is step 1 of the three-step recipe ([[The Three-Step Recipe for Modeling Data]]). RMSD vs ML returns in VL6 (the spatial-vision model is fit by
ML on a $d'$ probabilistic model) and is the foundation for VL3's deviance/AIC
(which are built from the log-likelihood) and VL8's $G^2$ statistic.

## Exam or project relevance

Highly exam-relevant (Wichmann: "only the material covered in the lectures is
relevant for the exam" for VL2–4). Be ready to: define a discrepancy function;
explain why SSE/MSE/RMSD give the same fit; argue why least squares lacks
statistical properties; explain the probability-vs-likelihood distinction
(Figure 4.5); state and motivate sufficiency, consistency, bias and
parameterisation invariance; and explain local minima and why simulated
annealing escapes them. There are pen-and-paper analytic exercises on LMSE and
ML (on ILIAS).

## Links to global concepts

- [[Maximum Likelihood Estimation]] (global)
- [[Fisher Information]] (global — sufficiency/precision link)

## Open questions

- Figure 4.5 (probability vs likelihood) is the single most important visual;
  the user already has it as `DifferenceProbabilityAndLikelihood.png` in their
  notes ([[Farrell and Lewandowsky Chap 3.1-3.6 + Chap 4]]).
