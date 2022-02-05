---
layout: post
title: Cryptographic Primitives - 5 (Lecture - 7) - Blockchain Course Notes
---

Notes for the “Blockchain and its applications” course by IIT Kharagpur (Jan 2022 - Apr 2022).

<!--more-->

## Lecture Video

[Cryptographic Primitives - 5 (Week - 2, Lecture - 7)](https://youtu.be/qzsJv34xW-8)

Topics covered in this lecture.

- RSA Encryption and Decryption
- Digital Signature
- Hashing and Digital Signature

## Co-prime Numbers

- Co-prime numbers are pairs of numbers that do not have any common factor other than 1.
- There should be a minimum of two numbers to form a set of co-prime numbers.
- Such numbers have only 1 as their highest common factor (HCF) or greatest common denominator (GCD).

## Euler’s Totient Function

- It is represented as `phi` or ``⏀(n)``.
- It is defined as number of +ve integers less than ``n`` that are co-prime to ``n``.

## RSA Encryption Decryption

### Key Selection

- Select 2 prime numbers: ``p = 17``, ``q = 11``.
- Calculate ``n = p * q = 17 * 11 = 187``.
- Calculate ``⏀(n)  = (p - 1) * (q - 1) = 16 * 10 = 160``.
- Select ``e`` such that ``e`` is relatively prime or co-prime to ``⏀(n) = 160`` and less than ``⏀(n)``. Let ``e = 7``.
- Determine ``d`` such that ``d * e = 1 mod 160`` and ``d < 160``; Can determine ``d = 23`` since ``23 * 7 = 161 = 1 * 160 + 1``.

In the above example, ``e`` and ``n`` forms the private key and public key.

### Example
![Screenshot 1]({{ site.url }}/public/images/2022-02-03-cryptographic-primitives-5/screen-1.png)

## Digital Signature in Blockchain

- Used to validate the origin of a transaction
    - Prevent non-repudiation
        - Alice cannot deny her own transactions
        - No one else can claim Alice’s transaction as his/her own transaction
- Bitcoin uses Elliptic Curve Digital Signature Algorithm (ECDSA)

## References

- [YouTube Video on Euler’s Totient Function by Abhishek Sharma (Hindi)](https://youtu.be/ZBkpYKGPHUs)
