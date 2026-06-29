---
type: concept
status: active
scope: local
classes: [Kognitive Architekturen]
projects: []
domains: [motor control, prediction, cognitive architecture]
sources: ["[[VL07 Motivation Homöostase und Antizipation]]", "[[Blakemore et al. (2000) Why cant you tickle yourself]]"]
created: 2026-06-09
updated: 2026-06-09
---

# Ideomotorik und Antizipation

## Short definition

Das **ideomotorische Prinzip** besagt: Handlungen werden über ihre **antizipierten
Effekte** ausgewählt – wir tun das, von dem wir glauben, dass es den gewünschten
sensorischen Effekt erzeugt. **Antizipation** (Vorhersage über Vorwärtsmodelle) ist
der Grundbaustein flexiblen Verhaltens und „höherer" Kognition.

## Intuition

Bevor du das Licht anschaltest, hast du schon das Bild „Raum wird hell" im Kopf –
und *dieses* vorgestellte Ergebnis löst die Handbewegung zum Schalter aus, nicht
umgekehrt. Dein Gehirn arbeitet rückwärts: vom gewünschten Effekt zur Handlung. Und
es sagt ständig voraus, was es gleich fühlen wird – deshalb kannst du dich nicht
selbst kitzeln.

## Explanation

### Sensomotorische Kodes als Basis von Weltmodellen

Durch Interaktion werden sensomotorische Korrelationen erkannt und zu
**sensomotorischen Kodes** komprimiert. Sie ermöglichen Antizipation, flexible
Interaktion (Aktionsauswahl nach erwartetem Effekt) und Verständnis (Planung,
Simulation, Vorstellung). Sie bilden topologische Räume mit Distanzen/Nachbarschaften
– die Grundstruktur des kognitiven Apparats und Basis für Analogien/Wissenstransfer.

### Das ideomotorische Prinzip

Historisch: Herbart (1825), William James (1890): *„An anticipatory image … of the
sensorial consequences of a movement … is the … forerunner of our voluntary acts."*
Ablauf: Intendierte, erreichbar scheinende **Effekte** lösen die Aktion aus, von der
geglaubt wird, dass sie sie herstellt; die *generierten* Effekte werden mit den
*intendierten* verglichen ($\Delta$), um die sensomotorischen Modelle zu verfeinern.

**Antizipatives Verhaltenskontrollprinzip** (Hoffmann, 1993): Lernen beginnt mit
reflexartigen Bewegungen → (1) latente, **bidirektionale** Aktions-Effekt-
Assoziationen entstehen → (2) sie werden durch **Bedingungen** ausdifferenziert,
sobald sie nicht immer zutreffen (Bedingung–Aktion–Effekt).

### Vorwärts- und invers-gerichtete Prozesse

- **Vorwärts** (forward): Simulation von Verhalten/Effekten, Antizipation von
  Konsequenzen und Zielen; antizipative sensorische Verarbeitung (Erwartung wird mit
  Input verrechnet → Informationsfusion).
- **Invers** (inverse): zielgerichtete (Top-down-)Aufmerksamkeit; Ziele bestimmen
  Verhalten – die Differenz Soll–Ist initiiert zielgerichtete Planung.

### Das Reafferenzprinzip (von Holst & Mittelstaedt, 1950)

Schlüsselmechanismus der antizipativen Filterung:
- **Efferenz**: motorisches Kommando.
- **Efferenzkopie**: Kopie des Kommandos → speist ein **Vorwärtsmodell**, das die
  **antizipierte Reafferenz** (vorhergesagtes sensorisches Feedback, *corollary
  discharge*) erzeugt.
- **Reafferenz**: sensorischer Effekt der *eigenen* Bewegung.
- **Exafferenz**: sensorische Änderungen aus *anderen* (externen) Quellen.

Die antizipierte Reafferenz wird vom tatsächlichen Feedback **abgezogen**; übrig
bleibt die unerwartete Exafferenz. So filtert das System selbsterzeugte Effekte
heraus. Nutzen von Antizipation: (1) adaptives Filtern, (2) Ersetzen/Hinzufügen
fehlender oder verzögerter Inputs (Verzögerungskompensation), (3) Ausführungs-
kontrollsignal (Soll-Ist-Vergleich), (4) Ausführungsinitiator (Ziel-Start-Vergleich).

Drei Fehlerquellen, die adaptives Filtern nötig machen: **sensorisches Rauschen**
(aleatorisch), **Vorwärtsmodellfehler** (epistemisch), **unberücksichtigte externe
Einflüsse** (aleatorisch).

### Anwendung: Warum man sich nicht selbst kitzeln kann

[[Blakemore et al. (2000) Why cant you tickle yourself|Blakemore, Wolpert & Frith
(2000)]] zeigen genau diesen Mechanismus: Bei **selbst-erzeugter** Berührung sagt
das Vorwärtsmodell (via Efferenzkopie) das Gefühl voraus und **attenuiert** es →
weniger kitzlig. Legt man eine **Verzögerung** (100–300 ms) oder eine **Trajektorien-
rotation** (30–90°) zwischen Bewegung und Berührung, wächst die Diskrepanz zwischen
vorhergesagtem und tatsächlichem Feedback → es wird **kitzliger**, fast wie fremd-
erzeugt. (Patienten mit bestimmten Symptomen zeigen die Attenuation nicht.)

### Vom Sense-Think-Act zum körpergrundierten Ansatz

Der klassische **Sense-Think-Act-Zyklus** (erst wahrnehmen, dann denken/planen, dann
handeln) ist zu langsam und ruft Homunculus-/Rahmenproblem auf. Stattdessen:
Sensorik und Motorik laufen **parallel** und gekoppelt; das Motivationssystem steuert;
ein Weltmodell entsteht aus sensomotorischen Erfahrungen (siehe
[[Körpergrundierte Kognition]]).

## Worked example

Schnelles Greifen (Desmurget & Grafton, 2000): Während der Bewegung erzeugt ein
**Vorwärtsmodell** der Armdynamik aus der Efferenzkopie eine Vorhersage des Endpunkts,
die laufend mit dem Zielort verglichen wird. So ist Korrektur möglich, **bevor**
langsames sensorisches Feedback eintrifft – Antizipation ersetzt fehlendes Feedback.

## Role in this class or project

VL07 etabliert Antizipation als „Grundbaustein für höhere Kognition und das
Verstehen der Welt". Verbindet Redundanz/Flexibilität (viele Wege zum Ziel) mit
Weltmodellen $(S,A,T)$ aus [[Reinforcement Learning|modellbasiertem RL]] und liefert
die Brücke zu Wahrnehmung als Inferenz ([[Predictive Coding]]).

## Formal definition / equations

Reafferenz-Vergleich (schematisch): $\text{wahrgenommene Exafferenz} =
\text{tatsächliches Feedback} - \text{antizipierte Reafferenz}$. Soll-Ist-Differenz
$\Delta = \text{intendierter Effekt} - \text{generierter Effekt}$ steuert sowohl
Verhaltenskorrektur als auch Modelllernen.

## Exam, assignment, or project relevance

Ideomotorisches Prinzip (James/Herbart, Hoffmann); vorwärts vs. invers;
**Reafferenzprinzip** mit Efferenz/Efferenzkopie/Reafferenz/Exafferenz **zeichnen
und erklären**; Blakemore-Kitzelbefund als Anwendung; Sense-Think-Act-Kritik. Übung 5
und Blakemore-Diskussion (Tutorium 6). Siehe
[[Tutorien – Übersicht und Diskussionsfragen]].

## Related global concepts

- [[Predictive Coding]] (Wahrnehmung als Vorhersage + Prädiktionsfehler)

## Related local pages

- [[Motivation und Homöostase]]
- [[Körpergrundierte Kognition]]
- [[Reinforcement Learning]] (Weltmodell $T$ für Planung)

## Common confusions

**Reafferenz** (Folge der *eigenen* Bewegung) vs. **Exafferenz** (externe Änderung)
nicht verwechseln – die Efferenzkopie sagt nur die *Reafferenz* voraus, damit die
Exafferenz „übrig bleibt". Und: ideomotorisch wird die Aktion durch ihren
**antizipierten Effekt** ausgewählt, nicht durch einen vorgelagerten Reiz.

## Sources

VL07 (Motivation, Homöostase & Antizipation); Blakemore, Wolpert & Frith (2000);
von Holst & Mittelstaedt (1950); James (1890); Hoffmann (1993).
