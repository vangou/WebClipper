# 【AI加持】只用了几天，我已经忘记其他同类工具！必备生产力工具！像ChatGPT 一样去提问
                            【AI加持】只用了几天，我已经忘记其他同类工具！必备生产力工具！像ChatGPT 一样去提问                                           

【AI加持】只用了几天，我已经忘记其他同类工具！必备生产力工具！像ChatGPT 一样去提问
==============================================

原创 我是小斐老师 [小斐实战](javascript:void(0);)

**小斐实战** 

微信号 xfsz2023

功能介绍 小斐实战，每一篇文章都是实战记录。

_2023-04-17 09:08_ _发表于江苏_

收录于合集

#生产力工具 31 个

#mac 3 个

#工具集 102 个

#命令行 3 个

#开源 11 个

> 微信公众号：\[小斐实战\] 关注技术分享，资源分享。问题或建议，请公众号留言。

只用了几天，我好像已经忘记其他命令行工具的外观了。它是一款新近推出的命令行工具，结合了 Rust 和 GPT 的双层缓冲区，被称为「21世纪的终端」，对传统终端进行了嘲讽和超越。

　　每天我都需要依赖命令行工具来提高生产力。在 Windows 平台上，我通常使用 MobaXterm，而在 macOS 上则更喜欢使用 iTerm。虽然一直觉得这些工具存在一些问题，但我从未深入思考过，直到遇到了 Warp。

传统命令行工具的构建受到 TTY 的限制，这种限制带来了如下影响：

*   键盘优先：传统命令行工具通常忽略鼠标、触摸板等非键盘输入方式，而且光标移动也只能使用方向键等键盘操作。
    
*   离线操作：许多命令行工具通常只在离线环境下使用，例如机房中的操作系统命令行窗口。
    
*   隐私担忧：命令行工具天生带有一层隐私和安全方面的担忧，人们普遍认为命令行工具是私人领域。
    

　　由于这些原因，传统命令行工具出厂设定通常非常简单和基础，功能更新也会受到发行版版本的限制而变得缓慢。与此同时，第三方命令行工具也没有摆脱这些限制。而 Warp 似乎天生就在试图打破这些“桎梏”。

**关注公众号，每天都有不一样的精彩内容**

* * *

　　Warp 的一个核心理念变革是采用现代 IDE 的思路来开发命令行工具。首先要摆脱仅支持键盘交互的负担，毕竟这已不再是唯一可以与系统交互的 TTY 工具。

### **命令行上的文本编辑**

输入命令时，可以在任何位置使用鼠标，就像编辑文本一样方便。

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnyBicx1J8vyJ9HG0xxkT3p39jCttn18F4pdp1P0QvoWORBRJqJ1Lvt5Bg/640?wx_fmt=gif)

可以在任何位置移动光标、进行选择、删除、复制和粘贴等操作。

![](https://mmbiz.qpic.cn/mmbiz_png/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnyb8nbLCSNSBwPWOEuglicrwBQ3Ja2L725Pj07f7bvbcUZGiae6enXem0Q/640?wx_fmt=png)

支持多行和列选择编辑，这些小小的功能大大提高了在多个服务器上操作命令的效率。

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVny9COGAia3sLICKEvo1uRDZDU5Azl42L6Q5QW5dVNlIhicnnK1rvAxymIQ/640?wx_fmt=gif)

可以在当前屏幕下直接使用 Command+F 搜索屏幕内容，更加便捷。

![](https://mmbiz.qpic.cn/mmbiz_png/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnyPucPIVqsQpV89Gtra2XL7LbDjUaCEq83H7uQ9ThbJEtMS3PaO3vHww/640?wx_fmt=png)

对于文件，可以使用本地文本编辑器快速打开，直观的操作可以提高效率。

### **开箱即用的补全、推荐和纠错**

Tab键无处不在，它可以自动补全命令，同时提供提示。这些细节的积累，使我们对Tab键产生了一种隐含的信任，似乎Tab键就像是命令行的小助手一样存在。

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnyyb4nGpickiaAPrhuEsKMDHZyILXano7Xx1hTHtoJtK60bAYMyic9fvwGw/640?wx_fmt=gif)

对于输错的选项和参数，Tab键也可以一键补全。

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnyzfttibeicbYfotMsJbEFE1sDjcM21ia1MjAAibJvm3LueseuOATaGvNlicQ/640?wx_fmt=gif)

最棒的地方是，这些功能都是开箱即用的，甚至可以在连接到远程服务器的环境中使用。

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnyxQ6vDNRk04IicXulcSrWRicKic6308vdQmI2rGu8kLdXbic6ZKL4nj0VGw/640?wx_fmt=gif)

### **Command Palette 统一入口**

快捷键 Command + P 和 Command + K 为各个应用软件和网页提供了统一的入口。这种设计非常符合用户的需求，因为它减少了使用软件的难度。有时候，记忆快捷键本身就是一种负担。更糟糕的是，我们可能会怀疑自己的记忆是否正确。

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnyzKJCTX9g3XgsgJHP4UL3QXKWP3w8vicwOE9ClwibaEicKM9lJAftmqnyQ/640?wx_fmt=gif)

在使用 Warp 这个命令行工具时，如果您不确定触发条件，可以随时使用 Command Palette 来执行后续操作。它会为您提供兜底的解决方案。

**关注公众号，每天都有不一样的精彩内容**

### **Workflow**

Warp的目标是将命令行操作流程系统化为Workflow，并通过开源仓库提供共建共享的方式。此外，Warp还提供了一个插件库分享页面，类似于迷你应用商店。

![](https://mmbiz.qpic.cn/mmbiz_png/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnypOu0E0YeRuUXALZ6P0icgb2MM0l8PGhlKMXCLYgcReBCueaEK8TYunQ/640?wx_fmt=png)

以下是Warp官网提供的一个最简单的Workflow示例，使用易于阅读的YAML格式：

```properties
name: Example workflow
command: echo {{string}}
arguments:
  - name: string
    description: The value to echo
```

### **创建你的第一个 Workflow**

以下是一个相对复杂的 Workflow 脚本示例，其中命令的具体内容可以忽略不计。

```properties
# 需要手动创建 workflows 目录
mkdir -p ~/.warp/workflows
# 创建 workflows 文件
vim  ~/.warp/workflows/create-topic-under-jason-ftns.yaml
```

Warp 会自动将格式正确的 YAML 文件解析为 Workflow，并存储在 ~/.warp/workflows 目录下。

在 YAML 的配置文件中，命令会存放在 Command 字段中，并且可以通过打上标签（tag）进行分组呈现。以下是一个完整的例子：

```perl
# The name of the workflow.
name: Create a topic and grant privileges to produce and consume to role "pulsar-consumer-test".
# The corresponding command for the workflow. Any arguments should be surrounded with two curly braces. E.g `command {{arg}}`.
command: |-
  alias pulsar-shell='JAVA_HOME=/Users/jason/.sdkman/candidates/java/17.0.6.fx-librca/ /Users/jason/Documents/workspaces/client/apache-pulsar-shell-2.11.0/bin/pulsar-shell'
  tenant=jason; namespace=ftns; topic={{topic_name}}; partition_num=3; user_role="pulsar-consumer-test"
  pulsar-shell -e "config use pulsar-azure"
  pulsar-shell -e "admin topics create-partitioned-topic --partitions $partition_num $tenant/$namespace/{{topic_name}}"
  pulsar-shell -e "admin topics list-partitioned-topics $tenant/$namespace"
  pulsar-shell -e "admin topics grant-permission --role $user_role --actions produce,consume $tenant/$namespace/{{topic_name}}"
  pulsar-shell -e "admin topics permissions $tenant/$namespace/{{topic_name}}"

# Any tags that the workflow should be categorized with.
tags:
  - pulsar
# A description of the workflow.
description: Create a topic and grant privileges to produce and consume to role "pulsar-consumer-test".
# List of arguments within the command.
arguments:
    # Name of the argument within the command. This must exactly match the name of the argument
    # within the command (without the curly braces).
  - name: topic_name
    # The description of the argument.
    description: The topic name under 'jason/ftns' you want to create grant permissions.
    # The default value for the argument.
    default_value: test
# The valid shells where this workflow should be active. If valid for all shells, this can be left empty.
# See FORMAT.md for the full list of accepted values.
shells: []
```

我们可以使用快捷键（Ctrl+Shift+R）唤醒 Workflow 面板，或从命令面板中触发。

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnyTqHg5As5MkZ7hSCH2GM3PWVBJRHBhw21xeqSgCZgXcQjkAIHvdPNDQ/640?wx_fmt=gif)

从演示中可以看到，Workflow 可以简化批量操作，积累知识。虽然类似概念代码片段不是什么新鲜内容，但结合 Warp 对格式的规范，如果能够在团队协作中使用，就可以真正激发代码片段的长尾价值。

**关注公众号，每天都有不一样的精彩内容**

### **引入Block概念**

Warp 将 Notion 中块的思想引入到命令行中，目前版本能够基于块实现基本操作，例如复制命令或结果。块的概念能够很好地隔离命令之间，方便实现单个块内的功能，例如拷贝执行过的命令，而在传统的命令行工具中需要使用鼠标从左往右复制命令。

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnydLXMTkAzKVJHjlHsrnU88Shwzia8DTu9DUps9pSvlXORz46XqT6bQoQ/640?wx_fmt=gif)

未来，块可能会像 Jupyter 一样可以随意放置、拖拽以更换顺序，并支持分享和协作。  

* * *

现在，我们来到了 Warp 最引以为傲的 AI 功能演示环节。

### **AI 命令搜索**

你可以通过快捷键 Control + ~ 来触发 AI 命令搜索，支持使用自然语言提问。

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnybDib58ZW6DS35kiapYOE5AImaYxSlhGRP52AJkMU6N640HYHqtXiajgQw/640?wx_fmt=gif)

即使是不那么热门的命令，也可以很好地搜索到：

![](https://mmbiz.qpic.cn/mmbiz_png/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVny3BJO2lrwvNW1LbqS414O3QxMicf6MtmAI7QznGagPxZ6BSCFdiac5WWg/640?wx_fmt=png)

### **像 ChatGPT 一样去提问**

比如提示词如下：

```cpp
How to export a Docker image, cut it up into chunks, each smaller than 100M, and finally assemble and import it into the Docker
```

### **随时随地的提问**

![](https://mmbiz.qpic.cn/mmbiz_gif/EcCS5Fd7NewWMsPoWPDPXIF47icdUYVnypSVSG4soE2vV6DticjPvT0zqI6bdct6dIrfPWDwibaanrEwVlXjmRNlA/640?wx_fmt=gif)

在演示中，我们刻意选择了一个旧版本的 Python 并出现了报错。然后，我们寻求 AI 的帮助并提出问题。AI 很好地识别了问题，并给出了解决建议。需要注意的是，使用 AI 相关功能无需特殊的网络环境。

### **总结**

Warp 是一款功能强大的命令行工具，不仅能够提供基本的命令行操作，还能通过 Workflow 管理命令流程、积累知识，并提供 AI 智能搜索、注解等功能，让使用者更加高效地操作命令行。Warp 还在不断更新和改进中，未来也许还会提供更多实用的功能和优化，让使用者更加愉快地使用命令行工具。

### **获取工具关键词****230417**

**关注公众号，每天都有不一样的精彩内容**

### **大数据为您推荐以下内容**

[【免费！流畅！不限速】是时候卸载TeamViewer了！免费支持100 台设备！国货精品！](http://mp.weixin.qq.com/s?__biz=MzkzNjIzMTUxNA==&mid=2247486970&idx=1&sn=be48ed1cdd909039bacaba5206c81fad&chksm=c2a09acff5d713d93b42b88f65f296144eb0baa5c614af6c17866639b5b5e0c5bf3f55817f43&scene=21#wechat_redirect)  

[【无需账号+无需秘钥+直连ChatGPT】将ChatGPT集成到浏览器！速度High起来！](http://mp.weixin.qq.com/s?__biz=MzkzNjIzMTUxNA==&mid=2247486957&idx=2&sn=78f46c562740cfa537dccff16a9249da&chksm=c2a09ad8f5d713ce6eb9e0fb7ddc278461727e57d40d6950a4e641b0ee26e34d713b744cb550&scene=21#wechat_redirect)  

[【神技！速度收藏！】不用梯子也可以直接调用ChatGPT API的方法！方法简单到爆！](http://mp.weixin.qq.com/s?__biz=MzkzNjIzMTUxNA==&mid=2247486957&idx=3&sn=53ca23e52675136d708f97e43321c3be&chksm=c2a09ad8f5d713cee3bdda91187f91174112ad310f10ed523768106cc8018401c35e3a7e6667&scene=21#wechat_redirect)  

[【强烈推荐】不限速，无限空间，自动销毁，单个文件50G，无需客户端，命令行上传下载！功能太多了](http://mp.weixin.qq.com/s?__biz=MzkzNjIzMTUxNA==&mid=2247486957&idx=6&sn=d8f26b2ac09f921837323f035c43a44a&chksm=c2a09ad8f5d713ceb40cf410b9978a4dc85679b5d7c9f04d710d417b25de095e6548b433a962&scene=21#wechat_redirect)  

[【功能媲美IDM！重点还免费】这款插件让浏览器下载功能脱胎换骨！速度飕飕的~](http://mp.weixin.qq.com/s?__biz=MzkzNjIzMTUxNA==&mid=2247486957&idx=4&sn=f32806105d00020643d86226fc562130&chksm=c2a09ad8f5d713ceea039b5ddb3d035a0ba7565980ef9f8d1370ec129dcd3ef7e6ecc375246b&scene=21#wechat_redirect)  

[【惊艳！不一样的Markdown】让你告别单调的写作体验，让写作变得更加自由！](http://mp.weixin.qq.com/s?__biz=MzkzNjIzMTUxNA==&mid=2247486957&idx=5&sn=e56ff71273d5ecc81b814bb9207d4eb8&chksm=c2a09ad8f5d713ce1a80d78a8115e357f139252bbb7a9ad4bf9eea5316ae23c3ba40fef8feb7&scene=21#wechat_redirect)

预览时标签不可点

收录于合集 #生产力工具

 31个

上一篇【免费！流畅！不限速】是时候卸载TeamViewer了！免费支持100 台设备！国货精品！

喜欢此内容的人还喜欢

盘点一些小众却令人难忘的网站

盘点一些小众却令人难忘的网站

程序那些事儿

不喜欢

不看的原因

确定

*   内容质量低
*   不看此公众号

![](https://mmbiz.qpic.cn/mmbiz_jpg/mOlp9rexrO9ncKkQsWtYrzHXuMkFWibJCDE3fWCicHROCQrUsiaPEwbfnmemvqibzsKHuiafN7JpkNQDh31I4FEQvPA/0?wx_fmt=jpeg)

推荐一个在线工具箱-即时工具

推荐一个在线工具箱-即时工具

低调的路过

不喜欢

不看的原因

确定

*   内容质量低
*   不看此公众号

![](https://mmbiz.qpic.cn/mmbiz_jpg/hibJgqYHNPopBo4P4QicdVjwwKReWhgf1jwLmibTqqOB4CjUIN2c5Y4Wu7guIfcghweC8cgBQNvvibVDNs08FwHgmg/0?wx_fmt=jpeg)

学得懂的 Android Framework 教程——HAL与硬件服务之 Linux 驱动开发入门

学得懂的 Android Framework 教程——HAL与硬件服务之 Linux 驱动开发入门

元代码空间

不喜欢

不看的原因

确定

*   内容质量低
*   不看此公众号

![](https://mmbiz.qpic.cn/mmbiz_jpg/JbNtVM0Jpq3E9aoCxrEvgwdibX9icaib5Mdcs39XBsl6ibAjiaw8HwCkHWcjcfuibqfUJia4Zpa90ibEboyGibJMcKW8MuA/0?wx_fmt=jpeg)

![](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MzkzNjIzMTUxNA==&mid=2247487023&idx=1&sn=cbcf1981fda27f3e7c6a203bcfe1b909&send_time=)

微信扫一扫  
关注该公众号

[知道了](javascript:;)

 微信扫一扫  
使用小程序

[取消](javascript:void(0);) [允许](javascript:void(0);)

[取消](javascript:void(0);) [允许](javascript:void(0);)

： ， 。  视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看

该账号因违规无法跳转