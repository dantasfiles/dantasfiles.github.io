---
title: "Notes on <i>Speech & Language Processing</i> by Jurafsky & Martin"
description: "An Introduction to Natural Language Processing, Computational Linguistics & Speech Recognition with Language Models"
author: Daniel Dantas
---

These are things I found interesting while reading _[Speech & Language Processing: An Introduction to Natural Language Processing, Computational Linguistics & Speech Recognition with Language Models](https://web.stanford.edu/~jurafsky/slp3/)_

The notes are still in progress as I have not yet finished reading the book

## I. Fundamental Algorithms for NLP

### 2. Regular Expressions, Tokenization, Edit Distance
- [ELIZA](https://en.wikipedia.org/wiki/ELIZA) was found convincing by many users because the system emulated a person who was not supposed to not refer to any outside context
- A collection of texts is called a _[corpus](https://en.wikipedia.org/wiki/Text_corpus)_
- Regular expressions in the book are placed between slashes `/ /`, but I can't find the historical context for that, as I don't remember using slashes in regular expressions in languages and tools that I've used
- One issue with backslashes `\` is that they are used to escape characters by both strings in the programming language, and also by the regular expression library. So to match a literal backslash `\` in a string, the regular expression `\\` is used. But those backslashes must also be escaped when written as a string in the programming language, so you end passing the string `"\\\\"` to the regular expression library. Languages like Python sometimes use [tricks like raw string notation](https://docs.python.org/3/howto/regex.html#the-backslash-plague) `r"\\"`to make the backslashes less annoying
- I'm not as familiar with the non-greedy (match as little as possible) Kleene operators `*?` and `+?`, and the [lookahead assertions](https://en.wikipedia.org/wiki/Regular_expression#Assertions) `(?=` and `(?!`, so it was interesting to learn about them. I wonder how often they come up in practice
- It's fun to have a detailed explanation of regular expressions. In practice, complicated regular expressions can be difficult to get right. Developers often looked up common complicated regular expressions on places like Stack Overflow then modified them to their particular taste. Now they often use LLMs for a first draft. 
- In Fei-Fei Li's _[The World's I See](https://dantasfiles.com/2023/11/07/notes-on-the-worlds-i-see.html#6-the-north-star)_, one of the themes was the importance of good training data. This book also focuses on explorations of training data, like the Brown corpus, the Switchboard corpus, and the massive Google n-grams corpus
- There's a link to _[Using uh and um in spontaneous speaking](https://www.sciencedirect.com/science/article/abs/pii/S0010027702000173)_ about how the fillers "uh" and "um" are used differently: "uh" for a short filled pause and "um" for a long filled pause
- In biology, the line between what is in the same species or not [is malleable and sometimes even political](https://news.yale.edu/2025/01/03/fish-center-key-conservation-fight-not-distinct-species-after-all). In the discussion of what is a _language_ and what is a dialect, I wonder if the same issues appear
- My grandfathers' primary languages were Portuguese and Spanish, so I heard _code-switching_ all the time growing up
- I've read many older books and have noted the differences in style over time, so it makes sense that researchers have explicitly created corpora from particular time periods
- One of the elements in the _datasheet_ is "_Are there copyright or other intellectual property restrictions?_" I think a lot of the law pertaining to training on copyrighted data is still up in the air, so I'd be interested in learning more about this topic
- Unix command pipelines like `tr` → `sort` → `uniq` may have been more common in the past, but the book points out that, these days, it's preferred to write easily-customizable solutions in scripting languages with mature Unicode support
- In compilers, the _tokenization_ stage is also called [lexical analysis](https://en.wikipedia.org/wiki/Lexical_analysis) or lexing
- The [Natural Language Toolkit (NTLK)](https://www.nltk.org/) for Python is recommended




