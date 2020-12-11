# Linux下创建


---

创建过程可能相当长且繁琐。 [F.A.Q.][1]页面为最常见的问题提供了解决方案。或者，使用[CARLA 论坛][2]发布可能发生的任何意外问题。

**Linux 创建命令摘要**
============

要在 Linux 上构建的命令行
    # Make sure to meet the minimum requirements
    # Read the complete documentation to understand each step
    
    # Install dependencies
    sudo apt-get update &&
    sudo apt-get install wget software-properties-common &&
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test &&
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add - &&
    sudo apt-add-repository "deb http://apt.llvm.org/$(lsb_release -c --short)/ llvm-toolchain-$(lsb_release -c --short)-8 main" &&
    sudo apt-get update
    
    # Additional dependencies for Ubuntu 18.04
    sudo apt-get install build-essential clang-8 lld-8 g++-7 cmake ninja-build libvulkan1 python python-pip python-dev python3-dev python3-pip libpng-dev libtiff5-dev libjpeg-dev tzdata sed curl unzip autoconf libtool rsync libxml2-dev &&
    pip2 install --user setuptools &&
    pip3 install --user -Iv setuptools==47.3.1
    
    # Additional dependencies for previous Ubuntu versions
    sudo apt-get install build-essential clang-8 lld-8 g++-7 cmake ninja-build libvulkan1 python python-pip python-dev python3-dev python3-pip libpng16-dev libtiff5-dev libjpeg-dev tzdata sed curl unzip autoconf libtool rsync libxml2-dev &&
    pip2 install --user setuptools &&
    pip3 install --user -Iv setuptools==47.3.1 &&
    pip2 install --user distro &&
    pip3 install --user distro
    
    # Change default clang version
    sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/lib/llvm-8/bin/clang++ 180 &&
    sudo update-alternatives --install /usr/bin/clang clang /usr/lib/llvm-8/bin/clang 180
    
    # Get a GitHub and a UE account, and link both
    # Install git
    
    # Download Unreal Engine 4.24
    git clone --depth=1 -b 4.24 https://github.com/EpicGames/UnrealEngine.git ~/UnrealEngine_4.24
    cd ~/UnrealEngine_4.24
    
    # Download and install the UE patch
    wget https://carla-releases.s3.eu-west-3.amazonaws.com/Linux/UE_Patch/430667-13636743-patch.txt 430667-13636743-patch.txt
    patch --strip=4 < 430667-13636743-patch.txt
    
    # Build UE
    ./Setup.sh && ./GenerateProjectFiles.sh && make
    
    # Open the UE Editor to check everything works properly
    cd ~/UnrealEngine_4.24/Engine/Binaries/Linux && ./UE4Editor
    
    # Clone the CARLA repository
    git clone https://github.com/carla-simulator/carla
    
    # Get the CARLA assets
    cd ~/carla
    ./Update.sh
    
    # Set the environment variable
    export UE4_ROOT=~/UnrealEngine_4.24
    
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
    python3 spawn_npc.py # Support for Python2 was provided until 0.9.10 (not included)
    python3 dynamic_weather.py # Support for Python2 was provided until 0.9.10 (not included)
    
    # Optionally, to compile the PythonAPI for Python2, run the following command in the root CARLA directory
    make PythonAPI ARGS="--python-version=2"


**要求**
==

**系统要求**
----

 - Ubuntu 18.04. CARLA为以前的 Ubuntu 版本提供至 16.04 的支持。但是，UE需要适当的编译器才能正常工作。Ubuntu 18.04 和以前版本的依赖项列在下面。确保安装与系统对应的依赖。
 - 30GB 磁盘空间。完整的构建将需要大量的空间，尤其是虚幻引擎。确保有大约 30/50GB 的可用磁盘空间。
 - 足够的 GPU。CARLA旨在进行逼真的仿真，因此服务器至少需要一个 4GB GPU。强烈建议使用专用 GPU 进行机器学习。
 - 两个 TCP 端口和良好的互联网连接。默认情况下为 2000 和 2001。确保防火墙或任何其他应用程序都不会阻止网络连接。

**依赖**
--

CARLA 需要运行许多依赖项。其中一些是在这个过程中自动构建的，例如Boost.Python。其他是二进制文件，应在开始生成之前安装（cmake、clang、Python的不同版本等等）。 为此，请在终端窗口中运行以下命令。

    sudo apt-get update &&
    sudo apt-get install wget software-properties-common &&
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test &&
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add - &&
    sudo apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-8 main" &&
    sudo apt-get update

**！警告**：以下命令取决于您的 Ubuntu 版本。请确保相应地选择。

**Ubuntu 18.04：**

    sudo apt-get install build-essential clang-8 lld-8 g++-7 cmake ninja-build libvulkan1 python python-pip python-dev python3-dev python3-pip libpng-dev libtiff5-dev libjpeg-dev tzdata sed curl unzip autoconf libtool rsync libxml2-dev &&
    pip2 install --user setuptools &&
    pip3 install --user -Iv setuptools==47.3.1 &&
    pip2 install --user distro &&
    pip3 install --user distro

**以前的Ubuntu版本：**

    sudo apt-get install build-essential clang-8 lld-8 g++-7 cmake ninja-build libvulkan1 python python-pip python-dev python3-dev python3-pip libpng16-dev libtiff5-dev libjpeg-dev tzdata sed curl unzip autoconf libtool rsync libxml2-dev &&
    pip2 install --user setuptools &&
    pip3 install --user -Iv setuptools==47.3.1 &&
    pip2 install --user distro &&
    pip3 install --user distro

**所有Ubuntu系统：**
为了避免UE和 CARLA 依赖项之间的兼容性问题，请使用相同的编译器版本和C++运行库来编译所有内容。CARLA 团队使用 clang-8 和 LLVM 的 libc+。更改默认的clang 版本以编译UE和CARLA依赖项。

    sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/lib/llvm-8/bin/clang++ 180 &&
    sudo update-alternatives --install /usr/bin/clang clang /usr/lib/llvm-8/bin/clang 180


----------


**GitHub**
======

1、创建[GitHub][3]帐户。CARLA 在不同的 GitHub 存储库中组织，因此需要一个帐户来克隆这些存储库。

2、安装[git][4]通过终端管理存储库。

3、创建一个[UE][5]帐户来访问虚幻引擎存储库，这些存储库是私有的。

4.连接GitHub和UE帐户。转到您的个人设置，在[UE][6]的网站有一个部分。单击`Connections > Accounts`并链接两个帐户。

**！警告**：新的虚幻引擎帐户需要激活。创建帐户后，将发送验证邮件。请查看它，否则UE存储库将在以下步骤中显示为不存在。

**Unreal Engine**
=============

CARLA 的当前版本仅在虚幻引擎 4.24 上运行。在本指南中，安装将在`~/UnrealEngine_4.24`中完成，但可以更改路径。如果路径不同，请相应地更改以下命令。

**！注意：**除了本节，还有另一个指南在Linux上构建UE。请记住，CARLA将需要4.24版本，而不是最新的版本。

1、在本地计算机上克隆虚幻引擎 4.24 的内容。

    git clone --depth=1 -b 4.24 https://github.com/EpicGames/UnrealEngine.git ~/UnrealEngine_4.24

2、进入已克隆 UE4.24 的目录。

    cd ~/UnrealEngine_4.24

3、下载虚幻引擎的修补程序。此修补程序修复了更改地图时可能发生的一些 Vulkan 可视化问题。使用以下命令下载并安装它。

    wget https://carla-releases.s3.eu-west-3.amazonaws.com/Linux/UE_Patch/430667-13636743-patch.txt 430667-13636743-patch.txt
    patch --strip=4 < 430667-13636743-patch.txt

**！警告：**如果UE已创建，请安装修补程序，然后再次创建。

4、进行创建。这可能需要一两个小时，具体取决于您的系统。

    ./Setup.sh && ./GenerateProjectFiles.sh && make

5、打开编辑器以检查UE是否安装正确。

    cd ~/UnrealEngine_4.24/Engine/Binaries/Linux && ./UE4Editor

到目前为止，出现任何问题都与UE有关。CARLA对此无能为力。但是，Unreal Engine提供的构建文档可能会有所帮助。

**CARLA构建**
=======

系统应准备好开始构建CARLA。为了清楚起见，到目前为止，简要的总结一下：

 - 运行 CARLA 的最低技术要求是合适的。
 - 已正确安装依赖项。
 - GitHub 帐户已准备就绪。
 - 虚幻引擎 4.24 运行平稳。

**！注意：**使用`sudo apt-get install aria2`下载aria2将加快以下命令的执行。

**克隆存储库**
-----

项目的官方存储库。下载并提取它，或使用以下命令行克隆存储库。

    git clone https://github.com/carla-simulator/carla

现在，模拟器的最新状态（存储库中的`master`分支）已复制到本地。以下是存储库中最相关的分支的简要介绍。请记住，您可以使用命令更改和检查分支。`git branch`

 - `master`分支-已测试的最新修补程序和功能。这些将在下一个 CARLA 版本中提供。
 - `dev`分支-仍在开发和测试中的最新修补程序和功能。当新版本到来时，此分支将与`master`合并。
 - `stable`分支-被标记为稳定的最新版本 CARLA 。以前的CARLA版本也有其自己的分支。

**获取资产**
----

下载资产，因为它们是运行 CARLA 所必需的。它们存储在一个分离的包中，以减少创建包的大小。脚本会自动下载和提取最新的稳定资产。软件包大小 >3GB，因此下载可能需要一些时间。

1、进入您的CARLA根目录。路径应与刚刚克隆的存储库对应。

 - cd ~/carla

2、运行脚本获取资产。

 - ./Update.sh


**！重要：**要下载当前开发中的资产，请访问[更新 CARLA][7]并阅读获取开发资产。

**设置环境变量**
------

这是 CARLA 查找虚幻引擎 4.24 安装文件夹所必需的。

    export UE4_ROOT=~/UnrealEngine_4.24

要持久地将该变量设置为会话范围，该变量应添加到`~/.bashrc`或`~/.profile`。否则，它只能从当前 shell 访问。为此，请按照以下步骤操作。

1.打开 。`~/.bashrc`

    gedit ~/.bashrc

2.在`~/.bashrc`文件中写入环境变量：

    export UE4_ROOT=~/UnrealEngine_4.24

3.保存文件并重置终端。

**编译CARLA**
-------

这是最终构建CARLA的最后一步。有不同的`make`命令来构建不同的模块。它们都在CARLA 根 文件夹中运行。

**！警告：**请确保运行`make PythonAPI`准备客户端，`make launch`启动服务器。或者，`make LibCarla`将准备 CARLA 库导入到任何地方。

**make PythonAPI** 编译 API 客户端，必须授予对模拟的控制权。这只需要第一次。记得在更新CARLA时再次运行它。脚本将能够在执行此命令后运行。

    make PythonAPI

**make launch** 编译服务器模拟器并启动虚幻引擎。按"Play"以启动观看视图并关闭编辑器窗口以退出。相机可以使用键盘`WASD`移动，并在移动鼠标时单击场景来旋转。

    make launch

可能会要求生成其他实例，比如`UE4Editor-Carla.dll`。同意以打开项目。在第一次启动期间，编辑器可能会显示有关着色器和网格距离字段的警告。这些需要一些时间来加载，城市不会正常显示，直到加载完成。

最后，让我们测试模拟器。`PythonAPI/examples`和`PythonAPI/util`有一些示例脚本，可能对初学者特别有用。以下命令将生成一些参与者到城镇，并创建一个天气循环。每个脚本应在一个终端中运行。

    # Support for Python2 was provided until 0.9.10 (not included)
    # Terminal A 
    cd PythonAPI/examples
    python3 spawn_npc.py  
    # Terminal B
    cd PythonAPI/examples
    python3 dynamic_weather.py 

**！重要：**如果模拟以非常低的 FPS 速率运行，请转到UE编辑器的`Edit/Editor preferences/Performance`，并在后台禁用使用较少CPU。

或者，要编译 Python2 的 PythonAPI，请运行CARLA 根目录中的以下命令。

    make PythonAPI ARGS="--python-version=2"

现在CARLA已经准备好出发了。以下是最有用的`make`命令摘要。

| 命令 | 描述 |
| --- | --- |
| `make help` |	打印所有可用的命令。|
|`make launch`|	在编辑器窗口中启动 CARLA 服务器。|
|`make PythonAPI`	|生成 CARLA 客户端。|
|`make package`|	生成 CARLA 并创建用于分发的打包版本。|
|`make clean`|	删除生成系统生成的所有二进制文件及其临时文件。|
|`make rebuild`|	`make clean`和`make launch`两者合一的命令。|

有关本指南的任何问题，请阅读 [F.A.Q.][8]页面或在[CARLA论坛][9]中发布帖子。

完成构建后提出的一些建议:了解如何更新 CARLA 或模拟应该做的第一步，并学习一些核心概念。


  [1]: 05_faq.md
  [2]: https://forum.carla.org/c/installation-issues/linux
  [3]: https://github.com/
  [4]: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
  [5]: https://www.unrealengine.com/en-US/feed
  [6]: https://www.unrealengine.com/en-US/
  [7]: https://carla.readthedocs.io/en/latest/build_update/#get-development-assets
  [8]: 06_faq.md
  [9]: https://forum.carla.org/c/installation-issues/linux