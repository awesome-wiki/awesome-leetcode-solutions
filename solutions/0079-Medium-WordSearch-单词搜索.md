# [0079-Medium-WordSearch-单词搜索](https://leetcode-cn.com/problems/word-search/)

## 题目

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用

示例 一：

![1](https://gitee.com/michael_xiang/images/raw/master/uPic/j2aMQg.png)

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

其他的示例略，可以[阅读原题](https://leetcode-cn.com/problems/word-search/)

## 题解

这道题拿到手之后，第一感觉就是利用 DFS 的回溯进行查找，心中将这个二维数组表示的内容想象为一个坐标轴。在每个格子里就要尝试向各个方向进行探索。
- 怎么判断探索到的结果是想要的呢？—— 利用一个变量记录目前已经探索了几位字符了，要与目标 word 对应位置的字符相等，直到二者长度一致
- 怎么去不断尝试从格子的下一个节点开始从 0 开始重新探索呢？——循环探索二维数组的格子，循环内去调用回溯函数，回溯函数执行完的结果不满足时，则会从下一个格子重新探索了；
- 怎么取不走重复的格子呢？—— 用一个同等长度的的数组，布尔值表示是否已走过；

上面的问题思考完，回溯函数的参数设计基本就差不多了，剩下的就是回溯函数内具体的执行逻辑实现。

### 回溯

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int iMax = board.length;
        int jMax = board[0].length;
        boolean flag = false;

        boolean[][] visited = new boolean[iMax][jMax];
        for (int i = 0; i < iMax; i ++) {
            for (int j = 0; j < jMax; j++) {
                // 从每个格子开始探索，一旦不符合，跳出从下一格子开始
                flag = check(board, i, j, visited, 0, word);
                if (flag) {
                    return true;
                }
            }
        }
        return false;
    }


    private boolean check(char[][] board, int m, int n,boolean[][] visited, int index, String word) {        
        int iMax = board.length;
        int jMax = board[0].length;

        // 边界条件检查
        if (m >= iMax || m < 0 || n >= jMax || n < 0) {
            return false;
        }
        // 格子是否已访问，如果已访问，则不继续向下执行
        if (visited[m][n]) {
            return false;
        }
        // 借助 index 可以知道目前查询到的位置
        if (board[m][n] != word.charAt(index)) {
            return false;
        } else if (index == word.length() - 1) {
            return true;
        }

        boolean flag = false;
        // 正在访问的格子要标记为已访问
        visited[m][n] = true;
        // 想办法尝试向各个方法去探索
        flag = check(board, m, n + 1, visited, index + 1, word);
        if (flag) {
            return true;
        }
        flag = check(board, m + 1, n,visited, index + 1, word);
        if (flag) {
            return true;
        }
        flag = check(board, m, n - 1, visited, index + 1, word);
        if (flag) {
            return true;
        }
        flag = check(board, m - 1, n, visited, index + 1, word);
        if (flag) {
            return true;
        }
        // 回溯结束，恢复之前的状态
        visited[m][n] = false;

        return false;
    }
}
```

上面的题解，可以发现在回溯函数内，终止条件有很多场景：
- 解符合目标
- 搜索范围超出边界

此外，上面在尝试向各个方向进行探索时，还有一种常见的做法：
```
class Solution {
    private int[][] directions = {{0, 1}, {0, -1}, {1, 0}, { -1, 0}};

    public boolean exist(char[][] board, String word) {
        int iMax = board.length;
        int jMax = board[0].length;
        boolean flag = false;

        boolean[][] visited = new boolean[iMax][jMax];
        for (int i = 0; i < iMax; i ++) {
            for (int j = 0; j < jMax; j++) {
                // 从每个格子开始探索，一旦不符合，跳出从下一格子开始
                flag = check(board, i, j, visited, 0, word);
                if (flag) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean check(char[][] board, int m, int n,boolean[][] visited, int index, String word) {        
        int iMax = board.length;
        int jMax = board[0].length;

        // 边界条件检查
        if (m >= iMax || m < 0 || n >= jMax || n < 0) {
            return false;
        }
        // 格子是否已访问，如果已访问，则不继续向下执行
        if (visited[m][n]) {
            return false;
        }
        // 借助 index 可以知道目前查询到的位置
        if (board[m][n] != word.charAt(index)) {
            return false;
        } else if (index == word.length() - 1) {
            return true;
        }


        // 正在访问的格子要标记为已访问
        visited[m][n] = true;
        // 想办法尝试向各个方法去探索
        for (int[] dir : directions) {
            boolean flag = check(board, m + dir[0], n + dir[1], visited, index + 1, word);
            if (flag) {
                return true;
            }
        }
        // 回溯结束，恢复之前的状态
        visited[m][n] = false;

        return false;
    }
}
```

针对可能探索的方向，提前创建好了一个方向集，它里面放着各个探索方向需要执行的坐标操作，然后针对这个探索方向集进行循环探索。

```java
x = x + dir[0];
y = y + dir[1];
```

这个方向的探索操作，在以前做过的一道题中见过：[874. 模拟行走机器人](https://leetcode-cn.com/problems/walking-robot-simulation/?utm_source=pocket_mylist)