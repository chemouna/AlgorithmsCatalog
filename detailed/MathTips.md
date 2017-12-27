
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
