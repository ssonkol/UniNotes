---
sr-due: 2022-11-03
sr-interval: 3
sr-ease: 250
---

 links: [[AI]], [[AIP]], [[Uni Courses]]

tags:   #flashcards #review #University #School

---

# Introduction to Planning

## Notes
---
- General Planning
- Formal Planning

#### General Planning
In planning problems we have:
- An initial state - Also known as 'I'
	- This describes a location
		- Words like; at, path and link

- A goal - Also known as 'G'
	- This describes a location
		- Words like; at, path and link

- Some Actions that are defined according to a domain - Also known as 'A'
	- This describes an action to do
		- Words like; load, walk, enter and drive

A planner takes these actions and gives us a plan.

Examples:
>- An ordered sequence of actions from A that will turn I into G
>
>- What to do; and when to do it
>
>- Performs search to consider the different possible plans available, until a plan from I to G is found

#### Formal Planning
A classical ([[STRIPS]]) planning problem is a tuple <P,A,I,G>

![[Pasted image 20220906174112.png]] [1]

This translates to:
1. My DVD is at Amazon
2. The delivery truck is at amazon
3. The driver is at home
4. The driver sets a path from their home to amazon
5. The driver in the truck drives from amazon to London
6. The driver then once in London, continues to drive to my house
7. Resulting in myDVD being delivered

#### Planning as Forward Search

We can also use something known as Search Spaces

These are nodes that describe a certain state. From here, with each action, a new state is generated.

As shown below: 
![[Pasted image 20220906180028.png]] [2]

![[Pasted image 20220906180117.png]]
*Note that walk then load is the same as load then walk!

![[Pasted image 20220906180223.png]][2]

Remember, don't go round in circles!
- Keep a closed list where all states have been seen before
- When expanding a state, **Ignore successors on the closed list**
![[Pasted image 20220906180419.png]] [2]
turns into...
![[Pasted image 20220906180454.png]] [2]

Since the search space is a Directed Graph a [[Forward Search]] from the initial state, with a closed list, builds a [[Tree]].

Hence only one path into each node is kept and there are no backwards edges.

But we can expand into so many other options...

If we had an open list,
1. we could set it up as a queue, which allows a **Breadth-first search** method.
	This way we can;
	- Generate all children of the current node
	- Expand nodes in the order they were generated
2. We could set it up as a stack, which allows a **Depth-first search** method.
	This way we can;
	- Generate all children of the current node
	- If it has children, select and expand its first child
	- If not, backtrack to the most recent node with unexpanded children


However this can all take a very long time since planning is P-Space hard.
Therefore we need to find a way to search through only the most promising looking plans.

That's what brings in the [[Heuristic Search]].

#### The Scanalyzer Domain

![[Pasted image 20220906184659.png]] [4]

Scanalyzers can be broken down into:
- **Segments**
- **Batches**
- **Predicates**

Example:
>Given a factory line that sorts plants:
>- Segments - Type of conveyor belts
>- Batches - Type of plants 
>- Predicates:
>	- A batch of plants is on a given segment
>	- A batch of plants has been analysed
>	- Segments are linked together in cycles


##### Scanalyzer: Initial State
![[Pasted image 20220906185057.png]] [4]

##### Scanalyzer: Actions in PDDL

![[Pasted image 20220906185155.png]] 
![[Pasted image 20220906185218.png]] [4]

##### Scanalyzer: Goal

 ![[Pasted image 20220906185258.png]][4]

---
## Questions
---
##### Question 1  
How might one encode this in PDDL? 

Initial state: Right door is open; standing in 1st room
Goal: Standing in third room 

- Right door open (knows rules)
- In First Room (nostranger tolove)
- Goal of standing in right room (so do I)
- Actions for buttons: Gonna & Give
- To move, Never & YouUp

![[Pasted image 20220906175237.png]] [1]

##### Question 2 
2. Assume you have a function h(S) that gives us a 'distance to go' from the state S to the goal:
	- For goal states, h(S) = 0
	- For other states, h(S) > 0 
	What if h(S) is admissible and consistent?
	*Note:
	- *Admissible - never overestimates the distance to a goal state
	- *Consistent (monotonic) - h(S) <= h(S') + d(S, S')*
[2]
###### Answer 2:
> At any point, the smallest f(S) on the open list underestimates (<=) the shortest possible plan that can solve the problem.
> 	Proof: g(S) is perfect, so it doesn't overestimate the distance from I to S; h(S) doesn't overestimate; so adding them together will never produce an overestimate

##### Question 3
3. What if we find a goal state but put it on the open list, and wait until it is expanded?
[2]
###### Answer 3:
>We have found the shortest possible plan.
>	Proof by contradiction: The search expands a state with the smallest f(S); if there was a shorter path to a goal state S', f(S') would be less than f(S), and it would have been expanded first.
>	Consistency guarantees that there is no node that has not yet been put on the open list that might have a shorter path than the one that is there...

##### Question 4
4. What if we want a plan that is 'good' quality but not necessarily optimal?
[2]
###### Answer 4:
>- f(S) = g(s) + W*h(s);
>- W is a constant that gives an optimality bound.
>- Now the solution we find will be within a factor W of optimal
>- Find a solution faster by biasing search towards nodes closer to the goal
>	Advantages:
>		- You don't have to explore as much of the search space to find a solution
>		- Still have some guarantee of the solution being a reasonable one.

---
## Footnote
---
Backlink: [[Artificial Intelligence Planning Outline]]

Reference:
1. 
	- Source: Planning Basics 01- What is Planning.ppt
	- Author: Amanda Coles
	- Accessed: 06/09/22
2. 
	- Source: Planning Basics 02- Planning As Forward Search.ppt
	- Author: Amanda Coles
	- Accessed: 06/09/22
3. 
	- Source: Planning Basics 03- Heuristic Search.ppt
	- Author: Amanda Coles
	- Accessed: 06/09/22
4. 
	- Source: Planning Basics - 04 - PDDL Modelling Application Example Scanalyzer Domain.ppt
	- Author: Amanda Coles
	- Accessed: 06/09/22