---
title: Notes on 📕<i>Data Structures & Abstractions with Java</i> by Frank M. Carrano
description: "In-progress, incomplete"
hidden: true
author: Daniel Dantas
---

I use these notes to track thoughts I had, and things I found interesting, while reading _Data Structures & Abstractions with Java_

The notes are still in progress as I have not yet finished reading the book

## Introduction
- Abstract data types and data structures are contrasted in Wikipedia [as](https://en.wikipedia.org/wiki/Abstract_data_type) as "_an abstract data type (ADT) is a mathematical model for data types, defined by its behavior (semantics) from the point of view of a user of the data, specifically in terms of possible values, possible operations on data of this type, and the behavior of these operations. This mathematical model contrasts with data structures, which are concrete representations of data, and are the point of view of an implementer, not a user_" and [as](https://en.wikipedia.org/wiki/Data_structure) "_Data structures serve as the basis for abstract data types (ADT). The ADT defines the logical form of the data type. The data structure implements the physical form of the data type_"

## 1. Bags
- A data type is defined in [Wikipedia](https://en.wikipedia.org/wiki/Data_type) as "_a collection or grouping of data values, usually specified by a set of possible values, a set of allowed operations on these values, and/or a representation of these values as machine types_"
- According to the Java [documentation](https://docs.oracle.com/javase/tutorial/java/javaOO/methods.html), "_You cannot declare more than one method with the same name and the same number and type of arguments, because the compiler cannot tell them apart_"
- The book recommends writing code that uses and tests the interface before attempting to implement the interface
- Encapsulation is definied in [Wikipedia](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) as "_the bundling of data with the mechanisms or methods that operate on the data_"
- The book recommends designing an abstract data type by only worrying about how the user will use it, and not about the implementation. There can be a tendency to let the underlying algorithms influence the interface, but this recommendation would resist that

## 2. Bag Implementations That Uses Arrays
- The `final` keyword in Java on a field ensures that the field cannot be changed after its initial assignment (though the contents of the field can change)
- There are three ways (at least) to shallow copy arrays: [Object.clone](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/lang/Object.html#clone()), [System.arraycopy](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/lang/System.html#arraycopy(java.lang.Object,int,java.lang.Object,int,int)), and [Arrays.copyOf](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Arrays.html#copyOf(T%5B%5D,int)). The latter two methods are useful for resizing arrays
- This book has a style where they set a result in various branches and then return the result at the end of the method when all the branches have come back together, instead of returning early when and if necessary. I find the latter style easier to understand
- The use of `.equals` as an equivalence relation has issues with `null`s
- The reason doubling is used in array resizing is it lets the `add`s have an amortized O(1) running time (each `add` banks a constant amount of time for copying during a resize)

## 3. A Bag Implementation That Links Data
- Inner / nested class is defined in [Wikipedia](https://en.wikipedia.org/wiki/Inner_class) as "_a class declared entirely within the body of another class or interface_"
- The book defines a nontraditional list remove method: it replaces the to-be-removed node's data with the first node's data, then pops the first node
- The book defines a list clear method as continually popping from the list, with O(n) running time. But it seems simpler to set the head reference to null and let the garbage collector do the work
- The Java [documentation](https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html) states "_If a class has no modifier (the default, also known as package-private), it is visible only within its own package_", which the book points out is an alternative to inner classes
- The Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/doc-files/coll-reference.html) describes List implementations as follows: "_ArrayList - Resizable array implementation of the List interface (an unsynchronized Vector). The best all-around implementation of the List interface. LinkedList - Doubly-linked list implementation of the List interface. Provides better performance than the ArrayList implementation if elements are frequently inserted or deleted within the list_"

## 4. The Efficiency of Algorithms
- Complexity is defined in [Wikipedia](https://en.wikipedia.org/wiki/Computational_complexity) as "_amount of resources required to run it. Particular focus is given to computation time (generally measured by the number of needed elementary operations) and memory storage requirements_"
- Analysis of algorithms is defined in [Wikipedia](https://en.wikipedia.org/wiki/Analysis_of_algorithms) as "_the process of finding the computational complexity of algorithms_"
- Big O notation is defined by [Wikipedia](https://en.wikipedia.org/wiki/Big_O_notation) as "_mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity_"

## 5. Stacks
- The book points out that pushing items onto, and then popping all items from a stack, reverses the order
- The book points out that infix operators require precedence and parentheses to process as expected, but prefix and postfix bake the precedence into the expression `1+2*4 vs. `1 2 4 * +`
- Shunting yard algorithm is defined in [Wikipedia](https://en.wikipedia.org/wiki/Shunting_yard_algorithm) as "_method for parsing arithmetical or logical expressions, or a combination of both, specified in infix notation... The input is processed one symbol at a time: if a variable or number is found, it is copied directly to the output... If the symbol is an operator, it is pushed onto the operator stack... If the operator's precedence is lower than that of the operators at the top of the stack or the precedences are equal and the operator is left associative, then that operator is popped off the stack and added to the output... Finally, any remaining operators are popped off the stack and added to the output_"
- The book explains that instead of outputting the result of the shunting yard algorithm as a postfix expression, you can evaluate it on the fly by using an operand stack
- Frame is defined in the Java [documentation](https://docs.oracle.com/javase/specs/jvms/se24/html/jvms-2.html#jvms-2.6) as "_used to store data and partial results, as well as to perform dynamic linking, return values for methods, and dispatch exceptions_"
- Java Virtual Machine stack is defined in the Java [documentation](https://docs.oracle.com/javase/specs/jvms/se24/html/jvms-2.html#jvms-2.5.2) as "_stores frames... it holds local variables and partial results, and plays a part in method invocation and return. Because the Java Virtual Machine stack is never manipulated directly except to push and pop frames, frames may be heap allocated. The memory for a Java Virtual Machine stack does not need to be contiguous_"
- `java.util.ArrayDeque<E>` is defined by the Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/doc-files/coll-reference.html) as "_efficient, resizable array implementation of the `Deque` interface_"

## 6. Stack Implementations
- Stacks using linked lists are described in [Wikipedia](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)#Linked_list) as "_Another option for implementing stacks is to use a singly linked list. A stack is then a pointer to the "head" of the list, with perhaps a counter to keep track of the size of the list...Pushing and popping items happens at the head of the list_"
- Stacks using arrays are described in [Wikipedia](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)#Array) as "_The program must keep track of the size (length) of the stack, using a variable top that records the number of items pushed so far, therefore pointing to the place in the array where the next element is to be inserted.... The size of the stack is simply the size of the dynamic array, which is a very efficient implementation of a stack since adding items to or removing items from the end of a dynamic array requires amortized O(1) time_"
- `java.util.Arrays.copyof` is described in the Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Arrays.html#copyOf(T%5B%5D,int)) as "_Copies the specified array, truncating or padding with nulls (if necessary) so the copy has the specified length_"
- The book makes sure to set the stack array to null upon pop or clear, so that garbage collection can kick in
- The book uses a `Vector`, but the current version is `java.util.ArrayList` which is described in the Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/ArrayList.html) as "_Resizable-array implementation of the List interface.... The `size`, `isEmpty`, `get`, `set`, `getFirst`, `getLast`, `removeLast`, `iterator`, `listIterator`, and `reversed` operations run in constant time. The `add`, and `addLast` operations runs in amortized constant time, that is, adding n elements requires O(n) time. All of the other operations_ \[e.g. `addFirst`\] _run in linear time (roughly speaking). The constant factor is low compared to that for the LinkedList implementation_"
- The book advises that a stack should not inherit from a vector because a stack has-a vector, not is-a vector
- Is-a is defined in Wikipedia as "_subsumptive relationship between abstractions (e.g., types, classes), wherein one class A is a subclass of another class B (and so B is a superclass of A). In other words, type A is a subtype of type B when A's specification implies B's specification. That is, any object (or class) that satisfies A's specification also satisfies B's specification, because B's specification is weaker_"
- Has-a is defined in Wikipedia as "_composition relationship where one object (often called the constituted object, or part/constituent/member object) 'belongs to' (is part or member of) another object (called the composite type), and behaves according to the rules of ownership. In simple words, has-a relationship in an object is called a member field of an object_"

## 7. Recursion

-  
