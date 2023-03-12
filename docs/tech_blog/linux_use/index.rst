.. 网页标题

.. .. title:: 主页

.. Metadata

.. meta::
   :description: 在 Linux 操作系统中连接 QuecPython 模块
   :keywords: QuecPython, quecpython, MicroPython, micropython, Linux, linux, Ubuntu, ubuntu

.. 默认语法高亮

.. highlight:: python



在 Linux 操作系统中连接 QuecPython 模块
===================================================

前言
----

当前，由于模组厂商只提供了适用于 Windows 操作系统的相关工具，因而
QuecPython 的固件烧录、合并、量产等环节通常都只能在 Windows
操作系统中进行。但一般性的程序开发和调试工作主要通过串口指令交互机制完成，因而不受这一限制，可以在大部分支持
USB CDC 串口的操作系统，如 macOS 和 Linux 中完成。

本文主要介绍在常用的桌面和服务器级 Linux 操作系统中连接 QuecPython
开发板（模块）并建立串口通信的方法。

测试平台
--------

本文所述的相关操作流程和技术细节已在以下模块和操作系统平台上进行过验证。

模块
~~~~

============ =============================
**模块型号** **固件版本**
============ =============================
EC600NCNLA   QPY_OCPU_V0006_EC600N_CNLA_FW
EC600NCNLC   QPY_OCPU_V0006_EC600N_CNLC_FW
EC600UCNLB   QPY_V0007_EC600U_CNLB_FW
EC600UCNLC   QPY_V0005_EC600U_CNLC_FW
============ =============================

操作系统
~~~~~~~~

=============== =============== ========
**系统名称**    **版本**        **架构**
=============== =============== ========
Ubuntu          20.04.3 Desktop AMD64
Ubuntu          20.04.3 Server  AMD64
Ubuntu          22.04 Desktop   AMD64
Ubuntu          22.04 Server    ARM64
Fedora          36 Workstation  AMD64
Fedora          36 Server       AMD64
CentOS          7.9.2009        AMD64
CentOS          8.5.2111        AMD64
Raspberry Pi OS 10 (Buster)     ARM64
=============== =============== ========


.. hint:: 

   从 22.04 版开始，Ubuntu 会自动加载 EC600S 和 EC600N
   的驱动。当用户将已经烧录有 QuecPython 固件的 EC600N
   模块连接到电脑时，会自动出现 :guilabel:`ttyACM0` 串口，连接到该串口即可开始
   Python 交互，无需其他操作。


操作流程
--------

.. hint:: 

   本文中的大部分操作在 Fedora 35 Workstation
   操作系统中完成。对于其他操作系统的用户，请根据实际情况自行调整相关指令。

首先，使用 USB 线缆连接模块和计算机，并确保模块已正常上电运行。

然后，在系统终端中执行 :command:`ls /dev/ttyUSB*` 命令，列出与本机连接的所有
USB 串口。由于未检测到 USB 串口设备，通常会出现“无法访问”错误。

.. code:: bash

   $ ls /dev/ttyUSB*
   ls: 无法访问 '/dev/ttyUSB*': 没有那个文件或目录

使用 :command:`lsusb` 命令列出所有连接的 USB 设备，在返回内容中可以看到 Quectel
设备及其 USB ID。

.. code:: bash

   $ lsusb
   Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
   Bus 003 Device 005: ID 0e0f:0002 VMware, Inc. Virtual USB Hub
   Bus 003 Device 004: ID 0e0f:0002 VMware, Inc. Virtual USB Hub
   Bus 003 Device 003: ID 2c7c:0901 Quectel Wireless Solutions Co., Ltd. Android
   Bus 003 Device 002: ID 0e0f:0003 VMware, Inc. Virtual Mouse
   Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
   Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
   Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub

若在此步骤未发现 Quectel
设备，请检查线缆连接和模块运行情况，或更换计算机再试。

通常情况下 EC600N 模块的 ID 为 :code:`2c7c 6001` ，EC600U 模块的 ID 为
:code:`2c7c 0901` ，请以实际返回值为准。

之后，使用以下命令手动添加 USB 串口设备。

.. code:: bash

   $ sudo modprobe option
   $ sudo sh -c 'echo "2c7c 0901" > /sys/bus/usb-serial/drivers/option1/new_id'
   # 请根据实际的设备 ID 修改此命令

此时，再执行 :command:`ls /dev/ttyUSB*` 命令可以看到新增的 USB 串口。

.. code:: bash

   $ ls /dev/ttyUSB*
   /dev/ttyUSB0  /dev/ttyUSB2  /dev/ttyUSB4  /dev/ttyUSB6
   /dev/ttyUSB1  /dev/ttyUSB3  /dev/ttyUSB5
   # 一般而言 EC600U 会新增 6 至 7 个端口，EC600N 为 3 个

至此，就可以使用 USB 串口与 QuecPython
模块进行通信了。一般的，在没有接入其他 USB 串口设备的情况下，EC600N
模块的 USB AT 口为 :guilabel:`ttyUSB1` ，Python 交互口为 :guilabel:`ttyACM0` ；EC600U
模块的 USB AT 口为 :guilabel:`ttyUSB0` ，Python 交互口为
:guilabel:`ttyUSB6` 。请以实际情况为准。


.. attention:: 

   -  新版的 QuecPython 固件在编译时未开启 MicroPython 的 :dfn:`WEAK_LINKS`
      特性，致使在引入内置模块（如 :code:`import sys` 时），无法自动转换为带
      :code:`u` 前缀的同名模块（如 :code:`usys` ）。因此，无法直接使用 Thonny
      等常见的 MicroPython 工具与烧录有 QuecPython
      固件的模组进行通信。建议改用 cutecom 等普通串口工具。

   -  使用虚拟机可能会降低串口通信的稳定性或导致串口间歇性失灵，因此不建议使用虚拟机执行操作。

   -  操作系统重启后，上述涉及 USB ID
      的改动会失效。必要情况下可将相关命令写入开机启动脚本。

   -  部分操作系统可能会自动将模块作为 4G
      网卡使用，建议用户手动检查并及时禁用该网卡，以避免无谓的流量消耗。
