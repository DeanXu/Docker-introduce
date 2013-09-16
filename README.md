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
>- [为什么关注Docker(针对运营人员)](#asdf)
>- [Docker有哪些主要的特性](#asdf)
>- [Docker最基本的函数有哪些](#asdf)
>- [容器是怎么工作的？(它和虚拟机有什么区别)](#asdf)
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
