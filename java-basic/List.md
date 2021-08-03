# Java List 相关的基本操作
## ArrayList
```java
// 什么时候使用Array（数组），什么时候使用ArrayList?
// 答案是：当我们不知道到底有多少个数据元素的时候，就可使用ArrayList；如果知道数据集合有多少个元素，就用数组。
// 注意：ArrayList类只支持对象类型，不支持 基础数据类型。就是说ArrayList对象只能存放对象，不能存放基础数据类型的数据
List<String> list = new ArrayList<>();
// 增加元素
list.add("michael");
list.add("qq");
list.add("zx");
list.add("mx");
list.add("qqh");
System.out.println(list);
// 索引 1 的位置，放置 hqh，后面的元素后移
list.add(1, "hqh");
System.out.println(list);

// 修改元素
list.set(1, "qqh");
System.out.println(list);

// 移除元素，可以传入 index
list.remove(2);
// 移除元素，传入不存在的 index，会报异常 IndexOutOfBoundsException
// list.remove(100);
// System.out.println("remove no exist index: " + list);
// 移除元素，可以传入 object，移除第一次找到的"michael"元素
list.remove("michael");
System.out.println("remove exist item: " + list);
// 移除一个不存在的元素，不报异常
list.remove("michael666");
System.out.println("remove no exist item: " + list);

// 检查元素的位置
Integer index = list.indexOf("hqh");
System.out.println("hqh index is: " + index);
// 检查的元素不存在，查看索引值，为 -1
Integer index2 = list.indexOf("mm");
System.out.println("mm index is: " + index2);
//返回元素在链表中最后一次出现的位置，如果返回-1，表示链表中没有这个元素
Integer index3 = list.lastIndexOf("michael");
System.out.println("hqh index is: " + index3);

// 检查链表是否包含某元素
boolean element = list.contains("michael");
boolean element2 = list.contains("michael233");
System.out.println("Check if the arrayList contains object michael: " + element);
System.out.println("Check if the arrayList contains object michael233: " + element2);

// 检查链表是否为空
Boolean check = list.isEmpty();
System.out.println("Check list is empty: " + check);

// 获取链表大小
System.out.println("list size is: " + list.size());

// 获取指定位置的元素
String item = list.get(0);
System.out.println("The item of the index 0 is: " + item);
// 索引超过链表大小，会报异常 IndexOutOfBoundsException
// System.out.println("Out of index: " + list.get(100));

// 遍历
// 方法一
for (int i = 0; i < list.size(); i++) {
    System.out.println("Index is: " + i + "- Item: " + list.get(i));
}
// 方法二
for (String s : list) {
    System.out.println("Item is: " + s);
}
// 方法三
for (Iterator<String> it = list.iterator(); it.hasNext(); ) {
    System.out.println("Item is: " + it.next());
}

// 转换
// ArrayList -> Array
String[] simpleArray = list.toArray(new String[list.size()]);
System.out.println(simpleArray);
// ArrayList -> String
System.out.println(list.toString());
// 从链表中删除所有元素，无返回值
list.clear();
System.out.println(list);
```

## LinkedList

ArrayList 是一个数组队列，LinkedList 是一种链表队列。与 ArrayList 相比，LinkedList 的增加和删除对操作效率更高。

> 当需要频繁在列表开头、末尾增删元素操作时，推荐用 LinkedList。

LinkedList 是 List 接口的实现类，同时，也是也实现了 Deque（双端队列） 接口。因此，既可以当成栈来使用，也可以当成队列来使用。

```java
LinkedList<String> linkedList = new LinkedList<>();
linkedList.add("One");
linkedList.addLast("Two");
linkedList.addFirst("Zero");
linkedList.add("Three");
linkedList.add("Four");
System.out.println(linkedList);

// 仅仅是取元素
System.out.println(linkedList.getFirst());
System.out.println(linkedList.getLast());
// 获取列表首元素
System.out.println(linkedList.peek());
System.out.println(linkedList.peekFirst());
// 获取列表尾元素
System.out.println(linkedList.peekLast());

// 取出列表的头元素并移除
System.out.println(linkedList.poll());
// 取出列表的头元素并移除
System.out.println(linkedList.pollFirst());
// 去列表最后元素并移除
System.out.println(linkedList.pollLast());

// 移除并返回列表首元素，如果列表为空，这个会抛异常
System.out.println(linkedList.removeFirst());
// 移除发病返回列表尾元素，如果列表为空，会抛异常
System.out.println(linkedList.removeLast());
```