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


