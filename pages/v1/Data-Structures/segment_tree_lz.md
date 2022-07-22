---
title: "SegmentTree with Lazy Propagation"
category: "data-structures"
displayOrder: -100
version: "v1"
notoc: true
---

```java
class SegmentTree2 {
    private long seg[];
    private int n;
    private long lazy[];

    public SegmentTree2(int arr[]) {
        this.n = arr.length;
        seg = new long[4 * n];
        lazy = new long[4 * n];
        build(0, n - 1, 0, arr);
    }

    private void build(int start, int end, int node, int arr[]) {
        if (start == end) {
            seg[node] = arr[start];
            return;
        }
        int mid = (start + end) / 2;
        build(start, mid, 2 * node + 1, arr);
        build(mid + 1, end, 2 * node + 2, arr);
        seg[node] = seg[2 * node + 1] + seg[2 * node + 2]; // depends on the operation
    }

    private long query(int start, int end, int l, int r, int node) {
        if (start > r || end < l) {
            return 0; // depends on the operation
        }

        // lazy propagation
        if (lazy[node] != 0) {
            seg[node] += lazy[node] * (end - start + 1);
            if (start != end) {
                lazy[2 * node + 1] += lazy[node];
                lazy[2 * node + 2] += lazy[node];
            }
            lazy[node] = 0;
        }

        if (start >= l && end <= r) {
            return seg[node];
        }

        int mid = (start + end) / 2;
        long left_ans = query(start, mid, l, r, 2 * node + 1);
        long right_ans = query(mid + 1, end, l, r, 2 * node + 2);
        return left_ans + right_ans; // depends on the operation
    }

    public long query(int l, int r) {
        return query(0, n - 1, l, r, 0);
    }

    private void update(int start, int end, int node, int l, int r, long val) {
        if (start > r || end < l) {
            return;
        }

        // lazy propagation
        if (start >= l && end <= r) {
            seg[node] += val * (end - start + 1);
            if (start != end) {
                lazy[2 * node + 1] += val;
                lazy[2 * node + 2] += val;
            }
            return;
        }
        int mid = (start + end) / 2;
        update(start, mid, 2 * node + 1, l, r, val);
        update(mid + 1, end, 2 * node + 2, l, r, val);

        seg[node] = seg[2 * node + 1] + seg[2 * node + 2]; // depends on the operation

    }

    public void update(int l, int r, long val) {
        update(0, n - 1, 0, l, r, val);
    }
}
```