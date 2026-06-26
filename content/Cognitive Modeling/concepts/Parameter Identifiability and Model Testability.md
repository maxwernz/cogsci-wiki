---
type: concept
status: active
scope: local
classes: [Cognitive Modeling]
projects:
domains: [statistics, modeling]
sources:
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_03_GoF.pdf
  - Classes/Cognitive Modeling/raw/Slides/VLCogMod_07_InterpretingModeling.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Parameter Identifiability and Model Testability

## Short definition

A model is **identifiable** if the data pin down a unique set of parameter
values; it is **testable (falsifiable)** if some conceivable experimental outcome
would be inconsistent with it.

## Intuition

Identifiability asks: *given the data, can I trust the specific parameter numbers
I read off?* If two different parameter settings predict exactly the same data,
the data cannot tell them apart and the numbers are not trustworthy. Testability
asks: *could this model ever be proven wrong?* A model that fits any conceivable
data is not making a real claim — like a theory that "predicts" everything and
therefore explains nothing.

## Explanation

These are properties of a model you should check *before* trusting any fit — both
addressed in [[VL03 Goodness-of-fit]] (conceptually, Farrell & Lewandowsky) and
[[VL07 Interpreting Modeling]] (formally, via the Jacobian).

**Identifiability** fails in three typical ways:

1. **Over-parameterisation:** more parameters than necessary, so one parameter's
   value can be compensated by another. Often (not always) revealed by
   over-fitting / poor GoF.
2. **Dependent parameters:** two parameters co-vary so that increasing one can be
   offset by changing the other. Sometimes a *re-write* fixes it — e.g.
   $f(x;\alpha,\beta)=x^{\alpha}/x^{\beta}$ is non-identifiable, but
   $x^{\alpha}/x^{\beta}=x^{\alpha-\beta}$ shows only the *difference* matters.
3. **Periodic functions:** e.g. $f(t;\alpha,\beta)=\alpha\sin(t+\beta)$ has
   infinitely many equivalent $(\alpha,\beta)$ because of the periodicity.

**Testability.** A model is testable iff "there exists a conceivable
experimental outcome with which the model is not consistent" (Bamber & van
Santen, 2000). The **saturated** polynomial model (order = #points − 1) is *not*
testable: it fits *any* dataset perfectly, so no data could refute it.

**Formal (Jacobian) treatment** (Butz, VL7). Let the prediction function be
$y=f(\theta,x)$ and form the **Jacobian** $J_\theta$ of partial derivatives of
the outputs with respect to the parameters (size $m\times n$, where $m$ =
number of parameters, $n$ = number of independent data points), with rank $r$:

- **Identifiability rule:** identifiable iff $r=m$ (the parameters produce
  linearly independent effects on the output). If $r<m$, some parameter directions
  do nothing distinguishable → non-identifiable.
- **Testability (Jacobian) rule:** testable iff $r<n$.
- **Counting rule:** testable iff $m<n$ (more data points than parameters).

A practical, empirical check: run the optimiser from many starting points — if
runs reach **equal likelihood but different parameters**, the parameters are
non-identifiable.

**Is non-identifiability fatal?** Often, but not always. Useful information can
survive: Sternberg's recognition model still tells us encoding+decision time
together, that all items are compared, and that RT grows linearly with set size —
even though $a$ and $c$ individually cannot be recovered. **Fixes:**
(1) re-parameterise (replace the confounded pair by their identifiable
combination, e.g. $a+c=t_{op}$); (2) add experimental constraints (fix a
parameter by design); (3) gather another dependent variable (e.g. confidence
ratings) to break the degeneracy.

**Using a model without testing it.** Sometimes we deliberately apply a
non-testable model *axiomatically*. Signal detection theory converts hits/false
alarms into sensitivity $d'$ and criterion for *any* numbers — it always "works".
We are not testing SDT, we are *assuming* it (a **measurement model**) and using
its parameters for inference. The modeller must be clear which mode they are in:
*testing* a model, or *assuming* its adequacy and reading off parameters.

## Worked example

Sternberg (1975) memory-scanning model: $RT = t_{op} + b\,s$, where $s$ is the
set size, $b\approx35$–$40$ ms is comparison time per item, and the intercept
$t_{op}$ bundles encoding time $a$ and response time $c$. The model is **testable**
— it predicts RT linear in $s$ and equal for old/new items, which data could
contradict. But because only $a+c=t_{op}$ enters, $a$ and $c$ are
**non-identifiable**: any split of $t_{op}$ into $a+c$ fits identically.
Re-parameterising to use $t_{op}$ directly removes the problem.

## Formal definition / equations

With Jacobian $J_\theta$ of size $m\times n$ and rank $r$:

$$\text{identifiable} \iff r=m,\qquad \text{testable} \iff r<n \;(\text{equivalently } m<n).$$

- $m$: number of independent free parameters; $n$: number of independent data
  points; $r$: rank of the Jacobian (number of linearly independent parameter
  effects on the predictions).

## Role in this class or project

Closes [[VL03 Goodness-of-fit]] and is formalised in [[VL07 Interpreting Modeling]]. It is a prerequisite check for meaningful fitting, model comparison,
and parameter interpretation throughout the course.

## Exam, assignment, or project relevance

Define identifiability and testability; give the three identifiability-failure
modes with examples; state the Jacobian-rank and counting rules; work the
Sternberg example and the three fixes; and explain using a non-testable model
axiomatically (SDT as a measurement model).

## Related global concepts

- [[Overfitting and the Bias-Variance Trade-off]]
- [[Maximum Likelihood Estimation]]

## Related local pages

- [[Goodness-of-Fit and Overfitting]]
- [[Numerical Optimisation for Model Fitting]]
- [[Model Interpretation: Necessity and Sufficiency]]

## Common confusions

- **Identifiability ≠ testability.** Sternberg's model is testable but not fully
  identifiable; the saturated polynomial is identifiable-ish in form but not
  testable.
- **"Non-identifiable means useless."** Often informative still (constraints,
  combined parameters, qualitative predictions).
- **"A perfect fit is the goal."** A model that fits *anything* (saturated /
  non-testable) makes no empirical claim.

## Sources

- [[VL03 Goodness-of-fit]]
- [[VL07 Interpreting Modeling]]
- [[Farrell and Lewandowsky Chap 10]] (user note)
