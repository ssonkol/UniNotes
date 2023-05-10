# Planning with Preferences
Tag: #review 

---
## Definitions

---
## Notes

Most real problems involve resources - Money, materials, people and components etc.
These can be discrete numbers but we also need to take care of continuous values.

We can use PDDL in these cases too...

#### Semantic Curio
PDDL demands that we can't be ambiguous about a state - meaning simultaneous actions have to be non-interfering
> In example, you can close a door and also ask someone to walk through it

#### Reachability Analysis
1. At each action layer, identify multiple actions and then apply all effects together.
2. We then maintain a record of all reachable values
	1. Decrease effects to reduce lower bound and increase effects to increase upper bound.

##### Example
![[Pasted image 20221107223729.png]][1]

#### Resolving Effects
An effect will increase the upper bound for fluent x by the maximum value - vice versa for decrease

The maximum value of an expression is found as follows:![[Pasted image 20221107223901.png]][1]

 ![[Pasted image 20221107224154.png]][1] increases the upper bound to the maximum of its current value and the maximum value of ![[Pasted image 20221107224228.png]][1]
  and decreases the lower bound similarly

Multiple effects on the same variable can be evaluated in any order - the right hand side expressions are always evaluated using the values from the preceding fact layer.

#### Evaluating Conditions

A condition can be checked using similar interval arithmetic
![[Pasted image 20221107224415.png]][1]

Then from an initial state with (x = 0) we can reach x in [0,2] after one step, which appears to satisfy a goal (x = 1), even though that goal cannot be satisfied with this action and initial state.

#### Extracting A Relaxed Plan
As usual, if we need a proposition to have a certain value (1/0 or  True/False) then we can add the earliest achieving action to the relaxed plan.

If we need a numeric operation or goal to be satisfied.
We can take the first level at which the condition is satisfied and then proceed as follows
- We now consider conditions of the form A > 0 or A >= 0, and we focus on A: rewrite A as a sum of terms: $t1 + t2 + t3$ … to that each $ti$ has no addition/subtraction in it (a ti could be negative and can include multiplication or division  - this is simply arithmetic to split compound expressions) Eg: ($3x - y(u + 2v/w)$) becomes $3x + (– yu) + (– 2yv/w)$ etc

- Now evaluate the range of each term in this sum $[a,b]$ (remember that $–[a,b] = [-b,-a]$ and a number, n, has range $[n,n]$)

- Ideally, we want the cheapest plan to achieve the condition – there are various options here, but best is to ask what the largest value of our expression (A) was in the preceding layer – say it was x – and then find achievers at the current layer that increase x by enough to satisfy A > 0 (or A>= 0)
	- we can look for the relative contributions of each variable to the expression and request the biggest contribution from the most significant contributor first, and then keep adding in more contributions until we achieve the target.

- Then we push back to the preceding layer any outstanding requirement after these contributors have done their work.

##### Example
![[Pasted image 20221107224859.png]][1]

#### Limitations
Building bounds by incrementally applying actions repeatedly at each layer has an important cost - If we start to increase bounds the reachability graph increases the amount of required layers.
> i.e. An action increase by 1 with a bound of 10000000, will require a reachability graph of 10000000 layers.


To get around this we let the bound go to infinity and use the relaxed plan extraction to count the number of repetitions of the increasing action required to achieve the goal

This has a propagating effect
> If increasing (X) by 1 costs $1 and we can work a day to earn a dollar, then to get (X) >= 1000000 requires 1000000 repetitions of the increase, which will require $1000000 and this, in turn, requires 1000000 days of work)


If the number of applications is bounded by some limited resource, this can be used to bound the maximum value of a variable

### Numeric Planning

In principle, PDDL numeric preconditions compromise
- A comparison operator i.e. $<,>, <=, >=, =$
- A left- and right-hand side written using constraints, the values of functions, and operators i.e. $+,-,*$ 

#### Numeric Effects
These compromise of:
- A variable to update
- How to update it
	- Assign (=)
	- Increase (+=)
	- Decrease (-=)
	- Scale-Up
	- Scale-down
- A right-hand-side formula, as in preconditions

##### Examples
![[Pasted image 20221107230456.png]][1]

#### Metric Functions
We can have numeric state variables by defining a metric function for the planner to optimise

These metrics refer to the values of variables after the plan has finished executing, i.e. in the goal state.

Defining a metric function is *optional* for a numeric planning problem


### LP-RPG
#### Linear Programming
This is using a linear function to solve problems 
 *Note, don't take this definition literally, this is my understanding*

#### Integer LPs

If we can only use integer values for some variables, then we further constrain the LP to an Integer LP - these are NP-hard to solve where LPs are polynomial.

ILPS can sort of do planning.
Propositional planning can be complied into an ILP *if* the plan length is fixed or bounded - you can also solve SAT problems using ILP but SAAT solvers are better at SAT problem solving and planners are better at planning

You have to use the same iterated deepening search deal to find optimal length plans

#### Weaknesses of Numeric RPG
- Cyclical Resource Transfer
- Helpful Action Distortion

#### Relax LP
- We can relax the propositional part of the problem - then the ILP can capture just the numeric bit
- We can relax the integer constraint on the action counts and just use an LP
	- Them the solution to the LP will give us a good guide to the choice of the right helpful actions and also account for the reality of cyclic transfer of goods
- The LP can be used to propagate bounds on the numeric variables in the reachability construction, solving, for each variable, to find the minimum and maximum values, given other constraints.
	- This makes the reachability analysis more informative
		- But we can also use the LP in relaxed plan extraction: we modify the LP that describes the contributions to each variable by adding the bound on the required value needed to satisfy a goal or precondition, then solve to minimize the number of actions needed 

#### LP review
- LPs are not as cheap to solve as typical reachability bound computations, so this idea has to be used with care
	- Lots of tricks can be employed to improve the LP (identifying actions that are only applicable a bounded number of times, spotting important propositional constraints etc)

•Assignment doesn’t fit the LP pattern (multiple applications of an assignment action don’t impact on the final value of the affected variable) so they have to be handled using the previous approach – that complicates relaxed-plan extraction as well

### Modelling
In our domain we declare
- **Numeric fluents** like predicates 

These fluents can be used in preconditions and effects.

Remember, we can only use built-in predicates on numeric expressions i.e. $<,>, <=, >=, =$
Numeric expressions are built using fluents, constants and standard arithmetic operators ($+,-,*$ etc.)

The effects can modify numeric fluents using:
- Increase
- Decrease
- Scale-Up
- Scale-down

*Note that only a few planners handle scale-up or scale-down effects*

### Soft Goals
#### Compiling Goal Preferences 
- Add a fact **normal-mode** asa precondition to every action
- Add an action **end** that deletes **normal-mode** and adds **end-mode**
- Two actions for each goal preference pi
	- **collect(p)** - Has pi as its precondition, adds p'i
	- **forgo(p)** - has (not(pi)) as its precondition, adds p'i and **increases plan cost by cost(pi)**
- Set goal to: $(and (p'0) (p'1) (p'2)...)$


### LPRPG-P
#### Tracking Preference Satisfaction in Search

Preferences have corresponding automata:
- Automated translation from LTL into automata
- Each state maintains an automation corresponding to each preference
	- Each starts in initial position, update according to initial state
- Each time an action is applied (state expanded):
	- Update the automation if condition from current position fires

#### Search in LPRPG-P

Preference violation cost of a state PVC(S):
- Sum of violation costs of all automata that are in E-Vio
- Search until a solution is found:
	- A plan that satisfies all the hard goals
- Continue searching once a goal is found:
	- But prune all states where PVC(S) > cost of best solution found so far

![[Pasted image 20221108000609.png]][6]

If we have a problem with no hard goals and only preferences/soft goals the RPG heuristic value is zero for every state!

##### RPG Example

Initial State : at A
Goal State: at E![[Pasted image 20221108000734.png]][6]
![[Pasted image 20221108000752.png]][6]


Add preconditions to goals![[Pasted image 20221108000818.png]][6]

Therefore ![[Pasted image 20221108000845.png]][6]

**What do we need?**
Effectively we need to track knowledge about preferences whilst building the RPG

To do this we need:
- Termination Criteria
	- Stop building graph when goals appear insufficient
- A mechanism for selecting the right achiever
	- Earliest is not always the best
	- Arbitrary could miss something good

#### Preference Aware RPG
- At each fact layer we maintain a set of preferences for each fact. 
	- These are the preferences that are violated in achieving the fact at this layer;
	- For facts that appear in the current state this is empty;
	- The preference violation set for a newly appearing fact is that of the action that achieves it, and the union of those for the action's preconditions.
	- If a new path to a fact is discovered, use the lowest cost of its existing/new sets;
	- Otherwise the set at that layer is the set from the previous layer.
- Now we can build the RPG to the point at which:
	- No new actions appear and;
	- No preference violation sets are changing.

This means we have to build the RPG to more layers, but it does mean that we can generate potentially longer relaxed plans that satisfy preferences.
![[Pasted image 20221108001214.png]][6]

#### Optimistic Automation Positions

In PDDL3 there is always a 'best' position in the automata so we can maintain the best position possible for RPG layers
- In general LTL we'd have to maintain all possible positions

A violates P when applied in I if, it activates a transition from the (all) automation position(s) in I:
- to E-Vio (e.g. sometime-before), (at-most-once)
- to Unsat and the facts required to achieve the transition back to Sat state are not yet in the RPG (e.g. sometime-after)
![[Pasted image 20221108001517.png]][6]

#### Reappearing Actions
If an action appears later in the RPG with a lower preference violation cost
- Add it again with the precondition that made the automation transition
- Propagate to tis effects and actions that rely on them by building further action layers until no further change in violation sets

Then continue building RPG as normal

Termination criterion: No other facts/actions appearing and preference violation sets unchanging

![[Pasted image 20221108001735.png]][6]

#### Solution Extraction

Not all preference problems have hard goals, so we need to decide what goals to achieve:
- Some soft goals are explicit in the problem (at-end)
- Others are implicit in currently Unsat preferences (sometime-after a b) (sometime p)

For goal generation look into automata: any automation which is currently unsat, add the condition on tis transition to Sat as a goal in the RPG

![[Pasted image 20221108002101.png]][6]

If the transition doesn't appear in the RPG then preference is E-Vio not Unsat

![[Pasted image 20221108002144.png]][6]


### Distance Cost Pairs
This is where we try to find the balance between how many actions (distance) will equate to a lower cost

i.e.

4 actions will get down to cost 20
8 actions will get down to cost 10
10 actions will get down to cost 7 

Which one do we choose?

1. Start by pretending all goals are hard goals![[Pasted image 20221108002919.png]][7]
2. Colour code with reason each action is in the plan (note H is Hard goals)![[Pasted image 20221108002933.png]][7]

The distance-cost pairs of the above plan are as follows
- 5 actions = cost 3
- 7 actions = cost 2
- 11 actions = cost 1
- 12 actions = cost 0

Now there are many different combinations of actions to costs, but finding these can take ages. 

Instead, use a greedy algorithm to compromise and start with the hard goals and then add preferences one at a time.
- Greedy by length: add the preference that requires the fewest actions to be added to the relaxed plan in order to satisfy it (minimise distance to go);
- Greedy by cost: add the preference that reduces the cost of the resulting relaxed plan by the most (i.e. the most expensive one that is still violated).

#### How do we use these

Use dual open-list search
- One open-list sorted by h(all) the length of the relaxed plan to satisfy all preferences;
- One open-list sorted by h(<C) the shortest distance from a distance cost pair which has a cost less than the cost of the current solution (C*) – g(s).

Search in alternation putting new states on both open-lists.

---
## Footnotes
Backlink: [[Artificial Intelligence Planning Outline]]

Sources:

1. 
	- Name: [Lecture Slides: Planning with Numbers](https://keats.kcl.ac.uk/mod/resource/view.php?id=6375834)
	- Author: Derek Long
	- Date: 07/11/22
2. 
	- Name: [Lecture slides: LP-RPG](https://keats.kcl.ac.uk/mod/resource/view.php?id=6375835)
	- Author: Derek Long
	- Date: 07/11/22
3. 
	- Name: [Numeric Planning - Introduction](https://keats.kcl.ac.uk/pluginfile.php/8525323/mod_folder/content/0/Numeric%20Planning%20-%20Introduction.pptx?forcedownload=1)
	- Author: Derek Long
	- Date: 07/11/22
4. 
	- Name: [Preferences - 01 - Introduction](https://keats.kcl.ac.uk/pluginfile.php/8525323/mod_folder/content/0/Preferences%20-%2001%20-%20Introduction.pptx?forcedownload=1)
	- Author: Derek Long
	- Date: 07/11/22
5. 
	- Name: [Preferences - 02 - Modelling](https://keats.kcl.ac.uk/pluginfile.php/8525323/mod_folder/content/0/Preferences%20-%2002%20-%20Modelling.ppt?forcedownload=1)
	- Author: Derek Long
	- Date: 07/11/22
6. 
	- Name: [Preferences - 03 and 04 - LPRPG-P](https://keats.kcl.ac.uk/pluginfile.php/8525323/mod_folder/content/0/Prefernces%20-%2003%20and%2004%20-%20LPRPG-P.pptx?forcedownload=1)
	- Author: Derek Long
	- Date: 07/11/22
7. 
	- Name: [Preferences - 05 - Distance Cost Pairs](https://keats.kcl.ac.uk/pluginfile.php/8525323/mod_folder/content/0/Prefernces%20-%2005%20-%20Distance%20Cost%20Pairs.pptx?forcedownload=1)
	- Author: Derek Long
	- Date: 07/11/22