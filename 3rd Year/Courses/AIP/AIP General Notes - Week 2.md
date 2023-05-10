tags: #review

---

# AIP General Notes - Week 2

###### A* search 

$f(S) = g(S) + h(S)$

The heuristic has to be admissible e.g. it can't overestimate

However RPG isn't admissible 

Consistent (monotonic): $h(s) <= h('S) + d(S,'S)$
 $'S$ means a successor 

heuristic $h(S)$ is either less than or equal to the successor's heuristic + the distance between S and its successor (usually a value of 1)


##### Sussman Anomaly 
This is referring to questions 2a and 2b in the Tutorial exercise for week 1

You would most likely encounter the Sussman Anomaly...

This can actually make a solution plan worse

non-interleaved planning



---
## Footnote
Backlink: [[AIP]]
 