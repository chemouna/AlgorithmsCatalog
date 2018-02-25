
# Binary Search 

- it seems there are two generalisations for binary search : one is for monotonic functions and the other is more general by having a predicate that fullfils a requirement 
  (more details [here](https://www.topcoder.com/community/data-science/data-science-tutorials/binary-search/))

- we can apply binary search to any monotonically increasing sequence or abstract function.
- Let a function f(x) return true or false according to a specific criteria. If for all values of f(x) <= f(x+1) then we can use binary search to 
  find the smallest spot in which the value changes from false to true in O(log n) time. 

while (hi > lo + 1) {
   long long mid = (lo + hi) / 2;
   if (func(mid)) {
      hi = mid;
   } else {
      lo = mid;
   }
}

[For an example check here](http://wilanw.blogspot.fr/2009/08/binary-search-algorithm.html)

## Binary Search on Reals 

```
int binarySearch() {
  // want: lo is always <x, and hi always >=x
  double lo, hi, mi; lo=a; hi=b;
  while(lo + EPS < hi) {
    // you need to decide what is the right EPS, 1e-9? 
    mid=(lo + hi) / 2.0;
    if(mid is too small) {
       lo=mid; 
    }
    else {
     hi=mid; 
    }
 }
 return hi; 
}
```

