---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: paper
raw_path: Classes/Cognitive Modeling/raw/Literature/Schutt_2016.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Schütt, Harmeling, Macke & Wichmann (2016) — Painfree and Accurate Bayesian Estimation of Psychometric Functions

> Cited in [[VL05 Bayes]] / the [[ReadingList-VL2-5.pdf|reading list]] as suggested
> further reading on **Bayesian modeling** (it is the Bayesian counterpart to the
> frequentist Wichmann & Hill psychometric-function papers). Suggested reading,
> not compulsory.

## Summary

A Bayesian re-working of psychometric-function estimation, and a clean example of
"Bayesian modeling" in the VL5 sense: instead of a point estimate plus a
bootstrap confidence interval (the frequentist VL2–VL4 route), it places a
**prior** over the function's parameters and returns a **posterior** /
**credible interval**. Its main technical contribution is replacing the standard
**binomial** observation model with a **beta-binomial** model, which absorbs
**overdispersion** — extra trial-to-trial variability caused by non-stationary
observers (lapses of attention, learning, fatigue). With the binomial model such
overdispersion makes confidence intervals far too narrow; the beta-binomial
model yields accurate credible intervals even when the data are overdispersed.
This is the engine behind the widely used `psignifit 4` toolbox.

## Key points

- **Frequentist vs Bayesian, made concrete:** bootstrap CIs (Wichmann & Hill,
  2001b) vs Bayesian credible intervals from a posterior — the same VL5 contrast
  applied to one model.
- **Overdispersion** is the practical problem: real observers are not stationary
  binomial samplers, so naive binomial CIs are over-confident.
- **Beta-binomial model** adds a dispersion parameter, widening intervals
  appropriately and giving accurate coverage.
- Demonstrates that "Bayesian modeling" is not just philosophy — it can solve a
  concrete estimation problem (honest error bars under overdispersion) better
  than the standard approach.

## Local relevance

Connects VL5 (Bayesian modeling) back to the VL4 problem of getting honest error
bars on fitted parameters: where the bootstrap gave frequentist CIs, the
Bayesian route gives credible intervals and handles overdispersion gracefully.

## Exam or project relevance

Low/optional (suggested reading). Useful as a worked contrast of bootstrap CIs
vs Bayesian credible intervals, and as an example of why the observation model
(binomial vs beta-binomial) matters for variability estimates.

## Links to global concepts

- [[Bayesian Inference]] (global)
- [[The Bootstrap]] (global — the frequentist alternative it replaces)

## Open questions

- The MCMC/numerical-integration machinery is beyond the course; treat as
  "Bayesian modeling in practice".
