# DFS 与 递归

## 递归

一个函数调用自身，这样的方式就是递归。

> 引入题：井字格，如果不走远路的话，有多少种走法？最核心的部分：`f(m,n)=f(m-1, n)+f(m,n-1)`，注意剔除特殊点。 

```java
private static int f(int m, int n) {
    if (m < 0 || n < 0) {
        return 0;
    }
    if (m == 0 && n == 0) {
        return 1;
    }

    return f(m - 1, n) + f(m, n - 1);
}
```

分治法（Divide Conquer）：看上面的公式，可以发现缩小了问题的空间，这种思想就是分治。

递归可能性能不是很高，可以通过一个 Count 来记录计算的次数，用来观察。

通过加 Cache 的方法，可以优化解法，让复杂度大大降低。

```java
public class Solution {
    static int count = 0;
    static int[][] cached = new int[100][100];

    public static void main(String[] args) {
        System.out.println(f(3, 2));
    }

    private static int f(int m, int n) {
        count++;
        if (m < 0 || n < 0) {
            return 0;
        }
        if (m == 0 && n == 0) {
            return 1;
        }
        if (cached[m][n] != 0) {
            return cached[m][n];
        }
        cached[m][n] = f(m - 1, n) + f(m, n - 1);
        return f[m][n];
    }
}
```

## 动态规划

上面的题目也可以用动态规划的解法来解。因为，可以从起点开始，先把显而易见的结果准备好，然后根据已经得到的结果，进行推导出后续点的结果。

```java
private static int dp(int m, int n) {
    int[][] dp = new int[m + 1][n + 1];
    dp[0][0] = 1;
    for (int i = 1; i <= m; i++) {
        dp[i][0] = 1;
    }
    for (int i = 1; i <= n; i++) {
        dp[0][i] = 1;
    }
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }
    }
    return dp[m][n];
}
```

1. 把显而易见的结果放在那边——数据准备好
2. 按照规划好的路线，根据已经准备好的数据，继续计算

从显而易见的结果，能够规划出向目标推进的一条路线，利用已经获得的结果进行推算，一直推算到最后的结果，叫动态规划。

## DFS

如果上面的题目条件做了改变：不一定要走近路，可以绕着走，只要不走过同一个路口，这样有多少种路径？

> 深度搜索是一种很重要的解法，强相关的是回溯法解法。BFS 相对出现频率相对较少。

回溯是与 DFS 强相关的一种编程技巧。用递归来实现回溯，是一种常见的写法。

在每个点上，规定一个探路的规矩，顺时针方向。 探路的过程，为了找到全部的路线，在找到一条路线后，需要返回，然后继续尝试。

深度优先搜索，考虑的出发点有 2 点：
1. 深度：在本问题中，往前走一步可以就看做深度上加了一层；—— 考虑函数的设计、参数的定义
2. 广度：有多少种选项，四个方向。选项执行不能重复，要看满足什么条件时，走那种选项。亦或者，项循环去执行每种选项。

```java
public class Solution {
    // 题目限定的范围
    static int ROW = 5; // y，行，其实对应了 y 坐标
    static int COL = 6; // x，列，其实对应了 x 坐标
    static int count = 0;
    static int[][] visited = new int[100][100];

    public static void main(String[] args) {
        System.out.println(dfs(4, 4, 5, 4));
    }

    private static int dfs(int x, int y, int m, int n) {
        // 找到它
        if (x == m && y == n) {
            return 1;
        }
        // 有效性检查
        if (x < 0 || y < 0 || x > COL || y > ROW) {
            return 0;
        }
        // 已经访问过的路口
        if (visited[x][y] == 1) {
            return 0;
        }

        visited[x][y] = 1;
        // go right
        int sum = 0;
        sum += dfs(x + 1, y, m, n);
        // go down
        sum += dfs(x, y - 1, m, n);
        // go left
        sum += dfs(x - 1, y, m, n);
        // go up
        sum += dfs(x, y + 1, m, n);
        visited[x][y] = 0;
        return sum;
    }
}
```

## 回溯练习题

典型例题
- [22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/) 中等
- [46 全排列](https://leetcode-cn.com/problems/permutations/)
- [51. N 皇后](https://leetcode-cn.com/problems/n-queens/) 困难

