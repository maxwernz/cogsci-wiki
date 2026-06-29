---
type: source_note
status: processed
scope: local
class: Kognitive Architekturen
project:
source_type: paper
raw_path: "raw/Paper zum Diskutieren/Brooks (1990)_ Elephants Dont Play Chess.pdf"
exercise_ref: "Übung 1 (Subsumption); Tutorium 2"
created: 2026-06-09
updated: 2026-06-09
---

# Brooks (1990) – Elephants Don't Play Chess

> Diskussionspaper. Relevant für **Übung 1 (Subsumption)** und **Tutorium 2**. Hier
> bewusst **keine** Übungs-/Tutoriumsaufgabeninhalte.

## Summary

Brooks formuliert eine **Alternative zur klassischen, symbolischen KI**: Statt
abstrakte Symbole zu manipulieren (deren Grundierung selten gelingt), soll
Intelligenz aus **fortlaufender physischer Interaktion mit der Umwelt** entstehen.
Kernideen: die **Physical Grounding Hypothesis** und die **Subsumptionsarchitektur**.
Der Titel: Elefanten sind hochintelligent (Wahrnehmung, Navigation, Sozialverhalten),
ohne Schach zu spielen – Intelligenz ≠ symbolisches Schließen.

## Key points

- **Kritik an der „Physical Symbol System Hypothesis"** (Newell & Simon): Symbolische
  KI steckt in „incrementalism" fest; ungegründete Repräsentationen liefern keine
  echte Intelligenz.
- **Physical Grounding Hypothesis**: Intelligente Systeme müssen ihre
  Repräsentationen in der physischen Welt **verankern**; die Welt ist „ihr eigenes
  bestes Modell" – Sensorik liest sie direkt aus, statt sie intern abzubilden.
- **Subsumptionsarchitektur**: Verhalten wird in **Schichten** (layers of competence)
  organisiert, die parallel und weitgehend unabhängig laufen; höhere Schichten
  **subsumieren** (unterdrücken/überschreiben) tiefere. Kein zentrales Modell, keine
  zentrale Planung. Aufgebaut aus einfachen endlichen Automaten (AFSMs).
- **Mobile Roboter** (z. B. Allen, Herbert) zeigen robustes, situiertes Verhalten ohne
  symbolische Repräsentation („Intelligence without representation/reason").

## Important concepts

[[Emergenz und Attraktoren]] (situiertes, emergentes Verhalten);
[[Körpergrundierte Kognition]] (Physical Grounding); Subsumptionsarchitektur;
situated activity.

## Methods, models, or theories

Subsumptionsarchitektur (geschichtete, prioritätsbasierte Verhaltenssteuerung);
behavior-based robotics; AFSMs (augmented finite state machines).

## Local relevance

Direkte Fortsetzung von [[VL02 Emergenz und drei zeitliche Perspektiven]]
(Brooks/Minsky/Pfeifer). Die Subsumptions-Idee taucht später wieder auf, etwa beim
Rennwagen-Controller in [[VL06 Belohnungslernen II]]. Gegenpol zur symbolischen KI
und zum Sense-Think-Act-Zyklus.

## Exam or project relevance

Physical Symbol System vs. Physical Grounding Hypothesis; Subsumptionsarchitektur
(Schichten, Subsumption, kein zentrales Modell); „Intelligence without
representation"; warum bottom-up/situiert. Übung 1.

## Links to global concepts

[[Marr's Levels of Analysis]] (Verschiebung weg von expliziter
komputational-symbolischer Repräsentation hin zur situierten algorithmischen Ebene).

## Open questions

Skaliert reine Subsumption zu „höherer" Kognition (Sprache, Abstraktion)? Brooks ist
optimistisch; der Kurs ergänzt später lern-, modell- und antizipationsbasierte
Mechanismen.
