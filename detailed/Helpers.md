

# Helpers 

## Compute Presums 

```java
int[] preSums = new int[n + 1];
for (int i = 1; i < preSums.length; i++) {
  preSums[i] = as[i - 1] + preSums[i - 1];
}
```
