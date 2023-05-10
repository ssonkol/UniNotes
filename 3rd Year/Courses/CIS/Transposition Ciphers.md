# Transposition Ciphers
## Definitions

**Transposition Cipher**
>Perform some sort of permutation on the plaintext letters. Works on blocks of letters of the plaintext.

## Notes

Formally:

- For block length $t$, let $K$ be the set of permutations on ${1, . . . , t}$.
- For each $e ∈ K$ and $m ∈ M$
	$E_{e}(m) = m_{e(1)} m_{e(2)} · · · m_{e(t)}$

- The set of all such transformations is called a transposition cipher.

To decrypt $c = c_1 c_2 · · · c_t$ compute _D_{d (c) = cd(1) cd(2) · · · cd(t)_ , where $d$ is inverse permutation.

Below are a list of Transposition Ciphers:
- [[Rail Fence Cipher]]
- [[Rotating Grilles]]
- [[Multiple-Stage Columnar Transposition Cipher]]

## Questions
![[Pasted image 20221015162018.png]][1]

---
## Footnote

Backlink: [[Ciphers]]

Sources:
1.
	- Name: [CIS-lec03.4: Transposition ciphers (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354995)
	- Author: Luca Vigano
	- Date: 15/10/12
