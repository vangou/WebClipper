# Windows/macOS/Linux上安装Node.js，并使用NVM管理多版本Node.js - 雨月空间站
[![](https://www.mintimate.cn/custom/img/oops.webp)
](https://wwads.cn/page/whitelist-wwads)

作者：Mintimate

博客：[https://www.mintimate.cn](https://www.mintimate.cn/)

> Mintimate’s Blog，只为与你分享

我们构建一些项目，经常需要旧版本的node，如：Hexo目前支持性比较好的版本是v12，而最新的Node稳定版本是v14。这个时候，为了避免bug，我们需要切换Node版本。本次教程，就教大家用NVM安装node.js，并且可以无缝切换node.js的版本。

如果要使用NVM切换node.js且事先以及配置单体版node.js，那么请先卸载node.js，或者环境变量内，降低node.js的优先等级到NVM之后。

本教程适用：

*   Linux（x86架构&ARM架构）
*   macOS（x86架构&ARM架构）
*   Windows（X86架构，ARM架构未测试）

警告⚠️：

*   十分不推荐使用NPM下，n模块来管理node版本

本教程同步发布：

*   [腾讯云社区：如何使用NVM安装并管理多版本Node](https://cloud.tencent.com/developer/article/1812323)
*   [腾讯云计算社区：Linux上如何安装和管理多版本Node.js？NVM如何配置？](https://computeinit.com/archives/3668)

首先，明确说明，小白用户完全可以看此篇文章后，自己搭建环境。

迫于生计:

*   接受付费远程帮忙搭建：[博客协助端口（方式）](https://www.mintimate.cn/about/#%E5%8D%8F%E5%8A%A9%E7%AB%AF%E5%8F%A3)
*   接受爱发电捐赠：[@Mintimate](https://afdian.net/@mintimate/plan)

感谢所有捐赠用户⁄(⁄ ⁄ ⁄ω⁄ ⁄ ⁄)⁄

对于不同的操作系统，我们准备不同的NVM工具，以下是项目地址，感兴趣可以去项目源地址看看嗷：

*   For Mac/Linux：[https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)
*   For Windows：[https://github.com/coreybutler/nvm-windows](https://github.com/coreybutler/nvm-windows)

配置前，请事先卸载你已经安装的Node版本和配置的环境变量，避免冲突。

Windows下配置NVM，根据[NVM项目地址](https://github.com/coreybutler/nvm-windows)的配置方法，有两种方法：

*   安装器安装
*   手动配置（推荐）

之所以不推荐用**安装器安装NVM**，是觉得不方便管理啦。本质上两个方法没有区别。

[](#Opt1-安装器)[](#Opt1-安装器 "Opt1:安装器")Opt1:安装器
---------------------------------------------

进入NVM-Windows项目发布地址：[https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases)，选择最新发行版本`nvm-setup.zip`下载：

[![](https://imagehost.mintimate.cn/post_nvmNode/mon1z8g9g6.png)
](https://imagehost.mintimate.cn/post_nvmNode/mon1z8g9g6.png "setup未安装器版本")

之后，解压出自压缩文件，点击安装：

[![](https://imagehost.mintimate.cn/post_nvmNode/nai350bd9n.png)
](https://imagehost.mintimate.cn/post_nvmNode/nai350bd9n.png "解压")

这边注意⚠️：NVM的安装和配置路径**不要有中文**，因为我Windows虚拟机只分配C盘，大家可以最好安装到D盘等其他用户盘：

[![](https://imagehost.mintimate.cn/post_nvmNode/2c9g3802gl.png)
](https://imagehost.mintimate.cn/post_nvmNode/2c9g3802gl.png "路径不要有中文")

[![](https://imagehost.mintimate.cn/post_nvmNode/38fwoza68e.png)
](https://imagehost.mintimate.cn/post_nvmNode/38fwoza68e.png "一样不要中文路径")

安装完成后，在`CMD`或者`Powershell`下，输入NVM，即可发现安装完成：

[![](https://imagehost.mintimate.cn/post_nvmNode/ivug5qnme3.png)
](https://imagehost.mintimate.cn/post_nvmNode/ivug5qnme3.png "安装完成")

[](#Opt2-手动配置【推】)[](#Opt2-手动配置【推】 "Opt2:手动配置【推】")Opt2:手动配置【推】
-------------------------------------------------------------

这个是我推荐的方法，我们下载NVM项目文件，进行手动配置。进入[项目发布地址](https://github.com/coreybutler/nvm-windows/releases)，下载`nvm-noinstall.zip`：  
[![](https://imagehost.mintimate.cn/post_nvmNode/downloadNoinstallZIP.png)
](https://imagehost.mintimate.cn/post_nvmNode/downloadNoinstallZIP.png "下载压缩包")  
解压到一个空白文件内，这个文件夹就是NVM地址目录，比如我这里的地址地址是：`D:\myEnvironment\nvm`  
[![](https://imagehost.mintimate.cn/post_nvmNode/uninstallZIP.png)
](https://imagehost.mintimate.cn/post_nvmNode/uninstallZIP.png "解压压缩包")  
之后，找到电脑的环境变量，比如Windows10：右键`此电脑`-`高级系统设置`-`环境变量`：  
[![](https://imagehost.mintimate.cn/post_nvmNode/findPath.png)
](https://imagehost.mintimate.cn/post_nvmNode/findPath.png "系统变量")

最后，添加环境变量：

*   `NVM_HOME`：NVM地址目录，比如：`D:\myEnvironment\nvm`
*   `NVM_SYMLINK`：NVM配置Node.js的软链接，**该目录需指向并不存在的目录（NVM使用时候会自动创建）**，比如：`D:\myEnvironment\nodejs`

[![](https://imagehost.mintimate.cn/post_nvmNode/pathHome.png)
](https://imagehost.mintimate.cn/post_nvmNode/pathHome.png "系统变量")

追加内容到`Path`，追加的内容：

```haml

```

[![](https://imagehost.mintimate.cn/post_nvmNode/addPath.png)
](https://imagehost.mintimate.cn/post_nvmNode/addPath.png "追加变量")  
安装完成后，在`CMD`或者`Powershell`下，输入NVM，即可发现安装完成：  
[![](https://imagehost.mintimate.cn/post_nvmNode/finishedInstallInWindows.png)
](https://imagehost.mintimate.cn/post_nvmNode/finishedInstallInWindows.png "安装完成")

[](#配置国内源)[](#配置国内源 "配置国内源")配置国内源
---------------------------------

中国大陆这边连接Node.js和NPM官方服务器有点困难，甚至不单单是下载慢了，有时候直接无法下载使用。所以我们换NVM和Node.js成国内源。

注意扩展名，Windows默认隐藏扩展名（如果你之前没设置过的话），不要再有人问这种低级问题了；比如这样实际上是`settings.txt.txt`：  
[![](https://imagehost.mintimate.cn/post_nvmNode/errorSettingsInWindows.png)
](https://imagehost.mintimate.cn/post_nvmNode/errorSettingsInWindows.png "错误示范")

也挺无语的，居然这么多人直接上来就说教程不行，结果一看是这么低级的错误。也再次提醒，就算教程不行，也不要上来就喷，做教程免费给你分享，还不够？

到你NVM安装路径，打开settings.txt文件（如果没有，则创建即可），更改：

```dts

```

[![](https://imagehost.mintimate.cn/post_nvmNode/changeSourceInWindows.png)
](https://imagehost.mintimate.cn/post_nvmNode/changeSourceInWindows.png "换源")  
这里解释一下参数：

*   root：NVM的安装地址。即上文的`%NVM_HOME%`
*   path：激活node.js时的存储路径，即上文的`%NVM_SYMLINK%`
*   arch：系统架构，如果你的Windwos不是`x64`，则填`32`
*   proxy：是否走代理
*   node_mirror：node.js的下载源
*   npm_mirror：npm的下载源

虽然可以使用项目包管理工具安装NVM（比如：[Homebrew](https://brew.sh/)、[APT](https://en.wikipedia.org/wiki/APT_(software))），但还是**推荐macOS和Linux使用手动配置方法**（Git安装、常规安装），安装NVM，本文也是讲解使用非项目包管理器安装NVM。

[](#Opt1-官方脚本)[](#Opt1-官方脚本 "Opt1:官方脚本")Opt1:官方脚本
-------------------------------------------------

官方脚本，需要连接Github，**如果你的设备无法有效连接Github，请选择其他方法（如：常规安装、Git安装）**

Terminal使用`curl`

```awk

```

或者使用`wget`

```awk

```

[![](https://imagehost.mintimate.cn/post_nvmNode/installByScript.png)
](https://imagehost.mintimate.cn/post_nvmNode/installByScript.png "使用脚本")

因为官方项目还在更新，这里粘贴脚本可能会过时。建议大家进入[官方项目地址](https://github.com/nvm-sh/nvm)里进行粘贴。

安装好后，在根据你使用的Shell，在环境变量内追加：

```bash

```

一般macOS在`~/.zshrc`内追加，Linux在没手动配置ZSH情况下，在`~/.bashrc`内追加：  
[![](https://imagehost.mintimate.cn/post_nvmNode/addToZSH.png)
](https://imagehost.mintimate.cn/post_nvmNode/addToZSH.png "追加配置")

最后，在Terminal重载环境变量配置即可：

```bash

```

终端输入nvm命令，就不会报`command not find`了，比如：

```ebnf

```

[![](https://imagehost.mintimate.cn/post_nvmNode/nvmMacOS.png)
](https://imagehost.mintimate.cn/post_nvmNode/nvmMacOS.png "查看nvm版本")

[](#Opt2-Git安装)[](#Opt2-Git安装 "Opt2:Git安装")Opt2:Git安装
-----------------------------------------------------

官方也推荐使用Git进行配置，但是官方的还是使用Github。国内的连接…… 所以，我推荐使用Gitee，在Terminal上一次输入：

```bash

```

我们安装好NVM以后，我们需要配置到环境变量：

```bash

```

在环境变量内，追加：

```routeros

```

最后，在Terminal重载环境变量配置即可：

```bash

```

终端输入nvm命令，就不会报`command not find`了，比如：

```ebnf

```

[![](https://imagehost.mintimate.cn/post_nvmNode/nvmMacOS.png)
](https://imagehost.mintimate.cn/post_nvmNode/nvmMacOS.png "查看nvm版本")

[](#Opt3-常规安装)[](#Opt3-常规安装 "Opt3:常规安装")Opt3:常规安装
-------------------------------------------------

常规安装，其实就是手动实现`Opt1`或`Opt2`。手动下载nvm源码，并解压重命名为`.nvm`。最后，按上文方法，添加

```routeros

```

到环境变量，重载即可。

[](#配置国内源-1)[](#配置国内源-1 "配置国内源")配置国内源
-------------------------------------

大陆这边连接Node和NPM源有点忙，进而NVM也比较慢，所以我们使用前换成国内源。  
临时使用：在终端内输入

```routeros

```

需要长期使用，就配置到配置文件里。

Windows版本和macOS/Linux版本的NVM，操作基本一样，尤其是管理Node.js的命令；本章节，的操作下，**采用一个步骤两个图的模式（一张为Windwos版本NVM的操作截图，一张为macOS/Linux版本的操作截图）**

[](#1-查看已经版本)[](#1-查看已经版本 "1. 查看已经版本")1\. 查看已经版本
------------------------------------------------

```ebnf

```

查看已经安装的版本：  
[![](https://imagehost.mintimate.cn/post_nvmNode/gr2rx5dxlz.png)
](https://imagehost.mintimate.cn/post_nvmNode/gr2rx5dxlz.png "未安装任何版本node")  
[![](https://imagehost.mintimate.cn/post_nvmNode/nvmListWindwos.png)
](https://imagehost.mintimate.cn/post_nvmNode/nvmListWindwos.png "未安装任何版本node")

[](#2-查看可安装版本)[](#2-查看可安装版本 "2. 查看可安装版本")2\. 查看可安装版本
----------------------------------------------------

如何查看通过NVM安装的Node.js版本呢？  
你可以直接使用NVM命令：

```applescript

```

[![](https://imagehost.mintimate.cn/post_nvmNode/listVersionsMacOS.png)
](https://imagehost.mintimate.cn/post_nvmNode/listVersionsMacOS.png "查看可安装版本")  
[![](https://imagehost.mintimate.cn/post_nvmNode/listVersionsWindows.png)
](https://imagehost.mintimate.cn/post_nvmNode/listVersionsWindows.png "查看可安装版本")

[](#3-安装Node-js)[](#3-安装Node-js "3. 安装Node.js")3\. 安装Node.js
------------------------------------------------------------

我们安装v12.21版本node：

[![](https://imagehost.mintimate.cn/post_nvmNode/ibukc8zc9x.png)
](https://imagehost.mintimate.cn/post_nvmNode/ibukc8zc9x.png "安装12.21的node")  
[![](https://imagehost.mintimate.cn/post_nvmNode/nvmInstallNodejsInWindows.png)
](https://imagehost.mintimate.cn/post_nvmNode/nvmInstallNodejsInWindows.png "安装12.21的node")

[](#4-激活Node-js版本)[](#4-激活Node-js版本 "4. 激活Node.js版本")4\. 激活Node.js版本
--------------------------------------------------------------------

我们安装好Node.js以后，需要激活

```apache

```

测试一下可以使用用的：

[![](https://imagehost.mintimate.cn/post_nvmNode/8840obrrb7.png)
](https://imagehost.mintimate.cn/post_nvmNode/8840obrrb7.png "node使用")  
[![](https://imagehost.mintimate.cn/post_nvmNode/checkNodejsWindwos.png)
](https://imagehost.mintimate.cn/post_nvmNode/checkNodejsWindwos.png "node使用")

如果你需要卸载NVM以及NVM所安装的Node.js，也很简单，且没有残留文件。

[](#Windwos)[](#Windwos "Windwos")Windwos
-----------------------------------------

Windwos用户，如果是用安装器安装，使用其自带的反安装快捷方式即可。我们看看手动配置的方法如何卸载。

### [](#1-删除NVM和Node-js软链接)[](#1-删除NVM和Node-js软链接 "1. 删除NVM和Node.js软链接")1\. 删除NVM和Node.js软链接

删除的地址，就是安装过程中的：

*   NVM_HOME：NVM地址目录，比如：D:\\myEnvironment\\nvm
*   NVM_SYMLINK：NVM配置Node.js的软链。比如：D:\\myEnvironment\\nodejs

[![](https://imagehost.mintimate.cn/post_nvmNode/rmInWindows.png)
](https://imagehost.mintimate.cn/post_nvmNode/rmInWindows.png "删除文件")

[](#2-删除环境变量)[](#2-删除环境变量 "2. 删除环境变量")2\. 删除环境变量
------------------------------------------------

之后：`右键`此电脑-`高级系统设置`-`环境变量`:  
[![](https://imagehost.mintimate.cn/post_nvmNode/findPath.png)
](https://imagehost.mintimate.cn/post_nvmNode/findPath.png "环境变量")  
删除上文的`NVM_HOME`、`NVM_SYMLINK`以及`PATH`内的：

```haml

```

[![](https://imagehost.mintimate.cn/post_nvmNode/addPath.png)
](https://imagehost.mintimate.cn/post_nvmNode/addPath.png "删除内容")

[](#macOS-Linux)[](#macOS-Linux "macOS/Linux")macOS/Linux
---------------------------------------------------------

macOS和Linux更简单了，终端执行：

```bash

```

在环境变量内**移除**：

```bash

```

到此，NVM卸载完全。

[](#Hexo博客)[](#Hexo博客 "Hexo博客")Hexo博客
-------------------------------------

在搭建Hexo博客的时候，目前（2021.07）最好还是使用Node.js v12。所以，我搭建Hexo博客，一般也喜欢切换Node.js到v12:  
[![](https://imagehost.mintimate.cn/post_nvmNode/Hexo.png)
](https://imagehost.mintimate.cn/post_nvmNode/Hexo.png "Hexo")

[](#Minecraft面板)[](#Minecraft面板 "Minecraft面板")Minecraft面板
---------------------------------------------------------

这里我先挖个坑，以后有机会和大家说说如何使用Node.js编译Minecraft的控制面板。

[](#VUE)[](#VUE "VUE")VUE
-------------------------

这个不用多说，安装VUE无法就那么几个方法。用Node.js的包管理工具NPM安装VUE再正常不过，运行也方便：  
[![](https://imagehost.mintimate.cn/post_nvmNode/d2b5ca33bd970f64a6301fa75ae2eb22-1024x371.webp)
](https://imagehost.mintimate.cn/post_nvmNode/d2b5ca33bd970f64a6301fa75ae2eb22-1024x371.webp "VUE")

NVM管理Node就到此介绍，有机会，给大家做个视频教程嗷~欢迎关注：

*   [Mintimate’s Bilibili：https://space.bilibili.com/355567627](https://space.bilibili.com/355567627)

如果觉得教程很有用，且财力雄厚。可以：

*   [Mintimate’s 爱发电：https://www.afdian.net/@mintimate/plan](https://www.afdian.net/@mintimate/plan)

* * *