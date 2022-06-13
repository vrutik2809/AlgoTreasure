---
title: "Discrete"
category: "algorithms"
displayOrder: -100
version: "v1"
notoc: false
---

## Binary Search

#### Using Loop
- Time Complexity: *O(log(N))*
- Space Complexity: *O(1)*

> Java

```java
public static int binarySearch(int arr[],int l,int r,int target){
    for(;l <= r;){
        int mid = (l + r) / 2;
        if(arr[mid] == target) return mid;
        if(target < arr[mid]) r = mid - 1;
        else l = mid + 1;
    }
    return -1;
}
```
#### Using Recursion
- Time Complexity: *O(log(N))*
- Space Complexity: *O(1)*

> Java

```java
public static int binarySearch(int arr[],int l,int r, int x) {
    if (l <= r) {
        int mid = (l + r) / 2;

        if (arr[mid] == x)
            return mid;

        if (arr[mid] > x)
            return binarySearch(arr, l, mid - 1, x);

        return binarySearch(arr, mid + 1, r, x);
    }
    return -1;
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