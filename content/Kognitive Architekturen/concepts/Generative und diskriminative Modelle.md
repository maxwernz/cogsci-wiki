---
type: concept
status: active
scope: local
classes: [Kognitive Architekturen]
projects:
domains: [machine learning, probabilistic modeling, perception]
sources: ["VL09 Visuelle Wahrnehmung Top-Down"]
created: 2026-06-17
updated: 2026-06-17
---

# Generative und diskriminative Modelle

## Short definition

Zwei Grundstrategien, um aus Daten auf eine Klasse/Ursache zu schließen: ein
**diskriminatives** Modell lernt direkt die Grenze $p(c\mid o)$ (welche Klasse bei diesen
Daten?); ein **generatives** Modell lernt, wie Daten entstehen ($p(o\mid c)$ und $p(c)$),
und dreht die Frage per Bayes-Regel um.

## Intuition

Stell dir zwei Arten von Tierkennern vor. Der **diskriminative** Kenner hat tausende
Fotos gesehen und nur gelernt, *die Grenze* zu ziehen: „Streifen + Hufe → Zebra“. Er
sagt schnell, was auf einem Bild ist, kann aber kein Zebra *beschreiben oder malen*. Der
**generative** Kenner hat ein **inneres Modell** „wie ein Zebra aussieht“; er kann sich
ein Zebra **vorstellen** und vorhersagen, welche Pixel zu erwarten sind – und schließt
umgekehrt: „Diese Daten passen am besten zu meinem Zebra-Modell.“ Top-down-Wahrnehmung
ist generativ: Das Gehirn *erwartet* etwas und prüft, ob die Daten passen.

## Explanation

Gegeben eine Menge möglicher Beobachtungen $O$ und eine Menge von Klassen/Zuständen $C$:

- **Diskriminatives Modell:** $C$ enthält alle Klassen; Ziel ist die Schätzung von
  $p(c\mid o)$ direkt aus Trainingsdaten. Typisch: ein **vorwärtsgerichtetes tiefes
  neuronales Netz**. Es ist datengetrieben / bottom-up und oft sehr genau im
  Klassifizieren, hat aber **kein Modell der Welt**: Es kann keine Daten erzeugen, keine
  fehlenden Teile ergänzen, keine Erwartung formulieren.

- **Generatives Modell:** $C$ definiert die Zustände eines **internen Modells**; man
  schätzt die gemeinsame Verteilung $p(o,c)=p(o\mid c)\,p(c)$ aus klassenbedingten
  Wahrnehmungsverteilungen $p(o\mid c)$ und Priors $p(c)$. Zum Klassifizieren invertiert
  man per **Bayes-Regel** zu $p(c\mid o)$. Weil das Modell beschreibt, *wie* Daten
  entstehen, kann es **Beispiele erzeugen**, Wahrnehmung **vorhersagen/filtern/
  fokussieren**, Objekte bei **Okklusion vervollständigen** und Lokationen im nächsten
  Zeitschritt **prädizieren**. Genau diese Fähigkeiten braucht Top-down-Wahrnehmung – und
  sie sind die Grundlage vieler optischer „Täuschungen“.

Warum überhaupt generativ/probabilistisch? Weil die Welt **nicht vollständig
beobachtbar** ist: Ignoranz (unbekannte Abhängigkeiten), schiere Komplexität,
physikalischer Zufall (Quanten, Chaos) und Wahrnehmungsungenauigkeit (begrenzte Sicht,
Sensorrauschen). Wahrscheinlichkeitstheorie und die Bayes-Regel sind das fundierte
Werkzeug, um unter dieser Unsicherheit zu schließen.

Ein generatives Modell braucht **interne Zustände**, die (invertiert) zu antizipierten
Wahrnehmungen kodiert werden können – etwa ein generatives Ampelmodell, das aus den
versteckten Zuständen STOP/GO/… die erwartete Farbe (rot/gelb/grün) und die
Zustandsübergänge erzeugt. Die konkrete Maschinerie generativer Modelle sind
**[[Bayes-Netzwerke]]** (diskret) und **[[Gaußsche Mischmodelle]]** (kontinuierlich).

## Worked example

**Zebraerkennung mit einem Streifendetektor.** Prior: $p(\text{Zebra})=0.02$. Der
binäre Streifendetektor liefert $p(o\!=\!\text{wahr}\mid \text{Zebra})=0.8$ und
$p(o\!=\!\text{wahr}\mid \neg\text{Zebra})=0.1$ (auch anderes hat Streifen). Bei
positiver Detektion:
$$ p(\text{Zebra}\mid o)=\frac{0.8\cdot 0.02}{0.8\cdot 0.02 + 0.1\cdot 0.98}
=\frac{0.016}{0.016+0.098}\approx 0.14. $$
Der Glaube steigt von 2 % auf ~14 % – eine deutliche Verbesserung, aber wegen der vielen
Falsch-Positiven (geringer Prior!) noch keine Gewissheit. Das ist generatives Schließen:
$p(o\mid c)$ und $p(c)$ getrennt modelliert, dann per Bayes zu $p(c\mid o)$ kombiniert.
Ein diskriminatives Netz hätte direkt $p(c\mid o)$ gelernt, ohne den Detektor und den
Prior je zu trennen.

## Formal definition / equations

$$ \text{diskriminativ: } p(c\mid o)\ \text{direkt}; \qquad
\text{generativ: } p(o,c)=p(o\mid c)\,p(c),\ \
p(c\mid o)=\frac{p(o\mid c)\,p(c)}{\sum_k p(o\mid c_k)\,p(c_k)}. $$
Die **MAP-Klasse** $c_{\max}=\arg\max_c p(c\mid o)=\arg\max_c p(o\mid c)\,p(c)$ (der
Nenner ist für alle $c$ gleich). Symbole: $o$ = Beobachtung, $c$ = Klasse/Zustand,
$p(c)$ = Prior, $p(o\mid c)$ = Likelihood, $p(c\mid o)$ = Posterior.

## Role in this class or project

Begrifflicher Rahmen von [[VL09 Visuelle Wahrnehmung Top-Down]]: Er ordnet die
datengetriebene Bottom-up-Verarbeitung ([[Bottom-Up Bildverarbeitung]]) als
*diskriminativ* ein und stellt ihr das *generative* Top-down-Modell gegenüber, das beide
in einem interaktiven Bayes-System vereint. Verbindet sich mit
[[Ideomotorik und Antizipation]] (antizipierte Wahrnehmung) und
[[Kernwissen und Zwei-Systeme-Modell]] (intuitive Physik als generatives Modell).

## Exam, assignment, or project relevance

Den Unterschied präzise erklären (Richtung der Modellierung, was jedes Modell *kann*);
warum Top-down-Wahrnehmung generativ ist; das Zebra-Beispiel rechnen; benennen, dass ein
diskriminatives DNN $p(c\mid o)$ lernt, ein generatives Modell $p(o\mid c)$ und $p(c)$.

## Related global concepts

[[Generative and Discriminative Models]] (allgemeine Seite), [[Bayes' Theorem]],
[[Bayesian Inference]] (Kernmechanik), [[Predictive Coding]]
(generative Vorhersage), [[Maximum Likelihood Estimation]] (Schätzung von $p(o\mid c)$).

## Related local pages

[[Bayes-Netzwerke]], [[Gaußsche Mischmodelle]], [[VL09 Visuelle Wahrnehmung Top-Down]],
[[Bottom-Up Bildverarbeitung]].

## Common confusions

- **Generativ ≠ besser.** Diskriminative Modelle klassifizieren oft genauer; generative
  Modelle *können mehr* (erzeugen, vervollständigen, vorhersagen).
- **„Generativ heißt erfinden.“** Nein – es heißt $p(o\mid c)$ zu modellieren (wie Daten
  aus Ursachen entstehen) und per Bayes zurückzurechnen.
- **Prior nicht vergessen.** Eine hohe Likelihood allein genügt nicht; ein kleiner Prior
  (seltene Klasse) drückt den Posterior stark (siehe Zebra: 14 %, nicht 80 %).

## Sources

VL09 (Folien: Kontrast vorwärts/rückwärts, Bayes-Sichtweise diskriminativ vs. generativ,
Ampel- und Zebra-Beispiel).
