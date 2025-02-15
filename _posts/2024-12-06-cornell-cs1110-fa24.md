---
title: 'Notes on 🏫<i>Intro. to Computing: A Design & Development Perspective</i>'
description: "Cornell CS 1110, Fall 2024 edition"
author: Daniel Dantas
---

I was curious to learn what has been updated since I took a version of this course (Cornell CS 1110) so I read through the lecture notes. The course website for the Fall 2024 semester is located at [https://www.cs.cornell.edu/courses/cs1110/2024fa/](https://www.cs.cornell.edu/courses/cs1110/2024fa/). The lecture videos are Cornell-only, but the slides are public.

I’ve noted anything that stuck out to me as interesting. When I took a version of the course, it used _Java_ , and now it uses _Python_. So some of my comments will be how the course differs between the two programming languages.

## Types & Expressions
  * This is one of the fundamental ideas in programming languages: “ _A type is both a set of values, and the operations on them_ ”
  * The integer division and double division operators are the same (`/`) in Java, but different (`/` vs. `//`) in Python, which prevents many simple bugs
  * An always useful reminder that floating point numbers have finite precision
  * When quickly reading code, it’s easy to misrecognize Java’s logical vs. bitwise operators. Python uses text (`and` `or` `not`) for [logical operators](https://docs.python.org/3.13/library/stdtypes.html#boolean-operations-and-or-not) and symbols (`&` `|` `!`) for [bitwise operators](https://docs.python.org/3.13/library/stdtypes.html#bitwise-operations-on-integer-types), which is easier to differentiate
  * In Python, values with types like integers won’t implicitly cast to string when adding/concatenating them to strings. This prevents some uncommon bugs that happen in Java.
  * Python allows single or double quotes for strings. It’s somewhat useful in that you can use the opposite quotation marks inside strings without escaping (`\`) them, but I don’t think it’s useful enough to justify the additional language complexity.

## Variables & Assignments
  * Python is dynamically typed: a variable has the type of its value, and you can change a variable’s type with an assignment. This allows bugs that a statically-typed language will prevent

## User-Defined Functions
  * Students are instructed to use vertical lines (\|) to show indention when writing code on paper. This is a requirement that isn’t needed in Java, where code blocks are more obvious from the surrounding braces. But considering you almost never write code on paper, I don’t see this as much of a negative against Python and it makes the code less verbose

## Specifications & Testing
  * Test writing is placed early in the course because it requires a lot of practice. Students get a whole semester to think about and experiment with test writing
  * I’ve never heard of the _Rule of Numbers (1, 2, 0)_ testing strategy before: 1. simplest test, 2. more then expected, 0. something missing

## Conditionals & Program Flow
  * The lack of explicit variable declarations in Python, unlike Java, can cause some confusion and bugs
  * Local variables in Python last until the end of the function, not the end of any code block they were created in. This is different from Java where variables declared in a code block do not exist after the block ends

## Algorithm Design
  * A _one page rule_ is recommended _:_ if a function gets longer than one page, break it up

## Objects
  * Everything is an object in Python, so “casts” are actually constructors that make an object of the new type. In Java, there’s a sharper demarcation between primitives and objects

## Memory in Python
  * Variables are either global variables that exist for the lifetime of program, or local variables in the call stack that exist for lifetime of function. They point to objects in the heap space, including module and function definitions. As such, functions are first-class objects in Python, unlike in Java.  
Items in the heap space are garbage-collected as necessary, similar to Java.

## Asserts & Error Handling
  * Stack traces in Python errors are caller → callee, while stack traces in Java errors are callee → caller. You typically need to know both the top and the bottom, so I’ve found it doesn’t matter much which is presented first.
  * Python divides converting an object to a string ([toString](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Object.html#toString\(\)) in Java) into two functions: [str](https://docs.python.org/3/library/functions.html#func-str) for readability, and [repr](https://docs.python.org/3/library/functions.html#repr) for unambiguous representations. The `str` function uses `__repr__` if `__str__` is not defined
  * Exceptions are difficult to model, because they pop call frames off the stack until a `try` `except` statement is reached

## Lists (& Sequences)
  * Python [lists](https://docs.python.org/3.13/library/stdtypes.html#list) are similar to Java [Lists](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/List.html) (`ArrayList`, etc.), not Java arrays. 
  * Python list slicing is useful, but makes a copy, which may cause efficiency issues

## For-Loops
  * To be used in a _for each_ loop, a Python class implements an [__iter__](https://docs.python.org/3.13/library/stdtypes.html#iterator-types) method, typically using the [yield](https://docs.python.org/3.13/reference/expressions.html#yieldexpr) keyword, while a Java class implements the [Iterable](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Iterable.html) interface

## Nested Lists
  * Slicing multidimensional lists does not deep-copy, so if you modify the underlying rows, the original table will change as well.

## Recursion
  * The Python package installer has a fun recursive name: _PIP Installs Packages_. 
  * Recursion and iteration are equivalent. (Converting from iterative to recursive is straightforward. Converting from recursive to iterative is straightforward if recursive function is tail-recursive. If the recursive function is not tail-recursive, a first draft is to create a stack data structure and simulate the recursion. Then you can simplify the resulting iterative function as necessary.)
  * Divide and conquer problems are typically easier to solve with recursion

## Dictionaries
  * Maps in Python ( _[dictionaries](https://docs.python.org/3.13/library/stdtypes.html#mapping-types-dict)_ ) are very intuitive to use. The [Map](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Map.html) interface is Java is fine, but not as fun
  * Python dictionaries can be used simulate the functionality of Python objects—Javascript style—but it’s clumsier and doesn’t perform certain checks to prevent bugs
  * Dictionaries are difficult to divide-and-conquer, so are rarely used as inputs to recursions

## Classes
  *  _[Type](https://docs.python.org/3.13/glossary.html#term-type)_ and _[class](https://docs.python.org/3.13/glossary.html#term-class)_ are synonyms in Python
  *  _[None](https://docs.python.org/3.13/library/constants.html#None)_ in Python is similar to `null` in Java

## Object-Oriented Design
  * Putting an underscore at the beginning of Python methods and attributes indicates that they are supposed to be private, but unlike in Java, there is no enforcement mechanism

## Inheritance
  * Python is dynamically typed, so it uses dynamic method dispatch by design. Java uses dynamic method dispatch except in special cases like private methods in the superclass.

## Operators & Abstraction
  * Operator in Python are [double underscore methods](https://docs.python.org/3/reference/datamodel.html#special-method-names), allowing operator overloading. Java doesn’t, which makes primitive data types look and work different from classes. But Java not having operator overloading protects against ambiguity and unexpected behavior. For example, a user would expect the `*` operator to be symmetric, but `a * b` may behave differently from `b * a` if `a` and `b` have different types
  * Python `is` is similar to Java `==`, while Python `==` is similar to Java `equals`. In Python, `is` implies `==`
  * You should use `isinstance` instead of comparing against the `type`, because someone may create a subtype of your class and break your code
  * Python [properties](https://docs.python.org/3/howto/descriptor.html#properties) are an interesting style of data encapsulation, but I think their use makes code more ambiguous

## While Loops
  * Forgetting to increment is a very common while-loop bug
  * In Python, if you’re not careful and don’t know what’s going on under the hood, you can write algorithms with some unexpectedly large running times, especially with list operations
  * Python has built-in optimizations for for-loops that often make them faster than open-ended while-loops. You can go even faster with [built-in functions](https://docs.python.org/3/library/functions.html) like `max`, and list comprehensions

## GUI Applications
  * Python enumerations are provided by a [library](https://docs.python.org/3/library/enum.html), but are [built-in](https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html) in Java 

## Advanced Error Handling
  * Exceptions in Python are not as slow as in languages like Java, with the expectation that you will use them often. The downside is the “control flow is more difficult to track” issue mentioned earlier

## Searching & Sorting
  * A common start to an algorithm is to sort the data

## Advanced Sorting
  * Python [sorting](https://docs.python.org/3/howto/sorting.html) is [stable](https://en.wikipedia.org/wiki/Sorting_algorithm#Stability) and uses combination of [insertion sort](https://en.wikipedia.org/wiki/Insertion_sort) and [merge sort](https://en.wikipedia.org/wiki/Merge_sort)

## Generators
  * Instead of creating new [iterables](https://docs.python.org/3/glossary.html#term-iterable) like lists each step, much memory can be saved by chaining [generators](https://docs.python.org/3/glossary.html#term-generator) together so that only one element is processed at a time. If necessary, the result generator can be turned back into an iterable at the end

## Wrap-Up
  * Many undergraduates are required to take calculus, but the mathematics used in computer science is different, so usually a separate “CS math” course is required

