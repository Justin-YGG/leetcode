=======================
151.翻转字符串里的单词
=======================

https://leetcode-cn.com/problems/reverse-words-in-a-string/

给定一个字符串，逐个翻转字符串中的每个单词。

示例 1：
::

   输入: "the sky is blue"

   输出: "blue is sky the"

示例 2：
::

   输入: " hello world! "

   输出: "world! hello"

解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。

示例 3：
::

   输入: "a good example"

   输出: "example good a"

解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

说明：

- 无空格字符构成一个单词。

- 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。

- 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。


-------------------------

**方法一**

直接调用 Python 内置方法，先 strip 后 split 将字符串分割成数组，倒序后通过空格拼接即可

.. code-block:: python

   class Solution(object):

        def reverseWords(self, s):
            """
            :type s: str
            :rtype: str
            """
            return ' '.join(s.strip().split()[::-1])


当然本题考察的肯定不是对 Python 内置方法的使用，所以我们考虑自己完成字符串的翻转


**方法二**：

要实现题目中的要求我们需要考虑分四步走，首先将字符串转换成数组，以便于操作

- 字符串整体翻转
- 分别将各个单词翻转
- 处理前后空格
- 处理单词直接多余空格


.. code-block:: python

    class Solution(object):

        def reverseWords(self, s):
            """
            :type s: str
            :rtype: str
            """
            s_list = list(s)
            s_list = self.reverse_string(s_list, 0 , len(s) - 1)
            s_list = self.reverse_word(s_list)
            s_list = self.strip_side(s_list)
            s_list = self.strip_space(s_list)
            return ''.join(s_list)

        def reverse_string(self, s_list, l, r):
            while l < r:

            s_list[l], s_list[r] = s_list[r], s_list[l]
                l += 1
                r -= 1
            return s_list

        def reverse_word(self, s_list):
            """ 采用双指针定位单个单词起始位置 """

            l, r = 0, 0
            while r < len(s_list):
                while r < len(s_list) and not s_list[r].isspace():
                    #: 此时 r 处在单个单词最后一个字符的下个空格位置，所以下面旋转时要减去 1
                    r += 1
                self.reverse_string(s_list, l, r - 1)
                # 因为 r 目前所在位置为空格，往后移动一个位置，保证下个单词翻转后，单词直接至少有一个空格
                r += 1
                l = r
            return s_list

        def strip_side(self, s_list):
            l, r = 0, len(s_list) - 1
            while l < r and s_list[l].isspace():
                l += 1
            while l < r and s_list[r].isspace():
                #: while 跳出时，r 处在最后一个字符上，考虑到数组左闭右开的特性，下面要加 1
                r -= 1
            return s_list[l:r+1]

        def strip_space(self, s_list):
            if not s_list:
                return []
            res = [s_list[0]]
            for i in xrange(1, len(s_list)):
                # 想象一下，单个单词的最后一个字母被追加进数组后，下个空格被追加，然后就会满足while条件，跳过多余空格
                if res[-1].isspace() and s_list[i].isspace():
                    continue
                res.append(s_list[i])
            return s_list
