# [209. 长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

## 题目

给定一个含有 n 个正整数的数组和一个正整数 target 。

找出该数组中满足其和 ≥ target 的长度最小的 连续子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

 

示例 1：
```
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
```

示例 2：
```
输入：target = 4, nums = [1,4,4]
输出：1
```

示例 3：
```
输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
```

提示：

- `1 <= target <= 109`
- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 105`
 

进阶：
- 如果你已经实现 O(n) 时间复杂度的解法, 请尝试设计一个 `O(n log(n))` 时间复杂度的解法

## 题解

### 解法一 滑动窗口

本题的提示中的时间复杂度 `O(n)` 就有联想，滑动窗口符合。这道题属于滑动窗口中的窗口大小不固定的类型。解法的话，考虑使用双指针的方式来解：


```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int length = nums.length;
        if (length == 0) {
            return 0;
        }
        // 这个变量用于标记一下最大值
        int ans = Integer.MAX_VALUE;
        int sum = 0;
        // 滑动窗口，窗口大小不固定，left = right = 0
        int left = 0;
        for (int right = 0; right < length; right ++) {
            sum += nums[right];
            // 找到满足条件之后，固定 right，增加 left
            while (sum >= target) {
                ans = Math.min(ans, right - left + 1);
                sum -= nums[left];
                left += 1;
            }
            // 不满足条件时，说明固定了 left，准备增加 right
        }
        return ans == Integer.MAX_VALUE ? 0 : ans;
    }
}
```