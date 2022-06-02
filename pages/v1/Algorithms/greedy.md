---
title: "Greedy"
category: "algorithms"
displayOrder: -100
version: "v1"
notoc: false
---

# Three sum

### Brute Force
- Time Complexity: O(N^3)
- Space Complexity: O(k) ;k = the number of unique triplets with sum = 0 for the given array

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

### Greedy
- Time Complexity: O(N^2)
- Space Complexity: O(1)

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
