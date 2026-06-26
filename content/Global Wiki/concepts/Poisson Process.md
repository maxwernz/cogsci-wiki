---
type: model
status: active
scope: global
classes: [Neural Coding]
projects:
domains: [probability, stochastic processes, neuroscience]
sources:
  - Classes/Neural Coding/raw/02_Homogeneous_Poisson_Process_NC.pdf
  - Classes/Neural Coding/raw/03_Inhomogeneous_Poisson_updated.pdf
created: 2026-05-14
updated: 2026-05-14
---

# Poisson Process

## Short definition

A Poisson process is a point-process model in which event counts over intervals follow Poisson distributions, with independent increments.

## General explanation

In neural coding, Poisson processes are used as baseline models for spike trains. A homogeneous Poisson process has constant rate $\lambda$; an inhomogeneous Poisson process has time-varying rate $\lambda(t)$.

## Intuition

The process describes random event times where the expected number of events is controlled by a rate.

## Formal definition

For a homogeneous Poisson process:

$$
\Delta L_j \sim \mathrm{Poisson}(\lambda\Delta t_j)
$$

For an inhomogeneous Poisson process:

$$
\Delta L_j \sim \mathrm{Poisson}\left(\int_{t_{j-1}}^{t_j}\lambda(t)\,dt\right)
$$

The Poisson count probability is:

$$
P(k\mid\mu)=\frac{\mu^k}{k!}e^{-\mu}
$$

## Why it matters

Poisson processes provide a mathematically tractable model of spike counts and spike times, making likelihoods, simulation, and variability analysis possible.

## Used in

- [[Homogeneous Poisson Process in Neural Coding]]
- [[Inhomogeneous Poisson Process in Neural Coding]]
- [[Firing Rate Variability in Neural Coding]]

## Related concepts

- [[Spike Train]]
- [[Fano Factor]]

## Common confusions

- Poisson spike generation is a model assumption, not a universal biological law.
- A time-varying Poisson process can model rate modulation, but it does not automatically capture refractory effects, correlations, or overdispersion.

## Sources

- [[02 Homogeneous Poisson Process]]
- [[03 Inhomogeneous Poisson Process]]
