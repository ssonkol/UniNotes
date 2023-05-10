---
sr-due: 2022-10-13
sr-interval: 3
sr-ease: 250
---

Tag: #review #OptionUncertainty #Courses

# Landmark Counting

### Landmark Counting (and LAMA)

- This is where we have landmarks for a given problem, we can estimate the goal distance by counting how many landmarks we have yet to solve for that problem.

##### Landmarks as Sub-goals

We can use landmarks as sub-goals by creating a plan from one set of landmarks, and repeating this till all landmarks are satisfied.

This is done by;
1. Give some landmarks a partial ordering on them
2. Set the goal to the first landmark (S), according to the landmark graph - then find a plan
3. Now update the initial state, and plan to the next landmarks


**Pros**
- Planning can be very fast given the planner has a lot less work to do, since landmarks solve so many elements for us

**Cons**
- It can lead to poor-quality plans
	- Sometimes landmarks need to be undone and achieved again if tackled in the wrong order
- Incomplete problems with dead ends


##### Landmarks as Heuristics

LM-Count is a path-dependent heuristic.
Unlike other heuristics, LM-Count cannot be derived solely from looking at the state and calculating the value.

Achieved landmarks are a function of the path taken, not an observation of the state

To compute LM-Count:

- $H(s,p) = ({L}-{Accepted(s,p)}) \cup ReqAgain(s,p)$
- $L$: size of the set of all landmarks discovered for the problem
- $Accepted(s,p)$: Accepted landmarks
	- A landmark is accepted if it's true in s and all its predecessors in the landmark graph are accepted
- $ReqAgain(s,p)$: Landmarks that we've seen but know we need to see again
	- $L$ is required again if:
		- Landmarks is false and it is a goal
		- Landmarks is false in s and is a greedy-necessary predecessor of a landmark $m$ (must be true the step before $m$), which is not accepted

**Cons**
- LM-Count is inadmissible given one action could satisfy more than one landmark.




## Questions


---
## Footnote

Backlink: [[Optimising Classical Planning]]

Sources:
1. 
	- Name: Improving Search 02 - RPG
	- Author: Amanda Coles