---
title: Notes on 📕<i>Algorithms</i> by 🐯Sedgewick & Wayne</i>
description: "In-progress, incomplete"
hidden: true
author: Daniel Dantas
---

These are thoughts I had, and things I found interesting, while reading [Algorithms](https://algs4.cs.princeton.edu/)

The notes are still in progress as I have not yet finished reading the book

## 1. Fundamentals
- An algorithm is defined in [Wikipedia](https://en.wikipedia.org/wiki/Algorithm) as "_a finite sequence of mathematically rigorous instructions, typically used to solve a class of specific problems or to perform a computation_". I don't really like the Wikipedia definition, the definition in this book is better.

### 1.1 Basic Programming Model
- Data abstraction is defined in [Wikipedia](https://en.wikipedia.org/wiki/Abstraction_(computer_science)#Data_abstraction) as "_a clear separation between the abstract properties of a data type and the concrete details of its implementation_"
- The book recommends using data all of the same primitive data type in expressions if at all possible instead of trying to figure out the intricacies of type conversion
- Strongly typed is definited in [Wikipedia](https://en.wikipedia.org/wiki/Strong_and_weak_typing) as "_stricter typing rules at compile time, which implies that errors are more likely to happen during compilation_"
- The books points out that recursive calls that overlap create great inefficiencies. This is why memoization / dynamic programming can help to avoid exponential running times.
- The book points out that the variable in a for loop is only in scope in the for loop block. If you need the value of that value outside the block, use a while loop (or save it somewhere)
- To print an array, use the [Arrays.toString](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Arrays.html#toString(java.lang.Object%5B%5D)) helper functions

### 1.2 Data Abstraction
- Abstract data type is defined in [Wikipedia](https://en.wikipedia.org/wiki/Abstract_data_type) as "_a mathematical model for data types, defined by its behavior (semantics) from the point of view of a user of the data, specifically in terms of possible values, possible operations on data of this type, and the behavior of these operations_"
- Aliasing is defined in [Wikipedia](https://en.wikipedia.org/wiki/Aliasing_(computing)) as "_a situation in which a data location in memory can be accessed through different symbolic names in the program_"
- Java's parameter-passing strategy is sometimes [called](https://en.wikipedia.org/wiki/Evaluation_strategy#Call_by_sharing) "call by sharing," but I agree with the book that it's pass by value for all practical purposes
- Generic type is defined by the Java [documentation](https://docs.oracle.com/javase/tutorial/java/generics/types.html) as "_a generic class or interface that is parameterized over types_"
- There's a nod in the book toward factory method patterns, but then it clarifies that the only advanced Java language topics that are going to be used are generics and iterators
- Encapsulation is defined in [Wikipedia](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) as "_the bundling of data with the mechanisms or methods that operate on the data. It may also refer to the limiting of direct access to some of that data, such as an object's components_"
- The book warns that APIs typically become too wide, because it's easy to add methods, but difficult to deprecate them
- The book contrasts interface inheritance / subtyping, with implementation inheritance / subclassing, though the definitions are a bit mixed together. Differences includee that the latter does not necessarily imply behavioral subtyping, and the latter can break encapsulation. The book recommends using interface inheritance, but using implementation inheritance only in particular situations and not in general
- Fragile base class problem is defined by [Wikipedia](https://en.wikipedia.org/wiki/Fragile_base_class) as "_base classes (superclasses) are considered "fragile" because seemingly safe modifications to a base class, when inherited by the derived classes, may cause the derived classes to malfunction_"
- Equivalence relation is defined by [Wikipedia](https://en.wikipedia.org/wiki/Equivalence_relation) as "_a binary relation that is reflexive, symmetric, and transitive_"
- The book recommends a standard `equals` implementation: check for reference equality, check for null, use `getClass` to check for same class (this is mostly, but not always desired), then check instance variables
- `Final` is defined in [Wikipedia](https://en.wikipedia.org/wiki/Final_(Java)) as "_an entity that can only be assigned once_". Note that even if a field is final, if it is a reference type, the underlying object can change state
- The book states immutable objects means that you are always creating new objects when you work with them, but that the Java garbage collector is optimized for that case
- Design by contract is defined in [Wikipedia](https://en.wikipedia.org/wiki/Design_by_contract) as "_software designers should define formal, precise and verifiable interface specifications for software components, which extend the ordinary definition of abstract data types with preconditions, postconditions and invariants_"
- The book recommends using exceptions to guard against problems outside your control, and assertions to guard against problems inside your control
- Fail-fast system is defined in [Wikipedia](https://en.wikipedia.org/wiki/Fail-fast_system) as "_immediately reports at its interface any condition that is likely to indicate a failure. Fail-fast systems are usually designed to stop normal operation rather than attempt to continue a possibly flawed process_"
- The book questions why Java does not have first class functions. Modern versions of Java have [lambda expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) and [functional interfaces](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/function/package-summary.html), which provide an approximation
- The book points out that Java use of both primitive and reference types is a compromise to allow the performance boost from primitive types
- The book points out that though Java is not thought of as having pointers, it does, but they are restricted to creation and assignment operators, which along with a good garbage collection algorithm and strong typing, eliminates many pointer problems
- The book recommends not using static variables except in certain cases

## 1.3 Bags, Queues & Stacks
- Parametric polymorphism is defined in [Wikipedias](https://en.wikipedia.org/wiki/Parametric_polymorphism) as "_allows a single piece of code to be given a "generic" type, using variables in place of actual types, and then instantiated with particular types as needed_"
- Autoboxing is defined in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html) as "_automatic conversion that the Java compiler makes between the primitive types and their corresponding object wrapper classes... If the conversion goes the other way, this is called unboxing_"
- `Iterable` is described in the Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/lang/Iterable.html) as "_implementing this interface allows an object to be the target of the enhanced for statement (sometimes called the "for-each loop" statement)... `Iterator<T> iterator()` Returns an iterator over elements of type T._"
- The book explains that stacks are useful for reversing the order of an arbitrary number of inputs
- The book describes an algorithm for evaluating arithmetic expressions that are fully surrounded by parentheses using an operator and an operand stack (pop from both as necessary and evaluate when hit a right parenthesis)
- Interpreter is defined in [Wikipedia](https://en.wikipedia.org/wiki/Interpreter_(computing)) as "_computer program that directly executes instructions written in a programming or scripting language, without requiring them previously to have been compiled into a machine language program_"
- The restrictions on generics in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/generics/restrictions.html) include "_you cannot create arrays of parameterized types_"
- `java.util.Arrays.copyOf` is described in the Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Arrays.html#copyOf(T%5B%5D,int)) as "_copies the specified array, truncating or padding with nulls (if necessary) so the copy has the specified length_"
- The book recommends setting references to null when no longer needed, rather than letting them loiter and avoid being garbage collected
- `java.util.Iterator` is described in the Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Iterator.html) as "_`boolean hasNext()` Returns true if the iteration has more elements. `E next()` Returns the next element in the iteration_"
- The book recommends overriding the default `remove` method for Iterators with a blank one (or throw an `UnsupportedOperationException`), because using the `remove` method can cause all kinds of confusion
- In the Iterator example in the book, `ReverseArrayIterator` isn't `ReverseArrayIterator<Item>` because it uses the outer class's type parameter, not defines a new one of its own
- Initializing fields is discussed in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/javaOO/initial.html) as "_you can often provide an initial value for a field in its declaration.... However, this form of initialization has limitations because of its simplicity.... Instance variables can be initialized in constructors, where error handling or other logic can be used_"
- The book explains that adding a new field (like adding a tail reference to a linked list) may make certain operations easier/faster, but also adds new invariants that need to be maintained in all operations (like when removing the first item in a list)
- Doubly linked lists are described in [Wikipedia](https://en.wikipedia.org/wiki/Doubly_linked_list) as "_while adding or removing a node in a doubly linked list requires changing more links than the same operations on a singly linked list, the operations are simpler and potentially more efficient (for nodes other than first nodes) because there is no need to keep track of the previous node during traversal or no need to traverse the list to find the previous node, so that its link can be modified_"
- The book provides a for loop idiom to traverse a linked list. I prefer a while loop--to me, it makes it easier to understand the traversal
- The book explains how data structures drive the fields of a class, while algorithms guide the methods. I think the separation is more porous--data structures often encompass the operations on the values
- Covariant arrays are described in [Wikipedia](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)#Covariant_arrays_in_Java_and_C#) as "_early versions of Java and C# did not include generics, also termed parametric polymorphism. In such a setting, making arrays invariant rules out useful polymorphic programs.... Therefore, both Java and C# treat array types covariantly.... With the addition of generics, Java and C# now offer ways to write this kind of polymorphic function without relying on covariance_"
- Type erasure is described in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/generics/erasure.html) as "_To implement generics, the Java compiler applies type erasure to: Replace all type parameters in generic types with their bounds or Object if the type parameters are unbounded. The produced bytecode, therefore, contains only ordinary classes, interfaces, and methods..._"
- The book points out that you can create an array of parametrized types by creating an array of the raw type then using an unchecked conversion to the parametrized type. However, it's better to use something like an `ArrayList` instead
- Static nested class is defined in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html) as "_do not have access to other members of the enclosing class.... In effect, a static nested class is behaviorally a top-level class that has been nested in another top-level class for packaging convenience._" Because static inner classes are treated like a top-level class, you have to be careful with generics
- The Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/doc-files/coll-reference.html) describes the following classes: "_`ArrayList` - Resizable array implementation of the List interface (an unsynchronized Vector). The best all-around implementation of the List interface. \[removeFirst is not O(1)\] `ArrayDeque` - Efficient, resizable array implementation of the Deque interface.
`LinkedList` - Doubly-linked list implementation of the List interface. Provides better performance than the ArrayList implementation if elements are frequently inserted or deleted within the list. Also implements the Deque interface. When accessed through the Queue interface, LinkedList acts as a FIFO queue_". The book points out that these classes frequently have wide interfaces, which may make them less efficient, and the client code harder to understand, than classes with more narrow interfaces
- Fail-fast iterator is defined in the Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/ArrayList.html) as "_if the list is structurally modified at any time after the iterator is created, in any way except through the iterator's own remove or add methods, the iterator will throw a `ConcurrentModificationException`. Thus, in the face of concurrent modification, the iterator fails quickly and cleanly, rather than risking arbitrary, non-deterministic behavior at an undetermined time in the future_"

## 1.4 Analysis of Algorithms
- The book points out that analyzing software is much less involved that analyzing the physical sciences and engineering world





