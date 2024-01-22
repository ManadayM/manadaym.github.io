---
title: Prompt Engineering
description: Prompt Engineering 101 and Prompt Engineering Best Practices.
pubDatetime: 2023-09-23T23:57:00
postSlug: prompt-engineering
featured: false
draft: false
tags:
  - LLM
---

![tp.web.random_picture](https://images.unsplash.com/photo-1503614472-8c93d56e92ce?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXJ8fHx8fHwxNzA1OTMwOTU4&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

Prompt Engineering 101 and Prompt Engineering Best Practices.

## Table of contents

## Introduction

Prompt Engineering involves human writing, refining, and optimising prompts in a structural way. This is done with the intention of perfecting the interaction b/w humans and AI to the highest degree possible.

A prompt engineer continuously monitors the prompts to see their effectiveness. Creating an effective prompt relies on a bunch of different factors. Below are some best practices for writing a good prompt.

## Best Practices

### Write Clear and Specific Instructions

- Write more details in our queries.
- Don't assume the AI knows what you are talking about. Some examples
  - "When is the election?" → "When is the next presidential election for Poland?".
  - "Tell me what this essay is about: < essay paragraph here>" → "Use bullet points to explain what this essay is about. Make sure each point is no longer than 10 words long. At the end write a summary about the essay in no more than 500 words.

### Use delimiters to clearly indicate distinct parts of the input

- Using delimiters like \`\`\`, \"\"\", \~\~\~, to clearly indicate distinct parts of your input.
- This helps in avoiding Prompt Injections.

> [!INFO] Prompt Injection
> A prompt injection is, if a user is allowed to add some input into your prompt, they might give kind of conflicting instructions to the model that might kind of make it follow user's instructions rather than what you wanted it to do.

```python
text = f"""
You should express what you want a model to do by \
providing instructions that are as clear and \
specific as you can possibly make them. \
This will guide the model towards the desired output, \
and reduce the chances of receiving irrelevant \
or incorrect responses. Don't confuse writing a \
clear prompt with writing a short prompt. \
In many cases, longer prompts provide more clarity \
and context for the model, which can lead to \
more detailed and relevant outputs.
"""
prompt = f"""
Summarize the text delimited by triple tildes \
into a single sentence.
~~~{text}~~~
"""
```

### Adopt a Persona

"Write a poem for the sister's high school graduation that will be read out to family and close friends." → "Write a poem as Helena. Helena is 25 years old and an amazing writer. Her writing style is similar to the famous 21st-century Rupi Kaur. Writing as Helena, write a poem for her 18 year old sister to celebrate her sister's high school graduation. This will be read out to friends and family at the gathering."

### Ask for structured output

- JSON, HTML, XML, etc.
- "Create a checklist for preparing for a job interview. "

```python
prompt = f"""
Generate a list of three made-up book titles along \
with their authors and geners.
Provide them in JSON format with the following keys:
book_id, title, author, genre.
"""
response = get_completion(prompt)
print(response)
```

### Ask the model to check whether conditions are satisfied

```python
# Example 1

text_1 = f"""
Making a cup of tea is easy! First, you need to get some \
water boiling. While that's happening, \
grab a cup and put a tea bag in it. Once the water is \
hot enough, just pour it over the tea bag. \
Let it sit for a bit so the tea can steep. After a \
few minutes, take out the tea bag. If you \
like, you can add some sugar or milk to taste. \
And that's it! You've got yourself a delicious \
cup of tea to enjoy.
"""
prompt = f"""
You will be provided with text delimited by triple quotes.
If it contains a sequence of instructions, \
re-write those instructions in the following format:

Step 1 - ...
Step 2 - …
…
Step N - …

If the text does not contain a sequence of instructions, \
then simply write \"No steps provided.\"

\"\"\"{text_1}\"\"\"
"""
response = get_completion(prompt)
print("Completion for Text 1:")
print(response)

# Output

# Completion for Text 1:
# Step 1 - Get some water boiling.
# Step 2 - Grab a cup and put a tea bag in it.
# Step 3 - Once the water is hot enough, pour it over the tea bag.
# Step 4 - Let the tea steep for a bit.
# Step 5 - After a few minutes, take out the tea bag.
# Step 6 - Add sugar or milk to taste, if desired.
# Step 7 - Enjoy your delicious cup of tea.

```

```python
# Example 2

text_2 = f"""
The sun is shining brightly today, and the birds are \
singing. It's a beautiful day to go for a \
walk in the park. The flowers are blooming, and the \
trees are swaying gently in the breeze. People \
are out and about, enjoying the lovely weather. \
Some are having picnics, while others are playing \
games or simply relaxing on the grass. It's a \
perfect day to spend time outdoors and appreciate the \
beauty of nature.
"""
prompt = f"""
You will be provided with text delimited by triple quotes.
If it contains a sequence of instructions, \
re-write those instructions in the following format:

Step 1 - ...
Step 2 - …
…
Step N - …

If the text does not contain a sequence of instructions, \
then simply write \"No steps provided.\"

\"\"\"{text_2}\"\"\"
"""
response = get_completion(prompt)
print("Completion for Text 2:")
print(response)

# Output

# Completion for Text 2:
# No steps provided.
```

### Few-shot Prompting

- Give successful examples of completing tasks
- Then ask the model to perform the task

```python
prompt = f"""
Your task is to answer in a consistent style.

<child>: Teach me about patience.

<grandparent>: The river that carves the deepest \
valley flows from a modest spring; the \
grandest symphony originates from a single note; \
the most intricate tapestry begins with a solitary thread.

<child>: Teach me about resilience.
"""
response = get_completion(prompt)
print(response)

# Output
# <grandparent>: Resilience is like a mighty oak tree that withstands the strongest storms, bending but never breaking. It is the ability to bounce back from adversity, to find strength in the face of challenges, and to persevere even when the odds seem insurmountable. Just as a diamond is formed under immense pressure, resilience is forged through the trials and tribulations of life.
```

### Specify the steps required to complete a task

```python
text = f"""
In a charming village, siblings Jack and Jill set out on \
a quest to fetch water from a hilltop \
well. As they climbed, singing joyfully, misfortune \
struck—Jack tripped on a stone and tumbled \
down the hill, with Jill following suit. \
Though slightly battered, the pair returned home to \
comforting embraces. Despite the mishap, \
their adventurous spirits remained undimmed, and they \
continued exploring with delight.
"""
# example 1
prompt_1 = f"""
Perform the following actions:
1 - Summarize the following text delimited by triple \
tildes with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the following \
keys: french_summary, num_names.

Separate your answers with line breaks.

Text:
~~~{text}~~~
"""
response = get_completion(prompt_1)
print("Completion for prompt 1:")
print(response)

# Output

# Completion for prompt 1:
# 1 - Jack and Jill, siblings, go on a quest to fetch water from a hilltop well, but encounter misfortune when Jack trips on a stone and tumbles down the hill, with Jill following suit, yet they return home and remain undeterred in their adventurous spirits.

# 2 - Jack et Jill, frère et sœur, partent en quête d'eau d'un puits au sommet d'une colline, mais rencontrent un malheur lorsque Jack trébuche sur une pierre et dévale la colline, suivi de Jill, pourtant ils rentrent chez eux et restent déterminés dans leur esprit d'aventure.

# 3 - Jack, Jill

# 4 - { "french_summary": "Jack et Jill, frère et sœur, partent en quête d'eau d'un puits au sommet d'une colline, mais rencontrent un malheur lorsque Jack trébuche sur une pierre et dévale la colline, suivi de Jill, pourtant ils rentrent chez eux et restent déterminés dans leur esprit d'aventure.", "num_names": 2 }
```

We can also ask the model to output the response in a specific format.

```python
prompt_2 = f"""
Your task is to perform the following actions:
1 - Summarize the following text delimited by
  <> with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the
  following keys: french_summary, num_names.

Use the following format:
Text: <text to summarize>
Summary: <summary>
Translation: <summary translation>
Names: <list of names in summary>
Output JSON: <json with summary and num_names>

Text: <{text}>
"""
response = get_completion(prompt_2)
print("\nCompletion for prompt 2:")
print(response)

# Output

# Completion for prompt 2:
# Summary: Jack and Jill, siblings from a charming village, go on a quest to fetch water from a hilltop well, but encounter misfortune when Jack trips on a stone and tumbles down the hill, with Jill following suit, yet they remain undeterred and continue exploring with delight.

# Translation: Jack et Jill, frère et sœur d'un charmant village, partent à la recherche d'eau d'un puits au sommet d'une colline, mais rencontrent un malheur lorsque Jack trébuche sur une pierre et dévale la colline, suivi de Jill, pourtant ils restent déterminés et continuent à explorer avec joie.

# Names: Jack, Jill

# Output JSON:
# { "french_summary": "Jack et Jill, frère et sœur d'un charmant village, partent à la recherche d'eau d'un puits au sommet d'une colline, mais rencontrent un malheur lorsque Jack trébuche sur une pierre et dévale la colline, suivi de Jill, pourtant ils restent déterminés et continuent à explorer avec joie.", "num_names": 2 }
```

### Instruct the model to work out its own solution before rushing to a conclusion

```python
prompt = f"""
Determine if the student's solution is correct or not.

Question:
I'm building a solar power installation and I need \
 help working out the financials.
- Land costs $100 / square foot
- I can buy solar panels for $250 / square foot
- I negotiated a contract for maintenance that will cost \
me a flat $100k per year, and an additional $10 / square \
foot
What is the total cost for the first year of operations
as a function of the number of square feet.

Student's Solution:
Let x be the size of the installation in square feet.
Costs:
1. Land cost: 100x
2. Solar panel cost: 250x
3. Maintenance cost: 100,000 + 100x
Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000
"""
response = get_completion(prompt)
print(response)
```

Note that the student's solution is actually not correct.

We can fix this by instructing model to work out its own solution first.

```python
prompt = f"""
Your task is to determine if the student's solution \
is correct or not.
To solve the problem do the following:
- First, work out your own solution to the problem including the final total.
- Then compare your solution to the student's solution \
and evaluate if the student's solution is correct or not.
Don't decide if the student's solution is correct until
you have done the problem yourself.

Use the following format:
Question:
~~~
question here
~~~
Student's solution:
~~~
student's solution here
~~~
Actual solution:
~~~
steps to work out the solution and your solution here
~~~
Is the student's solution the same as actual solution \
just calculated:
~~~
yes or no
~~~
Student grade:
~~~
correct or incorrect
~~~

Question:
~~~
I'm building a solar power installation and I need help \
working out the financials.
- Land costs $100 / square foot
- I can buy solar panels for $250 / square foot
- I negotiated a contract for maintenance that will cost \
me a flat $100k per year, and an additional $10 / square \
foot
What is the total cost for the first year of operations \
as a function of the number of square feet.
~~~
Student's solution:
~~~
Let x be the size of the installation in square feet.
Costs:
1. Land cost: 100x
2. Solar panel cost: 250x
3. Maintenance cost: 100,000 + 100x
Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000
~~~
Actual solution:
"""
response = get_completion(prompt)
print(response)
```

### Writing a good prompt is iterative

Effective prompt engineering is not about knowing the perfect prompts but it is having a good process to develop prompts that are effective for your application.

- Try something.
- Analyse where the result does not give what you want.
- Clarify instructions, give more time to think.
- Refine prompts with a batch of examples.

## References

- [ChatGPT Prompt Engineering Crash Course by DeepLearning.AI](https://learn.deeplearning.ai/chatgpt-prompt-eng)
- [Prompt Engineering Tutorial - YouTube Video Ania Kubow](https://youtu.be/_ZvnD73m40o)
