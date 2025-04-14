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
- Abstract data type is defined in [Wikipedia](https://en.wikipedia.org/wiki/Abstract_data_type) as "_a mathematical model for data types, defined by its behavior (semantics) from the point of view of a user of the data, specifically in terms of possible values, possible operations on data of this type, and the behavior of these operations_"
- Aliasing is defined in [Wikipedia](https://en.wikipedia.org/wiki/Aliasing_(computing)) as "_a situation in which a data location in memory can be accessed through different symbolic names in the program_"
- Java's parameter-passing strategy is sometimes [called](https://en.wikipedia.org/wiki/Evaluation_strategy#Call_by_sharing) "call by sharing," but I agree with the book that it's pass by value for all practical purposes
- Generic type is defined by the Java [documentation](https://docs.oracle.com/javase/tutorial/java/generics/types.html) as "_a generic class or interface that is parameterized over types_"
- There's a nod in the book toward factory method patterns, but then it clarifies that the only advanced Java language topics that are going to be used are generics and iterators
- Encapsulation is defined in [Wikipedia](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) as "_the bundling of data with the mechanisms or methods that operate on the data. It may also refer to the limiting of direct access to some of that data, such as an object's components_"
- 





