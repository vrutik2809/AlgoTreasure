---
title: "FenwickTree"
category: "data-structures"
displayOrder: -100
version: "v1"
notoc: true
---

## FenwickTree (Binary Indexed Tree)

```java
public class FenwickTree {
    private long fn[];

    public FenwickTree(int n) {
        fn = new long[n + 1];
    }

    public void add(int idx, long val) {
        idx++;
        for (; idx < fn.length;) {
            fn[idx] += val;
            idx += (idx & (-idx));
        }
    }

    public long sum(int idx) {
        idx++;
        long ans = 0;
        for (; idx > 0;) {
            ans += fn[idx];
            idx -= (idx & (-idx));
        }
        return ans;
    }

    public long sum(int l,int r){
        return sum(r) - sum(l - 1);
    }
}
```