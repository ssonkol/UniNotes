# Dijkstra for Geo Problems
---

## Notes

We normally run Dijkstra from a source node and find all shortest paths for all vertices.
But what if we wanted to reduce calculation time by just setting the target to only find the destination vertex we are looking for?

At most, we will compute the whole graph, otherwise we will compute less.

We do this by using re-weighting of edges to favour edges leading "geographically" closer to the destination.

In other words, if it's closer to the destination then the re-weighting will promote this path and make Dijkstra follow the closer path..

The weighting H(v) instead is -distance(v, d) where distance(v, d) is the straight-line distance from node v to destination d (Euclidean distance).

Thus the weighting formula used is ![[Pasted image 20230202165220.png]]

For example:
![[Pasted image 20230202165246.png]]



---
Backlink: [[ShortPaths&GeoPaths]]
