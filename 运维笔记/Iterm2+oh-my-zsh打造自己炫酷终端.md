**iTerm2 官网**

https://iterm2.com/

- iTerm2 是一款完全免费，专为 Mac OS 用户打造多命令行应用。

- 安装完成后，在/bin目录下会多出一个zsh的文件。

- Mac系统默认使用dash作为终端，可以使用命令修改默认使用zsh：chsh -s /bin/zsh

- 如果想修改回默认dash，同样使用chsh命令即可：chsh -s /bin/bash

- Zsh 是一款强大的虚拟终端，既是一个系统的虚拟终端，也可以作为一个脚本语言的交互解析器。


**iterm2 安装**

下载地址：

https://iterm2.com/downloads.html

**iTerm操作快捷键**

- command + t：新建窗口 

- command + d：垂直分屏，

- command + shift + d：水平分屏。

- command + ] 和command + [ 在最近使用的分屏直接切换.

- command + alt + 方向键：切换到指定位置的分屏。

- command + 数字：切换标签页。

- command + 方向键：按方向切换标签页。

- shift + command + s：保存当前窗口快照。

- command + alt + b：快照回放。很有意思的功能，你可以对你的操作根据时间轴进行回放。可以拖动下方的时间轴，也可以按左右方向键


**创建一键登录服务器**

````shell
set user lhadmin
set host 10.231.143.218
set password cd93c5f4cf^Keo90
spawn ssh $user@$host
expect "*assword:*"
send "$password\r"
interact
expect eof
````



**iTerm2配置添加：**   expect ~/.ssh/SIT02-10.231.143.184

**Oh My Zsh 介绍**

Oh My Zsh 官网：

https://ohmyz.sh/

Oh My Zsh 是一款社区驱动的命令行工具，它基于 zsh 命令行，提供了主题配置，插件机制，已经内置的便捷操作。给我们一种全新的方式使用命令行。

**oh my zsh 安装**

方式1

````shell
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
````

方式2

````shell
`sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`
````

方式3

````shell
zsh -c "$(curl -fsSL 'https://host.mintimate.cn/fileHost/download/MTM1NjkzNzI1OTIxMDg0NjIwOQ==')"
````

**卸载命令**

````shell
uninstall_on_my_zsh
````

**更换主题** vi ~/.zshrc

````shell
ZSH_THEME="macovsky-ruby"    "steeef"
````

**安装语法高亮插件**

````shell
cd ~/.oh-my-zsh/custom/plugins git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
````



**自动补全插件**

````shell
git clone https://github.com/zsh-users/zsh-autosuggestions.git
````



**启用插件**

````shell
vi ~/.zshrc ......... plugins=( git
  zsh-autosuggestions
  zsh-syntax-highlighting )
......... source ~/.zshrc
````





