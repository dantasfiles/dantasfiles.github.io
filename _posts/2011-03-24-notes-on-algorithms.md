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
- The book warns that APIs typically become too wide, because it's easy to add methods, but difficult to deprecate them
- The book contrasts interface inheritance / subtyping, with implementation inheritance / subclassing, though the definitions are a bit mixed together. Differences includee that the latter does not necessarily imply behavioral subtyping, and the latter can break encapsulation. The book recommends using interface inheritance, but using implementation inheritance only in particular situations and not in general
- Fragile base class problem is defined by [Wikipedia](https://en.wikipedia.org/wiki/Fragile_base_class) as "_base classes (superclasses) are considered "fragile" because seemingly safe modifications to a base class, when inherited by the derived classes, may cause the derived classes to malfunction_"
- Equivalence relation is defined by [Wikipedia](https://en.wikipedia.org/wiki/Equivalence_relation) as "_a binary relation that is reflexive, symmetric, and transitive_"
- The book recommends a standard `equals` implementation: check for reference equality, check for null, use `getClass` to check for same class (this is mostly, but not always desired), then check instance variables
- `Final` is defined in [Wikipedia](https://en.wikipedia.org/wiki/Final_(Java)) as "_an entity that can only be assigned once_". Note that even if a field is final, if it is a reference type, the underlying object can change state
- The book states immutable objects means that you are always creating new objects when you work with them, but that the Java garbage collector is optimized for that case
- Design by contract is defined in [Wikipedia](https://en.wikipedia.org/wiki/Design_by_contract) as "_software designers should define formal, precise and verifiable interface specifications for software components, which extend the ordinary definition of abstract data types with preconditions, postconditions and invariants_"
- The book recommends using exceptions to guard against problems outside your control, and assertions to guard against problems inside your control
- Fail-fast system is defined in [Wikipedia](https://en.wikipedia.org/wiki/Fail-fast_system) as "_immediately reports at its interface any condition that is likely to indicate a failure. Fail-fast systems are usually designed to stop normal operation rather than attempt to continue a possibly flawed process_"
- The book questions why Java does not have first class functions. Modern versions of Java have [lambda expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) and [functional interfaces](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/function/package-summary.html), which provide an approximation
- The book points out that Java use of both primitive and reference types is a compromise to allow the performance boost from primitive types
- The book points out that though Java is not thought of as having pointers, it does, but they are restricted to creation and assignment operators, which along with a good garbage collection algorithm and strong typing, eliminates many pointer problems
- The book recommends not using static variables except in certain cases

## 1.3 Bags, Queues & Stacks









