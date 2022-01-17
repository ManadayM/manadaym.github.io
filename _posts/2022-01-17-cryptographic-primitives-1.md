---
layout: post
title: Cryptographic Primitives - 1 (Lecture - 3) - Blockchain Course Notes
---

Notes for the “Blockchain and its applications” course by IIT Kharagpur (Jan 2022 - Apr 2022).

<!--more-->

## Lecture Video

[Cryptographic Primitives - 1 (Week - 1, Lecture - 3)](https://youtu.be/uTsAiyZ_cZ4)

Topics covered in this lecture.

- Cryptographic primitives behind the Blockchain technology
    - Cryptographically Secure Hash Functions
    - Digital Signature
- Hash functions - Used to connect the “blocks” in a “chain” in a *temper-proof* way.
    - SHA-256
    - Hash functions characteristics - Puzzle Friendly

## Hash Function

Hash function is a mathematical function that takes an *arbitrary amount of data input* (M) and *produces a fixed-size output* called a hash value or just “hash”. It should be *efficiently computable*.

Such **general** hash function can be used to build hash tables, but they are not of much use in cryptocurrencies. We need Cryptographic Hash Functions for such use cases.

### Cryptographic Hash Functions

A Hash Function is cryptographically secure if it satisfies the following 3 security properties.

- **Collision-free** - Two different inputs can never produce same hash.
- **Diffusion, or Avalanche Effect** - A change in a single bit of the original input should result in change of half the bits of its hash.
- **Puzzle-friendly** - Given X and Y, find out k such that Y = H ( X \|\| k) - used to solve the mining puzzle in Bitcoin proof-of-work.

## References:

- [What are cryptographic hash functions?](https://www.synopsys.com/blogs/software-security/cryptographic-hash-functions)

- [Hash Table - Data Structures & Algorithms Tutorials In Python #5](https://youtu.be/ea8BRGxGmlA)

- [Intro to Cryptography and Cryptocurrencies, New Mexico University](https://www.cs.unm.edu/~saia/classes/591-Blockchains-s19/lec/lec1-crypto.pdf)
