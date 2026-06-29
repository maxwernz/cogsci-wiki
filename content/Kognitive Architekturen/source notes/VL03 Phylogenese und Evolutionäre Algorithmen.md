---
type: source_note
status: processed
scope: local
class: Kognitive Architekturen
project:
source_type: lecture_slides
raw_path: "raw/VL Folien/KogArch_03_Phylogenese.pdf"
created: 2026-06-09
updated: 2026-06-09
---

# VL03 – Phylogenese & Evolutionäre Algorithmen

## Summary

Die phylogenetische Perspektive: Evolution formt Körpermorphologie, Hirnarchitektur
und sogar den Verlauf der Ontogenese. Der Großteil der VL erklärt **evolutionäre/
genetische Algorithmen** als Werkzeug, um zu verstehen, *was* Evolution geleistet
haben kann, und als allgemeines Optimierungsverfahren – inklusive Schema-Theorie und
Goldbergs Kontrollkarte.

## Key points

- **Evolution des Menschen** ist evolutionär „jung" (~0,044 % der Erdgeschichte;
  ~96 % Genidentität mit Schimpansen) → wahrscheinlich keine fundamental neuen
  Genom-Teilstrukturen, nur Modifikation/Rekombination/Duplikation bestehender.
- **Nischen**: Evolution findet in (sich wandelnden) ökologischen/kulturellen Nischen
  statt; Wettbewerb erzeugt Balance; Einfachheit/Kompaktheit gewinnt.
- **EA-Grundalgorithmus** und Terminologie (Genotyp/Phänotyp/Allel/Fitness/Operatoren).
- **Fitnesslandschaften**: One-Max (leicht), Needle (keine Hilfe), Trap (irreführend).
- **Schema-Theorem**, Building Blocks, Ordnung & definierende Länge.
- **Operator-Balance**: Selektion+Mutation = Hillclimbing; Selektion+Rekombination =
  Innovation. **Take-Over Time**; 1/5-Regel; CMA-ES; EDAs.
- **Goldbergs Race/Sweet-Spot/Hurdle** (Kontrollkarte) – siehe Paper.

## Important concepts

[[Evolutionäre Algorithmen]] (volle Mechanik, Schema-Theorem, Kontrollkarte);
[[Drei zeitliche Perspektiven]]; ökologische Nischen.

## Methods, models, or theories

EA/GA, Evolutionsstrategien (1/5-Regel, CMA-ES), EDAs (ECGA, BOA). Schematheorie
nach Holland (1975). Innovationsanalyse nach Goldberg.

## Equations or formal definitions

Schema-Theorem:
$\langle m(H,t{+}1)\rangle \ge m(H,t)\frac{f(H,t)}{\bar f(t)}[1-p_c\frac{\delta(H)}{l-1}](1-p_m)^{o(H)}$.
Take-Over Time: Truncation 50 % bzw. Tournament(2): $\log_2 N$. Alle Terme erklärt in
[[Evolutionäre Algorithmen]] und [[Formelsammlung (Tutorium)]].

## Local relevance

Liefert den Phylogenese-Baustein und ein wiederkehrendes Optimierungsparadigma
(CMA-ES taucht bei Policy Gradients in [[VL06 Belohnungslernen II]] wieder auf).
Diskussionspaper: [[Goldberg (1998) The Race the Hurdle and the Sweet Spot]] (Übung 2).

## Exam or project relevance

Sehr klausurrelevanter „praktischer" Block: Grundalgorithmus; Fitnesslandschaften;
Schema-Theorem (Terme); Ordnung/def. Länge berechnen; Take-Over-Time-Rechnung;
Race/Sweet-Spot/Hurdle. Übungen 1–2, Tutorien 2–3.

## Links to global concepts

_Globaler Promotionskandidat: „Evolutionary Algorithms"._

## Open questions

Welche neuronalen Grundbausteine sich genau verändert haben, um menschliche
Flexibilität/Sprache zu ermöglichen, bleibt laut Folien die große offene Frage der
evolutions-kognitionswissenschaftlichen Forschung.
