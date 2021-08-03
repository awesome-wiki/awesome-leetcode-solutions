# [46 全排列](https://leetcode-cn.com/problems/permutations/)

## 题目

给定一个不含重复数字的数组 nums ，返回其 所有可能的全排列 。你可以 按任意顺序 返回答案。

示例 1：
```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

示例 2：
```
输入：nums = [0,1]
输出：[[0,1],[1,0]]
```

示例 3：
```
输入：nums = [1]
输出：[[1]]
```

提示：
- 1 <= nums.length <= 6
- -10 <= nums[i] <= 10
- nums 中的所有整数 互不相同

## 题解

### 回溯

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, nums, new LinkedList<>());
        return result;
    }

    private void backtrack(List<List<Integer>> result, int[] nums, LinkedList<Integer> s) {
        if (s.size() == nums.length) {
            result.add(new ArrayList<>(s));
            return;
        }
        for (int i=0; i < nums.length; i++) {
            if (!s.contains(nums[i])) {
               s.add(nums[i]);
               backtrack(result, nums, s);
               s.removeLast();
            }

        }
    }
}
```