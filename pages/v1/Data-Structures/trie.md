---
title: "Trie"
category: "data-structures"
displayOrder: -100
version: "v1"
notoc: true
---

## Trie

```java
public class Trie {
    private Trie hash[];
    private int endsWith;
    private int prefixCount;

    public Trie() {
        hash = new Trie[26];
        endsWith = prefixCount = 0;
    }

    public void insert(String word) {
        int n = word.length();
        Trie curr = this;
        for (int i = 0; i < n; i++) {
            int c = word.charAt(i) - 'a';
            if (curr.hash[c] == null) {
                curr.hash[c] = new Trie();
            }
            curr = curr.hash[c];
            curr.prefixCount++;
            if (i == n - 1)
                curr.endsWith++;
        }
    }

    public int countWord(String word) {
        int n = word.length();
        Trie curr = this;
        for (int i = 0; i < n; i++) {
            int c = word.charAt(i) - 'a';
            if (curr.hash[c] == null)
                return 0;
            curr = curr.hash[c];
            if (i == n - 1)
                return curr.endsWith;
        }
        return -1;
    }

    public int countPrefix(String prefix) {
        int n = prefix.length();
        Trie curr = this;
        for (int i = 0; i < n; i++) {
            int c = prefix.charAt(i) - 'a';
            if (curr.hash[c] == null)
                return 0;
            curr = curr.hash[c];
            if (i == n - 1)
                return curr != null ? curr.prefixCount : 0;
        }
        return -1;
    }

    public void erase(String word) {
        int n = word.length();
        Trie curr = this;
        for (int i = 0; i < n; i++) {
            int c = word.charAt(i) - 'a';
            if (curr.hash[c] == null)
                return;
            curr = curr.hash[c];
            curr.prefixCount--;
            if (i == n - 1) {
                curr.endsWith--;
                if (curr.prefixCount == 0)
                    curr = null;
            }
        }
    }

    public boolean search(String word) {
        return countWord(word) > 0 ? true : false;
    }

    public boolean startsWith(String prefix) {
        return countPrefix(prefix) > 0 ? true : false;
    }

}
```