---
title: QFramework 使用指南 (2020) - Res Kit（2）模拟模式与非模拟模式
iscopyright: true
comments: true
lang: cn
tags:
  - Unity
  - Framework
  - QFramework
  - QFramework.ResKit
  - AssetBundle
categories:
  - QFramework
abbrlink: qf_reskit_02
date: 2019-09-08 23:00:59 
author: 凉鞋 | 凉鞋的笔记：liangxiegame.com
---


<center>
<a href="https://tdou.cc/cn/qf_reskit_01.html">上一阶段</a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://tdou.cc/cn/qframework.html">回到总览</a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://tdou.cc/cn/qf_reskit_03.html">下一阶段</a>
</center>


在上一篇，介绍了 Res Kit 的基本使用，相信大家已经体会到了 Res Kit 的简便之处了。

在这一篇，我们试着探讨一下 Res Kit 的设计背后原理。

## AssetBundle 的不便之处
在使用 Res Kit 之前，相信大家多多少少接触过 AssetBundle。 有的童鞋可能是在项目中用过 AssetBundle，有的童鞋可能只是简单学习过 AssetBundle。总之，AssetBundle 在不通过 Res Kit 使用之前，总结下来就两个字：麻烦。

AssetBundle 麻烦在哪里呢？

首先 AssetBundle，需要打包才能在运行时加载资源。而打包需要我们写编辑器扩展脚本，在编辑器扩展脚本中还要处理平台和路径相关的逻辑。

在运行时，还需要根据平台和路径去加载对应的 AssetBundle。

这些操作想想就比较头痛。

既然 AssetBundle 这么麻烦，我们为什么还要用 AssetBundle 呢？

因为 AssetBundle 可以给项目带来更好的性能，而且 AssetBundle 支持热更新。

有了这两个优势，AssetBundle 就成了很多项目的必然选择。

而 Res Kit 中，为了解决频繁打包的问题，引入了一个概念：模拟模式（Simulation Mode）。

### 模拟模式（Simulation Mode）
在上一篇，我们已经接触了模拟模式（Simulation Mode）。

**什么是模拟模式？**

顾名思义，就是模拟加载 AssetBundle 的模式，这里只是模拟，并没有真正去加载 AssetBundle，而是去加载 Application.dataPath 目录下的资源，也就是 Assets 目录下的资源。

**这样做有什么好处呢？**

好处就是每当有资源修改的时候，就不用再打 AB 包了，就可以在运行时加载到修改后的资源。

如果是非模拟模式下，每当有资源修改时，就需要再打一次 AB 包，才能加载到修改后的资源。

所以一个模拟模式，解决了频繁打 AB 包的问题，从而在开发阶段提高我们的开发效率。

那么在使用 Res Kit 的时候，模拟模式对应的阶段是开发阶段，那么非模拟模式对应的是什么阶段呢？

答案就是真机阶段。

## 开发阶段、真机阶段
开发阶段、真机阶段并不是 Unity 提供的概念，而是笔者在迭代 Res Kit 中提出的两个概念。

这两个概念很容易理解：
* 开发阶段：开发逻辑的阶段，需要编写大量的逻辑，大部分情况下都在 Unity Editor 环境下开发。
* 真机阶段：需要在真机上运行的阶段，这个阶段主要是做大量的测试或者真正发布了。

相信有点规模的项目都会分阶段出来的，比如开发阶段、测试阶段、生产阶段等等，大家理解起来应该不难。

接下来简单分析一下开发阶段、真机阶段的特点。

**开发阶段**
在开发阶段，开发者需要写大量的逻辑，而且资源的目录还没有稳定，一般在开发过程中会有很大的变化。
如果每次资源的修改都需要打 AB 包的话，会非常影响开发进度。

**真机阶段**
真机阶段，一般就是一个版本的逻辑都写完了，只需要做一些测试和 debug 工作。在这个阶段，资源目录都稳定了，不需要做很大的调整。

在真机阶段，每次打 App 包之前，只需要 Build 一次 AB 即可。

当然，在 Unity Editor 环境中，可以取消勾选模拟模式，这样在 Unity Editor 环境下可以加载真正的 AssetBundle 包。

在上一篇文章所说的，拥抱各个开发阶段指的就是为开发阶段、和真机阶段做了考虑。

此篇的内容就这些。

## 小结
* 开发阶段：
  *  模拟模式
* 真机阶段：
  * 每次打 App 包之前，打一次 AB 包。
  * 可以在 Unity Editor 环境下，取消勾选模拟模式，这时在运行时加载的资源则是真正的 AssetBundle 资源

* 转载请注明地址：凉鞋的笔记：liangxiegame.com。
* 任何问题欢迎到 QQ 群：623597263 交流。


<center>
<a href="https://tdou.cc/cn/qf_reskit_01.html">上一阶段</a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://tdou.cc/cn/qframework.html">回到总览</a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://tdou.cc/cn/qf_reskit_03.html">下一阶段</a>
</center>
