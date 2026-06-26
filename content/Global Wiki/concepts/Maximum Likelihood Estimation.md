---
type: method
status: active
scope: global
classes: [Cognitive Modeling, Neural Coding]
projects:
domains: [statistics, modeling, machine learning, neuroscience]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_02_RMSD-ML.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Maximum Likelihood Estimation

## Short definition

Maximum likelihood estimation (MLE) chooses the parameter values that make the
observed data most probable under an assumed probability model.

## General explanation

Given a probability model $f(x\mid\theta)$ for the data, the **likelihood** of a
parameter value is the probability (density or mass) it assigns to the data you
actually observed. MLE returns the $\hat\theta$ that maximises this likelihood —
the parameter setting under which the data are least surprising. In practice one
maximises the **log-likelihood** $\ell(\theta)=\sum_i\ln f(x_i\mid\theta)$,
because sums are numerically stable and the log is monotonic (same maximiser).

MLE is the workhorse of statistical inference because of its estimator
properties: it is **(minimally) sufficient** (uses all the information the sample
carries about $\theta$), **consistent** (converges to the truth as $n\to\infty$),
**invariant to reparameterisation** ($\widehat{g(\theta)}=g(\hat\theta)$), and
asymptotically efficient — though it is **not necessarily unbiased** for finite
samples. Its asymptotic precision is governed by the [[Fisher Information]]
(Cramér–Rao bound: $\mathrm{Var}(\hat\theta)\ge 1/J(\theta)$). Unlike
least-squares fitting, MLE requires committing to a probability model, and that
commitment is exactly what enables goodness-of-fit tests, model comparison
(deviance, AIC/BIC), and confidence intervals.

## Intuition

You believe the data came from a process with unknown "dials" (parameters). MLE
turns the dials to the setting that would have made your particular data the most
expected. The key mental shift is **likelihood ≠ probability**: probability fixes
the parameters and varies the data (and integrates to 1); likelihood fixes the
data and varies the parameters (and does not).

## Formal definition

$$L(\theta;x)=\prod_{i=1}^{n}f(x_i\mid\theta),\qquad \hat\theta=\arg\max_\theta\sum_{i=1}^{n}\ln f(x_i\mid\theta).$$

- $f(x_i\mid\theta)$: model probability of the $i$-th observation; $n$: sample
  size. The maximiser is usually found analytically for simple models and
  numerically (simplex, simulated annealing, gradient methods) otherwise.

## Worked example

Bernoulli: $k=18$ successes in $n=20$ trials, model $p$. Then
$\ell(p)=k\ln p+(n-k)\ln(1-p)$; setting $\ell'(p)=0$ gives $\hat p=k/n=0.9$. For a
Gaussian with known variance, the MLE of the mean is just the sample mean — MLE
recovers familiar estimators and extends to models with no closed form.

## Why it matters

MLE is the basis for fitting almost any parametric model, for the likelihood-based
model-selection criteria (deviance, AIC, BIC), and for connecting models to
estimation-precision limits via Fisher information. It is the frequentist
counterpart to [[Bayesian Inference]] (which adds a prior and returns a posterior
rather than a point estimate).

## Used in

- [[Maximum Likelihood Estimation in Cognitive Modeling]] (VL2)
- [[VL06 Modeling Visual Cognition]] (ML fit of a $d'$ model)
- [[VL08 Model Comparison Example]] (sequence likelihood, $G^2$)
- [[Fisher Information]] (precision of the ML estimator)

## Related concepts

- [[Fisher Information]]
- [[Model Selection: AIC and BIC]]
- [[Bayesian Inference]]
- [[The Bootstrap]]

## Common confusions

- Likelihood is not a probability over parameters; its absolute value is
  meaningless, only ratios matter.
- MLE is only *asymptotically* unbiased; finite-sample bias is possible.
- Higher likelihood within a model family is automatic for more parameters —
  hence the need for complexity penalties.

## Sources

- [[VL02 RMSD and ML]]
