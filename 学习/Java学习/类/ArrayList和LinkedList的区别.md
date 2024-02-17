ArrayList和LinkedList的区别有以下几点：

- 1. ArrayList是实现了基于动态数组的数据结构，而LinkedList是基于链表的数据结构

- 2. 对于随机访问get和set，ArrayList要优于LinkedList，因为LinkedList要移动指针

- 3. 对于添加和删除操作add和remove，一般大家都会说LinkedList要比ArrayList快，因为ArrayList要移动数据