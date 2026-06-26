---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: lecture_slides
raw_path: Classes/Cognitive Modeling/raw/Slides/VLCogMod_07_InterpretingModeling.pdf
created: 2026-06-09
updated: 2026-06-09
---

# VL07 — Interpreting Modeling

> Lecturer: Martin Butz. Further information cited on the slides: Farrell &
> Lewandowsky (2018) ch. 5 (pp. 105–122), ch. 10 (pp. 261–270), ch. 12
> (pp. 311–326), plus papers. Not in the VL2–5 reading list; the referenced
> papers (Bamber & van Santen 2000, Cohen/Sanborn/Shiffrin 2008, Estes 1956,
> Pitt & Myung 2002, Ratcliff 1979, etc.) are link-only.

## Summary

A major recap of quantitative cognitive modeling plus three deeper
interpretation themes. After re-stating the recipe (model types, LSE vs MLE,
optimisation, the model-comparison workflow), Butz adds: (1) **which data to
fit** — individuals vs averaged vs aggregated data, and the traps of averaging
(Simpson's paradox); (2) **over-fitting, cross-validation and generalization**,
including the **model-recovery procedure**; and (3) **identifiability,
testability, necessity and sufficiency** — culminating in the message that
**interpretability is the real goal**: a model that fits well is not
automatically *good*; you must explain *why* it fits and *which mechanisms*
matter.

## Key points

- **LSE vs MLE (recap).** LSE: focuses on fit (e.g. RMSE), conceptually simple,
  but no statistical properties → no statistical model comparison. MLE: based on
  the likelihood the model generates the data, gives goodness-of-fit and
  statistical comparison, at the cost of balancing fit against complexity.
- **Quantitative model-comparison workflow:** (1) specify each model's PDF/PMF;
  (2) fit by MLE; (3) compare — $\chi^2$ (likelihood-ratio) for *nested* models,
  AIC/BIC for *non-nested*; (4) bootstrap parameter variability.
- **Which data to fit?** Fitting individuals avoids averaging artefacts and
  exposes individual differences (different strategies, working-memory capacity)
  but needs enough data per person (rule of thumb: ≥10 data points, and ≥2× the
  number of parameters). Fitting the average gives "fit to the average", which
  can misrepresent every individual.
- **Simpson's paradox** (Berkeley 1973 admissions): an aggregate trend
  (apparent gender bias) *reverses* once you condition on department. The same
  reversal can corrupt cognitive modeling of averaged data. Averaging can also
  turn sharp individual choice points into a smooth sigmoid, and falsified the
  "power law of practice" (it is exponential at the individual level).
- **Hybrid options:** fit subgroups (clustering in parameter space), or fit
  **aggregate/binned** data via "vincentizing" (quantile bins of RTs), or
  multilevel/hierarchical modeling.
- **Model recovery procedure:** generate data from a *known* model, fit all
  candidate models, and count how often the true model wins — quantifies how
  confident a model-selection decision is. Closely related to the bootstrap.
- **Pitt & Myung (2002)** cautionary example: under RMSE, the most flexible
  (3-parameter) model almost always "wins", because RMSE ignores complexity —
  motivating AIC/BIC/MDL.
- **Identifiability & testability via the Jacobian.** A model's parameters are
  identifiable iff the rank $r$ of the Jacobian of its prediction function
  equals the number of parameters $m$; the model is testable iff $r$ is less
  than the number of independent data points $n$.
- **Necessity vs sufficiency.** A simpler model that fits as well as a complex
  one shows its mechanisms are *sufficient*. Showing mechanisms are *necessary*
  requires ruling out all alternatives (very hard); **ablation studies** give
  *local* necessity (turning a component off worsens the fit).
- **Interpretability is key.** The point of modeling is identifiable,
  interpretable mechanisms you can plausibly attribute to the brain — not a
  "winner-takes-all" leaderboard.

## Equations or formal definitions

**Sternberg (1975) recognition model** — a non-identifiability example:

$$RT = t_{op} + b\,s$$

- $s$: number of memorised items; $b$: comparison time per item (~35–40 ms);
  $t_{op}$: intercept (~380–500 ms) that *bundles* encoding time $a$ and
  response time $c$. Because only $a+c=t_{op}$ enters, $a$ and $c$ cannot be
  separated — the model is *testable* (it predicts a linear, old/new-equal RT)
  but $a$ and $c$ are *non-identifiable*.

**Identifiability / testability rules** (Jacobian $J_\theta$ of size $m\times n$,
rank $r$): identifiable iff $r=m$; testable iff $r<n$. Fixes for
non-identifiability: re-parameterise (e.g. replace $a,c$ by $t_{op}$); add
experimental constraints (fix a parameter); or gather another dependent variable.

## Methods, models, or theories

- [[Choosing Data to Fit (Individual vs Aggregate)]] (Simpson's paradox,
  vincentizing, multilevel modeling).
- [[Model Interpretation: Necessity and Sufficiency]] (ablation, model recovery).
- [[Parameter Identifiability and Model Testability]] (Jacobian-rank treatment).
- Recap of [[Model Selection Criteria (Deviance, AIC, BIC)]],
  [[Cross-Validation and Regularisation]], and [[The Bootstrap]].

## Local relevance

Bridges the fundamentals (VL2–5) to the concrete comparison in
[[VL08 Model Comparison Example]]. The data-choice and interpretability themes
are the "how to do this responsibly" layer on top of the recipe.

## Exam or project relevance

Be able to: explain Simpson's paradox and averaging artefacts and when to fit
individuals vs groups; describe the model-recovery procedure; state the
Jacobian-rank rules for identifiability and testability; give the Sternberg
non-identifiability example and the three fixes; and distinguish necessity from
sufficiency (and explain ablation studies). Several slides are flagged "not exam
relevant" (Estes averaging maths; multilevel side-note).

## Links to global concepts

- [[Model Selection: AIC and BIC]] (global)
- [[Cross-Validation]] (global)
- [[The Bootstrap]] (global)

## Open questions

- Averaging-effect figures (individual vs averaged curves) and the
  identifiability/testability flowchart are the high-value visuals; not extracted.
