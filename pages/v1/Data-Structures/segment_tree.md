---
title: "SegmentTree"
category: "data-structures"
displayOrder: -100
version: "v1"
notoc: true
---

## SegmentTree

```java
class SegmentTree {
    private long seg[];
    private int n;

    public SegmentTree(long arr[]) {
        this.n = arr.length;
        seg = new long[4 * n];
        build(0, n - 1, 0, arr);
    }

    private void build(int start, int end, int node, long arr[]) {
        if (start == end) {
            seg[node] = arr[start];
            return;
        }
        int mid = (start + end) / 2;
        build(start, mid, 2 * node + 1, arr);
        build(mid + 1, end, 2 * node + 2, arr);
        seg[node] = seg[2 * node + 1] + seg[2 * node + 2];
    }

    private long query(int start, int end, int l, int r, int node) {
        if (start > r || end < l) {
            return 0;
        }

        if (start >= l && end <= r) {
            return seg[node];
        }

        int mid = (start + end) / 2;
        long left_ans = query(start, mid, l, r, 2 * node + 1);
        long right_ans = query(mid + 1, end, l, r, 2 * node + 2);
        return left_ans + right_ans;
    }

    public long query(int l, int r) {
        return query(0, n - 1, l, r, 0);
    }

    private void update(int start, int end, int node, int idx, long val) {
        if (start == end) {
            seg[node] = val;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid)
            update(start, mid, 2 * node + 1, idx, val);
        else
            update(mid + 1, end, 2 * node + 2, idx, val);

        seg[node] = seg[2 * node + 1] + seg[2 * node + 2];

    }

    public void update(int idx, long val) {
        update(0, n - 1, 0, idx, val);
    }
}
```