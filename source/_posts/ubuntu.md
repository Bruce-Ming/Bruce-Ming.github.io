---
title: ubuntu杂记
date: 2019-10-17 22:14:42
categories:
- 服务器相关
tags: 
- ubuntu 
- vscode 
- win10 
- nginx 
- nvm
---
## win10下子系统ubuntu安装

在win10商店直接搜索安装,安装好运行时会报错

```bash
Installing, this may take a few minutes...
Installation Failed!
Error: 0x8007019e
Press any key to continue...
```

原因:未开启子系统支持服务.win10命令行管理员模式输入以下代码

```bash
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

回车,输入Y,等待重启,重新打开安装就行了.
注:win10下ubuntu系统的文件夹在以下目录(括号中换成你自己用户的文件夹)

``` bash
C:\Users\(Administrator)\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs
```

## 在ubuntu安装nginx,和使用nginx

* apt-get install nginx (安装nginx)
* sudo service nginx start/stop/reload/restart (启动nginx等操作)
* nginx -h 查看相关命令

## 安装nvm,配置node开发环境,参考[nvm的github](https://github.com/nvm-sh/nvm)

``` bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh | bash
```

或者

``` bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh | bash
```

切记:安装好关闭命令行重启生效.
常用命令:nvm install/ls/use/run/exec/alias default/-h/-v

## vscode配合win10下ubuntu的开发扩展remote-wsl

### 连接本机刚刚配置好的ubuntu

安装好后左下角会有个><标志,点击可以启动连接ubuntu,做远程开发,但是需要使用root账户登录才行,否则会有权限问题. powersell管理员模式输入以下命令即可

```bash
ubuntu config --default-user root
```

### 配置远程linux系统 (无linux服务器未验证)

在vscode的远程资源管理器中新建配置文件

``` bash
Host 连接的主机的名称，可自定

Hostname 远程主机的IP地址

User 用于登录远程主机的用户名

Port 用于登录远程主机的端口

IdentityFile 本地的id_rsa的路径
```

具体配置及操作参考 [VS Code Remote SSH配置](https://zhuanlan.zhihu.com/p/68577071)



