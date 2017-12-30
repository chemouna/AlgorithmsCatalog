

# Dynamic Programming 


## Bitmasking 

* To check whether the jth object is in the subset (check whether jth bit is 1):
   use the bitwise AND operation T = A & (1 << j).
   If T = 0, then the j-th item of the set is off.
   If T != 0 (to be precise, T = (1 << j)), then the j-th item of the set is on.

``` 
 For example:    A = 42 (base 10) = 101010 (base 2)
                 j = 3, 1 << j    = 001000 <- bit ‘1’ is shifted to the left 3 times
                                    -------- AND (only true if both bits are true)
                 T = 8 (base 10)  = 001000 (base 2) -> not zero, the 3rd item is on
```

* To iterate through all subsets of a set of size n:
```c++
   for ( x = 0; x < (1 << n); ++x )
```

* Checks whether bit i is on in x. Or in terms of set theory, if i is included in the set x:
```
  ((x) >> (i) ) & 1)
```

* Sets the bit i in bitmask x to 0. Or in terms of set theory, set x without i:
```
  x & ~(1 << i)
```

##  Resource 
* [Codeforces BITMASKS — FOR BEGINNERS](http://codeforces.com/blog/entry/18169)
