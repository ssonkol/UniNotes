# Perceptron
---
## Notes
As the simplest type of ANN, a perceptron consists of a single neuron.

The input of the neuron is the weighted sum of the inputs plus the bias term and the output is some function of the input

A perceptron is able to compute linearly separable functions.

![[Pasted image 20230303192211.png]]
- x1, x2 are inputs 
- w1,w2 are synaptic weights; wo is a bias weight
- th is the threshold
- s is the dot product of the input x and the weight (w) vectors plus the bias ![[Pasted image 20230303192228.png]]
- g is a transfer/threshold/activation function applied to s

### Transfer/Threshold Functions

- Sign function
![[Pasted image 20230303195242.png]]
![[Pasted image 20230303195247.png]]



- Step
![[Pasted image 20230303195226.png]]

- Sigmoid function![[Pasted image 20230303195039.png]]
![[Pasted image 20230303195054.png]]

- Hyperbolic function
![[Pasted image 20230303195114.png]]

![[Pasted image 20230303195126.png]]



A perceptron can compute linearly separable functions.
Simply using the step function, we can have for example:
![[Pasted image 20230303195407.png]]



### Single Layer network
A single layer network is usually used for a Two class classifier (1, -1)

If the data is linearly separable, then the error correction method will find the linear boundary between classes

- The idea is to find the weights w0 to wn so than the members of one class all have value 1 and the members of the other all have the value -1.

#### Error Correction Method

We train a perceptron by adjusting its weights:
- Start with random weights
- Repeat until the stop condition is met
	- Update the weight by ![[Pasted image 20230303210045.png]]
	- a is the learning rate
	- t is the target output for the network
	- g(s) is the prediction produced by the neural network

By training to +/-1 we are implicitly using the sign function


---
Backlink: [[Neural Networks]]