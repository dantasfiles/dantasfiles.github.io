---
title: 'Notes on 🐯<i>Computer Science: An Interdisciplinary Approach</i>'
# description: Princeton COS 126, Spring 2025 edition
author: Daniel Dantas
---

I was curious to learn what has been updated since I was a [teaching assistant for COS 126](https://dantasfiles.com/2005/05/30/princeton-cos-126.html), so I am reading through the [lecture slides for the Spring 2025 semester](https://www.cs.princeton.edu/courses/archive/spr25/cos126/)

I use these notes to keep track of thoughts I have during reading, and anything that sticks out to me as interesting. My notes are incomplete as I have not yet finished reading the slides

## 0. Introduction
  * The _everything_ is correctly in quotes in the statement “ _‘Everything’ can be encoded as a sequence of bits_ ” because continuous things, like real numbers, cannot always be encoded in a _finite_ sequence of bits

  * The class continues to use _Java_ as it did when I was a teaching assistant   
The upside is that Java’s verbosity and strong typing make it very explicit what you are doing, and provide a strong foundation of understanding. The downside is that those same features make Java a more difficult first language\ 
Some universites, like [Cornell](https://dantasfiles.substack.com/p/cornell-cs-reading-list-spring-2025), use a looser language like Python for the [first programming course](https://dantasfiles.substack.com/p/notes-on-introduction-to-computing) to get students coding quickly, then Java for the [second](https://www.cs.cornell.edu/courses/cs2110/2025sp/) to learn the deeper details of programming\
I don’t know which system works best—it probably depends on the student

## 0. Hello, world
  * Machine language, natural language, and high-level programming language are contrasted, and it is pointed out that natural language is getting more understandable by computers since I was a teaching assistant for the course

## 0. Built-in data types
  * “ _A data type (type) is a set of values and a set of operations on those values_ ” is a key concept in programming languages
  
  * Java overloading the division symbol (`/`) to perform both integer and floating point division causes confusion

  * The standard warning not to use equality testing (`==`) with floating point numbers is presented

  * Java is [statically typed](https://en.wikipedia.org/wiki/Type_system#Static_type_checking): the types of expressions are determined at compile time, and the compiler will use the type system to catch common errors

  * Java will concatenate (`+`) strings with other types automatically (e.g. using the [toString](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Object.html#toString\(\)) method for objects)

  * Explicitly casting floating point numbers to integers rounds down

## 1. Conditionals
  * Local variables declared in a Java code block are not accessible outside the block

  * Even if the body of an `if` statement only has a single statement, it is recommended to put that single statement in a code block, which is good advice.

## 1. Loops

  * Java’s for-each / enhanced-for statements are not explored, because which limits the power of for statements, but avoids talking about Collections this early in the class.

## 2. Arrays
- The example `double[] a = new int[10];` is used to demonstrate a compile-time type mismatch error.<br>What's interesting is that arrays of reference types in Java are _covariant_, allowing `Object[] a = new String[10];`. However, this will cause a runtime `ArrayStoreException` if you try to store anything other than a `String` in array `a`.<br>When _generics_ (`List<T>`) were added to Java, they were correctly invariant--`List<Object> l = new ArrayList<String>();` will fail to compile with a type-mismatch error.
- I was uncertain if the shuffle algorithm presented was correct, because it was different from the [traditional presentation](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle#The_modern_algorithm), but [apparently it is indeed correct](https://stackoverflow.com/questions/68064254/correctness-of-fisher-yates-shuffle-executed-backward) so that was cool to learn

## 3. Functions
- Functions can only return a single item. Unlike in languages that have tuples built-in, if you want to return more information from a function, you can create a class to hold the information, or you can use the [syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar) of [record classes](https://docs.oracle.com/en/java/javase/23/language/records.html)
- Java chooses which overloaded function to call based on the arguments and their types, not based on the return type
- The scope of a Java variable is until the end of the block in which it is declared

## 3. Libraries & Clients
- A [sawtooth function](https://en.wikipedia.org/wiki/Sawtooth_wave) is implemented: `2 * (freq*t - Math.floor(freq*t + 0.5))`



