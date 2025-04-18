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
- The book presents the canonical list iteration: `while (n != null) { _do something_; n = n.next; }`. A `for` loop version is also presented, but I prefer not to use `for` loops when the length is unspecified
- Tail call is defined in [Wikipedia](https://en.wikipedia.org/wiki/Tail_call) as "_a subroutine call performed as the final action of a procedure. If the target of a tail is the same subroutine, the subroutine is said to be tail recursive.... Tail calls can be implemented without adding a new stack frame to the call stack.... Tail recursion can be related to the while statement, an explicit iteration_"
- The book points out that Java does not implement tail call optimization. I believe one reason is that the Java security mechanism does stack inspection

## 14. Linked Lists
- The Java [documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/doc-files/coll-reference.html) describes List implementations as follows: "_ArrayList - Resizable array implementation of the List interface (an unsynchronized Vector). The best all-around implementation of the List interface. ArrayDeque - Efficient, resizable array implementation of the Deque interface. LinkedList - Doubly-linked list implementation of the List interface. Provides better performance than the ArrayList implementation if elements are frequently inserted or deleted within the list. Also implements the Deque interface. When accessed through the Queue interface, LinkedList acts as a FIFO queue_"
<!-- I believe there are bugs in the implementation of `MList`. In the `prepend` method, the `tail` should point to the new node if the list was previously empty. In the `append` and `remove` methods, the `last` pointer doesn't get set correctly --> 

## 15. Parametric polymorphism (generics)
- Subtype polymorphism is defined in [Wikipedia](https://en.wikipedia.org/wiki/Subtyping) as "_a form of type polymorphism. A subtype is a datatype that is related to another datatype (the supertype) by some notion of substitutability, meaning that program elements (typically subroutines or functions), written to operate on elements of the supertype, can also operate on elements of the subtype_"
- Parametric polymorphism is defined in [Wikipedia](https://en.wikipedia.org/wiki/Parametric_polymorphism) as "_allows a single piece of code to be given a 'generic' type, using variables in place of actual types, and then instantiated with particular types as needed_"
- The books has a clever contrast of subtype polymorphism, where a client can use multiple implementations of an interface, with parametric polymorphism, where an interface can be used by multiple clients in different ways
- Type inference is defined in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/generics/genTypeInference.html) as "_a Java compiler's ability to look at each method invocation and corresponding declaration to determine the type argument (or arguments) that make the invocation applicable. The inference algorithm determines the types of the arguments and, if available, the type that the result is being assigned, or returned. Finally, the inference algorithm tries to find the most specific type that works with all of the arguments_"
- The Java [documentation](https://docs.oracle.com/javase/tutorial/java/generics/inheritance.html) discusses generics and subtypes: "_Given two concrete types A and B..., `MyClass<A>` has no relationship to `MyClass<B>`, regardless of whether or not A and B are related. The common parent of `MyClass<A>` and `MyClass<B>` is `Object`_"
- Variance is defined in [Wikipedia](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)) as "_the category of possible relationships between more complex types and their components' subtypes_"
- The Java [documentation](https://docs.oracle.com/javase/tutorial/java/generics/wildcardGuidelines.html) discusses wildcards: "_An "in" variable serves up data to the code.... An "out" variable holds data for use elsewhere.... An "in" variable is defined with an upper bounded wildcard, using the `extends` keyword. An "out" variable is defined with a lower bounded wildcard, using the `super` keyword_". This is basically covariance and contravariance
- Type erasure is defined in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/generics/erasure.html) as "_To implement generics, the Java compiler applies type erasure to: - Replace all type parameters in generic types with their bounds or Object if the type parameters are unbounded. The produced bytecode, therefore, contains only ordinary classes, interfaces, and methods..._"
- Raw type is defined in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/generics/rawTypes.html) as "_the name of a generic class or interface without any type arguments.... When using raw types, you essentially get pre-generics behavior_"
- Lembda expressions are defined in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) as "_let you express instances of single-method classes more compactly_"
- Method references are definied in the Java [documentation](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html) as "_compact, easy-to-read lambda expressions for methods that already have a name_"

## 16. Asymptotic Complexity
- L'Hôpital's rule is defined in [Wikipedia](https://en.wikipedia.org/wiki/L%27H%C3%B4pital%27s_rule) as "_a mathematical theorem that allows evaluating limits of indeterminate forms using derivatives_". In certain cases, lim<sub>x→c</sub> f(x) / g(x) = lim<sub>x→c</sub> f'(x) / g'(x)

## 17. Trees
- Branching factor is defined in [Wikipedia](https://en.wikipedia.org/wiki/L%27H%C3%B4pital%27s_rule) as "_number of children at each node, the outdegree_"
- Height is defined in [Wikipedia](https://en.wikipedia.org/wiki/Tree_(abstract_data_type)#Terminology) as "_length of the longest downward path to a leaf from that node. The height of the root is the height of the tree_", while depth is "_length of the path to its root_"
- Binary search tree is defined in [Wikipedia](https://en.wikipedia.org/wiki/Binary_search_tree) as "_rooted binary tree data structure with the key of each internal node being greater than all the keys in the respective node's left subtree and less than the ones in its right subtree_"
- The Java documentation specifies the difference between the `Comparable` [interface](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/lang/Comparable.html): "_imposes a total ordering on the objects of each class that implements it. This ordering is referred to as the class's natural ordering, and the class's `compareTo` method is referred to as its natural comparison method. Lists (and arrays) of objects that implement this interface can be sorted automatically by Collections.sort (and Arrays.sort)_" and the `Comparator` [interface](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Comparator.html): "_a comparison function, which imposes a total ordering on some collection of objects. Comparators can be passed to a sort method (such as Collections.sort or Arrays.sort) to allow precise control over the sort order_"
- The book explains that many tree operations are expressed naturally as recursive functions
- In tree algorithms, there are usually variations in whether null is checked for before making a recursive call on a child, or at the start of each recursive call
- `TreeMap` is defined in the Java documentation as "_Red-Black tree based `NavigableMap` implementation. The map is sorted according to the natural ordering of its keys, or by a `Comparator` provided at map creation time, depending on which constructor is used_"
- Randomized algorithm is defined in [Wikipedia](https://en.wikipedia.org/wiki/Randomized_algorithm) as "_typically uses uniformly random bits as an auxiliary input to guide its behavior, in the hope of achieving good performance in the "average case" over all possible choices of random determined by the random bits; thus either the running time, or the output (or both) are random variables_"
- Fisher–Yates shuffle is defined in [Wikipedia](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle) as "_takes a list of all the elements of the sequence, and continually determines the next element in the shuffled sequence by randomly drawing an element from the list until no elements remain. The algorithm produces an unbiased permutation: every permutation is equally likely_" 
- The book directs that converting non-tail-recursive tree algorithms to iterative versions can either use parent pointers if available, or a explicit stack
- Tree sort is defined in [Wikipedia](https://en.wikipedia.org/wiki/Tree_sort) as "_builds a binary search tree from the elements to be sorted, and then traverses the tree (in-order) so that the elements come out in sorted order. Its typical use is sorting elements online_
- The book explains that range queries can be done by performing an in-order traversal that skips the unneeded parts of the tree
- Tree traversals are contrasted on [Wikipedia](https://en.wikipedia.org/wiki/Tree_traversal): "pre-order traversal is a topologically sorted one, because a parent node is processed before any of its child nodes is done.... Post-order traversal can be useful to get postfix expression of a binary expression tree.... in-order traversal retrieves the keys in ascending sorted order_"

## 18. Grammars and parsing
- Parse tree is defined in [Wikipedia](https://en.wikipedia.org/wiki/Parse_tree) as "_ordered, rooted tree that represents the syntactic structure of a string according to some context-free grammar_"
- Syntax error is defined in [Wikipedia](https://en.wikipedia.org/wiki/Syntax_error) as "_error in the syntax of a sequence of characters that is intended to be written in a particular programming language_"
- Formal grammar is defined in [Wikipedia](https://en.wikipedia.org/wiki/Formal_grammar) as "_describes which strings from an alphabet of a formal language are valid according to the language's syntax_"
- Context-free grammar is defined in [Wikipedia](https://en.wikipedia.org/wiki/Context-free_grammar) as "_formal grammar whose production rules can be applied to a nonterminal symbol regardless of its context_". For example a<sup>n</sup>b<sup>n</sup> is not context-free
- Symbols are defined in [Wikipedia](https://en.wikipedia.org/wiki/Terminal_and_nonterminal_symbols) as "_lexical elements used in specifying the production rules constituting a formal grammar_"
- Lexical tokenization is defined by Wikipedia as "_conversion of a text into (semantically or syntactically) meaningful lexical tokens belonging to categories defined by a 'lexer' program_"
- Production is defined in [Wikipedia](https://en.wikipedia.org/wiki/Production_(computer_science)) as "_rewrite rule specifying a symbol substitution that can be recursively performed to generate new symbol sequences_"
- Formal language is defined in [Wikipedia](https://en.wikipedia.org/wiki/Formal_language) as "_words whose letters are taken from an alphabet and are well-formed according to a specific set of rules called a formal grammar_"
- Recursive grammar is defined in [Wikipedia](https://en.wikipedia.org/wiki/Recursive_grammar) as "_production rules that are recursive, meaning that expanding a non-terminal according to these rules can eventually lead to a string that includes the same non-terminal again_"
- Ambiguous grammar is defined in [Wikipedia](https://en.wikipedia.org/wiki/Ambiguous_grammar) as "_context-free grammar for which there exists a string that can have more than one leftmost derivation or parse tree_"
- Recursive-descent parser is defined in [Wikipedia](https://en.wikipedia.org/wiki/Recursive_descent_parser) as "_top-down parser built from a set of mutually recursive procedures (or a non-recursive equivalent) where each such procedure implements one of the nonterminals of the grammar_", and predictive parser as "_a recursive descent parser that does not require backtracking_"
- Abstract syntax tree is defined in [Wikipedia](https://en.wikipedia.org/wiki/Abstract_syntax_tree) as "_tree representation of the abstract syntactic structure of text (often source code) written in a formal language.... The syntax is 'abstract' in the sense that it does not represent every detail appearing in the real syntax, but rather just the structural or content-related details_"
- Left recursion is defined in [Wikipedia](https://en.wikipedia.org/wiki/Left_recursion) as "_special case of recursion where a string is recognized as part of a language by the fact that it decomposes into a string from that same language (on the left) and a suffix (on the right).... Left recursion often poses problems for parsers, either because it leads them into infinite recursion (as in the case of most top-down parsers) or because they expect rules in a normal form that forbids it (as in the case of many bottom-up parsers). Therefore, a grammar is often preprocessed to eliminate the left recursion_"
- Metasyntax is defined in [Wikipedia](https://en.wikipedia.org/wiki/Metasyntax) as "_syntax used to define the syntax of a programming language or formal language. It describes the allowable structure and composition of phrases and sentences of a metalanguage, which is used to describe either a natural language or a computer programming language_"

## 19. Hash tables
- Map is defined in [Wikipedia](https://en.wikipedia.org/wiki/Associative_array) as "_abstract data type that stores a collection of (key, value) pairs, such that each possible key appears at most once in the collection_"
- Partial function is defined in [Wikipedia](https://en.wikipedia.org/wiki/Partial_function) as "_binary relation over two sets that associates to every element of the first set at most one element of the second set_"
- Lookup table is definied in [Wikipedia](https://en.wikipedia.org/wiki/Lookup_table) as "_array that replaces runtime computation of a mathematical function with a simpler array indexing operation, in a process termed as direct addressing_"
- Injective function is defined in [Wikipedia](https://en.wikipedia.org/wiki/Injective_function) as "_maps distinct elements of its domain to distinct elements of its codomain_"
- Hash functions are discussed on [Wikipedia](https://en.wikipedia.org/wiki/Hash_function#Uniformity): "_A good hash function should map the expected inputs as evenly as possible over its output range. That is, every hash value in the output range should be generated with roughly the same probability. The reason for this last requirement is that the cost of hashing-based methods goes up sharply as the number of collisions—pairs of inputs that are mapped to the same hash value—increases_"
- Separate chaining is defined in [Wikipedia](https://en.wikipedia.org/wiki/Hash_table#Separate_chaining) as "_building a linked list with key–value pair for each search array index_"
- Open addressing / closed hashing / probing is defined in [Wikipedia](https://en.wikipedia.org/wiki/Open_addressing) as "_searching through alternative locations in the array (the probe sequence) until either the target record is found, or an unused array slot is found, which indicates that there is no such key in the table_"
- 



