# Python成功解决：可用性域*中配置 VM.Standard.A1.Flex 的容量不足 | LOUIS.HE
简介
--

Oracle 允许我们在其云服务中创建免费资源（例如 VM）以进行测试。例如，具有最大 4 个 OCPU 和 24GB RAM 的 VM.Standard.A1.Flex 非常适合托管网站。然而，交易并不总是可用的，因为需求总是比甲骨文所能提供的多。如果您现在尝试创建免费 VM，大多数情况下您会收到“VM.Standard.A1.Flex 的容量不足”错误消息。在这篇文章中，我将向您展示如何运行一个脚本，该脚本会随着时间的推移运行并尝试创建一个 VM，直到它成功。

亲测的Python运行脚本：（代码中涉及服务器隐私信息，仅供自己使用，如有需要请移步下文自行下载原生脚本！）

链接：[https://pan.baidu.com/s/13wnDfoZ0IUVD0Bs8cMvHtw](https://pan.baidu.com/s/13wnDfoZ0IUVD0Bs8cMvHtw)  
提取码：(保密)

Out of capacity for shape VM.Standard.A1.Flex in availability domain AD-1. Create the instance in a different availability domain or try again later. 如果指定了容错域，请尝试在不指定容错域的情况下创建实例。如果这样不起作用，请稍后重试。 [了解有关主机容量的更多信息。](https://www.oracle.com/cloud/free/faq.html)

脚步
--

*   该脚本是 Python 脚本。您需要在计算机上安装[Python](https://www.python.org/downloads/)。该脚本需要一些设置才能正常工作。变量的值可以通过以下步骤获得。
*   转到[Oracle Cloud](https://cloud.oracle.com/)并开设一个帐户。你需要一张主卡。主**区域**是您要创建 VM 的位置。**Home 区域**设置后无法更改。因此，请明智地选择您所在的地区，以便您以后可以利用 VM。
*   创建帐户后，登录到您的帐户。在右上角，单击配置文件图标，然后选择**用户设置**。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-1.png)

Oracle 添加API秘钥

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-2.png)

添加API秘钥

*   确保选中 **生成API密钥对**，单击 **下载私有秘钥** 并将其保存为文件 **oci\_private\_key.pem**。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-4.png)

**oci\_private\_key.pem**

*   单击**添加**。从 textarea 复制内容并将其保存为文件**config**。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-3.png)

*   将**config**和**oci\_private\_key.pem**文件放在同一目录中。

*   打开**配置**文件并编辑**key\_file**的行。那是您的私钥的路径。注意：如果您使用 Windows，则路径必须是绝对路径。

*   转到[Oci Python 脚本存储库](https://github.com/chacuavip10/oci_auto)并下载文件**oci\_auto.py**。将其与其他文件一起保存在目录中。下载后只需要修改如下红框区域，其他信息请勿修改。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-5.png)

修改python脚本文件

*   返回[Oracle Cloud](https://cloud.oracle.com/)并**创建 VM 实例**。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-6.png)

**创建 VM 实例**

向下滚动到**网络**。点击**编辑**。选择**不分配公共 IPv4 地址**。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-7.png)

不分配公共IP

向下滚动到**添加 SSH 密钥**。单击**保存私钥**和**保存公钥**。将它们存放在安全的地方。我们稍后会需要它。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-8.png)

生成密钥对

*   在创建 VM 之前，按**F12**打开 DevTools。选择标签**网络**。

*   单击**创建**。你会收到一个错误。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-9.png)

在 开发者工具 的选项卡**Network**中，现在搜索**实例**请求。右键单击它。选择**复制 –> 复制为 cURL (cmd)**。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-10.png)

开发者工具**复制为 cURL (cmd)**

*   将内容复制到编辑器。找到零件**–data-raw**。
*   打开您之前下载的**oci\_auto.py**并将值替换为**–data-raw**中的值。

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-11.png)

参考文件

根据上面文件，完成下面文件！

![](https://www.louishe.com/wp-content/uploads/2022/02/oracle-vps-free-5.png)

python脚本

```
instance_display_name = 'instance-********'
compartment_id = 'ocid1.tenancy.oc1..********'
domain = "OFDj:AP-SINGAPORE-1-AD-1"  # availability_domain
image_id = "ocid1.image.oc1.ap-singapore-1.********"
subnet_id = 'ocid1.subnet.oc1.ap-singapore-1.********'
ssh_key = "ssh-rsa ******** ssh-key-2022-01-14"
```

设置完成后，在 **Ubuntu** 使用以下命令：

```
sudo apt-get update
sudo apt-get upgrade

sudo apt install python3-pip

pip3 install --upgrade pip    //因为ubuntu系统已经默认安装pip3,这边要更新一下！
pip3 install requests    //亲测过程，只使用命令：pip install requests
pip3 install oci
python3 oci_auto.py    //该命令必须到当前文件夹下打开终端后输入！
```

如果您看到这一点，则表示脚本已成功运行。

![](https://www.louishe.com/wp-content/uploads/2022/03/oracle-vps-free-2.png)

脚本运行成功（图片来源网上）

可能需要几天的时间才能为您提供一个免费的位置。当他成功创建虚拟机时，脚本将退出并返回一条消息。

**补充20220326：** 从运行脚本开始，到注册成功，本人亲测时长为一个月左右，成功注册时间如下图。

![](https://www.louishe.com/wp-content/uploads/2022/03/oracle-vps-free-1.jpg)

注册成功

然后再到Oracle Cloud后台验证一下是否已经申请到实例了。

![](https://www.louishe.com/wp-content/uploads/2022/03/oracle-vps-free-3.png)

登录后台验证成功

*   创建 VM 后，转到实例，选择新创建的实例。
*   向下滚动到**资源**。选择**附加的 VNIC**。单击新创建的 VNIC。（默认的VNIC随脚本一起创建成功！我们只需要点击进入就可以）

![](https://www.louishe.com/wp-content/uploads/2022/03/oracle-vps-free-4.png)

单击进入脚本创建好的VNIC

单击进入附加的VNIC后，下拉找到**IPv4地址**选项。

![](https://www.louishe.com/wp-content/uploads/2022/03/oracle-vps-free-5.png)

编辑IPv4地址

*   向下滚动到**资源**。选择**IPv4 地址**。**编辑**并选择**临时公共 IP**。单击**更新**。

![](https://www.louishe.com/wp-content/uploads/2022/03/oracle-vps-free-6.jpg)

生成临时公共IP

然后就有了上图获得的公共IP地址了。通过IP和之前保存的私钥连接到服务器就可以。

**备注：** 中间出现一个小插曲，就是我第一次申请了一个临时IP地址，尝试连接并没有成功（检测过IP的22端口是开启的），还重启了一次服务器。后来重新更换了一次IP，成功登录SSH。

[Oracle 虚拟服务器（VPS）更换 IP](https://www.louishe.com/2022/01/17/doc-11528.html)

**备注2：** 最后再提醒一下，务必在Oracle Cloud后台开放几个端口，如果未开启，会导致搭建的web应用无法正常访问！

![](https://www.louishe.com/wp-content/uploads/2022/03/oracle-vps-free-8.png)

开启几个通用的端口

如何操作？如下图：

![](https://www.louishe.com/wp-content/uploads/2022/03/oracle-vps-free-7.png)

端口开启操作方法

安装成功后，需要在Oracle VPS上部署（宝塔/小皮）web环境推荐阅读：[https://www.youtube.com/watch?v=g7sP33QtuxM&t=245s](https://www.youtube.com/watch?v=g7sP33QtuxM&t=245s)

因为我是选择的Oracle VPS**映像是:** Oracle-Linux-8.5-aarch64-2022.01.27-0（该镜像的内核是 **Centos** ）。其实很简单，就 **2** 行命令：(具体参考网站：[https://www.bt.cn/new/download.html](https://www.bt.cn/new/download.html))

```
sudo -i   //切换到管理员权限
yum update -y   //更新
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```

等待6分钟安装成功！