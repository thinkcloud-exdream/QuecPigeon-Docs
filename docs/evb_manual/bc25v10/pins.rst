.. 网页标题

.. .. title:: 主页

.. Metadata

.. meta::
   :description: BC25_QuecPython_EVB_V1.0/V1.2 快速参考手册
   :keywords: QuecPython, quecpython, BC25, bc25, NB, nb, MicroPython, micropython, 开发板, 核心板, EVB, evb

.. 默认语法高亮

.. highlight:: python



IO 功能概览
=================================================

本节主要介绍开发板所搭载的排针等接口与模块引脚的对应连接关系，以及它们所具备的 GPIO、SPI 等功能。模块本身实际的资源数量可能大于表中所示的值。


.. :widths: 20, 20, 20, 20, 20, 15, 15


.. csv-table::
   :file: ./media/bc25_evb1_pins.csv
   :widths: auto
   :header-rows: 1
   :align: center



.. note::

   .. [1] 指与排针直接相连或经由电平转换芯片间接相连的 BC25 模块的物理引脚编号。
   
   .. [2] 表中所示为《Quectel_BC25系列_QuecOpen_硬件设计手册》规定的引脚名称。在适用于标准 AT 开发方式的《Quectel_BC25系列_硬件设计手册》中，部分引脚被标注为 ``RESERVED`` 。

   .. [3] 不代表 BC25 模块引脚的原始电平范围。

   .. [4] 表中所示的功能只适用于 QuecPython 开发。在基于 QuecOpen（CSDK）进行开发时，可用功能数量及编号次序与表中存在较大差异。请注意区分 QuecPython 和 QuecOpen 的开发资料，避免将两者混淆。

   .. [5] 此处的 ``GPIO2`` 仅作为引脚名称标识之用，不代表实际的 GPIO 编号。在使用 QuecPython 开发时，若需要将该引脚作为 GPIO 使用，请使用 ``GPIO10`` 。表中其余各处同理。

   .. [6] 仅适用于 BC25_QuecPython_EVB_V1.2 开发板。

   .. [7] 在使用 QuecPython 开发时，不可作为普通串口用于数据传输。

   .. [8] 引脚输入 / 输出能力有限，不建议连接外部器件。

   .. [9] 分别与用户按键 S4 和 S5 相连接，使用时应注意避免功能冲突。

