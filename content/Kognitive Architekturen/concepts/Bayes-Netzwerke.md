---
type: concept
status: active
scope: local
classes: [Kognitive Architekturen]
projects:
domains: [probabilistic graphical models, inference, perception]
sources: ["VL09 Visuelle Wahrnehmung Top-Down", "Tutorien – Übersicht und Diskussionsfragen"]
created: 2026-06-17
updated: 2026-06-17
---

# Bayes-Netzwerke

## Short definition

Ein Bayes-Netzwerk ist ein **gerichteter azyklischer Graph (DAG)**, dessen Knoten
Zufallsvariablen und dessen Kanten direkte (bedingte) Abhängigkeiten sind. Es
**faktorisiert** eine gemeinsame Wahrscheinlichkeitsverteilung kompakt und erlaubt,
unter Unsicherheit zu schließen.

## Intuition

Statt eine riesige Tabelle „Wahrscheinlichkeit jeder möglichen Weltkombination“ zu
speichern, zeichnet man, **was direkt was beeinflusst**: Einbruch → Alarm, starker Wind →
Alarm, Alarm → Hund bellt, Alarm → Polizei kommt. Jeder Pfeil sagt „Eltern verursachen
Kind“. Aus diesem kleinen Bild kann man jede Frage beantworten („Wie wahrscheinlich ist
ein Einbruch, wenn der Hund bellt?“), ohne die volle Verbundtabelle je hinzuschreiben.
Das Netz ist also eine **kompakte, lesbare Landkarte der Abhängigkeiten**.

## Explanation

**Aufbau.** Knoten = Variablen (diskret = Quadrat, kontinuierlich = Kreis; schattiert =
beobachtet, leer = versteckt). Kanten = bedingte Abhängigkeiten. Der Graph ist
**gerichtet und azyklisch** (keine Schleifen). **Wurzeln** haben nur einen Prior;
**Blätter** haben keine Kinder. Jeder Knoten trägt eine **bedingte
Wahrscheinlichkeitstabelle/-verteilung** gegeben seine Eltern.

**Faktorisierung.** Die zentrale Ersparnis: die gemeinsame Verteilung ist das Produkt
der knotenweisen bedingten Verteilungen,
$p(x_1,\dots,x_n)=\prod_i p(x_i\mid \text{parents}(x_i))$. Statt einer in $n$
exponentiell großen Tabelle nur ein kleiner Faktor pro Knoten.

**Bedingte (Un-)Abhängigkeit und d-Separation.** Das Netz kodiert, welche Variablen
einander (un)abhängig sind. Zwei Knoten $X,Y$ sind durch eine beobachtete Menge $E$
**d-separiert** (→ unabhängig gegeben $E$), wenn alle ungerichteten Pfade zwischen ihnen
**blockiert** sind. Drei Pfadtypen entscheiden, ob ein Pfad blockiert:

- **Fork / tail-to-tail** ($X \leftarrow V \rightarrow Y$): gemeinsame Ursache $V$.
  *Unbeobachtet* sind $X,Y$ abhängig; **beobachtet man $V$, werden sie unabhängig.*
  Beispiel: Regen ist gemeinsame Ursache von „Straße nass“ und „Luftfeuchtigkeit“.
- **Chain / tail-to-head** ($X \rightarrow V \rightarrow Y$): Kette. *Unbeobachtet*
  abhängig; **beobachtet man das mittlere $V$, werden sie unabhängig.*
- **Collider / head-to-head** ($X \rightarrow V \leftarrow Y$): gemeinsame Wirkung $V$.
  **Umgekehrt!** *Unbeobachtet* sind $X,Y$ unabhängig; **beobachtet man $V$ (oder ein
  Kind von $V$), werden sie abhängig** – das ist „explaining away“ / interkausal.

![[d-separation.pdf]]
*Die drei d-Separations-Fälle. Bei Fork und Chain macht Beobachtung des mittleren Knotens
die Endknoten unabhängig; beim Collider ist es genau umgekehrt – Beobachtung der
gemeinsamen Wirkung macht die Ursachen abhängig.*

**Vier Arten der Deduktion** (Schließen über das Netz):

1. **Prädiktiv** (Wurzel → Blatt): aus Ursachen Erwartungen über Wirkungen erzeugen,
   per Marginalisierung. „Gegeben Farb-/Formdetektor, wie wahrscheinlich ist die Tasse?“
2. **Diagnostisch** (Blatt → Wurzel): aus beobachteter Wirkung auf die Ursache schließen,
   per Bayes-Regel. „Untertasse gesehen – wie wahrscheinlich eine Tasse?“
3. **Kombiniert**: Evidenz von „oben“ und „unten“ zugleich (erst prädiktiv, dann
   diagnostisch verrechnen).
4. **Interkausal**: zwei a-priori unabhängige Ursachen werden **abhängig**, sobald ihre
   gemeinsame Wirkung beobachtet ist (Collider; „explaining away“).

## Worked example

**Tassen-Netz** $A,B \rightarrow O \rightarrow C,N$. $A$ = Farbdetektor (rot-braun, Tee),
$B$ = Formdetektor (Tassenform), $O$ = „Objekt ist eine Tasse“, $C$ = greifen, $N$ =
Untertasse in der Nähe.

![[bayes-net-tasse.pdf]]
*Das Tassen-Bayes-Netz aus VL09: zwei Feature-Detektoren als Eltern von $O$, und zwei
Konsequenzen $C,N$ als Kinder von $O$.*

Mit $p(a)=0.2$, $p(b)=0.1$ und der Tabelle $p(o\!=\!T\mid A,B)$ (TT: 0.95, TF: 0.6, FT:
0.5, FF: 0.01):

- **Prädiktiv ohne Evidenz** (Marginalisierung über $A,B$):
  $p(O\!=\!T)=\sum_{a,b} p(O\!=\!T\mid a,b)\,p(a)\,p(b)$
  $=0.95(0.2)(0.1)+0.6(0.2)(0.9)+0.5(0.8)(0.1)+0.01(0.8)(0.9)\approx 0.16$.
- **Prädiktiv mit Evidenz $a=T$:** $p(O\!=\!T\mid a\!=\!T)=0.95(0.1)+0.6(0.9)=0.635$.
- **Diagnostisch:** beobachte $N\!=\!T$ und schließe zurück auf $O$ via
  $p(O\mid N)\propto p(N\mid O)\,p(O)$.

(Eine zweite klassische Übung ist das **Alarm-Netz** Einbruch/Wind → Alarm → Hund/Polizei
aus Tutorium 8 – gleiche Mechanik: faktorisieren, marginalisieren, Bayes anwenden.)

## Formal definition / equations

Faktorisierung: $p(x_1,\dots,x_n)=\prod_{i=1}^{n} p(x_i\mid \text{parents}(x_i))$.
Diagnostische Deduktion (ein Elternknoten):
$$ p(o\mid n)=\frac{p(n\mid o)\,p(o)}{p(n)}; \qquad
\text{mit weiterem Elter } X:\ p(o\!=\!T\mid n\!=\!T)=
\frac{\sum_X p(n\mid o,X)\,p(o\mid X)\,p(X)}{p(n)}. $$
Bedingte Tabellen: diskreter Knoten mit diskreten Eltern → **Wahrscheinlichkeitstabelle**;
diskretes Kind mit kontinuierlichen Eltern → **Likelihood-Funktion**; kontinuierliches
Kind → **Wahrscheinlichkeitsdichteverteilung** (siehe [[Gaußsche Mischmodelle]]).

## Role in this class or project

Die diskrete Maschinerie generativer Modelle in [[VL09 Visuelle Wahrnehmung Top-Down]]:
Bayes-Netze zeigen, **wie** Top-down-Erwartungen formal mit Bottom-up-Evidenz verrechnet
werden. Brücke zu [[Generative und diskriminative Modelle]] und – im Kontinuierlichen –
zu [[Gaußsche Mischmodelle]].

## Exam, assignment, or project relevance

Kern des **praktischen Klausurteils** (Tutorium 8 / Übungsblatt 8): ein Netz
faktorisieren; $p(E,W,A)$ für alle Kombinationen berechnen; die vier Deduktionsarten
benennen und je eine kleine Rechnung führen; **d-Separation** auf konkrete Knotenpaare
anwenden (welche sind (un)abhängig, gegeben was?), insbesondere den **Collider-Fall**
nicht mit Fork/Chain verwechseln. Die Wahrscheinlichkeitsregeln stehen in der
[[Formelsammlung (Tutorium)]].

## Related global concepts

[[Bayesian Network]] (allgemeine Seite), [[Bayes' Theorem]], [[Bayesian Inference]]
(Grundlage), [[Predictive Coding]] (hierarchische Vorhersage),
[[Marr's Levels of Analysis]].

## Related local pages

[[Generative und diskriminative Modelle]], [[Gaußsche Mischmodelle]],
[[VL09 Visuelle Wahrnehmung Top-Down]], [[Tutorien – Übersicht und Diskussionsfragen]].

## Common confusions

- **Collider verkehrt herum.** Bei Fork/Chain macht **Beobachten** des Mittelknotens
  unabhängig; beim Collider macht **Beobachten** der Wirkung **abhängig**. Häufigster
  Fehler.
- **Kante ≠ Korrelation in eine Richtung.** Pfeilrichtung kodiert die generative
  Abhängigkeit (Eltern → Kind), nicht „kausalen Fluss der Inferenz“ – diagnostisch
  schließt man entgegen der Pfeile.
- **„Keine Kante = unabhängig.“** Nicht unbedingt: Abhängigkeit kann über Pfade laufen;
  erst d-Separation gibt die korrekte Antwort.

## Sources

VL09 (Folien: Bayes-Netzwerke I–IV, d-Separation, vier Deduktionsarten, Tassen-Beispiel);
Tutorium 8 (Alarm-Netz, d-Separation-Wiederholung).
