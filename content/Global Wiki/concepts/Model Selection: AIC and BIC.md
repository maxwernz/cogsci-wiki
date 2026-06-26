---
type: method
status: active
scope: global
classes: [Cognitive Modeling, Data Literacy]
projects:
domains: [statistics, modeling, model selection]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Model Selection: AIC and BIC

## Short definition

AIC and BIC compare models by adding a complexity penalty to twice the negative
log-likelihood, so that a model is rewarded for fitting well but charged for the
parameters it uses.

## General explanation

Raw likelihood always favours the more complex model, so fair comparison requires
penalising complexity. **AIC** penalises by $2K$ and estimates the
**Kullback–Leibler distance** between model and truth (smallest estimated
information loss wins). **BIC** penalises by $K\ln n$ and approximates the model
with the **highest posterior probability**. Because $\ln n>2$ for $n>7$, BIC
punishes complexity harder for any realistic sample and so tends to select simpler
models. Lower AIC/BIC is preferred.

For **nested** models a likelihood-ratio test is also available: the difference in
**deviance** $D=2(\ell_{\text{saturated}}-\ell_{\text{fitted}})$ is
$\chi^2$-distributed with degrees of freedom equal to the parameter-count
difference. Neither parameter count fully captures complexity (functional form and
parameter space also matter), which is why **MDL** (minimum description length) and
**NML** exist, and why empirical methods like [[Cross-Validation]] are popular
complements.

## Intuition

Charge rent for complexity. Two tenants (models) want the apartment; the one that
gives the best "fit per parameter" — best penalised score — wins. AIC charges a
flat rent ($2K$); BIC charges rent that rises with how much data you have
($K\ln n$), so it is stricter about adding rooms (parameters).

## Formal definition

$$\mathrm{AIC}=-2\ln L(\hat\theta;y)+2K,\qquad \mathrm{BIC}=-2\ln L(\hat\theta;y)+K\ln n.$$

- $L(\hat\theta;y)$: maximised likelihood; $K$: number of free parameters; $n$:
  number of data points. $G^2=-2\ln L$ is the "badness-of-fit" currency; smaller
  is better.

## Worked example

Comparing a 2- vs 3-parameter model with $G^2$ of 509.47 and 508.74 ($N=250$):
the deviance difference is $0.73 < \chi^2_{1,.05}=3.84$, so the simpler model is
retained; the BIC comparison agrees (Bayes factor ≈ 9.4 for the simpler model).

## Why it matters

AIC/BIC are the standard, widely reported tools for choosing among competing
models in statistics, psychology, ecology, machine learning and beyond — the
practical answer to the overfitting problem.

## Used in

- [[Model Selection Criteria (Deviance, AIC, BIC)]] (VL3)
- [[VL07 Interpreting Modeling]] · [[VL08 Model Comparison Example]]

## Related concepts

- [[Maximum Likelihood Estimation]]
- [[Overfitting and the Bias-Variance Trade-off]]
- [[Cross-Validation]]

## Common confusions

- The likelihood-ratio (deviance) test applies only to *nested* models.
- AIC and BIC optimise different targets (KL distance vs posterior probability)
  and are not interchangeable; BIC penalises complexity more.
- Parameter count alone does not capture complexity (functional form matters →
  MDL/NML).

## Sources

- [[VL03 Goodness-of-fit]]
