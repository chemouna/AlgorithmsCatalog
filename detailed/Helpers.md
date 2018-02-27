

# Helpers 

## Compute Presums 

```java
int[] preSums = new int[n + 1];
for (int i = 1; i < preSums.length; i++) {
  preSums[i] = as[i - 1] + preSums[i - 1];
}
```

## Comparing doubles

The rule of thumb is: if the difference is less than EPS, the values are equal.
So, if your formula contains "a < b" (less), then you write "a < b - EPS". And if it contains "a <= b" (less or equal), then you write "a < b + EPS".

```java
int compareDouble(double a, double b){
	if(a < b - EPS)
		return -1;
	if(a > b + EPS)
		return 1;
	return 0;
}
```

