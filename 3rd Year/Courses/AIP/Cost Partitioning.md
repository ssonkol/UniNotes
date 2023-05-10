# Cost Partitioning
Tag: #review 

---
## Definitions

## Notes

If we want to achieve optimal planning, we need to ensure admissible heuristics are provided.

But given planning is hard, we can't expect one heuristic to always work well in a given task. Furthermore, not one heuristic can really grasp the complexity of larger domains.

**Example problem:**

If we have multiple abstraction heuristics for the state space, how do we know which is best for a given problem and can we determine what is a good way to blend them together?
- It's difficult to determine, especially when using domain independent heuristics.
- It's even more difficult to determine on a per-domain and per-problem basis.

### Cost Partitioning
This is where we are hoping to split the action costs - partition them- among the heuristics in such a way that the total cost implied by the heuristic doesn't exceed the original action cost, thus remaining admissible.

#### Optimal Cost Partitioning
This is where we aim to find the best heuristic values for a given state among all of the cost partitions that we have available.

This is essentially ensuring that if we found the best values in one heuristic, we tweak the other heuristic such that it still is additive.

Example:

Now when we first look first at h1, we can see the optimal cost is 5, given we take the black action which has a value of four, followed by the green action with a value of one. 

This results in 5, which is fine, but when we now consider h2, we can’t achieve the same goal using the same path.  Instead we need to the red and then blue action to get 5.

But the two actions that across both abstractions ensure a path to the goal are black and blue, so let’s redistribute their costs such that we get an admissible heuristic each time that is also additive for both h1 and h2.

So in this case, we assign the full cost of the black action to h1 and thus give it a value of 0 in h2, while we need to redistribute the cost of four across both h1 and h2.  We given it a value of 1 in h1 and 3 in h2.  Resulting in h1 being 5, h2 being 3 and an additive admissible partitioned heuristic value of 8.

So this requires us to analyse and recompute costs across all of the actions in each abstraction.  It works and is relatively fast to compute, and by fast we mean it runs in polynomial time, but it still isn’t all that feasible to run on larger problems.  Given rolling this out in even small example state spaces is going to be quite time consuming to do.
![[Pasted image 20221015215317.png]][1]

##### Pros & Cons of Optimal Cost Partitioning

###### Pro
- It's fast to compute (polynomial time)

###### Con
- It's still to expensive in practice

#### Post Hoc Optimisation

Next up, we have post-hoc optimisation, whereby we isolate what are the relevant actions in each abstraction and once we have those, we find a set of weights that we are going to apply to each heuristic, such that the summation of their calculations is additive and in-turn admissible.


**Example:**

It’s clear that in both cases the black and green actions are relevant given in both cases they get us to the goal.  Meanwhile in h1 the red action is not relevant, given that keeps us in the same abstract state and the same applies to the green action in h2.  So in it’s clear than in h1, the black blue and green actions are relevant, while in h2, the black, blue and red actions are relevant.

So next we calculate a weighting for each heuristic w1 and w2 – each of which being between 0 and 1 and sum up to a value of 1 – such that when we then multiply each cost of a relevant action by the weight and if it isn’t a relevant action, we set it to 0.

So if we return to h1 under post-hoc optimisation, we have calculated a weighting of 0.25 such that it now means the black and blue actions are now 1 each, and in h2 with a weighting of 0.75 they are 3 each.  Meanwhile the red action in h1 is now 0 given it isn’t relevant to the heuristic calculation and the same applies for the green action in h2.  Now this is but one configuration, we could set weights w1 and w2 differently, but this gives us whole numbers for each action – which is easier to work with – and still retains the additive feature we so desire.

![[Pasted image 20221015215939.png]][1]

#### Greedy Zero-One Cost

We order our heuristics into a particular sequence and then we use the cost of a given action in the heuristic in the first instance we find a heuristic where that action is relevant to reaching the goal.  If the same action then appears in subsequent heuristics, we just set that value to zero.  Plus if the action is not relevant, it also gets set to zero.

**Essentially**…
1. Order heuristics in a particular sequence
2. Use the full costs for the first relevant heuristic

**Example:**

The black blue and green actions are relevant actions in this context.  Hence we keep them as they originally were, with costs of 4, 4 and 1 respectively.  Clearly, as we’ve seen in the previous example on post-hoc optimisation, the red action in h1 isn’t relevant.  So we scrub it and set it to zero.

Meanwhile, if we look at h2, the green action is again not relevant, so we set it to zero, but all the other actions are relevant.  However, we have already used the black and blue action in this case, so we also set those a value of zero.  Hence the only action that retains its cost value is the red one, given the green one isn’t relevant.  This actually means that the heuristic value is 0 for h2.  Not terribly informative, but it still gives us an additive set of heuristics.

But, it’s also a little wasteful, given if we think about it, we stripped any useful information from h2 because already used the costs of relevant actions in h1.  But what’s interesting here, is that if we think about it, the cost of the blue action in h1 isn’t relevant, given we don’t use that to calculate the heuristic.  Hence we have a slightly improved version of this approach called saturated cost partitioning.
![[Pasted image 20221015220237.png]][1]

#### Saturated Cost Partitioning
We do the same thing as with Greedy Zero Partitioning, but this time, we set the costs of relevant actions to the best the minimum cost that preserves the heuristic estimate.  Then we use whatever remaining cost is left for the relevant actions in the other heuristics.

**Essentially**… 
1. Order heuristics in particular sequence
2. Use the minimum costs to preserve the estimate value
3. Use the remaining cost for other heuristics

**Example**:

So if we revisit this example from the greedy-zero one partitioning, the blue action is reduced to a cost of one in h1, bringing it in line with the green action and this means that for the blue action in h2, we can use that remaining cost value as part of the heuristic calculation.

This now means that with saturated cost partitioning we have a cost of 8, which is not only again closer to the actual value and thus a little more informative, but is also still admissible.
![[Pasted image 20221015220503.png]][1]


#### Uniform Cost Partitioning
This method considers all of the relevant actions in each heuristic and then divides their cost uniformly over the number of heuristics that those relevant actions appear in.

**Essentially**…
1. Distribute these costs uniformly to all relevant actions
2. Distribute across all heuristics

**Example**:

If we look at h1, then in this instance the red action is not relevant.  But the black blue and green actions are relevant.

Meanwhile, over in h2, the green action is not relevant, but the red, black and blue actions are relevant.  If we consider the union of these two sets, then only black and blue actions are relevant in both.  So we will divide their total cost by the number of heuristics that use them.  Meaning we then divide their cost by 2.  So this means that in both h1 and h2 the black and blue actions now only cost 2 in each case. 

However, the cost of the red action in h1 is set to zero because it is not a relevant action, but the green action – given it is only relevant in h1, keeps its cost of 1.

And we can see the exact same thing with h2, only this time red is relevant and green is not.  So their costs are set accordingly.

![[Pasted image 20221015220737.png]][1]

#### Summary
- Cost partitioning is one method to allow us to combine multiple heuristics


## Questions
---
## Footnote

Backlink: [[Optimal Planning]]

Source:
1. 
	- Name: Optimal Planning 3 - Cost Partitioning.pptx
	- Author: Tommy Thompson
	- Date: 15/10/22
