---
type: method
status: active
scope: global
classes: [Cognitive Modeling]
projects:
domains: [optimisation, statistics, machine learning]
sources:
created: 2026-06-17
updated: 2026-06-17
---

# Numerical Optimisation

## Short definition

Numerical optimisation is the family of algorithms that *search* for the
parameter values minimising an objective (error / loss) function — or maximising
a likelihood — when no closed-form solution exists.

## General explanation

Many models cannot be fit analytically: there is no formula for the
best-fitting parameters, so you must search the parameter space numerically. The
objective defines an **error surface** over parameters, and optimisation walks
that surface looking for the lowest point. Methods divide along two axes.

**Local (gradient or downhill) methods.** These exploit the slope at the current
point to step downhill — gradient descent and its variants when derivatives are
available, or derivative-free **Nelder–Mead (simplex)** when they are not. A
simplex is a shape with one more vertex than there are parameters (a triangle for
2, a tetrahedron for 3); the algorithm evaluates the error at each vertex and
"tumbles" downhill by reflecting the worst vertex through the opposite face and
contracting as it nears a minimum. Local methods are **efficient** but **prone to
getting stuck in local minima** and degrade in high dimensions.

**Global / stochastic methods.** These deliberately accept occasional *uphill*
moves to escape local minima. **Simulated annealing** accepts a worse move with
the Metropolis probability $P=\exp(-\Delta E/T)$, governed by a **temperature**
$T$ on a **cooling schedule**: high $T$ jumps around and escapes traps, and as
$T\to0$ the search "freezes," ideally into the global minimum. It is **robust**
to local minima but **inefficient** and needs tuning. Population-based methods
such as evolutionary strategies ([[Evolutionary Algorithms]], e.g. CMA-ES) are
another global, black-box option.

**The local-minimum problem.** A local minimum is a parameter setting better than
all its neighbours but worse than the global optimum. A greedy method that lands
there reports a poorer fit than truly achievable and the *wrong* parameters — and
you may not know it happened. The standard guard is to run the optimiser from
**multiple starting points**: if different starts converge to different parameters
with similar error, you have hit local minima (and possibly a non-identifiable
model). How many function evaluations are needed depends on the start, the data
and model, the *shape* of the error surface (ruggedness, flatness, correlated
parameters), the convergence tolerance, and any parameter bounds.

## Intuition

Picture the error as a landscape: each point on the ground is a parameter
setting, and the height is how badly the model fits there. Fitting means finding
the lowest valley, but you can only feel the slope where you stand, not see the
whole terrain — so you need a strategy to walk downhill. The danger is settling
in a small dip (a *local* minimum) while a deeper valley (the *global* minimum)
lies elsewhere.

## Formal definition

You seek $\hat\theta=\arg\min_\theta E(\theta)$ for an objective $E$. Simulated
annealing accepts a worse move of size $\Delta E>0$ with probability

$$P(\text{accept})=\exp\!\left(-\frac{\Delta E}{T}\right),$$

where $\Delta E$ is the increase in error and $T$ the current temperature. At
high $T$ the exponent is near $0$ so $P\approx1$ (almost any move accepted); as
$T\to0$, $P\to0$ for any uphill move (pure downhill search).

## Worked example

Fitting a 3-parameter curve by least squares: place a simplex (a tetrahedron of
4 parameter triples), evaluate the sum of squared errors at each vertex, reflect
the worst vertex downhill, and iterate until the simplex contracts onto a
minimum — a standard routine converges in roughly a hundred evaluations for a
simple fit. If the error surface has a shallow secondary dip, a simplex started
near it gets trapped, whereas simulated annealing — accepting occasional uphill
moves at high temperature — can climb out and reach the deeper global valley.

## Why it matters

Numerical optimisation is the engine under almost every model fit, from
psychological models and statistics to training deep neural networks (where
gradient descent on a loss is exactly this problem at scale). Understanding local
minima, restarts, and the efficiency/robustness trade-off is essential to
trusting any fitted parameters.

## Used in

- [[Numerical Optimisation for Model Fitting]] (Cognitive Modeling: simplex vs
  simulated annealing; the local-minimum problem)
- [[Maximum Likelihood Estimation]] (the optimisation that finds the MLE)
- [[Optimization for Language Models in Understanding LLMs]] (gradient descent at scale)

## Related concepts

- [[Maximum Likelihood Estimation]]
- [[Least-Squares Estimation]]
- [[Evolutionary Algorithms]]

## Common confusions

- **"A good optimiser guarantees the global optimum."** No deterministic downhill
  method does; restarts and/or annealing mitigate but do not prove global
  optimality.
- **Nelder–Mead "simplex" ≠ the linear-programming simplex.** Different
  algorithm; here it means derivative-free downhill search.

## Sources

- Nocedal & Wright, *Numerical Optimization*; Press et al., *Numerical Recipes*.
