===================
206. 反转链表
===================

https://leetcode-cn.com/problems/reverse-linked-list/

反转一个单链表。

示例:
::

    输入: 1->2->3->4->5->NULL
    输出: 5->4->3->2->1->NULL

---------------------------------

双指针法

申请两个指针，pre 最初指向 null，cur 指向 head，然后遍历cur

每次迭代到 cur，都将 cur的 next指向 pre，然后 pr e和 cur 往后移一位, **注意保存 cur 的 next 节点，避免链表断开**

迭代完成后 cur 变成 null，pre 就是最后一个节点。


.. note::

    - 时间复杂度：O(n)
    - 空间复杂度: O(1)

.. warning::

    依赖 python 的语法特性，链表节点的交换可以一行语句搞定，但不容易记忆

    编写时脑海中可以模拟交换的过程，一个变量一个变量的写，达到最终效果如下

    ``cur.next = pre``

    ``cur.next, cur = pre, cur.next``

    ``cur.next, cur, pre = pre, cur.next, cur``

------------------------------------------

.. code::  python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def reverseList(self, head):
            """
            :type head: ListNode
            :rtype: ListNode
            """
            pre = None
            cur = head
            while cur:
                tmp = cur.next
                cur.next = pre
                pre = cur
                cur = tmp
            return pre
