---
type: concept
status: active
scope: local
classes: [Kognitive Architekturen]
projects: []
domains: [developmental psychology, cognitive architecture]
sources: ["[[VL04 Ontogenetische Entwicklung]]", "[[Lin et al. (2022) Infants Physical Reasoning]]"]
created: 2026-06-09
updated: 2026-06-09
---

# Kernwissen und das Zwei-Systeme-Modell

## Short definition

Säuglinge kommen mit einem **Kernwissen** (*core knowledge*) aus angeborenen
Prinzipien und Konzepten zur Welt, das ihr Schließen über physikalische Ereignisse
leitet. Die kognitive Architektur dahinter trennt ein **Objekt-Daten-File-System**
(was/wo eines Objekts) von einem **Interaktions-/Physical-Reasoning-System** (wie
sich Ereignisse entfalten).

## Intuition

Ein Baby ist kein „leeres Blatt". Es bringt eine grobe Physik mit – Dinge
verschwinden nicht einfach, fallen wenn ungestützt, stoßen sich beim Zusammenprall.
Aber es nutzt dieses Wissen **selektiv**: Je nach Ereignistyp (etwas wird hinter
einer Platte versteckt vs. in einem Becher) achtet es auf andere Eigenschaften.
Wie ein Anfänger, der je nach Situation nur auf das achtet, was er schon gelernt
hat zu beachten.

## Explanation

### Kernwissen (Lin, Stavans & Baillargeon, 2022)

Untersucht v. a. mit dem **Violation-of-Expectation (VoE)**-Paradigma: Babys schauen
**länger** auf physikalisch *unmögliche* Abläufe → Überraschung → Hinweis auf
Erwartung/Verständnis. Gemessen werden Fixationsorte und -dauern.

**Kernprinzipien** (Constraints auf Objektverhalten):
- **Persistenz**: Objekte bestehen fort, verschwinden/zerbrechen/verschmelzen/
  verwandeln sich nicht spontan; zwei Objekte teilen nicht denselben Raum (Solidität).
- **Trägheit (Inertia)**: Ruhende Objekte bleiben in Ruhe; bewegte folgen einer
  glatten Bahn – außer hinreichende Kräfte wirken.
- **Schwerkraft (Gravity)**: Ungestützte Objekte fallen.

**Kernkonzepte** (unbeobachtbare Erklärgrößen):
- **Selbst-generierte Kraft / interne Energie**: Selbstangetriebene („agentive")
  Objekte können spontan Kräfte erzeugen, Eigenbewegung kontrollieren und externen
  Kräften widerstehen. Babys finden es *nicht* überraschend, wenn ein
  selbstangetriebenes Objekt die Richtung ändert – ein inertes hingegen schon.
- **Kraft**: Ein Zusammenstoß überträgt Kraft (wie ein Richtungspfeil).

Erklärungen sind „**kinds of explanations**" (Keil): flach, ohne mechanistische
Details, aber ausreichend für viele Inferenzen.

### Das Verarbeitungskapazitäts-Argument (A-nicht-B)

Ein scheinbarer **Widerspruch**: Im VoE zeigen schon junge Babys Objektpermanenz –
aber im **A-nicht-B-Fehler** (Piaget) suchen sie ein Objekt an der *alten* Stelle A,
obwohl sie es bei B verstecken sahen. Auflösung: **begrenzte
Verarbeitungskapazität**. Objektrepräsentation *und* gleichzeitig Greifhandlung
planen überfordert die Ressourcen; habituelles Verhalten zu überschreiben ist
„energetisch zu teuer". Das Wissen ist da – die *Handlung* scheitert an der Last.

### Ereignis-selektive Kodierung

Babys bilden **Ereigniskategorien** (Verstecken hinter Platte / im Behälter / unter
Tuch / in Röhre / vergraben; Kollisionen; Kopplungen) und kodieren Objektmerkmale
**ereignisspezifisch**. Welche Merkmale wann „identifiziert" sind, unterscheidet
sich pro Ereigniskategorie (**Décalages**, zeitliche Verschiebungen). Beispiele:
- **Höhenänderung** wird bei „hinter Platte" ab ~3,5 Mon. bemerkt, im Becher erst
  ~7,5 Mon., unter Tuch ~12 Mon., in Röhre ~14 Mon.
- **Oberflächenstabilität**: 5,5 Mon. „liegt, wenn oben aufgelegt" → 8 Mon.
  Kontaktpunktregel → 13 Mon. proportionale Volumenregel.

### Das Zwei-Systeme-Modell

Erklärt, warum Merkmale registriert, aber nicht genutzt werden (vgl. *change
blindness* bei Erwachsenen):

- **Objekt-Daten-File-System** (*object-file system*): temporäre, **detaillierte**
  Repräsentationen mit „**Wo**" (Lokalisation) und „**Was**" (alle Eigenschaften).
- **Interaktionsverarbeitungssystem** (*physical-reasoning system*): aktiviert bei
  kausaler Interaktion, baut eine **spezialisierte** Ereignisrepräsentation, teilt
  Rollen zu (Behälter vs. Objekt-im-Behälter), antizipiert den Ablauf und
  integriert **nur ereignis-relevante** „Was"-Merkmale (ruft sie aus dem Objekt-File
  ab). Ist ein Merkmal für die Ereigniskategorie noch nicht „identifiziert", wird es
  nicht abgerufen → das Baby bemerkt die Veränderung nicht (obwohl das Objekt-File
  sie kennt). Verwandt mit **Inattentional Blindness**.

Es gibt Hinweise, dass das Gehirn diese Aufteilung tatsächlich in verschiedenen
Arealen realisiert.

### Kernwissen im sozialen Kontext

- Ab ~6 Mon.: Babys erwarten, dass Agenten sich **rational** verhalten (Kosten
  minimieren; Liu & Spelke, 2017).
- Ab ~10 Mon.: Babys **verrechnen** Belohnung mit Bewegungsaufwand und leiten den
  *Wert* eines Ziels aus dem Aufwand ab (Liu et al., 2017) – ein früher Vorläufer
  von [[Reinforcement Learning|Werten/Belohnung]].

## Worked example

Selbstangetriebene Box hinter Schirm (Luo et al., 2009): Bei **einem** Schirm
schauen 6-Mon.-Babys länger (Box „verschwindet" magisch → Persistenzverletzung);
bei **zwei** Schirmen nicht (sie folgern, die Box nutze ihre interne Energie, um
hinter den zweiten Schirm zu schlüpfen). Prinzip (Persistenz) + Konzept (interne
Energie) greifen nahtlos ineinander.

## Role in this class or project

VL04 (Ontogenese) zeigt am Beispiel der frühkindlichen intuitiven Physik, **wie**
Verständnis progressiv und körpergrundiert entsteht und das
Symbolgrundierungsproblem teilweise löst. Die Zwei-System-Architektur ist ein
konkretes Beispiel für eine „kognitive Architektur".

## Exam, assignment, or project relevance

VoE-Paradigma erklären; Kernprinzipien vs. Kernkonzepte unterscheiden; A-nicht-B und
das Kapazitätsargument; ereignis-selektive Kodierung/Décalages; Objekt-File- vs.
Physical-Reasoning-System (inkl. *errors of omission/commission*). Tutorium 4 hat
genau diese Diskussionsfragen (Übung 3). Siehe
[[Tutorien – Übersicht und Diskussionsfragen]].

## Related global concepts

- [[Bayesian Inference]] (intuitive Physik als probabilistisches Schließen – Ausblick)
- [[Predictive Coding]] (Überraschung = Prädiktionsfehler)

## Related local pages

- [[Drei zeitliche Perspektiven]]
- [[Körpergrundierte Kognition]]
- [[Reinforcement Learning]] (Wert-aus-Aufwand-Inferenz)

## Common confusions

VoE und A-nicht-B widersprechen sich **nicht**: VoE misst *Wissen* (Schauen),
A-nicht-B misst *Handlung* unter Ressourcenlast. „Errors of omission" (ein
relevantes Merkmal fehlt) entstehen, wenn das Physical-Reasoning-System es noch
nicht für die Ereigniskategorie identifiziert hat – nicht, weil es nie kodiert wurde.

## Sources

VL04 (Ontogenetische Entwicklung); Lin, Stavans & Baillargeon (2022);
Liu & Spelke (2017); Liu et al. (2017); Luo et al. (2009).
