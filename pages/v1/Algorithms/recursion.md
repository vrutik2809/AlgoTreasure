---
title: "Recursion"
category: "algorithms"
displayOrder: -100
version: "v1"
notoc: false
---

## Tower of Hanoi
- Time Complexity:
- Space Complexity:

> Java

```java
public static void towerOFHanoi(int n, char src, char dest, char help) {
    if (n == 0) {
        return;
    }
    towerOFHanoi(n - 1, src, help, dest);
    System.out.println("Move from " + src + " to " + dest);
    towerOFHanoi(n - 1, help, dest, src);
}
```

## All Substring
- Time Complexity:
- Space Complexity:

> Java

```java
public static void allSubString(String ans, String str) {
    if (str.length() == 0) {
        System.out.println(ans);
        return;
    }
    allSubString(ans, str.substring(1));
    allSubString(ans + str.charAt(0), str.substring(1));
}
```