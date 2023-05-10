# Non-Forward Planning

---
## Definitions

## Notes

### GraphPlan
This is where you construct a graph that encodes constraints on possible plans

- The planning graph constraints search to a valid plan
	- Finds the shortest plans
	- Will search backwards from the end of the graph to the initial state

This means:
- Graphs can be built fairly quickly
	- Since graphs are built in polynomial time
	- Will terminate with failure if there is no plan

Given the example:

In the rocket domain problem, we have a rocket  which we wish to load packages to and send to space.

Literals:
- $at X Y$: X is at location Y
- $fuelR$: rocket R has fuel
- $inXR$: X is in rocket R

Actions:
- $loadXL$: Load X (onto R) at location L(X and R must be at L)
- $unloadXL$: unload X(from R) at location L (R must be at L)
- $moveXY$: move rocket R from X to Y (R must be at L and have fuel)

Graph representation:
- Solid black lines: preconditions/effects
- Dotted red lines: negated preconditions/effects

![[Pasted image 20221018150722.png]][1]


So we build out our graph in the same way we did RPG but in this case we use the red lines to negate the actions and facts which are no longer possible.
![[Pasted image 20221018151002.png]][1]

As you can see... there are actions and facts here that are physically not possible...

![[Pasted image 20221018151434.png]][1]
You can't load things onto P whilst P is moving..

![[Pasted image 20221018151533.png]][1]

##### Valid Plans
Now for the GraphPlan to work we need to make sure the plans are valid.

For a plan to be valid:
- Actions at the same level don't interfere with one another
- Each action's preconditions are true at that point in the plan
- Goals are satisfied at the end of the graph

This is where we use **mutexes**:
- This is where two actions or literals are mutually exclusive if no valid plan could obtain both

##### Basic GraphPlan Algorithm
1. Grow the planning graph until all goals are reachable and none are pairwise mutex
2. Search backwards from the max fact layer for a valid plan
3. If none found
	1. Add a level to the planning graph and try again

###### Plan Generation
1. Backward chain on the planning graph
2. At level $i$, pick a non-mutex subset of actions that achieve the goals at level $i+1$
	1. The preconditions of these actions become the goals at level $i$
3. Build the action subset by iterating over goals, choosing an action that has the goal as an effect
	1. Use an action that was already selected if possible. Do forward checking on remaining goals

![[Pasted image 20221018152408.png]][1]

### SAT Planning

##### Boolean Satisfiability Problems(SAT)
This is a form of deductive reasoning where we attempt to encode a problem into a Boolean expression.

If we can find a valid combination of values for this expression, we can consider the SAT problem to be satisfiable.

We usually try to put it into this format...

**Problem** : our planning formulation $\rho = (\sum , S_{i}, g)$

**Idea**: Propositional variables for each state variable 
- Create unit clauses that specify
	- The initial state
	- The goal state

**Solution**: Create a SAT formula $\phi$ such that...
- If $\phi$ is satisfiable, then a plan exists for the planning problem $\rho$
- Every possible solution for $\phi$ results in a different valid plan for $\rho$

###### SAT Encoding: Variables

1. State Variables
	- A set of propositional variables $v^i$ that encode the state after $i$ steps of the plan
	- There is a finite number of steps of the plan, encoding as T: the planning horizon
		![[Pasted image 20221018153457.png]][2]
2. Action Variables
	- A set of propositional variables $a^i$ that encode the actions applied at the $i^{th}$ step of the plan

###### SAT Encoding: Actions

For all actions that exist in the domain, we need to encode the preconditions and the add and delete effects of the action.

But we need to do it for each time step $i$ for the planning horizon T
Sub formulas for encoding preconditions, add/delete effects.

![[Pasted image 20221018154543.png]][2]

###### State Variables
Using our planning formulation 
$\rho = (\sum , S_{i}, g)$

Encode our initial states using the initial state propositions
![[Pasted image 20221018153750.png]][1]

Encode our goal states
![[Pasted image 20221018153838.png]][1]

Note that horizon point T is an estimate of our goal distance

In this case set T=1

##### Problem Example - 

Given the gripper example:
- Take a box in one room to another.
	- The gripper will grab the box.
![[Pasted image 20221018154254.png]][2]
{at(r1,locA), at(b1,locA), free(left), free(right)}

T=1

**Initial State**
![[Pasted image 20221018154152.png]][2]

We need to capture all the facts that are true and all the facts that are not true in this state, given information moves from one state to another.

**Goal state**

at(b1,locB,1)

###### Actions
- Gripper Actions
![[Pasted image 20221018154738.png]][2]

- Sat Encoding
![[Pasted image 20221018154808.png]][2]

###### Framing Problem
- We need a way to capture information that does not change between time steps $i$ and $i+1$

There are two approaches to solve this...
- **Classical Frame Axioms** (*this is not focused on in the module*)
	- State which facts are not effected for each actions
	- Must enumerate for all/action pairs where the number of facts is not affected by the action
	- Relies on one action being executed per time-step so axioms can be applied
- **Explanatory Frame Axioms**
	- Instead of listing what facts are not changed, explain why a fact might have changed between two time steps
		- If a fact changes  between $i$ and $i+1$, then an action at step $i$ must have caused it

##### Continuing Example
Enumerate the set of action that could result in a fact changing between time steps

![[Pasted image 20221018155503.png]][2]

######  Exclusion Axioms

We identify actions that cannot occur at the same time.

**Complete Exclusion Axiom:** Only one action at a time.

![[Pasted image 20221018160125.png]][2]

**Complete Exclusion Axiom**: Prevents invalid actions on the same timestep

Our collection of axioms are converted into conjunctive normal form and then fed to a SAT solver.

The SAT solver will iterate out (increasing T) until it can find an assignment of truth values that satisfy $\phi$

Once reached - provided planning is total order - there will be exactly one action $a$ such that $a^i$ = true.
	This is the $i_{th}$ action of the plan.

### Partial Order Planning
Forward search works by pushing from the initial state, till we get to our goal state.

- We might create redundant steps in our plans
- We may find loops in our state space
- We may be at the mercy of the state space to find the actual solution

So why don't we try Regression Search...

##### Regression Search
This is a searching method that searches backwards from the goal state.
- Instead of aiming for a state that holds all goals, we search for an assignment of the goal facts
- Find actions with add effects that create goal facts
- Then add (unsatisfied) preconditions as sub-goals to achieve

Searching backwards is a valuable method because searching backwards vs searching forwards are not symmetric.

**Forward Search**:
- One initial State
- Apply action $a$ to state $s$? One valid unique successor $s'$

**Backward Search**
- A set of goal states
- Multiple states where $a$ can be applied to reach $s'$

###### More Formally

- The set of actions $A(s)$ applicable in $s$ are the operators
	$op \in O$ that are relevant and consistent
	- Namely for which Add operations and s are not equal to Delete options and S 

The state $s = f(a,s)$ that follows the application of
	$a \in A(S)$
	$s = s - Add(a) + Pre(a)$


#### Example
![[Pasted image 20221018192720.png]][3]

You have a DVD delivering service  and the DVD is currently at your house (we're in the goal state)

The next states could be...
- Loading MyDVD onto the Truck at H (home)
- Loading MyDVD onto the Truck at L (London)
- Loading MyDVD onto the Truck at A (Amazon)
- Driving the Truck from L to H (London to my Home)

Now as mentioned, it’s important to factor in whether or not an action is consistent.  In this case, the first action, loading MyDVD onto the truck, isn’t a good action, because it also deletes a goal fact of MyDVD being at H.  So it’s not applicable, we ignore it.

Driving from L to H makes a lot of sense here.  But notice the other two load actions for loading MyDVD onto the truck.  Now we’re only interested in whether the add effects satisfy our current sub-goal, which is to have MyDVD on the Truck.  So these are valid paths of the state space to explore, even though it leads to the possibility in that the truck is in one of two different places in each of theses scenarios.

![[Pasted image 20221018193041.png]][3]

Rolling out the top two state sets above, we see the need to satisfy two preconditions:

- In the first instance, the driver is in the truck and we know that would happen if the driver has driven the truck somewhere. Now this gives us a more concrete state, but it doesn’t address the fact that somehow the drive between L and H happens before loading M onto T at L? 

- The second rollout sees us also add a drive action.  Which means we can now confirm the driver is in T.  But we still don’t really know where the Truck is at this point.  It could be either at A or at L given we’ve driven away from H to L.

![[Pasted image 20221018193247.png]][3]

Same process here...
But the key thing, is we’re actually getting closer to a valid initial state, given that Drive AL driving from Amazon to London is a state where M is in T, T is at A and D is driving T.  So we only have to get M loaded onto T, for D to board T at A which in turn requires D to walk from their home to Amazon.  At which point the plan is satisfied. 

But it is possible that we could have found other valid actions throughout this search graph.  In fact we found actions such as the driver boarding the truck and the package being loaded onto the truck that are useful, but just not at that point in time.  Hence, it would useful if we could establish that certain actions are good to have in the plan, but just don’t commit to them entirely.

#### POP Planning
This is planning in a plan space, using a lifted framework where we have an:
- Initial Plan
- Initial State
- Goal State

We either:
- Pick an unresolved goal
	- Select an action to achieve it (or initial state)
	- Add to the plan
	- Add a casual link and add its preconditions as open goals
	- Find an unbound parameter and select a binding
	- Find a threat, resolve by promotion or demotion

##### Example

Consider the example where we start with the initial and goal state, and then we consider how to achieve the goal fact of having the DVD at H.

We could consider using the unload action, given that would achieve the desired effect, we then need to consider the preconditions involved and what assignment to all of these variables is required.![[Pasted image 20221018193618.png]][3]


We can quickly fill in the possible values for this, with Truck T being used and the DVD being at location H (my house).  We can try a variety of combinations, but this is the one that works.

This not only sets up our preconditions, but also sets the new goal for us to solve is getting the truck to H and the DVD in the truck.![[Pasted image 20221018193721.png]][3]


Next we consider how to satisfy loading the DVD onto the truck at L, but that doesn’t work.  Because the facts, given there is an inconsistency within some of the facts of where T is.  If we assigned the variable L to be H, then it violates the goal we’ve already solved.  And doesn’t give us useful information of how the truck got to location H in the first place.  So let’s scrap that for now.![[Pasted image 20221018193756.png]][3]


However...
We can establish that driving from L to H will get us to the correct destination and also, it generates a causal link in saying that Driving from T to H is required before we unload the DVD.  There’s also a causal link dependency on the drive action, because in order for it to work, we know that Link LH needs to be a valid fact.  So we know at some point before executing this action, we have to be at L in order to reach H.![[Pasted image 20221018193942.png]][3]

Having tackled how the truck reached L, we’ve achieved a lot of useful information: we now know that Driving T from A to L can satisfy the need for T to be at L before it drives on to H.

But also, we create three new causal links.  We establish that Drive T from A to L is required before we then drive it from L to H.  But also, we link the preconditions of Driving from A to L to the initial state.  So we know that driving T from A to L not only has to happen before we drive to H, but it also needs to happen after the initial state. ![[Pasted image 20221018194103.png]][3]


By assigning the value of the location in the load action to A, we now see some nice causal links established between the location of both T and the DVD in the initial state and how that will ultimately satisfy the rest of the plan.
We’ve actually satisfied not just the goal fact, but also all of the preconditions of the facts relied on in order to give us the final solution.  But there is still the issue of what the final order is.

We now have a threat that’s emerged in the partial plan.  Both the Load and Drive actions appear to be applicable off the back of the initial state.  But  we can see that the Load action requires the truck to be at A, as does the drive action, but we know that the drive action will result in the truck being at L. ![[Pasted image 20221018194734.png]][3]


We go ahead and dictate the ordering such that the load action has to go before it, given that the Drive action threatened the causal ink between At TA in the initial state and the load action, we promote the Drive action forward to past the conflict.  This now ensures – based on the orderings – we will load the DVD onto the truck before we driving away from Amazon.

As a result, we now have a successful plan ordering that will ensure a complete transition of actions from initial state to goal.![[Pasted image 20221018194837.png]]

#### HTN Planning


#### Pros & Cons of Backward Search
##### Pros
- Regression can help us reduce state spaces
- Produces 'least commitment' plans
##### Cons
- High branching factor: threats, bindings, actions
- Hard to compute heuristics

### HTN Planning
Hierarchical Task Network Planning (HTN) is a planning process which looks at tasks to complete as opposed to goals.

In addition, we then use methods to express how a given task could be solved.  These methods then decompose the original task into subtasks, which in turn can be solved either by transforming that task into a single concrete action, or the task is handled by another method, which further decomposes said task into more tasks.
We then can apply much broader sets of constraints on action execution. 

#### HTN Planning: More formally
If we were to consider this more formally, then we would consider the HTN planning problem as 4-tuple, $(∑, M, s_0, T)$

Where 
$∑$- A state variable planning domain
$M$ - A set of methods
$s_0$ - The initial state of the problem
$T$ -  A list of tasks to complete

#### HTN Planning

HTN planning defines to types of tasks:
- Primitive Tasks
	- Translate to single planning action
- Compound Tasks
	- Translate into a collection of one or more tasks

**Planning Process**:
- Recursively refine each task into subtasks
- Ensure tasks can then be grounded with literals

![[Pasted image 20221025120827.png]][4]

So as you can see from the above diagram, we start with the original task we were given to complete, and given this is a compound task the method is applied to find a valid permutation of possible tasks based on the current state.

This is then decomposed into two tasks and we approach them from left to right.  So we visit the first task and as we decompose this into a primitive task, which translates into an action, which then results in the plan moving from s0 to s1, Meanwhile, we can’t find an action that matches the task on the right, so we once again need to run a method to find a valid decomposition of this task, which in this case is two more primitive tasks, enabling for us to move from s1 to s2 and then finally s3

What this allows is for a top-down approach to behavioural design.  If you think about how plans are usually constructed, it’s more of a bottom-up approach, whereby the individual actions are selected and the resulting plan emerges from the planner finding out that putting actions together in a specific sequence yields an intelligent response.  We then have to go back and correct this as we realise the search is taking us down dead-ends, but ultimately it’s more focussed on individual actions being glued together in the correct sequence.  

However, in this case, what we’re seeing is that the resulting plan is at the mercy of the task networks.  By embedding specific constraints on how a particular task is executed, we’re expressing a total order over a subset of actions that will yield a resulting behaviour that is exactly what the designer intended.

#### Example: Dockworker

**Task**:
- Moving containers from one pallet in the yard to another

**Goal**:
- Moving containers from original pallet X to destination Y, while preserving the order of containers on the new pallet.
![[Pasted image 20221025121132.png]][4]

Task: 
- move -stack(p, q)

Parameters:
- p - The original location
- q - The destination location

##### **Actions**
- Take <k, l, c, p, o>
	 **Preconditions**
	 - belong(k, l), attached(p, l), empty(k), in(c, p), top(c, p), on(c, o)
	 Effects
	 - holding(k, c), top(o, p), not(in(c, p)), not(top(c, p)), not(on(c, o), not(empty(k))  

- Put <k, l, c, p, o>
	 **Preconditions**
	 - belong(k, l),attached(p, l), holding(k, c), top(o, p)
	 **Effects**
	 - in(c, p), top(c, p), on(c, o), not(top(o, p), not(holding(k, c), empty(k)

When we consider the actions we can execute, we have only two.  Taking a container off of a pallet and putting it on another one.

This is all relatively straightforward, in that the both actions require the crane (denoted as k) and the pallets that the container is either being lifted from or put onto are related to the location.  Hence the use of the belong and attached predicates.

The take action will then pick up a container and the crane will hold it.  It will then also reassign the other container o as the top of that particular pile.  Note that in this case, o can either be another container or the pallet itself, denoting that there are now no longer any containers atop that particular pallet.

Meanwhile, when we then attempt to put it down, in a manner similar to BlocksWorld and its ilk, we check whether the location is clear for us to put it where we intend to.  All pretty straightforward and nothing we’ve never really seen before.

So if we were trying to solve this problem, we could in theory do this with a regular PDDL representation.  We could move the containers around between locations and eventually reach the correct combination.  However, there is a lot of bespoke information here about the nature of the problem that – if we knew about it in advance – would be really helpful.  And this is where the HTN methods will come in handy, given they will permit us the ability to create compound tasks that allow us to deal with some of the specific issues we’re about to see here.

##### Methods

**Recursive-Move(p, q, c, x)**
- Task: move-stack(p, q)
- Pre: top(c, p),on(c, x)
- Subtasks:
	- move-topmost-container(p, q)
	- move-stack(p, q)

**Do-Nothing(p, q)**
- Task: move-stack(p, q)
- Pre: top(pallet, p)
- Subtasks (none)


If we take a look at this method a little more closely, it has preconditions that state we cannot run this task lest we know that container c is at the top of pile p and we can figure out which container that c is atop of, so we can then set that as top afterwards.  Plus we can see that it not only is designed to solve the move-stack task, but it does so using two subtasks: first we move the topmost container from the original pile and onto another, but also, we have the move-stack task emerge as a subtask.  This ensures that we continue to work our way down the stack by applying the same method again. 

This task is recursive because it is asking us to solve the original task after it does everything else it needs to do.  But in order for a recursive task like this to work, it also needs a base case.  A situation where we can ensure that the recursion stops.  To address this, there is the Do-Nothing task.  This task checks whether only the pallet is at the top of a given pile, which means that the pile is empty.  In the event that the pile is empty, we can apply this method which will effectively stop the recursive-move task from continuing to run, given we’ve completed moving every object.

But of course, we now have another task here, the move-topmost-container which will move items between each pile.

**Take-and-Put(c, k, l1, l2, p1, p2, x1, x2)**
- Task: move-topmost-container(p1, p2)
- Pre: top(c, p1), on(c, x), attached(p1, l1),  belong(k, l1),  attached(p2, l2),  top(x2, p2)
- Subtasks:
	- take(k, l, c, x1, p1)
	- put(k, l2, c, x2, p2)

So now we consider how the move-topmost-container task could be implemented.  We have another method entitled take-and-put, which is rather self explanatory.  In this instance, we are aiming to take the topmost item on a given pile and then move it to another one.  The actual tasks are as expected, to execute both the take and put actions in that order.  But what is interesting is that the preconditions of the method are essentially reinforcing that the grounding of variables for each task lines up in such a way that it is possible for these two actions to happen back to back.  Hence we ensure that the two locations both use the same crane but also that we have the correct grounding of variables for each of these actions such that we don’t have to wait until the preconditions fail before realising that this isn’t valid.
![[Pasted image 20221025122232.png]][4]

But this still doesn’t solve the problem, given we can now move one pile of containers from one position to another, but when we do so, the ordering is now upside down.  So how do we resolve this?

**Move-Stack-Twice(p1, p2, p3)**
- Task: move-stack(p1, p3)
- Pre: None
- Subtasks:
	- move-stack(p1, p2)
	- move-stack(p2, p3)

The solution, is to create another method that can solve the move-stack problem.  In this case, we create a task that actually moves a stack twice, by running the move stack task twice but on a collection of three parameters.  Our main locations we wish to move between and an intermediate.   So if we were to consider the three pallets in location 1, p1a p2b and p1c, we would list them in this order, given we can then move the collection into an upside down configuration in the intermediary location, followed by then moving it back into the correct orientation in the final location.

So in essence, we can then solve the moving of one stack from a given location to another using the one task, which will then be decomposed into the recursive task, generating the take and put actions in the correct sequence.

##### Improvement
**Move-Each-Twice()**
- Task: move-all-stacks()
- Pre: None
- Subtasks:
	- move-stack(p1a, p1b)
	- move-stack(p1b, p1c)
	- move-stack(p2a, p2b)
	- move-stack(p2b, p2c)
	- move-stack(p3a, p3b)
	- move-stack(p3b, p3c)

And in fact we can then roll this out one step further, by actually solving the entire problem using one method, which is to then call all of these other methods. 

#### Searching HTN

Unlike state-space planning, where you either search forward or backward, we have the option of searching in two directions in HTN:
- Backward/Forward
	- Selecting tasks![[Pasted image 20221025122736.png]][4]
- Up/Down
	- Processing tasks into sub-tasks or action![[Pasted image 20221025122755.png]][4]

So if we consider how the HTN planning process works, it’s a process of selecting tasks and then configuring them with the correct parameters.  Hence we’re moving across the search space to generate tasks, and then downwards as we explore the valid permutations of those tasks.  This is very much in contrast to regular search where we either search forwards into the state space and find valid state action pairings or backwards from the goal to reach the initial state. 

It’s a different approach where given we already have the tasks available to us, the process is less about finding states that get us closer to the goal, but instead finding valid permutations of the tasks grounded with respected to the current state facts such that it will provide a valid path through the state space to the goal.  Which in this case, is simply satisfying the original problem states that we’re provided with.

It's important to ensure that when we attempt to process a task, we know what the world state would be at this point

Hence in this instance, it's important that when a task is broken into subtasks, they're processed in order such that the world state is already planned in advance.

#### Total vs Partial Ordering
- The simplest approach (STN planning) is reliant on ordering constraints.  
- Forward search required given need to test for applicability of the state.  
- Interweaving actions need to be written into a more concise formalism.  
- Partial ordering is feasible, but requires a more complex algorithm to achieve it.

![[Pasted image 20221025123107.png]][4]


#### STN vs HTN Planning

- HTN planning is a more general implementation of STN.  
- Variety of formalisms and algorithms that are employed.
	- Forward Search – SHOP2
	- Plan-space Planning – O-Plan
		- Constraints can be associated with tasks and methods.
		- i.e. What facts are true at the before, during and after a task/method is executed.  
- Use of goals/sub-goals instead of tasks/subtasks.
	- GDP/GoDeL

## Questions

---
Backlink: [[Artificial Intelligence Planning Outline]]

Sources:
1. 
	- Name: Non-Forward Search 01 - GraphPlan.pptx
	- Author: Tommy Thompson
	- Date: 18/10/22
2. 
	- Name: Non-Forward Search 02 - Planning as SAT.pptx
	- Author: Tommy Thompson
	- Date: 18/10/22
3. 
	- Name: Non-Forward Search 03 - POP.pptx
	- Author: Tommy Thompson
	- Date: 18/10/22
4. 
	- Name: Non-Forward Search 04 - HTN Planning.pptx
	- Author: Tommy Thompson
	- Date: 18/10/22