# 集合

## 增

```java
Set<Integer> seen = new HashSet<>();
// 集合未出现 1，返回 true
seen.add(1);
// 添加已出现的元素，返回 false
System.out.println(seen.add(1))
```