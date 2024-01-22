---
title: Large Language Model (LLM)
description: Notes on Large Language Models aka LLMs.
pubDatetime: 2023-11-21T20:20:00
postSlug: large-language-model
featured: false
draft: false
tags:
  - LLM
---

![tp.web.random_picture](https://images.unsplash.com/photo-1458966480358-a0ac42de0a7a?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXJ8fHx8fHwxNzA1OTI2NjU5&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

Notes on Large Language Models aka LLMs.

## Table of contents

## Introduction

A large language model (LLM) is a type of language model that is designed to understand and generate language. LLMs are commonly trained with large amounts of data and computing resources. These models work by taking a text and predicting the next work accurately. Notable LLMs include OpenAI’s GPT-4, Meta’s LLaMa, Google’s PaLM and Anthropic’s Claude.

It's like a super smart computer program that has read a lot of books, websites, and other information. It can understand and generate human-like language, helping people by answering questions, providing information, and even chatting with them. It's a bit like having a really clever robot friend who knows whole bunch of stuff!

Essentially, it's a tool that can process and generate human-like text based on the patterns and information it learned during its training.

## Types of LLMs

### Base LLM

Base LLM predicts next word, based on text training data.

For example, If you write "once upon a time, there was a unicorn", then it may complete it by adding "that lived in a magical forest with all her unicorn friends".

But if you may prompt "what is the capital of France?" then it may answer with another set of questions like "what's France's largest city?" or "what is France's population?", etc. Because articles on the internet could quite possibly list such questions about the country of France.

### Instruction Tuned LLM

An instruction-tuned LLM has been trained to follow instructions.

## Model Limitations

### Hallucination

Makes statements that sound plausible but are not true.

**Reducing hallucinations**

Ask the model to first find the relevant information then answer the question based on the relevant information.
