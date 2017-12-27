
# Primes 

## Prime number
A natural number is a prime number if it has exactly two positive divisors, 1 and the number itself. 

## Composite number
A natural number greater than 1 that is not a prime number is called a composite number.

### Prime Factorization 

#### Prime Factorization Algorithms

## Coprime numbers
Coprime numbers are a set of integers that have no common divisor other than 1 or -1.
 
## The fundamental theorem of arithmetic
every integer larger than 1 can be written as a product of one or more primes in a way that is unique except for the order of the prime factors.
Primes can thus be considered the “basic building blocks” of the natural numbers

## Euclid’s theorem

## Dirichlet’s theorem

## Primality Tests

### Miller–Rabin Primality Test

```python
def is_primer_miller_rabin(n, k=10):
    """
    Miller-Rabin primality test.

    A return value of False means n is certainly not prime. A return value of
    True means n is very likely a prime.
    """
    if n == 2:
        return True
    if not n & 1:
        return False

    def check(a, s, d, n):
        x = pow(a, d, n)
        if x == 1:
            return True
        for i in xrange(s - 1):
            if x == n - 1:
                return True
            x = pow(x, 2, n)
        return x == n - 1

    s = 0
    d = n - 1

    while d % 2 == 0:
        d >>= 1
        s += 1

    for i in xrange(k):
        a = random.randrange(2, n - 1)
        if not check(a, s, d, n):
            return False
    return True
```


### AKS Primality Test

### Fermat Primality Test

#### Fermat’s little theorem 
 if p is a prime number and a is a positive integer less than p, then
```
ap = a ( mod p )
```
or alternatively:
```
a(p-1) = 1 ( mod p )
```


### Sieves

#### Sieve of Eratosthenes

#### Sieve of Atkin

## Segmented Sieve

## Goldbach’s Conjecture
 
## Euler’s totient function

## Number of prime numbers below a given number
 
## Pollard’s rho algorithm



