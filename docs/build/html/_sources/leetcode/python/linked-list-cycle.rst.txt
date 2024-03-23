==================
141. 环形链表
==================

https://leetcode-cn.com/problems/linked-list-cycle/

给定一个链表，判断链表中是否有环。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。


示例 1：
::

    输入：head = [3,2,0,-4], pos = 1
    输出：true

解释：链表中有一个环，其尾部连接到第二个节点。

示例 2：
::

    输入：head = [1,2], pos = 0
    输出：true

解释：链表中有一个环，其尾部连接到第一个节点。


示例 3：
::

    输入：head = [1], pos = -1
    输出：false

解释：链表中没有环。

-------------------------------

快慢指针，快指针一次走两步，满指针一次走一步，如果有环，必会相遇。

这种写法思想是 `LBYL`_，其实也是符合正常思路的写法

.. _LBYL: https://docs.python.org/3/glossary.html#term-lbyl

.. note::

    - 时间复杂度： O(n)
    - 空间复杂度： O(1)


-------------------------------

.. code::  python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def hasCycle(self, head):
            """
            :type head: ListNode
            :rtype: bool
            """
            if not head or not head.next:
                return False
            slow, fast = head, head.next
            while fast and fast.next:
                slow = slow.next
                fast = fast.next.next
                if slow is fast:
                    return True
            return False

------------------------------

另外提供一种 `EAFP`_ 的写法

.. _EAFP: https://docs.python.org/3/glossary.html#term-eafp


.. code::  python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def hasCycle(self, head):
            """
            :type head: ListNode
            :rtype: bool
            """
            try:
                slow, fast = head, head.next
                while fast is not slow:
                    fast = fast.next.next
                    slow = slow.next
                return True
            except Exception:
                return False


