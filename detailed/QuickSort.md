
# QuickSort 

## Q/A
* Q: When can the worst case for QuickSort occur ?
  A: If the first element is always chosen as the pivot, then an already sorted list is the worst-case. Often there's a high probability that the array is already/nearly sorted, so this implementation is rather poor.
     Analogously, selecting the last element as the pivot is bad for the same reason.
     Some implementations tries to avoid this problem by choosing the middle element as the pivot. This would not perform as badly on already/nearly sorted arrays, but one could still construct an input that would exploit 
     this predictable pivot selection and make it run in quadratic time.


