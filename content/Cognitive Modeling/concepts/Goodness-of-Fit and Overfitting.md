---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
  - Classes/Cognitive Modeling/raw/Computational Modeling of Cognition and Behavior/10.1_pp_241_272_Model_Comparison.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Goodness-of-Fit and Overfitting

## Short definition

Goodness-of-fit measures how closely a model reproduces the data; over-fitting is
when a model fits so closely that it captures random noise as well as the true
signal, and so predicts new data worse.

## Intuition

A more flexible model can always hug the data more tightly — but data are noisy,
and the wiggles a flexible model adds to pass through every point are usually
chasing noise, not signal. Like Ptolemy adding epicycle upon epicycle to fit
planetary positions, you can always improve the fit by adding complexity, but at
some point you stop describing the world and start memorising your particular,
noisy sample. The counterintuitive punchline: **a worse fit can be a better
model.**

## Explanation

**Goodness-of-fit (GoF)** is just a discrepancy measure — the smaller the
residuals (or the higher the likelihood), the better the fit. The lecture's
central warning is that **GoF by itself cannot prevent over-fitting**, because
you can always improve GoF by making the model more flexible.

**Over-fitting** is fitting noise as well as signal. Assume the data come from a
true generating process plus random noise; our goal is to recover the process and
*ignore* the noise. An over-fit model handles every data point — including the
noise — and therefore generalises poorly to fresh data drawn from the same
process.

Over-fitting is inseparable from **model complexity (flexibility)** — the
model's ability to produce many different data patterns. Three things drive it:

1. **Number of free parameters** — more parameters generally fit better.
2. **Functional form** — even with the same parameter count, one model can
   produce a wider range of shapes than another.
3. **Extension of the parameter space** — the bounds on parameters. Constraining
   a 2nd-order polynomial's coefficients to be positive, for instance, lets it
   make only linear or U-shaped (not ∩-shaped) curves, reducing flexibility.

The **bias–variance trade-off** formalises the tension. *Bias* is systematic
mis-prediction: a model too simple to capture the true process misses it the
same way no matter how much data you average (e.g. a straight line fit to a
cubic). *Variance* is how much the fitted curve swings from one noisy sample to
the next: a flexible model has the power to chase each sample's particular noise,
so its fits are unstable. Simple → high bias, low variance; complex → low bias,
high variance. **Total error is minimised where complexity matches the true
generating process** — the "sweet spot".

A deep practical point (the lecture's Q3): to actually *draw* the bias–variance
trade-off you must know the true generating process and the noise properties, so
you can measure how far average predictions sit from the truth (bias) and how much
they vary (variance). When modeling a real cognitive process the truth is exactly
what you do *not* know — so the trade-off is theoretically illuminating but
**not directly usable** in practice. This is why we need *proxies* for prediction
error: the train/test split, [[Cross-Validation and Regularisation|cross-validation]],
and penalty criteria like [[Model Selection Criteria (Deviance, AIC, BIC)|AIC/BIC]].

**Fit vs prediction** captures the same idea operationally. As complexity grows,
**training error** (fit to the data used for fitting) decreases monotonically.
But **test error** (on held-out data) first decreases then *increases* — the
U-shape whose minimum marks the right complexity. A model low in both bias and
variance predicts unseen data well; an over-fit one does not. (Note the subtle
distinction the lecture's Q4 raises: in the bias–variance plot, bias hits zero
once the model is complex enough to *contain* the true process, e.g. order ≥ 3
for a cubic truth; but training error keeps dropping past that, because extra
flexibility keeps fitting noise.)

## Worked example

Bishop's polynomial curve fitting ([[Bishop 2006 Pattern Recognition and Machine Learning]]): fit polynomials of order $M$ to 10 noisy points from $\sin(2\pi x)$.
$M=3$ recovers the sine nicely; $M=9$ passes through all 10 points with *zero*
training error yet oscillates wildly — perfect fit, terrible prediction. Plotting
RMS error vs $M$ shows training error falling to zero while test error dips at
$M\approx3$ and then shoots up: the textbook over-fitting signature.

## Formal definition / equations

Decomposition of expected prediction error at a point (conceptual form):

$$\mathbb{E}\big[(y-\hat f(x))^2\big] = \underbrace{\mathrm{Bias}^2[\hat f(x)]}_{\text{systematic miss}} + \underbrace{\mathrm{Var}[\hat f(x)]}_{\text{sample-to-sample wobble}} + \underbrace{\sigma^2}_{\text{irreducible noise}}.$$

- $\hat f(x)$: the fitted model's prediction; bias falls and variance rises with
  complexity; $\sigma^2$ is the noise floor that no model can beat.

## Role in this class or project

Step 2 of the recipe ([[VL03 Goodness-of-fit]]) and the conceptual heart of model
comparison. It motivates every later tool: deviance/AIC/BIC, cross-validation,
regularisation, and the model-recovery and generalization methods of
[[VL07 Interpreting Modeling]].

## Exam, assignment, or project relevance

Very high. Explain why GoF cannot prevent over-fitting; list the three complexity
drivers; define bias and variance and the trade-off; explain why the trade-off
plot is impossible in practice for a cognitive process; and describe the
train-vs-test-error curves and why training error keeps falling past the point
where bias is zero. The epicycles/Occam's-razor connection is a likely question.

## Related global concepts

- [[Overfitting and the Bias-Variance Trade-off]]
- [[Cross-Validation]]
- [[Regularisation]]

## Related local pages

- [[Model Selection Criteria (Deviance, AIC, BIC)]]
- [[Cross-Validation and Regularisation]]
- [[Parameter Identifiability and Model Testability]]

## Common confusions

- **"Better fit = better model."** Not if the extra fit is to noise; prediction
  on new data is the real test.
- **"Complexity = number of parameters."** Functional form and parameter bounds
  matter too.
- **"Bias means a biased estimator."** Here bias means systematic
  mis-*prediction* of the data, a property of model complexity.

## Sources

- [[VL03 Goodness-of-fit]]
- [[Farrell and Lewandowsky Chap 10]] (user note)
- [[Bishop 2006 Pattern Recognition and Machine Learning]]
