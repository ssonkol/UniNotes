# Passive Reinforcement Learning
---

## Notes

What if the agent doesn't know the transition model:
- P(s' | s, a)
and it doesn't know the reward function
- R(s)


In passive reinforcement learning the agent's policy is fixed.
The agents learns the utility by carrying out runs through the environment, following some policy.

Passive reinforcement learning is a type of reinforcement learning where the agent learns from a fixed dataset without interacting with the environment. In passive reinforcement learning, the agent is provided with a fixed set of training examples, which are typically obtained by observing a human expert or by running a pre-existing policy. The agent's goal is to learn a policy that maximizes the expected cumulative reward over the training examples.

Passive reinforcement learning is often used in scenarios where it is not feasible or desirable for the agent to interact with the environment directly. For example, in some robotics applications, it may be too dangerous or expensive to allow the robot to interact with the environment during the learning phase. In such cases, a pre-existing dataset can be used to train the robot's policy using passive reinforcement learning.

Passive reinforcement learning can be contrasted with active reinforcement learning, where the agent interacts with the environment in real-time and learns from the feedback it receives.

The agent computes each step using one-step lookahead on the expected value of actions.
- Picks the action with the greatest expected utility
- However its data on actions will be limited because it has only been trying pi(s)

---
Backlink: [[Reinforcement Learning]]
