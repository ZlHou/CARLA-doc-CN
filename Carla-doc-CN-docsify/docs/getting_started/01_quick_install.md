# 快速入门

---


**安装摘要**
========

显示快速启动安装的命令行摘要

    # Install required modules Pygame and Numpy
     pip install --user pygame numpy
    
    # There are two different ways to install CARLA
    
    # Option A) Debian package installation
    # This repository contains CARLA 0.9.10 and later. To install previous CARLA versions, change to a previous version of the docs using the pannel in the bottom right part of the window
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1AF1527DE64CB8D9
    sudo add-apt-repository "deb [arch=amd64] http://dist.carla.org/carla $(lsb_release -sc) main"
    sudo apt-get update
    sudo apt-get install carla-simulator # Install the latest CARLA version or update the current installation
    sudo apt-get install carla-simulator=0.9.10-1 # install a specific CARLA version
    cd /opt/carla-simulator
    ./CarlaUE4.sh
    
    # Option B) Package installation
    #   Go to: https://github.com/carla-simulator/carla/blob/master/Docs/download.md
    #   Download the desired package and additional assets
    #   Extract the package
    #   Extract the additional assets in `/Import`
    #   Run CARLA (Linux).
    ./CarlaUE.sh
    #   Run CARLA (Windows)
    > CarlaUE4.exe
    
    # Run a script to test CARLA.
    cd PythonAPI/examples
    python3 spawn_npc.py # Support for Python2 was provided until 0.9.10 (not included)
    
    # The PythonAPI can be compiled for Python2 when using a Linux build from source


----------

**要求**
======

快速入门安装使用预打包版本的CARLA。内容包含在一个边界中，该边界可以自动运行，无需安装生成。API可以完全访问，但高级定制和开发选项不可用。

要求比生成安装的要求简单。

 - 服务器端。运行高度逼真的环境需要 最小4GB的 GPU。对于机器学习，强烈建议使用专用 GPU。
 - 客户端。Python是通过命令行访问API所必需的。此外，一个良好的互联网连接和两个TCP端口（默认为2000和2001）。
 - 系统要求。任何 64 位操作系统都应该可以运行 CARLA。但是，自版本 0.9.9 以来，CARLA 无法使用默认编译器在 16.04 Linux系统中运行。这些应该升级，以便与CARLA一起工作。
 - 其他要求。两个 Python 模块： Pygame直接使用 Python 创建图形， Numpy用于出色的微积分。 若要使用 pip
   安装两个模块，请运行以下命令。

>  pip install --user pygame numpy

**CARLA安装**
========

Debian 安装是获取 Linux 中最新版本的最简单方法。

下载 GitHub 存储库以获得特定版本或 CARLA 的 Windows 版本。

A. Debian CARLA安装
-----------------

在系统中设置 Debian 存储库。

    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1AF1527DE64CB8D9
    sudo add-apt-repository "deb [arch=amd64] http://dist.carla.org/carla $(lsb_release -sc) main"

安装 CARLA 并在文件夹中检查安装。`/opt/`

    sudo apt-get update # Update the Debian package index
    sudo apt-get install carla-simulator # Install the latest CARLA version, or update the current installation
    cd /opt/carla-simulator # Open the folder where CARLA is installed

此存储库包含 CARLA 0.9.10 和版本更新的版本。若要安装特定版本，请将版本标记添加到安装命令中。

    sudo apt-get install carla-simulator=0.9.10-1 # In this case, "0.9.10" refers to a CARLA version, and "1" to the Debian revision

**！重要**：若要安装 0.9.10 之前的 CARLA 版本，请使用窗口右下角的 pannel 更改为文档的早期版本，然后按照旧说明进行操作。（就说明未翻译）

B. 封装安装
-------

[CARLA repository][1]
存储库包含可用的模拟器的不同版本。开发和稳定部分列出了不同官方发布的包。版本越晚，实验性越大。nightly build是当前开发版本，最不稳定的。

每个版本可能有许多文件。该包是名为"CARLA_version.number "的压缩文件。

下载并提取发布文件。它包含模拟器的预编译版本、Python API 模块和一些用作示例的脚本。

**导入额外资产**
======

对于每个版本，还有包含其他资产和地图的包，例如CARLA 0.9.9.2 的 Additional_Maps_0.9.9.2，其中包含Town06、Town07和Town10。 这些存储是分开存储的，以减少创建包的大小，因此只能在导入这些包后运行它们。

下载包并移动到"Import"文件夹，然后运行以下脚本来提取它们。

> cd ~/carla
> 
> ./ImportAssets.sh

**！注意**：在 Windows上，直接提取根文件夹上的包。

**运行卡拉**
====

打开 CARLA 主目录中的终端。运行以下命令以执行包文件并启动模拟：

>  Linux:
> 
>  ./CarlaUE4.sh
> 
>  Windows:
> 
>  CarlaUE4.exe

**！重要**：在deb 安装中，将位于 中，而不是通常位于的主文件夹中。`CarlaUE4.sh/opt/carla-simulator/bin/carla/`

将弹出一个窗口，其中包含城市视图。这是观众的视角。要在城市中飞行，请使用鼠标和键盘（单击）。服务器模拟器已经运行，等待客户端与世界连接和交互。
现在是开始运行脚本的时间了。下面的示例将生成一些参与者到城市：`WASD`

    # Go to the folder containing example scripts
    > cd PythonAPI/examples
    
    > python3 spawn_npc.py # Support for Python2 was provided until 0.9.10 (not included)

**！注意**：当使用来自源的 Linux版本时，可以使用Python2编译PythonAPI。

命令行选项
-----

启动 CARLA 时有一些配置选项可用。

 - `-carla-rpc-port=N`侦听端口的客户端连接。默认情况下处理端口设置为`N` `N+1`
 - `-carla-streaming-port=N`指定传感器数据流的端口。使用 0 获取随机未使用的端口。第二个端口将自动设置为 `N+1`
-`quality-level={Low,Epic}`更改图形质量级别。在渲染选项中了解更多信息。
 - [UE4 命令行参数的完整列表][2]。UE 提供了许多选项。但是，并非所有这些都将在 CARLA 中提供。

    > ./CarlaUE4.sh -carla-rpc-port=3000

该脚本提供了更多配置选项。`PythonAPI/util/config.py`



    > ./config.py --no-rendering      # Disable rendering
    > ./config.py --map Town05        # Change map
    > ./config.py --weather ClearNoon # Change weather
    
    > ./config.py --help # Check all the available configuration options


----------


更新卡拉
====

打包的版本不需要更新。内容被捆绑起来，因此与 CARLA 的特定版本绑定。每次有版本时，都会更新存储库。若要运行此最新版本或任何其他版本，请删除前一个版本并安装所需的版本。

后续行动
====

因此，快速启动安装过程结束。如果发生任何意外的错误或问题，[CARLA 论坛][3]对所有人开放。有一个安装问题类别来发布这种问题和疑问。

到目前为止，CARLA应该在所需的系统中运行。终端将用于通过脚本与服务器联系、与模拟交互和检索数据。为此，必须了解 CARLA 中的核心概念。阅读"第一步"部分，了解这些步骤。此外，有关 Python API 的所有有关类及其方法的信息都可以在 Python API 参考中访问。


  [1]: https://github.com/carla-simulator/carla/blob/master/Docs/download.md
  [2]: https://docs.unrealengine.com/en-US/Programming/Basics/CommandLineArguments
  [3]: https://forum.carla.org/