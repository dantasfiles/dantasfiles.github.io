---
title: Notes on 🐯<i>Algorithms & Data Structures</i>
hidden: true
# subtitle: Princeton COS 226, Spring 2025 edition
author: Daniel Dantas
---


I was curious to learn what has been updated since I took a [version of this course at a 🐻 different university](https://dantasfiles.com/1998/08/27/cornell-freshman-fall.html), so I am reading through the [lecture notes for the Fall 2024 semester](https://www.cs.princeton.edu/courses/archive/fall24/cos226/)

I use these notes to keep track of anything that sticks out to me as interesting. My notes are incomplete as I have not yet finished reading the lecture notes

## 1. Introduction
  * “_Bad programmers worry about the code. Good programmers worry about data structures and their relationships_” by Linus Torvalds is a great quote

## 1. Union-find
  * The first pass of designing an algorithm can be simple concentric sweeps of the data. Optimize after fully understanding the simpler but slower algorithm.
  * When designing algorithms, consider creating an extra data structure (typically an array / list, or a map / dictionary) that will map items to information the algorithm needs or will generate (e.g. _visited_ , _parent, size_ )

## 2. Analysis of Algorithms
  * For [3SUM](https://en.wikipedia.org/wiki/3SUM), a first-draft algorithm can be three nested loops. Understand the simpler, slower algorithm, then optimize
  * Algorithms topics focus on system-independent effects, while systems topics focus on system-dependent effects like hardware, systems software, and operating system. I always found the latter super-interesting
  * Reminder that `(n choose k) = n!/k!(n-k)! = (n*…*(n-k+1))/k! `This [definition](https://en.wikipedia.org/wiki/Binomial_coefficient) often comes in useful
  * There used to be confusion over the size of a kilobyte: 10^3 (1,000) or 2^10 (1,024). Now _[kilo](https://en.wikipedia.org/wiki/Kilobyte)_[bytes](https://en.wikipedia.org/wiki/Kilobyte) are 10^3 (1,000) bytes, while _[kibi](https://en.wikipedia.org/wiki/Byte#Multiple-byte_units)_[bytes](https://en.wikipedia.org/wiki/Byte#Multiple-byte_units) are 2^10 (1,024) bytes. The same holds for other prefixes: _mega_ / _mebi_ , _giga_ / _gibi_ …
  * Modern processors in computers and mobile devices typically handle data in 64-bit (8-byte) blocks
  * In [Java](https://docs.oracle.com/javase/specs/jls/se23/html/jls-4.html#jls-4.2), _bytes_ are 8 bits, _short_ : 16 bits, _int_ : 32 bits, _long_ : 64 bits, _float_ : 32 bits, _double_ : 64 bits, _char_ : 16 bit [unicode](https://en.wikipedia.org/wiki/UTF-16), _boolean_ s use an unspecified number of bits

## Stacks & Queues

### 3. S&Q: Resizable Arrays
  * Stacks and queues occur in [real life](https://en.wikipedia.org/wiki/Queueing_theory) as well as in computer science
  * The fundamental methods of a stack are _push_ , _pop_ , and _isEmpty_
  * The fundamental methods of a queue are _enqueue_ , _dequeue_ , and _isEmpty_
  * If implementing stacks and queues as an array, be aware that if the object reference in the underlying array is not explicitly set to null after popping or dequeuing the object, Java garbage collection will not understand that the object has been removed from the stack or queue
  * A common tactic in implementing a mutable data structure as a fixed-length array, is, upon overflow, to create a new array a certain percent larger than the old array. Then the old array is copied to the new larger array  
Java _[ArrayLists](https://github.com/openjdk/jdk/blob/8f6ccde9829ea0e4fe1c087e68bec4d9efb55c64/src/java.base/share/classes/java/util/ArrayList.java#L232)_ typically expand as necessary to 1.5x the previous array size
  * Python's implementation of lists as resizeable arrays is mentioned. The time complexity of various Python list operations [is examined here](https://wiki.python.org/moin/TimeComplexity)
  * A queue can be implemented with two stacks: a push stack and a pop stack. The items on the push stack are moved into the pop stack as necessary.
  * Generic array creation is not allowed: `new T[n]`. This is because once your code is compiled, type parameters like `T` are [erased](https://docs.oracle.com/javase/tutorial/java/generics/erasure.html) (to enable backwards compatibility and reduce runtime overhead), and cannot be used at runtime. Instead, an explicit cast is necessary: `T[] a = (T[]) new Object[n])`

### 4. S&Q: Linked Lists
- Linked list implementations of lists are simpler to resize than array implementations, but take up more memory, and are slow when accessing random elements of the list and when accessing list in order (due to [sequential locality](https://en.wikipedia.org/wiki/Locality_of_reference) and caching).
- Typical linked list iteration code is `for (Node n = first; n != null; n = n.next) {`
- Implementations typically need an empty-list case, where first and last pointers are null; and a normal case, where first and last pointers point to nodes
- To implement the [`Iterable`](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Iterable.html) interface, your `iterator` method can either use an inner class that implements the `Iterator` interface, or it can just return an iterator on a instance variable of your class
- A diagram of the Java Collections Framework is located [here](https://docs.oracle.com/javase/tutorial/collections/interfaces/index.html)
- A table summarizing the Java Collections Framework is located [here](https://docs.oracle.com/javase/tutorial/collections/implementations/index.html), and is copied here as well

| Interfaces	| Hash table Impl.	| Resizable array Impl.	| Tree Impl.	| Linked list Impl.	| Hash table + Linked list Impl. |
| --- | --- | --- | --- | --- | --- |
| Set	| HashSet	| | TreeSet	| |	LinkedHashSet |
| List	| |	ArrayList	| |	LinkedList | |
| Queue | | | | | |	 	 	 	 	 
| Deque	| | ArrayDeque | | LinkedList | |	 
| Map	| HashMap	| | TreeMap | |	LinkedHashMap |

## 5. Elementary Sorts
- Sorts are defined as requiring a binary relation that is transitive and comparable (a ≤ b and/or b ≤ a). I believe implementing the Java `Comparable` interface requires a [total ordering](https://en.wikipedia.org/wiki/Total_order), where it's recommended that if `a` ≤ `b` and `b` ≤ `a`, then `a.equals(b)`
- It's claimed that Python uses first-class functions to enable sorting. However, this was [changed in Python 3](https://docs.python.org/3/whatsnew/3.0.html#ordering-comparisons): "_`sorted()` and `list.sort()` no longer accept the cmp argument providing a comparison function. Use the key argument instead_"
- An example in the notes uses the [raw type](https://docs.oracle.com/javase/tutorial/java/generics/rawTypes.html) `Comparable`. This bypasses generic type checking and relies on runtime exceptions to determine when something goes wrong with the `compareTo` method.
- The notes use a clever trick of defining each sort algorithm in terms of a common `less` comparison and an `exch` exchange methods to make analyzing running time easier.
- _Selection sort_ has O(n²) compares, O(n) exchanges, and O(1) extra space
- The notes refer the fun blog post: _[Extra, Extra - Read All About It: Nearly All Binary Searches and Mergesorts are Broken](https://research.google/blog/extra-extra-read-all-about-it-nearly-all-binary-searches-and-mergesorts-are-broken/)_. It's very easy to get the fundamental algorithms wrong: a longstanding overflow bug involved using `int mid = (low + high) / 2;` instead of `int mid = low + ((high - low) / 2);`
- 3-Sum in O(n²) time and O(1) extra space uses 3 pointers. For each i, set j to i+1 and k to end, and iterate j and k inward, marking all sums.
- _Insertion sort_ has worst-case O(n²) compares and exchanges
- _Binary insertion sort_ has worst-case O(n log n) compares and O(n²) exchanges
- _Binary search_ has worst-case O(n log n) compares 

### 6. Mergesort

