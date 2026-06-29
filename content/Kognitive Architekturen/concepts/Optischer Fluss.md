---
type: concept
status: active
scope: local
classes: [Kognitive Architekturen]
projects:
domains: [visual perception, motion, computer vision]
sources: ["VL08 Visuelle Wahrnehmung Bottom-Up", "Formelsammlung (Tutorium)", "Tutorien – Übersicht und Diskussionsfragen"]
created: 2026-06-17
updated: 2026-06-17
---

# Optischer Fluss

## Short definition

Der optische Fluss ist das **Vektorfeld der Bildbewegung**: Er gibt für jeden Bildpunkt
an, in welche Richtung und wie schnell sich das projizierte Bild über die Zeit
verschiebt – sei es durch Eigenbewegung des Betrachters oder durch Bewegung der Objekte.

## Intuition

Schau aus dem Seitenfenster eines fahrenden Zugs: Nahe Objekte rauschen schnell vorbei,
ferne Berge ziehen langsam. Schaust du dagegen **nach vorne** beim Gehen, scheint die
Welt aus einem Punkt vor dir nach außen zu „explodieren“ – Türrahmen und Boden wandern
vom Zentrum zum Bildrand. Genau dieses Muster aus Pfeilen ist der optische Fluss. Sein
Trick: Aus reiner 2D-Bildbewegung lässt sich 3D-Information (Tiefe, Eigenbewegung, Zeit
bis zum Aufprall) zurückrechnen, ohne die Szene je „verstanden“ zu haben.

## Explanation

Kanten und Texturen sind **statische** Informationsquellen. Sobald sich etwas bewegt –
der Betrachter oder ein Objekt –, kommt eine reiche **dynamische** Quelle hinzu. Der
optische Fluss charakterisiert diese Bildveränderung. Man unterscheidet die
kontinuierliche Verschiebung (z. B. durch Objektbewegung) von der sprunghaften
Re-Lokalisierung (z. B. durch eine Augensakkade).

Formal ist der Fluss ein Vektorfeld mit horizontaler Komponente $v_x(x,y,t_0)$ und
vertikaler Komponente $v_y(x,y,t_0)$ am Bildpunkt $(x,y)$ zur Zeit $t_0$. Lokal lässt er
sich besonders gut **an Kanten** messen (dort ändert sich die Helligkeit), und über
Flächen integrieren, wenn genug Textur vorhanden ist. Bei verrauschter oder texturarmer
Wahrnehmung wird er unzuverlässig.

Der entscheidende Sonderfall ist **Eigenbewegung**. Bewegt sich der Betrachter ohne
Drehung mit der Translation $(T_x,T_y,T_z)$, dann gibt es genau einen Bildpunkt ohne
Fluss – den **Fokusexpansionspunkt** (focus of expansion, FoE) bei
$(-T_x/T_z,\,-T_y/T_z)$. Um diesen Punkt strömt das ganze Bild radial nach außen; je
weiter ein Punkt vom FoE entfernt ist und je näher das Objekt, desto größer der
Flussvektor. Diese Geometrie ist eine **emergente Informationsquelle**: Sie verrät die
Bewegungsrichtung (der FoE liegt dort, wohin man sich bewegt) und – über die Zeit
integriert – die Tiefe.

Weil der Fluss aber **vor allem von der eigenen Bewegung** dominiert wird, muss das
Gehirn den eigenbewegungsbedingten Fluss herausfiltern, um **Fremdbewegung** zu
erkennen. Genau das leistet das **Reafferenzprinzip** (antizipierter, selbstverursachter
Fluss wird abgezogen) – siehe [[Ideomotorik und Antizipation]]. Neuronal beginnt die
Bewegungsverarbeitung schon in V1 (richtungsselektive Zellen, laterale Propagierung über
die retinotopische Karte; einfachstes Modell: **Reichardt-Detektor**) und kulminiert in
MT/V5.

## Worked example

**Fokusexpansionspunkt.** Du gehst geradeaus und leicht nach rechts:
$T_x=1,\ T_y=0,\ T_z=4$ (vorwärts dominiert). Dann liegt der FoE bei
$$ \Big(-\tfrac{T_x}{T_z},\,-\tfrac{T_y}{T_z}\Big)=\Big(-\tfrac14,\,0\Big)=(-0.25,\,0). $$
Der „Pol“, aus dem die Welt nach außen strömt, sitzt also knapp links der Bildmitte –
konsistent damit, dass du dich leicht nach rechts bewegst.

**Zeit bis zum Kontakt.** Eine Fliege fliegt mit $T_z$ auf eine Wand in Distanz $Z$ zu.
Die Zeit bis zum Aufprall ist
$$ t = \frac{Z}{T_z}. $$
Bei $Z=2\,\text{m}$ und $T_z=0.5\,\text{m/s}$ also $t=4\,\text{s}$. Das Schöne: Der
optische Fluss kodiert genau diese (inverse) Rate **direkt** – die Fliege muss $Z$ und
$T_z$ nie einzeln kennen, um rechtzeitig zu landen. Tauben erzeugen denselben Effekt
durch Vor-/Zurück-Bewegungen des Kopfes.

## Formal definition / equations

Vektorfeld des Flusses: $v_x(x,y,t_0)$, $v_y(x,y,t_0)$ = horizontale/vertikale
Bildbewegung am Punkt $(x,y)$ zur Zeit $t_0$. Für reine Translation (kein Rotieren)
liefert die Projektionsgeometrie eine Form
$$ v_x(x,y)=\frac{T_x + x\,T_z}{Z}, \qquad v_y(x,y)=\frac{T_y + y\,T_z}{Z}, $$
mit Szenentiefe $Z$ am betreffenden Punkt. Setzt man $v_x=v_y=0$, erhält man den
Fokusexpansionspunkt $(x,y)=(-T_x/T_z,\,-T_y/T_z)$. Definiert man $x' := x + T_x/T_z$ und
$y' := y + T_y/T_z$ (Koordinaten relativ zum FoE), so wächst der Fluss linear mit dem
Abstand vom FoE und skaliert mit $T_z/Z$ – der inversen Zeit-bis-Kontakt.

![[optical-flow-expansion.pdf]]
*Expansionsfluss bei Vorwärtsbewegung: alle Vektoren strahlen vom rot markierten
Fokusexpansionspunkt aus, ihr Betrag wächst zur Peripherie. Aus diesem Muster lassen
sich Bewegungsrichtung und Zeit-bis-Kontakt ablesen.*

## Role in this class or project

Zentraler Bottom-up-Cue in [[VL08 Visuelle Wahrnehmung Bottom-Up]] und Brücke zur
Antizipation: Der Fluss verbindet **Wahrnehmung** (Bewegung/Tiefe sehen) mit
**Handlung** (Landen, Ausweichen, Eigenbewegung kompensieren). Er ist eines der besten
Beispiele für die Kursthese, dass Kognition aus sensomotorischer Interaktion emergiert
([[Körpergrundierte Kognition]]).

## Exam, assignment, or project relevance

Sehr hoch und **gerechnet** (Tutorium 7 / Übungsblatt 7): FoE aus $(T_x,T_y,T_z)$
bestimmen; Zeit-bis-Kontakt $t=Z/T_z$ berechnen; visual translation $v_x,v_y$ an einem
Punkt ausrechnen; erklären, warum Eigenbewegung herausgefiltert werden muss
(Reafferenz). Die Formeln stehen in der [[Formelsammlung (Tutorium)]].

## Related global concepts

[[Predictive Coding]] (selbstverursachter Fluss wird vorhergesagt und abgezogen),
[[Marr's Levels of Analysis]] (Fluss als algorithmische Tiefen-/Bewegungsschätzung).

## Related local pages

[[Bottom-Up Bildverarbeitung]], [[Ideomotorik und Antizipation]] (Reafferenzprinzip),
[[Emergenz und Attraktoren]] (Fluss als emergente Informationsquelle),
[[VL08 Visuelle Wahrnehmung Bottom-Up]].

## Common confusions

- **FoE-Vorzeichen.** Der Fokusexpansionspunkt liegt bei $-T_x/T_z$, nicht $+T_x/T_z$ –
  achte auf das Minus (Projektion steht auf dem Kopf bzw. relative Geometrie).
- **„Fluss = Objektbewegung“** ist falsch: Der größte Teil des Flusses stammt meist von
  der **Eigenbewegung**. Fremdbewegung ist erst das, was *nach* Filterung der
  Eigenbewegung übrig bleibt.
- **Statisch vs. dynamisch:** Kanten liefern Information ohne Bewegung; der optische
  Fluss ist die zusätzliche, *bewegungsabhängige* Quelle – beide ergänzen sich.

## Sources

VL08 (Folien zu optischem Fluss, Eigenbewegung, Reichardt-Detektor);
[[Formelsammlung (Tutorium)]] (Abschnitt optischer Fluss); Tutorium 7.
