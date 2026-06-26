---
type: concept
status: active
scope: global
classes: [Neural Coding]
projects:
domains: [statistics, neuroscience]
sources:
  - Classes/Neural Coding/raw/04_Tuning_Curves.pdf
created: 2026-05-14
updated: 2026-05-14
---

# Fano Factor

## Short definition

The Fano factor is the ratio of variance to mean.

## General explanation

For a count variable with mean $\mu$ and variance $\sigma^2$, the Fano factor is:

$$
F=\frac{\sigma^2}{\mu}
$$

For a Poisson distribution, $F=1$. Values larger than $1$ indicate overdispersion relative to Poisson variability.

## Intuition

The Fano factor asks whether counts fluctuate as much as, less than, or more than a Poisson model predicts.

## Formal definition

$$
F=\frac{\mathrm{Var}(X)}{E[X]}
$$

## Why it matters

In neural data, Fano factors help evaluate whether Poisson noise is a reasonable response-noise model.

## Used in

- [[04 Tuning Curves and Encoding-Decoding]]
- [[Firing Rate Variability in Neural Coding]]

## Related concepts

- [[Poisson Process]]
- [[Tuning Curve]]

## Common confusions

- $F>1$ does not identify one unique mechanism; it only shows overdispersion relative to a Poisson baseline.
- Time-varying rates can increase observed count variance even when conditional spike generation is Poisson.

## Sources

- [[04 Tuning Curves and Encoding-Decoding]]
