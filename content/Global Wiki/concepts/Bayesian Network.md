---
type: model
status: active
scope: global
classes: [Kognitive Architekturen]
projects:
domains: [probabilistic graphical models, inference, machine learning]
sources:
created: 2026-06-17
updated: 2026-06-17
---

# Bayesian Network

## Short definition

A Bayesian network is a **directed acyclic graph (DAG)** whose nodes are random
variables and whose edges are direct (conditional) dependencies. It
**factorises** a joint probability distribution compactly and supports reasoning
under uncertainty.

## General explanation

**Structure.** Nodes are variables, edges are conditional dependencies; the graph
is directed and acyclic (no loops). **Roots** carry only a prior; **leaves** have
no children. Each node stores a **conditional probability table/distribution**
given its parents.

**Factorisation.** The central saving: the joint distribution is the product of
the per-node conditionals,
$p(x_1,\dots,x_n)=\prod_i p(x_i\mid \text{parents}(x_i))$. Instead of one table
that is exponential in $n$, you store one small factor per node. This is what
makes inference and learning tractable for structured problems.

**Conditional independence and d-separation.** The graph encodes which variables
are (in)dependent. Two nodes $X,Y$ are **d-separated** by an observed set $E$
(hence independent given $E$) if every undirected path between them is blocked.
Three path types decide blocking:

- **Fork / common cause** ($X\leftarrow V\rightarrow Y$): unobserved, $X,Y$ are
  dependent; **observing $V$ makes them independent.**
- **Chain** ($X\rightarrow V\rightarrow Y$): unobserved, dependent; **observing
  the middle $V$ makes them independent.**
- **Collider / common effect** ($X\rightarrow V\leftarrow Y$): the reverse!
  unobserved, $X,Y$ are independent; **observing $V$ (or a descendant) makes them
  dependent** — this is "explaining away."

**Four modes of inference:** *predictive* (root→leaf, propagate causes to effects
by marginalisation), *diagnostic* (leaf→root, infer causes from effects by
Bayes' rule), *combined* (evidence from both directions), and *intercausal* (two
a-priori independent causes become dependent once their common effect is
observed — the collider case).

## Intuition

Rather than store a giant table of "probability of every possible world," you
draw *what directly influences what*: burglary → alarm, strong wind → alarm,
alarm → dog barks, alarm → police called. Each arrow says "parent causes child."
From this small picture you can answer any query ("how likely is a burglary if
the dog barks?") without ever writing down the full joint table. The network is a
compact, readable map of dependencies.

## Formal definition

Factorisation: $p(x_1,\dots,x_n)=\prod_{i=1}^{n} p(x_i\mid \text{parents}(x_i))$.
Diagnostic inference with one parent:

$$p(o\mid n)=\frac{p(n\mid o)\,p(o)}{p(n)};\qquad
\text{with a further parent } X:\ p(o{=}T\mid n{=}T)=
\frac{\sum_X p(n\mid o,X)\,p(o\mid X)\,p(X)}{p(n)}.$$

A discrete node with discrete parents stores a probability **table**; a
continuous child stores a conditional **density** (e.g. a
[[Gaussian Mixture Model]]).

## Worked example

Network $A,B\rightarrow O\rightarrow N$, with $A$ = colour detector, $B$ = shape
detector, $O$ = "object is a cup," $N$ = saucer nearby. With $p(a)=0.2$,
$p(b)=0.1$ and the table $p(O{=}T\mid A,B)$ (TT 0.95, TF 0.6, FT 0.5, FF 0.01):

- **Predictive, no evidence** (marginalise over $A,B$):
  $p(O{=}T)=\sum_{a,b}p(O{=}T\mid a,b)\,p(a)\,p(b)\approx0.16$.
- **Predictive with evidence $a=T$:** $p(O{=}T\mid a{=}T)=0.95(0.1)+0.6(0.9)=0.635$.
- **Diagnostic:** observe $N{=}T$ and infer $O$ via $p(O\mid N)\propto p(N\mid O)\,p(O)$.

## Why it matters

Bayesian networks are a foundational formalism for probabilistic reasoning: they
make structured joint distributions compact, expose conditional independence
explicitly, and unify prediction, diagnosis, and causal "explaining away" in one
framework. They underpin expert systems, diagnosis, and structured generative
models of perception and cognition.

## Used in

- [[Bayes-Netzwerke]] (Kognitive Architekturen: discrete machinery of top-down
  generative perception; d-separation; four deduction modes)
- [[Generative and Discriminative Models]] (a Bayesian network is a generative model)

## Related concepts

- [[Bayes' Theorem]]
- [[Bayesian Inference]]
- [[Gaussian Mixture Model]]
- [[Predictive Coding]]

## Common confusions

- **Collider is reversed.** For fork/chain, *observing* the middle node makes the
  ends independent; for a collider, *observing* the effect makes the causes
  dependent. The most common mistake.
- **An edge is not "one-directional correlation."** Arrow direction encodes the
  generative dependency (parent→child); diagnostic inference runs *against* the
  arrows.
- **"No edge = independent" is false in general.** Dependence can run along paths;
  only d-separation gives the correct answer.

## Sources

- Pearl, *Probabilistic Reasoning in Intelligent Systems*; Koller & Friedman,
  *Probabilistic Graphical Models*.
