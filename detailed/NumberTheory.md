
# Number Theory Problems 

## Finding the Last Digit of a Power

 
### Methods 

#### Using Modular Arithmetic
- Finding the last digit of a positive integer is the same as finding the remainder of that number when divided by n. 
- In general, the last digit of a power in base n is its remainder upon division by n 
  finding the last n digits amounts to computation mod 10^n. 
- Every digit 0 thru 9 has a pattern of 4 digits when raised to an exponential power. 
  Simply divide the power by 4 and the remainder shows you where you are at in the pattern. 
  Here are the patterns for all 10 digits :
{ 0,0,0,0, 1,1,1,1, 6,2,4,8, 1,3,9,7, 6,4,6,4, 
  5,5,5,5, 6,6,6,6, 1,7,9,3, 6,8,4,2, 1,9,1,9 }

(See Proof [here](https://stackoverflow.com/questions/7214419/how-to-find-the-units-digit-of-a-certain-power-in-a-simplest-way))

### Using Chinese Remainder Theorem
- find a number mod 5^n and mod 2^n and then combine those results, using the Chinese remainder theorem, to find that number mod 10^n.

### Using Euler's Theorem 
- Large exponents can be reduced by using Euler's theorem: if gcd(a,n) = 1 and Phi(n) denotes Euler's totient function, then
    a^phi(n) = 1 (mod n)
  
### Using Binomial Expansion


### Repeated Squaring for Exponentiation
 
 
 
 
 

