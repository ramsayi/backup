---
title: Powershell终端代理问题
tags:
  - Powershell
categories:
  - 踩坑记录
  - 终端
abbrlink: 3fc4dfb9
date: 2022-10-22 18:34:18
---

### Windows 终端的选择

首先得说明我使用的终端是 `Windows PowerShell`，并不是 `cmd`，甚至于我使用的是 `win11` 中的 `Terminal`，不过 `Terminal`是集成终端，我使用的默认界面是 `Windows PowerShell`。所以归根结底，使用的终端是 `Windows PowerShell`。但是我都会提到相关的设置。

### cmd 设置代理

由于 cmd 终端的广泛流传，我先将 cmd 代理设置的方式列出：

```bash
set http_proxy=http://127.0.0.1:7890
set https_proxy=http://127.0.0.1:7890
```

每次在打开的 cmd 终端中执行这两段命令，会让终端中的所有命令走端口代理软件的代理。（注意：此处非走代理服务器，而是走代理软件，还会通过代理规则的判断）

当然这是临时命令，重新代理终端需要重新输入。如果想要永久设置代理，我建议是使用自定义配置，使每次代理 cmd 窗口时，运行如上命令。

1. 新建一个 `cmd_init.cmd`，将上面的命令放入其中。
2. 打开注册表：`win+R` -> 输入 `regedit` 后运行
3. 找到 `HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\`，在文件夹下，新建字符串值 `AutoRun`，数据的值是一个绝对路径，路径指向新建的 `cmd_init.cmd`，可以将这个文件放在 C 盘根目录，即路径为 `C:\cmd_init.cmd`。
4. 重新打开终端，你会看到命令行会先运行这两条命令，而不需要你自己输入。

### PowerShell 设置代理

为 `PowerShell` 设置代理的方式类似，命令如下：

```bash
$Env:http_proxy="http://127.0.0.1:7890"
$Env:https_proxy="http://127.0.0.1:7890"
```

当然这也是临时命令，重新代理终端需要重新输入。如果想要永久设置代理，我建议是使用自定义配置，使每次代理 `PowerShell` 窗口时，运行如上命令。

1. 在 `PowerShell` 窗口中运行如下指令：

```bash
if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
notepad $PROFILE
```

2. 默认会使用记事本打开一个文件，在文件中加入上面设置代理的命令，保存关闭即可。

上面的配置文件在 `此电脑\文档\WindowsPowerShell` 下，文件名为：`Microsoft.PowerShell_profile.ps1`， 这个文件的内容会在 `PowerShell` 的每次运行时使用。（注意不要修改文件位置，除非你明白这样操作的目的）

上述的自定义配置方法，便于设置和修改，故为我所推崇，如果你使用网上的永久设置，我想可能会有各种问题，不如这样设置的直观，当然观点仅供参考。

3. 设置不代理的地址

```bash
$Env:NO_PROXY="localhost,127.0.0.1,::1"
```

### 为 `git` 设置代理

不得不说，为终端设置代理主要是为 `git` 设置全局代理，这里给出单独设置的方法。

```bash
git config --global https.proxy http://127.0.0.1:7890
git config --global https.proxy https://127.0.0.1:7890
```

这里给出取消设置代理的方法，防止端口需要切换。

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

