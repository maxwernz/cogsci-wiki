---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: paper
raw_path: Classes/Cognitive Modeling/raw/Literature/BecharaDamasioTranelDamasio1997DecidingAdvantageouslyBeforeKnowingTheAdvantageousStrategy.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Bechara, Damasio, Tranel & Damasio (1997) — Deciding Advantageously Before Knowing the Advantageous Strategy

> Referenced directly in [[VL08 Model Comparison Example]] (Butz). This is the
> *empirical* origin of the Iowa Gambling Task; the cognitive *models* fit to it
> come from [[Busemeyer and Stout 2002 Cognitive Decision Models]].

## Summary

The founding study of the **Iowa Gambling Task (IGT)**. Participants repeatedly
draw cards from four decks; two are advantageous (modest wins, small losses, net
gain over time) and two disadvantageous (bigger immediate wins but occasional
large losses, net loss over time). Healthy participants gradually learn to
prefer the advantageous decks; patients with **ventromedial prefrontal cortex
(VMPFC) damage** keep choosing the disadvantageous decks. The striking finding
that gives the paper its title: healthy participants began to generate
**anticipatory skin-conductance responses (SCRs)** before risky decks *before*
they could verbally state which decks were bad — they were "deciding
advantageously before knowing the advantageous strategy". VMPFC patients failed
to develop these anticipatory signals. This is a cornerstone of the **somatic
marker hypothesis**: emotional/bodily signals guide advantageous decision-making.

## Key points

- The IGT operationalises real-life decision-making under uncertainty (immediate
  reward vs delayed punishment) in the lab.
- Behavioural deficit: VMPFC patients persist with disadvantageous decks despite
  mounting losses — interpreted as an inability to anticipate long-term negative
  consequences.
- Physiological dissociation: anticipatory SCRs precede explicit knowledge in
  controls; patients lack them.
- The behavioural data are *confounded*: poor performance could reflect a
  deficit in memory, contingency learning, win/loss weighting, or impulsive
  choice — which is exactly why cognitive modeling (VL8) is needed to decompose
  it.

## Local relevance

VL08 uses the IGT as the task for an end-to-end model comparison. The clinical
ambiguity ("which process is broken?") is the motivation for fitting and
comparing the strategy-switching, Bayesian-utility, and expectancy-valence
models, and for interpreting their parameters across patient vs control groups.

## Exam or project relevance

Know the task structure (4 decks, advantageous vs disadvantageous) and the core
finding (patients persist with bad decks; anticipatory SCRs precede explicit
knowledge in controls). The *modeling* detail lives in [[VL08 Model Comparison Example]].

## Links to global concepts

- [[Model Selection: AIC and BIC]] (global)

## Open questions

- None for the course's purposes; the paper is used as task background, not as a
  modeling source.
