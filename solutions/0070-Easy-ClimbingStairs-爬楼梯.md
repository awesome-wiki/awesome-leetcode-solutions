# 70-ClimbingStairs-爬楼梯

[力扣](https://leetcode-cn.com/problems/climbing-stairs/)
## 问题

[70-爬楼梯/Climbing Stairs](https://leetcode-cn.com/problems/climbing-stairs/)

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

> You are climbing a stair case. It takes n steps to reach to the top.Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

注意：给定 n 是一个正整数。

示例 1：
```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
```

示例 2：

```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```

## 题解

除了递归之外，大部分题解都是采用的动态规划。

### 递归

官方题解：[递归求解，数组存值](https://leetcode-cn.com/problems/climbing-stairs/solution/di-gui-qiu-jie-shu-zu-cun-zhi-by-rang-dan-dan-fei/) 用的递归

思路：「自上而下」的一种思维方式，将大问题拆分为子问题，采用递归的思想解决了问题。

Java：

```java
class Solution {
    public int climbStairs(int n) {
        // 传入一个初始化的空数组，大小是 n+1
        // 因为要用 arr[n] 表示 n 台阶的对应的方法数，不加1，会数组越界
        return method(n, new int[n + 1]);
    }

    public int method(int n, int[] arr) {
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }

        if (arr[n] > 0) {
            return arr[n];
        }

        arr[n] = method(n - 1, arr) + method(n - 2, arr);
        return arr[n];
    }
}
```