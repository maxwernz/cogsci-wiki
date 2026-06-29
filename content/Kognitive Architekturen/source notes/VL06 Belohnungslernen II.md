---
type: source_note
status: processed
scope: local
class: Kognitive Architekturen
project:
source_type: lecture_slides
raw_path: "raw/VL Folien/KogArch_06_BelohnungslernenII.pdf"
created: 2026-06-09
updated: 2026-06-09
---

# VL06 – Belohnungslernen II (RL II)

## Summary

Drei Wege, das oft **langsame** Standard-RL zu beschleunigen bzw. zu erweitern:
(1) **episodisches Gedächtnis** (Eligibility Traces, DYNA), (2) **hierarchische
Strukturierung** (Optionen/Semi-MDPs), (3) **direkte** Strategieoptimierung
(**Policy Gradients**) ohne Wertefunktion.

## Key points

- **Eligibility Traces / TD($\lambda$)**: seltene Belohnung über die Erinnerungsspur
  verteilen; $\lambda$ steuert die Reichweite; akkumulierende vs. ersetzende Spur;
  Q($\lambda$)/SARSA($\lambda$).
- **DYNA-Q** (Sutton): lerne ein Übergangsmodell, „plane" mit simulierter Erfahrung
  parallel/asynchron → löst „Planung zu langsam/zu speicherhungrig". **Planung =
  modellbasiertes RL** („indirektes RL"); RL = modellfreies Lernen.
- **Update-Dimensionen**: flach↔tief (DP↔Monte Carlo), modellbasiert↔modellfrei.
- **Hierarchie**: Aktionen → **Verhalten/Optionen** (Start-/Endmengen);
  **Semi-MDP** als Framework; schnellere Planung, Generalisierung (4-Räume-Beispiel).
- **Policy Gradients**: lerne keine Wertefunktion, projiziere Belohnungsgradient auf
  parametrisierte Strategie $\pi_\theta$; Pro/Contra. Beispiel: Rennwagen-Controller
  (CMA-ES-optimierte Mapping-Funktion, integriert in subsumptionsartige Struktur).

## Important concepts

[[Reinforcement Learning]] (Eligibility Traces, DYNA, Optionen/Semi-MDP, Policy
Gradients – volle Tiefe).

## Methods, models, or theories

TD($\lambda$), Q($\lambda$)/SARSA($\lambda$); DYNA-Q; Semi-MDP/Optionen; Policy
Gradient (Gradientenaufstieg auf $J(\theta)$); CMA-ES zur Parameteroptimierung.

## Equations or formal definitions

Eligibility-Update: $V(s)\leftarrow V(s)+\alpha\,e(s)[r_{t+1}+\gamma V(s_{t+1})-V(s_t)]$
mit Spur $e(s)$ (akk.: $(1-\lambda)\sum_k(\lambda\gamma)^{t-k}\delta_{s,s_k}$).
Policy-Update: $\theta_{m+1}=\theta_m+\alpha_m g$, Ziel $J(\theta)=\mathbb{E}\sum_k a_k r(x_k,u_k)$.
Erklärt in [[Reinforcement Learning]] und [[Formelsammlung (Tutorium)]].

## Local relevance

Vervollständigt den RL-Block; verbindet zu [[Evolutionäre Algorithmen]] (CMA-ES) und
[[Brooks (1990) Elephants Dont Play Chess|Subsumption]] (Controller-Struktur).
Übung 4 (RL II), Tutorien 5–6.

## Exam or project relevance

Eligibility Traces (akk. vs. ers. Spur **rechnen**); DYNA-Prinzip; Optionen/Semi-MDP;
Policy Gradients Pro/Contra; Reflektionen zum RL-Design (Zustands-/Aktionsraum,
Belohnung, Frame-Problem-Bezug). POMDPs als offenes Problem.

## Links to global concepts

_Globaler Promotionskandidat: „Reinforcement Learning"._

## Open questions

POMDPs (unvollständige Zustandsinfo), Unsicherheit, große/kontinuierliche
Zustandsräume, effektives Erlernen hierarchischer Umweltmodelle – laut Folien die
zentralen offenen Probleme. Wie man das **Modell** lernt → [[VL07 Motivation Homöostase und Antizipation]].
