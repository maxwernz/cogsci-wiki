---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, modeling, model selection]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
  - Classes/Cognitive Modeling/raw/Computational Modeling of Cognition and Behavior/10.1_pp_241_272_Model_Comparison.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Model Selection Criteria (Deviance, AIC, BIC)

## Short definition

A family of likelihood-based numbers that compare models by balancing how well
they fit against how complex they are — deviance and the likelihood-ratio test
for nested models, AIC and BIC (and MDL/NML) for nested *or* non-nested models.

## Intuition

Raw fit always favours the more complex model, so a fair comparison must "charge
rent" for complexity. These criteria all take the model's fit (its
log-likelihood) and subtract a penalty that grows with the number of parameters.
The model with the best penalised score wins — a computational version of
Occam's razor: the simplest model that still fits well.

## Explanation

**The problem with raw likelihood.** The likelihood $L(\hat\theta;y)$ and
log-likelihood depend on the number of data points $n$ *and* on the particulars
of the probability distribution, so their absolute values are meaningless and a
naive correction for $n$ is insufficient. We need a *relative* or *penalised*
quantity.

**Deviance** solves the "raw values are meaningless" problem by comparing your
model to the **saturated model** $\theta_{\max}$ — a model with one free
parameter per data point, which fits perfectly ($f(\theta_{\max};x_i)=y_i$).
Deviance is twice the log-likelihood *ratio* of your fitted model against this
best-possible model: it tells you how far your model is from a perfect fit, on a
scale that washes out the nuisance dependence on $n$ and the distribution.

**Likelihood-ratio test (nested models).** Asymptotically (and often even for
small $n$) deviance is $\chi^2$-distributed with $n-K$ degrees of freedom ($K$
free parameters). For two **nested** models (one a restricted version of the
other, e.g. polynomials of order 2 vs order 5 from the same family), the
*difference* in deviance is $\chi^2$ with df = the difference in parameter count.
If that difference exceeds the $\chi^2$ critical value, the extra parameters
*significantly* improve the fit; otherwise keep the simpler model.

**AIC and BIC (nested or non-nested).** The likelihood-ratio test only works for
nested models, and deviance is biased from a Kullback–Leibler perspective. AIC
and BIC instead add an explicit complexity penalty to $-2\ln L$:

- **AIC** penalises by $2K$. It estimates the **Kullback–Leibler distance**
  between model and truth — the model with the smallest estimated information
  loss.
- **BIC** penalises by $K\ln n$. It approximates the model with the **highest
  posterior probability** given the data. Because $\ln n>2$ once $n>7$, **BIC
  punishes complexity harder than AIC for any realistic sample**, so BIC tends to
  prefer simpler models.

Lower AIC/BIC = preferred. Crucially, **the number of parameters does not capture
all of complexity** (functional form and parameter space also matter), which is
why richer criteria exist: **MDL** (minimum description length) and **NML**
(normalized maximum likelihood), which use the Fisher-information geometry to
account for functional form. These trade fit against complexity *analytically*;
[[Cross-Validation and Regularisation|cross-validation]] does the same thing
*empirically*.

## Worked example

From [[VL08 Model Comparison Example]]: comparing a 3-parameter (free weight $w$)
vs 2-parameter (fixed $w=.5$) expectancy-valence model — these are **nested**.
The general model gives $G^2=508.74$, the restricted $G^2=509.47$. The deviance
difference is $509.47-508.74=0.73$. With df = 1 the $\chi^2$ critical value at
$\alpha=.05$ is $3.84$. Since $0.73<3.84$, retain the simpler model: for this
participant, wins and losses were weighted equally. A BIC comparison on the same
numbers ($N=250$, $\ln 250\approx5.52$) likewise favours the simpler model, with
a Bayes factor of about 9.4 (considerable evidence).

## Formal definition / equations

Deviance and the nested LR test:

$$D = 2\big(\ell(\theta_{\max};y) - \ell(\hat\theta;y)\big),\qquad \Delta D \sim \chi^2_{\Delta K}.$$

AIC and BIC:

$$\mathrm{AIC} = -2\ln L(\hat\theta;y) + 2K,\qquad \mathrm{BIC} = -2\ln L(\hat\theta;y) + K\ln n.$$

- $\hat\theta$: fitted parameters; $\theta_{\max}$: saturated (perfect-fit) model;
  $K$: number of free parameters; $n$: number of data points; $\Delta K$:
  difference in parameter count between nested models. $G^2 = -2\ln L$ is the
  same "badness-of-fit" currency used in VL8.

## Role in this class or project

The quantitative core of step 2 ([[VL03 Goodness-of-fit]]). Reused as the model-
comparison engine in [[VL07 Interpreting Modeling]] (workflow) and worked
end-to-end in [[VL08 Model Comparison Example]].

## Exam, assignment, or project relevance

Very high. Define the saturated model; compute deviance; run a likelihood-ratio
test on nested models (deviance difference vs $\chi^2$); write AIC and BIC and
explain their penalty terms; explain *why* BIC penalises complexity more for
large $n$; and name MDL/NML as criteria that also account for functional form.

## Related global concepts

- [[Model Selection: AIC and BIC]]
- [[Maximum Likelihood Estimation]]
- [[Overfitting and the Bias-Variance Trade-off]]

## Related local pages

- [[Goodness-of-Fit and Overfitting]]
- [[Cross-Validation and Regularisation]]
- [[Maximum Likelihood Estimation in Cognitive Modeling]]

## Common confusions

- **"Use the likelihood-ratio test for any two models."** Only *nested* models.
- **"AIC and BIC are interchangeable."** They optimise different things (KL
  distance vs posterior probability) and BIC penalises complexity more.
- **"Counting parameters fully measures complexity."** No — functional form and
  parameter bounds matter (the reason MDL/NML exist).

## Sources

- [[VL03 Goodness-of-fit]]
- [[Farrell and Lewandowsky Chap 10]] (user note)
