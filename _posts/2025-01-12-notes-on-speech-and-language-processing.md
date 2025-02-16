---
title: "Notes on <i>Speech & Language Processing</i> by Jurafsky & Martin"
description: "An Introduction to Natural Language Processing, Computational Linguistics & Speech Recognition with Language Models"
author: Daniel Dantas
---

These are things I found interesting while reading _[Speech & Language Processing: An Introduction to Natural Language Processing, Computational Linguistics & Speech Recognition with Language Models](https://web.stanford.edu/~jurafsky/slp3/)_

The notes are still in progress as I have not yet finished reading the book

## I. Fundamental Algorithms for NLP

### 2. Regular Expressions, Tokenization, Edit Distance
- ELIZA was found convincing by many users because the system emulated a person who was not supposed to not refer to any outside context
- A collection of texts is called a _corpus_
- Regular expressions in the book are placed between slashes `/ /`, but I can't find the historical context for that, as I don't remember using slashes in regular expressions in languages and tools that I've used
- One issue with backslashes `\` is that they are used to escape characters by both strings in the programming language, and also by the regular expression library. So to match a literal backslash `\` in a string, the regular expression `\\` is used. But those backslashes must also be escaped when written as a string in the programming language, so you end passing the string `"\\\\"` to the regular expression library. Languages like Python sometimes use [tricks like raw string notation](https://docs.python.org/3/howto/regex.html#the-backslash-plague) `r"\\"`to make the backslashes less annoying
- I'm not as familiar with the non-greedy (match as little as possible) Kleene operators `*?` and `+?`, and the lookahead operators `(?=` and `(?!`, so it was interesting to learn about them. I wonder how often they come up in practice
- It's fun to have a detailed explanation of regular expressions. In practice, complicated regular expressions can be difficult to get right. Developers often looked up common complicated regular expressions on places like Stack Overflow then modified them to their particular taste. Now they often use LLMs for a first draft. 
- In [Python](https://docs.python.org/3/library/re.html)
  - regular expressions are automatically compiled and cached, but you can manually `compile` and save them 
  - the `search` method checks if a match to the regular expression is found anywhere in the string
  - the `match` method checks if the start of the string matches the regular expression, which is similar to `^`regexp
  - the `fullmatch` methods checks if the entire string matches the regular expression, which is similar to `^`regexp`$`
  - the `split`, `findall` & `finditer` methods find all the matches to the regular expression in the string 



