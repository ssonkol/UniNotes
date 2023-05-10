# Feistel Cipher
Tag: #review 

---
## Definitions

## Notes
Many symmetric block encryption algorithms in current use are based on the **Feistel Block Cipher**.

You can review the [[Block Cipher]].

### Feistel Cipher

Basing off of [[Composite Ciphers]], Feistel Cipher is a practical application to develop a product cipher that alternates confusion and diffusion functions.

Product Ciphers chain combinations of substitutions and transpositions.
- S-Boxes 'Confuse' input bits
- P-Boxes 'diffuse' bits across S-Box inputs

*Note that permutation doesn't directly equate with diffusion (permutation, by itself, doesn't change the statistics of the plaintext at the level of individual letters or permuted blocks)*![[Pasted image 20221020202037.png]][1]

#### Feistel Encryption/Decryption

In a nutshell we:
- Partition the input block into two halves
- Process through multiple rounds which
	- Perform a substitution on the left data half
	- Then have permutation swapping halves
![[Pasted image 20221020202231.png]][1]

##### Encryption Detail

**Encryption Input:**
- 2 $w$-bit plaintext block
- key $K$

**Plaintext block divided into 2 halves** $LE_0$ and $RE_0$ which;
- Pass through $n$ rounds of processing (in the above example $n = 16$)
- Combine the 2 halves to produce ciphertext block

Each round $i$ has inputs:
- $LE_{i-1}$ and $RE_{i-1}$ derived from the previous round
- Subkey $K_i$ is derived from overall $K$

Subkeys $K_i$ are different from $K$ and each other.![[Pasted image 20221020203809.png]][1]

A substitution is performed on $LE_i$ by applying a round function $F$ to $RE_i$ and then XORing the output with $LE_i$

$F$ has the same general structure for each round but is parameterized by the round subkey $K_i$ 

$F(RE_{i},K_{i+1}):$ $w$ bits x ${y}$ bits $\rightarrow W$ bits

Then a permutation is performed - which is the interchange of two halves of data.

The final round is followed by an interchange that undoes interchange that is part of the final round (to simplify decryption).![[Pasted image 20221020203833.png]][1]

###### Parameters & Design Features of Feistel Cipher

**Block Size:**
- Larger means greater security but reduced en/de-cryption speed
- Larger security achieved by greater diffusion
- Traditionally: 64-bit blocks is a reasonable trade-off

**Key Size:**
- Larger size increases security but may decrease en-/de-cryption speed
- Greater security achieved by greater resistance to brute-force attacks and greater confusion
- Keys 64 bits or less are now inadequate
	- 128 bits has become a common size

**Number of Rounds:**
- Single round offers inadequate security
- Multiple rounds offer increasing security 
	- typical size: 16 rounds

**Subkey generation algorithm:**
- Greater complexity means greater resistance to cryptanalysis

**Round function** F:
- Greater complexity means greater resistance to cryptanalysis

##### Decryption Detail

Decryption is essentially the same as encryption

**Decryption Input**:
- Ciphertext
- Subkeys $K_i$ in reverse order ($K_n$ to $K_1$)

**Intermediate Value** of  decryption process
	$LD_{16-I} || RD_{16-i} = RE_{i} || LE_i$
equal to the corresponding value of the encryption process with two halves of value swapped
	$LE_{i}||RE_i$
![[Pasted image 20221020204207.png]]
![[Pasted image 20221020204221.png]][2]

#### General Encryption/Decryption Rounds

One of the main strengths of the Feistel Cipher is that each round of encryption or decryption has the following general shape.![[Pasted image 20221020204326.png]][2]

where the only difference is that:
- At encryption round $i$, the key $K_i$ is used
- At decryption round $i$, the key $K_{17-i}$ is used 
	- For decryption we take the keys in revers order


###### The Math behind it...

Let's take the ciphertext...
	$LD_{17} || RD_{17} = RE_{16} || LE_{16}$
And use it as input to the same algorithm.

- Assume that $LD_{0} = RE_{16}$ and that $RD_{0} = LE_{16}$

We need to show that the output of decryption round 1 is equal to $w$-bit swap of input encryption round 16.![[Pasted image 20221020205613.png]][2]

**Encryption Side**
![[Pasted image 20221020205507.png]][2]

**Decryption Side**
![[Pasted image 20221020205527.png]][2]
Hence...![[Pasted image 20221020205540.png]][2]


- Inputs to the $i^{th}$ iteration of encryption can be recast as a function of the outputs:
		![[Pasted image 20221020205730.png]][2]
	Rearranging terms around...
		![[Pasted image 20221020205801.png]][2]

Finally, output of the last round of decryption is $RE_0||LE_0$

A $w$-bit swap covers the original plaintext.

###### General Result

In general, for $1 \le i \le 16$, we can prove that the output of decryption round $16-i$ is equal to the $w$-bit swap of the input to encryption round $i+1$ 

In other terms we can prove the equation
$LD_{16-I} || RD_{16-i} = RE_{i} || LE_i$
for $1 \le i \le 16$

- We carry out the proof by induction, by assuming that we have already proved that the output od the decryption round $16-i-1 = 15-i$ is equal to the $w$-bit swap of the input to encryption round $i+1+1 = i+1$
- Then showing that the output of decryption round $16-i$ is equal to $w$-bit swap of the input to encryption round $i+1$:

As seen below:![[Pasted image 20221020210322.png]][2]

###### Specific Example

Consider encryption round 15, corresponding to decryption round 2...![[Pasted image 20221020210417.png]][2]

Suppose that
- 32-bit blocks (two 16-bit halves)
- 24-bit key
- At the end of encryption round 14, the value of the intermediate block (in hexadecimal) is DE7F03A6
- Value of $K_{15}$ is 12DE52

The $LE_{15} =$ 03A6 = $RD_1$ and $RE_{15} = F(03A6, 12DE52) \oplus DE7F = LD_1$

We prove that $LD_{2}= RE_{14} = 03A6$ and $RD_{2}= LE{14} = DE7F$![[Pasted image 20221020210858.png]][2]


----
## Footnotes

Links: [[Ciphers]], [[Composite Ciphers]]

Sources:

1. 
	- Name: [CIS-lec04.2: Composite (product) ciphers and the Feistel Cipher (part 1/2)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355005)
	- Author: Luca Vigano
	- Date: 20/10/22
2. 
	- Name: [CIS-lec04.3: The Feistel Cipher (part 2/2)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6355007)
	- Author: Luca Vigano
	- Date: 20/10/22

