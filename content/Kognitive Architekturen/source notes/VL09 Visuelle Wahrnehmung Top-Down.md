---
type: source_note
status: processed
scope: local
class: Kognitive Architekturen
project:
source_type: lecture_slides
raw_path: "raw/VL Folien/KogArch_09_VisuelleWahrnehmungTopDown.pdf"
created: 2026-06-17
updated: 2026-06-17
---

# VL09 – Visuelle Wahrnehmung: Top-Down

## Summary

VL08 hat das Bild **datengetrieben zerlegt**; VL09 dreht die Richtung um: Wahrnehmung
wird durch ein **internes, generatives Modell** der Welt geleitet, das vorhersagt,
welche Sinnesdaten zu erwarten sind, und die mehrdeutigen Bottom-up-Signale damit
deutet. Die Vorlesung liefert das **mathematische Werkzeug** dafür in drei Schichten.
Erstens der Gegensatz **generativ vs. diskriminativ**: ein diskriminatives Modell lernt
direkt $p(c\mid o)$ (welche Klasse bei diesen Daten?), ein generatives Modell lernt
$p(o\mid c)$ und $p(c)$ (welche Daten erzeugt diese Ursache?) und invertiert per
**Bayes-Regel**. Zweitens **Bayes-Netzwerke**: gerichtete azyklische Graphen, die eine
gemeinsame Verteilung kompakt faktorisieren, mit d-Separation für bedingte
(Un-)Abhängigkeit und vier Deduktionsarten (prädiktiv, diagnostisch, kombiniert,
interkausal). Drittens der **kontinuierliche Fall**: die (multivariate) Gauß-Verteilung
mit ihrer Kovarianzmatrix und **Gaußsche Mischmodelle**, mit denen man beliebige
Verteilungen – und damit Bilder – approximieren kann. Am Ende steht die Vision eines
**neuronalen, hierarchischen, modularen Bayes-Modells**, das Bottom-up und Top-down
vereint (Chikkerur et al. 2010; ausgeführt in der VL Aufmerksamkeit).

Kerngedanke: Die Welt ist **nicht vollständig beobachtbar** (Ignoranz, Komplexität,
physikalischer Zufall, Sensorrauschen). Wahrscheinlichkeitstheorie – speziell die
Bayes-Regel – ist das fundierte Werkzeug, um unter dieser Unsicherheit zu schließen,
und damit die formale Grundlage für Top-down-Einflüsse und viele optische „Täuschungen“.

## Key points

- **Vorwärts vs. rückwärts.** Diskriminativ (bottom-up): gegeben Daten, finde Klasse,
  $p(c\mid o)$ – z. B. ein vorwärtsgerichtetes tiefes neuronales Netz. Generativ
  (top-down): gegeben Modell, erzeuge/erwarte Daten, schätze $p(o,c)=p(o\mid c)\,p(c)$
  und klassifiziere über Bayes. Siehe [[Generative und diskriminative Modelle]].
- **Bayes-Regel** $p(c\mid o)=\dfrac{p(o\mid c)\,p(c)}{p(o)} \propto p(o\mid c)\,p(c)$.
  Der Nenner $p(o)$ ist für alle Klassen gleich → für die Klassenwahl (MAP) weglassbar.
- **Zebra-Beispiel:** mit Prior $p(\text{Zebra})=0.02$ und einem Streifendetektor
  ($p(o\mid \text{Zebra})=0.8$, $p(o\mid \neg\text{Zebra})=0.1$) hebt eine positive
  Detektion den Glauben auf $\approx 0.14$ – eine deutliche Verbesserung gegenüber 0.02,
  aber wegen vieler Falsch-Positiver noch lange keine Sicherheit.
- **Bayes-Netzwerke** sind gerichtete azyklische Graphen; Knoten = Variablen, Kanten =
  bedingte Abhängigkeiten. Die gemeinsame Verteilung faktorisiert als
  $p(x_1,\dots,x_n)=\prod_i p(x_i\mid \text{parents}(x_i))$. **d-Separation** liest
  bedingte (Un-)Abhängigkeit aus der Graphstruktur ab; **Collider** (head-to-head)
  verhalten sich gegenläufig. Siehe [[Bayes-Netzwerke]].
- **Vier Deduktionsarten:** prädiktiv (Wurzel→Blatt), diagnostisch (Blatt→Wurzel, via
  Bayes), kombiniert, interkausal („explaining away“).
- **Kontinuierlich:** die **Gauß-Verteilung** ist die Standardverteilung; die
  **Kovarianzmatrix** $\Sigma$ streckt und rotiert sie. **Gaußsche Mischmodelle** =
  gewichtete Summe von Gauß-Komponenten ($\sum_m \pi_m \mathcal{N}_m$) approximieren
  beliebig komplexe Dichten. Siehe [[Gaußsche Mischmodelle]].
- **Synthese:** Ein interaktives Modell kombiniert Bottom-up- und Top-down-Inferenz mit
  Bayes-Prinzipien (diskret + kontinuierlich gemischt).

## Important concepts

[[Generative und diskriminative Modelle]], [[Bayes-Netzwerke]] und
[[Gaußsche Mischmodelle]] (alle drei mit voller Tiefe). Diese Seite ist die formale
Heimat für [[Optischer Fluss|Tiefen-/Bewegungs-Cues]] aus VL08, die top-down zu
Objekt- und Szenenhypothesen integriert werden.

## Methods, models, or theories

- **Bayessche Klassifikation** über ein generatives Modell (MAP/Likelihood).
- **Bayes-Netzwerke** mit bedingten Wahrscheinlichkeitstabellen (diskret), bedingten
  Wahrscheinlichkeitsfunktionen (diskretes Kind, kontinuierliche Eltern) und
  Wahrscheinlichkeitsdichteverteilungen (kontinuierliches Kind); **d-Separation**.
- **(Multivariate) Gauß-Verteilung** und **Gaussian Mixture Models** zur Repräsentation
  kontinuierlicher und gemischter (diskret-kontinuierlicher) Verteilungen, z. B.
  Pixelklassifikation (Wand/Busch/Schild/Straße aus Graustufen).
- **Hierarchisches, modulares neuronales Bayes-Modell** (Chikkerur, Serre, Tan, Poggio
  2010: „What and where“) als Bottom-up-/Top-down-Synthese – Details in der VL
  Aufmerksamkeit.

## Equations or formal definitions

**Grundregeln.** Gemeinsame Wahrscheinlichkeit $p(x,y)=p(x\mid y)\,p(y)$; bei
Unabhängigkeit $p(x,y)=p(x)\,p(y)$. Marginalisierung
$p(x)=\sum_y p(x\mid y)\,p(y)$ (bzw. $\int$ im Kontinuierlichen) „summiert eine Variable
heraus“. Daraus die **Bayes-Regel**:
$$ p(c\mid o)=\frac{p(o\mid c)\,p(c)}{p(o)}=\frac{p(o\mid c)\,p(c)}{\sum_k p(o\mid c_k)\,p(c_k)} \;\propto\; p(o\mid c)\,p(c). $$
$p(c)$ = Prior (Vorannahme über die Ursache), $p(o\mid c)$ = Likelihood (wie gut die
Ursache die Daten erklärt), $p(c\mid o)$ = Posterior (revidierter Glaube nach den
Daten), $p(o)$ = Evidenz (Normierung).

**Faktorisierung im Bayes-Netz.**
$p(x_1,\dots,x_n)=\prod_{i=1}^{n} p\big(x_i\mid \text{parents}(x_i)\big)$ – statt einer
exponentiell großen Verbundtabelle nur ein kleiner Faktor pro Knoten. Voll erklärt in
[[Bayes-Netzwerke]].

**Multivariate Gauß-Verteilung.**
$$ \mathcal{N}(x;\mu,\Sigma)=\frac{1}{(2\pi)^{n/2}\,|\Sigma|^{1/2}}\,
\exp\!\Big(-\tfrac12 (x-\mu)^{\top}\Sigma^{-1}(x-\mu)\Big) $$
$n$ = Dimensionen, $x,\mu$ = Vektoren, $\Sigma$ = Kovarianzmatrix (Diagonale = Varianzen,
Nebendiagonale = Kovarianzen/Abhängigkeit), $|\Sigma|$ = Determinante, $\top$ =
Transponiert, $-1$ = Inverse. Eine **Mischverteilung** ist
$p(x)=\sum_{m=1}^{M}\pi_m\,\mathcal{N}(x;\mu_m,\Sigma_m)$ mit Mischgewichten
$\pi_m\ge 0,\ \sum_m \pi_m=1$. Voll erklärt mit Worked Example in
[[Gaußsche Mischmodelle]].

![[covariance-effect.pdf]]
*Wirkung der Kovarianzmatrix auf eine 2D-Gauß-Verteilung: $\Sigma=I$ ergibt einen
Kreis, eine Diagonalmatrix streckt achsenparallel, Nebendiagonalterme korrelieren die
Dimensionen und rotieren die Verteilung.*

![[gmm-mixture.pdf]]
*Eine Gaußsche Mischverteilung ist die gewichtete Summe einzelner Gauß-Komponenten
(gestrichelt); so lassen sich beliebig komplexe, mehrgipflige Dichten – und damit auch
Bildstatistiken – approximieren.*

## Local relevance

VL09 ist die formale Klammer um den ganzen Wahrnehmungsteil: Sie zeigt, **wie** die
redundanten Bottom-up-Cues aus [[VL08 Visuelle Wahrnehmung Bottom-Up]] top-down zu
Hypothesen über Objekte und Szenen integriert werden, und liefert das Bayes-Werkzeug,
das später für Multimodalität/Informationsfusion (VL10–11) und Aufmerksamkeit (VL12)
gebraucht wird. Sie schließt auch an [[Ideomotorik und Antizipation]] (antizipierte
Wahrnehmung, Prädiktion) und an [[Kernwissen und Zwei-Systeme-Modell]] (intuitive
Physik als generatives Modell) an. Tutoriums-Pendant: Bayessches Schließen in
[[Tutorien – Übersicht und Diskussionsfragen]] (Tutorium 8, Übungsblatt 8).

## Exam or project relevance

Sehr hoch und **rechnerisch** (Übungsblatt 8/Tutorium 8): Bayes-Regel auf ein konkretes
Netz anwenden (Alarm/Einbruch/Wind/Hund-Beispiel; Tassen-Netz); die vier Deduktionsarten
auseinanderhalten und je eine kleine Rechnung führen; **d-Separation**-Regeln (fork,
chain, collider) anwenden und begründen, wann zwei Knoten (un)abhängig sind;
generativ vs. diskriminativ erklären; die Kovarianzmatrix interpretieren (Streckung,
Rotation, Determinante) und Varianz/Kovarianz **berechnen** (auch Übungsblatt 10). Die
Formelsammlung deckt genau diese Formeln ab → [[Formelsammlung (Tutorium)]].

## Links to global concepts

[[Bayes' Theorem]] und [[Bayesian Inference]] (direkt: Prior/Likelihood/Posterior,
generative Inferenz), [[Predictive Coding]] (Top-down-Vorhersage filtert Wahrnehmung),
[[Marr's Levels of Analysis]] (Bayes als rechnerische Theorie der Wahrnehmung).

## Open questions

- Wie die bedingten Verteilungen / Mischmodelle tatsächlich **gelernt** werden
  (EM-Algorithmus o. Ä.) bleibt in den Folien implizit.
- Die konkrete neuronale Realisierung des hierarchischen Bayes-Modells (Chikkerur et al.
  2010) wird auf die VL Aufmerksamkeit verschoben.
