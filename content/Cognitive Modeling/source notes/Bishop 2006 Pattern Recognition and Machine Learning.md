---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: book
raw_path: Classes/Cognitive Modeling/raw/Literature/Bishop_2006.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Bishop (2006) — Pattern Recognition and Machine Learning (§1.1 Polynomial Curve Fitting)

> Referenced in [[VL03 Goodness-of-fit]] and the [[ReadingList-VL2-5.pdf|reading list]]: the regularisation outlook is taken from Bishop §1.1 *Polynomial Curve
> Fitting*. Not compulsory, but uploaded to ILIAS. Only §1.1 is relevant for this
> course; the rest of the book is a graduate ML text.

## Summary

Bishop's opening example — fitting a polynomial of order $M$ to 10 noisy points
sampled from $\sin(2\pi x)$ — is the canonical illustration of **over-fitting and
regularisation** that VL3 uses. It makes the abstract bias–variance story
concrete and visual: as $M$ grows, the fit to the training points improves until
($M=9$) it passes through every point *exactly* yet wildly oscillates and is a
*terrible* representation of the true curve. The example then shows the two
classic cures: **more data** and **regularisation** (penalising large
coefficients), and introduces using a held-out set to choose model complexity.

## Key points

- **The setup.** $N=10$ training points $(x_i,t_i)$; predict $t^\*$ for a new
  $x^\*$ using a polynomial $y(x,\alpha)=\sum_{j=0}^{M}\alpha_j x^j$.
- **Over-fitting visualised.** $M=0,1$ underfit (high bias); $M=3$ fits the
  underlying $\sin$ curve well; $M=9$ achieves *zero* training error but
  oscillates violently — excellent fit, dreadful generalisation.
- **Train vs test RMS** (Bishop's Fig. 1.5): training RMS error falls
  monotonically with $M$; test RMS error has the characteristic U-shape — the
  same point as Farrell & Lewandowsky's Figs 10.4–10.5.
- **More data helps:** with $M=9$ but $N=15$ then $N=100$, the over-fitting
  disappears — a flexible model is fine if you have enough data to constrain it.
- **Regularisation:** add $\lambda\lVert\alpha\rVert^2$ to the error; a
  well-chosen $\ln\lambda$ tames the $M=9$ polynomial without reducing its order.

## Equations or formal definitions

Polynomial model and (unregularised) sum-of-squares error:

$$y(x,\alpha)=\sum_{j=0}^{M}\alpha_j x^j, \qquad E(\alpha)=\sum_{i=1}^{N}\{y(x_i,\alpha)-t_i\}^2, \qquad E_{RMS}=\sqrt{E(\alpha)/N}$$

Regularised (ridge / weight-decay) error:

$$E(\alpha)=\sum_{i=1}^{N}\{y(x_i,\alpha)-t_i\}^2 + \lambda\lVert\alpha\rVert^2, \quad \lVert\alpha\rVert^2 = \alpha^\top\alpha = \alpha_0^2+\dots+\alpha_M^2$$

- $M$: polynomial order (model complexity); $\alpha$: coefficients;
  $\lambda$: regularisation strength (larger → smaller coefficients → simpler
  effective model). This is exactly the L2/ridge penalty in [[Regularisation]].

## Local relevance

The visual backbone of the over-fitting / regularisation portion of VL3. It is
where the course's "more data or regularisation" message is made tangible and
where the train-vs-test RMS curve is first seen.

## Exam or project relevance

The polynomial curve-fitting picture (under/good/over-fit at $M=0,3,9$; train vs
test RMS U-curve; "more data or regularisation") is exactly the intuition VL3
expects you to reproduce and explain.

## Links to global concepts

- [[Overfitting and the Bias-Variance Trade-off]] (global)
- [[Regularisation]] (global)

## Open questions

- Bishop §1.1 figures (1.4a–d, 1.5, 1.6, 1.7) are the high-value visuals; not
  extracted.
