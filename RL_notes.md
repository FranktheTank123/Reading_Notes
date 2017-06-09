# Reinforcement Learning Notes
**Author: Frank Xia**

## The difference between supervised & reinforcement learning

* Supervised learning is of the form

$$y =f(x)$$

and we are given $x$ and $y$ to learn $f(\cdot)$.

* Reinforcement learning is of the form

$$y = f(x) \\ z$$

and we are given $x$ and $z$ to learning $y$ and $f(\cdot)$.

## Markov Decision Process (MDP)
* **Markov** means
    1. only present matters
    2. $P$'s are stationary (they don't change over time)

### The Problem
- States: $s$, all the possible current positions
- Model: $T(s,a,s')~P(s'|s,a)$ where $a\in A(s)$ this is the probability of **end up $s'$ with state $s$ and action $a$.**
- Actions: $A(s), A$, the all actions we **can** make at state $s$.
- Reward:
    - $R(s)$: scalar value at state $s$
    - $R(s,a)$: enter $s$ with taking an action $a$
    - $R(s,a,a)$: $s$ to $s'$ via $a$

### Solution
- Policy: a function $\pi(s) \to a$. $\pi^*$ will optimize long term reward $R(s)$

$$
\pi^* \equiv f\\ r \equiv z \\ s \equiv x
$$

### More on rewards
* **Delayed** rewards
* minor changes matter (which will change the policy)

### Sequences of rewards: assumptions
* Infinite horizon
* Utility of Sequence
$$U(s_0,...,s_n...) = \sum \gamma ^t R(s_t)$$ with $\gamma \in [0, 1)$

## Policies 
We define the optimized policy as

$$\pi^* = argmax_\pi E\left[\sum_t \gamma^t R(s_t)|\pi\right]$$

so the **utility of policy $\pi$ at state $s$** to be

$$
U^\pi(s) = E\left[ \sum \gamma^tR(s_t) | \pi, s_0 = s \right]
$$

Notice that the above utility is the **long term feedback**. It is not equal to $R(s)$, which is the **immediate feedback**.

For instance, there could be negative $R(s)$ (say, college tuition), but long term positive $U^\pi (s)$.

Let's go to each state: the optimal action to take at state $s$ is: (check all the actions on the transition probability multiplied by the next state's utility)

$$
\pi^*(s) = argmax_a \sum_{s'}T(s,a,s')U(s')
$$

For convenient purpose, we denote

$$
U(s) \equiv U^{\pi^*}(s)
$$

combining the equation gives us the **Bellman Equation**

$$
U(s) = R(s) + \gamma \max_a\sum_{s'}T(s,a,s')U(s')
$$

However, we cannot solve this directly even we have $N$ equations and $N$ unknowns ($|S|=N$), because of the $\max$ operator is non-linear.

### Value Iteration
1. Start with arbitrary utilities
2. Update utilities based on neighbours
3. repeat 2 until converge

$$
\hat{U}_{t+1}(s) = R(s) + \gamma \max_a\sum_{s'}T(s,a,s')\hat{U}_t(s')
$$

The intuition behind the convergence is that $R(s)$ is the truth, and the error term are discounted by $\gamma$.

### Policies: finding policies
We usually use VI to find policy, so we don't really need to find the precise $U$.

1. Start with guessing $\pi_0$
2. Evaluate: gives $\pi_t$ calculate $U_t = U^{\pi^t}$
3. Improve: $\pi_{t+1} = argmax_a\sum T(s,a,s')U_t(s')$

PI usually have a faster convergence rate than VI. Note that in 2:

$$
U_t(s) = R(s) + \gamma T(s, \pi_t(s), s')U_t(s')
$$

we use **the given policy, not to max the policy**, so this linear system is solvable.

### Another way to do Bellman's Equations

Rewrite the regular BE:

$$V(s) = \max_a \left( R(s,a) + \gamma \sum T(s,a,s')V(s') \right)$$ 

Define Q to be the inner part of the outer $\max$:

$$
Q(s,a) = R(s,a,) + \gamma \sum T(s,a,s')\max_{a'}Q(s',a')
$$

Why doing this? Because Q form is much more useful to take expectation

## Reinforcement Learning Basics
In MDP problem, we  have agent (policy) with environment (the MDP). Now, in RL, agent and environment are separate. Therefore, agent needs to explore the environment using action, and the feedback are rewards & new states. Under this set-up, we **don't know the rules**.

### Behavior structures
* **Plan**: a fixed sequence of actions.
    * **Con 1**: cannot do this during learning
    * **Con 2**: what if environment is stochastic
* **Conditional Plan**: plan with if statement
* **Stationary Policy / Universal Plan**: mapping from state to action
    * **Con 1**: very large
**For MDP, we always have optimal stationary policy.**

### Evaluating a learner
In RL, we don't evaluate policy, we evaluate learner, who outputs policy.

Possible evaluation metrics:

* value of returned policy
* computational complexity (time)
* sample complexity (how much data it needs)
* space complexity (usually not an issue vs. the other 2 above)

