# 树莓派 Zero USB/以太网方式连接配置教程

> 



![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021034284.jpeg)



树莓派 Zero 之所以成为一款非常棒的单板计算机并不全因为它小巧的尺寸和便宜的价格，还得益于它便捷、易用的特性。在加装了 [Zero Quick Plug](https://shumeipai.nxez.com/rpi-zero-quick-plug) 或 microUSB/USB 转换头之后，将树莓派 Zero 和电脑连接起来。树莓派 Zero 即可配置成 USB/以太网设备，这时仅需要一个 USB 接口就实现给树莓派供电的同时将它接入因特网。不再需要携带额外的电源适配器、 USB HUB和无线网卡。可以说这是迄今为止连接树莓派最简单、方便的方式！
对于 Raspbian 2016-10-5 之后的系统镜像，你只需要在系统 SD 卡上修改几处配置文件即可将树莓派配置成一个 USB/以太网设备。
这个教程基于 Windows 平台，在连接树莓派之前，你可能需要在电脑上安装 Bonjour。它允许你的电脑自动识别 USB/以太网设备，例如打印机、扫描仪以及我们需要的树莓派。Bonjour 被包含在 iTunes 与 Adobe CS 软件中，所以很可能你已经装有这个软件，如果没有，你可以在[这里单独下载](https://support.apple.com/kb/DL999?locale=en_US)安装。

#### 一、配置 CONFIG.TXT 和 CMDLINE.TXT 文件

开始刷入系统，请确认你下载的系统镜像是 2016-10-5 之后的版本。在电脑上将系统镜像写入 micro SD 卡，可以使用 Win32 Disk Imager 这个工具（[这里下载](https://shumeipai.nxez.com/download)）。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021034678.jpeg)

完成之后，在电脑上打开这个 micro SD 卡的根目录 (例如. boot(E:)) 并打开 config.txt 文件。在文件末尾添加一行 dtoverlay=dwc2。



![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021035065.png)

保存并关闭 config.txt 文件。

再打开 cmdline.txt 文件，请确认你的编辑器已关闭“自动换行”。编辑这个文件的时候不需要插入任何换行符，所有字符都在同一行。找到 rootwait，在后面插入 modules-load=dwc2,g_ether。



![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021035377.png)

保存并关闭 cmdline.txt 文件。

最后在根目录创建一个名为 ssh 的文件或目录。

好了，可以从电脑上弹出 SD 卡了。把 SD 卡插入树莓派 Zero，用 [Zero Quick Plug](https://shumeipai.nxez.com/rpi-zero-quick-plug) 或 microUSB/USB 转换头将树莓派 Zero 和电脑连接起来。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021035417.jpeg)

图中用到的这款连接部件是树莓派 Zero 多功能 USB 插头（[Zero Quick Plug](https://shumeipai.nxez.com/rpi-zero-quick-plug)），详见下图。



![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021036394.jpeg)

这时 Windows 会自动识别到树莓派，并尝试安装驱动。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021036342.jpeg)

*注意，有用户发现在 Windows 10 下设备会被识别为 COM 设备，这时请在设备管理器中更新该设备的驱动程序即可。*[驱动程序可在这里下载](https://pan.baidu.com/s/1mjQCb6S)*。*

到这里，打开 PuTTY（[这里下载](https://shumeipai.nxez.com/download)）并尝试通过 SSH 连接树莓派的地址 raspberrypi.local。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021036439.jpeg)

如果你发现可以正常连接和登录树莓派，恭喜你！下面“安装 RNDIS 驱动”的步骤可以跳过了！直接从下面“设置共享互联网连接”开始阅读。

如果在这里遇到错误提示 “Unable to open connection to raspberrypi.local. Host does not exist”, 那么你需要在电脑上安装 RNDIS 驱动。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021037248.png)

#### 二、安装 RNDIS 驱动（酌情跳过）

保持树莓派与电脑的连接，打开 Windows 的“设备管理”，在“其他设备”中找到“RNDIS/Ethernet Gadget”, 右键选择“更新驱动程序”。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021037795.jpeg)

再选择“Browse my computer for driver software”。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021037099.png)

选择“Let me pick from a list of device drivers on my computer”。



![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021037784.png)

选择“Network adapters”，下一步。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021037911.jpeg)

在 “Manufacturer” 列表中选择 “Microsoft”。在 “Network Adapters” 列表中选择“Remote NDIS Compatible Device”，下一步。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021038891.jpeg)

在弹出的对话框中选择“Yes”。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021038485.png)

安装完驱动之后，你将看到这个窗口。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021038695.png)

现在尝试用 PuTTY 连接地址 raspberrypi.local。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021038189.png)

#### 三、设置共享互联网连接

为了将电脑的互联网连接共享给树莓派，我们需要允许共享你电脑上的一个网络连接。打开“Network Connections”。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021038382.png)

你的树莓派在里面显示为 “RNDIS/Ethernet Gadget” 的设备类型，在上图示例中，名字是“Ethernet 2”。

现在你要确定用哪一个连接给树莓派访问用 （WiFi 或以太网）。这里我选择让树莓派通过电脑的“Wi-Fi”这个连接去访问互联网，所以我启用这个连接之后在右键“属性”中进行设置。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021039637.png)

选择“共享”标签。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021039014.png)

勾选“Allow other network users to connect through this computer’s Internet connection”，在下拉菜单中找到树莓派的连接名称（这里选择 Ethernet 2）。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021039607.jpeg)

WiFi 网络这时出现“Shared”标注了。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021039111.png)

现在可以重启你的树莓派并重新用 PuTTY 登录了。

登录树莓派之后，用 ifconfig 命令查看 usb0 连接可以看到网络上行和下行的流量。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021039293.png)

Ping 一下某些网站域名，确认互联网连接是否正常。

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021040894.png)

如果你用的是 Raspbian 桌面版，你可以安装一个 RDP（远程桌面协议）客户端然后在电脑上通过远程桌面（ “Remote Desktop Connection” ）客户端连接到树莓派，连接地址同样是raspberrypi.local。（[具体方法](https://shumeipai.nxez.com/2013/10/06/windows-remote-desktop-connection-raspberry-pi.html)）

![img](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202302021040619.png)

将你的树莓派 Zero 配置成 USB/以太网设备，可以仅需要一个 USB 接口就实现给树莓派供电的同时将它接入因特网。不再需要携带额外的电源适配器、 USB HUB和无线网卡。可以说这是迄今为止连接树莓派最简单、方便的方式！

另有 macOS 平台下使用这一功能的教程，[移步这里阅读](https://shumeipai.nxez.com/2018/02/20/raspberry-pi-zero-usb-ethernet-gadget-tutorial-macos.html)。