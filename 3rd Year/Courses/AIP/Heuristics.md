Tags: #review #AIP #AI #Planning

---
# Heuristics
---
## Definitions
Heuristic
> A heuristic, or heuristic technique, is any approach to problem solving or self-discovery that employs a practical method that is not guaranteed to be optimal, perfect, or rational, but is nevertheless sufficient for reaching an immediate, short-term goal or approximation. [1]


## Notes 

##### Heuristic Search Planning
- We need to establish a heuristic of a problem space which tells us information about how close we are to the goal (denoted as $h$)
- We also need to know how far we have travelled (denoted as $g$), this is the **cost** of everything we have done to reach this point

Depending on the algorithm we can exploit $g$ and $h$ to help us prioritise how to explore the problem space.

Examples: 
> Uniform Cost Search expands open nodes with the lowest $g$ value, which Best First Search uses the $h$ value.
> We can combine these in A* Search to achieve a much more effective technique.

---
## Footnote
Backlink : [[Optimising Classical Planning]]

Resources: 
1. Source: Wikipedia
	1. Link: https://en.wikipedia.org/wiki/Heuristic
	2. Accessed: 02/10/22