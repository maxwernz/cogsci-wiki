---
type: theory
status: active
scope: global
classes: [Cognitive Modeling]
projects:
domains: [cognitive science, neuroscience, philosophy of science]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_05_Bayes.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Marr's Levels of Analysis

## Short definition

David Marr's claim that any complex information-processing system must be
understood at three loosely-coupled levels: computational (what problem is solved
and why), algorithmic (what representations and procedures solve it), and
implementational (how it is physically realised).

## General explanation

Marr (1982) argued you cannot understand a complex information-processing system
purely bottom-up (from neurophysiology or behaviour); you first need a theory of
*what the system is trying to do*. He proposed three levels of description:

1. **Computational level** — *what* is the goal of the computation and *why*?
   The abstract problem and its optimal (rational) solution. In Bayesian terms,
   this is the **ideal-observer / rational analysis**.
2. **Algorithmic level** — *how*? The representations used and the algorithm that
   transforms input to output.
3. **Implementational level** — *with what*? The physical substrate (neurons,
   circuits, hardware) realising the algorithm.

The levels are **coupled but only loosely**: the choice of algorithm is
influenced by the goal and by the hardware, but each level can be studied with
considerable independence. A key consequence for cognitive modeling: you can
endorse a "Bayesian" account at one level (e.g. computational/ideal-observer)
without committing to it at the others — a frequent source of confusion in the
[[Bayesian Inference|Bayesian brain]] debate, since a computational-level Bayesian
model does *not* require neurons to represent distributions or apply Bayes' rule.

## Intuition

Understanding a pocket calculator: the *computational* level says "it adds
numbers" (and why that's useful); the *algorithmic* level says "it uses
binary addition with carry"; the *implementational* level says "transistors in
these logic gates". Knowing the transistors alone never tells you it's *for*
arithmetic — you need the top level to make sense of the bottom.

## Worked example

How a fly measures visual motion (Marr's levels in VL5):
- **Computational:** the goal is to estimate optic-flow / self-motion from the
  changing retinal image (e.g. to stabilise flight).
- **Algorithmic:** the **Hassenstein–Reichardt detector** — correlate the signal
  from one photoreceptor with a delayed signal from a neighbour to detect motion
  direction.
- **Implementational:** specific medulla neurons (Mi1, Tm3, T4) and lamina
  circuitry in the fly's optic lobe realise this correlation.

## Why it matters

It is a foundational organising framework for cognitive science and computational
neuroscience: it clarifies what kind of explanation a model offers, prevents
category errors (mistaking a computational-level claim for a mechanistic one), and
structures debates about rational/Bayesian models of mind and brain.

## Used in

- [[Bayesian Inference in Cognitive Modeling]] (VL5 — placing "Bayesian brain"
  claims at the correct level)
- [[VL05 Bayes]]

## Related concepts

- [[Bayesian Inference]]
- [[Bayes' Theorem]]

## Common confusions

- The three levels are not strictly hierarchical or tightly determined by one
  another — they are loosely coupled.
- A computational-level (rational/ideal-observer) account is not automatically a
  claim about algorithms or neural implementation.

## Sources

- [[VL05 Bayes]]
