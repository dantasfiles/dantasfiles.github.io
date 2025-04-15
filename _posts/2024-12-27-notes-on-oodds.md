---
title: Notes on 📕<i>Object-Oriented Design and Data Structures</i> by 🐻Myers & Kozen
description: "In-progress, incomplete"
hidden: true
author: Daniel Dantas
---

I use these notes to track thoughts I had, and things I found interesting, while reading [Object-Oriented Design and Data Structures](https://andrewcmyers.github.io/oodds/)

The notes are still in progress as I have not yet finished reading the book

## 2. Introduction
- The book starts off with the great observation: "_One of the joys of working with computers is that it is relatively easy to create new things...The constraints of the real world weigh much less heavily on software developers than on engineers in other disciplines_." This is often expressed in technology social media as "_you can just do things_"

## 3. Values, Types, and Variables
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
<!-- I believe the `add` function in the Rational class doesn't maintain the class invariants -->

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
- The unchecked exception classes are defined in the Java [documentation](https://docs.oracle.com/javase/specs/jls/se7/html/jls-11.html#jls-11.1.1) as "_the run-time exception classes and the error classes", and the checked as "_all exception classes other than the unchecked exception classes_". The book constrasts unchecked as programmer errors, and checked as unusual conditions. If the unusual condition should never occur, the book advises catching it then throwing an unchecked exception like Error
- A try-with-resources statement is defined in the Java [documentation](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html) as "_a try statement that declares one or more resources...ensures that each resource is closed at the end of the statement_"

## 10. Inheritance and the specialization interface
- The book provides a Java inheritance example that forks a game implementation, changes it, then merges changes from the original, that sounds very similar to a source control story. I don't know what insights to take from that yet, but it's interesting
- Dynamic dispatch is defined in [Wikipedia](https://en.wikipedia.org/wiki/Dynamic_dispatch) as "_the process of selecting which implementation of a polymorphic operation (method or function) to call at run time_"

## 11. Modular design and implementation
- The book advises to assume by default that fields cannot be null, and note in the specifications if they can be null
- Behavioral subtyping is defined by [Wikipedia](https://en.wikipedia.org/wiki/Behavioral_subtyping) as "_the principle that subclasses should satisfy the expectations of clients accessing subclass objects through references of superclass type, not just as regards syntactic safety (such as the absence of "method-not-found" errors) but also as regards behavioral correctness_"
- The book advises to use top-down design on the parts where you're worried about matching client expectations and overall structure, and bottom-up on the parts where you're worried about feasibility and performance

## 12. Testing
- Continuous testing is defined in [Wikipedia](https://en.wikipedia.org/wiki/Continuous_testing) as "_the process of executing automated tests as part of the software delivery pipeline to obtain immediate feedback on the business risks associated with a software release candidate_"
- Regression testing is defined in [Wikipedia](https://en.wikipedia.org/wiki/Regression_testing) as "_re-running functional and non-functional tests to ensure that previously developed and tested software still performs as expected after a change_"
- Black-box testing is defined in [Wikipedia](https://en.wikipedia.org/wiki/Black-box_testing) as "_a method of software testing that examines the functionality of an application without peering into its internal structures or workings_". It's useful for helping design the specification in the first place
- Test coverage is defined in [Wikipedia](https://en.wikipedia.org/wiki/Black-box_testing#Test_coverage) as "_the percentage of software requirements that are tested by black-box testing for a system or application_"
- Glass-box testing is defined in [Wikipedia](https://en.wikipedia.org/wiki/White-box_testing) as "_a method of software testing that tests internal structures or workings of an application, as opposed to its functionality_"
- Code / test coverage is defined in [Wikipedia](https://en.wikipedia.org/wiki/Code_coverage) as "_a percentage measure of the degree to which the source code of a program is executed when a particular test suite is run_"
- Fuzzing is defined in [Wikipedia](https://en.wikipedia.org/wiki/Fuzzing) as "_an automated software testing technique that involves providing invalid, unexpected, or random data as inputs to a computer program. The program is then monitored for exceptions such as crashes, **failing built-in code assertions**, or potential memory leaks.... Typically, a fuzzer is considered more effective if it achieves a higher degree of code coverage.... A white-box fuzzer leverages program analysis to systematically increase code coverage or to reach certain critical program locations... A gray-box fuzzer leverages instrumentation rather than program analysis to glean information about the program_"
- Reference implementationis defined in [Wikipedia](https://en.wikipedia.org/wiki/Reference_implementation) as "_a program that implements all requirements from a corresponding specification.... A reference implementation may or may not be production quality_"
- The book alleges that if there is a bug, there is usually a small counterexample that exposes a bug. So it may be worthwhile searching shallowly but comprehensively, rather than deeply but nonexhaustively
- The book points out that formal proofs of code correctness are an area of future research
- Symbolic execution is defined in [Wikipedia](https://en.wikipedia.org/wiki/Symbolic_execution) as "_a means of analyzing a program to determine what inputs cause each part of a program to execute. An interpreter follows the program, assuming symbolic values for inputs rather than obtaining actual inputs as normal execution of the program would. It thus arrives at expressions in terms of those symbols for expressions and variables in the program, and constraints in terms of those symbols for the possible outcomes of each conditional branch_"

## 13. Recursion
<!-- I think there's a bug in the section "_We can view the space of inputs as a table, in which the value of each cell other than the top row and the diagonal is determined by adding the numbers directly above and diagonally to the left_" -->
<!-- I'm not sure "_ Its value decreases by 1 in both recursive calls, so it can never go below zero._" is true. In C(3,2), min(n-r,r) = min(1,2) = 1. In one recursive call, C(3-1,2-1) = C(2,1), min(n-r,r) = min(1,1) = 1 -->
- Recursive data type is defined in [Wikipedia](https://x.com/home) as "_a data type for values that may contain other values of the same type_"
- Sentinel node is defined in [Wikipedia](https://en.wikipedia.org/wiki/Sentinel_node) as "_a specifically designated node used with linked lists and trees as a traversal path terminator_"
- The book presents the canonical list iteration: `while (n != null) { _do something_; n = n.next; }. A `for` loop version is also presented, but I prefer not to use `for` loops when the length is unspecified
- Tail call is defined in [Wikipedia](https://en.wikipedia.org/wiki/Tail_call) as "_a subroutine call performed as the final action of a procedure. If the target of a tail is the same subroutine, the subroutine is said to be tail recursive.... Tail calls can be implemented without adding a new stack frame to the call stack.... Tail recursion can be related to the while statement, an explicit iteration_"
- The book points out that Java does not implement tail call optimization. I believe one reason is that the Java security mechanism does stack inspection

## 14. Linked Lists
- The Java documentation describes List implementations as follows: "_ArrayList - Resizable array implementation of the List interface (an unsynchronized Vector). The best all-around implementation of the List interface. LinkedList - Doubly-linked list implementation of the List interface. Provides better performance than the ArrayList implementation if elements are frequently inserted or deleted within the list. Also implements the Deque interface. When accessed through the Queue interface, LinkedList acts as a FIFO queue_
- 
- 



