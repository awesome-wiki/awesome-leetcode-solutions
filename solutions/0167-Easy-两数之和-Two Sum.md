
# 两数之和-Two Sum

[力扣](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)
## 题目
给定一个已按照 升序排列  的整数数组 numbers ，请你从数组中找出两个数满足相加之和等于目标数 target 。

函数应该以长度为 2 的整数数组的形式返回这两个数的下标值。numbers 的下标 从 1 开始计数 ，所以答案数组应当满足 1 <= answer[0] < answer[1] <= numbers.length 。

你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

> Given an array of integers numbers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.Return the indices of the two numbers (1-indexed) as an integer array answer of size 2, where 1 <= answer[0] < answer[1] <= numbers.length.You may assume that each input would have exactly one solution and you may not use the same element twice.

示例一：
```
输入：numbers = [2,7,11,15], target = 9
输出：[1,2]
解释：2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 
```

示例二：
```
输入：numbers = [2,3,4], target = 6
输出：[1,3]
```

示例三：
```
输入：numbers = [-1,0], target = -1
输出：[1,2]
```

## 题解

### 双指针

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int low = 0;
        int high = numbers.length - 1;
        while (low < high) {
            int sum = numbers[low] + numbers[high];
            if (sum == target) {
                return new int[]{low + 1, high + 1};
            } else if (sum < target) {
                low ++;
            } else {
                high --;
            }
        }
        return new int[]{-1, -1};
    }
}
```

复杂度分析：
- 时间复杂度：O(n)，其中 nn 是数组的长度。两个指针移动的总次数最多为 nn 次。
- 空间复杂度：O(1)