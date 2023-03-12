.. 网页标题

.. .. title:: 主页

.. Metadata

.. meta::
   :description: 使用 Thonny 进行 QuecPython 开发
   :keywords: QuecPython, quecpython, MicroPython, micropython, Thonny, thonny

.. 默认语法高亮

.. highlight:: python


使用 Thonny 进行 QuecPython 开发
=====================================================


.. warning:: 

    - 本文内容仅适用于 Thonny 3.3.11、3.3.13 和 3.3.14 版本。
    - Thonny 4.0 及之后的版本在软件代码和架构上进行了大幅调整，无法直接应用本文介绍的方法。
    - 鉴于 Thonny 开发者的部分倾向性言论和行为，为避免潜在的技术风险和其他隐患，本文将不再对新版 Thonny 进行适配，同时也不建议用户继续使用 Thonny 作为 Python 和 MicroPython 的开发工具。


.. attention:: 

    本文主要介绍通过修改 Thonny 源码的方式，使其支持 QuecPython 开发的方法。我们注意到，部分用户在阅读完本教程后，将修改完的 Thonny 源代码文件在国内的一些 MicroPython 线上论坛和交流群组中分享，并建议新用户通过直接替换文件的方式完成源码修改。

    虽然直接替换文件这一方式与手动逐行修改源码相比较为简便，但不同版本的 Thonny 的源代码存在一定差异，无视版本差异直接替换源代码文件的做法可能会带来潜在的兼容性问题。因此，不推荐采用这种方式。



前言
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Thonny 是一款对于初学者非常友好的 Python IDE，且对 MicroPython 提供了较为完整的支持。当前，Thonny 支持包括 STM32、ESP32、Raspberry Pi Pico、BBC micro:bit 在内的多种硬件平台，并提供了代码高亮、错误提示、文件上传 / 下载等实用功能，因此深受国内 MicroPython 培训机构的推崇。

QuecPython 是移远通信推出的全新的模组二次开发方式。与传统的 CSDK 相比，该方式通过在 4G Cat.1、NB-IoT 等通信模组上移植并运行 MicroPython，实现了基于 Python 脚本的通信模组二次开发。极大地降低了开发门槛。

目前，由于 QuecPython 官方固件在编译时未开启 MicroPython 的 :dfn:`WEAK_LINKS` 特性，致使在引入内置模块（如 :code:`import sys` 时），无法自动转换为带 :code:`u` 前缀的同名模块（如 :code:`usys` ）。而 Thonny 工具极其依赖这一特性。因此，直接使用 Thonny 与烧录有 QuecPython 固件的模组进行通信时会发生严重报错。为实现两者的正常交互，需要手动修改 Thonny 的部分源码。

本文将介绍使用 Thonny 进行 QuecPython 开发前的一些必要举措。为了便于 MicroPython 初学者理解，本文将尽量避免使用过于专业的概念和表述形式。同时，考虑到 QuecPython 和 Thonny 依旧处于快速发展和变动的阶段，本文的内容存在随时过时的可能性，因而对文章内容的正确性和时效性不做任何保证。


安装 Thonny
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Windows 用户
---------------------------------------------

推荐的安装方式是从 `GitHub Release`_ 上下载安装包。初学者可以下载 Portable 压缩包（“绿色版”），它内置了 Python 3.6 运行环境，开箱即用，无需安装其他程序。

.. _GitHub Release: https://github.com/thonny/thonny/releases

.. hint:: 

    由于 3.3.14 版本尚未提供二进制安装包，建议下载 `3.3.13 版本`_ 。

.. _3.3.13 版本: https://github.com/thonny/thonny/releases/tag/v3.3.13


当然，如果此前电脑上已经安装了 Python 3 和 pip，则可通过在命令提示符（CMD）或 PowerShell 窗口中执行以下命令安装最新版本的 Thonny。

.. code-block:: powershell
    :caption: 通过 pip 安装 Thonny

    python -m pip install thonnyapp

通过 pip 安装时，会自动创建桌面和开始菜单快捷方式。


macOS 用户
-------------------------------------------------

建议按照 `官方 wiki`_ 的说明进行操作。

.. _官方 wiki: https://github.com/thonny/thonny/wiki/MacOSX


Linux 用户
--------------------------------------------------

Thonny 已经被加入到大部分 Linux 发行版的软件仓库内，用户通常可通过简单的命令调用软件包管理器完成安装。

.. tab-set:: 

    .. tab-item:: Ubuntu

        .. code-block:: bash
            :caption: Ubuntu 安装 Thonny

            sudo apt install python3-tk thonny

    .. tab-item:: Fedora

        .. code-block:: bash
            :caption: Fedora 安装 Thonny

            sudo dnf install python3-tkinter thonny


修改源码
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

为了使 Thonny 可被用于 QuecPython 开发，需对其 MicroPython 组件的源码做少许修改。

.. warning:: 

    - 用户应具备基本的 Python 编程技能和编辑器（如 Visual Studio Code）使用技能，否则可能导致修改失败、程序崩溃和其他严重后果。
    - 在用户能读懂将要修改的代码的含义之前，不建议独自尝试。如执意尝试修改，强烈建议提前对原文件进行备份。


在 Thonny 主界面顶部的菜单栏中，选择 :menuselection:`工具 --> 打开Thonny安装目录...` ，进入 Thonny 的程序文件夹。

需要修改以下几个文件。


backend.py
---------------------------------------------

文件路径：:file:`thonny/plugins/micropython/backend.py`


:func:`_get_all_helpers` 函数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

位置：文件的 200 - 250 行左右

将其中被 :code:`"""` 包围的代码中的

.. code-block:: python3
    :caption: 修改前
    :linenos:

    class __thonny_helper:
        import builtins
        try:
            import uos as os
        except builtins.ImportError:
            import os
        import sys    


修改为

.. code-block:: python3
    :caption: 修改后
    :linenos:
    :emphasize-lines: 5, 7, 9, 10

    class __thonny_helper:
        import builtins
        try:
            import uos as os
        except ImportError:
            import os
        try:
            import sys
        except ImportError:
            import usys as sys


即加入一个判定机制，若导入 :code:`sys` 模块失败，则改为导入 :code:`usys` 模块。


:func:`_fetch_epoch_year` 函数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

位置：文件的 420 - 470 行左右

将其中被 :code:`"""` 包围的代码中的

.. code-block:: python3
    :caption: 修改前
    :linenos:

    try:
        from time import localtime as __thonny_localtime
        __thonny_helper.print_mgmt_value(__thonny_helper.builtins.tuple(__thonny_localtime(%d)))
        del __thonny_localtime
    except __thonny_helper.builtins.Exception as e:
        __thonny_helper.print_mgmt_value(__thonny_helper.builtins.str(e))


修改为

.. code-block:: python3
    :caption: 修改后
    :linenos:
    :emphasize-lines: 2, 4, 5

    try:
        try:
            from time import localtime as __thonny_localtime
        except ImportError:
            from utime import localtime as __thonny_localtime
        __thonny_helper.print_mgmt_value(__thonny_helper.builtins.tuple(__thonny_localtime(%d)))
        del __thonny_localtime
    except __thonny_helper.builtins.Exception as e:
        __thonny_helper.print_mgmt_value(__thonny_helper.builtins.str(e))


即加入一个判定机制，若导入 :code:`time` 模块失败，则改为导入 :code:`utime` 模块。


bare_metal_backend.py
---------------------------------------------

文件路径：:file:`thonny/plugins/micropython/bare_metal_backend.py`

串口波特率
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. hint:: 
    仅在使用 BC25 模组进行开发时需要修改本处。

位置：文件的 50 - 60 行左右

将

.. code-block:: python3
    :caption: 修改前
    :linenos:

    BAUDRATE = 115200


修改为

.. code-block:: python3
    :caption: 修改后
    :linenos:

    BAUDRATE = 57600


:func:`_read_file_via_serial` 函数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

位置：文件的 1100 - 1200 行左右


将

.. code-block:: python3
    :caption: 修改前
    :linenos:

    if hex_mode:
        self._execute_without_output("from binascii import hexlify as __temp_hexlify")    


修改为

.. code-block:: python3
    :caption: 修改后
    :linenos:

    if hex_mode:
        self._execute_without_output("from ubinascii import hexlify as __temp_hexlify")    


即将 :code:`binascii` 模块修改为 :code:`ubinascii` 模块。


:func:`_write_file_via_serial` 函数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

位置：文件的 1200 - 1300 行左右


将其中被 :code:`"""` 包围的代码中的

.. code-block:: python3
    :caption: 修改前
    :linenos:

    from binascii import unhexlify as __thonny_unhex
    def __W(x):
        global __thonny_written
        __thonny_written += __thonny_fp.write(__thonny_unhex(x))
        __thonny_fp.flush()
        if __thonny_helper.builtins.hasattr(__thonny_helper.os, "sync"):
            __thonny_helper.os.sync()    


修改为

.. code-block:: python3
    :caption: 修改后
    :linenos:
    :emphasize-lines: 1, 3, 4

    try:
        from binascii import unhexlify as __thonny_unhex
    except ImportError:
        from ubinascii import unhexlify as __thonny_unhex
    def __W(x):
        global __thonny_written
        __thonny_written += __thonny_fp.write(__thonny_unhex(x))
        __thonny_fp.flush()
        if __thonny_helper.builtins.hasattr(__thonny_helper.os, "sync"):
            __thonny_helper.os.sync()    


即加入一个判定机制，若导入 :code:`binascii` 模块失败，则改为导入 :code:`ubinascii` 模块。


连接设备
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

上述修改完成后，关闭并重新启动 Thonny。在 Thonny 主界面顶部的菜单栏中，选择 :menuselection:`工具 --> 设置...` ，打开 Thonny 设置窗口。

切换到 :guilabel:`解释器` 选项卡，在上方的解释器列表中选择 :guilabel:`MicroPython(一般)` ，在下方的端口列表中选择 QuecPython 的交互串口（如 EC600N 选择 :guilabel:`Quectel USB MI05 COM Port` ），然后点击 :guilabel:`确定` 。

之后，Thonny 会自动尝试和 QuecPython 设备建立连接。当 Thonny 主界面下方的 :guilabel:`Shell` 窗口内出现类似


.. code-block:: text
    :caption: QuecPython 启动输出
    

      ____                          __  __           
     / __ \__ _____ _______  __ __ / /_/ / ___  ___ 
    / /_/ / // / -_) __/ _ \/ // / __/ _ \/ _ \/ _ \
    \___\_\_,_/\__/\__/ .__/\_, /\__/_//_/\___/_//_/
                     /_/   /___/                    

    Quecpython v1.12 on Thu_Jan_13_2022_4:46:28_PM ; EC600N with QUECTEL 

    Type "help()" for more information.


的输出时，表明连接成功。之后就可以像开发一般的 MicroPython 设备一样对 QuecPython 设备进行开发了。


已知 bug
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

根据以上流程完成源码修改后，Thonny 的大部分功能即可正常使用，但依旧存在少许缺陷。目前已知的缺陷包括：

- 点击 :guilabel:`变量` 窗格内的变量项目时，后台会发生错误并弹出报错窗口，但不影响主程序运行。

    该错误发生的原因是下位机返回的变量 ID 为负值，导致 Thonny 后台转换过程（在 :file:`memory.py` 中）发生错误。

- 在用户脚本运行时，中断执行（ :kbd:`Ctrl` + :kbd:`C` ）、软重启（ :kbd:`Ctrl` + :kbd:`D` ）和重启后端进程（ :kbd:`Ctrl` + :kbd:`F2` ）功能可能会失灵。

    该故障通常出现在脚本中包含死循环，且循环中未设计任何跳出机制的情况下。此时需要重启硬件或重新烧录固件才可解决，或是使用 QuecPython 官方的 QPYcom 工具。


注意事项
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Thonny 在连接设备时会自动将设备端的时间与上位机（电脑）时间进行同步，这可能导致部分与日期和时间相关的用户脚本在运行时出现意料之外的结果。
- 在使用 Thonny 连接过 QuecPython 设备后，再使用其他串口工具连接设备可能会出现 REPL 界面无响应的情况。此时需手动重置设备（Reset 或重启），或是按下 :kbd:`Ctrl` + :kbd:`B` 键（串口发送 :code:`0x02` ）切换到普通模式，方可进行交互。
- 无法向 QuecPython 设备的文件系统根目录 :code:`/` 写入文件。因此，在使用 Thonny 将脚本保存至设备时，用户需手动将存储路径修改为 :code:`/usr` 分区下。
- 本文介绍的源码修改方法仅能解决基础的交互和文件传输问题，部分功能可能依旧无法正常工作。







