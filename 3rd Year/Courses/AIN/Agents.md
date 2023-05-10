Tags: #review #flashcards #School #University #Courses #Outline #AI #Agent
Links: [[Uni Courses]], [[AI]]

---
# Agents

**Agents are robots( think of them as an [[Object]] in OOP) without any of the hardware**.

>This essentially means that it may or may not do what it is programmed to do due to it's autonomy.

### Intelligent Agents

For an Agent to be intelligent, it must talk about: 
- Its environment (where it is situated) 
- Its sensors (how it perceives the environment)
- Its effectors or actuators (how it acts upon the environment)

#### Constraints

Every AI has constraints on its decisions. These include;

- [[Option Uncertainty]]
- [[Incommensurability]]
- Outcome Uncertainty
- Resource Constraints
- Time Constraints 


### Rational Agents

A rational agent is an agent acting in the real world under resource constraints.

The problem in AI is knowing the right thing to do...
It sounds easy but in practice they need to be able to;
- Identify the alternatives
- Decide which alternative will lead to the best outcome
- Perform the decision quickly enough for it to be useful

#### An Ideal Rational Agent
 This type of agent will act to maximise its expected performance measure based on the information provided by the sequence of precepts, together with any information/rules built into the agent.

But this isn't anywhere close to perfect...

We need to think about the Agent's:

- [[Actions]]
- [[Environments]]
	- [[Agents In An Environment]]

### Agents and Goals

An agent may have conflicting goals from time to time, or even many different ways of achieving the same goal.
- These different means may have different costs & benefits, and different consequences.
- They may have different likelihoods of being successful.


## Questions
#### Intro Questions
Some questions to think about: 

- **Is a cat an agent ?**

> I would think no since it is not programmed or instructed to do anything, although it has full autonomy over itself and may or may not do what it is programmed to do

- **Is a dog an agent ?**

> This is the same as a cat. It depends on who we say is the programmer/instructor and possibly the nature of the [[Object]] (in this case, animal)

- **Is a light-switch an agent ?**

> I wouldn't say so, since a light switch is binary - on or off. The only time it doesn't do what is expected is when it has a bug.

#### Question 1
Given a simple vacuum cleaner with;
- 2 sensors:
	- Location (Room A or B)
	- Dirty? (Yes or No)
- 3 Actions:
	- Suck-up-dirt
	- Move-Right
	- Move-Left

Can you make a list of rules of the form:
If *condition* then *action*
to control this simple vacuum cleaning agent.
![[Pasted image 20220908193637.png]] [1]

###### Answer
>if *dirty = Yes* then *Suck-up-dirt*
>else if *Location = A* then *Move-Right*
>else if *Location = B* then *Move-Left*

---

## Footnote

References :
1. 
	-  Name: 6CCS3AIN 2021-2022 Part A Introduction - McBurney - PDF
	- Accessed: 03/09/2022


Backlinks: [[AIN]]