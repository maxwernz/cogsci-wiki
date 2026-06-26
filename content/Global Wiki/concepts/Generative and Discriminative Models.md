---
type: comparison
status: active
scope: global
classes: [Kognitive Architekturen, Understanding LLMs]
projects:
domains: [machine learning, probabilistic modeling]
sources:
created: 2026-06-17
updated: 2026-06-17
---

# Generative and Discriminative Models

## Short definition

Two basic strategies for inferring a class or cause $c$ from data $o$. A
**discriminative** model learns the boundary $p(c\mid o)$ directly (which class
for these data?). A **generative** model learns how data are produced —
$p(o\mid c)$ and the prior $p(c)$ — and inverts the question with Bayes' rule.

## General explanation

Given observations $O$ and classes/states $C$:

- **Discriminative model.** Estimates $p(c\mid o)$ directly from training data.
  Typical example: a feed-forward deep neural network classifier. It is
  data-driven / bottom-up and often very accurate at classifying, but it has *no
  model of the world*: it cannot generate data, fill in missing parts, or form an
  expectation about what it should see.

- **Generative model.** Estimates the joint distribution
  $p(o,c)=p(o\mid c)\,p(c)$ from class-conditional distributions $p(o\mid c)$ and
  priors $p(c)$. To classify, it inverts via **Bayes' rule** to $p(c\mid o)$.
  Because it describes *how* data arise, it can **generate samples**, **predict /
  filter / focus** perception, **complete** occluded inputs, and **predict** the
  next state — abilities a pure classifier lacks.

Why model generatively at all? Because the world is not fully observable —
ignorance of dependencies, sheer complexity, physical randomness, and
measurement noise all force reasoning under uncertainty, and probability theory
with Bayes' rule is the principled tool for that. The trade-off is the classic
one: discriminative models tend to classify more accurately for a given amount of
data (they spend all their capacity on the decision boundary), while generative
models *do more* and degrade more gracefully with missing data, at the cost of
having to model the full data distribution. The concrete machinery of generative
models includes [[Bayesian Network|Bayesian networks]] (discrete) and
[[Gaussian Mixture Model|Gaussian mixture models]] (continuous); modern deep
generative models (VAEs, diffusion models, autoregressive language models) are
the same idea scaled up.

## Intuition

Picture two animal experts. The **discriminative** expert has seen thousands of
photos and learned only *where to draw the line*: "stripes + hooves → zebra." It
answers fast but cannot *describe or draw* a zebra. The **generative** expert
holds an *inner model* of what a zebra looks like; it can imagine one and predict
which pixels to expect, then reason backward: "these data fit my zebra model
best." Top-down perception is generative — the brain expects something and checks
whether the data fit.

## Formal definition

$$
\text{discriminative: } p(c\mid o)\ \text{learned directly};\qquad
\text{generative: } p(o,c)=p(o\mid c)\,p(c),\quad
p(c\mid o)=\frac{p(o\mid c)\,p(c)}{\sum_k p(o\mid c_k)\,p(c_k)}.
$$

The **MAP class** is $c_{\max}=\arg\max_c p(c\mid o)=\arg\max_c p(o\mid c)\,p(c)$
(the denominator is the same for all $c$). Symbols: $o$ observation, $c$
class/state, $p(c)$ prior, $p(o\mid c)$ likelihood, $p(c\mid o)$ posterior.

## Worked example

**Zebra detection from a stripe detector.** Prior $p(\text{zebra})=0.02$. A binary
stripe detector gives $p(o{=}\text{true}\mid\text{zebra})=0.8$ and
$p(o{=}\text{true}\mid\neg\text{zebra})=0.1$. On a positive detection:

$$p(\text{zebra}\mid o)=\frac{0.8\cdot0.02}{0.8\cdot0.02+0.1\cdot0.98}\approx0.14.$$

Belief rises from 2% to ~14% — a real improvement, but the low prior and many
false positives keep it far from certainty. That is generative reasoning:
$p(o\mid c)$ and $p(c)$ modelled separately, then combined by Bayes. A
discriminative net would have learned $p(c\mid o)$ directly, never separating the
detector from the prior.

## Why it matters

The generative/discriminative distinction organises much of machine learning and
of theories of perception: it explains the trade-off between raw classification
accuracy and the ability to imagine, complete, and predict, and it underlies the
top-down/bottom-up split in models of the brain.

## Used in

- [[Generative und diskriminative Modelle]] (Kognitive Architekturen: top-down
  perception as generative inference)
- [[Bottom-Up Bildverarbeitung]] (the discriminative / bottom-up side)
- [[Autoregressive Language Models in Understanding LLMs]] (deep generative model
  of token sequences)

## Related concepts

- [[Bayes' Theorem]]
- [[Bayesian Inference]]
- [[Maximum Likelihood Estimation]]
- [[Predictive Coding]]

## Common confusions

- **Generative ≠ better.** Discriminative models often classify more accurately;
  generative models *can do more* (generate, complete, predict).
- **"Generative" does not mean "made up."** It means modelling $p(o\mid c)$ — how
  data arise from causes — and inverting with Bayes.
- **Do not forget the prior.** A high likelihood alone is not enough; a small
  prior (rare class) strongly pulls the posterior down.

## Sources

- Bishop, *Pattern Recognition and Machine Learning*, ch. 1, 4.
