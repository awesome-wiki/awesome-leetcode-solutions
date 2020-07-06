# [242-Valid Anagram/有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram)

## Problems

### CN

给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

示例 1:
```
输入: s = "anagram", t = "nagaram"
输出: true
```

示例 2:
```
输入: s = "rat", t = "car"
输出: false
```

说明:
- 你可以假设字符串只包含小写字母。

### EN

Given two strings s and t , write a function to determine if t is an anagram of s.

Example 1:
```
Input: s = "anagram", t = "nagaram"
Output: true
```

Example 2:
```
Input: s = "rat", t = "car"
Output: false
```

Note:
- You may assume the string contains only lowercase alphabets.

## 解法

### 解法一

思路：利用排序思想，将给定字符串都想办法排序，然后比较二者是否相等。

Java：

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        // 先判断字符串长度是否一样，不一样，直接返回false
        // 要结束，早结束！
        if (s.length() != t.length()) {
            return false;
        }
        // String 的 toCharArray 方法，将 String 转换为字符数组
        char[] str1 = s.toCharArray();
        char[] str2 = t.toCharArray();
        // Arrays.sort 将指定数组按升序排序
        Arrays.sort(str1);
        Arrays.sort(str2);
        // equals方法：比较两个数组
        return Arrays.equals(str1, str2);

    }
}
```