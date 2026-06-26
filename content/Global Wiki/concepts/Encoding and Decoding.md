---
type: concept
status: active
scope: global
classes: [Neural Coding]
projects:
domains: [neuroscience, statistics, cognitive science]
sources:
  - Classes/Neural Coding/raw/01_Introduction_NC.pdf
  - Classes/Neural Coding/raw/04_Tuning_Curves.pdf
created: 2026-05-14
updated: 2026-05-14
---

# Encoding and Decoding

## Short definition

Encoding asks how variables generate responses; decoding asks how variables can be inferred from responses.

## General explanation

In neural coding, encoding usually models $P(r\mid s)$, the distribution of neural response $r$ given stimulus $s$. Decoding estimates $s$ from $r$, often through a decoder $\hat{s}(r)$ or posterior $P(s\mid r)$.

## Intuition

Encoding runs from world to activity. Decoding runs from activity back to the variable being represented.

## Formal definition

Encoding:

$$
P(r\mid s)
$$

Decoding:

$$
P(s\mid r)
$$

For squared error, the ideal observer is:

$$
\hat{s}_{\mathrm{MSE}}(r)=E[s\mid r]
$$

## Why it matters

This distinction organizes modeling questions across neuroscience, cognitive science, psychophysics, and machine learning.

## Used in

- [[01 Introduction to Neural Coding]]
- [[04 Tuning Curves and Encoding-Decoding]]
- [[Tuning Curves in Neural Coding]]
- [[Minimal Discriminator Error in Neural Coding]]

## Related concepts

- [[Neural Coding]]
- [[Tuning Curve]]
- [[Fisher Information]]

## Common confusions

- A good encoding model does not automatically imply an easy or biologically plausible decoder.
- A decoder can be used as an analysis tool without claiming that the brain uses that exact decoder.

## Sources

- [[01 Introduction to Neural Coding]]
- [[04 Tuning Curves and Encoding-Decoding]]
