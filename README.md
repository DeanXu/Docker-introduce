全面了解Docker
=====================
<a name="About-Docker"></a>
----------
关于Docker
---------

Docker是一个开源工具，能自动化部署应用作为一个轻量级的，便携的，独立的容器，几乎能跑在任何地方。

Docker的容器能将任何负载压缩，能保持一致性跑在几乎任何服务器上。一个开发者在笔记本上建立和测试的一个容器，能跑在测试环境，生产环境，虚拟机上，一个什么都没有的服务器，OpenStack集群，公用的电脑等等上面。

Docker的一般使用在以下几点：
>- 自动化打包和部署应用
>- 创造一个轻量级的，私人的 PAAS 环境
>- 自动化测试和连续的 整合/部署
>- 部署WEB应用，数据库和后端服务

<a name="Table-of-contents"></a>
----------
内容列表
----------
>- [关于Docker](#About-Docker)
>- [内容列表](#Table-of-contents)
>- [背景](#Background)
>- [为什么关注Docker(针对开发者)](#Why-Should-I-Care-1)
>- [为什么关注Docker(针对运营人员)](#Why-Should-I-Care-2)
>- [Docker有哪些主要的特性](#What-Main-Features)
>- [Docker最基本的函数有哪些](#What-are-the-Basic-Docker-Functions)
>- [容器是怎么工作的？(它和虚拟机有什么区别)](#How-Do-Containers-Work)
>- [Docker 和 dotCloud的关系是什么？](#asdf)
>- [使用Docker的一些好方式](#asdf)
>- [更多的一些你想知道的内容](#asdf)

<a name="Background"></a>
----------
背景
----------
15年前，几乎所有的应用的编写，都使用已经被定义好的服务堆栈和部署在一个庞大的专有的服务器上。今天，开发者建立和组合一个应用，必须要为这些应用准备去发布到各种环境下面，像公共环境，本地环境，甚至虚拟机的环境下。

<div style="text-align:center;">
    <img width="100%" src="https://github.com/DeanXu/Docker-introduce/blob/master/evolution_of_it.jpg?raw=true">
</div>
图1：IT的演变

这张图给我们展示了以下几个意思：
>- 在不同服务器和不同依赖关系，存在不利的交互
>- 通过不同硬件，迅速部署和发布的挑战性。一个集群的不同的服务器在不同类型的硬件条件下，发布时管理起来看起来是个不可能完成的任务。

<div style="text-align:center;">
    <img width="100%" src="https://github.com/DeanXu/Docker-introduce/blob/master/the_challenge.jpg?raw=true">
</div>
图2：多样化堆栈和多样性硬件环境的挑战

或者看一下下面的矩阵图，我们能看到这些组合会是一个巨大的数字，是应用/服务 和 硬件环境的排列组合， 这些都是我们每一次写或者重写一个应用需要去考虑的。这创造了一个非常困难的局面，不管是写程序的开发者还是需要保证操作环境可扩展、安全、高性能的运维人员。

<div style="text-align:center;">
    <img width="100%" src="https://github.com/DeanXu/Docker-introduce/blob/master/matrix.jpg?raw=true">
</div>
图3：动态堆栈和动态硬件环境创造了一个N乘N的矩阵

我们怎么来解决这个问题？全球化的运输是一个好的参照物。在1960年之前，大部分货物运输的过程。托运人和搬运工都会担心不同类型的货物之间会发生互相损坏（比如：一堆铁锹在运输时，有可能倒下压坏同时在运输的一袋香蕉）。同样的，将不同货品做分类的运输也是非常痛苦的一件事情。有些需要被转运的货物在运输途中，会在一个港口卸下来，等待相同类型的货物一起重新装到指定的火车、货车或者其他运输工具上。一路上，很多货物被损坏，也有很多的货物被偷盗。不同的运输机制和不同的货物组成了一个N乘N的矩阵。

<div style="text-align:center;">
    <img width="100%" src="https://github.com/DeanXu/Docker-introduce/blob/master/analogy.jpg?raw=true">
</div>
图4：比对：1960年之前的运输

幸运的是，这个问题已经解决，一个标准化的运输集装箱可以解决这个问题。任何类型的货物，不管是开心果，还是保时捷。都能被集中打包放入一个标准的运输集装箱内。这个集装箱在运输途中是封闭不可以打开的,直到将它运输到目的地。这整个集装箱看做一个个体，装载，卸下，堆放，运输，有效的解决长距离的运输带来的问题。在运输过程中，从轮船到火车，再到卡车，都可以通过起重机（吊车）,形成流程自动化。不需要管集装箱里面的东西。许多人都相信，运输集装箱在运输工具和一般的全球物流方面会发起一场革新。今天，全球有1800万个集装箱，搬运量占全球运输的90%。

<div style="text-align:center;">
    <img width="100%" src="https://github.com/DeanXu/Docker-introduce/blob/master/standard_container.jpg?raw=true">
</div>
图5：解决运输瓶颈的是标准化的集装箱

以某种程度来说，Docker可以被看做一个代码方面 的集装箱综合运输系统。

<div style="text-align:center;">
    <img width="100%" src="https://github.com/DeanXu/Docker-introduce/blob/master/docker_container.jpg?raw=true">
</div>
图6：软件运输的解决方案也是一个标准化的集装箱系统

Docker 能让任何的应用和它的依赖打包成为一个轻量级的，便携的，独立的一个集装箱。集装箱有标准的运作模式，因此可以方便自动化。他们被设计成能跑在几乎所有LINUX服务器上的容器。一个开发者在笔记本上建立和测试的一个Docker容器，能跑在测试环境、生产环境、虚拟机、新买的服务器、OpenStack集群、公共环境、或者是以上的组合的服务器群上。

换句话说，开发者可以搭建他们的应用仅仅一次，就能保证让这个应用保持一致的跑在任何地方。运营人员可以将他们的服务器配置一遍，就能跑任何应用。

<a name="Why-Should-I-Care-1"></a>
----------
为什么关注Docker(针对开发者)
---------
#### 构建一次 可以跑在任何环境下

“Docker 引起了我的兴趣，因为它可以做到简单的环境隔离和可重复性。我可以把代码在一个环境跑起来，打个包，然后就可以在任何机子上面再次跑这段代码。而且，是通过一种类似虚拟机机制d的主机,使得代码可以跑在独立的环境下。更另人兴奋的是，任何东西看起来都是 这么快速和简单。”

<a name="Why-Should-I-Care-2"></a>
----------
为什么关注Docker(针对运营人员)
---------
#### 配置一次 可以跑任何代码

>- 使整个生命周期更高效，更一致，可重复性更高
>- 提高开发者的代码质量
>- 排除开发、测试、生产以及自定义环境的不一致
>- 支持职责分离
>- 在持续的发布和持续的整合新系统的情况下，可以有效的提高开发速度和代码的可靠性
>- 因为Docker容器非常轻量级，高性能，不付费，方便部署，可移植性强

<a name="What-Main-Features"></a>
----------
Docker有哪些主要的特性
---------

将Docker和运输的集装箱做主要特性的对比是个很好的方法。（看以下表格）

/         | 物理集装箱 | Docker
--------- | ----- | -----
无关内容  | 集装箱几乎支持所有类型的货物 | 能压缩任何负载和依赖
无关硬件  | 标准化的尺寸和交接使得集装箱可以通过货船火车货车运输，用起重机交接不需要换一个容器或者打开集装箱 | 使用操作系统的基本体（像LXC）能一致的跑在几乎任何硬件下，不需要对硬件做额外的修改
内容隔离和相互作用 | 不需要关心铁锹会砸坏香蕉。集装箱可以一起堆放一起运输 | 资源、网络和内容的独立避免了依赖问题
自动化 | 标准化使得自动化装载卸货和移动变得方便 | 使用标准的操作指令去跑start/stop/commit/search等等。对运营人员：CI、CD、自动化测试、hybrid clouds
高效 | 不需要打开不需要改动什么，高效的点对点的方式 | 轻量级，几乎没有启动的消耗，高效的移植性和操控性
职责分离 | 发货人只需要关心箱子内部的事情，托运人只需要关心箱子外部的东西 | 开发者只需要关心代码层面，运营人员只需要关心服务器的基础环境

图表7: 主要的Docker 特性

从技术方面来看，一个更多的特性，请看以下几点：

>- 文件系统分离：每一个进程容器跑在完全分离的root权限的文件系统下。
>- 资源分离：系统资源（像CPU、内存）能被指定的分配给每一个进程容器,使用cgroups。
>- 网络分离：使用一个虚拟的接口和IP地址，每一个进程容器跑在它自己的网络命名空间。
>- copy-on-write：root文件系统用copy-on-write方式进行创建，使得发布显得非常快捷，节省了内存和硬盘
>- 日志：每一个进程容器的标准数据流（标准输出/标准错误/标准输入）会被收集并且实时或者分配检索记录下来
>- 改变管理：改变一个容器的文件系统能被提交到一个新的镜像，可以被重用去创造更多的容器。不需要模板或者管理配置的要求。
>- 交互性Shell: Docker 会分配一个伪终端，在所有的容器里都可以使用标准的输入，for example to run a throwaway interactive shell.

<a name="What-are-the-Basic-Docker-Functions"></a>
----------
Docker最基本的函数有哪些
---------

Docker使得建立、修改、发布、搜索、运行容器变得简单方便。下面的这张图表将给你一个来自Docker基础的直观的感受。对于Docker来说，一个容器包含应用和所有的依赖。容器可以被手动的创造，或者如果一个源码仓库如果包含一个DockerFile的话，可以自动创建。随后，这些修改保存到一个基本的Docker镜像被提交到一个新的容器，通过commit方法推送到一个Central Registy。
在一个Docker Registry(包含公共或者私有),Docker容器能用Docker Search被找到。容器能用pull命令从Registry上被拉下来，能被运行，开始，停止等等操作。使用Docker跑命令，显然，一个在运行的命令行,能是你的服务，公共实例，也可以是他们的组合。

<div style="text-align:center;">
    <img width="100%" src="https://github.com/DeanXu/Docker-introduce/blob/master/docker_functions.jpg?raw=true">
</div>
图表8：基本的Docker函数

想拿到更多的函数列表，请访问：[http://docs.docker.io/en/latest/commandline/](#http://docs.docker.io/en/latest/commandline/)

Docker 运行的3种方式：
>- 在你的Linux主机，作为一个守护进程去管理LXC容器（sudo docker -d）
>- 使用守护进程的REST接口，在命令行界面运行（sudo run ...）
>- 作为一个客户端仓库，用来分享你建立的Docker容器（docker pull,cocker commit）

<a name="How-Do-Containers-Work"></a>
----------
容器是怎么工作的？(它和虚拟机有什么区别)
---------

一个容器包含一个应用和它的依赖包。 在主机的操作系统里，为每个独立的用户提供独立的进程。
这和传统的虚拟机不一样。传统虚拟机（像VMWare/KVM/Xen?EC2）通过硬件虚拟化来创造一整个虚拟系统。每一个虚拟机内的应用不仅仅包含这个应用的一些类库代码（这个应用可能只有10几M）,而且还包含一整个操作系统（将近10G的容量A）。

下面的图片给你展示2者的不同
<div style="text-align:center;">
    <img width="100%" src="https://github.com/DeanXu/Docker-introduce/blob/master/docker_vm.jpg?raw=true">
</div>
图表9：Docker容器 VS 传统虚拟机

因为所有的容器分享一个操作系统（包含适当的文件和类库），他们显然会比虚拟机更小一些，使得他们可以存在100多个虚拟的系统在一个主机上（而不像一个严格限制数量的虚拟机）。此外，因为他们利用了主机的操作系统，重启一个虚拟的系统部意味着重启操作系统，因此，Docker容器相比之下显的更便捷和高效。

Docker容器，
