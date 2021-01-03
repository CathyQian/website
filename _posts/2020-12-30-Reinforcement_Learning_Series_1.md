---
layout: post
title: Reinforcement Learning Series 1
description: Foundamentals of reinforcement learning 
date: 2020-12-30
tags: reinforcement learning
comments_id: 25
---

This article series include my personal notes of the Reinforcement learning Specialization provided by the Unversity of Alberta and Alberta Machine Intelligence Institute on [Coursera](https://www.coursera.org/specializations/reinforcement-learning). The following four courses covered in this specialization are:

- 1. Foundamentals of Reinforcement Learning
- 2. Sample-based Learning Methods
- 3. Prediction and Control with Function Approximation
- 4. A Complete Reinforcement Learning System (Capstone)

This article is for Course 1, Foundamentals of Reinforcement Learning.

# Week 1, k-armed bandit problem and sample-average method

k-armed bandit problem is defined as 'we have an *agent* who chooses between k *actions* and receives a *reward* based on the action it takes.' The reward each action takes is stochastically choosen from a probability distribution (where **uncertainty** comes from), and the goal of the agent is to **maximize the return of the actions at each step**. It is a sequential decision making process under uncertainty.

An example is a doctor (agent) who has to choose between multiple treatments (action) without full knowledge of each treatments' effect on patients (uncertainty). The doctor's goal is to maximize the effect (rewards) of the treatments (actions) over some period of time. 

[<img src="/assets/2020-12-30-15-59-06.png" width="300"/>](/assets/2020-12-30-15-59-06.png)

If we know the *value* of each action, then it's fairly easy to make a choice at each step, as the agent can simply choose the action with the maximum value. However, we don't know the true value of each action beforehand, therefore we need to estimate the action value through experiments in which the agent take some action, get rewards, and estimate the action value based on the rewards. 

Two major questions can be asked about this process:

- How to estimate action values?
    We don't know the exact value for each action, so we estimate it using **sample-average method**.

    [<img src="/assets/2020-12-30-16-28-26.png" width="400"/>](/assets/2020-12-30-16-28-26.png)

    To make the calculation more computationally effective (less memory and less computing power), a bit of mathematical trick can be used so that estimated action value at the current step can be calculated based on the estimated action value and reward from the prior step. This trick is called incremental update rule.

    [<img src="/assets/2020-12-30-16-31-40.png" width="450"/>](/assets/2020-12-30-16-31-40.png)

    Here 1/n is called step size. It will decay over time as n increases gradually. A more general form of this equation is 

    [<img src="/assets/2020-12-30-16-34-04.png" width="450"/>](/assets/2020-12-30-16-34-04.png)

    The step size can be a constant value between 0 and 1. Is a constant step size better or a decaying step size better? It depends on the specific problem. In general, if the distribution of rewards change over time, i.e., non-stationary bandit problem, using a fixed step size may be more effective. Decay step size may be better for stationary bandit problem of which the distribution of rewards doesn't change over time. 

    If a fixed step size is used, the incremental update rule can be further simplified and it's intuitive that contribution from past rewards (n-t) decay exponentially with distance to the present time step (t).

    [<img src="/assets/2020-12-30-16-38-51.png" width="450"/>](/assets/2020-12-30-16-38-51.png)

    Choosing a fixed step size also requires experimentation. If the step size is too small, the estimated action value may not get close to the actual value; if it is too big, the estimated value may be very susceptible to stochasticity in the rewards and thus oscillate around the true value too much. 

    Keep in mind that due to the uncertainty in such experiments, a large number of runs (i.e., hundreds) are required and their averaged values are needed in order to fairly compare the impact of step sizes.

- Based on what principles does the agent take action during the experiments?

    Even if the agent knows the estimated action values at each step, it may take different actions. It can simply choose the action with the highest estimated value, or randomly choose an action regardless of its action value. The former is called exploitation and the later is called exploration. Exploitation will help the agent maximize short term rewards based on partial knowledge, and thus the agent may lose the opportunity to explore other actions and optimize overall returns in the long run. Exploration allows the agent to know more about all actions and thus optimize overall returns in the long run, however, the short-term return may not be optimal.

    Therefore, we have greedy action selection rule by which the agent always select the acton with the highest estimated value, and epsilon-greedy action selection rule by which the agent behave greedily most of the time, but select randomly among all actions regardless of their estimated action values with a small probability epsilon.

    [<img src="/assets/2020-12-30-16-58-06.png" width="400"/>](/assets/2020-12-30-16-58-06.png)

    Other methods for balancing exploitation and exploration include optimistic initial values and upper-confidence bound action selection. The former only drive early exploration and are not suited for non-stationary problems. It also require some knowledge of the max reward which is usually set as the optimistic initial value. 


# Week 2, Markov decision processes (MDP) and goal of agent in reinforcement learning

The problem of k-armed bandits problem is that it only considers short-term returns while in many cases long-term thinking is needed in order to optimize rewards.*Markov decision processes (MDPs) are a classical formalization of sequential decision making, where actions influence not just immediate rewards, but also subsequent situations, or states, and through those future rewards.*

Three major parties involved in MDPs are:
- agent: the learner and decision maker
- environment: the thing the agent interacts with, comprising everything outside the agent
- reward: numerical values that the agent seeks to maximize over time through its choice of actions, it passed from the environment to the agent

[<img src="/assets/2020-12-31-14-36-08.png" width="550"/>](/assets/2020-12-31-14-36-08.png)

Typical agent and environment interaction in MPDs can be described as above. The agent and environment interact at each of a sequence of discrete time steps, t = 0, 1, 2, 3.... Note that the real time interval between each time step can be anything depending on the specific problem. At time step t, the agent select an action At based on its environment's state St. Such an action will bring reward Rt+1 to the environment and change its state from St to St+1. The MDP and agent thereby give rise to a trajectory like this: *S0, A0, R1, S1, A1, R2, S2, A2, R3, ...*

The **dynamics** of a *finite* MDP which has finite number of states, actions and rewards is defined as the function p as follows:

[<img src="/assets/2020-12-31-14-47-27.png" width="450"/>](/assets/2020-12-31-14-47-27.png)

Importantly, the following condition is satisfied.

[<img src="/assets/2020-12-31-14-50-28.png" width="400"/>](/assets/2020-12-31-14-50-28.png)

The essence of this equation is that the probability of each possible value for St and Rt depends only on the immediately preceding state and action, St-1 and At-1, irrelevant of earlier states and actions. That is to say, the present state have the **Markov property** ---  it includes all the information necessary to predict the future interactions.

Previously we mentioned that MDPs considers long-term rewards while k-armed bandits problem only considers immediate reward. Why do we care about reward? Because it is what we are trying to optimize in reinforcement learning. A formal definition as the **reward hypothesis** is the goals and purposes of reinforcement learning is to *maximize the expected value of the cumulative sum of a received reward*.

So how do we define rewards mathematically?

There are two types of tasks: episodic task and continuous task. Episodic tasks are tasks in which the interaction breaks natually into subsequences called episodes, each episode ends in a terminal state, and episodes are independent. Continous tasks are tasks in which the interactions goes on continually and no terminal state exist.

For episodic task, we seek to maximize expected return. Here expected return instead of return is used because of randomness involved in the process. The return is the sum of rewards:

[<img src="/assets/2020-12-31-15-39-44.png" width="400"/>](/assets/2020-12-31-15-39-44.png)

For continous task, the above equation easily goes into infinity. A mathematical trick is to introduce discounting by adding discount rate gama ([0, 1]) into future rewards as follows:

[<img src="/assets/2020-12-31-15-43-32.png" width="450"/>](/assets/2020-12-31-15-43-32.png)

Mathematically, we can prove Gt is finite.

[<img src="/assets/2020-12-31-15-50-11.png" width="550"/>](/assets/2020-12-31-15-50-11.png)

If gama < 1 and the reward is a constant +1, then the return is

[<img src="/assets/2020-12-31-15-49-13.png" width="550"/>](/assets/2020-12-31-15-49-13.png)

The discount rate indicates a reward received k time steps in the future is worth only gama^(k-1) times what it would be worth if it were received immediately. If gama = 0, it means the agent only cares about the immediate reward. The closer gama to 1, the stronger the agent takes future rewards into account.

Alternatively, Gt can be defined recursively to allow us calculate Gt backwards starting from the termination state G(T) = 0.

[<img src="/assets/2020-12-31-15-52-28.png" width="450"/>](/assets/2020-12-31-15-52-28.png)


# Week 3, Value functions and Bellman equations

Now we have formally defined the MDPs and goal of reinforcement learning, our next question comes naturally -- how do we calculate the rewards for any MDPs and decide on the optimal way to act in order to maximize expected returns?

We need to be quantitative here. So let's first define some quantities using some mathematical formula, and translate our initial question into an optimization problem.

- **Policy**

    A policy is a mapping from states to probabilities of selecting each possible action. It tells an agent how to behave in their environment. If an agent is folloiwng a policy Pi at time t, then Pi(a|s) is the probability that At = a if St = s. If Pi is a constant for every single state, meaning there is only one action to take after each state, this policy is called a deterministic policy. Otherwise, it is called a stochastic policy. For stochastic policy, the following condition is satisfied:

    [<img src="/assets/2021-01-01-15-17-37.png" width="250"/>](/assets/2021-01-01-15-17-37.png)

    For MDPs (note most reinforcement learning process constitutes a MDP), policies are only determined by the current state, not other things like time or previous states. 

- **Value function**
 
    A value function defines the expected return for a state or state-action pair. Specifically, a *state-value function* of a state s under policy Pi is defined as:
    
    [<img src="/assets/2021-01-01-15-23-08.png" width="550"/>](/assets/2021-01-01-15-23-08.png)

    An *action-value function* of taking action a in state s under a policy Pi is defined as:

    [<img src="/assets/2021-01-01-15-25-26.png" width="550"/>](/assets/2021-01-01-15-25-26.png)

    Note that both value functions quantify the expected return at a certain state, so *the state-value function is a collective sum of action-value functions over different actions at the same state.*

- **Bellman equation**

    Bellman equation denotes the relationship between value functions of the present state and value functions of its possible successor state. *With Bellman equations and some termination conditions, value function for each state and state-action pairs can be calculated.*

    [<img src="/assets/2021-01-01-15-31-16.png" width="450"/>](/assets/2021-01-01-15-31-16.png)

    [<img src="/assets/2021-01-01-15-32-12.png" width="450"/>](/assets/2021-01-01-15-32-12.png)
    
    A good example of using Bellman equation to calculate value function is Gridworld (see Page 60 of the textbook).

Now we know how to calculate expected return of each state, so what is considered an optimal policy which can guarantee the maximum return? Formally, an optimal policy is defined as a policy that is at least as good (has the same or higher state-value function) as every other policy in every state. *A finite MDP may have more than one optimal policy but they will all share the same value function.*

Under optimal policy, optimal functions are defined as follows:

[<img src="/assets/2021-01-01-15-39-49.png" width="450"/>](/assets/2021-01-01-15-39-49.png)

[<img src="/assets/2021-01-01-15-40-04.png" width="450"/>](/assets/2021-01-01-15-40-04.png)

Similarly, *Bellman optimality equations can be used to calculate optimal value functions under optimal policy.* If we have the optimal state-value function or optimal action-value function, it is easy to work out the optimal policy.

# Week 4, Policy Iteration and Dynamic Programming

Now we know by solving Bellman equation state-value function and action-value function can be calculated -- the prediction problem. If we have the optimal state-value function or optimal action-value function, we can easily find out the optimal policy. So the question is how do we find optimal state-value function or optimal action-value function based on randomly initialized values given that value functions are usually randomly initialized because we have little knowledge about them?

The process of finding an optimal policy --- the control problem --- is called policy iteration. Dynamic programming is the computation method used for updating the values in this optimization process.

**Policy Iteration**

Policy iteration contains three major steps as follows:

- Initializing state-value function and policy arbitrarily for all states and actions involved. This step is easy as both state-value function and policy are represented as matrixes and we all know how to randomly initialize them. For example, a system has m states and n actions in each state, then the state-value function will be a m x 1 matrix and the policy will be an m x n matrix.

- Policy evaluation. It is the task of determining state-value function *V* for a policy Pi using Bellman equation. The state-value functions are updated iteratively using dynamic programming until the values converge (doesn't change much anymore.)

- Policy improvement. It is the process of making a new policy that improves on an original policy, by making it greedy with respect to the state-action value function of the original policy. Here greedy means choosing the action at the current state to be the one with the maximum state-action value among all actions, then update the policy accordingly. 

    [<img src="/assets/2021-01-02-16-48-24.png" width="650"/>](/assets/2021-01-02-16-48-24.png)

Below is a toy implementation of this process in Python.

```Python
def policy_iteration(env, gamma, theta):
    
    # 1. initialization of state value function V and policy pi
    V = np.zeros(len(env.S))
    pi = np.ones((len(env.S), len(env.A))) / len(env.A)
    policy_stable = False
    
    while not policy_stable:
        
        # 2. policy evaluation
        V = evaluate_policy(env, V, pi, gamma, theta)

        # 3. policy improvement
        pi, policy_stable = improve_policy(env, V, pi, gamma)
        
    return V, pi

def evaluate_policy(env, V, pi, gamma, theta):
    delta = float('inf')
    while delta > theta:
        delta = 0
        for s in env.S:
            v = V[s]

            # Bellman update
            new = 0
            for action in range(len(pi[0])):
                transitions = env.transitions(s, action)
                for state in range(len(transitions)):
                    reward = transitions[state][0]
                    p = transitions[state][1]
                    new += pi[s][action]*p*(reward + gamma*V[state])
            V[s] = new

            delta = max(delta, abs(v - V[s]))
            
    return V


def improve_policy(env, V, pi, gamma):
    policy_stable = True
    for s in env.S:
        old = pi[s].copy()

        # q greedify policy
        num_actions = len(pi[0])
        q = [0 for _ in range(num_actions)]
        for action in range(num_actions):
            transitions = env.transitions(s, action)
            for state in range(len(transitions)):
                reward = transitions[state][0]
                p = transitions[state][1]
                q[action] += p*(reward + gamma*V[state])
        max_action = np.argmax(q)
        pi[s] = [0 if i != max_action else 1 for i in range(num_actions)]

        if not np.array_equal(pi[s], old):
            policy_stable = False
            
    return pi, policy_stable

```

One question we may ask here is that there are much overlapped computation between the policy evaluation and policy improvement step, so it it possible to simplify such process? The answer is Yes, by truncating the policy evaluation step to only one sweep (one update of each state). Convergence to the optimal policy is proved to be still guaranteed. This algorithm is called value iteration. See detailed implementation below.

[<img src="/assets/2021-01-03-12-37-26.png" width="650"/>](/assets/2021-01-03-12-37-26.png)

```Python
def value_iteration(env, gamma, theta):
    V = np.zeros(len(env.S))

    while True:
        delta = 0
        for s in env.S:
            v = V[s]

            # Bellman Optimality update
            num_actions = len(pi[0])
            q = [0 for _ in range(num_actions)]
            for action in range(num_actions):
                transitions = env.transitions(s, action)
                for state in range(len(transitions)):
                    reward = transitions[state][0]
                    p = transitions[state][1]
                    q[action] += p*(reward + gamma*V[state])
            V[s] = max(q)

            delta = max(delta, abs(v - V[s]))
        if delta < theta:
            break

    # policy update 
    pi = np.ones((len(env.S), len(env.A)))/len(env.A)
    for s in env.S:
        # q greedify policy
        num_actions = len(pi[0])
        q = [0 for _ in range(num_actions)]
        for action in range(num_actions):
            transitions = env.transitions(s, action)
            for state in range(len(transitions)):
                reward = transitions[state][0]
                p = transitions[state][1]
                q[action] += p*(reward + gamma*V[state])
        max_action = np.argmax(q)
        pi[s] = [0 if i != max_action else 1 for i in range(num_actions)]

    return V, pi
```

**Dynamic programming**

Dynamic programming (DP) is a general approach to solving problems by breaking them into subproblems that can be solved separately, cached, then combined to solve the overall problem. It can be used to solve both policy evaluation and control tasks in MDP, if we have access to the dynamics function *p*. The reason we need dynamic programming in reinforcement learning is because it is computationally more efficient than other methods such as Monte Carlo Sampling or Brutal-force Search. DP is synchronous if it systematically sweeps the entire state space at each iteration (update every state exactly once at each iteration) and aynchronous if it does not update all states at each iteration and updates some states more than others. Asynchronous DP converges faster than synchornous DP and thus used widely in real world reinforcement learning problem.
