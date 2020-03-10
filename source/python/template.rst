==============
模板
==============

递归

---------------------------

.. note::

    1. 拒绝人肉递归

    2. 找最近重复子问题

    3. 运用数学归纳法的思维

----------------------------

.. code:: python

    def recursion(level, param1, param2, ...):
        # recursion terminator
        if level > MAX_LEVEL:
           process_result
           return

        # process logic in current level
        process(level, data...)

        # drill down
        self.recursion(level + 1, p1, ...)

        # reverse the current level status if needed