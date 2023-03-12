.. 网页标题

.. .. title:: 主页

.. Metadata

.. meta::
   :description: BC25_QuecPython_EVB_V1.0/V1.2 快速参考手册
   :keywords: QuecPython, quecpython, BC25, bc25, NB, nb, MicroPython, micropython, 开发板, 核心板, EVB, evb

.. 默认语法高亮

.. highlight:: python


开发板软件功能简介
=========================================


BC25_QuecPython_EVB_V1.0 和 BC25_QuecPython_EVB_V1.2 在出厂时，默认内置了标准固件。用户可使用 AT 指令通过主串口与板载的 BC25 模块进行交互。

如希望使用 QuecPython 对模块进行二次开发，需要手动为其烧录专门的 QuecPython 固件。具体操作可参考 :doc:`QuecPython 快速上手教程 </docs/basic_intro/quick_start/index>` 。


烧录完 QuecPython 固件后，设备具有的功能包括：


- 基本系统功能
    - 文件系统管理
    - 文件编辑
    - 自动内存回收
    - 时间和计时
    - 多线程管理
    - 电源管理
- 常用工具功能
    - 随机数生成
    - 数学运算
    - JSON 文件解析
    - HASH 计算
    - 正则表达式
    - 日志打印
- 物联网通信相关功能
    - SIM 卡设置
    - 网络设置
    - 数据拨号
    - TCP / UDP 客户端
    - MQTT 客户端
    - OceanConnect 平台接入
    - 电信 AEP 平台接入
    - 移动 OneNET 平台接入
- 硬件相关功能
    - ADC 电压测量
    - GPIO 和外部中断
    - 串口
    - I2C
    - SPI
    - 定时器
    - RTC 时钟
- 其他功能
    - 固件远程升级
    - 用户脚本远程升级


受硬件型号、固件版本和开发进度影响，设备内部实际可供正常使用的功能可能与上表内容不符，请以实际情况为准。用户可在 QuecPython 的 REPL 交互串口中执行 ``help("modules")`` 语句以查看当前固件内置的所有功能库。

关于各功能（库）的具体使用方法，请参考 `在线 Wiki`_ 和在线文档。


.. 超链接统一管理

.. _在线 Wiki: https://python.quectel.com/wiki/#/
