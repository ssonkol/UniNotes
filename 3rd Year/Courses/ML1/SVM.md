# SVM
---
## Notes

This video explains parts 1-2 of the content on SVMs for week 5

Support Vector Machine is a supervised learning algorithm that  takes an object that we want to classify and puts it on a grid (n dimensional). SVMs then draw a line/plane in this graph that separates these data points/features so that all points of one category are on one side of the plane and all points of the other are on the other side.

SVM tries to find the plane that best separates the two categories by calculating the maximum distance between the data points on either category.![[Pasted image 20230213211432.png]]
The points that are closest to the separator are the support vectors.

### Convex Optimization Problem
![[Pasted image 20230213213537.png]]

This statement states that if we have an instance that is part of our positive class (y) then we want the equation to return a positive number (>=+1) and if we have an instance which is part of our negative class we want it to return a negative number(>=-1).
Also shown as: ![[Pasted image 20230213213630.png]]
Which define our margin.

To get our Plane/Line, we calculate the Euclidean distance between h1 and h2 and find the middle.






### The Kernel Trick
SVM tries to find a hyperplane between categories however data is not always easily separable.
Data will always be linearly separable if we map them into a space with enough dimensions

Kernel : This is the mapping from the input space x to the higher dimension space![[Pasted image 20230213212239.png]]

The advantage of using kernel functions is that we can compute what the dot product would be if we had actually projected the data.




---
Backlink: [[Kernel Machines]]
