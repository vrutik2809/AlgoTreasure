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