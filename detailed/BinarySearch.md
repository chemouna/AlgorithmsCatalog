
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
    mid = (lo + hi) / 2.0;
    if(mid is too small) {
       lo = mid; 
    }
    else {
     hi = mid; 
    }
 }
 return hi; 
}
```

## Other Binary Search Recipes 

Problem:

You want to find the smallest x in the given interval [a,b] such that some propety P(x) holds. You know that if P(x) and y>x, 
then also P(y). You also know that P(b) holds. This could be either an interval of integers, or of real numbers.

The most common application of binary search is the following. You have a non-decreasing function f, and a constant C. You have 
to find the smallest x for which f(x) = C (or, if there is none, the smallest x for which f(x) ≥ C). In this case, your property P(x) is "f(x) ≥ C".

Solution:

If [a,b] is an interval of integers:
```java
int l = a, r = b;
while(l < r) {
  int m = (l+r) >> 1; // take the center of the interval
  // replace the interval [a,b] with either [a,m] or [m+1,b],
  // depending on whether P(m) is already satisfied
  if(P(m)) {
    r = m; 
  }
  else {
    l = m+1;
  }
}
x=l
```

If [a,b] is an interval of real numbers:

```java
double l = a, r = b;
for(int iterations=0; iterations<100; iterations++) {
  double m = (a+b)/2;
  if(P(m)) {
    r = m; 
  } else {
    l = m;
  }
}
x=l;
```

Make sure that your binary search works for intervals [a,a+1]—there are two possible answers for this problem, and after one step of binary 
search we should always have an interval [x,x] with a single possible answer. If you change one of the three places "m=(l+r)>>1", "r=m", "l=m+1", 
even by adding or subtracting one to the right side of one of the assignments, the result will probably fail (one of two subintervals is likely 
to be either nonsense [a,a-1], which means that there is an error, or [a,a+1] again, which means that the algorithm loops infinitely).

You need to be careful if you're using negative integers in your range. As written this should work on Java and with most C compilers (>> of a 
negative number is implementation-defined in C99 though). If you replace >> 1 with / 2, it will break, because that will round towards zero instead 
of downwards. Also, you need to be careful about the case when 2*b does not fit into the range of the integer type ((l+r)>>1 will return a wrong
answer in this case, although this can be easily fixed).

Don't forget that the P property must hold for all numbers from certain x. If it does not, but you still know that P(b) holds and P(a-1) does not, 
you will just find some x for which P(x) is satisfied and P(x-1) is not.


## Ternary Search 
Problem:

You have a function f in an interval [a,b] of real numbers, and you want to find the x for which f(x) is maximized. You know that the function f is unimodal: it is strictly increasing in the interval [a,x], and strictly decreasing in the interval [x,b].

Solution:

If we are working with an interval of integers, not an interval of reals, simply use binary search (see "binary search" recipe). (The property P(x) we are working with is the following one: f(x) > f(x+1).)

For reals, use the following algorithm, known as ternary search:
```java
double l = a, r = b;
 
for(int i=0; i<200; i++) {
  double l1 = (l*2+r)/3;
  double l2 = (l+2*r)/3;
  if(f(l1) > f(l2)) {
    r = l2; 
  } 
  else {
    l = l1;
  }
}
x = l;
```
- This works because after each step the interval [a,b] is reduced to 2/3 of its previous size. After 200 steps, we will know the answer up to an error of at most (2/3)^200 of the original interval, 
- Don't forget that ternary search is not the only way of finding the maximum of a function; some basic knowledge of differentiation might also be helpful. In case if f is easily differentiable, 
  you need to find x such that f'(x)=0; for some functions f such x can be calculated easily, without having to go through 200 iterations. For example, we can easily check that the function f(x) = x(1-x)
  reaches its maximum at 1/2. However, you need to be careful about floating point errors and situations where the maximum is reached at the end of the interval.
  
  
