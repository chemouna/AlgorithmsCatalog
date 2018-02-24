
# Intervals Overlap

- Throw the endpoints of the intervals into an array, marking them as either start- or end-points. 
   Sort them by breaking ties by placing end-points before start-points if the intervals are closed, or the other way around if they're half-open.

    1S, 2S, 3E, 4E, 5S, 10E, 12S, 13S, 14E, 15E
   Then iterate through the list, keeping track of how many intervals we're in (this equates to number of start-points processed minus number of end-points). 
   Whenever we hit a start-point while we are already in an interval, this means we must have overlapping intervals.

    1S, 2S, 3E, 4E, 5S, 10E, 12S, 13S, 14E, 15E
         ^                          ^
       overlap                    overlap
   We can find which intervals overlap with which by storing data alongside the end-points, and keeping track of which intervals we're in. 



## Interesting variants

- Suppose I have a set of intervals and for any given interval I want to know how many intervals in my set are fully contained in it ?

If you sort all intervals in the set according to their right ends the problem is easily transformed into a well-known problem "How many elements from l to r have their values  ≥ x".

after sorting by minimum left end. Now for a query [L, R] we want to know how many intervals from those whose left end equals L to those whose left end equals R, has a right end ≤ R. 
This can be done in  by sqrt decomposition, decompose the intervals into buckets after sorting them by left end, and then sort every bucket by its right end. Then each query can be done 
by binary search in every candidate bucket.


## Sources 
- [Checking for interval overlap](https://fgiesen.wordpress.com/2011/10/16/checking-for-interval-overlap/)

