---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [modeling, philosophy of science, methodology]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_07_InterpretingModeling.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Model Interpretation: Necessity and Sufficiency

## Short definition

After a model wins a comparison, interpretation asks *why*: whether its
mechanisms are **sufficient** to explain the data, whether they are **necessary**
(no alternative explains it as well), and what the fitted parameters reveal about
the underlying process.

## Intuition

A model that fits well is not automatically *good*. The scientific payoff is
explanation, not a leaderboard win: you want to say *which* mechanisms made it
fit and *why* the others failed, so you can plausibly claim the brain implements
those mechanisms. Sufficiency is "this is enough to do the job"; necessity is
"nothing else would do" — and necessity is far harder to establish.

## Explanation

**Sufficiency.** A model is sufficient if it accounts for the data "well enough"
(inevitably a bit arbitrary, since "well" is not precisely defined). The
**sufficiency argument**: a *simpler* model (fewer parameters, fewer assumed
processes) that fits *as well* as more complex models implies its processes are
*sufficient* to explain the data — no extra process is needed. This is Occam's
razor in mechanistic dress.

**Necessity.** A model is necessary if its mechanisms are *required* to account
for the data — i.e. there is *no alternative* that does equally well. Proving this
globally is very hard (you would have to rule out all conceivable alternatives).
What is achievable is **local necessity**: show that *within* a given model,
turning a component off (an **ablation study**) significantly worsens the fit —
evidence that *that* component is doing real work.

**Model recovery.** How confident can we be that our winning model really is best?
The **model-recovery procedure** quantifies this: generate many datasets from a
*known* model, fit all candidate models to each, and count how often the true
model wins (by MLE/AIC/BIC). If the true model is recovered most of the time, the
selection method is trustworthy for these models and data sizes; if not, your
"winner" may be an artefact. It is closely related to the [[The Bootstrap|bootstrap]]
(both repeatedly simulate and refit). The cautionary flip-side is **Pitt & Myung
(2002)**: under a complexity-blind measure like RMSE, the most flexible model
almost always "wins" regardless of truth — which is exactly why complexity-aware
criteria (AIC/BIC/MDL) and recovery checks are needed.

**Interpretability is the goal.** Cognitive models that fit well are not
necessarily good models. The point is to identify interpretable mechanisms,
processes, or representations that are *essential* to fitting the data, so that we
can expect the brain to implement something like them. Practical advice (Butz):
provide intuition and links to the literature; make modeling implications
explicit; avoid a simplistic "winner-takes-all" story; instead argue *"this model
fits better for these reasons"*, *"these mechanisms were key (shown by ablation)"*,
and *"the fitted parameters show participants apply mechanism XYZ in this specific
way"*.

## Worked example

[[VL08 Model Comparison Example]]: the Expectancy Valence model wins the
comparison — but the *interpretation* is what matters. Its three parameters
separate controls from patients: controls update carefully ($a\approx.03$),
weight wins and losses about equally ($w\approx.49$), and choose with moderate
exploration ($c\approx.09$); patients update erratically ($a\approx.3$, large SD),
over-weight gains ($w\approx.26$), and choose less consistently ($c\approx.01$).
This decomposes the clinical deficit into interpretable cognitive/motivational/
response components — the real scientific result, beyond "EV model won". An
ablation (e.g. fixing the loss weight $w$) tests whether differential win/loss
weighting is locally necessary.

## Role in this class or project

The capstone interpretive layer of [[VL07 Interpreting Modeling]], applied in
[[VL08 Model Comparison Example]]. It sits on top of the whole recipe: estimation
(VL2), GoF/selection (VL3), variability (VL4) — and asks what the surviving model
*means*.

## Exam, assignment, or project relevance

Distinguish sufficiency from necessity; state the sufficiency argument (simpler +
equally-good ⇒ sufficient); explain local necessity via ablation studies;
describe the model-recovery procedure and how it relates to the bootstrap; and
explain why a good fit is not enough (Pitt & Myung; interpretability as the goal).

## Related global concepts

- [[Model Selection: AIC and BIC]]
- [[The Bootstrap]]

## Related local pages

- [[Parameter Identifiability and Model Testability]]
- [[Choosing Data to Fit (Individual vs Aggregate)]]
- [[The Three-Step Recipe for Modeling Data]]

## Common confusions

- **"Best fit = best model."** Complexity-blind measures favour flexible models
  (Pitt & Myung); and a good fit does not establish necessity or interpretability.
- **Sufficiency vs necessity.** Sufficiency = "enough"; necessity = "nothing else
  works" (only *local* necessity, via ablation, is practically attainable).
- **"Model recovery = bootstrap."** Related (both simulate+refit) but recovery
  asks *which model* wins, not the variability of one model's parameters.

## Sources

- [[VL07 Interpreting Modeling]]
- [[VL08 Model Comparison Example]]
