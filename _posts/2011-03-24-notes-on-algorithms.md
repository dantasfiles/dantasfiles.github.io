---
title: Notes on 📕<i>Algorithms</i> by 🐯Sedgewick & Wayne</i>
description: "In-progress, incomplete"
hidden: true
author: Daniel Dantas
---

These are thoughts I had, and things I found interesting, while reading [Algorithms](https://algs4.cs.princeton.edu/)

The notes are still in progress as I have not yet finished reading the book

## 1. Fundamentals
- An algorithm is defined in [Wikipedia](https://en.wikipedia.org/wiki/Algorithm) as "_a finite sequence of mathematically rigorous instructions, typically used to solve a class of specific problems or to perform a computation_". I don't really like the Wikipedia definition, the definition in this book is better.

### 1.1 Basic Programming Model
- Data abstraction is defined in [Wikipedia](https://en.wikipedia.org/wiki/Abstraction_(computer_science)#Data_abstraction) as "_a clear separation between the abstract properties of a data type and the concrete details of its implementation_"
- The book recommends using data all of the same primitive data type in expressions if at all possible instead of trying to figure out the intricacies of type conversion
- Strongly typed is definited in [Wikipedia](https://en.wikipedia.org/wiki/Strong_and_weak_typing) as "_stricter typing rules at compile time, which implies that errors are more likely to happen during compilation_"
- The books points out that recursive calls that overlap create great inefficiencies. This is why memoization / dynamic programming can help to avoid exponential running times.
- The book points out that the variable in a for loop is only in scope in the for loop block. If you need the value of that value outside the block, use a while loop (or save it somewhere)
- To print an array, use the [Arrays.toString](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Arrays.html#toString(java.lang.Object%5B%5D)) helper functions

### 1.2 Data Abstraction

