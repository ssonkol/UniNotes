---
sr-due: 2023-01-13
sr-interval: 74
sr-ease: 270
---

Tags: #review


# Classical Planning Fundamentals


When trying to formulate a planning problem, we need to make sure that we encapsulate all of the knowledge required to express any possible permutation of a problem - essentially the domain - and any individual problems that may arise themselves. 

Then we need to put this in the PDDL language so that planning systems can look for a solution.

Thinking of Forward, Breadth or Depth First Search allow us to explore the search space but this isn't effective...

What we really want to do is prioritise things within the open list on some criteria - which is where [[Heuristics]] may come in to search the state space faster.

To achieve the best search process we need 3 key features:
- **Admissible**
	This is where the heuristic never overestimates the cost of reaching the goal from a given destination. It either underestimates or - in the worst case - calculates exactly how far away we are from the goal
- **Consistent**
	For any child state, the heuristic value will be equivalent to the parent's heuristic value minus the cost it took us to reach it
	> ![[Pasted image 20221002124728.png]]
- **Additive** 
	Where two heuristics $h1$ and $h2$ are additive, if they and a third heuristic, which is the summation of the two are all admissible
	>![[Pasted image 20221002124842.png]]

However there are some questions which may arise...

- How do we build a heuristic for a given domain or problem?
	- Especially if using a planning system that relies on PDDL, where we're not going to be giving it this information.
		- We just give the domain and problem notation
- How can we search more effectively in the state space?
	- All the heuristic search systems we've seen work fine, but there are larger and complex problem spaces. So we need to find a way to further optimise our search process.
	- How do we build more effective heuristics that help us better search the state space?
	- Can we build heuristics that help not just prioritise states on the path to the goal, but also help us search the problem more efficiently


## Questions


---
## Footnote

Backlink: [[Optimising Classical Planning]]

Sources:
1. 
	- Name: Improving Search 02 - RPG
	- Author: Amanda Coles