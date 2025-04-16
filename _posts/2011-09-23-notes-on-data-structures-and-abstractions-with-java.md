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


- 
- 
