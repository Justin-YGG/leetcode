===================================
25. K 个一组翻转链表
===================================

https://leetcode-cn.com/problems/reverse-nodes-in-k-group/


给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

 

示例：

给你这个链表：1->2->3->4->5

当 k = 2 时，应当返回: 2->1->4->3->5

当 k = 3 时，应当返回: 3->2->1->4->5

 

说明：

你的算法只能使用常数的额外空间。
你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。

.. note::

    - 时间复杂度：O(n)

    Same as the iterative solution. It is because that in each function call, we need to first check if there are k nodes left starting from input head, and if there is, we have to reverse them. So two linear scans are still necessary.

    - 空间复杂度：O(n/k)

    With recursion, we need to take the cost of call stacks into consideration. For every k nodes, we are supposed to recursively call the function for once. So the total number of recursive calls is n / k. Within each function, we are still using a couple of pointers only in this algorithm, so they are constant cost. Thus, the total space complexity is O(n / k).


.. code:: python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def reverseKGroup(self, head, k):
            """
            :type head: ListNode
            :type k: int
            :rtype: ListNode
            """
            if not head or k <= 0:
               return
            node_a = node_b = head
            for _ in range(k):
                if not node_b:
                    return head
                node_b = node_b.next

            # 上面遍历完成后，node_b 是下一组的头结点，统一也是翻转部分连接的退出条件，等价于正常翻转数组的null
            new_head = self.reverse(node_a, node_b)
            node_a.next = self.reverseKGroup(node_b, k)
            return new_head

        def reverse(self, node_a, node_b):
            pre = None
            cur = node_a
            while cur is not node_b:
                tmp = cur.next
                cur.next = pre
                pre = cur
                cur = tmp
            return pre