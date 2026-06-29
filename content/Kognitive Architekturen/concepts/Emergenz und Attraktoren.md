---
type: concept
status: active
scope: local
classes: [Kognitive Architekturen]
projects: []
domains: [cognitive science, robotics, dynamical systems]
sources: ["[[VL02 Emergenz und drei zeitliche Perspektiven]]", "[[Brooks (1990) Elephants Dont Play Chess]]"]
created: 2026-06-09
updated: 2026-06-09
---

# Emergenz und Attraktoren

## Short definition

**Emergentes Verhalten** entsteht indirekt aus einfachen, modularen Kopplungen
(Körper–Sensor–Motor–Umwelt), ohne dass es zentral berechnet oder gezielt geplant
wird. Stabile, störungsrobuste Muster solchen Verhaltens heißen **Attraktoren**.

## Intuition

Niemand „berechnet" eine Ameisenstraße – sie entsteht von selbst, weil jede Ameise
einer simplen Pheromon-Heuristik folgt. Das Muster (die effiziente Straße) ist
*mehr* als die Summe der Einzelregeln: es **emergiert**. Und es ist stabil – stört
man es leicht, kehrt es zurück. Solche stabilen Zustände sind „Attraktoren", weil
das System wie von selbst hineinläuft.

## Explanation

**Morphologische Berechnung** (*morphological computation*): Der Körper selbst
„rechnet". Beispiele:

- **Passive Walker** gehen einen Abhang hinunter ganz ohne Motor/Steuerung – die
  Mechanik erledigt die „Berechnung".
- Elastische Beine/Muskel-Sehnen-Systeme stabilisieren Lokomotion automatisch und
  *reduzieren* damit nötige Rechenarbeit (Pfeifer & Bongard, 2006).
- **Insektenaugen**: Die gekrümmte, ungleichförmige Facettenanordnung macht die
  Berechnung des **optischen Flusses** trivial. Geschwindigkeit des optischen
  Flusses korreliert direkt mit der Distanz – damit halten Insekten Abstand und Höhe
  und timen die Landung (maximale Flussexpansion → landen).

**Emergente / morphologische Attraktoren**: Aus Körper-Sensor-Motor-Kopplung
entstehen dynamische Attraktoren (gehen, traben, galoppieren, springen) und
Körperhaltungen (sitzen, liegen). Attraktoren sind teilweise störungsstabil und
**hervorragend zur Symbolisierung geeignet** – sie lassen sich „benennen" und
bilden so eine Brücke zum Symbolgrundierungsproblem (siehe
[[Vier Kernprobleme der Kognitionswissenschaft]]).

**Braitenberg-Fahrzeuge** (Braitenberg, 1984): Direkte Kopplung von Sensorsignal zu
Motoraktivität erzeugt scheinbar zielgerichtetes Verhalten (Hinfahren zur/Wegfahren
von einer Lichtquelle), je nach erregender/hemmender und gerader/gekreuzter
Verschaltung. Froschverhalten: kleiner schneller optischer Fluss → Zunge (Fressen);
großer dunkler expandierender Fluss → Flucht.

**Kollektive Emergenz**: Ameisenstraßen (Pheromone, kürzeste Wege akkumulieren mehr
Pheromon); „Schweizer Roboter" (Didabots) schieben Blöcke zu Haufen zusammen –
obwohl sie nur Braitenberg-artige Distanzsensor-Motor-Kopplungen haben und „nichts"
über Haufen wissen.

### Das Beobachterproblem (frame-of-reference problem)

**Vorsicht bei der Interpretation von Verhalten!** Was der Beobachter sieht (die
Ameise „plant eine komplexe Hindernis-vermeidende Trajektorie") und was der Agent
tut (folge grober Sonnenrichtung, minimiere Distanz per Snapshot) können
fundamental auseinanderfallen. Unsere Deutungen sind durch menschliches Wissen und
kulturelle Standards verzerrt (Heider & Simmel, 1944: wir schreiben bewegten
Dreiecken Absichten zu). Kognitive Architekturen als **Modelle** helfen, Verhalten
*mechanistisch* statt projizierend zu beschreiben.

## Worked example

Insekt fliegt mittig zwischen zwei Wänden: Es hält den optischen Fluss links =
optischen Fluss rechts. Kommt eine Wand näher, steigt deren Flussgeschwindigkeit,
das Insekt weicht aus, bis beide wieder gleich sind – ein Attraktor „Mittellinie",
ganz ohne Distanzberechnung. (Tutoriumsaufgabe, siehe
[[Tutorien – Übersicht und Diskussionsfragen]].)

## Role in this class or project

VL02 etabliert Emergenz als Erklärungsprinzip „von unten" und als Gegengewicht zu
zentralistischen Architekturen – die Brücke von [[Körpergrundierte Kognition]] zu
[[Brooks (1990) Elephants Dont Play Chess|Brooks' Subsumption]] und zu den späteren,
„höheren" Mechanismen.

## Formal definition / equations

Optischer Fluss (retinale Abbildung, aus der Formelsammlung):
$$v_x(x,y) = \frac{T_x + x\,T_z}{Z}, \qquad v_y(x,y) = \frac{T_y + y\,T_z}{Z}$$
mit Bildkoordinaten $(x,y)$, Translationskomponenten $(T_x,T_y,T_z)$ der
Eigenbewegung und Tiefe $Z$. Kernaussage: Bei reiner Vorwärtsbewegung ($T_z$)
skaliert der Fluss **invers mit der Tiefe** $Z$ – nahe Dinge erzeugen schnelleren
Fluss. Genau das nutzt morphologische Distanz-/Höhenkontrolle.

## Exam, assignment, or project relevance

Emergentes vs. geplantes Verhalten; morphologische Berechnung mit Beispielen;
Attraktoren und ihre Rolle für Symbolisierung; **Beobachterproblem** sauber erklären.
Optischer Fluss taucht später (Übung 6) und in der Formelsammlung auf.

## Related global concepts

- [[Predictive Coding]] (spätere, „höhere" Form modellbasierter Verarbeitung)

## Related local pages

- [[Körpergrundierte Kognition]]
- [[Drei zeitliche Perspektiven]]
- [[Vier Kernprobleme der Kognitionswissenschaft]]

## Common confusions

„Emergent" heißt nicht „magisch" oder „unerklärlich" – im Gegenteil, es heißt
*mechanistisch aus einfachen lokalen Regeln ableitbar*. Und Attraktoren sind keine
Orte im Raum, sondern stabile Zustände/Muster im Zustandsraum des gekoppelten
Systems.

## Sources

VL02 (Emergenz und drei zeitliche Perspektiven); Braitenberg (1984);
Pfeifer & Bongard (2006); Heider & Simmel (1944).
