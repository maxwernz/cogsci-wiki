---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, optimisation, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_02_RMSD-ML.pdf
  - Classes/Cognitive Modeling/raw/Computational Modeling of Cognition and Behavior/09.1_pp_47_71_Basic_Parameter_Estimation_Techniques.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Numerical Optimisation for Model Fitting

## Short definition

The set of algorithms used to *search* for the parameter values that minimise a
discrepancy function (or maximise a likelihood) when no closed-form solution
exists.

## Intuition

Picture the error as a landscape: each point on the ground is a parameter
setting, and the height is how badly the model fits there. Fitting means finding
the lowest valley. You cannot see the whole landscape at once — you can only feel
the slope where you stand — so you need a strategy to walk downhill. The danger
is settling in a small dip (a *local* minimum) while a deeper valley (the
*global* minimum) lies elsewhere.

## Explanation

For most cognitive models the best-fitting parameters cannot be derived
analytically; you must search numerically. The lecture covers two contrasting
algorithms, plus the central hazard they face.

**The simplex (Nelder–Mead).** A simplex is a geometric shape with one more
vertex than there are parameters (a triangle for 2 parameters, a tetrahedron for
3). The algorithm evaluates the error at each vertex and "tumbles" downhill by
*reflecting* the worst vertex through the opposite face, and *contracting*
(shrinking) as it nears a minimum. Farrell & Lewandowsky liken it to a
night-time parachutist feeling their way down a mountain in the dark. It is
**efficient** (few evaluations) and simple, but **prone to getting stuck in
local minima** and struggles in high dimensions (>~5 parameters).

**Simulated annealing.** A "thermal" method that, unlike greedy downhill search,
sometimes accepts an *uphill* (worse) move. The probability of accepting a worse
move is governed by a **temperature** $T$ that follows a **cooling schedule**:
at high $T$ the search jumps around erratically and easily escapes local minima;
as $T$ falls, uphill moves become rare and the system "freezes" — ideally into
the global minimum. It is **robust** to local minima and handles many parameters,
but is **inefficient** (many evaluations) and needs careful tuning of the cooling
schedule.

**The local-minimum problem.** A local minimum is a parameter setting that is
better than all its neighbours but worse than the global optimum. It matters
because a greedy method that lands there reports a *poorer fit* than truly
achievable and the *wrong* parameters — and you may not know it happened. This
is why one runs an optimiser from **multiple starting points**: if different
starts converge to different parameters with similar error, you have hit local
minima (and possibly a non-identifiable model — see [[Parameter Identifiability and Model Testability]]).

The number of function evaluations an optimiser needs (the lecture's Q2) depends
not just on starting point, data and model, but also on the *shape of the error
surface* (ruggedness, flatness, correlated parameters), convergence tolerances,
and parameter bounds. Other powerful methods exist beyond this course, e.g.
**CMA-ES** (covariance-matrix adaptation evolution strategy), mentioned in
[[VL07 Interpreting Modeling]]; for linear models, linear regression solves the
problem directly and optimally.

## Worked example

Fitting a 3-parameter forgetting curve by least squares: place a simplex
(tetrahedron) of 4 parameter triples in parameter space, evaluate SSE at each,
reflect the worst point downhill, and iterate; the R function `optim` in
Farrell & Lewandowsky found the optimum in ~121 evaluations for one such fit. Now
suppose the error surface has a shallow secondary dip: starting the simplex near
that dip lands you in the local minimum, while simulated annealing — by
occasionally accepting worse moves at high temperature — can climb out and find
the deeper global valley.

## Formal definition / equations

Simulated annealing accepts a worse move of size $\Delta E>0$ with the
Metropolis probability

$$P(\text{accept}) = \exp\!\left(-\frac{\Delta E}{T}\right),$$

- $\Delta E$: increase in error from the proposed move; $T$: current temperature.
  At high $T$ the exponent is near 0 so $P\approx 1$ (almost any move accepted);
  as $T\to 0$, $P\to 0$ for any uphill move (pure downhill search).

## Role in this class or project

The "how is the minimum actually found?" companion to both estimation methods in
[[VL02 RMSD and ML]]. Optimisation underlies every fit in the course, including
the ML fits in [[VL06 Modeling Visual Cognition]] and [[VL08 Model Comparison Example]].

## Exam, assignment, or project relevance

Explain how the simplex and simulated annealing work; state why local minima are
problematic; explain why simulated annealing escapes them (uphill moves via
temperature/cooling); and list what the evaluation count depends on. Compare the
two algorithms on efficiency, reliability and dimensionality.

## Related global concepts

- [[Numerical Optimisation]] (general method)
- [[Maximum Likelihood Estimation]]
- [[Evolutionary Algorithms]] (CMA-ES as a global optimiser)

## Related local pages

- [[Least-Squares Estimation in Cognitive Modeling]]
- [[Maximum Likelihood Estimation in Cognitive Modeling]]
- [[Parameter Identifiability and Model Testability]]

## Common confusions

- **"A good optimiser guarantees the global optimum."** No deterministic
  downhill method does; multiple restarts and/or annealing mitigate but do not
  prove global optimality.
- **Simplex = the linear-programming simplex.** Different algorithm; here
  "simplex" means Nelder–Mead downhill search.

## Sources

- [[VL02 RMSD and ML]]
- [[Farrell and Lewandowsky Chap 3.1-3.6 + Chap 4]] (user note)
