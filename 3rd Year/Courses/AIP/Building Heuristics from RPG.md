---
sr-due: 2022-10-13
sr-interval: 3
sr-ease: 250
---

Tag: #review

# Building Heuristics from RPG


## Notes

### Costs
- Consider the cost of the actions to satisfy in our fact layers
- If the facts are already achieved, the value is 0
- If the facts are not achieved, the value is $\infty$


Example:

![[Pasted image 20221008190111.png]][1]

We visualise all of that facts that can become true during the relaxed planning process.  In between each of these facts, is the costs of actions.

Our goal G is to have both d and e to be true.  So it’s important to factor how expensive each of those actions is and this can tell us how close we are to goal based on the facts that are emerging and the costs that it takes us to achieve them.

![[Pasted image 20221008190158.png]][1]

### $h_{Add}$ Heuristic
We then consider $h_{Add}$  (sometimes referred to as the additive heuristic)

- $h_{Add}$ = We sum the value of all costs to reach a given fact
- Inadmissible, given emphasis on goal independence.

This is can be rolled out using Dijkstra’s algorithm, whereby we sum the cost of actions and maintain the lowest total costs.  Then for the final goal set, we simply add up the total costs reached to get there. 

Hence while a is 0, b is 2 given in order to reach this fact there was an action with a cost of 2.  c has a value of 7, given it’s the summation of the original cost to achieve b, which was 2 plus the extra action with a cost of 5.  Note that both d and e are lower here, given that the other actions that we could execute from reaching point b would enable for us to achieve d and e with a value of 6, instead of 8 if it went via C.  And the goal facts, G are satisfied when both d and e are satisfied, hence it takes the sum of those two states as the overall value of 12.

![[Pasted image 20221008190540.png]][1]

Now we know this is inadmissible, because if we were to let FF solve it, it would generate the plan that we see here, where the total cost is actually 10. Given the nature of the heuristic, it means that we’re counting the actions several times over when we calculate the heuristic value.

Now this works fine, if we run on the assumption that the goals are completely independent of one another. But in most planning situations, they’re not.  You will typically work towards satisfying one goal while working on another.  So there are a lot of shared actions.   Even in this example you see here, the action that achieves fact b, moving from fact a is shared by both d and e.  Hence you’re counting this cost twice.  This is why in this particular example, $h_{Add}$ proves to be inadmissible.

Ultimately, it’s no longer admissible because actions are being counted several times over when achieving our heuristic value.


#### $h_{Max}$ Heuristic
- $h_{Max}$ = The most expensive path to reach a given fact
- Admissible, given on most expensive path to achieve goal
- When costs are uniform i.e. =1, $h_{Max}$ is simply number of RPG layers

![[Pasted image 20221008191034.png]][1]

We’re only interested in just how expensive it was to reach that goal state.  Or in other words, we’re simply counting the max of all the heuristic values of the goal preconditions.

So we calculate as before, only this time when we reach the goal set and they’re satisfied, we simply pick the most expensive of the paths that reached our satisfied goal set.  Hence in this case, the value is 6.

Now this means that $h_{Max}$ is an admissible heuristic, because we’re assuming that by solving this, we’re also largely solving the rest of the planning problem.  But the thing is it’s not terribly informative.  It doesn’t tell us all that much about how far we are from the goal.  And one of the reasons for this is there is an implicit assumption here that the goals – or rather the actions require to satisfy them - interweave to a point that by basing it on the most expensive path, it is a safe bet that this is how long it will take us to satisfy all of the goals.

And that’s a problem as it is not all that accurate.  Especially once you have independent goals. 

If we have independent goals it means that the actions we need to achieve all of the goals don’t really overlap with one another.  So even in this trivial case, it’s relying on the assumption that all of our facts are on the same path.  Hence it’s still reasonably informative for us here.



---
## Footnote

Backlink: [[Optimising Classical Planning]]

Sources:
1. 
	- Name: Improving Search 07 - Building on RPG
	- Author: Tommy Thompson