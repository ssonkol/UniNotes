# Number Theory
Tag: #review 

---
## Definitions

---
## Notes

### Relative Prime Numbers & Greatest Common Factor
#### Prime Factorisation

Numbers:
- naturals N = {0, 1, 2, . . .},
- integers Z = {0, 1, −1, . . .}
- primes P = {2, 3, 5, 7, ...}
To factor a number a is to write it as a product of other numbers, e.g., a = b × c × d.

The prime factorization of a number a amounts to writing it as a product of powers of primes:![[Pasted image 20221117175640.png]][1]

#### Divisors
a (as long as it doesn't equal 0) divides b (a | b) if there is an m such that m x a = b

#### Greatest Common Divisor/Factor
Two natural numbers a, b are relatively prime if they have no common divisors/factors apart from 1, i.e., if their greatest common divisor gcd is equal to 1

For example, 8 and 15 are relatively prime since
- Factors of 8 are 1, 2, 4, 8
- Factors of 15 are 1, 3, 5, 15
- 1 is the only common factor

Conversely, we can determine the greatest common divisor by comparing their prime factorizations and using least powers, e.g.
- 150 = 2$^1$ × 3$^1$ × 5$^2$ and 18 = 2$^1$ × 3$^2$ , thus gcd(18, 150) = 2$^1$ × 3$^1$ × 5$^0$ = 6.
- 60 = 2$^2$ × 3 × 5 and 14 = 2 × 7, thus gcd(60, 14) = 2

### Euclid's Algorithm & Extended Euclid's Algorithm

gcd can be computed quickly using **Euclid's Algorithm**

- gcd(60,14) : 60 = (4 x 14) + 4
- gcd(14,4)   : 14 = (3 x 4) + 2
- gcd(4,2)     : 4  = 2 x 2

**Extended Euclid's Algorithm** computes x , y $\in$ Z such that
- gcd(a , b) = ($x$ x a) + (y x b)

Here 2 = 13-3x (60-(4 x 14)) = (-3 x 60) + (13 x 14)

#### Euclid's Algorithm
gcd(a, b) = gcd(b, a mod b) for any nonnegative integer a and any positive integer b.


##### Algorithm
![[Pasted image 20221117180817.png]][1]
##### Example
gcd(55, 22) = gcd(22, 55 mod 22) = gcd(22, 11) = 11

#### Extended Euclid Algorithm
Extend Euclid’s algorithm to compute integer coefficients x, y such that d = gcd(a, b) = (a × $x$) + (b × y)

##### Algorithm
![[Pasted image 20221117180930.png]][1]

where q = $\lfloor$a/b$\rfloor$ is the quotient of the division (for a = (q × b) + r)

##### Example
![[Pasted image 20221117181445.png]][1]

### Modular Arithmetics

#### Remainder
The remainder r happens when something isn't fully divisible 22/10 = 2 r2

#### Congruent Modulo

a, b ∈ Z are congruent modulo n, if a mod n = b mod n
We write this as a =$_n$b 

Reflexivity: a =$_n$a
Symmetry: If a =$_n$b then b =$_n$a
Transitivity: If (a =$_n$b and b =$_n$c) then a =$_n$c.

#### Other properties
![[Pasted image 20221117181851.png]][1]

**Example**
![[Pasted image 20221117181911.png]][1]

If a × b =$_n$a × c and a relatively prime to n, then b = $_n$c.

**Example**

8 x 4 = $_3$ 8 x 1
8 is relatively prime to 3
So: 4 =  $_3$ 1


![[Pasted image 20221117182133.png]][1]

![[Pasted image 20221117184027.png]][1]

![[Pasted image 20221117184132.png]][1]
To demonstrate the last point, if n | (a − b), then (a − b) = k × n for some k.
So we can write a = b + (k × n).
Therefore, (a mod n) = (remainder when b + (k × n) is divided by n) = (remainder when b is divided by n) = (b mod n).
![[Pasted image 20221117184206.png]][1]


### Modular Arithmetics: Two Theorems
![[Pasted image 20221117184307.png]][1]

#### Fermat's Little Theorem
![[Pasted image 20221117184321.png]][1]



### Euler Totient Function
When doing arithmetic modulo n.
- Complete set of residues is 0, . . . , n − 1.
- Reduced set of residues consists of those numbers (residues) that are relatively prime to n.
- For instance, for n = 10:
	- complete set of residues is {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
	- reduced set of residues is {1, 3, 7, 9}
- Number of elements in reduced set of residues is called the Euler Totient Function φ(n).
	- In other words, φ(n) is the number of positive integers less than n which are relatively prime to n, i.e., φ(n) is the number of a ∈ {1, 2, . . . , n − 1} with gcd(a, n) = 1
![[Pasted image 20221117184535.png]][1]

#### Properties
![[Pasted image 20221117184606.png]][1]

Euler's Theorem
![[Pasted image 20221117184625.png]][1]

Example
- If a = 3 and n = 10, then φ(10) = 4 and 3$^4$ = 81 =10$^1$
- If a = 2 and n = 11, then φ(11) = 10 and 2$^10$ = 1024 =11$^1$


---
## Footnotes
Backlink: [[Artificial Intelligence Planning Outline]]

Sources:
1. 
	- Name: [CIS-lec07.1: Some number theory](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355036)
	- Author: Luca Vigano
	- Date: 17/11/22