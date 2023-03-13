# win11优化-集成PowerToys和Everything



> ### win11优化-集成PowerToys和Everything以实现mac的“聚焦”搜索

mac上自带的“聚焦”搜索，可以模糊匹配文件、应用程序、文稿、新闻，甚至也可以进行计算和单位的转换，搜索效率非常高，使用也非常方便，用command+空格键即可调出或隐藏。该功能十分有用。

![img](https://pic2.zhimg.com/80/v2-95a6999dfb1eb831b6be7c21b42c0d39_720w.webp)

大家都知道windows上面的第三方应用非常多，肯定有类似的第三方工具。因为我更喜欢免费和开源的，便找到了PowerToys+Everything的组合。

PowerToys是微软官方发布的一组增强工具，大家有兴趣的话，

可以到[https://learn.microsoft.com/zh-cn/windows/powertoys/](https://link.zhihu.com/?target=https%3A//learn.microsoft.com/zh-cn/windows/powertoys/)官方网址看看介绍，

也可以到[https://github.com/microsoft/PowerToys](https://link.zhihu.com/?target=https%3A//github.com/microsoft/PowerToys)这个地址去下载试用一下。

实用的功能还是比较多的，包括颜色选取、批量修改文件名、ORC文字提取等。

**本次主要介绍PowerToy Run和Everything的集成，以实现macOS的“聚焦”功能。**

### 基于windows11，先下载以下三个软件

1、PowerToys v0.63.0 （[https://github.com/microsoft/PowerToys](https://link.zhihu.com/?target=https%3A//github.com/microsoft/PowerToys)）

2、Everything 1.4.1（[https://www.voidtools.com/zh-cn/](https://link.zhihu.com/?target=https%3A//www.voidtools.com/zh-cn/)）

3、Everything-0.63.0-x64.zip （[https://github.com/lin-ycv/EverythingPowerToys](https://link.zhihu.com/?target=https%3A//github.com/lin-ycv/EverythingPowerToys)）

### 然后再安装PowerToys和Everything，并设置为开机启动

### 其次把Everything-0.63.0-x64.zip解压缩后，将Everything目录copy到Everything安装目录的插件地址，即C:\Program Files\PowerToys\modules\launcher\Plugins目录下。

![img](https://pic1.zhimg.com/80/v2-f11c861760853a0900359772a176aa04_720w.webp)

### 最后，需要重启PowerToys，到PowerToys Run下，找到Everything插件，并为开启状态。

如下图

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202301191403445.webp)

使用时按ALT+space快捷键，即可调出PowerToys Run

查询文件时，不使用@也可以实现搜索，而使用@开头会只执行Everything的插件功能。

![img](https://pic2.zhimg.com/80/v2-8fb96b05fe56218db746cae2a6f1128d_720w.webp)

最后，如果出现“是否安装了Everything"报警，确保已安装并启动了Everything。

![img](https://pic4.zhimg.com/80/v2-5c675403fcb99b531378ec6cf61bee33_720w.webp)

<details class="details-reset details-overlay details-overlay-dark" id="jumpto-line-details-dialog" style="box-sizing: border-box; display: block;"><summary data-hotkey="l" aria-label="Jump to line" role="button" style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none; transition: color 80ms cubic-bezier(0.33, 1, 0.68, 1) 0s, background-color, box-shadow, border-color;"></summary></details>