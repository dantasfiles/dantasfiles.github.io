---
title: 'Notes on 🏫<i>Computer Science: An Interdisciplinary Approach</i>'
# description: Princeton COS 126, Spring 2025 edition
author: Daniel Dantas
---

I was curious to learn what has been updated since I was a teaching assistant for this course, so I am reading through the lecture notes

The course website for Princeton COS 126, Spring 2025 semester, is located at <https://www.cs.princeton.edu/courses/archive/spr25/cos126/>

I’ve noted anything that stuck out to me as interesting. My notes are incomplete as I have not yet finished reading the lecture notes

## Introduction
  * The _everything_ is correctly in quotes in the statement “ _‘Everything’ can be encoded as a sequence of bits_ ” because continuous things, like real numbers, cannot always be encoded in a _finite_ sequence of bits

  * The class continues to use _Java_ as it did when I was a teaching assistant   
The upside is that Java’s verbosity and strong typing make it very explicit what you are doing, and provide a strong foundation of understanding. The downside is that those same features make Java a more difficult first language\ 
Some universites, like [Cornell](https://dantasfiles.substack.com/p/cornell-cs-reading-list-spring-2025), use a looser language like Python for the [first programming course](https://dantasfiles.substack.com/p/notes-on-introduction-to-computing) to get students coding quickly, then Java for the [second](https://www.cs.cornell.edu/courses/cs2110/2025sp/) to learn the deeper details of programming\
I don’t know which system works best—it probably depends on the student

## Hello, world
  * Machine language, natural language, and high-level programming language are contrasted, and it is pointed out that natural language is getting more understandable by computers since I was a teaching assistant for the course

## Built-in data types
  * “ _A data type (type) is a set of values and a set of operations on those values_ ” is a key concept in programming languages
  
  * Java overloading the division symbol (`/`) to perform both integer and floating point division causes confusion

  * The standard warning not to use equality testing (`==`) with floating point numbers is presented

  * Java is [statically typed](https://en.wikipedia.org/wiki/Type_system#Static_type_checking): the types of expressions are determined at compile time, and the compiler will use the type system to catch common errors

  * Java will concatenate (`+`) strings with other types automatically (e.g. using the [toString](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Object.html#toString\(\)) method for objects)

  * Explicitly casting floating point numbers to integers rounds down

## Conditionals
  * Local variables declared in a Java code block are not accessible outside the block

  * Even if the body of an `if` statement only has a single statement, it is recommended to put that single statement in a code block, which is good advice.

## Loops

  * Java’s for-each / enhanced-for statements are not explored, because which limits the power of for statements, but avoids talking about Collections this early in the class.



