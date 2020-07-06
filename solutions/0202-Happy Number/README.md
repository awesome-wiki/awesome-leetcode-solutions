# [202-Happy Number/快乐数](https://leetcode-cn.com/problems/happy-number)

## Problems

### CN

编写一个算法来判断一个数 n 是不是快乐数。

「快乐数」定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。如果 可以变为  1，那么这个数就是快乐数。

如果 n 是快乐数就返回 True ；不是，则返回 False 。

 

示例：
```
输入：19
输出：true
解释：
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

### EN

Write an algorithm to determine if a number n is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Return True if n is a happy number, and False if not.

Example: 
```
Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

## 解法

官方题解：[leetcode-cn/快乐数](https://leetcode-cn.com/problems/happy-number/solution/kuai-le-shu-by-leetcode-solution/) 有视频讲解

### 解法一：用 HashSet 检测循环

思路：找出过程中重复的数字避免进入无限循环

> 找出重复数字，就是解决题目的关键。

Java：

```java
class Solution {
    // 计算整数 n 各位置的平方和
    private int getNext(int n) {
        int totalSum = 0;
        while (n > 0) {
            // 数位分离，不断除以 10 取余
            int d = n % 10;
            n = n / 10;
            totalSum += d * d;
        }
        return totalSum;
    }

    public boolean isHappy(int n) {
        // 通过集合存储已经出现过的数字
        Set<Integer> seen = new HashSet<>();
        // 如果 n 不唯一的情况，集合中还未出现数字，就将该数字加入集合中，否则就跳出循环
        while (n != 1 && !seen.contains(n)) {
            seen.add(n);
            // 下一个数字赋值给 n
            n = getNext(n);
        }
        // 判断跳出循环后，n 是否为 1，如果不为 1，表示集合中出现了可以进入无限循环的数字
        return n == 1;
    }
}
```