---
title: "Disjoint Set Union"
category: "data-structures"
displayOrder: -100
version: "v1"
notoc: true
---

```java
public class DSU {
    public int par[];
    private long size[];

    public DSU(int n) {
        par = new int[n];
        size = new long[n];
        for (int i = 0; i < n; i++) {
            par[i] = i;
            size[i] = 1;
        }
    }

    public int get(int c) {
        if (c == par[c])
            return c;
        return par[c] = get(par[c]);
    }

    public void union(int x, int y) {
        x = get(x);
        y = get(y);
        if (x != y) {
            if (size[x] < size[y]) {
                int t = x;
                x = y;
                y = t;
            }
            par[y] = x;
            size[x] += size[y];
        }
    }
}
```