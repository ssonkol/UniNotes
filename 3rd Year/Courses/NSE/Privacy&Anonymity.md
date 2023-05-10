# Privacy&Anonymity
---

Privacy: A state in which one is not observed or disturbed by others
Anonymity: A state of not being identifiable within a set of subjects

### Anonymity 

Note-  you are only anonymous within a group if your actions cannot be distinguished from the actions of anyone else in the group - We call the group an **anonymity set**

You cannot be anonymous by yourself
- This is the big difference between anonymity and confidentiality
- Thus the best case is when a service has many users

To be anonymous, we must have no link between action and identity - this is called unlinkability.

Unobservability - This is where the observer cannot even tell whether a certain action took place or not.
- However this is normally hard  to achieve

**Attacks on Anonymity**
- Passive traffic analysis - This means you are now viewing other people's sensitive information e.g. IP, destination
- Active Traffic Analysis -
- Compromise of Network Nodes (routers)
	- An attacker may passively be logging traffic
	- Which is why we assume that some fraction of nodes are good - although we don't know which ones.

#### Unobservability/Anonymity
To achieve unobservability, we must anonymise the sender and/or the receiver.
- There might be linkage to actual identities only in restricted cases

We might use pseudonyms - but these sometimes need to be resolved into proper underlying names

##### Sender/recipient anonymity: proxies
Proxy - provides a gateway between users and the internet.
- Thus helping prevent cyber attackers from entering a private network.

Weakness:
- Proxy knows everything thus traffic analysis is possible
	-  We can get around this with cascaded proxy chains, mix networks etc.

###### Cascaded Proxies with encryption
1. We assume the client shares a key with a proxy
	1. The single proxy solution is ![[Pasted image 20230507210019.png]]
2. $K_p(M,S)$: Client C encrypts message M for proxy using proxy's public key $K_p$ along with server address S
3. Generalise to a chain of proxies with cascaded encryption![[Pasted image 20230507210152.png]]
**Why is it an improvement?**
Each proxy only knows the previous/next hop thus one uncompromised proxy is enough.
- But traffic analysis is still possible

#### Applications of privacy and anonymity
- Privacy
	- Hide online transactions
	- Web Browsing - Intrusive governments or archivists
- Untraceable Email
	- Corporate whistle blowers
	- Political dissidents
	- Confidential Business Negotiations
- Digital Cash
	- Electronic Currency
- Anonymous electronic voting
- Censorship-resistant publishing

### Mix Networks

#### Single Mix
Mix - A server that processes (mail) items

It is used for sending a message M to an agent at address B![[Pasted image 20230507210924.png]]
- Input the Mix on the left hand side of -> 
- Mix generates an output on the right hand side and sends the first component to B
- $r_i$ are padding strings of random bits

##### How to Foil Traffic Analysis
1. Agents/mixes work with uniformly sized items
	- i.e. messages split (or padded) into fixed size blocks
2. Order of arrival is hidden by outputting items in batches
	- You can used fixed ordering or random ordering
3. Repeated information must be blocked
	- Mixes must filter duplicates, cross checking across batches
	- Or string r includes a time stamp
4. Sufficient traffic from a large anonymity set is required
	- Few clients sending entails weak anonymity
	- The solution involves clients regularly sending and receiving dummy messages
![[Pasted image 20230507211411.png]]


#### Generating Receipts
If needed, a mix can return a receipt Y for messages received ![[Pasted image 20230507211527.png]]
where c is some large, unknown constant (e.g. a string of zeros)

The participant can later prove he sent the message by supplying ![[Pasted image 20230507211605.png]] as well as a retained string $r_1$

The verifying receipt is: ![[Pasted image 20230507211648.png]]
Weakness:
- If you compromise a single mix, you know everything
	- Although the weakness is lessened by forming Mix Networks (or cascade)

#### Mix Network
This is where messages are sent through a sequence of mixes.

Each mix is in a different 'administrative domain'
- Some mixes may be controlled by an attacker, but even a single good mix guarantees anonymity
![[Pasted image 20230507211946.png]]
Here, Alice (sender) chooses a Mix-path to Bob (receiver). Alice encrypts the message for every mix along the way.


##### Cryptographic Details.

1. Sender prepares item for every Mix in cascade, e.g. with n Mixes:![[Pasted image 20230507212159.png]]
2. Each Mix Peals off (decrypts) outermost layers, forwarding the result![[Pasted image 20230507212206.png]]
3. Final Mix processes the same data as in single-Mix cases![[Pasted image 20230507212213.png]]
##### Untraceable return addresses

To respond to an anonymous sender x with a return message M'
A single Mix case (with key $pk_{mix_{1}}$)
1. Sender includes "return address": ![[Pasted image 20230507212446.png]]
	- $r_1$ is a random string that can also be used as a shared key
	- $pk_x$ is a fresh public key, created for this purpose
	- $A_x$ is x's actual address
2. The receiver sends the "response" Mix: ![[Pasted image 20230507212612.png]]
3. The "response" Mix transforms this to ![[Pasted image 20230507212644.png]]
	- We send the second part to $A_x$

This way only the original sender can decrypt as he created both $pk_x$ and $r_1$

##### Return Addresses  - general case
- General return addresses of single Mix case![[Pasted image 20230507213141.png]]
- Recipient sends following response to the 1st return/response Mix ![[Pasted image 20230507213148.png]]
- Result of 1st Return Mix is ![[Pasted image 20230507213156.png]]
- Final result after n-1 mixes is ![[Pasted image 20230507213203.png]]

#### Mix Network Attacks

**Tracing a message**
![[Pasted image 20230507213231.png]]
Tracing a message

![[Pasted image 20230507213258.png]]
Tracing a message is prevented by dummy message

**Replay Attack**
![[Pasted image 20230507213434.png]]
Replay attack


![[Pasted image 20230507213449.png]]
Replay Attack is prevented by a replay filter

#### N-1 attack
Question: What happens if an attacker knows (e.g. has sent himself) n-1 of the n messages input to a mix.

This is performed by flooding a node with fake messages alongside a single message to be traced.

The attacker can recognise her messages and therefore link the sender with the receiver of the single message under surveillance. 
This is an active attack.

Countermeasures:
- Heartbeat Messages - Individual mixes being aware of their network environment and their state of connectivity with it by sending anonymous messages through the network back to themselves.
	- When a mix is under attack it cannot directly detect how much of the traffic it receives is genuine or simply the attacker's flooding traffic. Thus the mix tries to estimate the amount of flooding traffic from the rate of heartbeat messages and injects dummy traffic in order to artificially increase the anonymity provided to honest messages.

The key intuition for understanding the properties of RGBmixes is that the different colours of the traffic can only be observed by the mix itself.

Advantages:
- Very high degree of anonymity
	- No correlation between Mix input and output
	- Only some nonzero fraction of mixes need to be honest
	- With enough dummy traffic, the anonymity set is entire network
- Cryptography used in a novel way
	- With anonymous response, sender is anonymous even to the receiver
	- It can also be used for anonymous "certified mail" where the receipt is signed by the receiver and every Mix along the path.


Disadvantages:
- Public key encryption and decryption at each mix can be computationally expensive
- Dummy overhead
- High latency - It's okay for email but not for anonymous web browsing


### Dining Cryptographers (DC)

Three cryptographers are having dinner
- Either NSA is paying for the dinner, one of them is paying but wishes to remain anoymous.
1. Each diner flips a coin and shows it to his left neighbour
	- Every diner will see two coins, his own and his right neighbours
2. Each diner announces whether the two coins are the same
- If he is the payer, he lies (says the opposite)
3. If there are odd number of "same" => NSA is paying
4. If there are evenn number of "same" ==> one of them is paying
5. But a non-payer cannot tell which of the other two is paying



