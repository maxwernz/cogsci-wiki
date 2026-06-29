---
type: concept
status: active
scope: local
classes: [Kognitive Architekturen]
projects:
domains: [probability, density estimation, perception]
sources: ["VL09 Visuelle Wahrnehmung Top-Down", "Formelsammlung (Tutorium)"]
created: 2026-06-17
updated: 2026-06-17
---

# Gaußsche Mischmodelle

## Short definition

Ein Gaußsches Mischmodell (Gaussian Mixture Model, GMM) ist eine
Wahrscheinlichkeitsverteilung, die als **gewichtete Summe mehrerer Gauß-Verteilungen**
gebildet wird. Damit lässt sich nahezu jede komplexe, auch mehrgipflige Dichte
approximieren – im kontinuierlichen Gegenstück zu diskreten Bayes-Netzen.

## Intuition

Eine einzelne Gauß-„Glocke“ kann nur einen Hügel beschreiben. Die echte Welt hat aber
oft mehrere Häufungen – Pixel gehören z. B. zu „Wand“, „Busch“, „Schild“ oder „Straße“,
jede mit eigener typischer Helligkeit. Wirf für jede Häufung eine Glocke hin und
**addiere sie gewichtet**: Schon kann die Gesamtkurve mehrere Gipfel und beliebige Formen
haben. Mehr Komponenten = feinere Approximation. So „baut“ man komplexe Verteilungen aus
einfachen Bausteinen – wie man jede Melodie aus wenigen Grundtönen mischen kann.

## Explanation

**Baustein: die Gauß-Verteilung.** Im 1D-Fall beschreibt sie die Normalverteilung einer
Variablen mit Mittelwert $\mu$ und Standardabweichung $\sigma$ (Varianz $\sigma^2$). In
$n$ Dimensionen wird daraus die **multivariate** Gauß-Verteilung mit Mittelwertvektor
$\mu$ und **Kovarianzmatrix** $\Sigma$.

**Die Kovarianzmatrix** ist der Schlüssel zur Form: Sie ist symmetrisch; die **Diagonale**
enthält die Varianzen der einzelnen Dimensionen, die **Nebendiagonale** die Kovarianzen
(Abhängigkeit zwischen Dimensionen). $\Sigma=I$ ergibt einen Kreis; eine Diagonalmatrix
mit ungleichen Einträgen streckt achsenparallel; Nebendiagonalterme **korrelieren** die
Dimensionen und **rotieren** die Verteilung. (Fast) unabhängige Dimensionen haben sehr
niedrige Kovarianz.

![[covariance-effect.pdf]]
*Die Kovarianzmatrix streckt und rotiert die Gauß-Verteilung: Einheitsmatrix → Kreis,
Diagonalmatrix → achsenparallele Ellipse, Nebendiagonalterme → korrelierte, rotierte
Ellipse.*

**Die Mischung.** Ein GMM kombiniert $M$ solche Gauß-Komponenten mit Mischgewichten
$\pi_m$ (Wahrscheinlichkeit, dass ein Datenpunkt von Komponente $m$ erzeugt wurde):
$p(x)=\sum_m \pi_m\,\mathcal{N}(x;\mu_m,\Sigma_m)$, $\pi_m\ge 0$, $\sum_m\pi_m=1$. Zur
Vereinfachung kann man identische Kovarianzmatrizen für alle Komponenten verwenden.

![[gmm-mixture.pdf]]
*Eine Mischverteilung (schwarz) als gewichtete Summe einzelner Gauß-Komponenten
(gestrichelt). Mehrere Komponenten erzeugen mehrere Gipfel.*

**Warum hier?** Ein GMM ist ein **zusammengesetztes (gemischtes) generatives Modell**:
eine diskrete Zustands-/Klassenverteilung $p(C)$ mit zustandsbedingten kontinuierlichen
Verteilungen $p(O\mid C)$. Beispiel aus VL09: ein Pixel (Graustufe 0–255) soll einer von
vier Klassen (Wand/Busch/Schild/Straße) zugeordnet werden. Man lernt $p(O\mid C\!=\!c)$
als Dichte pro Klasse und Priors $p(C\!=\!c)$, berechnet
$p(O,C)=p(O\mid C)\,p(C)$ und klassifiziert per
$\arg\max_c p(C\!=\!c\mid O\!=\!o)=\arg\max_c p(O\!=\!o,C\!=\!c)$. Als **generatives**
Modell kann man umgekehrt aus $p(C)$ und $p(O\mid C)$ Pixelwerte **sampeln** – die
ergeben aber noch kein strukturiertes Bild, weil die lokalen räumlichen Zusammenhänge
fehlen. So verbindet das GMM die diskrete Welt der [[Bayes-Netzwerke]] mit dem
kontinuierlichen Wahrnehmungsraum.

## Worked example

**Pixelklassifikation (vereinfacht).** Zwei Klassen, Helligkeit $o\in[0,255]$:
„Straße“ $\sim \mathcal{N}(\mu\!=\!80,\sigma\!=\!20)$, „Wand“ $\sim
\mathcal{N}(\mu\!=\!180,\sigma\!=\!25)$, Priors $p(\text{Straße})=0.6$,
$p(\text{Wand})=0.4$. Für einen Pixel mit $o=150$:
- $p(o\mid\text{Straße})\,p(\text{Straße})$: die Straßen-Glocke ist bei 150 schon weit
  abgefallen (3.5 $\sigma$) → winzig.
- $p(o\mid\text{Wand})\,p(\text{Wand})$: 150 liegt 1.2 $\sigma$ unter 180 → deutlich
  größer.
→ MAP-Entscheidung: **Wand**. Die Gesamtdichte aller Pixel ist die Mischung
$p(o)=0.6\,\mathcal{N}(80,20)+0.4\,\mathcal{N}(180,25)$ – ein zweigipfliges GMM.

## Formal definition / equations

1D-Gauß: $\mathcal{N}(x;\mu,\sigma)=\frac{1}{\sigma\sqrt{2\pi}}
\exp\!\big(-\frac{(x-\mu)^2}{2\sigma^2}\big)$.
Multivariat:
$$ \mathcal{N}(x;\mu,\Sigma)=\frac{1}{(2\pi)^{n/2}|\Sigma|^{1/2}}
\exp\!\Big(-\tfrac12(x-\mu)^{\top}\Sigma^{-1}(x-\mu)\Big). $$
Varianz $\sigma^2=\frac{1}{N}\sum_i (x_i-\mu)^2$; Kovarianzmatrix
$\Sigma=\frac{1}{N}\sum_i (x_i-\mu)(x_i-\mu)^{\top}$ (Spaltenvektoren). Mischung:
$p(x)=\sum_{m=1}^{M}\pi_m\,\mathcal{N}(x;\mu_m,\Sigma_m)$. Symbole: $\mu$ = Mittelwert(vektor),
$\Sigma$ = Kovarianzmatrix, $|\Sigma|$ = Determinante, $\pi_m$ = Mischgewicht, $n$ =
Dimensionen, $N$ = Stichprobengröße.

## Role in this class or project

Liefert in [[VL09 Visuelle Wahrnehmung Top-Down]] die **kontinuierliche** Repräsentation
für generative Modelle und schließt damit den Bogen von diskreten
[[Bayes-Netzwerke|Bayes-Netzen]] zu reellwertigen Wahrnehmungsräumen (Bilder, Tiefen,
Bewegungen). Grundlage für Multimodalität/Informationsfusion (VL10–11).

## Exam, assignment, or project relevance

Gauß-Formel kennen und Symbole erklären; die **Kovarianzmatrix interpretieren**
(Streckung, Rotation, Determinante; Diagonale = Varianzen); Varianz/Kovarianz
**berechnen** (Übungsblatt 10 „Kovarianzmatrizen“); ein GMM als gewichtete Summe
beschreiben und für eine einfache Pixelklassifikation den MAP-Entscheid führen. Formeln
in der [[Formelsammlung (Tutorium)]].

## Related global concepts

[[Gaussian Mixture Model]] (allgemeine Seite), [[Bayesian Inference]]
(generative Klassifikation), [[Maximum Likelihood Estimation]]
(Komponenten schätzen, EM), [[Bayes' Theorem]].

## Related local pages

[[Bayes-Netzwerke]], [[Generative und diskriminative Modelle]],
[[VL09 Visuelle Wahrnehmung Top-Down]], [[Formelsammlung (Tutorium)]].

## Common confusions

- **Kovarianz ≠ nur Streuung.** Die Diagonale ist Streuung (Varianz); erst die
  **Nebendiagonale** kodiert Abhängigkeit/Rotation. $\Sigma=I$ ⇒ unkorreliert, rund.
- **Mischgewichte sind Wahrscheinlichkeiten.** $\pi_m\ge0$ und $\sum_m\pi_m=1$ – keine
  beliebigen Skalierungsfaktoren.
- **Sampling ≠ Bildstruktur.** Pixelweises Sampeln aus $p(O\mid C)$ erzeugt korrekte
  Statistik, aber kein kohärentes Bild – die räumlichen Abhängigkeiten fehlen.

## Sources

VL09 (Folien: zusammengesetzte Verteilungen, Gauß 1D/multivariat, Kovarianzmatrix,
Gaussian Mixture Models, Pixelklassifikations-Beispiel); [[Formelsammlung (Tutorium)]].
