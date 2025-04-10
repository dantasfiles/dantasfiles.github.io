---
title: "Notes on 🐯<i>Algorithms & Data Structures</i>"
description: "This course surveys the most important algorithms and data structures in use on computers today"
hidden: true
author: Daniel Dantas
---


I was curious to learn what has been updated since I took a [version of COS 226 at a 🐻different university](https://dantasfiles.com/1998/08/27/cornell-freshman-fall.html), so I am reading through the [lecture slides for the Fall 2024 semester](https://www.cs.princeton.edu/courses/archive/fall24/cos226/)

I use these notes to keep track of my thoughts while reading and to record anything that sticks out to me as interesting.

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

## 3. Stacks & Queues: Resizable Arrays
  * Stacks and queues occur in [real life](https://en.wikipedia.org/wiki/Queueing_theory) as well as in computer science
  * The fundamental methods of a stack are _push_ , _pop_ , and _isEmpty_
  * The fundamental methods of a queue are _enqueue_ , _dequeue_ , and _isEmpty_
  * If implementing stacks and queues as an array, be aware that if the object reference in the underlying array is not explicitly set to null after popping or dequeuing the object, Java garbage collection will not understand that the object has been removed from the stack or queue
  * A common tactic in implementing a mutable data structure as a fixed-length array, is, upon overflow, to create a new array a certain percent larger than the old array. Then the old array is copied to the new larger array  
Java _[ArrayLists](https://github.com/openjdk/jdk/blob/8f6ccde9829ea0e4fe1c087e68bec4d9efb55c64/src/java.base/share/classes/java/util/ArrayList.java#L232)_ typically expand as necessary to 1.5x the previous array size
  * Python's implementation of lists as resizeable arrays is mentioned. The time complexity of various Python list operations [is examined here](https://wiki.python.org/moin/TimeComplexity)
  * A queue can be implemented with two stacks: a push stack and a pop stack. The items on the push stack are moved into the pop stack as necessary.
  * Generic array creation is not allowed: `new T[n]`. This is because once your code is compiled, type parameters like `T` are [erased](https://docs.oracle.com/javase/tutorial/java/generics/erasure.html) (to enable backwards compatibility and reduce runtime overhead), and cannot be used at runtime. Instead, an explicit cast is necessary: `T[] a = (T[]) new Object[n])`

## 4. Stacks & Queues: Linked Lists
- Linked list implementations of lists are simpler to resize than array implementations, but take up more memory, and are slow when accessing random elements of the list and when accessing list in order (due to [sequential locality](https://en.wikipedia.org/wiki/Locality_of_reference) and caching).
- Typical linked list iteration code is `for (Node n = first; n != null; n = n.next) {`
- Implementations typically need an empty-list case, where first and last pointers are null; and a normal case, where first and last pointers point to nodes
- To implement the [`Iterable`](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Iterable.html) interface, your `iterator` method can either use an inner class that implements the `Iterator` interface, or it can just return an iterator on a instance variable of your class
- A diagram of the Java Collections Framework is located [here](https://docs.oracle.com/javase/tutorial/collections/interfaces/index.html)
- A table summarizing the Java Collections Framework is located [here](https://docs.oracle.com/javase/tutorial/collections/implementations/index.html), and is copied here as well

| Interfaces	| Hash table Impl.	| Resizable array Impl.	| Tree Impl.	| Linked list Impl.	| Hash table + Linked list Impl. | Synchronized Version |
| --- | --- | --- | --- | --- | --- | --- |
| [Set](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Set.html)	| ✨[HashSet](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/HashSet.html)✨	| | [TreeSet](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/TreeSet.html) (implements [SortedSet](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/SortedSet.html))	| |	[LinkedHashSet](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/LinkedHashSet.html) | |
| [List](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/List.html)	| |	✨[ArrayList](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/ArrayList.html)✨	| |	[LinkedList](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/LinkedList.html) | | |
| [Queue](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Queue.html) | | | | [LinkedList](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/LinkedList.html) | | [BlockingQueue](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/concurrent/BlockingQueue.html) | 
| [Deque](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Deque.html) (implements [Queue](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Queue.html))	| | [ArrayDeque](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/ArrayDeque.html) | | [LinkedList](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/LinkedList.html) | | |
| [Map](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Map.html)	| ✨[HashMap](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/HashMap.html)✨	| | [TreeMap](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/TreeMap.html) (implements [SortedMap](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/SortedMap.html)) | |	[LinkedHashMap](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/LinkedHashMap.html) | [ConcurrentMap](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html) |

## 5. Elementary Sorts
- Sorts are defined as requiring a binary relation that is transitive and comparable (a ≤ b and/or b ≤ a). I believe implementing the Java `Comparable` interface requires a [total ordering](https://en.wikipedia.org/wiki/Total_order), where it's recommended that if `a` ≤ `b` and `b` ≤ `a`, then `a.equals(b)`
- It's claimed that Python uses first-class functions to enable sorting. However, this was [changed in Python 3](https://docs.python.org/3/whatsnew/3.0.html#ordering-comparisons): "_`sorted()` and `list.sort()` no longer accept the cmp argument providing a comparison function. Use the key argument instead_"
- An example in the slides uses the [raw type](https://docs.oracle.com/javase/tutorial/java/generics/rawTypes.html) `Comparable`. This bypasses generic type checking and relies on runtime exceptions to determine when something goes wrong with the `compareTo` method.
- The slides use a clever trick of defining each sort algorithm in terms of a common `less` comparison and an `exch` exchange methods to make analyzing running time easier.
- _Selection sort_ has O(n²) compares, O(n) exchanges, and O(1) extra space
- The slides refer the fun blog post: _[Extra, Extra - Read All About It: Nearly All Binary Searches and Mergesorts are Broken](https://research.google/blog/extra-extra-read-all-about-it-nearly-all-binary-searches-and-mergesorts-are-broken/)_. It's very easy to get the fundamental algorithms wrong: a longstanding overflow bug involved using `int mid = (low + high) / 2;` instead of `int mid = low + ((high - low) / 2);`
- 3-Sum in O(n²) time and O(1) extra space uses 3 pointers. For each i, set j to i+1 and k to end, and iterate j and k inward, marking all sums.
- _Insertion sort_ has worst-case O(n²) compares and exchanges
- _Binary insertion sort_ has worst-case O(n log n) compares and O(n²) exchanges
- _Binary search_ has worst-case O(n log n) compares 

## 6. Mergesort
- The slides provide good advice about not allocating a helper array inside a recursive method, because then you have as many arrays in memory as the depth of the recursive call stack. Instead allocate the helper array outside, and then pass it in to the recursive method.
- Java uses quicksort on primitive types, and merge-sort variants on reference types. 
- Java has two sort methods: [Arrays.parallelSort](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Arrays.html#parallelSort(T%5B%5D)), which, on reference types, is a multithreaded merge sort variant, and [Arrays.sort](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Arrays.html#sort(java.lang.Object%5B%5D)), which is single-threaded and uses Python's [Timsort](https://en.wikipedia.org/wiki/Timsort) combination of natural merge sort and insertion sort. `Arrays.parallelSort` is the preferred sort for large arrays, as it calls `Arrays.sort` for small subarrays. In addition, [Collections.sort](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Collections.html#sort(java.util.List)) sorts a List by creating an array from the List, sorting that array with Timsort, then putting that result back into the List.
- A clever, [non-recursive variant](https://en.wikipedia.org/wiki/Merge_sort#Bottom-up_implementation) of merge-sort is presented

## 7. Quicksort
- The slides imply that newer languages and libraries often add some variation of merge / insertion / Timsort. The reasons seems to be that the latter has greatly improved with techniques like merging runs, and that the latter is easier to parallelize, which is useful with large datasets and multiple cores.
- A median can be estimated by picking 3 items at random and calculating their median
- The partition algorithm from quicksort can be used to find an item of a certain rank (e.g. median). This can be done in a while loop without recursion.
- Java has two sort methods: [Arrays.parallelSort](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Arrays.html#parallelSort(T%5B%5D)) and [Arrays.sort](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Arrays.html#sort(java.lang.Object%5B%5D)).
  - For primitive types, they [appear to be identical](https://github.com/openjdk/jdk/blob/master/src/java.base/share/classes/java/util/Arrays.java) and both use a quicksort variant.
  - For reference types. `Arrays.parallelSort` is a multithreaded merge sort variant, while `Arrays.sort` is single-threaded and uses Python's [Timsort](https://en.wikipedia.org/wiki/Timsort) combination of natural merge sort and insertion sort.
  - `Arrays.parallelSort` is the preferred sort for large arrays, as it calls `Arrays.sort` for small subarrays.
- In addition, [Collections.sort](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Collections.html#sort(java.util.List)) sorts a List by creating an array from the List, sorting that array with Timsort, then putting that result back into the List.
- The slides give the good advice of using the sorts built into the language libraries unless you're absolutely sure that you need a custom solution. This advice is useful for most algorithms built into language libraries, as the authors of those libraries usually have detailed understanding of the internals of the languages, compilers, and interpreters.

### 8. Priority Queues
- Java has two priority queues, the non-thread-safe [PriorityQueue](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/PriorityQueue.html), and the thread-safe [PriorityBlockingQueue](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/concurrent/PriorityBlockingQueue.html). For `PriorityQueue`, "_this implementation provides O(log(n)) time for the enqueuing and dequeuing methods (`offer`, `poll`, `remove()` and `add`); linear time for the `remove(Object)` and `contains(Object)` methods; and constant time for the retrieval methods (`peek`, `element`, and `size`)_"
- Heapsort that uses max-heaps sort from lowest to highest, while heapsorts that use min-heaps sort from highest to lowest
- There's a good chart in the slides that's useful enough to partially replicate here:

| | in-place? | stable? | remarks |
| --- | --- | --- | --- |
| selection | yes | | n exchanges |
| insertion | yes | yes | use for small n or partially sorted |
| merge | | yes | Θ(n log n) guarantee |
| timsort | | yes | improves merge sort when pre-existing order |
| quick | yes | | Θ(n log n) probabilistic guarantee; fastest in practice |
| heap | yes | | Θ(n log n) guarantee |
| ? | yes | yes | holy sorting grail | 

## 9. Elementary Symbol Tables
- The slides include a quote recommending [failing fast](https://en.wikipedia.org/wiki/Fail-fast_system) rather than silently accepting inputs that may cause problems later
- Another way to build a counter is to use the [Map.merge](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Map.html#merge(K,V,java.util.function.BiFunction)) method: `map.merge(key, 0, (count, _) -> count+1)`
- Java has [ordered symbol tables](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/SortedMap.html), primarily using [red-black trees](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree)

## 9. Binary Search Trees
- Tree algorithms are naturally written recursively, but can then be transformed into an iterative version for greater speed and less memory usage. Sometimes you can make the algorithm tail recursive, allowing an easy transition to a while loop. A typical iterative, not recursive, tree algorithm pattern is `Node n = root; while (n != null) { ... }`. If you can't make the algorithm tail-recursive, then you can use an explicit stack to hold the work still to be done

## 10. Balanced Search Trees
- [2-3 trees](https://en.wikipedia.org/wiki/2%E2%80%933_tree) were invented by 🐻[John Hopcroft](https://en.wikipedia.org/wiki/John_Hopcroft)
- The progression from 2-3 trees to [left-leaning red-black trees ](https://en.wikipedia.org/wiki/Left-leaning_red%E2%80%93black_tree) to [red-black trees](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree) in the lecture sludes is very well-done. It's more intuitive than when I learned red-black trees

## 13. Geometric Applications of Binary Search Trees
- I don't know why this is the case, but when I write tree algorithms in particular, I assume they need to be more complicated then they really are. So I write a complicated first draft, and then simplify as I realize what is going on
- The algorithms are described at a high-level, because the algorithms and data structures for computational geometry are too complex for a single lecture. The recommended course [was last taught in 2022](https://www.cs.princeton.edu/courses/archive/fall22/cos451/)
- Looking at the code for the [flocking boids](https://en.wikipedia.org/wiki/Boids), it doesn't appear that the k from the "_move toward the center of mass of k nearest boids_" rule is the same as the k from the "_point away from k nearest boids_" rule

## 14. Hash Tables
- I believe the [Object.hashCode](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Object.html#hashCode()) method returns a representation of the memory location of the object. This limits the `Object.equals` method to "_are these two things referencing the same underlying object?_" (`x == y`), because if two objects are `equals`, then they must have the same `hashCode`. So user-defined classes should override the `hashCode` method so they can have meaningful `equals` methods
- I was confused by the line "_if used only least significant 32 bits \[of Double.doubleToLongBits()\], all integers between −2^21 and 2^21 would have same hash code (0)_". I [read the documentation](https://docs.oracle.com/cd/E19957-01/806-3568/ncg_math.html) and remembered how, unlike the bit representation of an integer (3 is 0011, 15 is 1111) where the bits flow from least-significant to most-significant as the number rises, floating point numbers work differently.<br>To a very, very rough approximation, floating point numbers are repesented as 1.(_fraction_) x 2^(_biased exponent_). So for the integer 3 (1.1000... * 2^1), the fraction is 1000...., while for 15 (1.1110... * 2^3), the fraction is 1110... So as the integers (represented as floating point numbers) rise, the bits flow from the most-significant to least-significant bit. So now I understand the initial line in the slides
- There are three methods that help users quickly build `hashCode` methods for their classes:
  - [Arrays.hashCode](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Arrays.html#hashCode(java.lang.Object%5B%5D)) takes an array of primitive or reference values, hashes the values, then combines them into a `hashCode`
  - [Objects.hash](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Objects.html#hash(java.lang.Object...)) is a [varargs](https://docs.oracle.com/javase/8/docs/technotes/guides/language/varargs.html) version of `Arrays.hashCode` that makes it easy to generate `hashCode` methods for a user defined classes by passing in the fields of the class into the method
  - [Arrays.deepHashCode](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Arrays.html#deepHashCode(java.lang.Object%5B%5D)) is a deep version of the shallow `Arrays.hashCode` for situations where the array to be hashed contains arrays
- A `hashCode` in Java is a signed integer, so take particular care when converting it into an array index
- The great Donald Knuth quote is presented: "_We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil. Yet we should not pass up our opportunities in that critical 3%._" If you look up the quote on the internet, some sources say Donald Knuth, some say Donald Knuth quoting Tony Hoare, and some say Donald Knuth quoting Tony Hoare quoting Donald Knuth 🔁

## 15. Graphs and Digraphs I 
- A _path_ is defined as a "_sequence of vertices connected by edges, with no repeated edges_." This is slightly different from how I originally learned it, which was no repeated vertices (and thus no repeated edges). [Wikipedia](https://en.wikipedia.org/wiki/Path_(graph_theory)#Walk,_trail,_and_path) says both definitions are fine as long as you're clear which you are using
- The Java implementation of graphs in the slides uses a _bag_ for each vertex to record its adjacent vertices. Bags, which allow duplicate entries, are not in the Java libraries. The difference between a bag and a [Set](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Set.html) is that a bag can contain duplicate items. Replacing the bag with [Set](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Set.html)s disallows having multiple edges between the same two vertices, but I don't think this is a common case. In any case, if that was important, you could create a [Map](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/Map.html) for each vertex `a`, that mapped each neighbor vertex `b` to the number of edges between `a` and `b`
- The standard depth-first search algorithm is presented: "_Mark vertex v. Recursively visit all unmarked vertices w adjacent from v_". For marking vertex v, you can use a `visited` `Set`
- The [Wikipedia version](https://en.wikipedia.org/wiki/Depth-first_search#Pseudocode) is the following:
```
procedure DFS(G, v) is
  label v as discovered
  for all directed edges from v to w that are in G.adjacentEdges(v) do
    if vertex w is not labeled as discovered then
      recursively call DFS(G, w)
```
- The Wikipedia iterative version is the following:
```
procedure DFS_iterative(G, v) is
  let S be a stack
  S.push(v)
  while S is not empty do
    v = S.pop()
    if v is not labeled as discovered then
      label v as discovered
      for all edges from v to w in G.adjacentEdges(v) do
        if w is not labeled as discovered then
          S.push(w)
```
- In the above Wikipedia pseudocode, I wouldn't use the term "_discovered_," as the vertices are marked when the algorithm gets to them, not when they are discovered as a neighbor of the current vertex.
- In all versions of depth-first search, vertices must be marked after the algorithm processes them, not when they are first discovered as a neighbor and placed in the stack. The latter is how breadth-first search marks vertices. If, in depth-first search, vertices are marked when they are first discovered, then the algorithm will not process the vertices in the correct, depth-first order.

## 16. Graphs and Digraphs II
- The standard breadth-first search algorithm is presented: "_Add vertex s to FIFO queue and mark s. Repeat until the queue is empty: remove the least recently added vertex v. For each unmarked vertex w adjacent from v: add w to queue and mark_".
- The [Wikipedia version](https://en.wikipedia.org/wiki/Breadth-first_search) is the following:
```
procedure BFS(G, root) is
  let Q be a queue
  label root as explored
  Q.enqueue(root)
  while Q is not empty do
    v := Q.dequeue()
    for all edges from v to w in G.adjacentEdges(v) do
      if w is not labeled as explored then
        label w as explore
        Q.enqueue(w)
```
- In the above Wikipedia pseudocode, I wouldn't use the term "_explored_," as the vertices are marked when they are discovered as a neighbor of the current vertex, not when the algorithm processes them
- In breadth-first search, vertices are marked right away, when they are first discovered as a neighbor and placed in the queue. This makes sure the algorithm doesn't place vertices in the queue multiple times
- The topological sort algorithm works, because if `a` → `b` in a directed **acyclic** graph, the `b` will always come before the `a` in a depth-first search postorder, so the `a` will come before the `b` when the depth-first search postorder is reversed. As Wikipedia puts it, "_each node v is visited_ \[by the postorder\] _only after all its dependencies are visited_". A reverse postorder is not the same as a preorder, where `a` and `b` can appear in any order depending on the rest of the graph
- There's several good tables in the slides, which I combine and partially reproduce here:

| graph | Breadth-first Search | Depth-first Search | Problem |
| --- | --- | --- | --- |
| s-t path | yes | yes | Find a path between s and t | 
| shortest s-t path | yes | | Find a path with the fewest edges between s to t |
| shorted directed cycle | yes | | Find the shorted cycle in a directed graph |
| [Euler cycle](https://en.wikipedia.org/wiki/Eulerian_path) | | yes | Find a cycle that uses each edge exactly once |
| [Hamilton cycle](https://en.wikipedia.org/wiki/Hamiltonian_path) | | | Find a cycle that uses each vertex exactly once |
| [bipartiteness](https://en.wikipedia.org/wiki/Bipartite_graph) (\[no\] odd cycles) | yes | yes | |
| [connected components](https://en.wikipedia.org/wiki/Component_(graph_theory)) | yes | yes | Find connected components |
| [strong components](https://en.wikipedia.org/wiki/Strongly_connected_component) | | yes | every vertex is reachable from every other vertex | 
| [planarity](https://en.wikipedia.org/wiki/Planar_graph) | | yes | Draw in the plane with no crossing edges |
| [graph isomorphism](https://en.wikipedia.org/wiki/Graph_isomorphism) | | | Find an isomorphism between two graphs |
| single-source [reachability](https://en.wikipedia.org/wiki/Reachability) | yes | yes | | 
| [topological sort](https://en.wikipedia.org/wiki/Topological_sorting) | | yes | |

## 17. Minimum Spanning Trees
- A general algorithm is presented to find minimum spanning trees: "_T = ∅. Repeat until T is a spanning tree: Find a cut in G. e ← min-weight crossing edge. T ← T ∪ { e }_"
- The greedy [Kruskal's algorithm](https://en.wikipedia.org/wiki/Kruskal%27s_algorithm) is presented: "_Consider edges in ascending order of weight. Add next edge to T unless doing so would create a cycle_." The edges are sorted by weight, and union-find is used to examine and combine vertex sets. O(E log E) time, O(E) space.
- The  [Wikipedia pseudocode](https://en.wikipedia.org/wiki/Kruskal%27s_algorithm) for Kruskal's algorithm is as follows:
```
algorithm Kruskal(G) is
  F:= ∅
  for each v in G.V do
    MAKE-SET(v)
  for each {u, v} in G.E ordered by weight({u, v}), increasing do
    if FIND-SET(u) ≠ FIND-SET(v) then
      F := F ∪ { {u, v} }
      UNION(FIND-SET(u), FIND-SET(v))
  return F
```
- The greedy [Prim's algorithm](https://en.wikipedia.org/wiki/Prim%27s_algorithm) is presented: "_Start with vertex 0 and grow tree T. Repeat until V − 1 edges: add to T the min-weight edge with exactly one endpoint in T_." A priority queue is used to keep track of edges leading out of tree. O(E log V) time, O(V) space

## 18. Shortest Paths
- A general shortest path algorithm is presented: "_For each vertex v: distTo[v] = ∞. For each vertex v: edgeTo[v] = null. distTo[s] = 0. Repeat until distTo[v] values converge: Relax any edge_"
- The dynamic programming [Bellman-Ford algorithm](https://en.wikipedia.org/wiki/Bellman%E2%80%93Ford_algorithm) is presented: "_For each vertex v: distTo[v] = ∞. For each vertex v: edgeTo[v] = null. distTo[s] = 0. Repeat V-1 times: Relax each edge_". Negative cycles are not allowed. O(E V) time.
- The greedy [Dijkstra's algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm) is presented: "_For each vertex v: distTo[v] = ∞. For each vertex v: edgeTo[v] = null. T = ∅. distTo[s] = 0. Repeat until all vertices are marked: Select unmarked vertex v with the smallest distTo[] value. Mark v. Relax each edge incident from v._" A priority queue is used to track unmarked vertex v with the smallest distTo[] values. Negative weights are not allowed. O(E log V) time, so faster than Bellman-Ford.

## 19. Dynamic Programming
- Make sure you don't over-optimize, and you store enough information in your dynamic programming algorithm to trace back what path you took
- Having a dynamic programming solution doesn't necessarily make it fast, like [change-making](https://en.wikipedia.org/wiki/Change-making_problem) and the [knapsack problem](https://en.wikipedia.org/wiki/Knapsack_problem), which run in [pseudo-polynomial time](https://en.wikipedia.org/wiki/Pseudo-polynomial_time) (polynomial in the numeric value, not the length, of the input)
- Make sure the dependency order is dealth with correctly in your algorithm, and that there are no cycles, so the recurrence will terminate

## 20. Maxflows & Mincuts
- The greedy [Floyd-Fulkerson algorithm](https://en.wikipedia.org/wiki/Ford%E2%80%93Fulkerson_algorithm) is presented: "_Start with 0 flow. While there exists an augmenting path: Find an augmenting path P. Compute bottleneck capacity of P. Update flow on P by bottleneck capacity_." The [Edmonds-Karp algorithm](https://en.wikipedia.org/wiki/Edmonds%E2%80%93Karp_algorithm) uses breadth-first search to find the shortest path to augment.

## 21. Randomness
- The [binomial distribution](https://en.wikipedia.org/wiki/Binomial_distribution) describes the probability of getting a certain number of successes in `n` independent trials where the probability of success is `p`. Its probability mass function is given by `P(X=k) = (n choose k) * p^k * (1-p)^(n-k)`. The expected value is represented by `E(X) = n*p`
- We would like to determine the number of possible cuts in a graph with V vertices. By how [power sets](https://en.wikipedia.org/wiki/Power_set) work, there are `2^V` possible subsets of V vertices. We remove the empty and the full subset, because a cut has to have at least 1 vertex on each side, giving `2^V - 2` possible subsets. Finally, we divide that number in two, because each cut represents two subsets, giving `2^(V-1) - 1` possible cuts
- The randomized [Karger's algorithm](https://en.wikipedia.org/wiki/Karger%27s_algorithm) is presented: "_Assign a random weight (uniform between 0 and 1) to each edge. Run Kruskal’s MST algorithm until 2 connected components left. Return cut defined by connected components_"
- [Naive shuffling](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle#Na%C3%AFve_method) (where each array item can be replaced by any other array item) is biased, as opposed to a [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle).  There are `n^n` possible outcomes of naive shuffling, but `n!` permutations. Since `n!` does not divide `n^n` evenly, the shuffle is biased

## 22. Multiplicative Weights
- It's interesting that a lecture in the second-level computer science course is dedicated to machine learning topics. That would have been unusual when I took a version of the course
<!-- - An elimination algorithm is presented: "_On each day: Take the majority prediction over the experts predictions. After observing the actual outcome: remove all experts that predicted the wrong outcome_."<br>Another elimination algorithm is presented: "On each day: Take the majority prediction over the experts predictions. After observing the actual outcome: remove all experts that predicted the wrong outcome. If all experts got removed, add them all back."<br>A multiplicative weights elimination algorithm is presented: "_Initialize a double[n] array called `weights` and set all values to 1. On each day: Let `zeroWeight` be the sum of weights of experts predicting 0. Let oneWeight be the sum of weights of experts predicting 1. Predict 0 if `zeroWeight` ≥ `oneWeight`, predict 1 otherwise. After observing the actual outcome: halve the weight of all the experts that predicted incorrectly_."<br>A k-ary elimination algorithm is presented: "_On each day: Take the most popular prediction over the experts predictions. After observing the actual outcome: remove/ignore all experts that predicted the wrong outcome_" -->
- A simplified version of the [AdaBoost algorithm](https://en.wikipedia.org/wiki/AdaBoost) is presented: "_Initialize a double\[n\] array called weights and set all values to 1/n. Repeat T times: (Train a decision stump with the input weighted according to weights. Double weight of points incorrectly labelled by the decision stump (force the algorithm to do a better job on misclassified points). Normalize weights (divide each entry by the sum of weights).) To predict on new data use all decision stumps and take majority_"

## 23. Intractability
- The Church-Turing thesis is indirectly referenced. It is defined by [Wikipedia](https://en.wikipedia.org/wiki/Church%E2%80%93Turing_thesis) as "_a function on the natural numbers can be calculated by an effective method if and only if it is computable by a Turing machine_," and by the [Stanford Encyclopedia of Philosophy](https://plato.stanford.edu/entries/church-turing/) as "_every effective computation can be carried out by a Turing machine_"
- Changes or constraints in a problem [can change its computational complexity](https://en.wikipedia.org/wiki/NP-completeness#NP-complete_problems). Also, worst-case complexity may not occur on typical real-world inputs. Finally, intractable problems can have approximation algorithms

![Behnam Esfahbod, CC BY-SA 3.0 <https://creativecommons.org/licenses/by-sa/3.0>, via Wikimedia Commons](https://github.com/user-attachments/assets/cc7fa49a-ec24-45bb-900d-ce12b1a69944)

<a href="https://commons.wikimedia.org/wiki/File:P_np_np-complete_np-hard.svg">Behnam Esfahbod</a>, <a href="https://creativecommons.org/licenses/by-sa/3.0">CC BY-SA 3.0</a>, via Wikimedia Commons

- An interesting thought is presented in the slides that, in real life, creating something is harder than verifying something, so it's not surprising if that's the case in the computational world, with [P](https://en.wikipedia.org/wiki/P_(complexity)) != [NP](https://en.wikipedia.org/wiki/NP_(complexity)) 
- X [reduces](https://en.wikipedia.org/wiki/Reduction_(complexity)) to Y means that if you had an algorithm that solves Y efficiently, then you could use that algorithm to solve X efficiently. Y is harder than X
- An [NP-complete](https://en.wikipedia.org/wiki/NP-completeness) problem is an NP problem where every other NP problem can be reduced to it--it is harder than other NP problems. All NP-complete problems can be be reduced to each other (in the slides: "_NP-complete problems are different manifestations of the same fundamentally hard problem_"), though some reductions are harder than others. To prove an NP problem is NP-complete, reduce an NP-complete problem to it--it is harder than that NP-complete problem. The usefulness of this procedure is that you then know that your problem is (probably, if P != NP) intractable
- If there is at least one item in B for each item in A, then \|A\| <= \|B\|. One of the proofs in the slides uses this, but stated in a more complex way, so I simplify it for my own thoughts here

## 24. Algorithm Design
- Greedy algorithms are described as "_rarely lead to provably optimal solutions but often used anyway in practice, especially for intractable problems_"
- Dynamic programming is described as "_Break up problem into a series of overlapping subproblems. Build up solutions to larger and larger subproblems_"
- Divide and conquer is described as "_Break up problem into two or more independent subproblems. Solve each subproblem recursively. Combine solutions to subproblems to form solution to original problem. Turn brute-force Θ(n²) algorithm into Θ(n log n) one_"
- A randomized algorithm is described as an "_algorithm whose performance (or output) depends on the results of random coin flips_"


