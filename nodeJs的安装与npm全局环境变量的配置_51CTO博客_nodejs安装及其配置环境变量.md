# nodeJs的安装与npm全局环境变量的配置_51CTO博客_nodejs安装及其配置环境变量
nodeJs的安装与npm全局环境变量的配置
======================


©著作权归作者所有：来自51CTO博客作者编程小石头的原创作品，请联系作者获取转载授权，否则将追究法律责任

> 最近在做小程序开发时，有用到云函数，而云函数就是用node.js写的，所以其中难免会用到一些node类库。用node类库就必选在电脑上安装node.js环境，并且配置npm命令的环境变量。用mac电脑，这些基本上都是自带的，不用安装和配置。但是大多数同学都是window电脑，所以今天就来教大家如何在window电脑上安装node.js并且配置npm命令

一，下载node包

这里推荐大家直接到官网下载：[ https://nodejs.org/zh-cn/download/](https://nodejs.org/zh-cn/download/)  
![](https://s2.51cto.com/images/blog/202108/06/a89a2543a7cd72eed875863b654bcf4d.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)

二，安装node包

*   1，下载好以后直接双击安装即可，然后点击下图所示的next  
    ![](https://s2.51cto.com/images/blog/202108/06/f4ec733f572fc915a776edc3918125d6.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    
*   2，接受协议，点击next  
    ![](https://s2.51cto.com/images/blog/202108/06/0aea64ebc9c3c8a7c749b4d596ff6a7d.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    
*   3，选择安装目录，然后点击next  
    这里的安装目录一定要记清楚，后面会用到。  
    ![](https://s2.51cto.com/images/blog/202108/06/fd3455c8bac7a58a6f131a61d3f4d018.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    
*   4，选择安装选项  
    ![](https://s2.51cto.com/images/blog/202108/06/34878f33b2b4c8d27b13126a40b0d39b.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    

| 选项 | 说明 |
| --- | --- |
| Node.js runtime | 表示运行环境 |
| npm package manager | 表示npm包管理器 |
| online documentation shortcuts | 在线文档快捷方式 |
| Add to PATH | 添加到环境变量 |

全部保持默认，点击next即可

*   5，这里可以不勾选，直接点击next即可  
    ![](https://s2.51cto.com/images/blog/202108/06/f9722adf88e8047fd7ed0adb53fee5f7.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    
*   6，点击install  
    ![](https://s2.51cto.com/images/blog/202108/06/108fcc0fd1c3a537f17dd16c99e39338.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
      
    然后等待安装  
    ![](https://s2.51cto.com/images/blog/202108/06/e509af5c56acbf76c9138a7c33c433cf.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    
*   7，安装完成，点击finish  
    ![](https://s2.51cto.com/images/blog/202108/06/b81b4b700b3684400885a49811b8a484.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    

三，验证安装

win+R快捷键调出下图所示  
![](https://s2.51cto.com/images/blog/202108/06/be7a2828d90558f42c56038aa15bb9f1.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
  
输入cmd然后回车，进入dos命令行。  
输入node -v 如果出现下图所示，代表安装成功  
![](https://s2.51cto.com/images/blog/202108/06/d8b2624f9d1f286a93c19fc02886197b.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
  
然后输入npm -v 通常会出现下面错误  
![](https://s2.51cto.com/images/blog/202108/06/5f9dbd021d31ead4c65cb04858976e7f.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
  
这就代表我们npm全局环境变量没有配置，接下来就教大家如何配置npm环境变量。

四，npm环境变量的配置

*   1，配置环境变量  
    我的电脑->右键->属性->高级系统设置->高级->环境变量  
    ![](https://s2.51cto.com/images/blog/202108/06/5b79aee197bd45718e4ee3cb8d799aac.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    
*   2，点击PATH,然后点击编辑  
    ![](https://s2.51cto.com/images/blog/202108/06/9247d87630a01d305d061af00e64aa0c.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    
*   3，把我们的node安装目录追加到path里，前面用 ; 分割  
    ![](https://s2.51cto.com/images/blog/202108/06/054d763a195493f35a9c129a9175de4a.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    

设置完后，不要忘记点确定。

*   4，然后重新win+R ->cml–>打开dos命令行，输入npm -v  
    ![](https://s2.51cto.com/images/blog/202108/06/23b8b4cca81c014d818c3e0c1a77a8f0.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
      
    如上图所示，出现版本号，就代表npm全局环境变量配置完成。

五，（选学）把配置到别的盘

重要事情说三遍： 这里可以不用配置，这里可以不用配置，这一步非必须

*   再强调下，其实前面四步已经满足我们的需求了，这个第五步可以不用配置了。

我之所以写出来，是因为我们以后所有的node类库都是默认下载到c盘。通过npm root -g 可以看到。我的node类库都是存在c盘。有时候window电脑存过多的东西在c盘，会影响电脑运行速度。所以我决定把node类库都存在我的d盘里。  
![](https://s2.51cto.com/images/blog/202108/06/4bee72b22272fb6affb30888058bc0ec.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)

*   1，首先在d盘node的安装目录下配置创建两个文件如下图  
    ![](https://s2.51cto.com/images/blog/202108/06/0212e37af63cc3a9af6b8c214ac1f48b.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
      
    还记得上面的第二步的第3点吗，如下图。我这里选择的是d盘里的install目录下的node。  
    ![](https://s2.51cto.com/images/blog/202108/06/3ab05b281e641968a6857845837be73b.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    
*   2，然后下面命令

登录后复制

```
`npm config set prefix "D:\install\node\node_global"
npm config set cache "D:\install\node\node_cache"` 

*   1.
*   2.


```

注意：这里的 D:\\install\\node是我的node安装目录，你要替换成你自己的。  
执行完以后在输入npm root -g 可以看到我们的目录已经变了  
![](https://s2.51cto.com/images/blog/202108/06/4333478e97d46342b6a292f9d2861ab0.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)

*   3.把D:\\install\\node\\node_global配置到环境变量的PATH下，如下图  
    ![](https://s2.51cto.com/images/blog/202108/06/3d735b6e97c83e11ebd30b55d88a80b6.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
    
*   4，验证  
    如我们想安装request类库  
    ![](https://s2.51cto.com/images/blog/202108/06/1bb36d7736add1a360e1648e7783d20d.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
      
    可以看到我们的D:\\install\\node\\node_global目录下已成功的安装了request类库  
    ![](https://s2.51cto.com/images/blog/202108/06/3e326457eddcd60da9f48566f996117a.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=/format,webp/resize,m_fixed,w_1184)
      
    这样我们以后在下载的类库，就直接存到d盘里了，不会占用c盘空间了
