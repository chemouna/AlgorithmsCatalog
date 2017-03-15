
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

### Shortest Path Problem

### Djikstra's Algorithm


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

