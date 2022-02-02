---
layout: post
title: Cryptographic Primitives - 4 (Lecture - 6) - Blockchain Course Notes
---

Notes for the “Blockchain and its applications” course by IIT Kharagpur (Jan 2022 - Apr 2022).

<!--more-->

## Lecture Video

[Cryptographic Primitives - 4 (Week - 2, Lecture - 6)](https://youtu.be/HOXq7mLjhBU)

Topics covered in this lecture.

- Basics of Cryptography
- Public Key Cryptography
- Encryption and Decryption using Public Key Cryptography
- Digital Signature

## Digital Signature

A digital code, which can be included with an electronically transmitted document to verify

- The content of the document is authenticated
- The identity of the sender
- Prevent **non-repudiation** — sender will not be able to deny about the origin of the document.

Only the **signing authority** can sign a document, but everyone can verify the signature.

Signature is **associated with** the particular document — signature of one doc cannot be transferred to another.

## Properties of Public Key Cryptography

- Truly random.
- Sufficient length key.
- Sufficient entropy — All the bits in the key should be equally random.

## Public Key Encryption - RSA

RSA stands for **Rivest—Shamir—Adleman**.

### Phases

- Key Generation
- Key Distribution
- Encryption
- Decryption
