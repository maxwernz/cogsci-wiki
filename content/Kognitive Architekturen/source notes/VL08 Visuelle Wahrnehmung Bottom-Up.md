---
type: source_note
status: processed
scope: local
class: Kognitive Architekturen
project:
source_type: lecture_slides
raw_path: "raw/VL Folien/KogArch_08_VisuelleWahrnehmungBottomUp.pdf"
created: 2026-06-17
updated: 2026-06-17
---

# VL08 – Visuelle Wahrnehmung: Bottom-Up

## Summary

Diese Vorlesung erklärt, **wie aus Licht ein nützliches Bild und aus dem Bild
verwertbare Information wird** – ausschließlich „von unten nach oben“ (bottom-up),
also datengetrieben, ohne Vorwissen über die Szene. Sie hat drei Teile. Erstens
**Grundlagen der Bilderzeugung**: Lochkamera, perspektivische Projektion, Licht und
Reflektion, und der anatomische Weg vom Auge (Linse, Retina mit Stäbchen/Zäpfchen)
über LGN/Colliculus bis in den visuellen Cortex (V1, V2–V4, IT, MT/V5) mit dem
dorsalen („wo/wie“) und ventralen („was“) Strom. Zweitens **Bottom-up-Mechanismen**:
Bildglättung durch Faltung mit einem Gauß-Kern, Kantendetektion (Ableitung des
geglätteten Bilds, Canny/Sobel/Gabor), Kantentypen und das Kantenzuordnungsproblem
(Waltz 1975), sowie der **optische Fluss** als Bewegungs- und Tiefenquelle. Drittens
**optische Täuschungen** als Beleg dafür, dass diese Bottom-up-Verarbeitung von starken
**Top-down-Einflüssen** überschrieben wird (Helligkeitsnormalisierung, Gestaltschluss,
mehrdeutige Tiefe/Bewegung) – die Brücke zu [[VL09 Visuelle Wahrnehmung Top-Down]].

Kerngedanke: Das visuelle Signal wird absichtlich **in viele redundante Teilsignale
zerlegt** (Kanten, Tiefe, Fluss, Farbe, Bewegung). Diese Redundanz macht Wahrnehmung
robust – und ist genau der Stoff, aus dem Illusionen gemacht sind.

## Key points

- **Auge ≈ Kamera.** Lochkamera-Modell: ein Szenenpunkt $(X,Y,Z)$ projiziert auf einen
  Bildpunkt $(x,y)$; bei $Z \gg Z_0$ gilt die einfache skalierte orthographische
  Näherung $x=-sX,\;y=-sY$ mit $s=b/Z$. Die Linse bündelt mehr Licht (Preis:
  Schärfentiefe), ändert aber an dieser Rechnung grundsätzlich nichts.
- **Retina rechnet schon.** Stäbchen (Helligkeit, sehr lichtempfindlich) vs. Zäpfchen
  (Farbe, drei Typen ~ 650/530/430 nm → Drei-Farben-Theorie, Young 1801). Nach außen
  mehr Stäbchen, weniger Zäpfchen → **morphologische Berechnung**. Blinder Fleck am
  Sehnervaustritt.
- **Visueller Pfad.** Sehnervkreuzung (optic chiasm) teilt linkes/rechtes Gesichtsfeld;
  alter Pfad → Colliculus superior (schnelle Orientierungssakkaden), neuer Pfad → LGN
  (Vorverarbeitung/Normalisierung) → V1 (retinotopisch, raum-zeitliche Filter ~ lokale
  Fourier-Analyse: Kanten, Orientierung, Bewegung, Tiefe). V2–V4 (komplexere Formen,
  Aufmerksamkeit), IT (Objekt-/Gesichtserkennung), MT/V5 (Bewegung). **Dorsaler** Strom
  = wo/wie, **ventraler** Strom = was (alle Verbindungen eigentlich bidirektional).
- **Bottom-up-Pipeline:** (1) Rauschen reduzieren → Glättung, (2) selektiv ableiten →
  Kanten, Tiefe/3D, optischer Fluss, Farbe, Bewegung. Siehe
  [[Bottom-Up Bildverarbeitung]].
- **Optischer Fluss** charakterisiert Bildveränderung über die Zeit; bei Eigenbewegung
  entsteht ein Expansionsfluss um den **Fokusexpansionspunkt**. Filterung der
  Eigenbewegung nötig, um Fremdbewegung zu sehen → **Reafferenzprinzip**
  ([[Ideomotorik und Antizipation]]). Siehe [[Optischer Fluss]].
- **Optische Täuschungen** zeigen die Grenzen rein lokaler Cues und die Macht der
  Top-down-Interpretation (Helligkeitskonstanz, Gestalt-Vervollständigung, bistabile
  Würfel/Bewegung, Größenkontraste wie Ponzo/Ebbinghaus, Point-Light-Displays).

## Important concepts

[[Bottom-Up Bildverarbeitung]] (Faltung/Glättung, Kantendetektion, Kantentypen,
Waltz-Kantenzuordnung, Tiefen-Cues) und [[Optischer Fluss]] (mit voller Tiefe). Bezug
zu [[Emergenz und Attraktoren]] (morphologische Berechnung in der Retina) und
[[Ideomotorik und Antizipation]] (Eigenbewegungs-Filterung). Der Begriff
**retinotopisch** (benachbarte Bildpunkte → benachbarte Cortexzellen) trägt die ganze
frühe Verarbeitung.

## Methods, models, or theories

- **Lochkamera / perspektivische Projektion** und ihre orthographische Näherung.
- **Faltung (Konvolution) mit Gauß-Kern** zur Glättung; Ableitung-des-Gauß als
  Kantendetektor (mit der Identität $(f*g)' = f*g'$).
- **Kantendetektoren:** Canny (horizontal/vertikal über $G'_\sigma$, Orientierung via
  $\arctan(H_H/H_V)$), Sobel (lokaler Kontrast), Gabor (am nächsten an V1).
- **Waltz (1975) Kantenzuordnung** als Constraint-Satisfaction-Problem (NP-vollständig):
  finde eine global konsistente Typzuordnung aller Kanten/Kreuzungen → plausible
  Szeneninterpretation.
- **Optischer-Fluss-Modell** und **Reichardt-Detektor** (einfache neuronale
  Bewegungsdetektion über zeitversetzte, laterale Verknüpfungen).
- Ziel: **bidirektionale Objekterkennung** (Bottom-up-Features + Top-down-Hypothesen),
  technischer Rahmen = Bayessche generative Modelle → [[VL09 Visuelle Wahrnehmung Top-Down]].

## Equations or formal definitions

**Perspektivische Projektion (Lochkamera).** Ein Szenenpunkt in Distanz $Z$ bildet sich
mit $x=-b\,X/Z$, $y=-b\,Y/Z$ ab. $b$ = Abstand Loch→Bildfläche, das Minus = Bild steht
auf dem Kopf. Bei $Z \gg Z_0$ (Tiefenunterschiede klein gegen die Distanz) wird der
Skalierungsfaktor $s=b/Z$ über das Objekt fast konstant → **skalierte orthographische
Projektion** $x=-sX,\;y=-sY$.

**Bildglättung durch Faltung.** Der geglättete Bildwert an $(x,y)$ ist die mit einer
Gauß-Funktion gewichtete Summe der Nachbarpixel:
$$ (I * G_\sigma)(x,y) = \sum_{i}\sum_{j} I(x-i,\,y-j)\,G_\sigma(i,j), \qquad
G_\sigma(i,j)=\tfrac{1}{2\pi\sigma^2}\,e^{-\frac{i^2+j^2}{2\sigma^2}} $$
$I$ = Bildintensität, $G_\sigma$ = Gauß-Kern, $\sigma$ = Filterbreite (in der Praxis
reicht $-3\sigma$ bis $+3\sigma$). Intuitiv: jeder Pixel wird durch ein gewichtetes
Mittel seiner Umgebung ersetzt → Rauschen mittelt sich weg. Im Gehirn übernehmen das
laterale, rekurrente Verknüpfungen über die retinotopische Karte.

**Kantendetektion.** Eine Kante ist ein Ort starker Helligkeitsänderung, also ein
großer Betrag der räumlichen Ableitung: detektiere, wo $\lVert I'(x,y)\rVert > q$ für
eine Schwelle $q$. Da Rauschen falsche Kanten erzeugt, glättet man zuerst und nutzt die
Identität $(f*g)' = f*g'$, sodass man direkt mit der **Ableitung des Gauß**,
$G'_\sigma$, faltet: $H'(x,y) = I * G'_\sigma$. Canny in 2D kombiniert horizontale
($H_H = I * G'_\sigma(x)G_\sigma(y)$) und vertikale ($H_V = I * G_\sigma(x)G'_\sigma(y)$)
Antworten zu $H=\sqrt{H_H^2+H_V^2}$ mit Orientierung $\arctan(H_H/H_V)$.

![[gauss-smoothing-edge.pdf]]
*Erst glätten, dann ableiten: das verrauschte Helligkeitssignal wird mit einem
Gauß-Kern geglättet; die Kante erscheint als Maximum des Ableitungsbetrags über der
Schwelle $q$. So vermeidet man die Falschkanten, die eine direkte Ableitung des
Rauschens erzeugt.*

**Optischer Fluss bei Eigenbewegung.** Bei reiner Translation $(T_x,T_y,T_z)$ ohne
Drehung verschwindet der Fluss am **Fokusexpansionspunkt** $(-T_x/T_z,\,-T_y/T_z)$; um
diesen Punkt strömt das Bild radial nach außen. Die Zeit bis zum Erreichen einer Fläche
ist $Z/T_z$ – exakt das, was Fliegen für die Landung und Tauben über Kopf-Vor/Zurück
nutzen. Voll entwickelt in [[Optischer Fluss]].

![[optical-flow-expansion.pdf]]
*Expansionsfluss bei Vorwärtsbewegung: alle Flussvektoren strahlen vom (rot
markierten) Fokusexpansionspunkt aus; ihr Betrag wächst zur Bildperipherie. Genau diese
Geometrie kodiert Eigenbewegung und Zeit-bis-Kontakt.*

## Local relevance

VL08 ist Teil 8/9 der Komponenten-Landkarte des Kurses („Interaktive sensorische
Verarbeitung“). Sie liefert das **Wie** der Wahrnehmung auf der algorithmischen Ebene
([[Marr's Levels of Analysis]]) und bereitet den Boden für Multimodalität (VL10–11) und
Aufmerksamkeit (VL12). Das zugehörige Diskussionspaper ist
[[Stevens (2012) The Vision of David Marr]] (genau Marrs Bottom-up-/Pipeline-Sicht und
ihre Grenzen). Die Tutoriums-Rechnungen zum optischen Fluss stehen in
[[Tutorien – Übersicht und Diskussionsfragen]] (Tutorium 7, Übungsblatt 7).

## Exam or project relevance

Hoch und teils **praktisch gerechnet** (Übungsblatt 7/Tutorium 7): Lochkamera-Projektion;
Gauß-Glättung und Kantendetektion verstehen und begründen ($(f*g)'=f*g'$); optischer
Fluss, Fokusexpansionspunkt und Zeit-bis-Kontakt **berechnen**; Kantentypen und das
Waltz-Kantenzuordnungsproblem (warum NP-vollständig, wie löst das Gehirn es trotzdem);
dorsaler vs. ventraler Strom; und vor allem: **erklären, warum optische Täuschungen
entstehen** (lokale Cues + Top-down-Interpretation). Begriffe definieren können:
retinotopisch, morphologische Berechnung, Drei-Farben-Theorie.

## Links to global concepts

[[Marr's Levels of Analysis]] (Bottom-up als algorithmische Ebene),
[[Bayes' Theorem]] / [[Bayesian Inference]] (technischer Rahmen für die
Objekterkennung, ausgeführt in VL09), [[Predictive Coding]] (Top-down-Erwartung filtert
die Wahrnehmung).

## Open questions

- Konkrete Reichardt-Detektor-Mechanik (Zeitkonstanten) bleibt in den Folien skizzenhaft.
- Wie genau laterale + Top-down-Verknüpfungen die globale Bewegungs-/Gestaltintegration
  in V1 realisieren, wird erst mit dem hierarchischen Bayes-Modell (VL Aufmerksamkeit,
  Chikkerur et al. 2010) präzise – siehe [[VL09 Visuelle Wahrnehmung Top-Down]].
