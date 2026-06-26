---
type: concept
status: active
scope: global
classes: [Cognitive Modeling, Data Literacy, Understanding LLMs]
projects:
domains: [statistics, modeling, machine learning]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Overfitting and the Bias-Variance Trade-off

## Short definition

Overfitting is when a model fits the noise in a sample as well as the signal, so
it predicts new data poorly; the bias–variance trade-off explains why model
complexity must be tuned to the true process to minimise prediction error.

## General explanation

Data = signal (the true generating process) + noise. A more **complex
(flexible)** model can fit the training sample more tightly, but past a point it
starts fitting the noise — which is specific to that sample — and so generalises
worse. Complexity is driven by the number of free parameters, the functional
form, and the bounds on the parameter space (not parameter count alone).

The trade-off decomposes expected prediction error into **bias²** (systematic
mis-prediction, high for too-simple models that cannot capture the process),
**variance** (sample-to-sample wobble of the fit, high for too-flexible models
that chase noise), and an irreducible **noise** floor. Simple models: high bias,
low variance. Complex models: low bias, high variance. Total error is minimised
where complexity matches the true process. Operationally, **training error** falls
monotonically with complexity while **test (out-of-sample) error** is U-shaped —
its minimum marks the right complexity.

A crucial practical caveat: drawing the actual trade-off requires knowing the true
process and noise, which is exactly what you don't know when modeling a real
phenomenon. Hence we use *proxies* for prediction error — held-out test sets,
[[Cross-Validation]], penalty criteria ([[Model Selection: AIC and BIC]]), and
[[Regularisation]].

## Intuition

Memorising past exam papers verbatim (overfitting) gets you 100% on those papers
but fails on a new exam; learning the underlying principles (right complexity)
generalises. Adding epicycle upon epicycle to fit planetary data is the
historical analogue — more complexity, better fit, less understanding.

## Formal definition

$$\mathbb{E}\big[(y-\hat f(x))^2\big]=\mathrm{Bias}^2[\hat f(x)]+\mathrm{Var}[\hat f(x)]+\sigma^2.$$

- $\hat f(x)$: fitted prediction; bias decreases and variance increases with
  complexity; $\sigma^2$: irreducible noise.

## Worked example

Fit polynomials of order $M$ to 10 noisy points from $\sin(2\pi x)$ (Bishop): $M=3$
recovers the curve; $M=9$ achieves zero training error but oscillates wildly and
predicts terribly. RMS-error-vs-$M$ shows training error → 0 while test error dips
near $M=3$ then rises — the overfitting signature.

## Why it matters

It is the central reason goodness-of-fit alone is not enough, and it motivates
essentially every model-selection and regularisation technique across statistics,
machine learning, and cognitive modeling.

## Used in

- [[Goodness-of-Fit and Overfitting]] (VL3)
- [[Model Selection Criteria (Deviance, AIC, BIC)]]
- [[Cross-Validation and Regularisation]]

## Related concepts

- [[Cross-Validation]]
- [[Regularisation]]
- [[Model Selection: AIC and BIC]]

## Common confusions

- "Better fit = better model" — not if the extra fit is to noise.
- Complexity ≠ parameter count alone (functional form and bounds matter).
- "Bias" here means systematic mis-*prediction*, not a biased estimator.

## Sources

- [[VL03 Goodness-of-fit]]
- [[Bishop 2006 Pattern Recognition and Machine Learning]]
