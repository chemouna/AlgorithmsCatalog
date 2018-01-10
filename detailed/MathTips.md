
# Math Tips for Algorithms and Competitive Programming

## Divisibility Criteria 
Divisibility criteria are ways of telling whether one number divides another without actually carrying the division through. 

To fix the notation, A will be the number whose divisibility by another number d we are going to investigate. In the decimal system,
```
A = 10^n . a(n) + 10^(n−1) . a(n−1) +...+ 10^1 . a(1) + a(0)
```
a(n)≠0
```
s+(A)=a(n) + a(n−1) +...+ a(0)
s±(A) = a(0) − a(1) +…+ (−1)^n . a(n)
```

Divisibility by 3: A is divisible by 3 iff s+(A) is divisible by 3.

Divisibility by 9: A is divisible by 9 iff s+(A) is divisible by 9.

Divisibility by 11: A is divisible by 11 iff s±(A) is.

A function f(A) = f(a(n), …, a(0) is called a divisibility criterion by an integer d provided, starting with some A, |f(A)| < A and A is divisible by d iff f(A) is divisible by d.
O(d): the set of all divisibility criteria by d.
```
f7(A)=(a(2) . a(1) . a(0)) base10 − (a(5) . a(4) . a(3)) base10 + (a(8) . a(7) . a(6)) base10 −...∈ O(1001)
```
in some cases this rule helps, for example: 2,003,008 is divisible by 7 for so is (008) − (003) +2 = 7.

## Repeated Squaring
Repeated squaring, or repeated doubling is an algorithm that computes integer powers of a number quickly. The general problem is to compute x^{y} for an arbitrary integer y. 
The naive method, doing y multiplications of x, is very slow. It can be sped up by repeatedly squaring x until the current power of x exceeds y.

```
// Calculates n to the p power, where p is a positive number.
func power(var n as integer, var p as integer)
   if p = 0 return 1
   if p = 1 return n
   if p is odd
      return n * power( n * n, (p-1) / 2 )
   else
      return power( n * n, p / 2 )
end 
```

there's this also this useful relation for modular arithmetic:
```
(x * y) mod m = ((x mod m) * (y mod m)) mod m
``` 

## Euclid Algorithm

### Euclidean division
Euclidean division is the process of division of two integers, which produces a quotient and a remainder.


### Modular multiplicative inverse

