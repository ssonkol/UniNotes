# AIN - Week 1
 # AIN - Week 1
### Question 1
![[Pasted image 20220925114726.png]] 

#### Answer
> An example of an agent is the robot from iRobot.
> a) It has visual sensors (cameras for eyes)
> b) It can run, jump, climb, talk (i.e. same human actions)
> c) It operates in a real-time environment i.e. non-deterministic and dynamic

### Question 2
![[Pasted image 20220925114827.png]] 

#### Answer
> I would classify the environment as dynamic, non-deterministic and continuous as the environment is always changing, never the same and never really follows a set pattern (although some may argue that you can find a pattern in everything)


### Question 3
![[Pasted image 20220925114859.png]]

#### Answer
>Another agent could be a robotic vacuum cleaner
>a) It has visual/laser sensors
>b) It can move in all x and z axis
>c) It operates in an accessible, static and deterministic environment
>	i) this is because the robot only has to find dirt or move to another location... therefore it will only have a maximum of 3 general states (clean, move, rest)

### Question 4
![[Pasted image 20220925114941.png]]
![[Pasted image 20220925114925.png]]
#### Answer
### Question 5
![[Pasted image 20220925114954.png]]
#### Answer
> while (not in state (clean)){
> 	clean square
> 	move forward 
> 	if obstacle present forward (turn left)
> 	else if obstacle present 
> }
> # have the robot turn left, right or 180.

### Question 6
![[Pasted image 20220925115005.png]]
#### Answer
We can then instead make sure it cleans every quadrant its in.
If it can't detect an obstacle then let the obstacle try move - if it can't then it must turn around.

---
## Footnote
Backlink: [[AIN]]