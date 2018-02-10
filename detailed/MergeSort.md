
# Merge Sort


## Algorithm
Conceptually, a merge sort works as follows:
- Divide the unsorted list into n sublists, each containing 1 element (a list of 1 element is considered sorted).
- Repeatedly merge sublists to produce new sorted sublists until there is only 1 sublist remaining. This will be the sorted list


## Q/A

* Q: Is quicksort better than mergesort?
  A: Merge sort complexity is O(n log n) on both the average and worst case 
     Quick sort complexity is O(n log n) on the average case and O(n^2) in the worst case 
     - the often-quoted runtime of sorting algorithms refers to the number of comparisons or the number of swaps necessary to perform to sort the data. This is indeed a good measure of performance, 
      especially since it’s independent of the underlying hardware design. However, other things – such as locality of reference (i.e. do we read lots of elements which are probably in cache?) 
      also play an important role on current hardware. Quicksort in particular requires little additional space and exhibits good cache locality, and this makes it faster than merge sort in many cases.

    - What makes Quicksort better on average is that the inner loop implies comparing several values with a single one, while on the other two both terms are different for each comparison. In other words, 
      Quicksort does half as many reads as the other two algorithms. On modern CPUs performance is heavily dominated by access times, so in the end Quicksort ends up being a great first choice.

    - quicksort changes the array inplace - in the array it is working on [unlike merge sort, for instance - which creates a different array for it]. Thus, it applies the principle of locality of reference.
      Cache benefits from multiple accesses to the same place in the memory, since only the first access needs to be actually taken from the memory - the rest of the accesses are taken from cache, 
      which is much faster the access to memory.
      Merge sort for instance - needs much more memory [RAM] accesses - since every accessory array you create - is accessing the RAM again.

   - quicksort has a degenerate O(n2) worst case, there are many ways to avoid this. The introsort algorithm keeps track of the recursion depth and switches the algorithm to heapsort if it looks like the quicksort will degenerate. 
      This guarantees O(n log n) worst-case behavior with low memory overhead and maximizes the amount of benefit you get from quicksort. Randomized quicksort, while still having an O(n2) worst case, has a vanishingly small probability 
      of actually hitting that worst case.
   
   - Mergesort does need a lot of auxiliary memory, which is one reason why you might not want to use it if you have a huge amount of data to sort. It's worth knowing about, though, since its variants are widely used.
     
In addition, it’s very easy to avoid quicksort’s worst-case run time of O(n2) almost entirely by using an appropriate choice of the pivot – such as picking it at random (this is an excellent strategy).

* Q: The point when the time/space complexity for a merge sort would be as good/bad as an insertion sort for given values ? 
  A: 
