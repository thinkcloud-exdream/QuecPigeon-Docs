.. 语法测试专题网页


.. 网页标题

.. title:: 语法测试页面

.. Metadata

.. meta::
   :description: 非官方的 QuecPython 技术开发和入门文档
   :keywords: QuecPython, quecpython, MicroPython, micropython, Quectel, quectel, Python, python

.. 默认语法高亮

.. highlight:: python


.. 主标题

reStructuredText 语法测试
==========================================

.. 信息表

:Author: Exdream

:Date: 2023.02.17

:Status: Test

:Version: 0.0.1


.. 正文


普通文本
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

语法测试页面


空行作为分段标志，
不空行的所有句子被视作一个整体。

| 当然
| 也可以
| 手动断行。



段落
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

这是普通的文本。

这是普通文本的第二行。

   这是缩进之后的。

   缩进第二行。

      再次缩进

      缩进第二行

   测试一下

结束。



.. 标题等级

标题等级
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Level 3
------------------------------------------

Level 4
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Level 5
""""""""""""""""""""""""""""""""""""""""""

Level 6
******************************************



超链接
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. 超链接（见文末）

This is a `hyperlink`_ .



脚注
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. 脚注

Where is your mother [1]_ ?

.. rubric 构成不作为全文结构的小标题

.. rubric:: Notes

.. [1] Something you don't have.


.. 图像

.. .. figure:: ./path/test.png
..    :align: center
..    :alt: 图像不显示时的替代文字
..    :scale: 50 %

..    显示在图片下方的标题




行内字体测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. 粗体和斜体

**Never** gonna give *you* up.

.. 上下标

Put some H\ :sub:`2`\ O into I\ :sup:`2`\ C.


.. 替换标记（见文末）

I want to buy |PC| when I have |money|.



列表测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. 有序列表之自动编号

1. Apple
#. Banana
#. Cock
#. Duck


.. 无序列表及嵌套

- Apple
- Banana
- Orange
   - American Orange
   - Indian Orange
   - China Orange
       - good
       - bad
       - expensive
       - free




名词定义列表
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. 名词定义列表


Apple
   A kind of fruit.

Orange
   **Para1** Another kind of fruit.

   **Para2** Just buy it.

Banana : yellow
   Try another fruit.

Mango : yellow : sweet
   Eat it.



表格测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. 基于 list 的表格，并在表格中使用多行

.. list-table::
    :widths: 20 30 10 15
    :header-rows: 1
    :align: center

    * - 器件类型
      - 型号 / 功能
      - 数量
      - 位号
    * - NB-IoT 无线通信模块
      - BC25PA-04-STD
      - 1
      - U1
    * - 按键
      - | 开机按键（PWK）
        | 复位按键（RST）
        | 唤醒按键（EINT）
        | 自定义按键 1（KEY1）
        | 自定义按键 2（KEY2）
      - 5
      - | S1
        | S2
        | S3
        | S4
        | S5


.. 基于 CSV 文件的表格

.. .. csv-table::
..    :file: ./media/bc25_evb1_pins.csv
..    :widths: 20, 20, 20, 20, 20, 15, 15
..    :header-rows: 1


.. 手绘表格

================== ============
用途                表格类型
================== ============
列举快捷键           简单型
单元格跨行跨列　      网格型
结构简单但超长　      列表型
================== ============



代码
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. 行内代码

Try to input ``sudo rm -rf /`` command to boost your Linux.

.. 代码段

.. code-block:: shell
   :caption: Test Code
   :linenos:

   sudo rm -rf /
   sudo shutdown -P -h now




引用段落
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. 引用功能

测试如图


   苟利国家生死以，岂因祸福避趋之。

   -- 林则徐



选项列表
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. 选项列表

This function has the following parameters:

-a            command-line option "a"
-b file       options can have arguments
              and long descriptions
--long        options can be long also
--input=file  long options can also have
              arguments
/V            DOS/VMS-style options too



Doctest 测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doctest 测试

>>> print '(cut and pasted from interactive Python sessions)'
(cut and pasted from interactive Python sessions)



分割线
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. 分割线测试

上一段

----

下一段


警告和提示
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. 警告和提示元素


红色等级

.. danger:: 
   不要回头，这里不是家！

.. error:: 
   让人类永远保持理智，确实是一种奢望。

.. warning:: 
   空间站进入紧急状态。

橙色等级

.. attention:: 
   来着蓝色空间号的信息。

.. caution:: 
   不要回答！

黄色等级

.. hint:: 
   Test.

.. important:: 
   Test.

.. tip:: 
   小提示。


灰色等级

.. note:: 
   笔记内容测试。

.. admonition:: 自定义提示文本

   MOSS！你在杀人！


Topic 测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. topic:: 当你老了

   Sometimes when you are old.

   You will have no sex.


.. topic:: Genshin Impact

   A totally R18 Game.


侧边栏测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



这是一段在侧边栏之前写的正文。

通常来说，侧边栏会和这段话的底部对齐。

让我们试一下 -----------------------------


.. sidebar:: A little noise 
   :subtitle: I think you won't miss

   Hello.

   This is a secret.

   They have not found it.

   RUN!



这是一段在侧边栏之后写的正文。

通常来说，这段话会出现在侧边栏的左侧。


线性内容块测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

以下内容会按照代码原样渲染，保留换行和缩进格式:

    .. line-block::

        在漆黑的雨夜追赶一条船.
        我就是神里绫华的狗.
        但是当篮球的节奏伴随大肠的气味逐渐氤氲的时候
            有一个声音会在耳边响起.
        "太美丽了, 理塘."


数学公式测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. math::

  α_t(i) = P(O_1, O_2, … O_t, q_t = S_i \lambda)



题词
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

类似于引用的格式，通常放在一篇的开头。

它的字体比引用更大。


.. epigraph::

   No matter where you go, there you are.

   -- Buckaroo Banzai


相似的用法还包括高亮强调：


.. highlights:: 

   No matter where you go, there you are.


以及主体外引用：

.. pull-quote:: 

   No matter where you go, there you are.


实际上他们渲染起来效果一样。



行内元素测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


这是一个包含 :abbr:`缩写 (缩写的解释语句)` 的句子。

.. 以下写法不生效
.. 这是一个包含 :abbreviation:`SC (Super Chat)` 的句子。


这是一个包含代码 :code:`print("good")` 的句子.

这是一个包含系统级指令 :command:`rm -rf` 的句子.

这是一个包含公式 :math:`A_\text{c} = (\pi/4) d^2` 的句子.

这是一个包含 :dfn:`专业术语` 的句子.

这是一个包含 :guilabel:`开始` 按钮的句子.

这是一个包含键盘快捷键 :kbd:`Control-x` 或  :kbd:`Control+c` 或 :kbd:`Control` + :kbd:`F` 的句子.

这是一个包含 :menuselection:`开始 --> 所有程序 --> 扫雷` 的句子.

这是一个包含 :program:`程序名.exe` 的句子.

这是一个包含正则表达式 :regexp:`(\w+):\/\/([^/:]+)(:\d*)?([^# ]*)` 的句子.

这是一个包含可变代码 :samp:`print 1+{num}` 的句子.

这是一个包含完整版本 |release| , 版本 |version| 和日期 |today| 的句子.



Sphinx 专属功能块测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

在版本中新增的功能

.. versionadded:: 2.5
   The *spam* parameter.

在版本中修改的功能

.. versionchanged:: 2.4
   The *spam* parameter.

在版本中废弃的功能

.. deprecated:: 3.1
   Use :func:`spam` instead.

另见

.. seealso::

   参考文献 1
      母猪的产后护理.

   参考文献 2
      理塘旅游手册.


使用标准 TeX 语法写公式

.. math::
   :nowrap:

   \begin{eqnarray}
      y    & = & ax^2 + bx + c \\
      f(x) & = & x^2 + 2xy + y^2
   \end{eqnarray}



Sphinx-design 专属功能块测试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


表格和卡片的融合

.. grid:: 2

   .. grid-item-card::  Title 1

         A

   .. grid-item-card::  Title 2

      顶部文字
      ^^^
      
      正文内容

      +++
      底部文字

可点击的卡片

.. _cards-clickable:

.. card:: Clickable Card (external)
    :link: https://example.com

    The entire card can be clicked to navigate to https://example.com.

.. card:: Clickable Card (internal)
    :link: cards-clickable
    :link-type: ref

    The entire card can be clicked to navigate to the ``cards`` reference target.


下拉展开功能

.. dropdown::

   无标题隐藏内容



.. dropdown:: 带标题隐藏内容

   子内容

   .. dropdown:: 这是一个带动画的下拉
      :animate: fade-in-slide-down

      动画测试内容 1


.. dropdown:: 默认打开的隐藏内容
   :open:

   .. dropdown:: 这是另一个带动画的下拉
      :animate: fade-in

      动画测试内容 2



标签页的联动功能


.. tab-set::

    .. tab-item:: 母鸡
        :sync: key1

        Content 1

    .. tab-item:: 公鸡
        :sync: key2

        Content 2

.. tab-set::

    .. tab-item:: 炖汤
        :sync: key1

        Content 3

    .. tab-item:: 红烧
        :sync: key2

        Content 4


语言选项卡联动

.. tab-set-code::

   .. code-block:: javascript
      :linenos:
      
      a = 1;  

   .. code-block:: python3
      :linenos:
      
      a = 1



.. tab-set-code::

   .. code-block:: javascript
      :linenos:
      
      b = 2;  

   .. code-block:: python3
      :linenos:
      
      b = 2


标签测试

:bdg:`plain badge`

:bdg-primary:`primary`, :bdg-primary-line:`primary-line`

:bdg-secondary:`secondary`, :bdg-secondary-line:`secondary-line`

:bdg-success:`success`, :bdg-success-line:`success-line`

:bdg-info:`info`, :bdg-info-line:`info-line`

:bdg-warning:`warning`, :bdg-warning-line:`warning-line`

:bdg-danger:`danger`, :bdg-danger-line:`danger-line`

:bdg-light:`light`, :bdg-light-line:`light-line`

:bdg-dark:`dark`, :bdg-dark-line:`dark-line`


带超链接的标签

:bdg-link-primary:`https://example.com`

:bdg-link-primary-line:`explicit title <https://example.com>`


按钮

.. button-link:: https://example.com

.. button-link:: https://example.com

    带字样的按钮

.. button-link:: https://example.com
    :color: primary
    :shadow:

    带填充的按钮

.. button-link:: https://example.com
    :color: primary
    :outline:

    带外框线的按钮

.. button-link:: https://example.com
    :color: secondary
    :expand:

    延展至全宽的按钮



.. 超链接放置位置

.. _hyperlink: https://docs.krita.org/zh_CN/contributors_manual/krita_manual_conventions.html


.. 替换标记放置位置

.. |PC| replace:: MacBook

.. |money| replace:: waifu