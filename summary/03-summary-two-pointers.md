# 双指针

## 参考

- [B站 图灵星球/Array题型：双指针Two Pointers套路【LeetCode刷题套路教程2】](https://www.bilibili.com/video/BV1V54y1Q7bd?from=search&seid=8144097461918819139)

## 同向

0-i 处理好的数据
i-j 处理过但不需要的数据
j-n 待处理的数据

> 用此方法处理过的数组，处理好的数据的相对位置会保持一致。

注意点：
- 区间的开闭要处理正确，一个元素不要出现在多个区间内

### 解题思路

1. 初始化2个指针，i和j，通常都为0
2. `while j < array.length`:
  - 如果需要 array[j]，我们需要保存它，通过 array[i]=array[j]，然后就右移 i
  - 否则的话，就略过这个 j，我们不需要移动 i

> i 表示下一个可填充的位置，i 左边是已经处理好的元素

### 例题

- [26. 删除有序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

## 反向

o-i 处理好的数据
j-n 处理好的数据
i-j 待处理的数据

> 用此方法处理过的数组不会保留元素的相对位置

### 解题思路

1. 初始化2个指针，i = 0, j=array.length - 1
2. `while i <= j`:
  - 依据arry[i]和array[j]的值来做决定
  - 至少有一个指针在它的前进方向移动

> 解题思路只是阐述这种题型的一个通用的解题思路，具体细节还得因题而异。

### 例题

- [344. 反转字符串](https://leetcode-cn.com/problems/reverse-string/) 简单

## 总结

经过上面的总结，可以发现双指针同向和方向的场景，循环条件和指针初始化是有明显不同的，要多练习！