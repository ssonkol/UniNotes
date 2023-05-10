# Game Theory
Tag: #review 

---
## Definitions



---
## Notes

*When checking matrices, check on columns and rows - not diagonally! Unless we are doint Pareto Optimal*

### Dominant Strategies

Given any particular strategy s (either C or D) agent $i$, there will be a number of possible outcomes

We say $s_1$ dominates $s_2$ if every outcome possible by $i$ playing $s_1$ is preferred over every outcome possible by $i$ playing $s_2$

Thus in game:![[Pasted image 20221117141833.png]][1]

C dominates D for both players.

Generally there are two senses of "preferred"

1. $s_1$ strongly dominates $s_2$ if the utility of every outcome possible by $i$ playing $s_1$ is strictly greater than every outcome possible by $i$ playing $s_2$.
	- In other words, $u(s_1) > u(s_2)$, for all outcomes.
2. $s_1$ weakly dominates $s_2$ if the utility of every outcome possible by $i$ playing $s_1$ is no less than every outcome possible by $i$ playing $s_2$.
	- In other words, $u(s_1) >= u(s_2)$, for all outcomes.


A rational Agent will never play a dominated strategy.
- This means our agent will delete the dominated strategy

**Example**

![[Pasted image 20221117142631.png]][1]
In this example we can eliminate the dominated strategies and simplify the game

To do this, lets try check player B's columns in a matrix (denoted in blue)![[Pasted image 20221117143119.png]][1]

You can think of it as 3 vectors ![[Pasted image 20221117143141.png]][1]

We can say that every component of R (the right matrix) is dominated by L (left) this means we can remove R (the 0's vector).

Thid means we are left with ![[Pasted image 20221117143401.png]][1]

Let's pull it out again...![[Pasted image 20221117143505.png]][1]

check their columns![[Pasted image 20221117143447.png]][1]

As you can see (3,0) is dominated but (1,1) and (0,4) don't dominate therefore there is no domination overall.

Meaning, there is no strategy so we can't remove anything.

### Nash Equilibrium Strategy

In general, we will say that two strategies $s_1$ and $s_2$ are in Nash equilibrium (NE) if:
1. under the assumption that agent i plays $s_1$, agent j can do no better than play $s_2$; and
2. under the assumption that agent j plays $s_2$, agent i can do no better than play $s_1$.

Neither agent has any inventive to deviate from an NE.


**Example**
![[Pasted image 20221117155433.png]][2]

Here the Nash Equilibrium is (Y,Y).
- If $i$ assumes that $j$ is playing Y, then $i$'s best response is to play Y
- Similarly for J

If two strategies are equal to each other then they too are in NE
- In a game like this, you can find the NE by cycling through the outcomes, asking if either agent can improve its payoff by switching its strategy.
- E.g. (X,Y) is not NE because $i$ cam switch its payoff from 1 to 2 by switching from X to Y

##### Cons
- Not every interaction scenario has a pure strategy NE
- Some interaction scenarios have more than one NE


### Pareto Optimal Strategies

**An outcome is said to be Pareto optimal (or Pareto efficient) if there is no other outcome that makes one agent better off without making another agent worse off.**

If an outcome is Pareto optimal, then at least one agent will be reluctant to move away from it (because this agent will be worse off).

If an outcome $w$ is not Pareto optimal, then there is another outcome $w'$ that makes
everyone as happy, if not happier, than $w$

“Reasonable” agents would agree to move to $w'$ from $w$ if $w$ is not Pareto optimal
and $w'$ is.

**Example**
In this game, the Pareto Efficient Outcome is (D,D)![[Pasted image 20221117161303.png]][3]
Since there is no solution which either agent does better.

**Example 2**
This next game has two Pareto efficient outcomes, (C,D) and (D,C).![[Pasted image 20221117161437.png]][3]

Note that Pareto efficiency doesn't always mean it's fair.
- Just that you can’t move away and make one agent better off without making the other worse off.
- Different way of thinking about this: Ignore players and imagine you are buying
- socks online. All options cost the same $i$ is the number of stars (rating) and $j$ is the number of pairs you get.
Trade-off: all reasonable options are Pareto efficient

#### Social Welfare
The social welfare outcome $w$ is the sum of the utilities that each agent gets from $w$:![[Pasted image 20221117161837.png]][3]


Think of this as the total amount of money in the system

**Example**
In both games, (C,C) maximises social welfare![[Pasted image 20221117161947.png]][3]




### Normal Form Games
An n-person, finite, normal form game is a tuple (N, A, u), where;
- N is a finite set of players.
- A = $A_1$ x . . . x $A_n$ where $A_i$ is a finite set of actions available to $i$.
- Each a = ($a_1$, . . . , $a_n$) $\in$ A is an action profile.
- u = ($u_1$, . . . , $u_n$) where $u_i$ : A $\rightarrow R$ is a real-valued utility function for $i$.
Naturally represented by an n-dimensional matrix

We analyse games in terms of strategies, that is what agents decide to do
- Combined with what the other agent(s) do(es) this jointly determines the payoff
An agent's strategy set is its set of available choices
- This can just be the set of actions - pure strategies

**Example**
Here is the payoff matrix from the “choose which side” (of the road) game:![[Pasted image 20221117164027.png]][4]

Any game with $u_{1(a)}= u_j(a)$ for all $a \in A_{i}*A_j$ is a common payoff game

Example 2
The misanthropes’ (un)coordination game:
- Here we try to avoid each other.![[Pasted image 20221117164251.png]][4]

#### Constant Sum Games
Example![[Pasted image 20221117164358.png]][4]
All sections in their own individual right sum to 0 - This can also be known as Zero Sum

Where preferences of agents are diametrically opposed we have strictly competitive scenarios
- Zero Sum implies strictly competitive

*Note that Zero-sum encounters are very rare. Most encounters have some room for agents to fins a somewhat mutually beneficial outcome*

### Mixed Strategies

A mixed strategy is just a probability distribution across a set of pure strategies.

So, for a game where agent i has two actions $a_1$ and $a_2$, a mixed strategy for i is a
probability distribution:![[Pasted image 20221117165721.png]][5]

To determine the mixed strategy, $i$ can compute the best values of $P(a_1)$ and $P(a_2)$
These will be the values which give $i$ the highest expected payoff given the options that $j$ choose and the joint payoff that result.

We could write these down but there is also a graphical method.

**Example**
Considering the payoff matrix below![[Pasted image 20221117165928.png]][5]

We want to compute mixed strategies to be used by the players 

Looking at $i$'s pov
- Let's say you know that $j$ plays $a_3$
- $i$'s payoff will be 3 or 0 depending on whether $i$ picks $a_1$ or $a_3$
- The expected payoff therefore varies along the line, as $P(a_1)$ varies from 0 to 1
![[Pasted image 20221117170319.png]]

We can also consider J's perspective ![[Pasted image 20221117170512.png]][5]


If we join both lines, $i$ has the same expected payoff whatever $j$ does.
This is the rational choice of mixed strategy.![[Pasted image 20221117170614.png]][5]

Hence the given that $i$ picks $a_1$, the probability $j$ picks $a_3$ or $a_4$ is 0.2

This analysis will help $i$ and $j$ choose a mixed strategy in zero-sum games

#### General Sum Games

This game contains elements of cooperation and competition.
This leads to negotiation.

#### General Sum Nash Equilibrium

- x* gives a higher expected value to $i$ than any other strategy when $j$ plays y*
- Similarly, y* gives a higher expected value to $j$ than any other strategy when $i$ plays x*




---
## Footnote

Backlink : [[AIN Outline]]

Source:

1. 
	- Name: lect07-2 Dominant Strategies.pdf.pdf
	- Author: Fredrik Mallmann-Trenn
	- Date: 17/11/22
2. 
	- Name: lect07-3 Nash Equilibirum.pdf.pdf
	- Author: Fredrik Mallmann-Trenn
	- Date: 17/11/22
3. 
	- Name: lect07-4 Pareto Optimality.pdf.pdf
	- Author: Fredrik Mallmann-Trenn
	- Date: 17/11/22
4. 
	- Name: lect07-5 Normal Form Games.pdf.pdf
	- Author: Fredrik Mallmann-Trenn
	- Date: 17/11/22
5. 
	- Name: lect07-6 Mixed Strategies.pdf.pdf
	- Author: Fredrik Mallmann-Trenn
	- Date: 17/11/22

