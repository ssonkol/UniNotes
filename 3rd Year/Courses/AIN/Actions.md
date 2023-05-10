links: [[AI]], [[AIN]], [[Uni Courses]], [[Agents]]

tags: #OptionUncertainty #AI #Agent #flashcards #review #University #School #Actions #review 

---

# Actions
##### Simple Reflex Actions

With a simple reflex action, a simple agent maps each precept directly to an action.

This means we have to be able to make a correct decision based only on the current percept.

![[Pasted image 20220908193351.png]] [1]

###### Code
>function Simple-Reflex-Agent(precept) returns an action
>	Static: rules, a set of condition-action rules
>	state <-- Interpret-Input(precept)
>	rule <-- Rule-Match(state, rules)
>	action <-- rule. Action
>	return action

##### Agents with States and Goals

In this case, an agent with a state and goal contains;

- A new percept is interpreted in light of existing knowledge about the state
- Knowledge about the world is used to model inaccessible parts of the environment.
- Goal information is used to identify desirable states 

![[Pasted image 20220908201547.png]] [1]

##### Utility-based agents

**Utility** - A quantitative value that measures how "good" a state is.

![[Pasted image 20220908202143.png]] [1]

The utility of a state is a measure of the benefit or value of that state to a particular agent.

If a state is certain to come about, and if we can calculate the value of the state to an agent, then we can determine the utility of the state

In reality, it usually isn't easy to calculate the quantitative value of utility.

###### Expected Utilities

Most state are not certain to come about, but may only occur with some probability. Therefore, if we can calculate the utility of the state (S), and the probability that it will come about, we can calculate the **Expected Utility** of the state: 

![[Pasted image 20220908202726.png]] [1]

If we have more than one state, we assume to add up the pairs of probabilities multiplied by the utilities: 

![[Pasted image 20220908202741.png]] [1]

You can expect that summing up over all states might be very costly in terms of processing resources or time, due to the sheer number of states involved...

---

## Footnote

References :
1. 
	-  Name: 6CCS3AIN 2021-2022 Part A Introduction - McBurney - PDF
	- Accessed: 03/09/2022


Backlinks: [[Agents]]