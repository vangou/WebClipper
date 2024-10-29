# Linux 服务器安装 Clash代理
[Linux 服务器安装 Clash代理](https://blog.myxuechao.com/post/36#%E4%B8%80%E3%80%81%E4%B8%8B%E8%BD%BD%E5%AE%89%E8%A3%85%E5%8C%85) 

 [Linux 服务器安装 Clash代理](https://blog.myxuechao.com/post/36#%E4%B8%80%E3%80%81%E4%B8%8B%E8%BD%BD%E5%AE%89%E8%A3%85%E5%8C%85) 

 [

Linux 服务器安装 Clash代理

](/post/36 "Linux 服务器安装 Clash代理")

2023-12-11[

服务器

](/category/%E6%9C%8D%E5%8A%A1%E5%99%A8)174466

目录
--

一、下载安装包

二、应用安装

（1）linux 相关的有 3 个安装包

（2）安装步骤

（3）修改系统代理

1.临时修改

2.永久修改

3.一键开启/关闭 代理

（4）测试代理效果

三、使用守护进程Clash 自启动及后台运行

四、配置Clash可视化面板

（1）下载面板文件

（2）修改/root/clash/ 下的config.yaml

（3）重启服务

（4）访问页面

Linux 服务器安装 Clash代理

这篇文章主要介绍了如何在Linux服务器上安装和配置Clash代理，包括下载安装包、设置系统代理、使用守护进程使Clash自启动及后台运行，以及配置Clash的可视化面板。

一、下载安装包
=======

该文件为私密内容，如需讨论或获取，请私下联系我。

二、应用安装
======

> 由于 Linux 发行版版本众多，我们无法提供所有发行版的安装说明，下文以`CentOS Linux release 7.9.2009 (Core)`为例。（作为一个 Linux 用户，您应该明白如何安装。）

（1）linux 相关的有 3 个安装包
--------------------

*   `386`，指的是i386指的是intel80386,32位架构
*   `amd64`，指的是amd的64位架构，新的指令集，支持64位系统
*   `amd64-v3，`指的是使用 golang v3 环境变量，环境变量版本越高,兼容性越差,但性能可能因使用新指令而得到提升

**所以，32 位系统使用 `-386`, 64 位系统默认使用 `-amd64-v3`，如果存在不兼容的情况在使用`-amd64`**

（2）安装步骤
-------

1.  在终端执行 `cd /root` && `mkdir clash` ，创建 `clash` 文件夹。
2.  在终端执行 `cd clash` ，进入 `clash` 文件夹。
3.  下载 Clash 文件

> **我这里以**`clash-linux-amd64-latest.gz`**为例子**

bash

`#方法一
#直接拿到 文件链接地址下载
#所以下载命令为 wget -N --no-check-certificate 文件地址
wget -N --no-check-certificate https://github.com/Dreamacro/clash/releases/download/v1.4.1/clash-linux-amd64-v1.4.1.gz

#方法二
下载好文件后直接放在 clash 文件夹里面` 

![](https://image.myxuechao.com/VPN/21.png)

1.  在终端执行 `gunzip clash-linux-amd64-latest.gz` ，解压.gz文件。

![](https://image.myxuechao.com/VPN/22.png)

1.  将解压后的文件重命名为 `clash`。

bash

`# 更该改文件名称 为clash
mv clash-linux-amd64-latest clash` 

![](https://image.myxuechao.com/VPN/23.png)

1.  在终端执行 `chmod +x clash` 赋予 Clash 执行权限
2.  复制托管链接

![](https://image.myxuechao.com/VPN/24.png)

1.  在终端执行 `wget -O config.yaml` + 刚刚复制的托管链接

![](https://image.myxuechao.com/VPN/25.png)

1.  在终端执行 `./clash -d .` 即可启动 `Clash`，同時启动 HTTP 代理和 Socks5 代理。

> **首次运行之后会在`当前运行配置目录生成配置文件`，产生的目录为 `/root/clash` ，里面有 `config.yaml` 和 `Country.mmdb` 两个文件。** 

![](https://image.myxuechao.com/VPN/26.png)

（3）修改系统代理
---------

> 运行 clash 后还需要修改系统代理，这样流量才能走 clash

### 1.临时修改

bash

`export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890` 

### 2.永久修改

1.  运行 `cd ~`切换到 root 账户目录；
2.  运行 `vi .bashrc`编辑，添加系统代理；

bash

`export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
export all_proxy=socks5://127.0.0.1:7890` 

### 3.一键开启/关闭 代理

1.  在当前终端配置文件中增加相关函数

bash

`# 开启代理
function proxy_on(){
    export all_proxy=socks5://127.0.0.1:7890  # 注意你的端口号可能不是7890，注意修改
    export http_proxy=http://127.0.0.1:7890
    export https_proxy=http://127.0.0.1:7890
    echo -e "已开启代理"
}

# 关闭代理
function proxy_off(){
    unset all_proxy
    unset http_proxy
    unset https_proxy
    echo -e "已关闭代理"
}` 

2.  重新加载终端配置文件

bash

`source ~/.bashrc` 

3.使用函数

bash

`#在终端输入 proxy_on 代表使用代理
proxy_on
#在终端输入 proxy_off 代表关闭代理
proxy_off` 

4.查看代理的地址

bash

`env | grep proxy` 

（4）测试代理效果
---------

bash

`# 测试链接谷歌
curl https://www.google.com
#有返回结果即可（不能使用PING）
wget google.com` 

三、使用守护进程Clash 自启动及后台运行
======================

> 现在有一个问题就是在终端手动执行的执行 `./clash -d .` 即可启动 `Clash`，同時启动 HTTP 代理和 Socks5 代理。如果关闭了就无法代理。那么我们可以用进程的方法解决

1.  运行`cp clash /usr/local/bin`

2.1. 创建 `/etc/systemd/system/clash.service`

bash

`[Unit]
Description=Clash daemon, A rule-based proxy in Go.
After=network.target

[Service]
Type=simple
Restart=always
ExecStart=/usr/local/bin/clash -d   /root/clash

[Install]
WantedBy=multi-user.target` 

1.  运行 `systemctl enable clash`设置 clash 服务在系统启动时运行；
2.  运行 `systemctl start clash`立即运行 clash 服务；
3.  运行 `systemctl status clash`查看 clash 服务运行状态；
4.  运行 `systemctl stop clash` 停止服务
5.  运行 `systemctl restart clash` **重启服务**
6.  运行 `systemctl is-enabled clash` **查看服务是否正在运行**
7.  运行 `journalctl -xe`查看运行日志；

四、配置Clash可视化面板
==============

（1）下载面板文件
---------

bash

`# 1.切换到 /root/clash/文件夹里
cd /root/clash/
# 2.下载 ui
wget https://github.com/haishanh/yacd/archive/gh-pages.zip
# 3.解压
unzip gh-pages.zip
# 4.修改文件名为 dashboard
mv yacd-gh-pages/ dashboard/` 

（2）修改/root/clash/ 下的config.yaml
-------------------------------

*   `secret`就是`api的访问秘钥` 如果没有的话任何人都可以访问你的clash面板的api 不安全
*   这里的 `port` 是 http/https 代理端口
*   `socks-port` 是 socks 流量代理端口
*   `external-controller` 是外部控制端口，用于面板控制(前端页面的端口)
*   `external-ui` 是本地控制页面的源码（前端面板的路由）

bash

`port: 7890
socks-port: 7891
secret: 123456789
external-controller: 0.0.0.0:9090  #别忘记在服务器厂商开放端口号
external-ui: dashboard  #打开面板` 

（3）重启服务
-------

bash

`systemctl restart clash` 

（4）访问页面
-------

*   `IP`：就是`自己的宿主机 ip`
*   `端口`：就是刚才配置里的 `9090`
*   `密码secret`：就是 刚才配置的 `123456789`

bash

`# 宿主机 ip + 9090/ui
http://154.8.199.114:9090/ui/` 

![](https://image.myxuechao.com/VPN/27.png)

*   **访问到在线面板了 这里就是相当于自己部署了一个前端页面 跟随着`clash启动` 填入`对应的api`就可以查看到机器代理的情况了**
*   **那么对于我来说就是我的**

![](https://image.myxuechao.com/VPN/28.png)

如果对你有用的话，可以打赏哦

打赏

![](https://image.myxuechao.com/life/alipayPaymentCode.png)

![](https://image.myxuechao.com/life/WeChatPayCode.jpg)

本文作者:LiuXueChao

本文链接:https://blog.myxuechao.com/post/36

版权声明:本博客所有文章除特别声明外，均采用 BY-NC-SA 许可协议。转载请注明出处！

[

服务器

](/tag/%E6%9C%8D%E5%8A%A1%E5%99%A8)

* * *

[

< Docker 网络详解（十一）

](/post/35)

[

Docker Compose 容器编排（十二） >

](/post/37)