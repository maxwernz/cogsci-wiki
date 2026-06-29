---
type: source_note
status: processed
scope: local
class: Kognitive Architekturen
project:
source_type: lecture_slides
raw_path: "raw/VL Folien/KogArch_05_BelohnungslernenI.pdf"
created: 2026-06-09
updated: 2026-06-09
---

# VL05 – Belohnungslernen I (Reinforcement Learning)

## Summary

Einführung ins **Reinforcement Learning**: Verhaltensoptimierung allein aus
Belohnung. Von der Formalisierung als **MDP** über die **Bellman-Gleichung** und
modellbasierte **Werte-/Strategieiteration** bis zum modellfreien **TD-Lernen** und
**Q-Learning**, inkl. Exploration-Exploitation und **Actor-Critic**.

## Key points

- RL-Bezug zur Psychologie/Neuro: klassische Konditionierung ↔ TD(0)/Rescorla-Wagner;
  operante Konditionierung ↔ Policy Gradients; latentes Lernen ↔ modellbasiertes RL.
  Substrat: Basalganglien, Amygdala, Dopamin (Schultz et al., 1997).
- Drei Lerntypen: überwacht (inkl. autoregressiv/selbst-überwacht), Belohnungslernen,
  unüberwacht.
- **MDP** $(S,A,P,R,\gamma)$, Markov-Eigenschaft; **$V^\pi$/$Q^\pi$** und optimale
  Versionen; aus $Q^*$ Strategie direkt ablesbar, aus $V^*$ nur mit Modell.
- **Mit Modell**: Bellman/Werteiteration, Policy Iteration (EM-Prinzip).
- **Ohne Modell**: TD-Fehler, TD(0), **Q-Learning** (off-policy; Watkins-Konvergenz),
  **$\epsilon$-greedy**.
- **Actor-Critic**/SARSA; Ausblick neuronale Netze, RLHF.

## Important concepts

[[Reinforcement Learning]] (volle Tiefe: MDP, Bellman, TD, Q-Learning, Actor-Critic).

## Methods, models, or theories

Dynamische Programmierung; Policy/Value Iteration; TD(0); Q-Learning; SARSA;
Actor-Critic.

## Equations or formal definitions

$V^\pi(s)=\mathbb{E}\{\sum_k \gamma^k r_{t+k+1}\mid s,\pi\}$;
Q-Learning: $Q(s_t,a_t)\leftarrow Q(s_t,a_t)+\alpha[r_{t+1}+\gamma\max_a Q(s_{t+1},a)-Q(s_t,a_t)]$.
Labyrinth-Beispiel ($\gamma=0.9$): $Q^*=0.9^d$ bei Distanz $d$ zum Ziel. Vollständig
hergeleitet/erklärt in [[Reinforcement Learning]] und [[Formelsammlung (Tutorium)]].

## Local relevance

Verhaltenslern-Baustein für das Hier-und-Jetzt-System; baut auf der Wert-aus-Aufwand-
Inferenz aus [[VL04 Ontogenetische Entwicklung]] auf und wird in
[[VL06 Belohnungslernen II]] beschleunigt. Übung 3 (RL I), Tutorium 4.

## Exam or project relevance

MDP definieren; $V$/$Q$ und optimale Versionen; Bellman/Werteiteration; TD-Fehler &
Q-Learning **rechnen**; $\epsilon$-greedy; Actor-Critic/SARSA. Labyrinth-Q-Werte.

## Links to global concepts

_Globaler Promotionskandidat: „Reinforcement Learning"._ [[Bayesian Inference]]
(POMDP-Ausblick).

## Open questions

Kann man Verhalten ohne Modell optimieren? (Ja – TD/Q-Learning.) Wie lernt man das
MDP selbst? → [[VL07 Motivation Homöostase und Antizipation]].
