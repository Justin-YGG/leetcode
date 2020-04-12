====================
146. LRU缓存机制
====================

https://leetcode-cn.com/problems/lru-cache/

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果密钥 (key) 存在于缓存中，则获取密钥的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果密钥不存在，则写入其数据值。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

进阶:

你是否可以在 O(1) 时间复杂度内完成这两种操作？

示例::

    LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

    cache.put(1, 1);
    cache.put(2, 2);
    cache.get(1);       // 返回  1
    cache.put(3, 3);    // 该操作会使得密钥 2 作废
    cache.get(2);       // 返回 -1 (未找到)
    cache.put(4, 4);    // 该操作会使得密钥 1 作废
    cache.get(1);       // 返回 -1 (未找到)
    cache.get(3);       // 返回  3
    cache.get(4);       // 返回  4



.. code:: python

    class Node(object):
        def __init__(self, key, value):
            self.key = key
            self.value = value
            self.next = None
            self.pre = None


    class DoubleList(object):

        def __init__(self):
            self.head = Node(0, 0)
            self.tail = Node(0, 0)
            self.head.next = self.tail
            self.head.pre = self.tail
            self.tail.pre = self.head
            self.tail.next = self.head
            self.size = 0

        def add_first(self, node):
            node.next = self.head.next
            node.pre = self.head
            self.head.next.pre = node
            self.head.next = node

            self.size += 1

        def remove(self, node):
            node.pre.next = node.next
            node.next.pre = node.pre
            node.next = None
            node.pre = None

            self.size -= 1

        def get_last(self):
            if self.tail == self.head:
                return
            return self.tail.pre


    class LRUCache(object):

        def __init__(self, capacity):
            self.capacity = capacity
            self.cache = dict()
            self.linked_list = DoubleList()

        def get(self, key):
            if key not in self.cache:
                return -1

            val = self.cache[key].value
            self.put(key, val)
            return val

        def put(self, key, value):class Node(object):
        def __init__(self, key, value):
            self.key = key
            self.value = value
            self.next = None
            self.pre = None


    class DoubleList(object):

        def __init__(self):
            self.head = Node(0, 0)
            self.tail = Node(0, 0)
            self.head.next = self.tail
            self.head.pre = self.tail
            self.tail.pre = self.head
            self.tail.next = self.head
            self.size = 0

        def add_first(self, node):
            node.next = self.head.next
            node.pre = self.head
            self.head.next.pre = node
            self.head.next = node

            self.size += 1

        def remove(self, node):
            node.pre.next = node.next
            node.next.pre = node.pre
            node.next = None
            node.pre = None

            self.size -= 1

        def get_last(self):
            if self.tail == self.head:
                return
            return self.tail.pre


    class LRUCache(object):

        def __init__(self, capacity):
            self.capacity = capacity
            self.cache = dict()
            self.linked_list = DoubleList()

        def get(self, key):
            if key not in self.cache:
                return -1

            val = self.cache[key].value
            self.put(key, val)
            return val

        def put(self, key, value):
            node = Node(key, value)

            if key in self.cache:
                self.linked_list.remove(self.cache[key])
                self.linked_list.add_first(node)
                self.cache[key] = node
            else:
                if self.capacity == self.linked_list.size:
                    last = self.linked_list.get_last()
                    if last:
                        self.linked_list.remove(last)
                        self.cache.pop(last.key)
                self.linked_list.add_first(node)
                self.cache[key] = node