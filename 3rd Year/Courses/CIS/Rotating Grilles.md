# Rotating Grilles
Tag: #review 

---
## Definitions

**Transposition Cipher**
>Perform some sort of permutation on the plaintext letters. Works on blocks of letters of the plaintext.

---
## Notes
Using a mask (grille) with pre-cut holes
- Encoder writes plaintext in holes, removes mask, fills remainder with blind text, retaining appearance of an innocuous message.
- Decryption: recipient must possess an identical mask (or must know spacing that created it).
![[Pasted image 20221015160826.png]][1]

#### Rotating Grille

An example can better explain this:
> - 6 × 6 grid of squares, of which 9 are cut out.
> - Plaintext: The Lord is my shepherd. I shall not be in want.
> - Write first 9 letters in each square cut out, left to right, top to bottom.
> - Turn grille by 90◦ in predetermined direction (e.g., counter clockwise).
> - Write next 9 letters... until grille is filled. Read ciphertext (left to right, top to bottom):

mtdhyeisthlbesoehpirhadnelwrailnnsot.

![[Pasted image 20221015161046.png]]

To decipher, write the ciphertext in a 6 x 6 grid and use this rotating grid.

###### Procedure to select squares of the grille to be cut out
- Divide grid in 3 × 3 quadrants, number squares of each quadrant
- Among four squares numbered “1”, select one to be cut out (e.g., rightmost square of top row) to ensure that each of these four squares is exposed exactly once during enciphering
- Among four squares numbered “2”, one is selected to be cut out...

![[Pasted image 20221015161253.png]][1]
By choosing thus exactly one square to be cut out from among the four squares bearing the same number, it can be ensured that each square can be filled at one of the four rotating positions.

## Questions


---
## Footnote

Backlink: [[Transposition Ciphers]]

Sources:
1.
	- Name: [CIS-lec03.4: Transposition ciphers (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354995)
	- Author: Luca Vigano
	- Date: 15/10/12
