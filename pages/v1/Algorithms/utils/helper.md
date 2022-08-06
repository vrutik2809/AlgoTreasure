---
title: "Helper"
category: "algorithms"
displayOrder: -100
version: "v1"
parent: Algorithms/utils-main
notoc: false
---

## Check for prime number
- Time Complexity: *O(sqrt(N))*
- Space Complexity: *O(1)*

> Java

```java
public static boolean isPrime(int num) {
    if(num == 1) return false;
    for (int i = 2; i * i <= num; i++) {
        if (num % i == 0) return false;
    }
    return true;
}
```

## Maximum of an array
- Time Complexity: *O(N)*
- Space Complexity: *O(1)*

> Java

```java
public static int max(int arr[]) {
    int max = Integer.MIN_VALUE;
    for (int i = 0; i < arr.length; i++) {
        max = Math.max(max, arr[i]);
    }
    return max;
}
```

## Minimum of an array
- Time Complexity: *O(N)*
- Space Complexity: *O(1)*

> Java

```java
public static int min(int arr[]) {
    int min = Integer.MAX_VALUE;
    for (int i = 0; i < arr.length; i++) {
        min = Math.min(min, arr[i]);
    }
    return min;
}
```

## Reverse an array
- Time Complexity: *O(N/2)*
- Space Complexity: *O(1)*

> Java

```java
public static void reverse(int arr[]) {
    for (int i = 0, j = arr.length - 1; i < j; i++, j--) {
        int t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
    }
}
```