# Dijkstra2AStar
---

## Notes

Say we have a huge graph that is just too big to even input into Dijkstra and use the original pure algorithm.

So lets use estimates b(c) which estimate the cost of getting from c to the target t 

From here we:
1. Re-weight using the estimates![[Pasted image 20230202170243.png]]
2. Run variation of Dijkstra's Algorithm - A* Algorithm
	1. For each node we compute for the shortest path estimate - add it to the set S
	2. When considering the next node and it has a negative weight, this will mean the shortest-path estimate is reduced
	3. If this happens then the new node we were thinking of adding to the set S will be removed from the set and put back onto the priority queue Q



---
Backlink: [[ShortPaths&GeoPaths]]