# Win10上运行Docker

1. 前言
Docker最近推出了可以运行在Win10和Mac上的稳定版本，让我们赶紧来体验一下。 Docker发布Mac和Windows 的目标非常简单——开发者可以更加简单方便地在研发机器上使用Docker。下面是此次版本所改进的地方：

更快更可靠——在本地开发环境上，使用虚拟监控程序（hypervisors）就可以植入每个操作系统（无需VirtualBox）；
改进了Docker工具集成——开发者可以把所有的Docker工具绑定在本地应用程序上；
改进开发流程——大量的装备可用于代码和数据，还可以更加方便地访问在本地网络上运行的运行容器，IDEs支持在线调试，使代码迭代更快速更轻松；
支持企业网络，Mac和Windows版本轻松访问企业VPN；
所有的新功能都可以在Docker 1.12引擎上使用；
支持自动更新，无论是稳定版还是测试版。


2. 安装准备
需要的条件为： 64bit Windows 10，开启Hyper-V 

2.1 下载Docker for Windows
从官网的下面地址可以下载

https://download.docker.com/win/stable/InstallDocker.msi 

2.2 开启win10的Hyper-V
控制面板 -> 程序 -> 启用或关闭Windows功能 -> 选中Hyper-V

转自：http://www.aiweibang.com/yuedu/137913473.html

3.内存不够启动不了解决
Not enough memory to start Docker
You are trying to start docker but you don't have enough memory.
Free some memory or change your vm settings.


http://blog.csdn.net/zdy0_2004/article/details/52084452