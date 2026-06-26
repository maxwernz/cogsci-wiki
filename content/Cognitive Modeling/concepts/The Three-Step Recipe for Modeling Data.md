---
type: synthesis
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_02_RMSD-ML.pdf
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_04_CIs.pdf
created: 2026-06-09
updated: 2026-06-09
---

# The Three-Step Recipe for Modeling Data

## Short definition

The course's organising framework: fitting a model to data is always a
three-step procedure — (1) estimate parameters, (2) assess goodness-of-fit (and
compare models), (3) estimate the variability of the parameters — and skipping
steps 2–3 ("chi-by-eye") is bad practice.

## Intuition

Getting a best-fitting curve is only the first third of the job. You also need to
know whether the fit is actually *good* (or whether a simpler/different model
would do as well), and how *uncertain* your parameters are. A pretty plot that
"looks good" tells you none of this. The whole of VL2–VL4 is one recipe, not
three separate topics; VL5 (Bayes) offers an alternative way to do the same job.

## Explanation

Press et al. (Numerical Recipes) state it bluntly: a fitting procedure should
provide (i) parameters, (ii) error estimates on the parameters, and (iii) a
goodness-of-fit measure — and if (iii) says the model is a poor match, then (i)
and (ii) are "probably worthless". The course maps this onto four lectures:

- **VL2 — Measure the discrepancy (estimate parameters).** Choose a discrepancy
  function and minimise it. Least squares ([[Least-Squares Estimation in Cognitive Modeling]]) is intuitive but statistically blind; maximum likelihood
  ([[Maximum Likelihood Estimation in Cognitive Modeling]]) needs a probability
  model but unlocks tests, comparison and CIs. The optimum is found numerically
  ([[Numerical Optimisation for Model Fitting]]).
- **VL3 — Evaluate the discrepancy (goodness-of-fit & model comparison).** A good
  fit alone cannot prevent over-fitting ([[Goodness-of-Fit and Overfitting]]); you
  must trade fit against complexity using deviance/AIC/BIC ([[Model Selection Criteria (Deviance, AIC, BIC)]]) or cross-validation/regularisation
  ([[Cross-Validation and Regularisation]]), and first check the model is
  identifiable and testable ([[Parameter Identifiability and Model Testability]]).
- **VL4 — Assess variability (error bars).** Point estimates need confidence
  intervals; since analytic ones are usually impossible, use the bootstrap
  ([[The Bootstrap]]).
- **VL5 — A different philosophy.** Bayesian modeling ([[Bayesian Inference in Cognitive Modeling]]) replaces "estimate θ + bootstrap CI" with "compute a
  posterior distribution over θ", differing on what probability *means* and on the
  role of priors.

Each step depends on the previous: the *currency* of step 2 (deviance, $-2\ln L$,
$G^2$) is built from the step-1 likelihood, and the step-3 bootstrap *refits* the
step-1 model many times. Steps 2–3 also feed model *comparison* and
*interpretation* (VL7–VL8): you compare models on penalised fit, bootstrap their
parameter confidences, and then interpret what the winning model's parameters mean
([[Model Interpretation: Necessity and Sufficiency]]), having chosen the right data
to fit in the first place ([[Choosing Data to Fit (Individual vs Aggregate)]]).

## Worked example

Wichmann & Hill's two companion papers fit a psychometric function across exactly
these steps: 2001a does parameter estimation (step 1) and goodness-of-fit (step
2); 2001b does the bootstrap confidence intervals (step 3) ([[Wichmann and Hill 2001a Psychometric Function I]], [[Wichmann and Hill (2001b)]]). [[VL08 Model Comparison Example]] runs the full recipe on the Iowa Gambling Task: ML fit →
$G^2$/BIC comparison → (bootstrap/generalization) → parameter interpretation.

## Role in this class or project

The spine of the entire course. Use it as the mental index: any modeling task
maps onto "parameters → goodness-of-fit/comparison → error bars → interpretation".

## Exam, assignment, or project relevance

Be able to recite the three steps, say which lecture/tool implements each, and
explain why all three are needed (the chi-by-eye warning). This framing recurs at
the start of VL3, VL4 and VL6 and underlies VL7–VL8.

## Related global concepts

- [[Maximum Likelihood Estimation]]
- [[Model Selection: AIC and BIC]]
- [[The Bootstrap]]

## Related local pages

- [[VL02 RMSD and ML]] · [[VL03 Goodness-of-fit]] · [[VL04 Assessing variability]] · [[VL05 Bayes]]
- [[Least-Squares Estimation in Cognitive Modeling]]
- [[Maximum Likelihood Estimation in Cognitive Modeling]]
- [[Goodness-of-Fit and Overfitting]]
- [[The Bootstrap]]

## Common confusions

- **"Fitting is the whole job."** It is step 1 of 3; without GoF and error bars
  the estimates can be worthless.
- **"The three lectures are separate topics."** They are one procedure.

## Sources

- [[VL02 RMSD and ML]]
- [[VL03 Goodness-of-fit]]
- [[VL04 Assessing variability]]
