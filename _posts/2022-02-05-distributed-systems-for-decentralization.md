---
layout: post
title: Distributed Systems for Decentralization (Lecture - 8) - Blockchain Course Notes
---

Notes for the “Blockchain and its applications” course by IIT Kharagpur (Jan 2022 - Apr 2022).

<!--more-->

## Lecture Video

[Distributed Systems for Decentralization (Week - 2, Lecture - 8)](https://youtu.be/CRsDmiX9-_k)

Topics covered in this lecture.

- Distributed Systems
- Blockchain as a Distributed System
- Distributed Consensus – A History

## Pillars of Blockchain System

- Distributed Systems
- Cryptography
- Economic Models

## Core Problem

Other nodes in the network need to agree on a new block added to the blockchain network. This is a Classical Distributed Consensus Problem.

- The Byzantine Behaviour

## FLP Impossibility Theorem

- Consensus is impossible in a fully asynchronous system even with a single crash fault.
- Cannot ensure **Safety** and **Liveness** together. Here, **Safety** means correct processes will yield the correct output and **Liveness** means the output will be produced within a finite amount of time (eventual termination).

## Paxos

### Consensus with Paxos

- Consensus is agreeing on **one** result.
- Once a **majority** agrees on a proposal, that is consensus.
- The reached consensus can be **eventually** known by everyone.
- The involved parties want to agree on **any** result, not on their proposal.
- Communication channels may be **faulty**, that is, messages can get lost.

### Paxos basics

- Three roles
    - **Proposers** - proposes values to reach consensus on.
    - **Acceptors** - who helps to reaching the consensus.
    - **Learners** - who learn the agreed upon value. They can be later queried for what their consensus value was.
- In practice, **Paxos nodes** can take multiple roles, even all of them.
- **Paxos nodes** must know how many **acceptors** a majority is.
- **Paxos nodes** must be persistent: they can’t forget what they accepted.
- A **Paxos run** aims at reaching a **single consensus**. Once a consensus is reached, it **cannot progress** to another consensus. In order to reach **another consensus**, a different **Paxos run** must happen.

## References

- [YouTube Video on The Paxos Algorithm by Luis Quesada Torres from Google](https://youtu.be/d7nAGI_NZPk)
