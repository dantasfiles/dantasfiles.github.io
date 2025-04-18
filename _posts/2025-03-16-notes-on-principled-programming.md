---
title: Notes on 📕<i>Principled Programming</i> by 🐻Tim Teitelbaum
description: "In-progress, incomplete. Introduction to Coding in Any Imperative Language"
hidden: true
author: Daniel Dantas
---

These are things I found interesting while reading [Principled Programming: Introduction to Coding in Any Imperative Language](https://www.cs.cornell.edu/info/people/tt/Principled_Programming.html)

The notes are still in progress as I have not yet finished reading the book

## Preface
- The book is aimed at the level of a first computer class. However, it seems to fit better at a second class level, which is why it is a suggested resource in a second computer class, 🐻[CS 2110](https://www.cs.cornell.edu/courses/cs2110/2025sp/resources.html)

## 1. Introduction
- The book advises writing it right the first time, not assuming it will be fixed later, and avoiding debugging as much as possible. This is something that I try to do, but I've noticed a lot of other people don't
- There's a great example on how to think methodically about code in this chapter

## 2. Prerequisites
- The book includes the program counter in the definition of _state_, then defines _effect_ as a change in state. This implies that stepping through the code is an effect, which is not how most people think about effects

## 3. Specifications & Implementations
- The book advises to think of specifications in two directions: inwards in defining what the implementation will do, and outwards in defining how the specification will be used by the rest of the program
- The book bemoans that specifications contained in comments are essential to programming but are not used by the compiler or other tools. Perhaps it's worth exploring ways to change that
- The book advises that specifications should detail what to do and why you did it (don't assume you'll remember anything later), not how to do it--requirements, not processes
- Information hiding is defined in [Wikipedia](https://en.wikipedia.org/wiki/Information_hiding) as "_the principle of segregation of the design decisions in a computer program that are most likely to change, thus protecting other parts of the program from extensive modification if the design decision is changed_"
- The book recommends that programs should explicitly complain when inputs violate preconditions, to avoid bugs where the user of the specification is unaware that bad inputs are being sent 
- State space is defined in [Wikipedia](https://en.wikipedia.org/wiki/State_space_(computer_science)) as "_a discrete space representing the set of all possible configurations of a system_"
- A representation invariant is defined in [Wikipedia](https://en.wikipedia.org/wiki/Class_invariant) as "_a set of invariant properties that remain uncompromised regardless of the state of the object_"

## 4. Stepwise Refinement
- Stepwise refinement / top-down approach is defined in [Wikipedia](https://en.wikipedia.org/wiki/Bottom-up_and_top-down_design) as "_an overview of the system is formulated, specifying, but not detailing, any first-level subsystems. Each subsystem is then refined in yet greater detail, sometimes in many additional subsystem levels, until the entire specification is reduced to base elements_"
- The book warn to be wary of a stepwise refinement situation where you've divided the problem into subproblems that may be harder to solve then the overall problem
- The book points out that a specification of going from a precondition to a postcondition, is satisfied by an implementation that goes from a weakened version of the precondition (a superset of states allowed by the precondition) to a stronger version of the postcondition (a subset of states required by the postcondition). This way of thinking about specifications is incredibly useful
- The book points out that one reason pulling code into a helper method is useful is that it is easy to tell which variables do not get passed to  the helper function, and thus are not accessed or changed by the helper function's functionality
- Loop variant is defined in [Wikipedia](https://en.wikipedia.org/wiki/Loop_variant) as "_a mathematical function defined on the state space of a computer program whose value is monotonically decreased with respect to a (strict) well-founded relation by the iteration of a while loop under some invariant conditions, thereby ensuring its **termination**_"
- Loop invariant is defined in [Wikipedia](https://en.wikipedia.org/wiki/Loop_invariant) as "_a property of a program loop that is true before (and after) each iteration...expressed by formal predicate logic and used to prove properties of loops and by extension algorithms that employ loops (usually **correctness** properties)_"
- The book advises that to determine a loop invariant, examine the postcondition and weaken it. For [example](https://en.wikipedia.org/wiki/Loop_invariant#Floyd%E2%80%93Hoare_logic), if {C^I} body {I}, then {I} while(C){body} {!C^I} where !C^I satisfies the postcondition you are trying to achieve. This is a great way to think about loop conditions and invariants
- The book divides code into types: sequential, case analysis (conditional statements), iterative (loops), recursive, and library of previously solved patterns. This is an interesting way of thinking about how to break down problems
- The book suggests coding a loop in the following order: body, termination, initialization, finalization, boundary conditions (first & last iteration). I've never consciously thought about the order--it may be worth trying in the future

## 5. Online Algorithms
- Online algorithm is defined in [Wikipedia](https://en.wikipedia.org/wiki/Online_algorithm) as "_process its input piece-by-piece in a serial fashion, i.e., in the order that the input is fed to the algorithm, without having the entire input available from the start_". The keys are that you cannot store the input as it comes in, only update summary values, and you have to make decisions for each input without being able to look at the up-coming input.
- The book suggests that loop invariants are particularly visible, and crucial to specify correctly, in online algorithms

## 6. Enumeration Patterns
- Enumeration is defined in [Wikipedia](https://en.wikipedia.org/wiki/Enumeration) as "_complete, ordered listing of all the items in a collection_"
- The book points out two commonly off-by-one errors: the index associated with the nth object is n-1, and the number of objects between index m and n is m-n+1
- The `BigInteger` class is described in the Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/math/BigInteger.html) as "_immutable arbitrary-precision integers_"
- In the Python [documentation](https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex), "_integers have unlimited precision_"
- The book presents a typical indeterminate enumeration: `while ( i <= maxi && condition )` then check at end if `i > maxi`
- The books recommends using `for` loops for determinate enumerations and `while` loops for indeterminate enumerations. This is good advice--I've seen example code use `for` loops for indeterminate enumerations (with and without `break` statements) and it's usually more confusing then it has to be
- 
- 



