---
type: concept
status: active
scope: local
classes: [Kognitive Architekturen]
projects: []
domains: [motivation, cognitive architecture, AI]
sources: ["[[VL07 Motivation Homöostase und Antizipation]]"]
created: 2026-06-09
updated: 2026-06-09
---

# Motivation und Homöostase

## Short definition

Damit ein autonomes System überhaupt zielgerichtet handelt, braucht es **Eigen-
motivation**. Man unterscheidet **intrinsische/epistemische** Motivation (Wissens-
erwerb: Neugier, Überraschung) und **extrinsische/homöostatische** Motivation
(inneres Gleichgewicht erhalten).

## Intuition

[[Reinforcement Learning]] optimiert Verhalten gegeben eine Belohnung – aber
*woher kommt die Belohnung?* Ein Tier, dem nie etwas „wichtig" ist, würde nichts
tun. Motivation liefert die Belohnung von innen: Hunger drängt zur Futtersuche
(Gleichgewicht halten), Neugier drängt zum Erkunden (Wissen sammeln). Verhalten ist
das emergente Ergebnis konkurrierender Motivationen.

## Explanation

### Intrinsische / epistemische Motivation

Ziel: **Informationsgewinn** maximieren.
- **Neugier**: Suche nach Wissen über die Umwelt.
- **Überraschung**: Eintreten von Unerwartetem → triggert Neugier (Suche nach
  Erklärung).
- Einfache Kriterien: explorieren, was am längsten nicht getan wurde; Unsicherheit
  reduzieren (Vorhersagefehler minimieren). Problem: Umwelten mit prinzipiell
  unvorhersagbaren Regionen (man würde ewig auf „Rauschen" starren).
- Besseres Kriterium (**Schmidhuber, 1991**): nicht den Fehler, sondern die
  **erwartete Wissensverbesserung** maximieren – die *Veränderung* des
  Vorhersagefehlers. Wo schon viel bekannt ist, ist wenig zu lernen → dorthin keine
  Lernenergie. Muss **lokal/kontextuell** abgeschätzt werden. Umsetzbar mit
  RL-Methoden (Wissensgewinn als „Belohnung").

### Extrinsische / homöostatische Motivation

**Homöostase** = aktives Erhalten eines inneren Gleichgewichts (verwandt mit
**Autopoiese**, Maturana: Grundprinzip des Lebens). Komplexes Verhalten (z. B.
Futtersuche) entsteht im Dienst der Gleichgewichtserhaltung.

**Reservoir-Modell („Hullian Drives")**: Der Füllstand $\sigma_x$ eines
Motivationsmoduls $x$ wird durch eine Sigmoidfunktion $\omega(\sigma_x)$ skaliert und
mit einem globalen Relevanzgewicht $p_x$ multipliziert. **Ein leeres Reservoir →
starke Motivation.** Zwei Arten:
- **Konsum-basiert**: Reservoir wird durch eine Konsumhandlung gefüllt (z. B.
  Energieaufnahme); Auffüllen kann ein Belohnungssignal auslösen; Erfolg ist an Ort/
  Kontext gebunden → Lernen assoziiert Ort/Kontext mit Motivation (Werteiteration
  per modellbasiertem [[Reinforcement Learning|RL]]).
- **Eigenschafts-basiert**: Reservoir wird durch Umwelteigenschaften manipuliert
  (z. B. Bewegung durch sichere Gebiete lindert Angst) → es entsteht eine
  **Prioritätenkarte**.
- Soziale Motivationen: Verstehen anderer für Kooperation, Schutz, Angriff.

### Emergentes, selbst-motiviertes Verhalten

Beispiel: Ein System baut eine „kognitive Karte" (z. B. *time-growing neural gas*),
assoziiert Neuronen (place fields) mit Motivationen (Hunger), inhibiert sie nach
Konsum temporär; „Neugier" sucht neue Futterstellen; „Angst" meidet offene Bereiche
(Schutz an Wänden/Ecken). Aus dem Wettbewerb von Hunger und Angst entsteht
emergentes, kontinuierliches Verhalten (siehe [[Emergenz und Attraktoren]]).

## Worked example

Ein Roboter mit „Hunger"- und „Angst"-Reservoir: Beide leer → starke, konkurrierende
Motivation. Ist die Angst hoch, bleibt er an Wänden und füllt Hunger nur an sicheren
Futterstellen; sinkt die Angst, exploriert er offener nach neuen Quellen. Es gibt
keine fest programmierte Route – das Verhalten emergiert aus den
Reservoir-Dynamiken.

## Role in this class or project

VL07 schließt die Lücke von [[Reinforcement Learning]]: RL/Policy-Gradients
optimieren *eine* gegebene Belohnung; Motivation erklärt, **woher** die
körpergrundierte Wertefunktion $R$ kommt und wie ein System sich **selbst** Ziele
setzt – Voraussetzung für flexibles, autonomes Verhalten.

## Formal definition / equations

Motivationsstärke (schematisch): $m_x = p_x \cdot \omega(\sigma_x)$, mit Sigmoid
$\omega$, Reservoirfüllstand $\sigma_x$ und Relevanzgewicht $p_x$. Da $\omega$
fallend im Füllstand ist, gilt: niedriger Füllstand → hohe Motivation.

## Exam, assignment, or project relevance

Intrinsisch/epistemisch vs. extrinsisch/homöostatisch; Neugier & Überraschung;
Schmidhubers „erwartete Wissensverbesserung" (warum nicht bloß Fehler minimieren);
Reservoir/Hullian-Drives; konsum- vs. eigenschaftsbasiert; emergentes
selbst-motiviertes Verhalten. (Übung 5 „Flexibilität".)

## Related global concepts

- [[Predictive Coding]] (Überraschung als Prädiktionsfehler)

## Related local pages

- [[Reinforcement Learning]]
- [[Ideomotorik und Antizipation]]
- [[Emergenz und Attraktoren]]

## Common confusions

Reine **Fehlerminimierung** ist als Neugier-Kriterium *schlecht*: In rein zufälligen
(„rauschenden") Umweltregionen bleibt der Fehler hoch und das System bliebe ewig
hängen. Deshalb belohnt man die *Verringerung* des Fehlers (Lernfortschritt), nicht
den Fehler selbst.

## Sources

VL07 (Motivation, Homöostase & Antizipation); Schmidhuber (1991);
Maturana (Autopoiese); Hull (Drives).
