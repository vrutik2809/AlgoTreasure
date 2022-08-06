---
title: "Calculate"
category: "algorithms"
displayOrder: -100
version: "v1"
parent: Algorithms/utils-main
notoc: false
---

## Binary Exponentiation
- Time Complexity: *O(log(exp))*
- Space Complexity: *O(1)*

> Java

```java
public static long pow(long base, long exp) {
    long ans = 1;
    for (; exp != 0;) {
        if ((exp & 1) == 1)
            ans *= base;
        base *= base;
        exp = exp >> 1;
    }
    return ans;
}
```

## Binary Exponentiation with modulo
- Time Complexity: *O(log(exp))*
- Space Complexity: *O(1)*

> Java

```java
final int MOD = (int)1e9 + 7; 
public static long powMod(long base, long exp) {
    long ans = 1;
    for (; exp != 0;) {
        if ((exp & 1) == 1) {
            ans *= base;
            ans %= MOD;
        }
        base *= base;
        base %= MOD;
        exp = exp >> 1;
    }
    return ans;
}
```

## Binary Multiplication
- Time Complexity: *O(log(b))*
- Space Complexity: *O(1)*

> Java

```java
public static long mul(long a, long b) {
    long ans = 0;
    for (; b != 0;) {
        if ((b & 1) == 1) {
            ans += a;
        }
        a += a;
        b >>= 1;
    }
    return ans;
}
```

## Binary Multiplication with modulo
- Time Complexity: *O(log(b))*
- Space Complexity: *O(1)*

> Java

```java
final int MOD = (int)1e9 + 7; 
public static long mulMod(long a, long b) {
    long ans = 0;
    for (; b != 0;) {
        if ((b & 1) == 1) {
            ans += a;
            ans %= MOD;
        }
        a += a;
        a %= MOD;
        b >>= 1;
    }
    return ans;
}
```

## Big Addition
- Time Complexity: *O(max(num1.length,num2.length))*
- Space Complexity: *O(max(num1.length,num2.length) + 1)*

> Java

```java
public static String bigAddition(String num1, String num2,int r) {
    StringBuilder s = new StringBuilder();
    int c = 0,sum = 0;
    for(int i = num1.length() - 1,j = num2.length() - 1;i >= 0 || j >= 0;i--,j--){
        sum = c;
        if(i >= 0) sum += num1.charAt(i) - '0';
        if(j >= 0) sum += num2.charAt(j) - '0';
        s.append(sum % r);
        c = sum / r;
    }
    if(c != 0) s.append(c);
    return s.reverse().toString();
}
```

## Prime Sieve
Find all prime numbers less than or equals to N
- Time Complexity: *O(N * log(log(N)))*
- Space Complexity: *O(N)*

> Java
```java
public static void primeSieve(int n) {
    int arr[] = new int[n + 1];
    Arrays.fill(arr, 1);
    arr[0] = arr[1] = 0;
    for (int i = 2; i < arr.length; i++) {
        if (arr[i] == 1) {
            for (int j = i * i; j < arr.length; j += i) {
                arr[j] = 0;
            }
        }
    }
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == 1)
            System.out.print(i + " ");
    }
}
```

## Prime Factor
Find all prime factors of N
- Time Complexity: *O(sqrt(N))*
- Space Complexity: *O(1)*

> Java
```java
public static void primeFactor(long n) {
    if (n == 0 || n == 1) {
        System.out.println(n);
        return;
    }
    for (long i = 2; i * i <= n; i++) {
        for (; n % i == 0;) {
            System.out.print(i + " ");
            n /= i;
        }
    }
    if (n != 1) {
        System.out.print(n + "\n");
    }
}
```

## Prime Factor Sieve
Find all prime factors less than or equals to N
- Time Complexity: *O(N * log(log(N)))*
- Space Complexity: *O(N)*

> Java
```java
public static void primeFactorSieve(int n) {
    int arr[] = new int[n + 1];
    Arrays.fill(arr, n + 1);
    arr[0] = arr[1] = 1;
    for (int i = 2; i < arr.length; i++) {
        if (arr[i] == n + 1) {
            arr[i] = i;
            for (int j = i * i; j < arr.length; j += i) {
                arr[j] = Math.min(arr[j], i);
            }
        }
    }
    for (int i = 1; i < arr.length; i++) {
        int t = i;
        for (; t != 1;) {
            System.out.print(arr[t] + " ");
            t /= arr[t];
        }
        System.out.println();
    }
}
```