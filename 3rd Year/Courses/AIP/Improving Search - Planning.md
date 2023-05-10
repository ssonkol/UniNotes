---
sr-due: 2022-11-30
sr-interval: 30
sr-ease: 250
---

Tags: #review

# Improving Search - Planning


## Problem Relaxation and Relaxed Planning (RPG Heuristic)
#### Domain Independent Heuristics

The problems with these heuristics is that:

- They are uninformative about the problem
- They ignore a lot of the problem structure

#### Valid Solutions
Establishing valid solutions on a planning problem is hard

- Calculating whether a planning distance has any valid solutions exists within PSpace-complete and optimal planning is NP-Hard to compute
- We also need a polynomial time heuristic - given we are going to use is a lot

### Why RPG is better
Which is why Relaxed Plan Heuristics are a great way to achieve Relaxed Planning.
- This is where we create a simpler - relaxed - version of the problem that removes some of the constraints.
- We then solve the relaxed version of the problem from this state and this gives us an estimate of goal distance.
- This creates a domain-independent heuristic for any given problem.

Relaxed planning is based on the principle of delete relaxation... 
If we think about the type of effects we can have, we only have two:

- Add effects - Where we add new information to the state
- Delete effects - Where we remove information from the world state
	- This in turn means the fact is no longer considered

##### How does it apply to Heuristics

Since relaxed planning creates relaxed plans we can adopt this as a heuristic...

We do this by
- Evaluating any given state in our planning problem by solving the relaxed problem
	- Generate a relaxed plan from that state
- Use the cost of the relaxed plan as a heuristic value for that state
	- $h(S) =$ cost(actions) of the relaxed plan

Considering that we have generated the optimal relaxed plan, then this will provide us with an admissible heuristic

Example:

Considering the BlocksWorld problem: 
![[Pasted image 20221003185343.png]][1]
**Initial State **                                                                                               Goal State

If we want to create an RPG value we first need a ==**fact layer**==
This will include all the information that is true at the current point in time with respect to the problem

![[Pasted image 20221003185752.png]][1]

The first fact layer - *layer 0* - only has the facts that are true of the current state.
(The above example also includes facts that are not true, but these will not usually be in the fact layer - these are the ones noted in red)

![[Pasted image 20221003190002.png]][1]

Then we have the first action layer and all of its valid actions that can exist at this point in time
Therefore you can:
- Move C onto the table T
- Move C onto B
- Move B onto C

![[Pasted image 20221003190152.png]][1]

Now that we have all of these, actions, we can generate the 2nd fact layer. 
Since we are using delete relaxation, we apply the add effects to the new layer - but we don't apply the delete effects.

Given that the delete effects aren't applied, all of these facts are true in the fact layer (despite this being impossible for all three of them to be true at the same time)

![[Pasted image 20221003190504.png]][1]

This now generates our final fact layer. What we should note is that all three facts that we expect to see in our goal state are true - Hence we have reached a fact layer where all facts relating to the goal are true. Now we can work backwards to create a solution. 

#### Extracting a Solution

![[Pasted image 20221003191356.png]][1]
Given all facts are true the process of extracting the RP solution; we look at the preceding layer and whether a fact at layer $n$ existed in layer $n-1$ .

If it did, we add it $g(n-1)$. If it doesn't, we choose an action from the intermediate fact layer and add its preconditions to the $g(n-1)$.

We do this until we get to $g(0)$

![[Pasted image 20221003191434.png]][1]
So we need to two facts where A on B and B on C are true.
If we then look at the preceding fact layer, B on C is satisfied, but A on B is not, then we need to find the action that achieves it - in this case move A from the table onto B

![[Pasted image 20221003191638.png]] [1]
Next we have to factor not just the last remaining goal fact - B on C - but also the precondition to move A onto B action, which is that B is clear. The we add that action to the relaxed plan solution.

![[Pasted image 20221003191805.png]][1]

So we then can identify the two actions that achieve On BC. Which is moving B onto C as well as moving C onto the table.

This satisfies both of these facts in $g(n-1)$. The preconditions for moving C onto the table are already satisfied in fact layer $g(n-1)$. The only outstanding fact is whether B is clear, which is satisfied in $g(n-2)$. This means we have found a relaxed solution, with two actions set.

##### Summary
In summary...
- A good way to come up with heuristics is to solve a simplified version of the problem
- Using Delete Relaxation by discarding all delete effects, provides simplification that can be explored by using greedy search in polynomial time.
- Delete Relaxation always creates simplifications, hence problems are always easier to solve than the original.
- RPG layers provide admissible heuristics to relaxed problems
	- But note that the relaxed plan length is not

## Domain Independent Planning : FF

FF is a forward-chaining heuristic search-based planner.
It uses the RPG heuristic to guide search;
- This involves finding a plan from the current state S which achieves the goals G but ignores the delete effects of each action
- The length of this plan is used as a heuristic value for the state S

This means FF uses both local and systematic search
- Enforced Hill-Climbing (EHC)
	- Upon termination, EHC either outputs a solution plan or reports that it has failed
	- If EHC fails, best-first search is invoked

###### EHC
Enforced Hill Climbing runs on the idea that it will always seek the best possible improvement in the current state heuristic value

The basic Idea is that the lower the heuristic, the better
- It will always try and find states with the best heuristic value seen so far:
	- Start with $Best = h(S,init)$ and aim to get to $best =0$

1. Expand a state S
2. If we have a successor S' with $h(S')<best$:
	1. $S=S'$
	2. Return to step 1
3. If no state is found
	1. Breadth-first search until one is found;
	2. return to Step 1

###### EHC in practice
![[Pasted image 20221003195624.png]][1]
If we start with this first state with a value of 9, it will then find the next child state with a better value, hence this one here with eight. But then it has a problem...
It can’t find one with a better value...

This is what is known as a **plateau**. Given no states in proximity appear to be better than where we currently are in the search space.  So it runs breadth-first search until it finds this state with a  value of 7 a few layers down.  Then resumes as normal.

Interestingly, there is an interesting issue here, in that it is possible that this particular path doesn’t yield the desired outcome and that actually the goal state exists in the other subtree that we omitted right at the beginning…

- **EHC can sometimes fail to find a solution as the RPG heuristic can lead it down dead ends**
- **When EHC fails, FF resorts to systematic best-first search from the initial state**
	- FF maintains a priority queue of states (the state with the lowest $h(s)$ value is stored first)
	- The front state in the queue is expanded each time
	- The successors are added to the queue, and so on
- **Searching on a Plateau is expensive**
	- Systematic search is carried out on the part where the heuristic is worst

###### EHC Pros & Cons

**Pro**

- **EHC is fast**
	- Greedy algorithm takes better states when found therefore it can find solutions quickly
- **FF is complete**
	- If EHC fails, then start again from the initial state using best-first search
	- It may be slower but it is complete...


**Cons**

- **EHC is incomplete**
	- If a situation arose where the solution was actually down one of the paths we discarded or never generated because another state looked better
- **Sometimes can fail to find a solution**
	- The heuristic can lead it to dead ends
- **If FF fails, resorts to systematic best-first search from the start**
	- Priority queue of states (lowest $h(s)$ first)
	- Expand the next state each time
	- Add successors to the queue, and loop
- **Searching on Plateaux is expensive**
	- Systematic search on the part where the heuristic is worst


### Heuristic Cons

1. RPG is not perfect
	1. Few are, otherwise the problem would be easy
		1. The heuristic would be very expensive to compute
2. Making the right move doesn't always lower the heuristic value:
	1. It can stay the same; or,
	2. It can go higher
3. The move with the best heuristic value can be a really bad decision
	1. With local search (mentioned in [[Dual Heuristics]]), this can lead to no solution being found.

---
## Footnote

Backlink: [[Optimising Classical Planning]]

Sources:
1. 
	- Name: Improving Search 02 - RPG
	- Author: Amanda Coles