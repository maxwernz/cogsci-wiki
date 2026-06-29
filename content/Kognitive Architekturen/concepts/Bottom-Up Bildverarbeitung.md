---
type: concept
status: active
scope: local
classes: [Kognitive Architekturen]
projects:
domains: [visual perception, image processing, computer vision]
sources: ["VL08 Visuelle Wahrnehmung Bottom-Up"]
created: 2026-06-17
updated: 2026-06-17
---

# Bottom-Up Bildverarbeitung

## Short definition

Die rein **datengetriebene** frühe Verarbeitung eines Bildes: Aus den rohen
Pixelintensitäten werden – ohne Vorwissen über die Szene – nützliche, redundante
Teilsignale gewonnen (Glättung, Kanten, Tiefe/3D, Bewegung, Farbe).

## Intuition

Stell dir vor, du bekommst ein verrauschtes Foto und sollst es „verstehen“, darfst aber
nichts über die Welt annehmen. Sinnvolle erste Schritte: erst das **Rauschen
wegmitteln** (verwackeltes glätten), dann nach **Sprüngen in der Helligkeit** suchen
(das sind Kanten – Objekt­ränder, Schatten, Texturgrenzen), dann aus Kanten, Bewegung
und Schattierung auf **Tiefe** schließen. Genau diese Pipeline läuft in Auge und V1 ab,
bevor irgendeine „Bedeutung“ ins Spiel kommt. Das Bild wird dabei bewusst **in viele
redundante Signale zerlegt** – Redundanz macht die Wahrnehmung robust.

## Explanation

Die Bottom-up-Verarbeitung hat zwei Phasen:

**1. Rauschen reduzieren – Glättung.** Jeder Pixel wird durch ein **gewichtetes Mittel
seiner Nachbarn** ersetzt. Die beste Gewichtung ist die Gauß-Verteilung (nahe Pixel
zählen mehr als ferne). Mathematisch ist das eine **Faltung (Konvolution)** des Bildes
$I$ mit einem Gauß-Kern $G_\sigma$. $\sigma$ steuert die Filterbreite: groß = stark
verschwommen, klein = kaum geglättet. Im Gehirn realisieren laterale, rekurrente
Verknüpfungen über die retinotopische Karte denselben Effekt.

**2. Selektiv ableiten – Information extrahieren.** Aus dem geglätteten Bild werden
mehrere redundante Signale gezogen: **Kanten**, **Distanz/Tiefe (3D)**, **optischer
Fluss** ([[Optischer Fluss]]), **Farbe**, **Bewegung**.

*Kantendetektion.* Eine Kante ist ein Ort starker Helligkeitsänderung. Man detektiert
sie, wo der Betrag der räumlichen Ableitung eine Schwelle übersteigt. Da das Ableiten
Rauschen verstärkt, glättet man zuerst – und nutzt die Identität $(f*g)'=f*g'$, um
direkt mit der **Ableitung des Gauß** $G'_\sigma$ zu falten. **Canny** kombiniert
horizontale und vertikale Ableitungen zu Stärke und Orientierung; **Sobel** ist ein
einfacher lokaler Kontrastdetektor; **Gabor**-Filter sind der neuronalen V1-Aktivität am
ähnlichsten. Benachbarte Kanten gleicher Orientierung werden zu längeren Konturen
integriert, die dann die **Bildsegmentierung** erlauben.

*Kantentypen und ihre Bedeutung.* Kanten sind so wertvoll, weil verschiedene
physikalische Ursachen sie erzeugen: (1) **Tiefendiskontinuität** (Objektrand), (2)
**Oberflächenorientierungs-Diskontinuität** (Knick), (3) **Beleuchtungsdiskontinuität**
(Schatten), (4) **Reflektions-/Farbdiskontinuität**. Man unterscheidet konvexe (+) und
konkave (−) Kanten sowie verdeckende Kanten (Pfeile zeigen, welche Oberfläche vorne
liegt).

*Das Kantenzuordnungsproblem (Waltz 1975).* Gegeben eine Kantenverteilung im Bild: finde
eine **global konsistente** Typzuordnung aller Kanten/Kreuzungen, also eine sinnvolle
Szeneninterpretation. Das ist eines der ersten **Constraint-Satisfaction-Probleme** der
KI (Variablen = Kreuzungen, Werte = Kreuzungstypen, Constraint = jede Kante hat genau
einen Typ) und **NP-vollständig**. Erstaunlich, dass das Gehirn es scheinbar mühelos
löst – ein Hinweis auf massive Parallelität und Top-down-Hilfe.

*Weitere Tiefen-Cues.* Binokulares Stereosehen (Disparität), **Textur** (Texel
schrumpfen mit der Distanz), **Schattierung** (Reflektion verrät Oberflächenneigung),
Bewegung/optischer Fluss. Natürliche Szenen liefern mehrere dieser Cues gleichzeitig und
meist konsistent → redundante, robuste 3D-Information.

Diese Bottom-up-Signale reichen allein **nicht** für Objekterkennung aus; sie werden mit
**Top-down-Hypothesen** kombiniert (bidirektional). Der technische Rahmen dafür sind
Bayessche generative Modelle → [[Generative und diskriminative Modelle]],
[[VL09 Visuelle Wahrnehmung Top-Down]].

## Worked example

**Glättung + Kante an einem 1D-Helligkeitsprofil.** Ein verrauschtes Signal springt bei
$x=5$ von dunkel (0.2) auf hell (0.85). Direktes Ableiten würde überall kleine
Rausch-„Kanten“ erzeugen. Stattdessen: zuerst mit $G_\sigma$ falten (Rauschen mittelt
sich weg), dann ableiten. Der Ableitungsbetrag hat **ein klares Maximum bei $x=5$**, das
über der Schwelle $q$ liegt – dort und nur dort wird eine Kante gemeldet.

![[gauss-smoothing-edge.pdf]]
*Oben: verrauschtes vs. geglättetes Signal. Mitte: der Gauß-Glättungskern. Unten: der
Betrag der Ableitung mit Schwelle $q$ – die Kante ist das Maximum bei $x=5$.*

## Formal definition / equations

Faltung (Glättung):
$$ (I*G_\sigma)(x,y)=\sum_i\sum_j I(x-i,y-j)\,G_\sigma(i,j),\quad
G_\sigma(i,j)=\tfrac{1}{2\pi\sigma^2}e^{-\frac{i^2+j^2}{2\sigma^2}}. $$
Kantenstärke aus dem geglätteten Bild über die Gauß-Ableitung:
$$ H'(x,y)=I*G'_\sigma,\qquad H=\sqrt{H_H^2+H_V^2},\quad
\theta=\arctan\!\big(H_H/H_V\big), $$
mit $H_H=I*G'_\sigma(x)G_\sigma(y)$ (horizontal) und $H_V=I*G_\sigma(x)G'_\sigma(y)$
(vertikal). Eine Kante liegt vor, wo $H>q$. Symbole: $I$ = Bildintensität, $\sigma$ =
Filterbreite, $q$ = Schwelle, $\theta$ = Kantenorientierung.

## Role in this class or project

Liefert das **Wie** der frühen Wahrnehmung ([[Marr's Levels of Analysis]],
algorithmische Ebene) in [[VL08 Visuelle Wahrnehmung Bottom-Up]] und ist die
datengetriebene Hälfte, die in [[VL09 Visuelle Wahrnehmung Top-Down]] mit generativen
Modellen vervollständigt wird.

## Exam, assignment, or project relevance

Glättung als Faltung erklären; begründen, warum man **vor** der Kantendetektion glättet
und wieso $(f*g)'=f*g'$ den Rechenweg vereinfacht; Canny/Sobel/Gabor einordnen; die vier
Kantentypen nennen; das Waltz-Kantenzuordnungsproblem als NP-vollständiges CSP erklären;
Tiefen-Cues aufzählen. Übungsblatt 7 verbindet dies mit [[Optischer Fluss]].

## Related global concepts

[[Marr's Levels of Analysis]] (Bottom-up als algorithmische Theorie),
[[Bayesian Inference]] (Integration der Cues top-down).

## Related local pages

[[Optischer Fluss]], [[VL08 Visuelle Wahrnehmung Bottom-Up]],
[[Generative und diskriminative Modelle]], [[Stevens (2012) The Vision of David Marr]]
(Kanten als „konstruiert, nicht detektiert“), [[Emergenz und Attraktoren]]
(morphologische Berechnung in der Retina).

## Common confusions

- **Reihenfolge:** Erst **glätten**, dann ableiten – nicht umgekehrt, sonst dominiert
  Rauschen.
- **Kante ≠ Objektrand.** Eine detektierte Kante kann auch ein Schatten oder eine
  Farbgrenze sein; welcher Typ vorliegt, klärt erst das (Waltz-)Kantenzuordnungsproblem.
- **Bottom-up ≠ alles.** Reine Bottom-up-Segmentierung erkennt keine Objekte; dafür
  braucht es Top-down-Hypothesen (VL09).

## Sources

VL08 (Folien zu Glättung/Konvolution, Kantendetektion, Kantentypen, Waltz, Tiefen-Cues).
