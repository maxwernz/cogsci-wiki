---
type: source_note
status: processed
scope: local
class: Kognitive Architekturen
project:
source_type: paper
raw_path: "raw/Paper zum Diskutieren/Stevens (2012)_ The Vision of David Marr.pdf"
exercise_ref: "Diskussionspaper zu VL08 (Visuelle Wahrnehmung)"
created: 2026-06-17
updated: 2026-06-17
---

# Stevens (2012) – The Vision of David Marr

> Diskussionspaper (Perception 41, 1061–1072) zu
> [[VL08 Visuelle Wahrnehmung Bottom-Up]]. Rückblickender Essay eines früheren
> Marr-Studenten. Hier bewusst **keine** Übungs-/Tutoriumslösungen.

## Summary

Ein reflektierender Rückblick auf **David Marrs Berechnungsparadigma** für das Sehen,
geschrieben von Kent Stevens (Marr-Schüler ab 1975). Marr trennte das **Was** (Ziel und
Logik einer Berechnung) vom **Wie** (Repräsentation/Algorithmus) und **Womit** (neuronale
Implementierung) – die berühmten drei Ebenen ([[Marr's Levels of Analysis]]) – und
schlug eine Kaskade symbolischer Repräsentationen vor (primal sketch → 2½D-Sketch →
3D-Modell). Stevens würdigt, **dass** dieses Paradigma die Sicht auf biologisches Sehen
revolutionierte (Sehen als *Informationsverarbeitung*, nicht bloß Signalverarbeitung),
seziert aber **vier stillschweigende Annahmen**, die heute fragwürdig wirken. Der Essay
ist damit das ideale Gegenstück zu VL08/VL09: Er zeigt, warum die saubere
Bottom-up-Pipeline der Vorlesung eine nützliche Idealisierung ist – und wo sie an der
biologischen Realität (massiv bidirektional, nicht modular) zerbricht.

## Key points

- **Marrs Paradigma:** Sehen in trennbare „computational theories“ zerlegen, jede zuerst
  als *Was/Logik*, dann verfeinert zu Repräsentation/Algorithmus, dann Hardware. Leitende
  Prinzipien: explicit naming, modular design, least commitment, graceful degradation.
- **Vier hinterfragte Zusatzannahmen** (Stevens’ Kern):
  1. **Trennbare Berechnungsstrategien** – modulare „shape-from-X“-Module; Risiko des
     Über-Reduktionismus, wenn verschiedene Reize in Wahrheit dieselbe Strategie speisen.
     Evidenz pro Modularität: dissoziierbare Wahrnehmungsdefizite (z. B. Patient ohne
     subjektive Konturen, aber mit normalem Stereosehen).
  2. **Unterscheidbare Repräsentationen** – diskrete Symbolsysteme (Kante, Bar, Blob,
     „place tokens“). Marr: Konturen werden **konstruiert**, nicht **detektiert** (eine
     subjektive Kontur „ist nicht da“).
  3. **Pipeline-Charakter** (früh→spät, unidirektional) – eine Bequemlichkeitsmetapher
     aus der Informatik; biologisch dominieren bidirektionale, rekurrente Pfade, die
     „früh“ vs. „spät“ verwischen (Top-down hilft schon der primal sketch).
  4. **Primitive niedriger Dimension** – Tiefe/Neigung als skalare „Karten“. Stevens
     argumentiert, gerade Tiefe sei am **schwersten** zuverlässig wahrnehmbar; Form
     entsteht eher aus *Nichtlinearitäten* (Krümmung, Diskontinuitäten) und
     betrachterzentrierter Assoziation, nicht aus einer Tiefenkarte.
- **Pointe:** Die vier Annahmen spiegeln vielleicht weniger die Natur biologischer
  Informationsverarbeitung als unsere **Hoffnung**, sie mit den uns vertrauten
  (modularen, Pipeline-) Architekturen verstehen zu können. Marrs bleibender Verdienst:
  das Denken in **Abstraktions-/Erklärungsebenen**.

## Important concepts

[[Marr's Levels of Analysis]] (Was/Wie/Womit); primal sketch / 2½D-Sketch / 3D-Modell;
Konstruktion vs. Detektion von Kanten; Modularität vs. Superposition; betrachterzentrierte
vs. betrachterunabhängige 3D-Repräsentation. Bezug zu
[[Bottom-Up Bildverarbeitung]] (Kanten als symbolische Aussagen) und
[[Generative und diskriminative Modelle]] (Stevens’ Kritik motiviert die
interaktive, bidirektionale Bayes-Sicht aus VL09).

## Local relevance

Direktes Begleitpaper zu [[VL08 Visuelle Wahrnehmung Bottom-Up]]: Es ordnet die
Bottom-up-Pipeline historisch ein und liefert die Kritik, die zur **Top-down-/
bidirektionalen** Sicht in [[VL09 Visuelle Wahrnehmung Top-Down]] überleitet. Knüpft an
die Kursleitfrage „algorithmische Ebene (das Wie)“ an und schärft, was Marrs Ebenen
leisten – und was nicht.

## Exam or project relevance

Marrs drei Ebenen sicher erklären und auf Sehen anwenden; die vier
Pipeline-/Modularitäts-Annahmen und je ein Gegenargument nennen; „Konturen werden
konstruiert, nicht detektiert“ deuten; warum massive Rückkopplung das „früh vs. spät“
untergräbt. Klassische Diskussionsfragen: Ist visuelle Verarbeitung wirklich modular?
Ist Tiefe ein Primitive oder ein abgeleitetes Maß?

## Links to global concepts

[[Marr's Levels of Analysis]] (zentral), [[Bayesian Inference]] (generative,
bidirektionale Alternative zur reinen Pipeline), [[Predictive Coding]] (Top-down-
Konstruktion der Wahrnehmung).

## Open questions

Stevens schlägt betrachterzentrierte, assoziative 3D-Beschreibungen vor, lässt deren
konkrete Repräsentation aber offen – ein bis heute ungelöstes Problem der
Objekterkennung.
