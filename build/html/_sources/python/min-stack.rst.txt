=====================
155. 最小栈
=====================

https://leetcode-cn.com/problems/min-stack/

设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) -- 将元素 x 推入栈中。
pop() -- 删除栈顶的元素。
top() -- 获取栈顶元素。
getMin() -- 检索栈中的最小元素。

示例:
::

    MinStack minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    minStack.getMin();   --> 返回 -3.
    minStack.pop();
    minStack.top();      --> 返回 0.
    minStack.getMin();   --> 返回 -2.

----------------------------------------

.. note::

    我们在栈中的元素是一个 tuple，初始化是添加 ``(-1, float('inf'))``，元组第一个元素记录入栈元素的值，第二个元素记录最小值
    每次入栈时都与其比较，那么在栈“不为空”的情况下，最后入栈的元素所在的 tuple 即为最小值

----------------------------------------

.. code::  python

    class MinStack(object):

        def __init__(self):
            """
            initialize your data structure here.
            """
            self.stack = [(-1, float('inf'))]

        @property
        def is_empty(self):
            return len(self.stack) == 1

        def push(self, x):
            """
            :type x: int
            :rtype: None
            """
            self.stack.append((x, min(x, self.stack[-1][-1])))

        def pop(self):
            """
            :rtype: None
            """
            if self.is_empty:
                return
            return self.stack.pop()[0]

        def top(self):
            """
            :rtype: int
            """
            if self.is_empty:
                return
            return self.stack[-1][0]


        def getMin(self):
            """
            :rtype: int
            """
            if self.is_empty:
                return
            return self.stack[-1][-1]



    # Your MinStack object will be instantiated and called as such:
    # obj = MinStack()
    # obj.push(x)
    # obj.pop()
    # param_3 = obj.top()
    # param_4 = obj.getMin()