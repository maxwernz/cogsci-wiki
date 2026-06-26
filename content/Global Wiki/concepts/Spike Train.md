---
type: concept
status: active
scope: global
classes: [Neural Coding]
projects:
domains: [neuroscience, stochastic processes]
sources:
  - Classes/Neural Coding/raw/02_Homogeneous_Poisson_Process_NC.pdf
created: 2026-05-14
updated: 2026-05-14
---

# Spike Train

## Short definition

A spike train is a sequence or set of action-potential times observed over a time interval.

## General explanation

Spike trains are often represented by spike-time sets, delta functions, or counting functions. These representations make it possible to model neural activity as a point process.

## Intuition

Instead of tracking the full voltage trace, a spike train keeps the event times that matter for communication between neurons.

## Formal definition

Spike-time set:

$$
\mathcal{S}_n(0,T)=\{t_1^*,\ldots,t_n^*:t_k^*\in(0,T)\}
$$

Delta-function representation:

$$
a(t)=\sum_{t_k^*\in\mathcal{S}_n(0,T)}\delta(t-t_k^*)
$$

Counting function:

$$
L(t)=\sum_{t_k^*\in\mathcal{S}_n(0,T)}\Theta(t-t_k^*)
$$

## Why it matters

Spike trains are a primary data type in systems neuroscience and a natural object for point-process models.

## Used in

- [[Spike Train Representation in Neural Coding]]
- [[02 Homogeneous Poisson Process]]
- [[03 Inhomogeneous Poisson Process]]

## Related concepts

- [[Poisson Process]]
- [[Neural Coding]]

## Common confusions

- A spike train is not a continuous firing rate; a rate is a summary or model of event intensity.
- A counting function and a delta-function representation encode the same spike times in different mathematical forms.

## Sources

- [[02 Homogeneous Poisson Process]]
