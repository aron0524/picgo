### ZSH

[zsh (opens new window)](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)可以提高终端使用体验，是命令行终端必装软件，下面介绍在 MAC 与 UBUNTU 中的安装方法

**Mac**

在 mac 上还是建议使用 item 做为命令行终端，先安装 xcode。

```text
# 如果没有 brew 命令请自行安装 https://brew.sh/
brew install zsh zsh-completions

chsh -s /bin/zsh

# 如果没有 port 命令，需要先安装  https://www.macports.org/install.php
# 安装后需要执行 export PATH=/opt/local/bin:/opt/local/sbin:$PATH

sudo port install zsh zsh-completions
```

**ubuntu**

```text
# 安装zsh
sudo apt install zsh

# 查看版本号，检测安装是否成功
zsh --version

# 设置默认shell
chsh -s $(which zsh)

# 注销帐号后执行，查看当前shell是否是zsh
echo $SHELL
```

**centos**

安装软件

```text
sudo yum update && sudo yum -y install zsh
```

设置当前用户默认 shell

```text
chsh -s /bin/zsh
或
sudo usermod -s $(which zsh) 用户名
```

注销帐号后执行，查看当前 shell 是否是 zsh

```text
echo $SHELL
```

### [#](https://doc.houdunren.com/效率提升/4 zsh.html#oh-my-zsh)oh my zsh

[oh my zsh (opens new window)](https://ohmyz.sh/)是管理 ZSH 的配置，并提供了丰富的插件

![eastwood](https://doc.houdunren.com/assets/img/eastwood.c03c4d1c.jpg)

**软件安装**

因为是国外资源可能下载不成功，多试几次

```text
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

如果上面的不行，试试下面的命令

```text
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

如果还是不能下载，就再试试下面的命令

```text
sh -c "$(curl -fsSL https://gitee.com/shmhlsy/oh-my-zsh-install.sh/raw/master/install.sh)"
```

**初始配置**

第一次安装后，需要注销后重新登录。之后会显示如下初始配置界面，选择`q`退出

![Snipaste_2019-10-23_15-20-32](https://cdn.jsdelivr.net/gh/aron0524/picgo@main/doc/202301181602974.png)

主要在配置文件 `~/.zshrc` 中修改设置。

> 有些软件比如 LINUXBREW，的配置荐在`~/.profile`文件中，安装了 zsh 就需要复制到 `~/.zshrc ｀文件头部

## [#](https://doc.houdunren.com/效率提升/4 zsh.html#修改主题)修改主题

ZSH 拥有[丰富的主题 (opens new window)](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)（大叔使用的主题是`bira`）

### [#](https://doc.houdunren.com/效率提升/4 zsh.html#设置主题)设置主题

修改配置文件 `~/.zshrc` 中的 `ZSH_THEME` 来设置使用的风格

```text
ZSH_THEME="bira"
```

更新配置也可以选择重起终端

```text
source ~/.zshrc
```

### [#](https://doc.houdunren.com/效率提升/4 zsh.html#mac)Mac

Mac 也可以使用上面方式设置主题，但向军大叔使用的是 item 所以直接使用 item 的风格更好些。

```text
Preferences > Profiles > Colors > Color Presets
```

### [#](https://doc.houdunren.com/效率提升/4 zsh.html#颜色风格)颜色风格

有时 `zsh-autosuggestions` 插件的提示颜色看不清，可以通过修改颜色处理。打开配置文件 `~/.oh-my-zsh/custom/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh` 修改以下配置项

```text
typeset -g ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=12'
```

更新配置也可以选择重起终端

```text
source ~/.zshrc
```

## [#](https://doc.houdunren.com/效率提升/4 zsh.html#插件扩展)插件扩展

### [#](https://doc.houdunren.com/效率提升/4 zsh.html#配置文件)配置文件

- 插件需要修改 `~/.zshrc` 配置文件中的 `plugins`配置段
- 在目录 `~/.oh-my-zsh/plugins`中默认存在了大量插件，只要添加到配置项中即可。
- 更新配置后使用`source ~/.zshrc`命令重新加载配置

### [#](https://doc.houdunren.com/效率提升/4 zsh.html#历史记录)历史记录

这个插件需要单独下载

```text
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

下载后在配置文件的 `plugins` 选项的最后面添加即可

```text
plugins=(git history history-substring-search node npm wd web-search last-working-dir zsh-autosuggestions)
```

### [#](https://doc.houdunren.com/效率提升/4 zsh.html#大叔配置)大叔配置

下面是我的的`~/.zshrc`文件的配置内容

```text
plugins=(git history history-substring-search node npm wd web-search last-working-dir zsh-autosuggestions vi-mode)
```

### [#](https://doc.houdunren.com/效率提升/4 zsh.html#命令提示)命令提示

通过安装 [incr (opens new window)](https://mimosa-pudica.net/zsh-incremental.html)插件就可以实现以下命令提示效果

![img](https://doc.houdunren.com/assets/img/zsh.a9a9cc11.gif)

首先下载插件

```text
cd

wget https://mimosa-pudica.net/src/incr-0.2.zsh
```

加载插件

```text
source incr*.zsh
```

\##　其他设置

### [#](https://doc.houdunren.com/效率提升/4 zsh.html#默认编辑器)默认编辑器

在 `~/.zshrc`或`~/.bashrc`配置文中件添加以下指令。下例是将默认编辑器修改为 vscode

```text
export EDITOR=code
```