---
title: "Greedy"
category: "algorithms"
displayOrder: -100
version: "v1"
notoc: false
---

## Three sum

#### Brute Force
- Time Complexity: *O(N^3)*
- Space Complexity: *O(k) ;k = the number of unique triplets with sum = 0 for the given array*

> Java

```java
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> ans = new ArrayList<>();
    for(int i = 0;i < nums.length - 2;i++){
        for (int j = i + 1; j < nums.length; j++) {
            for (int k = j + 1; k < nums.length; k++) {
                if (nums[i] + nums[j] + nums[k] == 0) {
                    List<Integer> triplet = new ArrayList<>();
                    triplet.add(nums[i]);
                    triplet.add(nums[j]);
                    triplet.add(nums[k]);
                    Collections.sort(triplet);
                    ans.add(triplet);
                }
            }
        }
    }
    ans = new ArrayList<List<Integer>>(new LinkedHashSet<List<Integer>>(ans));
    return ans;
}
```
#### Greedy
- Time Complexity: *O(N^2)*
- Space Complexity: *O(1)*

> Java

```java
public List<List<Integer>> threeSum(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> ans = new ArrayList<>();
    for(int i = 0;i < nums.length - 2;i++){
        if(i > 0 && nums[i] == nums[i - 1]){
            continue;
        }
        for(int j = i + 1,k = nums.length - 1;j < k;){
            int sum = nums[i] + nums[j] + nums[k];
            if(sum == 0){
                ans.add(Arrays.asList(nums[i],nums[j],nums[k]));
                k--;
                while(j < k && nums[k] == nums[k + 1]) k--;
            }
            else if(sum < 0) j++;
            else k--;
        }
    }
    return ans;
}
```
References: 

## Kadane's Algorithm
- Time Complexity: *O(N)*
- Space Complexity: *O(1)*

> Java

```java
public static int maxSubArray(int arr[]){
    int meh = 0;
    int msf = Integer.MIN_VALUE;
    for(int v:arr){
        meh += v;
        meh = Math.max(meh, v);
        msf = Math.max(msf,meh);
    }
    return msf;
}
```

## Sub-sequence
Check whether `str1` is subsequence of `str2` or not
#### Using Loop
- Time Complexity: *O(str2.length)*
- Space Complexity: *O(1)*

> Java

```java
public static boolean isSubsequence(String str1,String str2){
    int n = str1.length(), m = str2.length();
    int i = 0;
    for(int j = 0;i < n && j < m;j++){
        if(str1.charAt(i) == str2.charAt(j)) ++i;
    }
    return i == n;
}
```

#### Using Recursion (uses stack memory)
- Time Complexity: *O(n)*
- Space Complexity: *O(1)*

> Java

```java
public static boolean isSubsequence(String str1, String str2,int m, int n){
    if (m == 0)
        return true;
    if (n == 0)
        return false;

    if (str1.charAt(m - 1) == str2.charAt(n - 1))
        return isSubsequence(str1, str2, m - 1, n - 1);

    return isSubsequence(str1, str2, m, n - 1);
}
```
References: [Check-for-Subsequence](https://www.geeksforgeeks.org/given-two-strings-find-first-string-subsequence-second/)