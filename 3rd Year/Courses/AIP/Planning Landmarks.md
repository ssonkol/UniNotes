---
sr-due: 2022-10-11
sr-interval: 1
sr-ease: 230
---

Tag: #review


# Planning Landmarks

### Planning Landmarks
- Landmarks are facts that must be true at some point in every valid solution to a problem
Example:
> If we were to consider the driver log domain, then all trucks need to visit the packages and in turn those packages need to be on a truck at some point in order for them to reach their destination.
> This is actually a useful means not just to estimate distance to goal, but can help decompose planning problems into smaller tasks that need to be solved.

We can then order these landmarks to dictate the order in which they should be achieved.

#### Three types of Landmarks
There are three types of Landmarks:
1. Fact Landmarks
	- A variable takes a particular value in at least one state
	>These are simply variables that need to hold a specific value in at least one state in the final plans execution
2. Action Landmarks
	- An action must be applied to the solution
3. Disjunction Action Landmark
	- One of a set of possible actions must be applied

#### How Do We Find Landmarks ?

We need to find good landmarks, given some will not be informative.
- The set of possible actions is technically a disjunctive action landmark
- Every variable that is true in the initial state is a fact landmark

Finding landmarks can be as hard as planning itself... So we can exploit the relaxed planning graph technique to generate landmarks

##### Finding Landmarks via Deletion Relaxation With RPG

The easiest way to generate landmarks, is to adopt the deletion relaxation once more.  Try removing a specific valid action from the if it adds a fact to the problem, generate the relaxed planning graph from there and if the goal no longer appears in a future fact layer, then we know the action was a landmark to the problem.

1. Delete Relaxation Landmarks
2. Iterate through all actions
	1. Remove action if it adds a fact to the planning problem
	2. Build the relaxed planning graph
	3. If the goal no longer appears in the RPG, then the action was a landmark of the problem

**This works... but it's slow to execute**

##### Finding Landmarks via Back-Chaining

In this instance we treat every goal as a Landmark and then analyse how these goals are satisfied.  Then find the actions that satisfy that goal, and what preconditions they all share.  If we have 3 actions that all have the same precondition A that generates that goal landmark B, then we know that the precondition A is a landmark.


1. Treat each goal (B) as a landmark, for each goal:
	1. Take intersection of preconditions of all actions that achieve goal (A)
	2. If numerous actions share A and achieve B, A is also a landmark;
	3. A is also ordered before (must be achieved before) the goal
2. Repeat for all landmarks found

#### **Finding Landmarks via RPG Propagation**

The third alternative is to use the RPG approach and pay attention to what facts hold true during the execution of a plan.

This propagation, whereby we take the union of preconditions of actions that achieve specific facts, helps us to establish what facts could be landmarks for the problem.

- Actions (numbers) take union over preconditions' labels (all are necessary)
- Facts (letters) take intersection of achievers' labels (at least one is necessary)
	- This gets rid of the false ones that aren't very important and leaves the critical labels that are essential to solving the problem

Think about your fact layers and action layers...

Steps:
1. Run RPG first
	1. Give Fact ad Action Layers
2. Remember that every fact is always labelled by itself
3. Use the RPG Propagation rules
	1. Finding Actions union preconditions
	2. Finding Facts intersection achiever's labels
4. Then find all the labels that apply to the actions and facts

#### Extracting Landmarks
We simply repeat the RPG Propagation process until the goals appear and once they have, we keep generating new action/fact layers until the labels no longer change.  At which point, we can then grab the goals in the final layer and check to see what fact layer unions are attached to them and voila, we have our fact landmarks, generated within polynomial time.

##### Landmark Orderings

Sound Ordering:

In sound orderings we know that A achieves B, but we just don’t know exactly when.  Hence we can have necessary ordering, where A is always true one step before B, **Greedy Necessary**, which is similar to necessary ordering, but this only applies the first time B comes true, rather than every time.  Natural ordering A is true, at some point?  Before B is.

- **Necessary Ordering**, $A ->n B: A$ is always true one step before B
- **Greedy-necessary Ordering**, $A->gn B : A$ is true one step before B is true for the first time
- **Natural Ordering**, $A -> B : A$ is true some of the time before B
![[Pasted image 20221007111517.png]][1]

Unsound Ordering (used in heuristics):

In Unsound orderings, we have special conditions on the orderings of landmarks.  Hence there is reasonable ordering, where if B was achieved before A, so the plan has to delete B to then achieve A and then re-achieve B possibly on the same time point.

- **Reasonable Ordering**, $A ->r B:$ If B was achieved before A then the plan should delete B to achieve A and re-achieve B after.
- **Obedient Reasonable Ordering**, $A - >or  B:$  If B was achieved before A then any plan that obeys reasonable orderings must delete B to achieve A and re-achieve B after.

## Questions


---
## Footnote

Backlink: [[Optimising Classical Planning]]

Sources:
1. 
	- Name: Improving Search 02 - RPG
	- Author: Amanda Coles