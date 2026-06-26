---
type: source_note
status: processed
scope: local
class: Cognitive Modeling
project:
source_type: book
raw_path: Classes/Cognitive Modeling/raw/Literature/Hastie_etal_2009.pdf
created: 2026-06-09
updated: 2026-06-09
---

# Hastie, Tibshirani & Friedman (2009) — The Elements of Statistical Learning (§7.10 Cross-Validation)

> Referenced in [[VL03 Goodness-of-fit]] / the [[ReadingList-VL2-5.pdf|reading list]]
> as *optional, deeper* reading on cross-validation: §7.10 in chapter 7. The
> reading list warns the book is "well beyond this course" and §7.10 is "somewhat
> arcane and only applicable in very restricted settings". Treat as a reference,
> not core material.

## Summary

ESL is the standard graduate text on statistical learning. For this course only
**§7.10 (Cross-Validation)** in the model-assessment chapter is cited, as the
rigorous backing for the cross-validation ideas VL3 introduces more informally.
Its course-relevant content: K-fold cross-validation is a practical estimator of
the **expected prediction error** across different training sets (the exact claim
VL3 attributes to "Hastie et al."), and the chapter formalises the
training-error-vs-test-error / bias–variance story that the lectures present
visually.

## Key points

- K-fold CV provides a reasonable estimate of expected (out-of-sample)
  prediction error — the justification VL3 cites for using CV to choose model
  complexity.
- The chapter also discusses subtleties (e.g. the "right way" to cross-validate,
  avoiding information leakage) that are beyond this course.

## Local relevance

Background depth for the cross-validation segment of VL3 and for the
generalization/CV criterion in [[VL07 Interpreting Modeling]] and [[VL08 Model Comparison Example]]. Not required reading; consult only if you want the formal
treatment.

## Exam or project relevance

Low — explicitly flagged as beyond the course. The exam-relevant CV content is
covered in the lectures and [[Cross-Validation and Regularisation]].

## Links to global concepts

- [[Cross-Validation]] (global)

## Open questions

- None — used purely as an optional reference pointer.
