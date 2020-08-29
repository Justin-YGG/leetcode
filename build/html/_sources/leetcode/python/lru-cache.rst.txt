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

    class ListNode(object):

        def __init__(self, key, value):
            self.key = key
            self.val = value
            self.pre = None
            self.next = None


    class LinkedList(object):

        def __init__(self):
            self.head = ListNode(0, 0)
            self.tail = ListNode(0, 0)
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
            if self.head == self.tail:
                return
            return self.tail.pre

    class LRUCache(object):

        def __init__(self, capacity):
            """
            :type capacity: int
            """
            self.capacity = capacity
            self.linkedlist = LinkedList()
            self.cache = {}

        def get(self, key):
            """
            :type key: int
            :rtype: int
            """
            if key not in self.cache:
                return -1

            val = self.cache[key].val
            self.put(key, val)
            return val

        def put(self, key, value):
            """
            :type key: int
            :type value: int
            :rtype: None
            """
            node = ListNode(key, value)
            if key in self.cache:
                self.linkedlist.remove(self.cache[key])
                self.linkedlist.add_first(node)
                self.cache[key] = node
            else:
                if self.capacity == self.linkedlist.size:
                    last = self.linkedlist.get_last()
                    if last:
                        self.linkedlist.remove(last)
                        self.cache.pop(last.key)

                self.linkedlist.add_first(node)
                self.cache[key] =  node



    # Your LRUCache object will be instantiated and called as such:
    # obj = LRUCache(capacity)
    # param_1 = obj.get(key)
    # obj.put(key,value)