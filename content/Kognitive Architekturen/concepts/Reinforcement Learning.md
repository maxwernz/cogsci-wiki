---
type: method
status: active
scope: local
classes: [Kognitive Architekturen]
projects: []
domains: [reinforcement learning, decision making, AI]
sources: ["[[VL05 Belohnungslernen I]]", "[[VL06 Belohnungslernen II]]"]
created: 2026-06-09
updated: 2026-06-09
---

# Reinforcement Learning (Belohnungslernen)

## Short definition

Reinforcement Learning (RL) optimiert **Verhalten** allein anhand von **Belohnung/
Bestrafung** als Feedback. Ziel ist eine Strategie (*policy*), die die erwartete
zukünftige Belohnung maximiert.

## Intuition

Ein Kind lernt Fahrradfahren nicht aus einer Anleitung, sondern durch Versuch,
Sturz (negative Belohnung) und gelungene Meter (positive Belohnung). Es weiß nicht
vorab, welche Muskelaktion „richtig" ist – es probiert, behält, was sich gut
anfühlt, und verteilt das Lob rückwärts auf die Aktionen, die dorthin geführt haben.
Das ist RL.

## Explanation

### Markov-Entscheidungsprozess (MDP)

RL-Probleme werden als **MDP** $(S, A(s), P(s'|s,a), R(s,s',a), \gamma)$ modelliert:
- $S$: Zustände; $A(s)$: Aktionen im Zustand $s$;
- $P(s'|s,a)$: Übergangswahrscheinlichkeit; $R(s,s',a)$: Belohnung;
- $\gamma \in [0,1]$: **Abschwächungsfaktor** (zukünftige Belohnung zählt weniger).

**Markov-Eigenschaft**: Der aktuelle Zustand reicht für maximal genaue
Zukunftsprädiktion – frühere Zustände bringen keinen Zusatznutzen; die Welt ist
voll observierbar.

### Wertefunktionen

$$V^\pi(s) = \mathbb{E}\{r_{t+1} + \gamma r_{t+2} + \gamma^2 r_{t+3} + \dots \mid s_t = s, \pi\}$$
$$Q^\pi(s,a) = \mathbb{E}\{r_{t+1} + \gamma r_{t+2} + \dots \mid s_t = s, a_t = a, \pi\}$$
- $V^\pi(s)$: erwartete zukünftige (abgeschwächte) Belohnung ab $s$ unter $\pi$;
- $Q^\pi(s,a)$: dasselbe, wenn zuerst Aktion $a$ ausgeführt wird.
- Optimal: $V^*(s)=\max_\pi V^\pi(s)$, $Q^*(s,a)=\max_\pi Q^\pi(s,a)$. Aus $Q^*$
  liest man die Strategie **direkt** ab: $\pi^*(s) = \arg\max_a Q^*(s,a)$; aus $V^*$
  nur **mit Modell**.

### Mit Modell: Dynamische Programmierung / Bellman

Ist das MDP bekannt, liefert die **Bellman-Gleichung** als Update die optimale
Wertefunktion (Werteiteration):
$$V(s) \leftarrow \max_a \mathbb{E}_{s'}[R(s,s',a) + \gamma V(s')]$$
$$Q(s,a) \leftarrow \mathbb{E}_{s'}[R(s,s',a) + \gamma \max_{a'} Q(s',a')]$$
**Policy Iteration** wechselt zwischen **Strategieevaluation** (Wertefunktion zu
gegebener $\pi$ abschätzen) und **Strategieverbesserung** (greedy bzgl. Werten) – ein
EM-artiges Verfahren, das gegen $\pi^*$ konvergiert.

### Ohne Modell: TD-Lernen und Q-Learning

Der **Temporal-Difference-Fehler** ist die Differenz zwischen gesehener und
erwarteter Belohnung (positiv = besser als erwartet):
$$\delta = r + \gamma V(s') - V(s)$$
- **TD(0)**-Update (Strategieevaluation):
  $V(s_t) \leftarrow V(s_t) + \alpha[r_{t+1} + \gamma V(s_{t+1}) - V(s_t)]$ mit
  Lernrate $\alpha\in[0,1]$ ($\alpha\to0$: langsame Mittelung; $\alpha=1$: direkte
  Übernahme).
- **Q-Learning** (lernt Werte **und** optimiert Strategie zugleich, *off-policy*):
  $$Q(s_t,a_t) \leftarrow Q(s_t,a_t) + \alpha\big[r_{t+1} + \gamma \max_{a} Q(s_{t+1},a) - Q(s_t,a_t)\big]$$
  Watkins (1989): Konvergiert gegen $Q^*$ (und $\pi\to\pi^*$), solange das MDP
  endlich ist und **jede Aktion hinreichend oft** probiert wird.

### Exploration vs. Exploitation

Damit jede Aktion oft genug vorkommt: **$\epsilon$-greedy** – meist die beste Aktion,
mit Wahrscheinlichkeit $\epsilon$ eine zufällige. Garantiert im Limit unendlich
häufige Exploration → Konvergenz.

### Actor-Critic

Mischt Werte- und Strategieiteration mit **Funktionsapproximation**:
- **Critic** schätzt die Wertefunktion über den TD-Fehler (z. B. **SARSA**-Update,
  *on-policy*: $Q(s_t,a_t)\leftarrow Q(s_t,a_t)+\alpha[r_{t+1}+\gamma Q(s_{t+1},a_{t+1})-Q(s_t,a_t)]$).
- **Actor** verstärkt $s\to a$ bei positivem TD-Fehler, schwächt es sonst ab.
- Mit neuronalen Netzen teils per Gradientenabstieg → schnellere Konvergenz; Basis
  z. B. für **RLHF** in LLMs.

### Beschleunigung (VL06)

- **Eligibility Traces / TD($\lambda$)**: Verteilen seltene Belohnung über die
  Erinnerungsspur. $\lambda\in[0,1)$ steuert die Reichweite; $\lambda=0$ = TD(0),
  $\lambda\to1$ = tiefe Verteilung. (Akkumulierende vs. ersetzende Spur.)
- **DYNA-Q** (Sutton): Lerne nebenbei ein **Zustandsübergangsmodell** und „plane" mit
  simulierten Erfahrungen → löst die Dilemmata „Planung zu langsam/zu speicherhungrig".
  **Planung = modellbasiertes RL** („indirektes RL"); direktes RL lernt aus echter
  Erfahrung.
- **Hierarchie / Optionen / Semi-MDPs**: Aktionen werden zu **Verhalten** („öffne
  Tür" statt Einzelschritte). Optionen haben Start-/Endmengen, erlauben Abstraktion,
  Generalisierung und schnellere Planung (z. B. 4-Räume-Aufgabe).
- **Policy Gradients**: Lernen **keine** Wertefunktion, sondern projizieren den
  Belohnungsgradienten direkt auf parametrisierte Strategie $\pi_\theta$:
  $\theta_{m+1} = \theta_m + \alpha_m g$. Pro: keine Divergenz, Occam (Strategien oft
  einfacher als Wertefunktionen), Komplexität unabhängig von Zustandsraumgröße. Contra:
  kein globales Optimum garantiert, keine Werteprädiktion, nur *on-policy*.

## Worked example (Labyrinth, $\gamma=0.9$)

Im Torus-Labyrinth aus VL05 gibt es Belohnung 1 nur am Ziel $G$ (Konsumhandlung).
Die optimalen Werte fallen mit jedem Schritt Abstand um den Faktor $\gamma$: ein
Feld 1 Schritt entfernt hat $Q^* = 0{.}9$, 2 Schritte $0{.}81$, 3 Schritte
$0{.}729$, … $= 0{.}9^d$ bei Distanz $d$. Genau diese geometrische Abschwächung
„zieht" die Strategie zum Ziel.

## Role in this class or project

VL05–06 liefern den Verhaltenslern-Mechanismus für das im Hier-und-Jetzt agierende
System. RL erklärt psychologische Phänomene: **klassische Konditionierung** ↔ TD(0)/
Rescorla-Wagner; **operante Konditionierung** ↔ Policy Gradients; **latentes Lernen**
↔ modellbasiertes RL. Neuro-Substrat: Dopamin/Basalganglien (Schultz et al., 1997).
VL07 zeigt dann, woher die **Belohnung selbst** kommt (siehe
[[Motivation und Homöostase]] und [[Ideomotorik und Antizipation]]).

## Exam, assignment, or project relevance

MDP-Definition; $V$/$Q$ und ihre optimalen Versionen; Bellman/Werteiteration;
TD-Fehler und Q-Learning-Update **rechnen** können (Übungen 3–4, Tutorien 4–6);
$\epsilon$-greedy & Exploration-Exploitation; Actor-Critic/SARSA; Eligibility Traces
(akk. vs. ers. Spur rechnen); DYNA; Optionen/Semi-MDPs; Policy Gradients Pro/Contra.

## Related global concepts

- [[Global Wiki/concepts/Reinforcement Learning|Reinforcement Learning]] (globale Seite: MDP, TD/Q-Learning, Actor-Critic, Policy Gradients)
- [[Bayesian Inference]] (Unsicherheit, POMDPs als Ausblick)

## Related local pages

- [[Motivation und Homöostase]]
- [[Ideomotorik und Antizipation]]
- [[Evolutionäre Algorithmen]] (CMA-ES ↔ Policy Gradients)

## Common confusions

- **V vs. Q**: Aus $V^*$ allein lässt sich ohne Modell *keine* Strategie ablesen,
  aus $Q^*$ schon.
- **On- vs. off-policy**: Q-Learning ist off-policy (lernt $Q^*$ auch beim
  Explorieren); SARSA/Policy Gradients sind on-policy (die ausgeführte Strategie
  *ist* das, was gelernt wird).
- **„biased" TD-Fehler**: In Q-Learning ist $\max_{a}Q(s',a)$ selbst eine
  Approximation → das Update ist verzerrt (im Gegensatz zum unbiased TD-Fehler über
  echte Folgewerte).

## Sources

VL05 (Belohnungslernen I), VL06 (Belohnungslernen II); Sutton & Barto (2018);
Watkins (1989); Schultz, Dayan & Montague (1997).
