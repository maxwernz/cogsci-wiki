---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: lecture_slides
raw_path: Classes/Cognitive Modeling/raw/Slides/VLCogMod_01_Introduction.pdf
created: 2026-06-09
updated: 2026-06-09
---

# VL01 — Introduction

## Summary

The opening lecture (Felix Wichmann, with input from Martin Butz) sets up the
course and argues *why* science needs formal models at all. Its central claim:
verbal theorizing alone is not enough once a field matures, because words hide
internal inconsistencies and gaps. A running computational model is a
"sufficiency proof" — if you can build it and it works, the idea it is based on
is at least internally coherent and complete. The lecture then illustrates the
*power* of quantitative models with an extended case study from the lecturer's
own lab: comparing deep neural networks (ANNs) to the human visual system.

The big organisational message: this course is a *core course* (Grundlagen /
Pflicht) for a cohort with very mixed backgrounds (maths/CS, psychology,
biology), so it is calibrated to give everyone a shared minimum of statistical
and modeling skills. Lectures 2–5 (Wichmann) cover modeling *fundamentals* and
are the conceptual backbone; the reading list for VL2–5 is the most important
preparation document.

## Key points

- **Why model?** Verbal theories can be "flawed by internal inconsistencies,
  logical contradictions, theoretical weaknesses and gaps" (Fum, Missier &
  Stocco, 2007). A computational model forces you to specify every detail and
  lets you derive predictions by simulation. Mathematical models also benefit
  from "the deductive power of mathematics" and protect against faulty intuition
  (Ulrich, 2009).
- **But not a silver bullet.** Verbal theories still matter: they are easy to
  communicate and are the only option when a field is young and ideas are still
  vague. Mathematical models need a "robust data basis" to be worthwhile.
- **Goals of cognitive science:** to *describe*, *predict*, and ultimately
  *explain* behaviour in complex tasks (perception, memory, attention, decision,
  reasoning, learning). Feynman's motto: "What I cannot create, I do not
  understand."
- **A taxonomy of models** (reused by Butz in VL7): descriptive (qualitative
  "box-and-arrow", quantitative/mathematical, normative), process models
  (systematic vs iterative), neural models, developmental models.

## Methods, models, or theories

**Case study — ANNs as models of human vision.** The lecturer's group compared
modern convolutional networks (AlexNet, GoogLeNet, VGG-16, ResNet-50) to human
observers on the *same* images, under controlled viewing (brief presentation,
masking). Findings:

- ResNet-50 reaches *super-human* accuracy on clean and on greyscale+uniform-noise
  ImageNet images — but shows a *striking generalisation failure*: trained on
  salt-and-pepper noise and tested on uniform noise, it drops to chance, whereas
  humans generalise across distortions (Geirhos et al., 2018).
- ANNs were assumed to recognise objects by *shape* (like humans). The
  texture–shape cue-conflict experiment (Geirhos et al., 2019) showed
  ImageNet-trained CNNs are instead heavily *texture-biased*: a cat-shaped image
  with elephant texture is labelled "elephant".

**Why this is the lecture's punchline:** having a well-performing *quantitative*
model is exactly what let the researchers pose and answer sharp hypotheses
("are ANNs as robust as humans?", "do they use shape?"). Without a runnable
model producing behaviour you can measure, the discovery that ANNs process
visual information differently would have been impossible. This is "the power of
models in science" in action.

## Local relevance

This lecture frames the whole course: models are tools for turning vague verbal
theory into testable, quantitative claims. The taxonomy of model types recurs in
[[VL07 Interpreting Modeling]]. The course structure (VL2 estimation → VL3
goodness-of-fit → VL4 variability → VL5 Bayes) is the spine captured in
[[The Three-Step Recipe for Modeling Data]].

## Exam or project relevance

Conceptual, not formal. Be able to argue *why* computational models add value
over verbal theory (sufficiency proof; deductive power; protection from faulty
intuition) and *when* verbal theory is still appropriate (young field, vague
ideas, thin data). The vision case study is a memorable example of "model as
hypothesis-testing tool".

## Links to global concepts

- [[Marr's Levels of Analysis]] (developed fully in [[VL05 Bayes]])

## Open questions

- The vision case study figures (generalisation matrix, texture–shape conflict)
  are high-value visuals; not yet extracted to `outputs/images/`.
