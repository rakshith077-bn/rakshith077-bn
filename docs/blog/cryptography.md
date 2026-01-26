title: Cryptography

The page aims to cover aspects covered by the author on the topic of the role of cryptography in theoretical computer science. 
- Demonstrate the cryptographic algorithms discussed and involved in developing a working algorithm of the RSA, Diffie-Helman and AES cryptographic protocols. 
- The page focuses on explaining the dependece of modern cryptography on the computational difficulty of inverting **one-way** functions, the the `P v/s NP` problem and other perspectives.

### Importance of Cryptography

 There are various aspects where cryptography takes an important role, concerning roles within & where privacy protection, data encryption, secure encryption, financial transactions, authentication and integrity, and national security is involved. But the fundamental bedrock of cryptographic protocols takes shape over a range of security measures employed to secure a specific type of operation, and involves providing confidentiality, integrity towards encryption and decryption.

### Major Complexity Classes

- `P`: Polynomial Time. 
- `NP`: Non-Deterministic Polynomial Time. 
- `NP-Complete`: The hardest problem in NP, to which all NP problems can be reduced in polynomial time.
- `NP-Hard`: Problems at least as hard as the hardest problem in **NP**. 
- `PSPACE`: Problems solvable using polynomial space, regardless of time. 
- `EXPTIME`: Problems solvable in exponential time. 
- `L` & `NL`: Where **L** refers to __Logarithmic space__ and **NL** refers to __Non-deterministic Logarithmic Space__. 
- `BPP`: Bounded-error probabilistic polynomial time. We cannot demonstrate that an encryption scheme (or any other type of cryptosystems) is secure just by running it.

If `P= N P` then one-way functions cannot exist. Based on the assumption that one-way functions take shape, one-way functions in cryptography are used in password hashing, message integrity, and cryptographic keys.

### The `P v/s NP` Problem

The concept of `P` vs `NP` stems from numerous theories of the `NP completeness`, the complexity based cryptography, as well as some practical consequences of building a constructive proof of the problem. Deriving it's root from the theory of complexity background, __Turing, Church, Godel__ and others during the 1930s. The primary question about the __NP__ class is condensed within another question namely, can every problem in __NP__ be solved in polynomial time? A common approach is that `NP != P` and is supported by the fact that factoring cryptographic algorithms remain unbroken till date because they, simply put - cannot be solved within polynomial time, bringing us to the fundamentals and the vertebrae of numerous cryptographic algorithms.

### Post Quantum Cryptography

Post-quantum cryptography is a specialized field within cryptography dedicated to crafting cryptographic systems that maintain their security even when faced with the formidable computational power of quantum computers. Post-quantum cryptography refers to the a field where the cryptography systems maintain their security even when attacks are launched with quantum computational power. Additionally there are quantum computing protocols often employ __quantum key distribution schemes__ namely __QKD__ protocol, __BB84__ protocol, __Ekert__ Protocol, __Falcon__ and __Di-Lithium__. 

### Exsisting Quantum Threats to Cryptographic Protocols

To understand the challenges of post quantum cryptography the need of awareness within the area of possible known attacks on classical and post quantum cryptographic protocols becomes critical. __Grover's__ algorithm, a very well known quantum algorithm that addresses an unsorted database. It can perform brute-force search attacks with that level of complexity that is the same square root of the number of items in the database. __Shor's__ algorithm, where the primary strength of the algorithm is its ability to factor large integers and solve discrete logarithmic problems.

### Cryptographic Protocols

#### Riverst, Shamir, and Adleman (RSA)

The RSA algorithm primarily relies on modular arithmetic. Also known as RSA algorithm, based on the factoring problem which involves multiplying two large prime numbers, which is easy. Factoring the product back into primes, obviously is computationally hard.

#### `Time Complexity of RSA`

The complexity of breaking the private key of RSA was concluded as `O(n4)`. The RSA takes various time complexity shapes, the generation of two prime numbers took the time complexity shape of `O(n2)`, where __n__ is the amount of prime numbers on that particular bit size. The **Euler's Totient** function of the multiplication of the two numbers is another `O(n2)`. Lastly, the computation of the inverse modulo of the co-prime with the extended euclidean algorithm has the time complexity of `O(logn)`. And computing the final time complexity involves $$ T(n) = n^{4} \cdot n^{2} + n \log n = n^{6} + n \log n = O(n^{6}) $$ We can also conclude that increasing the key size increases the security of the algorithm.

#### Advanced Encryption Standard

AES is a block cipher, at a high level it is a substitution-permutation network, with a block length of 128-Bits and allows for 192 bits, or 256 bits. The implemented AES algorithm illustrated only the encryption aspect due to time constraints. The core encryption flow of the algorithm namely, the **S-box** and __RoundConstant__ tables. However, the algorithm can generate a new key, use a default key or can also read a key from an external file. The Key Expansion takes a 128-bit secret key and expands it into 44 words (176 bytes) using the key schedule algorithms. Each round of encryption uses a different portion of this expanded key. 

The encryption process is as follows: 
- Consider for each 16-byte block the initial round performs a simple __XOR__ with the first round key followed by the 9 main rounds namely 
   - __SubBytes__ (Non-linear byte substitution using S-box), 
   - __ShiftRows__ (Cyclic shifting of rows), 
   - __MixColumns__ (Linear transformation mixing column data), 
   - __AddRoundKey__ (XOR with round-specific key).

#### One-Way Functions

The strength and the security of the AES protocol finds expression and strength in the aspect of pseudo random permutations, which are computationally indistinguishable from random permutations. A collection of adaptively 1-1 one way function is a family of 1-1 functions $$ \mathcal{F}_n = \{ f_{\text{tag}} : \{0, 1\}^n \mapsto \{0, 1\}^n \} $$, such that for every tag, it is hard to invert `ftag(r)` for a random __r__, even for an adversary that is granted access to an ”inversion oracle” for __ftag__, for every `tag != tag` thus making it hard to decrypt without the right key. **AES-128** works by encrypting a fixed block of 128-bits approximately takes the same amount of time for various sizes of inputs, thus the AES-128 can be termed as a `O(1)` for the encryption as well as the decryption options. When considering encryption and decryption of sizes larger than 128-bits, the time complexity yet remains the same and can be termed as `O(n)`, where __n__ is considered to be the size of the message to encrypt/decrypt.