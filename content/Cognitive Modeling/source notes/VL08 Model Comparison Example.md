---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: lecture_slides
raw_path: Classes/Cognitive Modeling/raw/Slides/VLCogMod_08_ModelComparisonExample.pdf
created: 2026-06-09
updated: 2026-06-09
---

# VL08 — Model Comparison (Example)

> Lecturer: Martin Butz. Directly referenced literature (ingested per your rule —
> cited on the slides): Bechara, Damasio, Tranel & Damasio (1997)
> ([[Bechara et al 1997 Deciding Advantageously]]) and Busemeyer & Stout (2002)
> ([[Busemeyer and Stout 2002 Cognitive Decision Models]]). Also cited:
> Bechara & Damasio (2005), Sutton & Barto (1998), Tolman (1948).

## Summary

A fully worked, end-to-end **quantitative model comparison** on a single
cognitive task — the concrete payoff of VL2–VL7. The task is the **Iowa Gambling
Task** (Bechara et al., 1997): choosing repeatedly from four card decks, two
advantageous and two disadvantageous, to study decision-making deficits (e.g.
prefrontal patients keep choosing disadvantageous decks). Three cognitive models
(plus a baseline) are fit to simulated data by **maximum likelihood**, compared
by **$G^2$**, **likelihood-ratio ($\chi^2$) tests**, **BIC**, and a
**generalization/cross-validation** criterion, and finally **interpreted** via a
parameter analysis distinguishing controls from patients. The **Expectancy
Valence model** wins on every criterion.

## Key points

- **The task.** Four decks; each card gives a win *and* a loss. Two decks are
  advantageous (small immediate wins, net +$2.5 per 10 cards); two are
  disadvantageous (larger immediate wins, net −$2.5 per 10 cards). Dependent
  measure: proportion of cards drawn from advantageous decks. The modeling
  question: *which cognitive process* explains poor performance — memory,
  long-term contingency learning, win/loss balancing, or impulsive choice?
- **Three candidate models** (after Busemeyer & Stout, 2002):
  1. **Strategy-switching model** (4 params $a,b,q,r$): a heuristic that switches
     from a high-immediate-payoff strategy to the advantageous strategy after big
     losses, via a logistic function of accumulated losses $S(t)$.
  2. **Bayesian utility model** (5 params): Bayes-updates loss probabilities,
     applies a power-law utility to net payoff, chooses the max-expected-utility
     deck (q-greedy). *Acknowledged to be poorly designed; details non-exam.*
  3. **Expectancy Valence model** (3 params $w,a,c$): integrates wins/losses into
     a *valence*, learns expected valences with a delta (reinforcement-learning)
     rule, and chooses probabilistically via a softmax. **The winner.**
  - **Baseline** (3 params): a multinomial with constant deck probabilities
    (predicts flat lines); cognitive models must beat it to be worth anything.
- **Fitting.** 60 participants × 250 trials → enough for *individual* fitting.
  Each model gives a per-trial PMF, so the sequence likelihood is computable;
  optimisation (simplex / simulated annealing) maximises it.
- **Goodness-of-fit currency = $G^2$** ($-2\ln L$): smaller is better ("badness
  of fit").
- **Comparison results.** $\chi^2$ test on the EV model's free vs fixed weight
  $w$: $\Delta G^2 = 0.73 < 3.84$ → keep the simpler model. BIC favours the
  Expectancy Valence model (the Bayesian utility model is *worse than baseline*).
  The generalization criterion (fit first 150 trials, test on last 100) agrees:
  EV generalises better for 100% of controls.
- **Parameter interpretation.** EV parameters separate groups: controls show
  careful updating ($a\approx.03$), balanced win/loss weighting ($w\approx.49$),
  moderate exploration ($c\approx.09$); patients show erratic updating
  ($a\approx.3$, large SD), gain-biased weighting ($w\approx.26$), and less
  focused choice ($c\approx.01$). This *interprets* the deficit, not just ranks
  models.

## Equations or formal definitions

**Expectancy Valence model.** Valence of an outcome:

$$v(t) = (1-w)\,R(D_t) + w\,L(D_t)$$

Delta-rule update of the chosen deck's expected valence:

$$Ev(D_t) \leftarrow Ev(D_t) + a\big(v(t) - Ev(D_t)\big) = (1-a)Ev(D_t) + a\,v(t)$$

Softmax (strength-ratio) choice:

$$P(D_j, t{+}1) = \frac{e^{c\,Ev(D_j)}}{\sum_{k} e^{c\,Ev(D_k)}}$$

- $R,L$: reward and loss; $w\in(0,1)$: loss-vs-gain weight; $a$: learning rate;
  $c$: choice sensitivity (softmax temperature, higher = greedier). The term
  $v(t)-Ev(D_t)$ is exactly the **temporal-difference error** of reinforcement
  learning.

**$G^2$ and BIC comparison** (worked on the slides):

$$G^2 = -2\ln L, \qquad 2\,\mathrm{BIC}_{AB} = (G^2_B - G^2_A) - (k_B-k_A)\ln N$$

- A 2- vs 3-parameter EV comparison gave $G^2_B-G^2_A = 0.73$, $N=250$; the BIC
  difference favoured the simpler model with a Bayes factor ≈ 9.4 (considerable
  evidence). Jeffreys' scale: 1–3 weak, 3–10 medium, 10+ strong evidence.

## Methods, models, or theories

- **Iowa Gambling Task** and three decision models (strategy-switching, Bayesian
  utility, expectancy valence) — the latter linked to reinforcement learning
  (Sutton & Barto, 1998; Tolman, 1948).
- The full comparison pipeline reuses [[Maximum Likelihood Estimation in Cognitive Modeling]], [[Model Selection Criteria (Deviance, AIC, BIC)]],
  [[Cross-Validation and Regularisation]], [[The Bootstrap]], and
  [[Model Interpretation: Necessity and Sufficiency]].

## Local relevance

The capstone worked example for the whole course: it instantiates all three
recipe steps plus interpretation, on data based on real clinical research
(Bechara/Damasio somatic-marker work; Busemeyer & Stout's decomposition).

## Exam or project relevance

Be able to walk through the comparison logic: per-trial PMF → sequence
likelihood → $G^2$ → $\chi^2$ for nested, BIC for non-nested → generalization
check → parameter interpretation. Know the Expectancy Valence model's three
equations and the meaning of $w,a,c$, and that the delta-rule term is the RL
prediction error. The Bayesian utility model details are explicitly non-exam.

## Links to global concepts

- [[Model Selection: AIC and BIC]] (global)
- [[The Bootstrap]] (global)

## Open questions

- The per-model simulation plots and the BIC/generalization comparison tables
  are the high-value visuals; not extracted.
