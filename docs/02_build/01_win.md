# Windows下创建


---

创建过程可能相当长且繁琐。 [F.A.Q.][1]页面为最常见的安装过程中的问题提供了解决方案。或者，使用[CARLA 论坛][2]发布可能发生的任何意外问题。

**Windows 创建命令摘要**
==============
若要执行以下命令，必须使用具有管理员权限的Visual Studio 2017 native console x64，否则可能会出现权限错误！！！重要信息：要执行下面的“make”命令，您**必须**使用具有**管理员权限的Visual Studio 2017 native console x64**，否则可能会出现权限错误。`make`
要在 Windows 上创建所使用的命令行:

    # Make sure to meet the minimum requirements
    
    # Necessary software: 
    #   CMake
    #   Git
    #   Make
    #   Python3 x64
    #   Unreal Engine 4.24
    #   Visual Studio 2017 with Windows 8.1 SDK and x64 Visual C++ Toolset
    
    # Set environment variables for the software
    
    # Clone the CARLA repository
    git clone https://github.com/carla-simulator/carla
    
    # make the CARLA client and the CARLA server
    make PythonAPI
    make launch
    
    # Press play in the Editor to initialize the server
    # Run example scripts to test CARLA
    # Terminal A 
    cd PythonAPI/examples
    python3 spawn_npc.py 
    # Terminal B
    cd PythonAPI/examples
    python3 dynamic_weather.py 
    # The PythonAPI will be built based on the installed Python version
    # The docs will use Python3, as support for  Python2 was provided until 0.9.10 (not included)


----------

**要求**
==

**系统细节**
----

 - x64 系统。模拟器需要在任何 64 位 Windows 系统中运行。
 - 30GB 磁盘空间。安装所需的所有软件和CARLA将需要大量的空间。确保有大约 30/50GB 的可用磁盘空间。
 - 足够的 GPU。CARLA旨在进行逼真的仿真，因此服务器至少需要一个4GB GPU。强烈建议使用专用GPU进行机器学习。
 - 两个 TCP 端口和良好的互联网连接。默认情况下为 2000 和 2001。确保防火墙或任何其他应用程序都没有阻止这些。


----------


**需要的软件**
=====

**次要安装**
----

 - [CMake][3]从简单的配置文件生成标准生成文件。
 - [Git][4]是一个用于管理 CARLA 存储库的版本控制系统。
 - [Make][5]生成可执行文件。
 - [Python3 x64][6]是 CARLA 中的主要脚本语言。安装 x32 版本可能会导致冲突，因此强烈建议卸载它。

**！重要：**请确保这些程序已添加到[环境路径][7]中。请记住，添加的路径将引导到bin目录。

**Visual Studio 2017**
------------------

从[这里][8]获取2017版本。社区是免费版本。使用Visual Studio安装程序安装两个附加元素。

 - Windows 8.1 SDK。在右侧的"安装详细信息"部分中选择它。
 - x64 Visual C++工具集。在“Workloads ”部分中，选择**Desktop development with C++**。这将启用用于创建的一个 x64命令提示符。按下按钮并搜索。注意不要打开一个`x86_x64`提示。`Win` `x64`

**！重要：**其他Visual Studio版本可能会导致冲突。即使冲突版本已经卸载，某些寄存器也可能仍然存在。要从计算机完全清除 Visual Studio，请转到并运行
`Program Files (x86)\Microsoft Visual Studio\Installer\resources\app\layout` `.\InstallCleanup.exe -full`

**Unreal Engine**
-------------

转到[Unreal Engine][9]并下载Epic游戏启动器。在Epic游戏启动器 中，下载**Unreal Engine 4.24.x**。请确保运行它，以检查所有内容是否已正确安装。`Engine versions/Library`

**！注意：**安装 VS2017 和 UE4.24后，右键单击.uproject文件时，应显示生成可视化 Studio 项目文件选项。如果不可用，UE4.24 安装出现问题。创建一个UE 项目进行检查，如有必要，重新安装。

**CARLA构建**
=======

**！重要：**到目前为止，发生了很多事情。强烈建议重新启动计算机。

**克隆存储库**
-----

[CARLA GitHub存储库][10]

项目的官方存储库。下载并提取它，或者使用 x64 终端中的以下命令行克隆它。

    git clone https://github.com/carla-simulator/carla

现在，项目的最新内容（`master`称为存储库中的分支）已复制到本地。

**！注意：**该`master`分支包含最新的修补程序和功能。稳定代码位于`stable`和 以前的 CARLA 版本中，它们有自己的分支。始终记住使用`git branch`命令检查 git 中的当前分支。

**获取资产**
----

至今，只有资产包尚未下载。 `\Util\ContentVersions.txt`包含指向 CARLA 版本资产的链接。这些必须在 `Unreal\CarlaUE4\Content\Carla`中提取。如果路径不存在，请创建它。

下载最新资产以与当前版本的 CARLA 使用。

**设置环境变量**
------

这是CARLA查找虚幻引擎安装文件夹所必需的。这样，用户可以选择要使用的虚幻引擎的特定版本。如果未指定环境变量，CARLA 将在目录中查找，并使用搜索顺序中的最新一个版本。

1. 打开 Windows 控制面板并转到 `Advanced System Settings`。
2. 在"高级"面板上打开`Environment Variables...`。
3.单击"new..." 来创建变量。
4. 将变量命名为`UE4_ROOT`，并选择 UE4 安装的文件夹路径。

构建CARLA
最后一步是最终构建CARLA。有不同的`make`命令来构建不同的模块。它们都在根 CARLA 根文件夹中运行。

**！警告：**请确保运行`make PythonAPI`以准备客户端和`make launch`来启动服务器。或者，`make LibCarla`将准备好的 CARLA 库导入到任何地方。

 - **make PythonAPI** 编译 API 客户端，这是授予对模拟器授权所必需的。这只是第一次需要。请记住在更新 CARLA 时再次运行它。执行此命令后，脚本将能够运行。`make PythonAPI`
 - **make launch**编译服务器模拟器并启动虚幻引擎。按"**Play**"以启动观看视图，关闭编辑器窗口以退出。相机可以使用`WASD`键移动，并在移动鼠标时单击场景来旋转。`make launch`

 项目可能会要求生成其他实例，如第一次会要求生成`UE4Editor-Carla.dll`。同意以打开项目。在第一次启动期间，编辑器可能会显示有关着色器和网格距离字段的警告。这些需要一些时间来加载，城市不会正常显示，直到加载成功。

最后，让我们测试模拟器。`PythonAPI/examples`和`PythonAPI/util`有一些示例脚本，可能对一些初学者特别有用。以下命令将生成一些参与角色到城镇，并创建一个天气周期。每个脚本应在单独一个终端中运行。

    # Terminal A 
    cd PythonAPI/examples
    python3 spawn_npc.py  
    # Terminal B
    cd PythonAPI/examples
    python3 dynamic_weather.py 
    # The PythonAPI will be built based on the installed Python version
    # The docs will use Python3, as support for  Python2 was provided until 0.9.10 (not included)

**！重要：**如果模拟以非常低的 FPS 速率运行，请转到UE编辑器`Edit/Editor preferences/Performance`，并在后台禁用使用较少 CPU。

现在CARLA已经准备好出发了。以下是最有用的`make`命令的简要。

| 命令 | 描述 |
|-|-|
| `make help` | 打印所有可用的命令。 |
| `make launch` | 在编辑器窗口中启动 CARLA 服务器。 |
|`make PythonAPI`|	生成 CARLA 客户端。|
|`make package`|	生成 CARLA 并创建用于分发的打包版本。|
|`make clean`|	删除生成系统生成的所有二进制文件及其临时文件。|
|`make rebuild`||	`make clean`和`make launch`合二为一的命令。|

有关本指南的任何问题，请阅读 [F.A.Q.页面][11]或在[CARLA论坛][12]中发布的帖子。

完成构建后提出的一些建议：了解如何更新CARLA构建或进行模拟的第一步，并学习一些核心概念。


  [1]: 05_faq.md
  [2]: https://forum.carla.org/c/installation-issues/linux
  [3]: https://cmake.org/download/
  [4]: https://git-scm.com/downloads
  [5]: Make
  [6]: https://www.python.org/downloads/
  [7]: https://www.java.com/en/download/help/path.xml
  [8]: https://developerinsider.co/download-visual-studio-2017-web-installer-iso-community-professional-enterprise/
  [9]: https://www.unrealengine.com/download
  [10]: https://github.com/carla-simulator/carla
  [11]: 05_faq.md
  [12]: https://forum.carla.org/c/installation-issues/linux