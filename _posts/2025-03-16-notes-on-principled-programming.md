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

