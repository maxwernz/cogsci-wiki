---
type: method
status: active
scope: global
classes: [Cognitive Modeling, Understanding LLMs]
projects:
domains: [statistics, machine learning, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Regularisation

## Short definition

Regularisation discourages over-fitting by adding a penalty for model complexity
directly to the fitting objective, so the optimiser avoids large or numerous
parameters unless the data justify them.

## General explanation

Where [[Cross-Validation]] *evaluates* models, regularisation *changes how a model
is fit*: it augments the goodness-of-fit term with a penalty on the size of the
parameters. The penalty is a (weighted) **norm** of the parameter vector — the
more, and the larger, the parameters, the bigger the penalty. The **L2** norm
($p=2$) gives **ridge** regression; the **L1** norm ($p=1$) gives **lasso**, which
can drive coefficients exactly to zero (feature selection). Regularisation
**increases bias but decreases variance**, producing simpler, more stable models;
for the right penalty strength the *total* error is lower.

The strength $\lambda$ is a **hyperparameter**, typically tuned by cross-validation
(and, to also assess the model honestly, by *nested* cross-validation).
Regularisation gives **smooth, continuous** control of effective complexity —
unlike discrete model-count criteria — and penalises parameter *magnitude*, not
just count (unlike AIC/BIC). It is closely analogous to a **Bayesian prior** that
disfavours complex models (e.g. L2 ↔ a Gaussian prior, giving MAP estimation); the
difference is that $\lambda$ is tuned by data rather than fixed a priori.

## Intuition

Pay a tax proportional to how big your parameters are. If a wiggle (large
coefficient) does not earn enough improvement in fit to cover its tax, the
optimiser drops it — so the model stays as smooth as the data warrant.

## Formal definition

$$E(\alpha)=\underbrace{\sum_{i=1}^{N}\{y_i-f(x_i,\alpha)\}^2}_{\text{fit}}+\lambda\lVert\alpha\rVert_p,\qquad \lVert\alpha\rVert_p=\Big(\sum_i|\alpha_i|^p\Big)^{1/p}.$$

- $\lambda\ge 0$: penalty strength (larger → simpler model); $p=2$ ridge, $p=1$
  lasso. With $p=2$ the penalty is $\lambda\,\alpha^\top\alpha$.

## Worked example

A 9th-order polynomial over-fits 10 noisy points; adding $\lambda\lVert\alpha\rVert^2$
with a CV-chosen $\ln\lambda$ shrinks the coefficients and removes the wild
oscillations *without* reducing the polynomial order — bias up a little, variance
down a lot, better generalisation.

## Why it matters

Regularisation (weight decay, ridge, lasso, dropout, early stopping) is everywhere
in modern statistics and machine learning, including the training of large neural
networks, and is the continuous counterpart to discrete model selection.

## Used in

- [[Cross-Validation and Regularisation]] (VL3)

## Related concepts

- [[Cross-Validation]]
- [[Overfitting and the Bias-Variance Trade-off]]
- [[Bayesian Inference]] (prior ↔ penalty)
- [[Model Selection: AIC and BIC]]

## Common confusions

- Regularisation changes the fit; cross-validation only evaluates.
- L1 (lasso) can zero out parameters; L2 (ridge) shrinks them smoothly.
- The penalty strength $\lambda$ must be tuned (CV), and assessing the tuned model
  needs nested CV.

## Sources

- [[VL03 Goodness-of-fit]]
- [[Bishop 2006 Pattern Recognition and Machine Learning]]
