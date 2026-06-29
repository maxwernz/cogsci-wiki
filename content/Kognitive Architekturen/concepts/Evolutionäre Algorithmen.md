---
type: method
status: active
scope: local
classes: [Kognitive Architekturen]
projects: []
domains: [optimization, evolution, AI]
sources: ["[[VL03 Phylogenese und Evolutionäre Algorithmen]]", "[[Goldberg (1998) The Race the Hurdle and the Sweet Spot]]"]
created: 2026-06-09
updated: 2026-06-09
---

# Evolutionäre Algorithmen (EA) und Genetische Algorithmen (GA)

## Short definition

Evolutionäre Algorithmen sind populationsbasierte, **„blinde"** (modellfreie)
Optimierungsverfahren, die das Prinzip der natürlichen Selektion nachbilden:
Eine Population von Lösungen wird wiederholt **bewertet, selektiert, mutiert und
rekombiniert**, bis gute Lösungen entstehen.

## Intuition

Stell dir vor, du suchst das beste Rezept, kannst es aber nicht ausrechnen. Du
kochst 100 Varianten, behältst die leckersten, mischst ihre Zutaten neu und
veränderst hier und da eine Prise. Wiederhole das viele „Generationen" lang – ohne
je zu *verstehen*, warum etwas schmeckt. Genau so „sucht" Evolution: ohne Modell,
ohne Plan, nur über Bewertung und Variation.

## Explanation

### Grundalgorithmus

1. **Initialisiere** Population $P$ (zufällig oder informiert).
2. WHILE nicht zufrieden:
   - **Evaluiere** den Phänotyp jedes Individuums (Fitnessfunktion).
   - **Selektiere & reproduziere** bessere Genotypen.
   - **Mutiere & rekombiniere** diese.
   - **Integriere** die neuen Genotypen in $P$.

### Terminologie

- **Population**: Menge sich entwickelnder Individuen.
- **Genotyp**: der Code (Folge von **Genen**; Ausprägung eines Gens = **Allel**).
- **Phänotyp**: die Bedeutung des Codes (Agent/Lösung/Lebewesen).
- **Fitnessfunktion**: misst die „Güte".
- **Selektion/Reproduktion, Mutation, Rekombination**: die Operatoren.

Beispiel Blutgruppen: 3 Allele (A, B, 0) → 6 Genotypen (AA, AB, BB, A0, B0, 00) →
4 Phänotypen (A, AB, B, 0). Genotyp ≠ Phänotyp.

### Wie die Operatoren zusammenwirken

- **Selektion** fokussiert die Suche auf Nachbarschaften guter Lösungen.
- **Mutation** kontrolliert die *Breite* der Nachbarschaftssuche (Bitflips bei
  binärem, Gauß-Streuung bei reellem Code). Selektion + Mutation = **Hillclimbing**
  / kontinuierliche Verbesserung.
- **Rekombination** tauscht Teilstrukturen aus. Selektion + Rekombination =
  **Innovation** (kreuzbefruchtende Kombination guter Bausteine; Goldbergs
  „innovation intuition").

### Fitnesslandschaften (warum manche Probleme schwer sind)

- **One-Max** (zähle die Einsen): ein globales Optimum, Fitness „führt" dorthin → leicht.
- **Needle-in-a-Haystack**: Fitness = 1 nur am Optimum, sonst 0 → keine Hilfe,
  systematische Suche nötig.
- **Trap**: Fitness führt zu einem *lokalen* Optimum, weg vom globalen → irreführend,
  schwieriges „Building-Block"-Problem.

### Schematheorie und Building Blocks (Holland, 1975)

Ein **Schema** / **Building Block (BB)** ist eine genotypische Teilstruktur, z. B.
`#10#1` (`#` = beliebig). Kennzahlen eines BB:
- **Ordnung** $o$: Anzahl festgelegter Stellen (`#10#1` → $o=3$).
- **Definierende Länge** $\delta$: Abstand der äußersten festgelegten Stellen
  (`#10#1` → $\delta=3$).

Das **Schema-Theorem** schätzt das Wachstum guter BBs ab:
$$\langle m(H,t{+}1)\rangle \ge m(H,t)\,\frac{f(H,t)}{\bar f(t)}\,
\Big[1 - p_c\,\frac{\delta(H)}{l-1}\Big]\,(1-p_m)^{o(H)}$$
- $m(H,t)$: Anteil der Individuen mit Schema $H$ zur Zeit $t$;
- $f(H,t)/\bar f(t)$: relative Fitness von $H$ (treibt Wachstum, **Selektion**);
- $p_c\,\delta(H)/(l-1)$: Wahrscheinlichkeit, dass **Crossover** $H$ zerreißt
  (steigt mit $\delta$ und Genomlänge $l$);
- $(1-p_m)^{o(H)}$: Wahrscheinlichkeit, dass **Mutation** $H$ verschont (sinkt mit $o$).

Lesart: **Kurze, niedrigordnungs- und überdurchschnittlich fitte** Bausteine
vermehren sich exponentiell. Konsequenz für die Biologie: Auch im biologischen
Genom müssen BBs *kompakt* kodiert sein, um propagiert/rekombiniert zu werden, ohne
zerstört zu werden.

### Take-Over Time (Selektion allein)

Die **Take-Over Time (TOT)** misst, wie lange das beste Individuum braucht, um die
ganze Population zu „übernehmen". Beispiele:
- **Truncation-Selektion** mit 50 %: $\text{TOT} = \log_2 N$;
- **Tournament-Selektion** (Turniergröße 2): $\text{TOT} = \log_2 N$;
- **Roulette-Wheel**: abhängig von Verteilung/Skalierung der Fitnesswerte.

### Goldbergs Kontrollkarte: Race, Sweet Spot, Hurdle

Aus [[Goldberg (1998) The Race the Hurdle and the Sweet Spot|Goldberg (1998)]]:

- **The Race**: Wettrennen zwischen **Innovationszeit** $t_i$ (mittlere Zeit, bis
  Rekombination etwas Besseres findet) und **Take-Over Time** $t^*$. Ist
  $t_i \le t^*$ → **steady-state innovation** (vor der Konvergenz wird Neues
  gefunden, „Innovationsuhr" wird zurückgesetzt). Ist $t_i > t^*$ → **vorzeitige
  Konvergenz** (Population konvergiert, bevor Innovation greift; `11111` × `11111`
  = `11111`, Diversität weg).
- **Sweet Spot / Control Map**: Im Raum (Selektionsdruck $s$, Crossover-Wahrschein-
  lichkeit $p_c$) gibt es eine Erfolgszone, begrenzt durch **Drift** (zu schwache
  Selektion → stochastische Fixierung), **Mixing/Innovation Boundary** (zu wenig
  Crossover → vorzeitige Konvergenz) und **Cross-Competition** (zu hohe Selektion →
  selbst unabhängige Merkmale konkurrieren, Diversität bricht zusammen).
- **The Hurdle**: Bei schweren Problemen (BBs größer als ein Bit) schrumpft der
  Sweet Spot, und einfache Crossover-Operatoren skalieren exponentiell schlecht.
  Lösung: „kompetente" GAs, die **Bausteine erst identifizieren, bevor sie zwischen
  ihnen entscheiden** (fast messy GA, gemGA, LLGA) → subquadratische Skalierung.

### Reellwertige Optimierung & ES

- **1/5-Regel** (Evolutionsstrategien): Erfolgswahrscheinlichkeit $p_e$ > 1/5 →
  Mutationsstreuung $\sigma$ vergrößern (schneller voran), sonst verkleinern
  (lokaler suchen).
- **CMA-ES** adaptiert eine ganze Kovarianzmatrix; verwandt mit **Policy Gradients**
  im [[Reinforcement Learning]]. **EDAs** (z. B. BOA) modellieren die Population
  (z. B. Bayes-Netz), um BBs automatisch zu finden.

## Worked example (Take-Over Time)

Population $N = 256$, 4 Individuen „A" mit $f(A)=64$, 252 „B" mit $f(B)=1$.
Bei **Truncation 50 %** verdoppelt sich der beste Anteil pro Generation, also
$\text{TOT} = \log_2 256 = 8$ Generationen, bis alles „A" ist. (Tutoriums-/
Übungsthema; Rechnung als Übung in [[Tutorien – Übersicht und Diskussionsfragen]].)

## Role in this class or project

VL03 nutzt EAs doppelt: (1) als **Werkzeug**, um zu verstehen, *was die biologische
Evolution geleistet haben könnte* (Nischen, Building Blocks, Kompaktheit des Codes),
und (2) als allgemeines Optimierungstool, das später für Verhaltens-/
Parameteroptimierung (z. B. CMA-ES für Policy Gradients) wiederkehrt.

## Exam, assignment, or project relevance

Grundalgorithmus + Terminologie; Fitnesslandschaften (One-Max/Needle/Trap);
Schema-Theorem mit allen Termen erklären; Ordnung/definierende Länge berechnen;
Take-Over-Time-Rechnungen; Goldbergs Race/Sweet-Spot/Hurdle. Sehr klausurrelevanter
„praktischer" Block. Übungen 1–2.

## Related global concepts

- [[Evolutionary Algorithms]] (allgemeine Seite: Schema-Theorem, Fitnesslandschaften, Goldbergs Race)
- [[Reinforcement Learning]] (CMA-ES ↔ Policy Gradients)

## Related local pages

- [[Drei zeitliche Perspektiven]]
- [[Reinforcement Learning]] (Verwandtschaft CMA-ES ↔ Policy Gradients)

## Common confusions

EAs sind **blind**: Es gibt kein Modell, das Mutationseffekte vorhersagt. Der „Trick"
liegt nicht in Intelligenz der Operatoren, sondern in der **Balance** zwischen
Selektion und Rekombination (Goldbergs Race). Und: Das Schema-Theorem erklärt vor
allem, *wann ein bereits gefundener* BB wächst – nicht, wie neue BBs entdeckt werden.

## Sources

VL03 (Phylogenese & Evolutionäre Algorithmen); Goldberg (1998); Holland (1975).
