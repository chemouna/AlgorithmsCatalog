
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

### External Sorting 

### In-Place RadixSort 

### American Flag sort 

### Near Sorting Algorithms

## Selection Algorithms

### Median Finding algorithms

## Insertion Algorithms 

## Scanning Algorithms 

## In-Place Algorithms
### In-Place Merging 

## String Matching Algorithms

## Graph Algorithms

## Overlapping subproblems

## Pearls

## Tree Algorithms 

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

#### Min-max-median Heap

#### D-ary Heap

#### Fibonacci Heap 

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

### Graphes 

### Succint Data Structures

### Data structures for Integer sorting

#### Van Emde Boas Tree

#### Y-fast Trie

#### Bucket Queue

### Others 


