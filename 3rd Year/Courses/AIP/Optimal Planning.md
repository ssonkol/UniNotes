# Optimal Planning
Tag: #review 

---
## Definitions
**Invariant**
> This is a logical formula $\phi$ that are true in all reachable states.
## Notes

A common problem is that, as problems begin to increase in complexity, the state spaces are exploding in scale accordingly.

We can try;
- Using heuristics, which help direct us through the space,
- Using landmarks that point out good intermediate goals to try and complete.
- Using FF and Identidem planners, we’re using variations of Enforce Hill Climbing – only how they handle local minima or plateau’s is really what is changing

But in each case we’re now being much more aggressive when searching the space – often ignoring other opportunities.

In each case, we’re sacrificing the completeness of the search: we may use inadmissible heuristics that prevent us from ever visiting a state, landmarks prune areas of the state space given we’re focussed on reaching them

### Invariants

Even though we as humans implicitly make use of 'obvious' properties and relationships between propositions to plan tasks. We still need to ensure PDDL captures this

#### Finding Invariants

Theoretically, testing whether an invariant is valid is as hard as planning itself.
- But, if we can find invariants and encode it in a way a planner can understand, we could potentially reduce the state space.  
- Even finding ‘obvious’  invariants could drastically improve our performance in solving the planning task.

##### Mutual Exclusion

**Mutual Exclusion (mutex)** is an invariant over a set of propositions where only proposition can be true at any given point of time.

Hence if we return to my example from earlier, being at the university and being at home is a mutex.  Because only one of those two propositions will be true in any given state.

###### Example
Let's take a look at this with the BlocksWorld example.
![[Pasted image 20221015170713.png]][1]
BlocksWorld Invariant:
$¬(ConA) ⋁ ¬ (ConB)$
aka $ConA$ or $ConB$ are mutex

But also
{$AonB, ConB,Bclear$} is mutex because every pair in this set are mutex

Now If we enumerate all of the unique subsets, we have three combinations:

A is on B and C is on B
A is on B and B is clear
C is on B and B is clear.

In each case, the pair of propositions is also mutex.  It’s impossible for C to be on B and A to be on B at the same time.
Plus if either A or C are on B, it’s impossible for B to be clear, because, y’know, there’s something sitting  on top of it.

### Finite-Domain State Variables

- We can use literals to reframe a problem using Finite-Domain State Variables
	- We create a variable $v$ AND A DOMAIN $dom(v)$ that expresses the range of possible values that can be assigned to $v$
		$s(v) \in dom(v) ∀ v \in V$

Taking another look at BlocksWorld using what we know now:

below-a: {b, c, table} = b
below-b: {a, c, table} = table
below-c: {a, b, table} = table
![[Pasted image 20221015171413.png]][1]

If we establish a different encoding, where we also model all of the blocks that are above A, B and C, we have successfully encapsulated all the information about the state that we needed.

So in this case, above-a, encodes the mutex of {B-on-A, C-on-A and A-clear).
As a result, while we have increased the total number of unique configurations from 27 to 216, this is significantly less than the original 4096 states we calculated earlier.

#### Finite Domain Formula

Given the Finite-Domain Representation (FDR) encoding, this is valuable because we can translate it back to the normal propositions, but safely encapsulating the mutex relationships we have discovered.

E.g.
$(above-a = nothing) ⋁ ¬( below-b = c)$

corresponds to 
(A-clear) ⋁ ¬(B-on-C)


Now that we know this, we can put it to use in;
- [[SAS+ Planning]]
- [[Pattern Databases]]
- [[Cost Partitioning]]

## Questions

---
## Footnote

Backlink: [[Artificial Intelligence Planning Outline]]

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

