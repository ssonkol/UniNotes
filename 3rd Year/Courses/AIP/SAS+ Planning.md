# SAS+ Planning
Tag: #review 

---
## Definitions


## Notes
In this planning method, we adopt the intuition from finite-state variables into our planning process.

To do this we need to;
1. Encode the planning task as a Boolean Satisfiability problem (SAT), through use of the propositions we’ve seen earlier.
2. Introduce the FDR encodings transforming the SAT problem into a SAS+ Planning problem.


#### SAS+ Formally
An SAS+ planning task  is a 4-tuple $Π = <V, O, s_0, s^∗>$ with the following components:
- $V = {v_1, . . . , v_n}$
	- A set of state variables (or fluents) V, each with an associated finite domain $D_v$. 
	- If $d ∈ D_v$ we call the pair $v = d$ an atom.
- $O$ = a set of operators
	Where an operator is a triple <name, pre, eff>
	- Name of the operator
	- Pre and eff are partial variable assignments (preconditions and effects)
- $s_0$ is the initial state, and s* is a partial assignment of atoms representing the goal.

#### Operators (Actions)
Actions look a little different under SAS+:
- Two sorts of conditions roll PDDL preconditions and effects together

**Prevail Conditions**
- Variable = Value that stays the same
- When loading a package p1 onto a truck t1 at location l1: <t1, at-l1, in-t1>

**Pre_post Conditions**
- The value of a variable changes from one value to another:
- When loading a package p1 onto a truck t1 at location l1: <p1,at-l1,in-t1>

#### Domain Transition Graphs (DTG)
- Domain: One for each variable, referring to its domain
- Transition: pre_post conditions of operators change the values of a variable;
- Graph: Transitions in the domain form a directed graph.


- Nodes:
	- The domain values
- Edges:
- An edge exists from A ->B if an operator exists with a pre_post condition <v, A, B>

![[Pasted image 20221015172821.png]][1]

Example:

A domain where a truck can drive around on land but also use a ferry to move between locations where plausible.

Actions:
- PDDL action: drive ?truck ?a ?b
	- First or all we have a drive action, that moves a truck from A to B.
	- Analysis will detect truck can only be in once place at once.
- Load the truck onto the ferry action: 
	- board-ferry ?truck ?ferry ?p
	- Deletes (at ?truck ?p) but gives (on ?ferry ?truck).
- Disembark from ferry

Now by encoding this as a SAS+ planning problem, we can observe numerous constraints on the problem.  First of all that the truck can only be in once place at once, which will be inferred from the action to drive the truck.

But also that getting on and off the ferry influences where the truck is as well.  As such, entire problem can be reduced to one variable: where the truck is and the domain captures all possible locations.

![[Pasted image 20221015173241.png]][1]



It’s just one variable, where is the truck?  And the edges of the graph are drive or load/unload actions that change that value.

Given you’ll notice there are specific locations, which are the letters and then of course there is the ferry, which is clearly noted here. Of course the ferry can only be achieved if that is a valid action when the variable is assigned to either D or C.

But in essence, we can see that this entire planning problem is one variable which has 8 possible values:

B, C, D, E, G, L, P or Ferry.

If we put this on a map, we get
![[Pasted image 20221015173400.png]][1]


#### Cons of SAS Planning

- It can only be used in very specific contexts 
	- Conditional effects are not possible

## Questions

---
## Footnote

Backlink: [[Optimal Planning]]

Source:
1. 
	- Name: Optimal Planning 1 - SAS Planning.pptx
	- Author: Tommy Thompson
	- Date: 15/10/22
2. 
	- Name: Optimal Planning 2 - Pattern Databses.pptx
	- Author: Tommy Thompson
	- Date: 15/10/22
3. 
	- Name: Optimal Planning 3 - Cost Partitioning.pptx
	- Author: Tommy Thompson
	- Date: 15/10/22


