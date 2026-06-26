---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, modeling, methodology]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_07_InterpretingModeling.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Choosing Data to Fit (Individual vs Aggregate)

## Short definition

The methodological decision of *which* data a model is fit to — each participant
individually, the group average, or some aggregate — which can change the
conclusions entirely.

## Intuition

Averaging people together feels like it should reveal the "typical" pattern, but
it can manufacture a pattern that *no individual* actually shows, and can even
*reverse* a real effect. If you want to understand individual behaviour, fit
individuals; if you fit the average, you only ever learn about the average — which
may be a fiction.

## Explanation

**Simpson's paradox.** An aggregate trend can reverse once you condition on a
grouping variable. The classic case (Berkeley, 1973): overall, men were admitted
at a higher rate than women (a highly significant $\chi^2$ → apparent gender
bias). But *within each department* women were admitted at equal-or-higher rates;
women simply applied more to competitive departments. The aggregate hid — and
inverted — the truth. The same reversal can corrupt cognitive modeling whenever a
hidden grouping factor structures the data.

**Averaging artefacts.** Averaging can distort the *functional form* of behaviour.
Sharp, near-deterministic individual choice points can average into a smooth,
seemingly probabilistic sigmoid; highly non-linear individual curves can average
into something nearly linear. A famous case: the "power law of practice" was
*falsified* by analysing individual data — the true individual learning curve is
**exponential**, and only averaging across people with different rates makes it
look like a power law. (Side note, non-exam: Estes (1956) gives mathematical rules
for when averaging is safe — e.g. it is fine for $y=a\log x$ or polynomials, but
distorts $y=a+be^{-cx}$.)

**Fitting individuals — pros and cons.** Fitting each participant gives the most
accurate fit, avoids Simpson's paradox and averaging artefacts, and turns the
*spread* of parameters into data: it reveals individual differences (distinct
strategies, working-memory capacity), can correlate parameters with other
measures, and flags model implausibility (if only a few people fit, parameters
swing wildly across people, or differ across optimisation runs on identical
data). The catch is data hunger: you may lack enough trials per person
(longitudinal gaps, short questionnaires, eyewitness lineups). Rules of thumb
(Cohen, Sanborn & Shiffrin, 2008): do not fit individuals with fewer than ~10
data points; and have at least ~2× as many data points as parameters.

**Hybrid options** when pure individual fitting is impossible:

- **Subgroup fitting:** fit clusters of participants who likely share a strategy
  or bias; clustering in parameter space can reveal these subgroups.
- **Aggregate / binned fitting ("vincentizing", Ratcliff, 1979):** sort each
  person's RTs, split into $n$ quantile bins, average the bin means across people,
  and fit the model to those quantile means. This summarises the *distribution*
  (not just the mean RT), avoids the addressed averaging errors, and is useful
  when there are few trials per person but many people. Some individual
  information is still lost.
- **Multilevel / hierarchical modeling (side note, non-exam):** posit a
  distribution for individual differences, fit those hyper-parameters, then fit
  each individual's responses within it.

**Bottom line.** Match the data to the question: individual data for questions
about individual behaviour; group-level fits are legitimate for questions about
the group, but beware that fitting aggregated data can skew conclusions about
individuals (cf. Simpson's paradox).

## Worked example

Berkeley admissions: aggregate 44% (men) vs 35% (women) → $\chi^2\approx110$,
$p<.00001$, "discrimination". Broken down by department, women's admission rates
*equal or exceed* men's in the departments they applied to; the aggregate effect
came from application choices, not bias. A cognitive analogue: averaging two
groups who switch strategy at different points yields a smooth group curve that
misrepresents both groups' sharp individual switches.

## Role in this class or project

Part of [[VL07 Interpreting Modeling]] (Butz). It is the "which data?" decision
that precedes and conditions every fit, comparison and interpretation — and is
applied concretely in [[VL08 Model Comparison Example]], where 60 participants ×
250 trials *do* permit individual fitting.

## Exam, assignment, or project relevance

Explain Simpson's paradox (with the Berkeley example) and averaging artefacts;
state when to fit individuals vs groups and the data-quantity rules of thumb;
describe vincentizing and subgroup fitting; and explain why the power law of
practice example matters. (Estes maths and multilevel modeling are flagged
non-exam.)

## Related global concepts

- [[Maximum Likelihood Estimation]]
- [[Overfitting and the Bias-Variance Trade-off]]

## Related local pages

- [[Model Interpretation: Necessity and Sufficiency]]
- [[The Three-Step Recipe for Modeling Data]]

## Common confusions

- **"The average is the typical participant."** It can be a pattern no individual
  shows, and can reverse the within-group effect.
- **"More participants always fixes things."** It does not fix averaging
  artefacts; you may need *individual* fitting, not just more people.

## Sources

- [[VL07 Interpreting Modeling]]
