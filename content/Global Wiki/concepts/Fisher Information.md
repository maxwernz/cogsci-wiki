---
type: method
status: active
scope: global
classes: [Neural Coding]
projects:
domains: [statistics, neuroscience, cognitive science]
sources:
  - Classes/Neural Coding/raw/04_Tuning_Curves.pdf
  - Classes/Neural Coding/raw/05_Fisher_and_MDE.pdf
created: 2026-05-14
updated: 2026-05-14
---

# Fisher Information

## Short definition

Fisher information measures how sensitively a probability distribution changes with a parameter.

## General explanation

If observations are drawn from $p(X\mid\theta)$, Fisher information quantifies how much the observation $X$ can tell us locally about $\theta$. It is the variance of the score, the derivative of log likelihood.

## Intuition

If a small parameter change strongly changes the likelihood, the observation carries high Fisher information about that parameter.

## Formal definition

Score:

$$
S_X(\theta)=\frac{\partial}{\partial\theta}\log p(X\mid\theta)
$$

Fisher information:

$$
J(\theta)=E[S_X^2(\theta)\mid\theta]
$$

Under regularity assumptions:

$$
J(\theta)=-E\left[\frac{\partial^2}{\partial\theta^2}\log p(X\mid\theta)\middle|\theta\right]
$$

Cramer-Rao bound:

$$
\mathrm{Var}(\hat{\theta})\geq \frac{1}{J(\theta)}
$$

## Why it matters

Fisher information links probability models to limits on estimation precision. In neural coding, it is used to analyze how accurately stimuli can be decoded from noisy responses.

## Used in

- [[Fisher Information in Neural Coding]]
- [[05 Fisher Information and Minimal Discriminator Error]]
- [[Minimal Discriminator Error in Neural Coding]]

## Related concepts

- [[Encoding and Decoding]]
- [[Tuning Curve]]

## Common confusions

- Fisher information is local in parameter space.
- It describes information in the statistical model, not necessarily the information used by a biological decoder.

## Sources

- [[04 Tuning Curves and Encoding-Decoding]]
- [[05 Fisher Information and Minimal Discriminator Error]]
