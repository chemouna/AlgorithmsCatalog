
# AlgorithmsCatalog
Inspired by the [website](https://wiki.algo.informatik.tu-darmstadt.de/Main_Page) and [Writing correct code, part 3: preconditions and postconditions]
(https://reprog.wordpress.com/2010/04/30/writing-correct-code-part-3-preconditions-and-postconditions-binary-search-part-4c/) this is an attempt to 
catalog algorithms by the general problems they solve and describe them in a more clear and formal way 
with their invariants, preconditions and postconditions and the example of problems they solve.

I will for each general algorithm try to provide a little bit more formal description, and describe how to identify 
how a problem is solved by it.

Note: This is still very much in progress and not polished at all yet.

## Pointer algorithms

### Runner technique

### Dropping anchors

### Alternate walking and skipping technique

### In Place reverse

## Element distinctness problem
* [Wikipedia: Element distinctness problem](https://en.wikipedia.org/wiki/Element_distinctness_problem)

## Finding repeated Elements 
* [Paper on Finding Repeated Elements by David Gries and J. Misra](http://www.cs.utexas.edu/users/misra/scannedPdf.dir/FindRepeatedElements.pdf)

## Search Algorithms

### Binary Search
#### Pseudo code 
Given an array A of n elements with values or records A0 ... An−1, sorted such that A0 ≤ ... ≤ An−1, 
and target value T, find the index of T in A.

1/ Set L to 0 and R to n − 1.
2/ If L > R, the search terminates as unsuccessful.
3/ Set m (the position of the middle element) to the floor (the largest previous integer) of (L + R) / 2.
4/ If Am < T, set L to m + 1 and go to step 2.
5/ If Am > T, set R to m – 1 and go to step 2.
6/ Now Am = T, the search is done; return m.

#### Common errors 

#### Variation of binary search

##### Fractional cascading

##### Exponential search

#### Additional resources
- Column 4 of the book Programming Pearls

## Sorting Algorithms 

- [When is each sorting algorithm used ?](http://stackoverflow.com/questions/1933759/when-is-each-sorting-algorithm-used)

### Insertion Sort 
- Complexity : O(n^2)

```C
void isort(int *A, int n) {
  for (int i = 1; i < n; i++) {
    // insert A[i] into A[0..i-1]
    int temp = A[i];
    int j = i-1;

    // shift all A[] > temp
    while (j >= 0 && A[j] > temp) {
      A[j+1] = A[j];
      j--;
    }
    A[j+1] = temp;
  }
}
```
- Loop invariant:
  At the beginning of each loop, A[0..i-1] is a sorted permutation of the first i elements of A[], and at the end of each 
  loop A[0..i] is a sorted permutation of the first i+1 elements of A[].


### Selection Sort 
- an in-place comparison sort. It has O(n2) time complexity, making it inefficient on large lists, and generally performs worse than the similar insertion sort. 

```
void sort(int [] a, int n) {
  for (int i=0; i<n-1; i++) {
    int best = i;
    for (int j=i; j<n; j++) {
      if (a[j] < a[best]) {
        best = j;
      }
    }
    swap a[i] and a[best];
  }
}
```
-  Outer loop invariant: 
      * a[0...i-1] is sorted
      * All entries in a[i..n-1] are larger than or equal to the entries in a[0..i-1] 
- Inner loop invariant: All entries in a[i..j-1] are greater than or equal to a[best]. 

### HeapSort 
- A heap is a structure designed to solve a common problem. You’ve got a collection of objects, 
  each of which has an associated numeric value. You want, at any time, to be able to find and remove 
  the largest value in the collection, and to be able to add new elements to it. Those two operations are 
  the core of the heap. Some variations also allow you to increase the value of objects inside the heap, 
  or to remove values other than the maximum. 
- Data structures used idealy should contain just the information we need no more and no less 
- Heap sort is efficient because the Insert and Delete-Max operations on a heap both run in O(log n) time, 
  meaning that n inserts and deletions can be done on the heap in O(n log n) time. A more precise analysis 
  can be used to show that, in fact, it takes Θ(n log n) time regardless of the input array 

- Heaps are commonly implemented with an array. Any binary tree can be stored in an array, but because a 
  binary heap is always a complete binary tree, it can be stored compactly. No space is required for pointers; 
  instead, the parent and children of each node can be found by arithmetic on array indices. These properties 
  make this heap implementation a simple example of an implicit data structure or Ahnentafel list. 

- Array Based implementation:

//TODO

- Pointer based implementation

//TODO 

- [Haskell Implementation](TODO)
- [Java Implementation]()

### SmoothSort 

### Poplar Sxsort 

### IntroSort 


### Counting Sort 

- Counting sort is an algorithm for sorting a collection of objects according to keys that are small integers (an integer sorting algorithm). 
  It operates by counting the number of objects that have each distinct key value, and using arithmetic on those counts to determine the positions 
  of each key value in the output sequence. Its running time is linear in the number of items and the difference between the maximum and minimum 
  key values, so it is only suitable for direct use in situations where the variation in keys is not significantly greater than the number of items. 

- Counting Sort complexity is O(n + k)

- For problem instances in which the maximum key value is significantly smaller than the number of items, counting sort can be highly space-efficient, 
  as the only storage it uses other than its input and output arrays is the Count array which uses space O(k)

- It is not enough to know the upper bound to run a counting sort: you need to have enough memory to fit all the counters.
Consider a situation when you go through an array of 64-bit integers, and find out that the largest element is 2^60. 
This would mean two things:
   - You need an O(2^60) memory, and
   - It is going to take O(2^60) to complete the sort.
The fact that O(2^60) is the same as O(1) is of little help here, because the constant factor is too large. 
This is very often a problem with pseudo-polynomial time algorithms.

- In the case where the inputs are arrays with maximum - minimum = O(n log n) (i.e. the range of values is reasonably restricted), 
  using counting sort may makes sense. If this is not the case, a standard comparison-based sort algorithm or even an integer sorting 
  algorithm like radix sort is asymptotically better.

- [Haskell implementation](TODO)
- [Java Implementation](TODO)

### Distribution Sort 

#### Bucket Sort 
- idea of the bucket sort is to place items into various buckets based on a key or partial information about a key. 

- BucketSort Steps :
    - Set up an array of initially empty "buckets".
    - Scatter: Go over the original array, putting each object in its bucket.
    - Sort each non-empty bucket.
    - Gather: Visit the buckets in order and put all elements back into the original array. 

- for bucket sort to be {\displaystyle O(n)} O(n) on average, the number of buckets n must be equal to the length of the array being sorted, 
  and the input array must be uniformly distributed across the range of possible bucket values.[1] If these requirements are not met, the 
  performance of bucket sort will be dominated by the running time of nextSort, which is typically {\displaystyle O(n^{2})} O(n^{2}) insertion sort.
  
- Bucket sort’s best case occurs when the data being sorted can be distributed between the buckets perfectly. 
   An example is [2303, 33, 1044], if buckets can only contain 5 different values then for this example 461 buckets would 
   need to be initialised. A bucket size of 200-1000 would be much more reasonable. 
  The inverse is also true; a densely allocated array like [103, 99, 119, 112, 111] performs best when buckets are as small as possible.

- Bucket sort performs at its worst, O(n^2)​​ when all elements at allocated to the same bucket.

#### Radix Sort 
- Radix sort is a O(n) sorting algorithm working on integer keys. 

- struct to be sorted has to be able to provide something that acts somewhat like an integer. Radix sort can be extended to floats,
  pairs, tuples and std::array. So if your struct can provide for example a std::pair<bool, float> and use that as a sort key, 
  you can sort it using radix sort. 

- Radix sort builds on top of two principles:
    1. counting sort is a stable sort. If two entries have the same number, they will stay in the same order.
    2. If you sort a numbers by their lowest digit first, and then do a stable sort on higher digits, the result will be a sorted list. 

- The in-place version of radix sort has a nice benefit: It starts sorting at the most significant digit. The LCD version  made radix
  sort slow for large keys because it always had to look at every byte of the key. The in-place version could early out after looking 
  at the first byte, which would potentially make it much faster for large keys.

* Preconditions: The input is a list of N values. Each value is an integer with d digits.
  Each digit is a value from 0 to k − 1, i.e., the value is viewed as an integer base k.
* Postconditions: The output is a list consisting of the same N values in nondecreasing order.

* The Algorithm: Loop through the digits from low to high order. For each, use a stable sort to sort the elements according to the current 
  digit, ignoring the other digits.

* Loop Invariant: After sorting with respect to  the first i low-order digits, the elements are sorted with respect to the value formed from these i digits. 
  (Stable sorting allows us to maintain this invariant)

#### Flash Sort

- [Haskell implementation](TODO)
- [Java Implementation](TODO)

### QuickSort
- One of the major factors is that quicksort has better locality of reference -- the next thing to be accessed is 
  usually close in memory to the thing you just looked at. By contrast, heapsort jumps around significantly more. 
  the element of the Since things that are close together will likely be cached together, quicksort tends to be faster.

### MergeSort

- If a dataset is really huge and doesn't fit into memory, then merge sort works better. 
  It's frequently used in clusters where dataset can span over hundreds of machines.

### American Flag sort 
- works similar to counting sort in that you need an array to count how often each element appears. So if we sort bytes, 
  we also need a count array of 256 elements. Then we also compute the prefix sum of this count array, like we did in 
  counting sort. Only the final loop is different Since American Flag Sort is in-place, the value in a new output array 
  we need to swap instead in place


### External Sorting 

### In-Place RadixSort 

### Near Sorting Algorithms

## Selection Algorithms

### Median Finding algorithms

## Insertion Algorithms 

## Scanning Algorithms 

## In-Place Algorithms
### In-Place Merging 

## Hashing 

* A simple hash function works by taking the "component parts" of the input (characters in the case of a string), and multiplying them by the 
  powers of some constant, and adding them together in some integer type. So for example a typical (although not especially good) hash of a string might be:
  ```
  (first char) + k * (second char) + k^2 * (third char) + ... 
  ```
* It turns out that "because of the nature of maths", if the constant used in the hash, and the number of buckets, are coprime, then collisions are minimised in 
  some common cases. If they are not coprime, then there are some fairly simple relationships between inputs for which collisions are not minimised. All the hashes 
  come out equal modulo the common factor, which means they'll all fall into the 1/n th of the buckets which have that value modulo the common factor. You get n 
  times as many collisions, where n is the common factor, hashtable implementations obviously have no control over the items put into them. They can't prevent them 
  being related. So the thing to do is to ensure that the constant and the bucket counts are coprime.  
  a paranoid hashtable can't assume a good hash function, so should use a prime number of buckets. Similarly a paranoid hash function should use a largeish prime 
  constant, to reduce the chance that someone uses a number of buckets which happens to have a common factor with the constant. 
  
  So putting the principle that "everything has to be prime" is a sufficient but not a necessary condition for good distribution over hashtables. It allows everybody to 
  interoperate without needing to assume that the others have followed the same rule. 
  

### Modular Hashing 

### Horner's method 

### Rolling Hashes 

### Carter-Wegman class of hash functions

### Double hash technique 

## String Matching Algorithms

### Knuth–Morris–Pratt algorithm

* The basic idea behind the algorithm discovered by Knuth, Morris, and Pratt is this: whenever we detect a mismatch, we
already know some of the characters in the text (since they matched the pattern characters prior to the mismatch). We can 
take advantage of this information to avoid backing up the text pointer over all those known characters. 

* Complexity : Since the two portions of the algorithm (search and table building) have of O(k) and O(n), the complexity of the overall algorithm is O(n + k).

* Algorithm Pseudo 
```
 algorithm kmp_search:
    input:
        an array of characters, S (the text to be searched)
        an array of characters, W (the word sought)
    output:
        an integer (the zero-based position in S at which W is found)

    define variables:
        an integer, m ← 0 (the beginning of the current match in S)
        an integer, i ← 0 (the position of the current character in W)
        an array of integers, T (the table, computed elsewhere)

    while m + i < length(S) do
        if W[i] = S[m + i] then
            if i = length(W) - 1 then
                return m
            let i ← i + 1
        else
            if T[i] > -1 then
                let m ← m + i - T[i], i ← T[i]
            else
                let m ← m + 1, i ← 0
            
    (if we reach here, we have searched all of S unsuccessfully)
    return the length of S
```

* The partial match table: The numbers in the partial Match Table tell you how many positions are already matched when an error occurs. 
We can use the values in the partial match table to skip ahead (rather than redoing unnecessary old comparisons) when we find partial matches. The formula works like this:
If a partial match of length partial_match_length is found and table[partial_match_length] > 1, we may skip ahead partial_match_length - table[partial_match_length - 1] characters.
- a value T[i] in T is the amount of "backtracking" we need to do after a mismatch

### Boyer-Moore Algorithm

* well-suited for applications in which the pattern is much shorter than the text or where it persists across multiple searches 
   matches on the tail of the pattern rather than the head, and to skip along the text in jumps of multiple characters rather than 
   searching every single character in the text. 

* compares the symbols of the pattern from right to left with the text. After a complete match the pattern is shifted according to 
  how much its widest border allows. After a mismatch the pattern is shifted by the maximum of the values given by the good-suffix 
  and the bad-character heuristics.
 
* The Boyer-Moore algorithm uses two different heuristics for determining the maximum possible shift distance in case of a mismatch: 
  the "bad character" and the "good suffix" heuristics. Both heuristics can lead to a shift distance of m. For the bad character heuristics 
  this is the case, if the first comparison causes a mismatch and the corresponding text symbol does not occur in the pattern at all. 
  For the good suffix heuristics this is the case, if only the first comparison was a match, but that symbol does not occur elsewhere in the pattern.

### Boyer–Moore–Horspool or Horspool algorithm

- instead of the "bad character" that caused the mismatch, in each case the rightmost character of the current text window is used 
  for determining the shift distance.
- preprocesses the pattern to produce a table containing, for each symbol in the alphabet, the number of characters that can safely be skipped. 

```
function preprocess(pattern)
    T ← new table of 256 integers
    for i from 0 to 256 exclusive
        T[i] ← length(pattern)
    for i from 0 to length(pattern) - 1 exclusive
        T[pattern[i]] ← length(pattern) - 1 - i
    return T
```
```
 function search(needle, haystack)
    T ← preprocess(needle)
    skip ← 0
    while length(haystack) - skip ≥ length(needle)
        i ← length(needle) - 1
        while haystack[skip + i] = needle[i]
            if i = 0
                return skip
            i ← i - 1
        skip ← skip + T[haystack[skip + length(needle) - 1]]
    return not-found
```
### Rabin-Karp algorithm 

* Rabin–Karp algorithm is a randomized algorithm for the string search problem that finds all probable matches 
for the needle in the haystack in linear time.

* The runtime of the Rabin-Karp algorithm is, in the worst case, O(|P||T|). This happens if by sheer dumb luck we end up having a hash collision on
 every length-|P| substring of T.  In the average case, though, it can be shown that the number of hash collisions is expected O(1), in which case the
 runtime of the algorithm is O(|P| + |T|), asymptotically much faster than the naive implementation.
 
* Compute a hash function for the pattern and then look for a match by using the same hash function for each possible M-character 
  substring of the text. If we find a text substring with the same hash value as the pattern, we can check for a match. 
  Rabin and Karp showed that it is easy to compute hash functions for M-character substrings in constant time (after some preprocessing),
  which leads to a linear-time substring search in practical situations 

* Using Monte Carlo:
always returns true if the hash code matche

* Using Las Vegas Algorithm: 
check if the string matches character by character once their hashes are equal.

* Rabin–Karp algorithm is inferior for single pattern searching to Knuth–Morris–Pratt algorithm, Boyer–Moore string search algorithm and 
  other faster single pattern string searching algorithms because of its slow worst case behavior. However, it is an algorithm of choice 
  for multiple pattern search. 

* Due to the Birthday paradox, if you want to expect zero collisions, the size of your prime for Rabin-Karp should be about n^2 or more, 
  where n is the length of the "haystack" string.


#### Rabin fingerprint
treats every substring as a number in some base, the base being usually a large prime. For example, if the substring is "hi" 
and the base is 101, the hash value would be 104 × 101^1 + 105 × 101^0 = 10609 (ASCII of 'h' is 104 and of 'i' is 105). 



### Aho–Corasick algorithm
 

## Algorithms on arrays

### Sliding Window Algorithm

#### minimum on a sliding window algorithm 

## Graph Algorithms

### Minimum Spanning Trees
* a spanning tree of a graph is a connected subgraph with no cycles that includes all the vertices. 
A minimum spanning tree (MST ) of an edge-weighted graph is a spanning tree whose weight (the sum of the weights 
of its edges) is no larger than the weight of any other spanning tree. 

#### Prim’s algorithm 

#### Kruskal’s algorithm 
* finds an edge of the least possible weight that connects any two trees in the forest. It is a greedy algorithm in graph
theory as it finds a minimum spanning tree for a connected weighted graph adding increasing cost arcs at each step. 
It finds a subset of the edges that forms a tree that includes every vertex, where the total weight of all the edges in 
the tree is minimized. If the graph is not connected, then it finds a minimum spanning forest (a minimum spanning tree for 
each connected component).
  
```
KRUSKAL(G):
  A = ∅
  foreach v ∈ G.V:
     MAKE-SET(v)
  foreach (u, v) in G.E ordered by weight(u, v), increasing:
     if FIND-SET(u) ≠ FIND-SET(v):
        A = A ∪ {(u, v)}
        UNION(u, v)
 return A   
```

#### Minimum spanning forest 
If a graph is not connected, we can adapt our algorithms to compute the MSTs of each of its connected components known
as a minimum spanning forest.

* Example problems solved by MST:
//TODO
//TODO problems from topcoder

### Single-Source Shortest Paths Algotithms

#### Djikstra's Algorithm

* This algorithm makes no attempt to direct "exploration" towards the destination as one might expect. Rather, the sole consideration in determining the next 
 "current" intersection is its distance from the starting point. This algorithm therefore expands outward from the starting point, interactively considering 
 every node that is closer in terms of shortest path distance until it reaches the destination. When understood in this way, it is clear how the algorithm 
 necessarily finds the shortest path. However, it may also reveal one of the algorithm's weaknesses: its relative slowness in some topologies. 

* asymptotically the fastest known single-source shortest-path algorithm for arbitrary directed graphs with unbounded non-negative weights.

```
function Dijkstra(Graph, source):
     create vertex set Q
 
     for each vertex v in Graph:             // Initialization
          dist[v] ← INFINITY                  // Unknown distance from source to v
          prev[v] ← UNDEFINED                 // Previous node in optimal path from source
          add v to Q                          // All nodes initially in Q (unvisited nodes)
 
          dist[source] ← 0                        // Distance from source to source
      
         while Q is not empty:
           u ← vertex in Q with min dist[u]    // Node with the least distance will be selected first
           remove u from Q 
         
           for each neighbor v of u:           // where v is still in Q.
              alt ← dist[u] + length(u, v)
              if alt < dist[v]:               // A shorter path to v has been found
                  dist[v] ← alt 
                  prev[v] ← u 

      return dist[], prev[]
```

another nice to express Djikstra's algorithm :
```
Dijkstra(G, w, s)  {
   Initialize-Single-Source(G, s)
   S ← Ø
   Q ← V[G]//priority queue by d[v]
   while Q ≠ Ø do
      u ← Extract-Min(Q)
      S ← S U {u}
      for each vertex v in Adj[u] do
         Relax(u, v)
}

Initialize-Single-Source(G, s) {
   for each vertex v  V(G)
      d[v] ← ∞
      π[v] ← NIL
   d[s] ← 0
}

Relax(u, v) {
   //update only if we found a strictly shortest path
   if d[v] > d[u] + w(u,v) 
      d[v] ← d[u] + w(u,v)
      π[v] ← u
      Update(Q, v)
}
```

* In common presentations of Dijkstra's algorithm, initially all nodes are entered into the priority queue. This is, however, not necessary:
  the algorithm can start with a priority queue that contains only one item, and insert new items as they are discovered (instead of doing a decrease-key, 
  check whether the key is in the queue; if it is, decrease its key, otherwise insert it).[3]:198 This variant has the same worst-case bounds as the common 
  variant, but maintains a smaller priority queue in practice, speeding up the queue operations.[4]

  Moreover, not inserting all nodes in a graph makes it possible to extend the algorithm to find the shortest path from a single source to the closest of a 
  set of target nodes on infinite graphs or those too large to represent in memory. The resulting algorithm is called uniform-cost search (UCS) in the artificial intelligence literature 

* Breadth-first search can be viewed as a special-case of Dijkstra's algorithm on unweighted graphs, where the priority queue degenerates into a FIFO queue.

* Shortest-paths algorithms typically rely on the property that a shortest path between two vertices contains other shortest paths within it. 
  
* A shortest path cannot contain a cycle neither negative or positive weight cycle 

* Dijkstra’s algorithm is like Prim’s algorithm in that both algorithms use a minpriority queue to find the “lightest” vertex outside a given set 
  (the set S in Dijkstra’s algorithm and the tree being grown in Prim’s algorithm).

* to examine an edge to see if it offers a better path to a node is referred to as relaxing the edge (because in general mathematically, relaxation 
is making a change that reduces constraints. When the Dijkstra algorithm examines an edge, it removes an edge from the pool, thereby reducing the number of constraints)

* Problems solved with Djikstra
- From Top Coder :
     [RoboCourier](https://community.topcoder.com/stat?c=problem_statement&pm=1749&rd=4555)
     [IslandFerries](https://community.topcoder.com/stat?c=problem_statement&pm=2437&rd=5069)
     [DungeonEscape](https://community.topcoder.com/stat?c=problem_statement&pm=2449&rd=5073)
     [BombMan](https://community.topcoder.com/stat?c=problem_statement&pm=2274&rd=5009)
     [KiloManX](https://community.topcoder.com/stat?c=problem_statement&pm=2288&rd=4725)
     
##### Fast marching method

##### Variants of Djikstra's Algorithm

###### Dial's Algorithm 

* Using Bucket queues 

* Using Van Emde Boas tree 

* Using a radix heap 
 
##### A* search algorithm

#### Bellman–Ford algorithm 


#### Flood fill

#### Floyd–Warshall algorithm 
* calculates the shortest routes between all pairs of nodes in a single run! Cycle weights must be non-negative, and the graph must be directed 

```
let dist be a |V| × |V| array of minimum distances initialized to ∞ 
 for each vertex v
     dist[v][v] ← 0
  for each edge (u,v)
     dist[u][v] ← w(u,v)  // the weight of the edge (u,v)
  for k from 1 to |V|
    for i from 1 to |V|
       for j from 1 to |V|
          if dist[i][j] > dist[i][k] + dist[k][j] 
             dist[i][j] ← dist[i][k] + dist[k][j]
         end if
```

* Running Dijkstra for all nodes gives you O(VE + V^2log V), while Floyd's is O(V^3). If E = O(V^2), 
 then the two are theoretically identical, with Floyd being faster in practice. If you E = O(V), then 
 running Dijkstra for all nodes if better both in theory and in practice.
 Basically, run Dijkstra from all nodes if you expect to have about as many edges as you have nodes, and run 
 Floyd if you expect to have almost complete graphs. 

#### Johnson's algorithm
A way to find the shortest paths between all pairs of vertices in a sparse, edge weighted, directed graph. It allows some of the edge 
weights to be negative numbers, but no negative-weight cycles may exist.
  
* Johnson's algorithm is a way to find the shortest paths between all pairs of vertices in a sparse, edge weighted, directed graph.

* Johnson's algorithm is a slight modification to running Dijkstra's algorithm from each node that allows that approach to work even if the graph contains negative edges (as long as there aren't any negative cycles). The algorithm works by first running Bellman-Ford on the graph to transform it to a graph with no negative edges, then using Dijkstra's algorithm starting at each vertex. Because Bellman-Ford runs in time O(mn), the overall asymptotic runtime is still O(mn + n2 log n), so if m = o(n2) (note that this is little-o of n), this approach is asymptotically faster than using Floyd-Warshall.

The one catch here is that this assumes that you have Dijkstra's algorithm backed by a Fibonacci heap. If you don't have Fibonacci heap available and aren't willing to put in the 72 hours necessary to build, debug, and test one, then you can still use a binary heap for Dijkstra's algorithm; it just increases the runtime to O(m log n), so this version of Johnson's algorithm runs in O(mn log n). This is no longer always asymptotically faster than Floyd-Warshall, because if m = Ω(n2) then Floyd-Warshall runs in O(n3) whileJohnson's algorithm runs in O(n3 log n) 
  - With a Fibonacci heap, Johnson's algorithm is always asymptotically at least as good as Floyd-Warshall, though it's harder to code up.
  - With a binary heap, Johnson's algorithm is usually asymptotically at least as good as Floyd-Warshall, but is not a good option when dealing with large, dense graphs. 


#### Gabow's Shortest Paths Algorithm

## Overlapping subproblems

## Pearls

## Tree and Graph Traversal

### BFS 

* Pseudo code :
```
Breadth-First-Search(Graph, root):
    create empty set S
    create empty queue Q

    root.parent = NIL
    add root to S
    Q.enqueue(root)

    while Q is not empty:
        current = Q.dequeue()
        if current is the goal:
            return current
        for each node n that is adjacent to current:
            if n is not in S:
                add n to S
                n.parent = current
                Q.enqueue(n)
```
* Example problems solved with BFS 
   - [SmartWordToy Problem](https://community.topcoder.com/stat?c=problem_statement&pm=3935&rd=6532)
   
### DFS 

* If you know a solution is not far from the root of the tree, a breadth first search (BFS) might be better. 
  If the tree is very deep and solutions are rare, depth first search (DFS) might take an extremely long time, 
  but BFS could be faster. If the tree is very wide, a BFS might need too much memory, so it might be completely impractical. 
  If solutions are frequent but located deep in the tree, BFS could be impractical. If the search tree is very deep you will 
  need to restrict the search depth for depth first search (DFS)

* DFS is typically used to traverse an entire graph, and takes time Θ(|V| + |E|),[4] linear in the size of the graph. 
  it uses space O(|V|) in the worst case to store the stack of vertices on the current search path as well as the set 
  of already-visited vertices.

* BFS goes level by level, but requires more space. The space required by DFS is O(d) where d is depth of tree, but space required 
  by BFS is O(n) where n is number of nodes in tree (Why? Note that the last level of tree can have around n/2 nodes and second last 
  level n/4 nodes and in BFS we need to have every level one by one in queue).

Recursive DFS:
```
procedure DFS(G,v):
      label v as discovered
      for all edges from v to w in G.adjacentEdges(v) do
          if vertex w is not labeled as discovered then
              recursively call DFS(G,w)
```

Non recursive DFS:
```
procedure DFS-iterative(G,v):
     let S be a stack
     S.push(v)
     while S is not empty
         v = S.pop()
         if v is not labeled as discovered:
             label v as discovered
             for all edges from v to w in G.adjacentEdges(v) do 
                 S.push(w)
```
* An important property of a depth-first search is that it partitions the edges of an undirected graph into exactly two classes: tree edges and back edges. 
The tree edges discover new vertices, and are those encoded in the parent relation. Back edges are those whose other endpoint is an ancestor of the vertex 
being expanded, so they point back into the tree. An amazing property of depth-first search is that all edges fall into these two classes. 

* DFS with processing methods to use for solving problems
```C
dfs(graph *g, int v) {
  edgenode *p; /* temporary pointer */
  int y; /* successor vertex */
  if (finished) return; /* allow for search termination */
  discovered[v] = TRUE;
  time = time + 1;
  entry_time[v] = time;

  process_vertex_early(v);
  
  p = g->edges[v];
  while (p != NULL) {
    y = p->y;
    if (discovered[y] == FALSE) {
      parent[y] = v;
      process_edge(v,y);
      dfs(g,y);
    }
    else if ((!processed[y]) || (g->directed))
      process_edge(v,y);
```
Finding cycle can be done with the above algorithm by just adding an implementation for process_edge :
```
process_edge(int x, int y) {
  if (parent[x] != y) { /* found back edge! */
     printf("Cycle from %d to %d:",y,x);
     find_path(y,x,parent);
     printf("\n\n");
     finished = TRUE;
 }
}
```

### Iterative deepening 
* a depth-limited version of depth-first search is run repeatedly with increasing depth limits until the goal is found. IDDFS is equivalent 
  to breadth-first search, but uses much less memory.

* The time complexity of IDDFS works out to be the same as depth-first search, i.e.  O(b^d) where b is the branching factor and d is the 
  depth of the goal, and space complexity of IDDFS is O(d) where d is the depth of the goal.

### Strongly Connected Components 
STRONGLY-CONNECTED-COMPONENTS.
   1. call DFS.G/ to compute finishing times u.f for each vertex u
   2. compute transpose of G
   3. call DFS. on transpose of G, but in the main loop of DFS, consider the vertices in order of decreasing u.f (as computed in line 1)
   4. output the vertices of each tree in the depth-first forest formed in line 3 as a separate strongly connected component
this linear-time (i.e., O(V+E)-time) algorithm computes the strongly connected components of a directed graph G=(V,E) using two depth-first
searches, one on G and one on transpose of G.

### Topological Sorting 


### Degeneracy of a graph

#### K-Cores graph algorithm 

### Topological Sorting

#### Kahn's algorithm 
```
L ← Empty list that will contain the sorted elements
S ← Set of all nodes with no incoming edges
while S is non-empty do
    remove a node n from S
    add n to tail of L
    for each node m with an edge e from n to m do
        remove edge e from the graph
        if m has no other incoming edges then
            insert m into S
if graph has edges then
    return error (graph has at least one cycle)
else 
    return L (a topologically sorted order)
```

### Coffman–Graham algorithm
 
## Dynamic programming 

### Longest increasing subsequence

### Longest common subsequence problem


```
function LCSLength(X[1..m], Y[1..n])
    C = array(0..m, 0..n)
    for i := 0..m
       C[i,0] = 0
    for j := 0..n
       C[0,j] = 0
    for i := 1..m
        for j := 1..n
            if X[i] = Y[j]
                C[i,j] := C[i-1,j-1] + 1
            else
                C[i,j] := max(C[i,j-1], C[i-1,j])
    return C[m,n]
```

## Computational Geometry Algorithms 

### Closest pair of points problem
- [Definition in wikipedia](https://en.wikipedia.org/wiki/Closest_pair_of_points_problem)

## Randomized Algorithms

## Backtracking 
- Backtracking is a general algorithm for finding all (or some) solutions to some computational problems that incrementally
  builds candidates to the solutions, and abandons each partial candidate c ("backtracks") as soon as it determines that c 
  cannot possibly be completed to a valid solution.

## Data Structures 

### Linear Data Structures 

#### Array

#### Stack

#### Bit Array

### Circular Buffer 

### Heap

#### Binary Heap 
- A binary heap is a heap data structure that takes the form of a complete binary tree. 
Binary heaps are a common way of implementing priority queues. 

#### B-Heap 

#### Binomial Heap 
* a heap similar to a binary heap but also supports quick merging of two heaps. This is achieved by using a special tree structure. 
It is important as an implementation of the mergeable heap abstract data type (also called meldable heap), which is a priority queue supporting merge operation.

The name comes from the shape: a binomial tree of order {\displaystyle n} n has {\displaystyle {\tbinom {n}{d}}} \tbinom n d nodes at depth {\displaystyle d} d. 
 (Binomial coefficient)
 
*  binomial heap is implemented as a set of binomial trees that satisfy the binomial heap properties:
   - Each binomial tree in a heap obeys the minimum-heap property: the key of a node is greater than or equal to the key of its parent.
   - There can only be either one or zero binomial trees for each order, including zero order.

* Merge Operation : the simplest and most important operation is the merging of two binomial trees of the same order within a binomial heap. 
  Due to the structure of binomial trees, they can be merged trivially. As their root node is the smallest element within the tree, by comparing 
  the two keys, the smaller of them is the minimum key, and becomes the new root node. Then the other tree becomes a subtree of the combined tree. 


#### Min-max-median Heap

#### D-ary Heap

#### Fibonacci Heap 
* Fibonacci heaps have asymptotically good runtime guarantees for many operations. In particular, insert, peek, and decrease-key all
run in amortized O(1) time. dequeueMin and delete each run in amortized O(lg n) time. This allows algorithms that rely heavily on decrease-key
to gain significant performance boosts.  For example, Dijkstra's algorithm for single-source shortest paths can be shown to run in O(m + n lg n) 
using a Fibonacci heap, compared to O(m lg n) using a standard binary or binomial heap.
 
* Fibonacci heaps are asymptotically great in an amortized sense, they have huge constant factors in practice.

* find-minimum operation takes constant (O(1)) amortized time.[1] The insert and decrease key operations also work in constant amortized time.
  Deleting an element (most often used in the special case of deleting the minimum element) works in O(log n) amortized time, where n is the size of the heap.
  
  So starting from an empty data structure, any sequence of a insert and decrease key operations and b delete operations would take O(a + b log n) worst case time,
  where n is the maximum heap size. In a binary or binomial heap such a sequence of operations would take O((a + b) log n) time. A Fibonacci heap is thus better 
  than a binary or binomial heap when b is smaller than a by a non-constant factor.
  
* The primary difference between the Fibonacci heap and the binomial heap is that it defers all ‘clean up’ jobs to a point where they are more convenient,
   guarenteeing Θ(1) for several operations. Due to the deferred clean up, the worst case time complexity of the delete and extract minimum operations is 
   O(n), however they are O(logn) amortised. 

* each of the trees of the fibonacci heap has to have at least Fn+2 nodes in them, where Fn + 2 is the (n + 2)nd Fibonacci number.
  So why is it called a Fibonacci heap ? Because each tree of order n has to have at least Fn+2 nodes in it.
  

#### Pairing Heap 

#### Brodal Heap 

#### Rank-Pairing Heap 

### Treap 

### Disjoint-set data structure

#### Disjoint-set forests 

#### Path compression 

#### Invariants 
head == tail  iff buffer is empty (this invariant is only valid in the method of implementation where the wrap-around goes back to 0).
If buffer is not empty, head points at next valid element to be consumed.
tail always points at the next empty element.
    => There is always one unused element in a full buffer.
     => length must be greater than 1
            
#### Implementation 

- One less common but better implementation:
circular buffer implementation needs only head and tail indices. `size'
above appears to be redundant.

Implementation-wise, the head and tail indices should *not* be constrained
to be less than the size of the buffer. They should be allowed to wrap all
the way back to zero. This allows you to distinguish between the
completely-empty and completely-full states while using 100% of the storage.

### Trie
- an ordered tree data structure that is used to store a dynamic set or associative array where the keys are usually strings.

- Lexicographic sorting of a set of keys can be done with a simple trie-based:
  - Insert all keys in a trie.
  - Output all keys in the trie using a pre-order traversal, which results in output that is in lexicographically increasing order.

- Trie allows fast searching for key in huge volume of texts. It is also useful for finding predecessor and successors as well as lexicographically sorting strings.

Exercices: 
- [Trie application I: Tagalog alphabet sorting](http://sukwonoh.blogspot.fr/2012/09/trie-application-i-topcoder-srm-342.html)

#### Bitwise Trie 

#### DAFSA 
(Deterministic Acyclic Finite State Automaton)

#### Discrimination Tree 

#### BurstSort 

### Suffix Tree
- built on top of a trie where, instead of just adding the string itself into the trie, you would also add every possible suffix of that string. As an example, if you wanted to index the string banana in a suffix tree, you would build a trie with the following strings:
```java
banana
anana
nana
ana
na
a
```
Once that's done search for any n-gram and see if it is present in the indexed string, the n-gram search is a prefix search of all possible suffixes of the string.


### Ternary Search Tree 

### B-Trie

### Hash Trie

### HAT-Trie

### Burst Trie 

### Hash array mapped trie


### Trees

#### B-Trees 

#### Multiway Trees 

#### Space-partitioning trees

#### Application-specific trees 

### Hashes

### Graphs 

### Succint Data Structures

### Data structures for Integer sorting

#### Van Emde Boas Tree

#### Y-fast Trie

#### Bucket Queue

### Others 

## Algorithms that work by building an automata
* Aho-Corasick algorithm uses a DFA in order to search for all the elements of a dictionary in a text in linear time, O(|w|) where w is our text. 
* Levenshtein DFA : we can check if a set of words has a specific maximum limit of the Levenshtein distance from a given word. For this we need to construct the Levenshtein Automaton for a constant k which accepts all strings within k 


### Blogs with problems solved with algorithms
* [Alan's Blog Algorithms Decomplexified](http://decomplexify.blogspot.fr/2014/04/wildcard-match-star-and-qmark-asymmetric.html)
