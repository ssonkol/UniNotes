# Substitution Ciphers
Tag: #review 

---
## Definitions

**Substitution Cipher**
> This is a cipher in which the letters of plaintext  are replaced by other letters or by numbers or symbols.

---
## Notes

As explained by the definition of a substitution cipher - If the plaintext is viewed as a sequence of bits, then substitution involves replacing plaintext bit patterns with ciphertext bit patterns.

Some examples of substitution ciphers include:
> - **Caesar Cipher**: Each plaintext character is replaced by character 3 to the right modulo 26
> - **ROT13**: Shift each letter by 13 places (works well under Unix like systems)
> - **Alphanumeric**: Substitute numbers for letters

Below are a list of Substitution Ciphers:
- [[Caesar Cipher]]
- [[Mono-Alphabetic Substitution Ciphers]]
- [[Homophonic Substitution Ciphers]]
- [[Playfair Cipher]]
- [[Polyalphabetic Substitution Ciphers]]
- [[Vernam Cipher]]
- [[One-Time Pad]]

### Cons of Substitution Ciphers

- Substitution ciphers are easy to crack using frequency analysis (letters, diagram, etc.)

Example:

>Given ciphertext: UZQSOVUOHXMOPVGPOZPEVSGZWSZOPFPESXUDBMETSXAIZ VUEPHZHMDZSHZOWSFPAPPDTSVPQUZWYMXUZUHSX EPYEPOPDZSZUFPOMBZWPFUPZHMDJUDTMOHMQ 
>
>- Count relative letter frequencies
>- Since P and Z occur most frequently, guess they correspond to E and T respectively
>- Count relative digram (a sequence of 2 letters, a.k.a. digraph) frequencies
>- Since ZW occurs most frequently, guess it corresponds to TH (which is the digram occurring most frequently in English)
>- Hence ZWP is THE.

>By proceeding with trial and error finally get: 
>	IT WAS DISCLOSED YESTERDAY THAT SEVERAL INFORMAL BUT DIRECT CONTACTS HAVE BEEN MADE WITH POLITICAL REPRESENTATIVES OF THE VIET CONG IN MOSCOW

## Questions
![[Pasted image 20221015162051.png]]

---
## Footnote

Backlink: [[Ciphers]]

Sources:
1. 
	- Name: [CIS-lec03.1: Substitution ciphers — Caesar cipher and mono-alphabetic substitution ciphers (slides)File](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354989)
	- Author: Luca Vigano
	- Date: 15/10/22
2. 
	- Name: [CIS-lec03.2: Substitution ciphers — Homophonic substitution ciphers, Playfair cipher, Polyalphabetic substitution ciphers (Vigenère cipher) (slides)File](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354991)
	- Author: Luca Vigano
	- Date: 15/10/22
3. 
	- Name: [CIS-lec03.3: Substitution ciphers --- Vernam cipher, One-time pad (slides)File](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354993)
	- Author: Luca Vigano
	- Date: 15/10/12
4. 
	- Name: [CIS-lec03.4: Transposition ciphers (slides)](https://keats.kcl.ac.uk/mod/resource/view.php?id=6354995)
	- Author: Luca Vigano
	- Date: 15/10/12