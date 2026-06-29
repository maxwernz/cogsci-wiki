---
type: source_note
status: processed
scope: local
class: Kognitive Architekturen
project:
source_type: paper
raw_path: "raw/Paper zum Diskutieren/Goldberg(1998)_ TheRaceTheHurdleAndTheSweetSpot.pdf"
exercise_ref: "Übung 2 (Evol. Algos); Tutorium 3"
created: 2026-06-09
updated: 2026-06-09
---

# Goldberg (1998) – The Race, the Hurdle, and the Sweet Spot

> Diskussionspaper. Relevant für **Übung 2 (Evolutionäre Algorithmen)** und
> **Tutorium 3**. Hier bewusst **keine** Übungs-/Tutoriumsaufgabeninhalte.

## Summary

Goldberg argumentiert, dass **genetische Algorithmen** ein mechanistisches Modell von
**Innovation** (und perspektivisch **Kreativität**) liefern. Er erklärt GAs über die
„innovation intuition": Selektion+Mutation = kontinuierliche Verbesserung
(Hillclimbing/Kaizen); Selektion+Rekombination = kreuzbefruchtende Innovation. Drei
qualitative Lektionen kompetenten GA-Designs: **The Race**, **The Sweet Spot
(Control Map)** und **The Hurdle**.

## Key points

- **Was GAs verarbeiten**: Quasi-Dekomposition und Reassemblierung von **Building
  Blocks (BBs)** – gut angepasste Teilstrukturen guter Lösungen (Holland).
- **The Race**: Wettrennen zwischen **Take-Over Time** $t^*$ (Selektion füllt die
  Population mit dem Besten) und **Innovation Time** $t_i$ (Rekombination findet etwas
  Besseres). $t_i \le t^*$ → **steady-state innovation**; $t_i > t^*$ → **premature
  convergence** (Diversität weg, `11111`×`11111`=`11111`).
- **The Sweet Spot / Control Map**: Erfolgszone im Raum (Selektionsdruck $s$,
  Crossover-Wahrscheinlichkeit $p_c$), begrenzt durch **drift** (zu schwache
  Selektion), **mixing/innovation boundary** (zu wenig Crossover) und
  **cross-competition** (zu hohe Selektion). $p_c$ sollte ~ mit $\log s$ wachsen.
- **The Hurdle**: Bei BBs > 1 Bit schrumpft der Sweet Spot; einfache Crossover-
  Operatoren skalieren exponentiell schlecht. **Lösung**: BBs **identifizieren, bevor**
  man zwischen ihnen entscheidet → kompetente GAs (fast messy GA, gemGA, LLGA) mit
  subquadratischer Skalierung.
- **Von Kompetenz zu Kreativität**: Kreativität = Wissenstransfer *zwischen* Domänen
  (Innovation = innerhalb).

## Important concepts

[[Evolutionäre Algorithmen]] (Schema-Theorie, Take-Over Time, Kontrollkarte – volle
Tiefe); Building Blocks; premature convergence; steady-state innovation.

## Methods, models, or theories

Innovation Intuition; Time-Scales-Argument (Race); Control Map; kompetente GAs
(fmGA/gemGA/LLGA); Bezug zu Population Sizing (∝ √(Anzahl Entscheidungsvariablen)).

## Equations or formal definitions

Qualitativ: $t^* \propto \log N / \log s$; $t_i \propto 1/(N\,p_c)$; Innovations-
grenze bei $t^* \approx t_i$. Quantitatives Schema-Theorem siehe
[[Evolutionäre Algorithmen]] und [[Formelsammlung (Tutorium)]].

## Local relevance

Vertieft die „Kontrollkarte" aus [[VL03 Phylogenese und Evolutionäre Algorithmen]] und
liefert die konzeptuelle Begründung, warum Operator-Balance über Erfolg/Misserfolg
entscheidet. Verbindet EA mit menschlicher Innovation/Kreativität.

## Exam or project relevance

Race ($t^*$ vs. $t_i$), Sweet Spot/Control Map (drift, mixing, cross-competition),
Hurdle und kompetente GAs erklären; Innovation Intuition (Selektion+Mutation vs.
Selektion+Rekombination). Übung 2, Tutorium 3 (Take-Over-Time- & Schema-Rechnungen).

## Links to global concepts

_Globaler Promotionskandidat: „Evolutionary Algorithms"._

## Open questions

Wie lässt sich „Kreativität" (Domänen-übergreifender Transfer) algorithmisch fassen?
Goldberg skizziert es nur als Programm.
