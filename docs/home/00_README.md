﻿# CARLA文档


---

欢迎阅读 CARLA 文档。

此主页包含一个索引，其中简要描述了文档中的不同部分。可以无论按任何顺序的随意选择阅读。无论如何，这里有一些为新人准备的阅读建议。

    - 安装CARLA。要么按照快速启动安装获取CARLA 版本，要么为所需的平台自己创建CARLA。
    - 开始使用CARLA。标题为"第一步"的部分介绍了最重要的概念。
    - 检查 API。有一个方便的 Python API引用来查找可用的类和方法。

CARLA 论坛可以发布阅读过程中可能出现的任何疑虑或建议。

**[CARLA 论坛](https://forum.carla.org/)**

**!重要**
本文档引用 CARLA 0.9.0 或更新版本。要阅读以前的版本，请检查[稳定分支][2]。


----------


**开始**
--

简介 - CARLA有什么值得期待的。

快速入门 - 获取 CARLA 版本。

**创建CARLA**
-------

Linux 创建 - 在 Linux 上创建。

Windows 创建 - 在 Windows 上创建。

更新 CARLA – 更新CARLA最新内容。

生成系统 – 了解如何创建CARLA。

在 Docker 中运行 -  使用容器解决方案运行 CARLA。

F.A.Q. – 一些最常见的安装问题。

**第一步**
---

核心概念 - CARLA 中基本概念概述。

1、世界和客户端 - 管理和访问模拟器。

2、交通参与者和蓝图 - 了解交通参与者以及如何处理他们。

3、地图和导航 - 探索不同的地图和车辆如何移动。

4、传感器和数据 -  使用传感器得到模拟数据。

**高级步骤**
----

OpenDRIVE 独立模式 - 使用任何 OpenDRIVE 文件作为 CARLA 地图。

PTV-Vissim 共同仿真 - 在 CARLA 和 PTV-Vissim之间运行同步仿真。

录像机 - 在模拟中记录事件，然后再次播放。

渲染选项 - 从质量设置到无渲染或屏幕外模式。 

RSS - 在 CARLA 客户端库中实现 RSS。

SUMO 共同仿真 - 在 CARLA 和 SUMO 之间运行同步仿真。

同步和时间步 -  客户端-服务器通信和模拟时间。

交通管理器 -  通过将车辆设置为自动驾驶模式来模拟城市交通。

**引用**
--

Python API 引用 - Python API 中的类和方法。

代码块 - 常用的一些代码片段。

蓝图库 - 为生成参与者提供的蓝图。

C++引用 - CARLA C++中的类和方法。

记录器二进制文件格式 -  记录器文件格式的详细说明。

传感器参考 -  有关传感器及其收集数据的一切。

**插件**
--

carlaviz-Web 可视化工具 -  用于侦听模拟并在 Web 浏览器中显示场景和一些模拟数据的插件。

**ROS bridge**
----------

ROS bridge安装 - 安装 ROS bridge的不同方式。

CARLA 消息引用 - 包含 ROS 中提供的每种类型的 CARLA 消息的解释和字段。

启动文件引用 -  列出提供的启动文件和节点，以及正在使用和发布的主题。

**教程 - 常规**
-------

添加摩擦触发器 -  定义车轮的动态框触发器。

控制车辆物理特性 -  设置车辆物理实体运行时的更改。

控制步行者的骨架 - 使用骨骼对步行者进行动画处理。

获取模拟数据– 使用记录器正确收集数据的分步指南。

**教程 - 资产**
-------

添加新地图 - 创建和导入新地图。

添加新车辆 - 添加在 CARLA 中使用的车辆。

添加新道具 - 将其他道具导入 CARLA。

创建独立包 - 生成和处理资产的独立包。

地图自定义 - 编辑现有地图。

材料定制 - 编辑车辆和建筑材料。

车辆建模 - 为 CARLA 创建新车辆。

**教程 - 开发人员**
-------

使用新资产贡献 - 向 CARLA 添加新内容。

创建传感器 - 开发用于 CARLA 的新传感器。

自定义车辆悬架 -  修改车辆的悬架系统。

发布 - 对于想要发布的开发人员。

生成详细的碰撞器 -  为车辆创建详细的碰撞器。

生成行人导航-  获取步行者四处走动所需的信息。

**贡献**
--

贡献指南 - 对 CARLA 贡献的不同方式。

行为准则 - 贡献者的标准权利和义务。

编码标准 - 编写正确代码的准则。

文档标准 - 编写正确文档的准则。


[1]: https://forum.carla.org/
[2]: https://carla.readthedocs.io/en/stable/