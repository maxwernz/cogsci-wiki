---
type: concept
status: active
scope: global
classes: [Neural Coding]
projects:
domains: [neuroscience, cognitive science]
sources:
  - Classes/Neural Coding/raw/01_Introduction_NC.pdf
created: 2026-05-14
updated: 2026-05-14
---

# Neural Coding

## Short definition

Neural coding studies how neural activity represents information about stimuli, actions, internal states, or behaviorally relevant variables.

## General explanation

The central question is how a stimulus or latent variable is transformed into neural response patterns and how those response patterns can be read out. This naturally splits into encoding and decoding questions.

## Intuition

Neural activity is treated as a signal about something else: a stimulus, a decision, a movement direction, a prediction error, or an internal state.

## Formal definition

Encoding is often written as:

$$
P(\text{response}\mid\text{stimulus})
$$

Decoding is often written as:

$$
P(\text{stimulus}\mid\text{response})
$$

## Why it matters

Neural coding links biological data to computational theories of perception, action, learning, and cognition.

## Used in

- [[01 Introduction to Neural Coding]]
- [[Population Coding in Neural Coding]]
- [[Rate and Temporal Codes in Neural Coding]]

## Related concepts

- [[Encoding and Decoding]]
- [[Spike Train]]
- [[Tuning Curve]]
- [[Fisher Information]]

## Common confusions

- A neural code is not necessarily a literal codebook; it can be a statistical relationship between variables and responses.
- Single-cell selectivity does not by itself prove that the full code is local rather than distributed.

## Sources

- [[01 Introduction to Neural Coding]]
