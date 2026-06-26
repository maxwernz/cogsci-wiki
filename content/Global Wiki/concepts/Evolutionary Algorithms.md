---
type: method
status: active
scope: global
classes: [Kognitive Architekturen]
projects:
domains: [optimisation, evolution, machine learning, AI]
sources:
created: 2026-06-17
updated: 2026-06-17
---

# Evolutionary Algorithms

## Short definition

Evolutionary algorithms (EAs), including genetic algorithms (GAs), are
population-based, **"blind"** (model-free) optimisation methods that imitate
natural selection: a population of candidate solutions is repeatedly
**evaluated, selected, mutated, and recombined** until good solutions emerge.

## General explanation

**The basic loop.** (1) Initialise a population $P$ (randomly or informed). (2)
While not satisfied: **evaluate** each individual's fitness; **select and
reproduce** the better ones; **mutate and recombine** them; **integrate** the
offspring back into $P$. The vocabulary mirrors biology: a **genotype** is the
encoded solution (a string of **genes**, each with an **allele** value); the
**phenotype** is what the code means (the agent/solution); the **fitness
function** scores quality; and selection, mutation, and recombination are the
operators.

**How the operators interact.** *Selection* focuses the search on neighbourhoods
of good solutions. *Mutation* controls the *width* of local search (bit-flips for
binary codes, Gaussian perturbation for real codes); selection + mutation behaves
like hill-climbing. *Recombination* (crossover) swaps sub-structures between
parents; selection + recombination drives *innovation* — combining good building
blocks from different individuals.

**Why some problems are hard — fitness landscapes.** *One-Max* (count the ones)
has a single optimum that fitness gradients lead straight to → easy.
*Needle-in-a-haystack* gives fitness 1 only at the optimum → no gradient to
follow. *Trap* functions actively mislead the search toward a local optimum away
from the global one → genuinely hard "building-block" problems.

**Schema theory (Holland).** A *schema* / *building block* is a partial genotype
pattern, e.g. `#10#1` (`#` = wildcard), characterised by its **order** $o$
(number of fixed positions) and **defining length** $\delta$ (span of the
outermost fixed positions). The **schema theorem** says short, low-order,
above-average-fitness building blocks proliferate roughly exponentially, because
they are fit (selection grows them), compact (crossover rarely disrupts them),
and low-order (mutation rarely hits them).

**Balance is everything.** Goldberg's analysis frames good EA design as a *race*
between **innovation time** (how long recombination takes to find something
better) and **take-over time** (how long the best individual takes to dominate
the population). If innovation wins, the search keeps finding new structure; if
take-over wins, the population converges prematurely and diversity collapses.
This defines a *sweet spot* in the space of selection pressure and crossover rate,
bounded by drift (too little selection), premature convergence (too little
mixing), and cross-competition (too much selection).

**Real-valued variants.** Evolution strategies add self-adapting step sizes (the
1/5 success rule); **CMA-ES** adapts a full covariance matrix and is closely
related to **policy-gradient** methods in [[Reinforcement Learning]]; estimation-
of-distribution algorithms model the population (e.g. with a Bayesian network) to
discover building blocks automatically.

## Intuition

Suppose you want the best recipe but cannot calculate it. You cook 100 variants,
keep the tastiest, blend their ingredients, and tweak a pinch here and there.
Repeat for many "generations" — never *understanding* why something tastes good.
That is how evolution "searches": no model, no plan, only evaluation and
variation.

## Formal definition

Take-over time under truncation or binary-tournament selection scales as
$\text{TOT}=\log_2 N$ for population size $N$. The schema theorem bounds the
expected growth of a schema $H$:

$$\langle m(H,t{+}1)\rangle \ge m(H,t)\,\frac{f(H,t)}{\bar f(t)}
\Big[1-p_c\,\frac{\delta(H)}{l-1}\Big](1-p_m)^{o(H)}.$$

Symbols: $m(H,t)$ fraction of individuals carrying schema $H$; $f(H,t)/\bar f(t)$
its relative fitness (selection growth); $p_c\,\delta(H)/(l-1)$ the chance
crossover disrupts $H$ (grows with defining length $\delta$ and genome length
$l$); $(1-p_m)^{o(H)}$ the chance mutation spares $H$ (shrinks with order $o$).

## Worked example

Population $N=256$ with 4 superior individuals "A" ($f=64$) and 252 "B" ($f=1$).
Under truncation selection at 50%, the best fraction doubles each generation, so
take-over takes $\text{TOT}=\log_2 256 = 8$ generations until the whole population
is "A."

## Why it matters

EAs are general-purpose black-box optimisers for problems with no gradient, no
model, or rugged/deceptive landscapes — used in engineering design, scheduling,
neural-architecture and hyperparameter search, and as a lens on biological
evolution itself. CMA-ES is a competitive baseline for continuous black-box
optimisation, including in reinforcement learning.

## Used in

- [[Evolutionäre Algorithmen]] (Kognitive Architekturen: schema theory, fitness
  landscapes, Goldberg's race / sweet spot)
- [[Reinforcement Learning]] (CMA-ES as an alternative to policy gradients)

## Related concepts

- [[Numerical Optimisation]]
- [[Reinforcement Learning]]
- [[Bayesian Network]] (estimation-of-distribution algorithms)

## Common confusions

- **EAs are blind.** There is no model predicting mutation effects; the power
  comes from the *balance* of selection and recombination, not clever operators.
- **The schema theorem explains growth, not discovery.** It says when an
  *already-found* building block proliferates — not how new ones are discovered.

## Sources

- Holland (1975); Goldberg (1989, 1998); Hansen, CMA-ES.
