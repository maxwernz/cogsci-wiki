---
type: method
status: active
scope: global
classes: [Kognitive Architekturen, Understanding LLMs]
projects:
domains: [reinforcement learning, decision making, machine learning, AI]
sources:
created: 2026-06-17
updated: 2026-06-17
---

# Reinforcement Learning

## Short definition

Reinforcement learning (RL) is learning *what to do* — a mapping from situations
to actions — purely from a scalar reward signal, so as to maximise the total
reward accumulated over time. The learner is never told the correct action; it
must discover which actions pay off by trying them.

## General explanation

RL sits between supervised learning (which needs labelled correct outputs) and
unsupervised learning (which finds structure with no feedback). Its feedback is
*evaluative* (how good was the action) rather than *instructive* (what the right
action was), and it is typically *delayed*: a reward may arrive many steps after
the action that earned it, so the learner must solve a **credit-assignment**
problem — figuring out which past actions deserve the praise.

**The Markov Decision Process (MDP).** RL problems are formalised as an MDP
$(S, A, P, R, \gamma)$: a set of states $S$, actions $A(s)$ available in each
state, transition probabilities $P(s'\mid s,a)$, a reward function
$R(s,s',a)$, and a discount factor $\gamma\in[0,1]$ that makes near-term reward
worth more than distant reward. The defining **Markov property** is that the
current state captures everything needed to predict the future — the past adds
no information once you know the present state.

**Value functions.** The agent's behaviour is a **policy** $\pi$ (a rule for
choosing actions). Its quality is measured by value functions: the state value
$V^\pi(s)$ is the expected discounted future reward starting from $s$ and
following $\pi$; the action value $Q^\pi(s,a)$ is the same but committing to
action $a$ first. The optimal values $V^*,Q^*$ are the best achievable. A key
asymmetry: from $Q^*$ you can read the optimal policy directly,
$\pi^*(s)=\arg\max_a Q^*(s,a)$, but from $V^*$ alone you need a model of the
environment to do so.

**With a model — dynamic programming.** If the MDP is known, the **Bellman
equations** define the optimal values recursively, and value iteration / policy
iteration solve them. Policy iteration alternates *policy evaluation* (compute
values for the current policy) and *policy improvement* (act greedily with
respect to those values), converging to $\pi^*$.

**Without a model — temporal-difference learning.** When the dynamics are
unknown, the agent learns from experience. The **TD error**
$\delta = r + \gamma V(s') - V(s)$ is the gap between the reward actually seen
and the reward expected; positive means "better than expected." TD(0) nudges
$V(s)$ toward $r+\gamma V(s')$ by a learning rate $\alpha$. **Q-learning** is the
landmark *off-policy* control method: it learns $Q^*$ (and hence $\pi^*$) even
while exploring, provided every action is tried often enough. **SARSA** is its
*on-policy* cousin, learning the value of the policy actually being followed.

**Exploration vs exploitation.** To learn good actions the agent must sometimes
try apparently worse ones. The simplest scheme is **$\epsilon$-greedy**: take the
best known action most of the time, a random action with probability $\epsilon$.
Sufficient exploration is what guarantees convergence.

**Scaling it up.** Real problems need extensions: **actor–critic** methods pair a
value estimator (critic) with a policy (actor) and support function
approximation, including neural networks — this is the basis of RL from human
feedback (**RLHF**) used to align large language models. **Eligibility traces /
TD($\lambda$)** spread a rare reward back over a memory trace. **Model-based RL**
(e.g. Dyna) learns a transition model and plans with simulated experience.
**Policy-gradient** methods skip value functions entirely and ascend the reward
gradient on a parameterised policy $\pi_\theta$.

## Intuition

A child does not learn to ride a bike from instructions but from trying:
wobbling, falling (negative reward), and gliding a few metres (positive reward).
Nobody says which muscle command is "correct"; the child keeps what feels good
and propagates the credit backward onto the actions that led there. That is RL.

## Formal definition

$$V^\pi(s)=\mathbb E\!\Big[\textstyle\sum_{k\ge0}\gamma^k r_{t+k+1}\,\big|\,s_t=s,\pi\Big],\qquad
Q^\pi(s,a)=\mathbb E\!\Big[\textstyle\sum_{k\ge0}\gamma^k r_{t+k+1}\,\big|\,s_t=s,a_t=a,\pi\Big].$$

Q-learning update (off-policy, model-free):

$$Q(s_t,a_t)\leftarrow Q(s_t,a_t)+\alpha\big[r_{t+1}+\gamma\max_a Q(s_{t+1},a)-Q(s_t,a_t)\big].$$

Symbols: $r$ reward, $\gamma$ discount factor, $\alpha\in[0,1]$ learning rate,
$\delta=r+\gamma V(s')-V(s)$ the TD error. $V^*(s)=\max_\pi V^\pi(s)$ and
$Q^*(s,a)=\max_\pi Q^\pi(s,a)$ are the optimal values.

## Worked example

A maze with reward $1$ only at the goal $G$ and discount $\gamma=0.9$. The
optimal value of a cell $d$ steps from the goal is $Q^*=\gamma^d$: one step away
$0.9$, two steps $0.81$, three steps $0.729$, and so on. This geometric decay is
exactly what "pulls" the greedy policy toward the goal — each state prefers the
neighbour with the higher discounted value.

## Why it matters

RL is the general theory of learning to act under delayed, evaluative feedback.
It underlies game-playing agents, robotics and control, the alignment of large
language models via RLHF, and — in cognitive science and neuroscience — models of
conditioning and the dopamine reward-prediction-error signal.

## Used in

- [[Classes/Kognitive Architekturen/wiki/concepts/Reinforcement Learning|Reinforcement Learning (Belohnungslernen)]]
  (Kognitive Architekturen: MDPs, TD/Q-learning, links to classical/operant
  conditioning and dopamine)
- [[Finetuning and RLHF in Understanding LLMs]] (RLHF: actor–critic / policy
  optimisation against a learned reward model)

## Related concepts

- [[Bayesian Inference]] (acting under uncertainty; partially observable MDPs)
- [[Evolutionary Algorithms]] (CMA-ES as a black-box alternative to policy gradients)
- [[Maximum Likelihood Estimation]]

## Common confusions

- **$V$ vs $Q$:** an optimal policy can be read directly from $Q^*$ but from
  $V^*$ only with a model of the environment.
- **On- vs off-policy:** Q-learning learns $Q^*$ even while exploring
  (off-policy); SARSA and policy gradients learn the value of the policy actually
  executed (on-policy).
- **RL is not supervised learning:** the feedback is a reward, not the correct
  action, and it is often delayed.

## Sources

- Sutton & Barto, *Reinforcement Learning: An Introduction* (2018)
- Watkins (1989); Schultz, Dayan & Montague (1997)
