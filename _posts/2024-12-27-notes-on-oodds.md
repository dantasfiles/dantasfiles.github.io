---
title: Notes on 📕<i>Object-Oriented Design and Data Structures</i> by 🐻Myers & Kozen
description: "In-progress, incomplete"
hidden: true
author: Daniel Dantas
---

I use these notes to track thoughts I had, and things I found interesting, while reading [Object-Oriented Design and Data Structures](https://andrewcmyers.github.io/oodds/)

The notes are still in progress as I have not yet finished reading the book

## 1. Introduction
- The book starts off with the great observation: "_One of the joys of working with computers is that it is relatively easy to create new things...The constraints of the real world weigh much less heavily on software developers than on engineers in other disciplines_." This is often expressed in technology social media as "_you can just do things_"

## 2. Values, Types, and Variables
- There are [different definitions of a strongly-typed language](https://en.wikipedia.org/wiki/Strong_and_weak_typing), but the one used in this book is "_run-time type errors are not possible_." Wikipedia points to an [article by Luca Cardelli](http://www.lucacardelli.name/Papers/TypefulProg.pdf) with a similar definition: "_the absence of unchecked run-time type errors_"
- The book observes  that Java, unlike Python, is whitespace-insensitive, but, in practice, everyone uses it in a whitespace-sensitive manner, with line breaks and indenting, for readability
- The book states "_Local variables are in scope from the point of declaration until the end of the block in which they are declared_" This is different from languages like Python, which have function, not block, scope. In Javascript, variables defined with `var` had function scope, but variables defined with the modern `let` and `const` are more similar to Java.
- I believe the only [variable shadowing](https://en.wikipedia.org/wiki/Variable_shadowing#Java) in Java that is disallowed is local variables over other local variables. Everything else is fair game and, as the book points out, the cause of various errors. As far as I know, there's no option to get the Java compiler to be stricter about shadowing and print warnings

## 4. Java Execution Model: Arrays, Strings, Autoboxing
- The book points out because Java arrays are subtypes of Objects, you can create an array of Objects, then point the first element of that array at the array itself
- The book points out that autoboxing uses [Integer.valueOf](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/lang/Integer.html#valueOf(int)): "_This method will always cache values in the range -128 to 127, inclusive, and may cache other values outside of this range_"
- The book advises that the less the obscure corners of a language are used, the better

## 5. Representing Java Values
- The book advises that though you can program while only knowing the top-level abstraction that the language provides, it's useful to understand the internals. This advice, and the "don't use obscure corners of a language" advice from the previous chapter, should be complementary, not contraditory
- The book points out that variables and fields with type `short`, `byte`, and `char` all use 32 bits of memory, like an int, in Java, but that arrays pack the smaller data types together more tightly. It also suggests using a [Bitset](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/BitSet.html) for large lists of boolean values
- Exponents are biased, according to [Wikipedia](https://en.wikipedia.org/wiki/Exponent_bias), because "_ exponents have to be signed values in order to be able to represent both tiny and huge values, but two's complement, the usual representation for signed values, would make comparison harder_"
- The book cautions about the subtleties of representing decimals as floating point numbers. One alternative in the [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/lang/Double.html) is "_scaling up so the monetary value is an integer — for example, multiplying by 100 if the value is denominated in cents or multiplying by 1000 if the value is denominated in mills — and then storing that scaled value in an integer type_"
- The book advises to use the type `double` unless there is a particular reason to use `float`

## 6. Encapsulation and information hiding
- **Abstraction** is defined in [Wikipedia](https://en.wikipedia.org/wiki/Abstraction_(computer_science)) as "_the process of generalizing concrete details, such as attributes, away from the study of objects and systems to focus attention on details of greater importance_"
- **Coupling** is defined in [Wikipedia](https://en.wikipedia.org/wiki/Coupling_(computer_programming)) as "_the degree of interdependence between software modules, a measure of how closely connected two routines or modules are, and the strength of the relationships between modules_"
- **Separation of concerns** is definied in [Wikipedia](https://en.wikipedia.org/wiki/Separation_of_concerns) as "_a design principle for separating a computer program into distinct sections. Each section addresses a separate concern, a set of information that affects the code of a computer program_"
- **Information hiding** is defined in [Wikipedia](https://en.wikipedia.org/wiki/Information_hiding) as "_the principle of segregation of the design decisions in a computer program that are most likely to change, thus protecting other parts of the program from extensive modification if the design decision is changed_"
- **Encapsulation** is definied in [Wikipedia](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) as "_the bundling of data with the mechanisms or methods that operate on the data_"
- An **abstract data type** is defined in [Wikipedia](https://en.wikipedia.org/wiki/Abstract_data_type) as "_a mathematical model for data types, defined by its behavior (semantics) from the point of view of a user of the data, specifically in terms of possible values, possible operations on data of this type, and the behavior of these operations_"
- The [BigInteger](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/math/BigInteger.html) class represents "_immutable arbitrary-precision integers_"

## 7. Interfaces and subtyping
- The book points out that downcasting can be used to get around information hiding -- avoid doing this
- **Structural subtyping** is defined in [Wikipedia](https://en.wikipedia.org/wiki/Subtyping) as "_the structure of two types determines whether or not one is a subtype of the other_", and **nominal subtyping** as "_only types declared in a certain way may be subtypes of each other_"
- **Behavioral subtyping** is defined in [Wikipedia](https://en.wikipedia.org/wiki/Behavioral_subtyping) as "_behavioral subtyping is the principle that subclasses should satisfy the expectations of clients accessing subclass objects through references of superclass type, not just as regards syntactic safety (such as the absence of "method-not-found" errors) but also as regards behavioral correctness_"
- The Java `new` operator requires the class of the created object to be explicitly specified at compile time. Factory methods allow the object creation process to be polymorphic, and the class of the created object to be specified elsewhere, at runtime.

## 8. Designing and documenting interfaces
- The book points out the there are disadvantages from making interfaces too wide and too narrow, but in practice, most problematic interfaces are too wide
- According to the Java [documentation](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html), abstract classes "_can declare fields that are not static and final, and define public, protected, and private concrete methods_", while interfaces require that  "_all fields are automatically public, static, and final, and all methods that you declare or define (as default methods) are public_"
- The **principle of least surprise** is defined in [Wikipedia](https://en.wikipedia.org/wiki/Principle_of_least_astonishment) as "_a component of a system should behave in a way that most users will expect it to behave, and therefore not astonish or surprise users_"
- **Command-query separation** is definied in [Wikipedia](https://en.wikipedia.org/wiki/Command%E2%80%93query_separation) as "_every method should either be a command that performs an action, or a query that returns data to the caller, but not both_"
- The book advises that it may be desirable to inherit the `Object.equals` method for reference equality if the class is mutable, in order to represent Liebniz equality rather than state equality. It's desirable to implement a state equality `equals` method for immutable classes as it will prevent a client from differentiating different implementions
- The book advices to treat null values passed in as arguments to a method, or returned from a method as exceptional conditions that must be documented if possible
- The book advises to be aware of a potential lack of symmetry between `s.equals(t)` and `t.equals(s)` if `S` is a subclass of `T` (or other similar other situations)

## 9. Exceptions
- The purpose of the `finally` block is to perform cleanup even if control is not returned to the code directly after the try-catch loop (the `catch` block returns, or `continue`s or `break`s out of a loop, or the exception is uncaught, or the `catch` block throws another exception...)
- 



