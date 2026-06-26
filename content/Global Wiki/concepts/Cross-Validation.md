---
type: method
status: active
scope: global
classes: [Cognitive Modeling, Data Literacy, Understanding LLMs]
projects:
domains: [statistics, machine learning, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Cross-Validation

## Short definition

Cross-validation estimates a model's out-of-sample prediction error by repeatedly
fitting on part of the data and testing on the held-out part.

## General explanation

Because an over-fit model fits its training data well but predicts new data
poorly, evaluating a model on data it was *not* fit to exposes overfitting and
identifies the right complexity. A single fixed train/test split wastes data;
cross-validation reuses data efficiently:

- **Leave-one-out (LOO):** each point is held out in turn; fit on the other
  $n-1$, test on the one.
- **K-fold:** split into $K$ folds; each fold serves once as the test set while
  the rest train. K-fold gives a reasonable estimate of expected prediction error
  across training sets (Hastie et al., 2009).

Picking the model (or hyperparameter) with the lowest validation error trades fit
against complexity automatically. CV is pragmatic, hugely successful in machine
learning, makes few assumptions, and works even with least-squares fits (which
lack statistical properties). Its weaknesses: usually no proofs that it works, and
unprincipled choices ($K$, what to do when folds disagree). To both tune a
hyperparameter *and* honestly estimate generalisation you need **nested CV**
(inner loop tunes, outer loop assesses) with a three-way train/validation/test
split.

## Intuition

Studying with practice questions, then testing yourself on *fresh* questions you
haven't seen: if you only memorised the practice set, you fail the fresh test.
Rotate which questions are "fresh" so every question gets used for both studying
and testing.

## Formal definition

K-fold CV error for a model fit by minimising loss $\mathcal L$:

$$\mathrm{CV} = \frac{1}{K}\sum_{j=1}^{K} \mathcal L\big(y_{(j)},\, \hat f^{\,-(j)}(x_{(j)})\big),$$

- $(j)$: the $j$-th held-out fold; $\hat f^{\,-(j)}$: the model fit on all folds
  except $j$. LOO is the special case $K=n$.

## Worked example

10-fold CV on a polynomial: for each candidate order $M$, fit on 9 folds, measure
error on the 10th, average over the 10 rotations; choose the $M$ with the lowest
average — typically near the true order, avoiding the high-$M$ overfit.

## Why it matters

Cross-validation is the default empirical tool for model selection and
hyperparameter tuning across machine learning and statistics, and the basis of
generalisation tests in cognitive modeling.

## Used in

- [[Cross-Validation and Regularisation]] (VL3)
- [[VL07 Interpreting Modeling]] · [[VL08 Model Comparison Example]]

## Related concepts

- [[Regularisation]]
- [[Overfitting and the Bias-Variance Trade-off]]
- [[Model Selection: AIC and BIC]]

## Common confusions

- CV *evaluates* models; it does not change them (that is regularisation).
- Reporting the CV error used to tune a hyperparameter as the generalisation
  error double-uses data — you need nested CV.

## Sources

- [[VL03 Goodness-of-fit]]
- [[Hastie et al 2009 Elements of Statistical Learning]]
