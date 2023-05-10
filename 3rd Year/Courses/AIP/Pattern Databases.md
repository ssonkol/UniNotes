# Pattern Databases
Tag: #review 

---
## Definitions

## Notes

If we know planning is hard and expensive, we want to find a way to speed up our exploration of the search space

To achieve this.. we need to Store solution costs for sub-problems within the search space.

In other words...
>**what if we can establish to cost of solutions to problems that are subsets of the current problem?**
>If we can calculate these subproblem heuristics, they will provide us with a very fast means to calculate during search of the main problem what the heuristic value is.


This is because solution costs to sub-problems will provide an admissible heuristic to solve the actual problem. Furthermore heuristic calculations become very fast.

This is because searching backwards from the goal, record costs of states. An expensive but one-time calculation.

**Example:**
Let’s consider the 8-puzzle problem, whereby we have a group of tiles, numbered one through 8 and the idea is that we use the one available empty slot to slide one tile at a time.

Over time we’re going to solve this problem by moving the tiles around such that they are ordered 1 through 8 in sequence from top to bottom.

![[Pasted image 20221015180344.png]][1]

If we were to ignore some of the tiles, it becomes an easier problem to solve.  By removing numbers 5 through 8 and simply acknowledging them as any number, then we can calculate a solution that ensure 1-4 are in the correct position, but the rest of it doesn’t really matter. 

Now if we were to calculate the solution to this problem, the actual cost of the solution – in this case the number of moves made –will be either less than or the equal to the number of moves required to achieve in the optimal solution in the original problem.  In a similar way to delete relaxations, we’re creating a variation of the search space that is guaranteed to produce an easier problem to solve.

![[Pasted image 20221015180456.png]][1]

So ultimately, solving a sub-problem optimally will always produce an admissible heuristic to the original problem.

#### Patterns
The above example is known as a pattern:
> A partial specification of a given state in the problem.  

Once we have all the target patterns for our problem we then calculate the pattern cost: which is going to be the minimum number of actions to achieve the target pattern.

This all sounds fine in theory, but it introduces a bunch of problems:
1. How do we search through a state space where each state is only a partial specification?
2. How do you then compute the distance to the target pattern?  

##### Pattern Discovery
- Search the abstraction of the state space
- Search is achieved using breath-first-search, moving backwards from the goal state.
	- Actions applied are the inverse of the original
- Pattern cost = search-tree depth from $s_{goal}$ to $s_{init}$

In layman's terms:
> We will generate a target pattern - think of it as a function - and when we apply that to the state space it creates what is known as an abstraction of the state space.  It’s going to group states together such that the overall number of states is now smaller and faster to search through.
> We can then search through the abstract state space, by using breadth first search backwards from the goal state.  Applying the actions in reverse, and once we reach the initial state, we can calculate how many actions are applied in the abstract state space and that’s our pattern cost.  One of the reasons we go backwards from the goal state, is that we’re actually going to have a much smaller search tree thanks to the abstraction. 

###### Abstractions

- Pattern discovery explores the abstract state space
- Our target patterns exist within the abstract state space
- Hence, we only care about specific values in any given state, so the number of unique states is now smaller

Mathematically, it looks like this....

- Function $α(S)=S′$ applied on a state $S$, transforming it into abstract state $S’$
	- The function helps to remove distinctions between states in the abstract space
		- Hence this may result in $α(S_1)=α(S_2)$
- The Maps state space is made into a smaller state space
	- In an abstract state transition system. similar states are now indistinguishable
- Hence the Abstraction Heuristic estimate is cost-to-goal in the abstract transition system.

Example:

![[Pasted image 20221015181631.png]][1]
Here we have a simple driver log problem of two trucks and one package.
The labels have been reduced to three letters, which correspond to the package, truck A and truck B.

The trucks can only be in two locations: location L and location R.
Meanwhile the package can be in locations L and R or it can be in trucks A and B.

So if we read this diagram from the left hand side, our initial state is that the package is in Location L and both trucks A and B are in location R. Meanwhile the goal states on the far right highlighted in green, say that the package is in Location R.

And if we look across the graph, what we are seeing is all the different paths that can arise when the trucks drive over to L, put the package on them and drive over to R and then unload them.

![[Pasted image 20221015181739.png]][1]

By applying the abstraction to only consider the location of the package, we abstract the entire state space into four states.

We can see the groups are predicated on whether the package (which again in the state is the symbol to the far left) is either L, A, B or R.

Hence now the transitions in the abstract state space, are either to the same abstract state or to another abstract state.  Hence in this case, our target pattern is the abstract state on the right hand, which is to have the package at location R.  But it’s actually an abstract state comprised of four different state.

And with this, we can search back and count that it’s only two actions required to get us from the abstract state which represents the initial state to the goal.

Hence our heuristic value is only two in this case.

#### Planning with Pattern Databases
- Create a set of all state propositions in mutex groups
	- These are the variables we're interested in
- Construct the abstract problem space(s)
- Construct the Pattern Database
- Run the planning process from the initial state

We then use breadth forward search from the goal state to search for solutions in the abstract state spaces and construct our pattern database.  And of course thanks to the abstractions the state spaces are exponentially smaller and easier to maintain.

Example:

Returning to the BlocksWorld problem again...![[Pasted image 20221015182314.png]][1]

We generate our mutex groups using SAS+ encoding of the problem space.![[Pasted image 20221015182419.png]][1]

Next we split them into groups![[Pasted image 20221015182446.png]][1]


Next we split the goals as well.
For a the even goal which is (on c a), we then generate all the heuristic values for all combinations of facts across those sets with respect to that goal. 

So in the case of the even goal (on, c a), there’s not that many non-mutex pairings here that we can consider as possible patterns.  So the list is quite short, and working back from the goal state it’s not as hard. 

However, in the case of the odd goals, (on a b) and (on a c), the number of combinations of facts generating new patterns is quite large.  Hence we have a much larger number of possible patterns and their corresponding heuristic values.![[Pasted image 20221015182505.png]][1]

#### Pros & Cons of Pattern Databases

###### Pros
- Heuristic calculations are now constant time (it’s a lookup function).
- Reusable when solving the same problem.

###### Cons
- Slow computation time to build the pattern database.
- Reusability is quite limited (changing goal or increasing variables etc.)


## Questions

---
## Footnote

Backlink: [[Optimal Planning]]

Source:
1. 
	- Name: Optimal Planning 2 - Pattern Databses.pptx
	- Author: Tommy Thompson
	- Date: 15/10/22
2. 
	- Name: Optimal Planning 3 - Cost Partitioning.pptx
	- Author: Tommy Thompson
	- Date: 15/10/22
