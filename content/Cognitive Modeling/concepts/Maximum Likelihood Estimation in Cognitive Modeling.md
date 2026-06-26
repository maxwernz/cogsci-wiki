---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_02_RMSD-ML.pdf
  - Classes/Cognitive Modeling/raw/Computational Modeling of Cognition and Behavior/09.2_pp_72_104_Maximum_Likelihood_Parameter_Estimation.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Maximum Likelihood Estimation in Cognitive Modeling

## Short definition

Maximum likelihood estimation (MLE) picks the parameter values under which the
observed data are most probable, given a chosen probability model for the data.

## Intuition

You assume the data were produced by some probabilistic process with unknown
"dials" (parameters). MLE asks: *which dial settings would have made the data I
actually saw the least surprising?* It then turns those dials to maximise that
"un-surprisingness" (the likelihood). Unlike least squares, this requires you to
commit to a probability story for the data — but that commitment is what buys you
statistical guarantees (tests, model comparison, confidence intervals).

## Explanation

MLE differs from [[Least-Squares Estimation in Cognitive Modeling]] in one
essential way: it **requires a probabilistic model**. You specify a distribution
(e.g. binomial for correct/incorrect responses, or a Wald distribution for
response times) whose parameters you want to estimate. The **likelihood** of a
parameter setting is the probability density/mass it assigns to the data you
observed; MLE chooses the setting that maximises it.

The single most important conceptual hurdle is the **probability-vs-likelihood
distinction**. They use the *same* function $f(x,\theta)$ but read it in
opposite directions:

- **Probability** fixes the parameters and varies the data: "given this model,
  how probable are various outcomes?" Probabilities of all outcomes sum/integrate
  to 1.
- **Likelihood** fixes the data and varies the parameters: "given the data I
  saw, how well does each candidate parameter value explain it?" Likelihoods do
  *not* integrate to 1 over parameters — their absolute scale is meaningless;
  only relative values matter.

This is exactly Farrell & Lewandowsky's Figure 4.5: a 3-D surface
$p(t,m)$ over response time $t$ and Wald parameter $m$; slicing at fixed $m$
gives a probability density over $t$, slicing at fixed $t$ gives a likelihood
function over $m$.

In practice one maximises the **log-likelihood** $\ell=\sum_i \ln f(x_i,\theta)$
rather than the product of probabilities, because (a) sums are numerically
stable where products of many small numbers underflow, and (b) the log is
monotonic so it has the same maximiser. As with least squares, the maximum is
usually found **numerically** (see [[Numerical Optimisation for Model Fitting]]).

MLE's estimator has properties that justify its dominance:

- **Sufficiency (minimal).** The ML estimate captures *all* the information the
  sample carries about $\theta$. "Minimally sufficient" means any non-equivalent
  estimator can only *lose* information — so you are never throwing information
  away by using MLE.
- **Consistency.** As the sample size $n\to\infty$, the estimate converges to the
  true parameter. Desirable because it means more data reliably gets you closer
  to the truth.
- **Not necessarily unbiased.** For finite $n$ the estimate can be
  systematically off (bias); MLE only guarantees this vanishes asymptotically.
- **Parameterisation (functional) invariance.** If $\hat\theta$ is the MLE of
  $\theta$, then $g(\hat\theta)$ is the MLE of $g(\theta)$ for any
  transformation $g$ — you can reparameterise freely without redoing the
  estimation.

Because MLE rests on a probability model, it unlocks everything VL3–VL4 need:
goodness-of-fit via **deviance**, model comparison via **likelihood-ratio
tests / AIC / BIC**, and (with the bootstrap) confidence intervals.

## Worked example

Binomial example: an observer is correct on $k=18$ of $n=20$ trials and you model
correctness as Bernoulli($p$). The log-likelihood is
$\ell(p)=k\ln p+(n-k)\ln(1-p)$. Setting $\mathrm{d}\ell/\mathrm{d}p=0$ gives
$\hat p=k/n=0.9$. Here MLE recovers the obvious proportion — but the same
machinery extends to models with no closed-form solution (e.g. the
expectancy-valence model in [[VL08 Model Comparison Example]], where the
per-trial choice probabilities are multiplied into a sequence likelihood and
maximised numerically).

## Formal definition / equations

For independent observations $x_1,\dots,x_n$ from model $f(\cdot,\theta)$:

$$L(\theta;x)=\prod_{i=1}^{n} f(x_i,\theta),\qquad \ell(\theta;x)=\sum_{i=1}^{n}\ln f(x_i,\theta),\qquad \hat\theta=\arg\max_\theta \ell(\theta;x).$$

- $L$: likelihood; $\ell$: log-likelihood; $f(x_i,\theta)$: the model's
  probability (density/mass) of observation $x_i$ under $\theta$.

## Role in this class or project

The statistically principled half of step 1 ([[VL02 RMSD and ML]]). It is the
foundation for the goodness-of-fit currency ($-2\ln L$, deviance, $G^2$), for
model comparison in [[VL07 Interpreting Modeling]] and [[VL08 Model Comparison Example]], and for the $d'$-based fitting in [[VL06 Modeling Visual Cognition]].

## Exam, assignment, or project relevance

Very high. Explain probability vs likelihood (Figure 4.5); state and motivate
sufficiency, consistency, (a)bias and parameterisation invariance; explain why
ML needs a probability model and LSE does not; and derive a simple MLE (e.g.
Bernoulli). Analytic exercises on ML are provided.

## Related global concepts

- [[Maximum Likelihood Estimation]]
- [[Fisher Information]]
- [[Bayesian Inference]] (the prior-free limit / contrast)

## Related local pages

- [[Least-Squares Estimation in Cognitive Modeling]]
- [[Numerical Optimisation for Model Fitting]]
- [[Model Selection Criteria (Deviance, AIC, BIC)]]
- [[Bayesian Inference in Cognitive Modeling]]

## Common confusions

- **"Likelihood is a probability."** It is not a probability over parameters; it
  does not integrate to 1 and its absolute value is meaningless.
- **"MLE is unbiased."** Only asymptotically; finite-sample bias is possible.
- **"Higher likelihood always means a better model."** Within a model family more
  parameters raise the likelihood mechanically — which is why GoF criteria
  penalise complexity (VL3).

## Sources

- [[VL02 RMSD and ML]]
- [[Farrell and Lewandowsky Chap 3.1-3.6 + Chap 4]] (user note)
