
# Algorithmscatalog
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

## Recursion 


## Divide and Conquer


## Search Algorithms

## Finding Median 

### By insertion sort

### By Self balancing BST

### Heaps 
* Similar to balancing BST in Method 2 above, we can use a max heap on left side to represent elements that are less than effective median, and a min heap on right 
  side to represent elements that are greater than effective median. 

* After processing an incoming element, the number of elements in heaps differ utmost by 1 element. When both heaps contain same number of elements, 
  we pick average of heaps root data as effective median. When the heaps are not balanced, we select effective median from the root of heap containing more elements.

* Heaps can be represented as arrays for which a[k] <= a[2*k+1] and a[k] <= a[2*k+2] for all k, counting elements from 0. For the sake of comparison,
  non-existing elements are considered to be infinite. The interesting property of a heap is that a[0] is always its smallest element (in case of min heap 
  and biggest element in case of max heap).
  - An application example is binary tournament we see in sports, each cell is the winner over the two cells it tops, and we can trace the winner down the tree
    to see all opponents s/he had.  However, in many computer applications of such tournaments, we do not need to trace the history of a winner.
    To be more memory efficient, when a winner is promoted, we try to replace it by something else at a lower level, and the rule becomes
    that a cell and the two cells it tops contain three different items, but the top cell "wins" over the two topped cells.

  - Another application example is event simulation since a  nice feature of the heap sort is that you can efficiently insert new items while the sort is going on, 
   provided that the inserted items are not "better" than the last 0'th element you extracted. and in event simulation contexts the tree holds all
   incoming events, and the "win" condition means the smallest scheduled time.  When an event schedule other events for execution, they are scheduled into
   the future, so they can easily go into the heap.  So, a heap is a good structure for implementing schedulers

  - If the heap invariant is protected at all time, index 0 is clearly the overall winner.  The simplest algorithmic way to remove it and
  find the "next" winner is to move some loser into the 0 position, and then percolate this new 0 down the tree, exchanging values, until 
  the invariant is re-established. This is clearly logarithmic on the total number of items in the tree. By iterating over all items, you get an O(n ln n) sort.
 
 
 
### Binary Search
Binary search is used to quickly find a value in a sorted sequence (consider a sequence an ordinary array for now). 
The search space is initially the entire sequence. At each step, the algorithm compares the median value in the search space to the target value. 
Based on the comparison and because the sequence is sorted, it can then eliminate half of the search space. By doing this repeatedly, it will eventually 
be left with a search space consisting of a single element, the target value.

#### Pseudo code 
Given an array A of n elements with values or records A0 ... An−1, sorted such that A0 ≤ ... ≤ An−1, 
and target value T, find the index of T in A.

1/ Set L to 0 and R to n − 1.
2/ If L > R, the search terminates as unsuccessful.
3/ Set m (the position of the middle element) to the floor (the largest previous integer) of (L + R) / 2.
4/ If Am < T, set L to m + 1 and go to step 2.
5/ If Am > T, set R to m – 1 and go to step 2.
6/ Now Am = T, the search is done; return m.

```
binary_search(A, target):
   lo = 1, hi = size(A)
   while lo <= hi:
      mid = lo + (hi-lo)/2
      if A[mid] == target:
         return mid
      else if A[mid] < target: 
         lo = mid+1
      else:
         hi = mid-1
            
   // target was not found
```

#### Discrete binary search
A sequence (array) is really just a function which associates integers (indices) with the corresponding values. However, there is no reason to restrict our usage of 
binary search to tangible sequences. In fact, we can use the same algorithm described above on any monotonic function f whose domain is the set of integers. 
The only difference is that we replace an array lookup with a function evaluation: we are now looking for some x such that f(x) is equal to the target value. 
The search space is now moreformally a subinterval of the domain of the function, while the target value is an element of the codomain. 

* We can use binary search to find the smallest legal solution, i.e. the smallest x for which p(x) is true. The first part of devising a solution based on 
  binary search is designing a predicate which can be evaluated and for which it makes sense to use binary search: we need to choose what the algorithm 
  should find. We can have it find either the first x for which p(x) is true or the last x for which p(x) is false. 

* One important thing to remember before beginning to code is to settle on what the two numbers you maintain (lower and upper bound) mean. A likely answer is a 
  closed interval which surely contains the first x for which p(x) is true. All of your code should then be directed at maintaining this invariant: it tells 
  you how to properly move the bounds, which is where a bug can easily find its way in your code, if you’re not careful.

* Advice : helpful advice can be given here other than to always double- and triple-check your bounds! Also, since execution time increases logarithmically 
  with the bounds, you can always set them higher, as long as it doesn’t break the evaluation of the predicate. Keep your eye out for overflow errors all around, 
  especially in calculating the median.
  And remember to always test your code on a two-element set where the predicate is false for the first element and true for the second.

* When you encounter a problem which you think could be solved by applying binary search, you need some way of proving it will work. 
  So consider a predicate p defined over some ordered set S (the search space). The search space consists of candidate solutions to the problem. 
   binary search can be used if and only if for all x in S, p(x) implies p(y) for all y > x. This property is what we use when we discard the second half of the search space. 
   It is equivalent to saying that ¬p(x) implies ¬p(y) for all y < x (the symbol ¬ denotes the   logical not operator), which is what we use when we discard the first half of the search space. 
   binary search can also be used when a predicate yields a series of yes answers followed by a series of no answers. 
   we can use binary search to find the smallest legal solution, i.e. the smallest x for which p(x) is true. The first part of devising a solution based on binary search is designing a predicate 
   which can be evaluated and for which it makes sense to use binary search: we need to choose what the algorithm should find. We can have it find either the first x for which p(x) is true or the last x for which p(x) is false
   
   
   
```
binary_search(lo, hi, p):
   while lo < hi:
      mid = lo + (hi-lo)/2
      if p(mid) == true: // When p(mid) is true, we can discard the second half of the search space, 
                         // since the predicate is true for all elements in it (by the main theorem). 
         hi = mid
      else:    // we can discard the first half of the search space, but this time including mid. p(mid) is false 
              //so we don’t need it in our search space. 
         lo = mid+1
          
   if p(lo) == false:
      complain                // p(x) is false for all x in S!
      
   return lo         // lo is the least x for which p(x) is true
```

using mid = lo + (hi-lo)/2 instead of the usual mid = (lo+hi)/2. This is to avoid another potential rounding bug: in the first case, 
we want the division to always round down, towards the lower bound. But division truncates, so when lo+hi would be negative, it would 
start rounding towards the higher bound. Coding the calculation this way ensures that the number divided is always positive and hence 
always rounds as we want it to. 

* we may use a greedy algorithm to evaluate the predicate (like in FairWorkLoad problem from topcoder). In other problems, evaluating the predicate can come 
  down to anything from a simple math expression to finding a maximum cardinality matching in a bipartite graph. 

* Remember to verify that the lower and upper bounds are not overly constrained: it’s usually better to relax them as long as it doesn’t break the predicate 

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

#### Counting sort 

#### Flash Sort

- [Haskell implementation](TODO)
- [Java Implementation](TODO)

### QuickSort
- One of the major factors is that quicksort has better locality of reference -- the next thing to be accessed is 
  usually close in memory to the thing you just looked at. By contrast, heapsort jumps around significantly more. 
  the element of the Since things that are close together will likely be cached together, quicksort tends to be faster.

### MergeSort

* If a dataset is really huge and doesn't fit into memory, then merge sort works better. 
  It's frequently used in clusters where dataset can span over hundreds of machines.

* Divide: Divide the n-element sequence to be sorted into two subsequences of n=2 elements each.
  Conquer: Sort the two subsequences recursively using merge sort.
  Combine: Merge the two sorted subsequences to produce the sorted answer.
  The recursion “bottoms out” when the sequence to be sorted has length 1, in which case there is no work to be done, since every sequence of length 1 is already in
  sorted order. 



### American Flag sort 
- works similar to counting sort in that you need an array to count how often each element appears. So if we sort bytes, 
  we also need a count array of 256 elements. Then we also compute the prefix sum of this count array, like we did in 
  counting sort. Only the final loop is different Since American Flag Sort is in-place, the value in a new output array 
  we need to swap instead in place

### Sorting nearly sorted data
Sorting nearly sorted data is common in practice :
  - Insertion sort is the clear winner for nearly sorted data.
  - Bubble sort is fast, but insertion sort has lower overhead.
  - Shell sort is fast because it is based on insertion sort.
  - Merge sort, heap sort, and quick sort do not adapt to nearly sorted data.
  - Insertion sort provides a O(n2) worst case algorithm that adapts to O(n) time when the data is nearly sorted. 
  - 

### External Sorting 
can handle massive amounts of data. External sorting is required when the data being sorted do not fit into the main memory 
of a computing device (usually RAM) and instead they must reside in the slower external memory (usually a hard drive). External 
sorting typically uses a hybrid sort-merge strategy. In the sorting phase, chunks of data small enough to fit in main memory are 
read, sorted, and written out to a temporary file. In the merge phase, the sorted subfiles are combined into a single larger file.


### In-Place RadixSort 


### Near Sorting Algorithms

## Selection Algorithms

### Median Finding algorithms

### K-th Order Statistics


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
  
### Collision resolution

#### Separate chaining with linked lists 
* Chained hash tables with linked lists are popular because they require only basic data structures with simple algorithms, and can use 
  simple hash functions that are unsuitable for other methods.

* More sophisticated data structures, such as balanced search trees, are worth considering only if the load factor is large (about 10 or more), 
  or if the hash distribution is likely to be very non-uniform, or if one must guarantee good performance even in a worst-case scenario. However,
  using a larger table and/or a better hash function may be even more effective in those cases. 

* Chained hash tables also inherit the disadvantages of linked lists. When storing small keys and values, the space overhead of the next pointer 
  in each entry record can be significant. An additional disadvantage is that traversing a linked list has poor cache performance, making the 
  processor cache ineffective. 

#### Separate chaining with other structures
* Instead of a list, one can use any other data structure that supports the required operations. For example, by using a self-balancing 
  binary search tree, the theoretical worst-case time of common hash table operations (insertion, deletion, lookup) can be brought down 
  to O(log n) rather than O(n). However, this introduces extra complexity into the implementation, and may cause even worse performance 
  for smaller hash tables, where the time spent inserting into and balancing the tree is greater than the time needed to perform a linear 
  search on all of the elements of a list.

#### Open addressing 
is a method of collision resolution in hash tables. With this method a hash collision is resolved by probing, or searching through alternate locations 
in the array (the probe sequence) until either the target record is found, or an unused array slot is found, which indicates that there is no such key in the table

* In another strategy, called open addressing, all entry records are stored in the bucket array itself. When a new entry has to be inserted, 
  the buckets are examined, starting with the hashed-to slot and proceeding in some probe sequence, until an unoccupied slot is found. When 
  searching for an entry, the buckets are scanned in the same sequence, until either the target record is found, or an unused array slot is 
  found, which indicates that there is no such key in the table.

Examples probe sequences: Double Hashing, Linear probing, Quadratic probing 

* has the best cache performance but is most sensitive to clustering, while double hashing has poor cache performance but exhibits virtually no clustering; 
  quadratic probing falls in-between in both areas. Double hashing can also require more computation than other forms of probing 

* the load factor increases towards 100%, the number of probes that may be required to find or insert a given key rises dramatically. Once the table becomes 
  full, probing algorithms may even fail to terminate. 

```
 record pair { key, value }
 var pair array slot[0..num_slots-1]

function find_slot(key)
     i := hash(key) modulo num_slots
     // search until we either find the key, or find an empty slot.
     while (slot[i] is occupied) and ( slot[i].key ≠ key )
         i = (i + 1) modulo num_slots
     return i

function lookup(key)
     i := find_slot(key)
     if slot[i] is occupied   // key is in table
         return slot[i].value
     else                     // key is not 
     in table
         return not found

function set(key, value)
     i := find_slot(key)
     if slot[i] is occupied   // we found our key
         slot[i].value = value
         return
     if the table is almost full
         rebuild the table larger 
         i = find_slot(key)
     slot[i].key   = key
     slot[i].value = value
```
 
Linear Probiling, quadratic probing and double hashing are a form of open addressing.

##### Linear Probing 
Linear probing is a scheme in computer programming for resolving collisions in hash tables, data structures for maintaining a collection 
of key–value pairs and looking up the value associated with a given key.

* Linear probing provides good locality of reference, which causes it to require few uncached memory accesses per operation. 
  Because of this, for low to moderate load factors, it can provide very high performance. However, compared to some other open 
  addressing strategies, its performance degrades more quickly at high load factors because of primary clustering, a tendency for 
  one collision to cause more nearby collisions

* Using linear probing, dictionary operations can be implemented in constant expected time. In other words, insert, remove and search 
  operations can be implemented in O(1), as long as the load factor of the hash table is a constant strictly less than one. 

* linear probing searches the table for the closest following free location and inserts the new key there. Lookups are performed in the same way, 
  by searching the table sequentially starting at the position given by the hash function, until finding a cell with a matching key or an empty cell. 

* Search: To search for a given key x, the cells of T are examined, beginning with the cell at index h(x) (where h is the hash function) 
  and continuing to the adjacent cells h(x) + 1, h(x) + 2, ..., until finding either an empty cell or a cell whose stored key is x. If a 
  cell containing the key is found, the search returns the value from that cell. Otherwise, if an empty cell is found, the key cannot be 
  in the table 

* Insertion: To insert a key–value pair (x,v) into the table (possibly replacing any existing pair with the same key),  follows the same sequence 
  of cells that would be followed for a search, until finding either an empty cell or a cell whose stored key is x. The new key–value pair is then 
  placed into that cell.
  If the insertion would cause the load factor of the table (its fraction of occupied cells) to grow above some preset threshold, 
  the whole table may be replaced by a new table, larger by a constant factor, with a new hash function. Setting this threshold close 
  to zero and using a high growth rate for the table size leads to faster hash table operations but greater memory usage than threshold 
  values close to one and low growth rates. 
  A common choice would be to double the table size when the load factor would exceed 1/2, causing the load factor to stay between 1/4 and 1/2. 

* Because linear probing is especially sensitive to unevenly distributed hash values,[7] it is important to combine it with a high-quality 
  hash function that does not produce such irregularities. 

###### Primary clustering
* One of two major failure modes of open addressing based hash tables, especially those using linear probing. It occurs after a hash 
  collision causes two   of the records in the hash table to hash to the same position, and causes one of the records to be moved to 
  the next location in its probe sequence.

* Primary Clustering is the tendency for a collision resolution scheme such as linear probing to create long runs of filled slots 
  near the hash position  of keys.
  If the primary hash index is x, subsequent probes go to x+1, x+2, x+3 and so on, this results in Primary Clustering.
  Once the primary cluster forms, the bigger the cluster gets, the faster it grows. And it reduces the performance. 

###### Secondary clustering, 
* Secondary Clustering is the tendency for a collision resolution scheme such as quadratic probing to create long runs of filled slots 
  away from the hash position of keys.
  If the primary hash index is x, probes go to x+1, x+4, x+9, x+16, x+25 and so on, this results in Secondary Clustering.
  Secondary clustering is less severe in terms of performance hit than primary clustering, and is an attempt to keep clusters from forming 
  by using Quadratic Probing. The idea is to probe more widely separated cells, instead of those adjacent to the primary hash site.

* Both types of clustering may be reduced by using a higher-quality hash function, or by using a hashing method such as double hashing that 
  is less susceptible to clustering 

###### Examples
* Java's HashTable: 
Hash tables deal with collisions in one of two ways.
1/ By having each bucket contain a linked list of elements that are hashed to that bucket. This is why a bad hash function can make 
   lookups in hash tables very slow.

2/ If the hash table entries are all full then the hash table can increase the number of buckets that it has and then redistribute all 
   the elements in the table. The hash function returns an integer and the hash table has to take the result of the hash function and 
   mod it against the size of the table that way it can be sure it will get to bucket. so by increasing the size it will rehash and run 
   the modulo calculations which if you are lucky might send the objects to different buckets. 

* The internal array of HashMap is of fixed size, and if you keep storing objects, at some point of time hash function will return same bucket 
  location for two different keys
  If we try to retrieve an object from this linked list, we need an extra check to search correct value, this is done by equals() method. 
  Since each node contains an entry, HashMap keeps comparing entry's key object with the passed key using equals() and when it return true, 
  Map returns the corresponding value.

* there is a potential race condition exists while resizing HashMap in Java, if two thread at the same time found that now HashMap needs 
  resizing and they both try to resizing. on the process of resizing of HashMap in Java, the element in the bucket which is stored in linked list 
  get reversed in order during their migration to new bucket because Java HashMap  doesn't append the new element at tail instead it append new 
  element at the head to avoid tail traversing. If race condition happens then you will end up with an infinite loop.

##### Cuckoo hashing 

##### Robin Hood hashing

### Modular Hashing 

### Horner's method 

### Rolling Hashes 

### Carter-Wegman class of hash functions

## Strings

### Double hash technique 

### String Matching Algorithms

#### Knuth–Morris–Pratt algorithm

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

#### Boyer-Moore Algorithm

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

#### Boyer–Moore–Horspool or Horspool algorithm

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
#### Rabin-Karp algorithm 

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


### Huffman Compression
* The idea is to abandon the way in which text files are usually stored: instead of using the usual 7 or 8 bits for each character, 
  we use fewer bits for characters that appear often than for those that appear rarely. 
  Huffman code is a particular type of optimal prefix code that is commonly used for lossless data compression. 

#### Variable-length code
* is a code which maps source symbols to a variable number of bits. 


### Aho–Corasick algorithm
 

## Algorithms on arrays

### Sliding Window Algorithm

#### minimum on a sliding window algorithm 

## Graph Algorithms

### Minimum Spanning Trees
* a spanning tree of a graph is a connected subgraph with no cycles that includes all the vertices. 
A minimum spanning tree (MST ) of an edge-weighted graph is a spanning tree whose weight (the sum of the weights 
of its edges) is no larger than the weight of any other spanning tree. 

```
GENERIC-MST.G;w/
A = Empty
while A does not form a spanning tree
    find an edge (u, v) that is safe for A
    A = A union {(u, v)}
return Ab
```
Kruskal and Prim differ in the way they choose a safe edge : 
In Kruskal’s algorithm, the set A is a forest whose vertices are all those of the given graph. The safe edge added to A 
is always a least-weight edge in the graph that connects two distinct components. In Prim’s algorithm, the
set A forms a single tree. The safe edge added to A is always a least-weight edge connecting the tree to a vertex not in the tree. 

#### Prim’s algorithm 

#### Kruskal’s algorithm 
* Kruskal’s algorithm finds a safe edge to add to the growing forest by finding, of all the edges that connect any two trees in the 
  forest, an edge (u, v) of least weight. 

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
  sort the edges of G:E into nondecreasing order by weight w
  foreach (u, v) in G.E ordered by weight(u, v), increasing:
     if FIND-SET(u) ≠ FIND-SET(v):
        A = A ∪ {(u, v)}
        UNION(u, v)
 return A
```
* This implementation uses a disjoint-set data structure to maintain several disjoint sets of elements. Each set contains 
  the vertices in one tree of the current forest. The operation FIND-SET(u) returns a representative element
  from the set that contains u. Thus, we can determine whether two vertices u and v belong to the same tree by testing 
  whether FIND-SET(u) equals FIND-SET(v).  

* With Kruskal’s algorithm and Prim’s algorithm, we can easily make each of them run in time O(E lgV), using ordinary binary heaps. 
  By using Fibonacci heaps, Prim’s algorithm runs in time O(E + V lg V), which improves over the binary-heap implementation 
  if |V| is much smaller than |E|. 

### Union find data structure / Disjoint sets datastructure
 The union–find data type (disjoint-sets data type). It supports the union and find operations,
 along with a connected operation for determining whether  two sites are in the same component and a count
 operation that returns the total number of components. 
 
- many applications for union-find data structur:
     - Friends in a social network
     - Pixels in a digital photo
     - Computers in a network
     ....
-  a disjoint-set data structure, also called a union–find data structure or merge–find set, is a data structure that keeps track of a set of elements partitioned into a number of disjoi   nt (nonoverlapping) subsets. 
 
- Union by rank: always attach the smaller tree to the root of the larger tree. Since it is the depth of the tree that affects the running time, the tree with 
  smaller depth gets added under the root of the deeper tree, which only increases the depth if the depths were equal. 
  (O(log n) algorithm)
  
```
 function MakeSet(x)
     x.parent := x
     x.rank   := 0
     
 function Union(x, y)
     xRoot := Find(x)
     yRoot := Find(y)
     // if x and y are already in the same set (i.e., have the same root or representative)
     if xRoot == yRoot
         return

     // x and y are not in same set, so we merge them
     if xRoot.rank < yRoot.rank
         xRoot.parent := yRoot
     else if xRoot.rank > yRoot.rank
         yRoot.parent := xRoot
     else
         yRoot.parent := xRoot
         xRoot.rank := xRoot.rank + 1
```

- Path compression
 flattening the structure of the tree whenever Find is used on it. The idea is that each node visited on the way to a root node may as well be attached directly to 
 the root node; they all share the same representative. To effect this, as Find recursively traverses up the tree, it changes each node's parent reference to point 
 to the root that it found, The resulting tree is much flatter, speeding up future operations not only on these elements but on those referencing them.
 
```
 function Find(x)
     if x.parent != x
        x.parent := Find(x.parent)
     return x.parent
```
With these two techniques the amortized time per operation is only  O(a(n)), where O(a(n)) is the inverse of the function 
n=f(x)=A(x,x) and A is the extremely fast-growing Ackermann function, Thus, the amortized running time per operation is effectively a small constant.. 

#### Other Applications


#### Disjoint set Forests 
- Disjoint-set forests are data structures where each set is represented by a tree data structure, in which each node holds a reference to its parent 
  node (see parent pointer tree).
  

#### Minimum spanning forest 
If a graph is not connected, we can adapt our algorithms to compute the MSTs of each of its connected components known
as a minimum spanning forest.

* Example problems solved by MST:
//TODO
//TODO problems from topcoder

#### Topological Sorting 
*  a topological sort or topological ordering of a directed graph is a linear ordering of its vertices such that for every directed edge uv from vertex u to 
   vertex v, u comes before v in the ordering. For instance, the vertices of the graph may represent tasks to be performed, and the edges may represent constraints
   that one task must be performed before another; in this application, a topological ordering is just a valid sequence for the tasks. A topological ordering is 
   possible if and only if the graph has no directed cycles 
* The usual algorithms for topological sorting have running time linear in the number of nodes plus the number of edges, asymptotically,  

##### Kahn's algorithm 
The idea of  Kahn’s algorithm is to repeatedly remove nodes that have zero in-degree. 

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
Time complexity is O(|V| + |E|) and space complexiy is O(|V|)

#### Topological sorting based on DFS 
loops through each node of the graph, in an arbitrary order, initiating a depth-first search that terminates when it hits any node that has already been visited 
since the beginning of the topological sort or the node has no outgoing edges (i.e. a leaf node):

```
L ← Empty list that will contain the sorted nodes
while there are unmarked nodes do
    select an unmarked node n
    visit(n) 
    
function visit(node n)
    if n has a temporary mark then stop (not a DAG)
    if n is not marked (i.e. has not been visited yet) then
        mark n temporarily //equivalent to discovered
        for each node m with an edge from n to m do
            visit(m)
        mark n permanently //eauivalent to visited
        unmark n temporarily
        add n to head of L
```

##### Coffman–Graham algorithm 

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

* DFS is typically used to traverse an entire graph, and takes time Θ(|V| + |E|) linear in the size of the graph. 
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

### Resemblence between BFS and DFS 
- the symetry between BFS and DFS is cool :
DFS:
```
list nodes_to_visit = {root}
while(nodes_to_visit isnt empty) {
  current_node = nodes_to_visit.take_first();
  nodes_to_visit.preprend(current_node.children);
  //do something
}
```

BFS:
```
list nodes_to_visit = {root}
while(nodes_to_visit isnt empty) {
  current_node = nodes_to_visit.take_first();
  nodes_to_visit.append(current_node.children)
}
```

### Connected Components
* A directed graph is weakly connected if it would be connected by ignoring the direction of edges. Thus, a weakly connected
  graph consists of a single piece. A directed graph is strongly connected if there is a directed path between every pair of vertices. 


#### Strongly Connected Components 
A strongly connected component is a maximal subgraph, where all the vertices are strongly connected with each other:

STRONGLY-CONNECTED-COMPONENTS.
   1. call DFS.G/ to compute finishing times u.f for each vertex u
   2. compute transpose of G
   3. call DFS. on transpose of G, but in the main loop of DFS, consider the vertices in order of decreasing u.f (as computed in line 1)
   4. output the vertices of each tree in the depth-first forest formed in line 3 as a separate strongly connected component
this linear-time (i.e., O(V+E)-time) algorithm computes the strongly connected components of a directed graph G=(V,E) using two depth-first
searches, one on G and one on transpose of G.

Kosaraju’s algorithm:
```
Given a digraph G, use DepthFirstOrder to compute the reverse postorder of its reverse, Gr.
    - Run standard DFS on G, but consider the unmarked vertices in the order just computed instead of the standard numerical order.
    - All vertices reached on a call to the recursive dfs() from the constructor are in a strong component (!), so identify them as in CC.
```
- Kosaraju’s algorithm is an extreme example of a method that is easy to code but difficult to understand. Despite its mysterious nature,
  if you follow the proof from Algorithms 4th Edition book for example you can be convinced that the algorithm is correct: 
  Algorithm: 
  ```
    - Create a order of vertices by finish time in decreasing order.
    - Reverse the graph
    - Do a DFS on reverse graph by finish time of vertex and created strongly connected components.
    - Runtime complexity - O(V + E)
    - Space complexity - O(V)
  ```
  Kosaraju uses a very clever trick based on the fact that if you reverse all of the edges in a graph, the resulting graph has the same 
  strongly connected components as the original. So using that, we can get the SCCs by doing a forward traversal to find an ordering of vertices, 
  then doing a traversal of the reverse of the graph in the order generated by the first traversal. 
 - the time complexity of Kosaraju is O(V+E).

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
* A DP is an algorithmic technique which is usually based on a recurrent formula and one (or some) starting states. 
A sub-solution of the problem is constructed from previously found ones. DP solutions have a polynomial complexity 
which assures a much faster running time than other techniques like backtracking, brute-force etc. 

* First step of DP is to find a state for which an optimal solution is found and with the help of which we can find the optimal solution for the next state. 
  where a state is a way to describe a situation, a sub-solution for the problem 
  Whenever a problem exhibits optimal substructure, we have a good clue that dynamic programming might apply, Consequently, we must take care to ensure that 
  the range of subproblems we consider includes those used in an optimal solution

* You will find yourself following a common pattern in discovering optimal substructure:
    1. You show that a solution to the problem consists of making a choice, such as choosing an initial cut in a rod or choosing an index at which to split 
       the matrix chain. Making this choice leaves one or more subproblems to be solved.
    2. You suppose that for a given problem, you are given the choice that leads to an optimal solution. You do not concern yourself yet with how to determine 
       this choice. You just assume that it has been given to you.
    3. Given this choice, you determine which subproblems ensue and how to best characterize the resulting space of subproblems.
    4. You show that the solutions to the subproblems used within an optimal solution to the problem must themselves be optimal 
     
*  Optimal substructure varies across problem domains in two ways:
    1. how many subproblems an optimal solution to the original problem uses, and
    2. how many choices we have in determining which subproblem(s) to use in an optimal solution. 

* for example In the rod-cutting problem, an optimal solution for cutting up a rod of size n uses just one subproblem (of size n - i ), but we must consider 
  n choices for i in order to determine which one yields an optimal solution. 
  Matrix-chain multiplication for the subchain A(i) A(i+1) ... A(j) serves as an example with two subproblems and j - i choices. For a given matrix 
  A(k) at which we split the product, we have two subproblems—parenthesizing A(i) A(i+1) .... A(k) and parenthesizing A(k+1) A(k+2) .... A(j) 
  and we must solve both of them optimally. Once we determine the optimal solutions to subproblems, we choose from among j - i candidates for
  the index k.

* the running time of a dynamic-programming algorithm depends on the product of two factors: the number of subproblems overall and how many
  choices we look at for each subproblem. In rod cutting, we had ‚.n/ subproblems overall, and at most n choices to examine for each, yielding 
  an O(n^2) running time.
  Matrix-chain multiplication had O(n^2) subproblems overall, and in each we had at most n - 1 choices, giving an O(n^3) running time.

* an in gradiant that an optimization problem must have for dynamic programming to apply is that the space of subproblems must be “small” in the sense
  that a recursive algorithm for the problem solves the same subproblems over and  over, rather than always generating new subproblems. Typically, 
  the total number of distinct subproblems is a polynomial in the input size. When a recursive algorithm revisits the same problem repeatedly, 
  we say that the optimization problem has overlapping subproblems.

* Whenever a recursion tree for the natural recursive solution to a problem contains the same subproblem repeatedly, and the total number of distinct subproblems

### Partition Problem
* problem deciding whether a given multiset S of positive integers can be partitioned into two subsets S1 and S2 such that the sum of the numbers in S1 equals the 
  sum of the numbers in S2. Although the partition problem is NP-complete, there is a pseudo-polynomial time dynamic programming solution, 
  an optimization version of the partition problem, which is to partition the multiset S into two subsets S1, S2 such that the difference between the sum of elements 
  in S1 and the sum of elements in S2 is minimized 
  

## Greedy Algorithms 
* follows the problem solving heuristic of making the locally optimal choice at each stage[1] with the hope of finding a global optimum, In mathematical optimization, 
greedy algorithms solve combinatorial problems having the properties of matroids. 

* greedy algorithms have five components:
 - A candidate set, from which a solution is created
 - A selection function, which chooses the best candidate to be added to the solution
 - A feasibility function, that is used to determine if a candidate can be used to contribute to a solution
 - An objective function, which assigns a value to a solution, or a partial solution, and
 - A solution function, which will indicate when we have discovered a complete solution 

* Steps to design greedy algorithms:
- Cast the optimization problem as one in which we make a choice and are left with one subproblem to solve. 
- Prove that there is always an optimal solution to the original problem that makes the greedy choice, so that the greedy choice is always safe 
- Demonstrate optimal substructure by showing that, having made the greedy choice, what remains is a subproblem with the property that if we 
  combine an optimal solution to the subproblem with the greedy choice we have made, we arrive at an optimal solution to the original problem. 

* Greedy-choice property: 
- We can assemble a globally optimal solution by making locally optimal (greedy) choices.  when we are considering which choice to make, we make
  the choice that looks best in the current problem, without considering results from subproblems.

* By preprocessing the input or by using an appropriate data structure (often a priority queue), we often can make greedy choices quickly, 
  thus yielding an efficient algorithm.

* Greedy versus dynamic programming:
- A dynamicprogramming algorithm proceeds bottom up, whereas a greedy strategy usually progresses in a top-down fashion, making one greedy 
  choice after another, reducing each given problem instance to a smaller one. 
  
### Matroids and greedy methods

#### Greedy algorithms on a weighted matroid

### Techniques for solving greedy algorithms problems 
- Preprocess the input first like sorting it or putting it in a datastructure such as a queue (An example is sorting the input by finish time as done in 
  activity scheduling problem).

- Decompose the greedy choice into multiple cases if it can be handled as one as used in this topcoder problem : [BoardSplitting](The greedy choice can be composed of multiple cases)

## Dynamic Programming 

### Longest increasing subsequence

### Longest common subsequence problem
An elegant recursive approach to solving this problem is based around the observation that the LCS of two sequences can be built from the LCSes of 
prefixes of these sequences.In algorithm speak, the longest common subsequence problem has optimal substructure.

LCS in DP:
```
def lcs(x, y):
    n = len(x)
    m = len(y)
    table = dict()  # a hashtable, but we'll use it as a 2D array here
 
    for i in range(n+1):     # i=0,1,...,n
        for j in range(m+1):  # j=0,1,...,m
            if i == 0 or j == 0:
                table[i, j] = 0
            elif x[i-1] == y[j-1]:
                table[i, j] = table[i-1, j-1] + 1
            else:
                table[i, j] = max(table[i-1, j], table[i, j-1])
 
    # Now, table[n, m] is the length of LCS of x and y.
 
    # Let's go one step further and reconstruct
    # the actual sequence from DP table:
 
    def recon(i, j):
        if i == 0 or j == 0:
            return []
        elif x[i-1] == y[j-1]:
            return recon(i-1, j-1) + [x[i-1]]
        elif table[i-1, j] > table[i, j-1]: #index out of bounds bug here: what if the first elements in the sequences aren't equal
            return recon(i-1, j)
        else:
            return recon(i, j-1)
 
    return recon(n, m)
```

### String Edit Distance

### Matrix Chain Multiplication
an optimization problem that can be solved using dynamic programming. Given a sequence of matrices, the goal is to find the most efficient way to multiply these matrices. 
The problem is not actually to perform the multiplications, but merely to decide the sequence of the matrix multiplications involved.

We can find the minimum cost using the following recursive algorithm:
- Take the sequence of matrices and separate it into two subsequences.
- Find the minimum cost of multiplying out each subsequence.
- Add these costs together, and add in the cost of multiplying the two result matrices.
- Do this for each possible position at which the sequence of matrices can be split, and take the minimum over all of them.

* One simple solution is called memoization: each time we compute the minimum cost needed to multiply out a specific subsequence, we save it.
  If we are ever asked to compute it again, we simply give the saved answer, and do not recompute it. Since there are about n2/2 different subsequences, 
  where n is the number of matrices, the space required to do this is reasonable. It can be shown that this simple trick brings the runtime down to 
  O(n^3) from O(2^n), which is more than efficient enough for real applications. 

* There are algorithms that are more efficient than the O(n3) dynamic programming algorithm, though they are more complex.

  An algorithm published by Hu and Shing achieves O(n log n) complexity. They showed how the matrix chain multiplication problem can be transformed (or reduced) 
  into the problem of triangulation of a regular polygon.

### Egg Dropping 
refers to a class of problems in which it is important to find the correct response without exceeding a (low) number of certain failure states. 
In a toy example, there is a tower of  floors, and an egg dropper with  ideal eggs. The physical properties of the ideal egg is such that it will shatter 
if it is dropped from floor  or above, and will have no damage whatsoever if it is dropped from floor  or below. The problem is to find a strategy such that 
the egg dropper can determine the floor  in as few egg drops as possible. This problem has many applications in the real world such as avoiding a call out to 
the slow HDD, or attempting to minimize cache misses, or running a large number of expensive queries on a database.

* To derive a dynamic programming functional equation for this puzzle, let the state of the dynamic programming model be a pair s = (n,k), where
  n = number of test eggs available, n = 0, 1, 2, 3, ..., N − 1.
  k = number of (consecutive) floors yet to be tested, k = 0, 1, 2, ..., H − 1.
  For instance, s = (2,6) indicates that two test eggs are available and 6 (consecutive) floors are yet to be tested. 

*  let W(n,k) = minimum number of trials required to identify the value of the critical floor under the worst-case scenario given that the process is in state s = (n,k).
   Then it can be shown that : 
   W(n,k) = 1 + min { max (W(n − 1, x − 1), W(n,k − x)): x = 1, 2, ..., k }
   with W(n,0) = 0 for all n > 0 and W(1,k) = k for all k. It is easy to solve this equation iteratively by systematically increasing the values of n and k.

    the above solution takes {\displaystyle O(nk^{2})} O(nk^{2}) time with a DP solution. This can be improved to  O(nk log k) time by binary searching 
    on the optimal  x in the above recurrence,  W(n-1,x-1) is increasing in x while W(n,k-x) is decreasing in x, thus a local minimum of 
    max( W(n-1, x-1), W(n, k-x)) is a global minimum. by storing the optimal x for each cell in the DP table and referring to its value for the 
    previous cell, the optimal x for each cell can be found in constant time, improving it to O(nk) time.

Pseudo code for the solution:
```
def drops(n,h):
    if(n == 1 or k == 0 or k == 1):
        return k
    end if

    minimum = ∞

    for x = 1 to h:
        minimum = min(minimum, 
                      1 + max(drops(n - 1, h - 1), drops(n, h - x))
                      )
    end for

    return minimum
```

### Optimal binary search tree
* An optimal binary search tree, sometimes called a weight-balanced binary tree, is a binary search tree which provides the smallest 
 possible search time for a given sequence of accesses (or access probabilities). Optimal BSTs are generally divided into 
 two types: static and dynamic. 
 - In the static optimality problem, the tree cannot be modified after it has been constructed. In this case, there exists some particular 
   layout of the nodes of the tree which provides the smallest expected search time for the given access probabilities.
 - In the dynamic optimality problem, the tree can be modified at any time, typically by permitting tree rotations.

* c(i,j) represents the expected cost of searching an optimal binary search tree containing the keys ki, ..., kj. w(i,j) represents 
  the probability sum of the subtree containing the keys ki, ..., kj. For the formula：
```
c(i, j) = min (i < k <= j) {c(i, k-1) + c(k, j) + p(k) + w(i, k-1) + w(k,j)}
```
```c(i,k-1)+w(i,k-1)```` reresents the cost for the left subtree if we choose key k as the root. c(k,j) + w(k,j) represents the cost for the
   right subtree. p(k) represents the cost for the root k.

   If we choose key k as the root, then the left subtree contains the keys ki, ..., k(k-1) and the right subtree contains the kyes k(k+1), ..., kj. 
   But we can not simply say that:
   ```
   c(i,j)=min (i < k <= j) {c(i, k-1) + c(k, j) + p(k)}
   ```
   Because when we choose the key k for the root, the generated subtrees has their depth added by 1. So c(i,k-1)+w(i,k-1) will be the right cost 
   for the left subtree! 

### Line breaking / Text Justification 
- The idea then is to come up with a configuration of line breaks which minimizes the total sum of such penalties, a strategy know as "minimum raggedness". 
  A line exceeding the allowed width should incur an infinitely large penalty; otherwise the cost should follow a quickly growing function, such as the 
  squared size of the gap. 

- line breaking defined is a special case of the "least weight subsequence" problem. 
- There is an optimum length for a line: lineopt, The penalty for a line being too short or too long ```= (length of current line – lineopt)^2```
  with the exception : last line cannot be penalized for being too short.

### The Least Weight Subsequence Problem

### Segment trees
- a tree data structure for storing intervals, or segments. It allows querying which of the stored segments contain a given point. It is, in principle, a static structure
- A segment tree for a set I of n intervals uses O(n log n) storage and can be built in O(n log n) time. Segment trees support searching for all the intervals that contain
  a query point in O(log n + k), k being the number of retrieved intervals or segments


### Interval Trees
- an interval tree is a tree data structure to hold intervals. Specifically, it allows one to efficiently find all intervals that overlap with any given interval or point.
  It is often used for windowing queries


### Fenwick Trees
- A Fenwick tree or binary indexed tree is a data structure that can efficiently update elements and calculate prefix sums in a table of numbers.
- When compared with a flat array of numbers, the Fenwick tree achieves a much better balance between two operations: element update and prefix sum calculation.
  In a flat array of n numbers, you can either store the elements, or the prefix sums. In the first case, computing prefix sums requires linear time; in the second case,
  updating the array elements requires linear time. Fenwick trees allow both operations to be performed in O(log n) time. This is achieved by representing the numbers as
  a tree, where the value of each node is the sum of the numbers in that subtree. The tree structure allows operations to be performed using only O(log n) node accesses.

- in practice they are implemented as an implicit data structure using a flat array. Given an index in the array representing a vertex, the index of a vertex's parent or
  child is calculated through bitwise operations on the binary representation of its index. Each element of the array contains the pre-calculated sum of a range of values,
  and by combining that sum with additional ranges encountered during an upward traversal to the root, the prefix sum is calculated.


## Computational Geometry Algorithms 

### Closest pair of points problem
- [Definition in wikipedia](https://en.wikipedia.org/wiki/Closest_pair_of_points_problem)

## Randomized Algorithms

### Random permutation/Shuffling
 
#### Fisher–Yates shuffle 
* Steps of the algorithm: 
    1 - Write down the numbers from 1 through N.
    2 - Pick a random number k between one and the number of unstruck numbers remaining (inclusive).
    3 - Counting from the low end, strike out the kth number not yet struck out, and write it down at the end of a separate list.
    4 - Repeat from step 2 until all the numbers have been struck out.
    5 - The sequence of numbers written down in step 3 is now a random permutation of the original numbers 

##### Modern version of Fisher-Yates (Algorithm P)

#### Sattolo's algorithm
* The only difference between Durstenfeld's and Sattolo's algorithms is that in the latter, in step 2 above, the random number j is chosen 
  from the range between 1 and i−1 (rather than between 1 and i) inclusive. This simple change modifies the algorithm so that the resulting 
  permutation always consists of a single cycle. 


### Cyclic Permutations 


## Backtracking 
- Backtracking is a general algorithm for finding all (or some) solutions to some computational problems that incrementally
  builds candidates to the solutions, and abandons each partial candidate c ("backtracks") as soon as it determines that c 
  cannot possibly be completed to a valid solution.

## Data Structures 

### Linear Data Structures 

#### Array

#### Stack
- a linear data structure, or more abstractly a sequential collection, the push and pop operations occur only at one end of the structure, referred to as the top of the stack.
This makes it possible to implement a stack as a singly linked list and a pointer to the top element.
 
There are multiple possible ways to implement a Stack:
- With a static array 

- With a Dynamic array 

- With a LinkedList 

##### Applications of stacks
- Expression evaluation

- Backtracking

- Efficient Algorithms


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

#### Min Heap


#### Max Heap 

#### Min-Max Heap 
* a min-max heap is a complete binary tree data structure which combines the usefulness of both a min-heap and a max-heap, that is, it provides 
constant time retrieval and logarithmic time removal of both the minimum and maximum elements in it. 


##### Min-max-median Heap

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
a B-tree is a self-balancing tree data structure that keeps data sorted and allows searches, sequential access, insertions, and deletions in logarithmic time. 
The B-tree is a generalization of a binary search tree in that a node can have more than two children. Unlike self-balancing binary search trees, the B-tree 
is optimized for systems that read and write large blocks of data. B-trees are a good example of a data structure for external memory. It is commonly used in 
databases and filesystems.

#### BST 

##### Usage 
- To quickly inserting in a sorted list of values.
  Consider using an array for this purpose. You have very fast access to read random values, but if you want to add a new value, 
  you have to find the place in the array where it belongs, shift everything over, and then insert the new value.
  With a binary search tree, you simply traverse the tree looking for where the value would be if it were in the tree already, 
  and then add it there. 

- It's easy to extend a Bst to efficiently record additional information or perform new operations. For example, one can record 
  the number of nodes in each subtree having a certain property.

#### Self-balancing binary search tree
 
##### AVL Tree 
- is a self-balancing binary search tree in which the heights of the two child subtrees of any node differ by at most one; if at any time they differ by more 
  than one, rebalancing is done to restore this property. Lookup, insertion, and deletion all take O(log n) time in both the average and worst cases, 
  where n is the number of nodes in the tree prior to the operation.

- is a binary search tree that is height balanced: for each node x, the heights of the left and right subtrees of x differ by at most 1. To 
  implement an AVL tree, we maintain an extra attribute in each node: x:h is the height of node x. 

##### Treap 
- A treap is a binary search tree with a modified way of ordering the nodes. 
- The nodes of the treap are ordered so that the keys obey the binary-searchtree property and the priorities obey the min-heap order property:
   - If v is a left child of u, then v.key < u.key.
   - If v is a right child of u, then v.key > u.key.
   - If v is a child of u, then v.priority > u:priority.
(This combination of properties is why the tree is called a "treap": it has features of both a binary search tree and a heap.) 


##### Red Black Tree
- is a kind of self-balancing binary search tree. Each node of the binary tree has an extra bit, and that bit is often interpreted as the color (red or black) 
  of the node. These color bits are used to ensure the tree remains approximately balanced during insertions and deletions. 

##### 2-3 Tree

##### Splay Tree 
 
##### AA Tree

-------

#### Multiway Trees 

#### Space-partitioning trees

#### Application-specific trees 


#### Tango tree

#### Rope data structure
- a data structure composed of smaller strings that is used to efficiently store and manipulate a very long string 
- Ropes can be viewed as search trees that are indexed by position. If each vertex contains the length of the string 
  represented by the subtree, then minimal modifications of the search tree algorithms yields these operations on ropes:
  1. Fetch ith character. A simple search tree look-up. Rather than examining the subtree containing the right key, we 
     examine the tree containing the proper position, as determined by the length fields.
  2. Concatenate two ropes.
  3. Substring. Two search tree split operations.
  4. Iterate over each character. Left-to-right tree traversal. 
- A rope is essentially a binary tree whose leaves are arrays characters, Concatenation of two ropes is just the creation 
 of a new tree node with both ropes as children, So rope enables much faster concatenation than ordinary strings and don't require 
 a large contiguous memory space to store a large string, the main disadventage is slower indexing.
 
#### SkipList
- Skip lists are a probabilistic data structure that seem likely to supplant balanced trees as the implementation method of choice 
 for many applications. Skip list algorithms have the same asymptotic expected time bounds as balanced trees and are simpler, 
 faster and use less space.

- Skip lists are a probabilistic alternative to balanced trees. Skip lists are balanced by consulting a random number generator.
  Although skip lists have bad worst-case performance, no input sequence consistently produces the worst-case performance
  (much like quicksort when the pivot element is chosen randomly). It is very unlikely a skip list data structure will
  be significantly unbalanced (e.g., for a dictionary of more than 250 elements, the chance that a search will take more
  than 3 times the expected time is less than one in a million). 

- a data structure that allows fast search within an ordered sequence of elements. Fast search is made possible by 
  maintaining a linked hierarchy of subsequences, with each successive subsequence skipping over fewer elements than 
  the previous one.
- A skip list is built in layers. The bottom layer is an ordinary ordered linked list. Each higher layer acts as an
  "express lane" for the lists below, where an element in layer i appears in layer i+1 with some fixed probability p 
  (two commonly used values for p are 1/2 or 1/4). On average, each element appears in 1/(1-p) lists, and the tallest 
  element (usually a special head element at the front of the skip list) in all the lists. 

- Search: A search for a target element begins at the head element in the top list, and proceeds horizontally until 
 the current element is greater than or equal to the target. If the current element is equal to the target, it has been found. 
 If the current element is greater than the target, or the search reaches the end of the linked list, the procedure is repeated 
 after returning to the previous element and dropping down vertically to the next lower list. b

- Example usage :
  - Skiplist is used in Redis to implement a "sorted set" data type. 
  
- Balanced treess (e.g., AVL trees [Knu73] [Wir76]) and selfadjusting trees can be used for the same problems as
  skip lists. All three techniques have performance bounds of the same order.
  
- An intersting thing to do to apply the idea of probabilistic balancing to some other problems arising both in data 
  structures and in incremental computation.
  
- From a theoretical point of view, there is no need for skip lists. Balanced trees can do everything that can be done with
  skip lists and have good worst-case time bounds (unlike skip lists). However, implementing balanced trees is an exacting
  task and as a result balanced tree algorithms are rarely implemented, Skip lists are a simple data structure that can be used in
  place of balanced trees for most applications. Skip lists algorithms are very easy to implement and are  as fast as highly optimized 
  balanced tree algorithms.


##### Indexable Skiplist 

### Hashes

### Graphs 

### Succint Data Structures

### Data structures for Integer sorting

#### Van Emde Boas Tree

#### Y-fast Trie

#### Bucket Queue

## Time Complexity 

### Polynomial time 
* An algorithm runs in polynomial time if its running time is upper bounded by a polynomial expression in the size of the input for the algorithm, 
  : T(n) = O(nk) for some constant k. 
* The selection sort sorting algorithm on n integers performs A. n^2 operations for some constant A. Thus it runs in time O(n^2) and is a polynomial
  time algorithm. 
* Maximum matchings in graphs can be found in polynomial time.

### Permutation algorithms

#### Lexicographic Permutations

##### Next lexicographical permutation algorithm
the basic idea: We need to try and keep the bigger digits to the right as much as possible.
So an algorithm for finding the next permutation in lexicographic ordering:
1 - Find the biggest i such that a[i] < a[i + 1];
2 - Find the biggest j greater than i such that a[j] > a[i];
3 - Swap a[i] and a[j];
4 - Reverse the elements from a[i + 1] to the last element.
If the first step fails (because such index does not exist) the current permutation is the last one.

Example:
The algorithm actually finds the next permutation -- the lexicographically next one. The idea is this: suppose you are given a sequence, say "32541". What is the next permutation?

If you think about it, you'll see that it is "34125". And your thoughts were probably something this: In "32541",

there is no way to keep the "32" fixed and find a later permutation in the "541" part, because that permutation is already the last one for 5,4, and 1 -- it is sorted in decreasing order.
So you'll have to change the "2" to something bigger -- in fact, to the smallest number bigger than it in the "541" part, namely 4.
Now, once you've decided that the permutation will start as "34", the rest of the numbers should be in increasing order, so the answer is "34125".




## Other Algorithms 

### Removing duplicates 
* To remove duplicates while preserving order in Java use LinkedHashSet


### Algorithms that work by building an automata
* Aho-Corasick algorithm uses a DFA in order to search for all the elements of a dictionary in a text in linear time, O(|w|) where w is our text. 
* Levenshtein DFA : we can check if a set of words has a specific maximum limit of the Levenshtein distance from a given word. For this we need to construct the Levenshtein Automaton for a constant k which accepts all strings within k 

### LinkedLists Techniques 

#### Iterate Down a List
```C++
struct node* current = head;
while (current != NULL) {
  count++;
  current = current->next;
}
```
#### Build: At Head With Push() 
```C++
struct node* AddAtHead() {
struct node* head = NULL;
 int i;
 for (i=1; i<6; i++) {
   Push(&head, i);
}
 // head == {5, 4, 3, 2, 1};
 return(head);
}
```

#### Build: With Tail Pointer 
Adding a node at the tail of a list most often involves locating the last node in the list, and then changing its .next field from NULL to point to the new node

#### Build: Special Case + Tail Pointer 
```C++
struct node* BuildWithSpecialCase() {
struct node* head = NULL;
struct node* tail;
 int i;
 // Deal with the head node here, and set the tail pointer
 Push(&head, 1);
 tail = head;
 // Do all the other nodes using 'tail'
 for (i=2; i<6; i++) {
  Push(&(tail->next), i); // add node at tail->next
  tail = tail->next; // advance tail to point to last node
 }
 return(head); // head == {1, 2, 3, 4, 5};
}
```

#### Build: Temporary Dummy Nod 
```C++
struct node* BuildWithDummyNode() {
struct node dummy; // Dummy node is temporarily the first node
struct node* tail = &dummy; // Start the tail at the dummy.
 // Build the list on dummy.next (aka tail->next)
int i;
 dummy.next = NULL;
 for (i=1; i<6; i++) {
  Push(&(tail->next), i);
  tail = tail->next;
 }
 // The real result list is now in dummy.next
 // dummy.next == {1, 2, 3, 4, 5};
 return(dummy.next);
}
```

#### Cycle Detection 

##### Robert W. Floyd method. 

##### Richard P. Brent method
 

### N-Way Merge

### Triangle Counting in Graphs

- Solution using Adjacency matrix: The (i, j) element in the n'th power of an adjacency matrix A counts the number of paths of length n starting at i and ending at j.
  A triangle is a path of length 3 that starts and ends at the same node. Therefore the i'th diagonal element of the 3rd power of A counts the number of triangles 
  that contain i as one of the nodes.
  Each distinct triangle will be counted twice for each of the three nodes in the graph (once in each direction, clockwise and anticlockwise).
  Therefore the number of distinct triangles is trace(A^3) / 6 

- [Related Paper](http://people.seas.harvard.edu/~babis/int-math-triangles.pdf)
- Example usages : 
    - In Spark: http://note.yuhc.me/2015/03/graphx-triangle-count-label-propagation/  and 
                https://github.com/apache/spark/blob/master/graphx/src/main/scala/org/apache/spark/graphx/lib/TriangleCount.scala 
    - With MapReduce: [Paper on the subject](https://www.cs.utah.edu/~jeffp/teaching/MCMD/S16-MR-triangles.pdf)

### Sliding Window Minimum Algorithm
//TBD
 
### Blogs with problems solved with algorithms
* [Alan's Blog Algorithms Decomplexified](http://decomplexify.blogspot.fr/2014/04/wildcard-match-star-and-qmark-asymmetric.html)
