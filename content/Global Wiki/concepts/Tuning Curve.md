---
type: concept
status: active
scope: global
classes: [Neural Coding]
projects:
domains: [neuroscience, statistics]
sources:
  - Classes/Neural Coding/raw/01_Introduction_NC.pdf
  - Classes/Neural Coding/raw/04_Tuning_Curves.pdf
  - Classes/Neural Coding/raw/05_Fisher_and_MDE.pdf
created: 2026-05-14
updated: 2026-05-14
---

# Tuning Curve

## Short definition

A tuning curve describes how an expected response changes as a function of a stimulus or task variable.

## General explanation

In neuroscience, a tuning curve is often written as $f(s)$, where $s$ is a stimulus and $f(s)$ is the expected firing rate, spike count, or response strength. Noise around this expected response defines a response distribution $p(r\mid f(s))$.

## Intuition

A tuning curve says what a neuron or population tends to respond to, and how strongly.

## Formal definition

Generic encoding model:

$$
s \mapsto f(s), \qquad r \sim p(r\mid f(s))
$$

For Poisson response noise:

$$
p(r\mid f(s))=\frac{f(s)^r}{r!}e^{-f(s)}
$$

## Why it matters

Tuning curves connect stimulus representation, decoding, Fisher information, and discrimination performance.

## Used in

- [[01 Introduction to Neural Coding]]
- [[Tuning Curves in Neural Coding]]
- [[Fisher Information in Neural Coding]]

## Related concepts

- [[Encoding and Decoding]]
- [[Fisher Information]]
- [[Neural Coding]]

## Common confusions

- A tuning curve is not the whole response distribution unless the noise model is also specified.
- A sharp tuning curve is not always globally better, especially in high-dimensional population codes.

## Sources

- [[01 Introduction to Neural Coding]]
- [[04 Tuning Curves and Encoding-Decoding]]
- [[05 Fisher Information and Minimal Discriminator Error]]
