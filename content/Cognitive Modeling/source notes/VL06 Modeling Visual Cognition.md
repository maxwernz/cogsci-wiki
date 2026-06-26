---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: lecture_slides
raw_path: Classes/Cognitive Modeling/raw/Slides/VLCogMod_06_VisCog.pdf
created: 2026-06-09
updated: 2026-06-09
---

# VL06 — Modeling Visual Cognition

> Not covered by the VL2–5 reading list. Supplementary literature cited on the
> slides (link-only — not ingested): Adelson & Bergen (1991), Campbell & Robson
> (1968), Watson & Ahumada (2005), Schütt & Wichmann (2017), Blakeslee & McCourt
> (2004), Blakeslee et al. (2009), Betz et al. (2015).

## Summary

The first *applied* lecture: it takes the abstract three-step recipe (VL2–4) and
runs it on real models of vision. Two case studies contrast **quantitative** and
**qualitative** modeling. (1) **Spatial vision** — detecting and discriminating
simple patterns — yields a fully *quantitative* image-computable model fit by
maximum likelihood. (2) **Lightness/brightness** perception can currently only
be modelled *qualitatively*, because the "data" (subjective appearance) cannot
be measured precisely enough for ML/RMSD fitting. The unifying technical lesson:
many vision models share three ingredients — **linear filters at multiple
scales, convolution, and non-linear (divisive) normalisation** — which mirror
the early primate visual system.

## Key points

- **Applying the recipe to spatial vision.** The Schütt & Wichmann (2017) model:
  decompose the image with **log-Gabor filters** (12 centre spatial frequencies
  × 8 orientations) → **divisive normalisation** (a nonlinearity dividing each
  response by a pooled response, 5 free params: $p,q,C,g_{sf},g_o$) →
  **population decoding** to a $d'$ (7 free parameters total). Parameters fit by
  **ML** on a probabilistic ($d'$) model. It reproduces the contrast sensitivity
  function (CSF) and contrast-discrimination ("dipper") data.
- **Only step 1 so far.** Goodness-of-fit is currently assessed "by eye" and
  there are no confidence intervals yet — steps 2 and 3 (proper GoF + CIs) are
  ongoing PhD work. Several choices (12 bands, 8 orientations, log-Gabor shape)
  are *arbitrary* and can only be compared once GoF/CI machinery exists. This is
  a concrete illustration of *why* VL3–VL4 matter.
- **When only qualitative modeling is possible.** For lightness/brightness the
  dependent variable is *subjective experience*, measured by inconsistent methods
  (matching, adjustment, triplets) with large individual and method differences.
  No ML possible; we accept a model that merely predicts "area A looks brighter
  than B". Qualitative modeling is the only option when a problem is not yet
  understood well enough to quantify.
- **The ODOG model** (oriented difference-of-Gaussians, Blakeslee & McCourt)
  predicts brightness illusions qualitatively; Betz et al. (2015) showed noise
  masking exposes weaknesses of such spatial-filtering accounts.
- **Common computational motifs** (filters / convolution / nonlinear
  normalisation) are found in the early visual system: linear receptive fields,
  retinotopy, nonlinear activation, divisive normalisation.

## Equations or formal definitions

Two-alternative forced-choice probability from the decoded $d'$:

$$p_{2AFC} = \int_{0}^{\infty} N\!\left(\frac{d'}{\sqrt 2}, 1\right)$$

- $d'$: the model's discriminability for the stimulus pair; the integral of a
  unit-variance Gaussian gives the predicted proportion correct, which is the
  *probabilistic model* enabling ML fitting (link to
  [[Maximum Likelihood Estimation in Cognitive Modeling]]).

## Methods, models, or theories

- **Image-computable spatial-vision model** (filter bank → normalisation →
  decoding), fit by ML — a worked application of [[The Three-Step Recipe for Modeling Data]] (step 1 only).
- **Qualitative modeling** as a legitimate strategy (contrast with quantitative).
- **ODOG** spatial-filtering model of brightness.

## Local relevance

Concretises the recipe and shows its limits: a state-of-the-art model that has
only completed step 1, plus a domain (brightness) where steps 1–3 are impossible
and qualitative modeling rules. Connects to VL1's model taxonomy (quantitative
vs qualitative) and to VL3's point that comparing model variants *requires* GoF
machinery.

## Exam or project relevance

Likely lighter than VL2–5 for the exam (an applied illustration). Worth knowing:
the three shared ingredients of vision models (filters/convolution/normalisation);
why ML fitting is possible for detection/discrimination ($d'$ data) but not for
subjective brightness; and the legitimate role of qualitative modeling.

## Links to global concepts

- [[Maximum Likelihood Estimation]] (global)

## Open questions

- The slides for lightness illusions (slides 19–24) are images with no text;
  the ODOG/Betz figures would be the high-value visuals if extracted.
