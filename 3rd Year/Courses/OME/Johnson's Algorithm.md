# Johnson's Algorithm
---
## Notes

Johnson's Algorithm is used so we can run Dijkstra's algorithm on a graph with negative edges.
Remember though!!!! This algorithm can not handle negative cycles in a graph

Steps:
1. Compute new edge weights
2. Run Bellman Ford once to compute all vertices
	1. If the algorithm returns false, then there is a negative cycle and we stop the whole thing
3. Otherwise
	1. Store all vertex weights 
	2. Use the computed edges from Bellman Ford for re-weighting edges using the formula ![[Pasted image 20230202154307.png]]
	3. Once done, run Dijkstra's algorithm
4. Return the graph

This algorithm has an average runnig time of ![[Pasted image 20230202154413.png]]

---
Backlink: [[ShortPaths&GeoPaths]]