---
sr-due: 2022-10-13
sr-interval: 3
sr-ease: 250
---

Tag: #review 


# Dual Heuristics

## Notes

### Combining Heuristics
If we had two heuristics  -  in this example both estimating the distance and/or cost to the goal

We could have two open lists...
1. One for each heuristic and alternate between them.
2. Then evaluate successors with both heuristics and put on both open lists.

##### Why use two or more heuristics?

1. If one heuristic is on a plateau:
	1. Plateau successors put on both open lists
	2. Second open list will order them by second heuristic so it will guide the search on the plateau
	>If we hit a plateau, whereby there’s no obvious next state to explore given all of the heuristics have stagnated at the same value, we could use the second heuristic to help us find a way out of the heuristic?

2. In any case - diversification by avoiding expanding just the states one heuristic likes

### Local Search

The procedure is as follows
1. Start with a state $S$
2. Expand $S$, generating successors
3. $S' =$ one of these successors
4. $S = S'$ and repeat
 
 The idea of the ‘best’ successor, is what is governed by the heuristic.
 We’re only interested in small, local optimisations that we make near where we are.

When using Local Search there are two aspects we need to focus on:
- **Diversification** - Try lots of different things, to try to brute-force around the weakness of the heuristic
- **Intensification**- Explore lots of options around a given state (near where the goal might be)

Local search is a balancing act
- Long probes = good for diversification
- Short probes = good for intensification


### Indentidem 
As an alternative to EHC (mentioned in [[Improving Search - Planning]])
1. Replace systematic search on plateaux with local-search with restarts
2. As in EHC: record the best state seen so far
	1. When expanding a state $S$ at the route of a plateau:
		1. Choose one successor, at random, even if it's not better than the best seen so far 
			- It's not since we're on a plateau
3. If more than $d$ steps since the best state ($d$ is the probe depth)
	1. Jump back and search from there again

![[Pasted image 20221008183450.png]][1]

![[Pasted image 20221008183708.png]][1]

Instead, we’re now reliant on this more structured local search through the plateau.  This will cut down on excessive exploration that doesn’t yield improvement in the best case and in the worst case it will prove no better than breadth first search.

##### Successor Selection
In Indentidem, roulette selection is used.

Once this evaluation is completed, we use a roulette wheel selection process: whereby if you think of it as a wheel that you spin for the selected region, the size of region of the wheel a given state has is biased based on the heuristic value, with the lowest having the largest segment.  Having three to pick from at random has proven to work quite effectively, given we still achieve some diversification since there is randomness still being employed here.

![[Pasted image 20221008185053.png]][1]

Indentidem performs better than FF (mentioned in [[Improving Search - Planning]]) most of the time.
- Systematic search is better in some domains
- Sometimes the parameters need changing
	- Random sample size, depth bound, whether to use roulette selection...
## Questions

---
## Footnote

Backlink: [[Optimising Classical Planning]]

Sources:
1. 
	- Name: Improving Search 06 - Dual Open List Search
	- Author: Tommy Thompson