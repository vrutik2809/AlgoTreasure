---
title: "Dynamic Programming"
category: "algorithms"
displayOrder: -100
version: "v1"
notoc: false
---

## Longest Common Sub-sequence (LCS)
Find the length of the LCS of two string `str1` and `str2`

<details>
<Summary>Using Recursion</Summary>

- Time Complexity: *O(2<sup>n</sup>)*
- Space Complexity: *O(1)*

> Java

```java
public static int lcs(String str1, String str2, int m, int n) {
    if (m == 0 || n == 0)
        return 0;

    if (str1.charAt(m - 1) == str2.charAt(n - 1))
        return 1 + lcs(str1, str2, m - 1, n - 1);

    return Math.max(lcs(str1, str2, m, n - 1), lcs(str1, str2, m - 1, n));
}
```
</details>

<details>
<Summary>Using DP-Memoization</Summary>

- Time Complexity: *O(m * n)*
- Space Complexity: *O(m * n)*

> Java

```java
public static int lcs(String str1, String str2, int m, int n,int dp[][]) {
    if (m == 0 || n == 0)
        return 0;

    if (dp[m][n] != -1)
        return dp[m][n];

    if (str1.charAt(m - 1) == str2.charAt(n - 1))
        return dp[m][n] = 1 + lcs(str1, str2, m - 1, n - 1,dp);

    return dp[m][n] = Math.max(lcs(str1, str2, m, n - 1,dp), lcs(str1, str2, m - 1, n,dp));
}
```
</details>

<details open>
<Summary>Using DP-Tabulation</Summary>

- Time Complexity: *O(m * n)*
- Space Complexity: *O(m * n)*

> Java

```java
public static int lcs(String str1, String str2) {
    int m = str1.length(), n = str2.length();
    int dp[][] = new int[m + 1][n + 1];
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                dp[i][j] = 0;
            else if (str1.charAt(i - 1) == str2.charAt(j - 1))
                dp[i][j] = dp[i - 1][j - 1] + 1;
            else
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
        }
    }
    return dp[m][n];
}
```
</details>

References: [LCS](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)

## Longest Increasing Sub-sequence (LIS)
Find the longest increasing sub-sequence in an integer array `arr`

<details>
<Summary>Using Recursion</Summary>

- Time Complexity: *O(2<sup>n</sup>)*
- Space Complexity: *O(1)*

> Java

```java
public class Solution 
{
    private static int ans;
    private static int helper(int arr[],int n){
        if(n == 0) return 1;
        int meh = 1;
        for(int i = 0;i < n;i++){
            int res = helper(arr,i);
            if(arr[n] > arr[i] && res >= meh) meh = 1 + res;
        }
        ans = Math.max(ans,meh);
        return meh;
    }
    public static int lis(int arr[]){
        ans = 1;
        helper(arr,arr.length - 1);
        return ans;
    }
}
```
</details>

<details>
<Summary>Using DP-Memoization</Summary>

- Time Complexity: *O(n<sup>2</sup>)*
- Space Complexity: *O(n)*

> Java

```java
public class Solution 
{
    private static int ans;
    private static int helper(int arr[],int n,int dp[]){
        if(dp[n] != 1) return dp[n];
        for(int i = 0;i < n;i++){
            int res = helper(arr,i,dp);
            if(arr[n] > arr[i] && res >= dp[n]) dp[n] = 1 + res;
        }
        ans = Math.max(ans,dp[n]);
        return dp[n];
    }
    public static int lis(int arr[]){
        int dp[] = new int[arr.length];
        Arrays.fill(dp,1);
        ans = 1;
        helper(arr,arr.length - 1,dp);
        return ans;
    }
}
```
</details>

<details open>
<Summary>Using DP-Tabulation</Summary>

- Time Complexity: *O(n<sup>2</sup>)*
- Space Complexity: *O(n)*

> Java

```java
public static int lis(int arr[]){
    int dp[] = new int[arr.length];
    Arrays.fill(dp,1);
    int ans = 1;
    for(int i = 1;i < arr.length;i++){
        for(int j = 0;j < i;j++){
            if(arr[i] > arr[j] && dp[j] >= dp[i]) dp[i] = 1 + dp[j];
        }
        ans = Math.max(ans,dp[i]);
    }
    return ans;
}
```
</details>



## 0/1 knapsack

<details>
<Summary>Using Recursion</Summary>

- Time Complexity: *O(2<sup>n</sup>)*
- Space Complexity: *O(1)*

> Java

```java
class Solution 
{ 
    private static int helper(int wt[],int val[],int i,int w){
        if(i == 0){
            if(w - wt[i] >= 0) return val[i];
            else return 0;
        }
        if(w - wt[i] >= 0){
            return Math.max(helper(wt,val,i - 1,w),val[i] + helper(wt,val,i - 1,w - wt[i]));
        }
        else{
            return helper(wt,val,i - 1,w);
        }
    } 
    public static int knapSack(int W, int wt[], int val[], int n) 
    { 
        return helper(wt,val,wt.length - 1,W);
    } 
}
```
</details>

<details>
<Summary>Using DP-Memoization</Summary>

- Time Complexity: *O(n * W)*
- Space Complexity: *O(n * W)*

> Java

```java
class Solution 
{ 
    private static int helper(int wt[],int val[],int i,int w,int dp[][]){
        if(i == 0){
            if(w - wt[i] >= 0) return dp[i][w] = val[i];
            else return dp[i][w] = 0;
        }
        if(dp[i][w] != 0) return dp[i][w];
        if(w - wt[i] >= 0){
            return dp[i][w] = Math.max(helper(wt,val,i - 1,w,dp),val[i] + helper(wt,val,i - 1,w - wt[i],dp));
        }
        else{
            return dp[i][w] = helper(wt,val,i - 1,w,dp);
        }
    } 
    public static int knapSack(int W, int wt[], int val[]) 
    { 
        int dp[][] = new int[wt.length + 1][W + 1];
        return helper(wt,val,wt.length - 1,W,dp);
    } 
}
```
</details>

<details open>
<Summary>Using DP-Tabulation</Summary>

- Time Complexity: *O(n * W)*
- Space Complexity: *O(n * W)*

> Java

```java
public static int knapSack(int wt[], int val[], int W) {
    int dp[][] = new int[wt.length + 1][W + 1];
    for (int i = 1; i <= wt.length; i++) {
        for (int w = 1; w <= W; w++) {
            if (w - wt[i - 1] < 0)
                dp[i][w] = dp[i - 1][w];
            else
                dp[i][w] = Math.max(dp[i - 1][w], val[i - 1] + dp[i - 1][w - wt[i - 1]]);
        }
    }
    return dp[wt.length][W];
}
```
</details>