---
title: Git起步
date: 2016-11-06 16:25:29
tags: 
- git起步
comments: true
categories: 
- 工具箱
---



>##  1.1 起步- 关于版本控制

版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。  
  *  本地版本控制系统RCS > 集中化的版本控制系统CVCS > 分布式版本控制系统DVCS

>##  1.2 起步- Git 简史  

linux 2002年整个项目组开始启用一个专有的分布式版本控制系统BitKeeper来管理和维护代码。到了2005年，BitKeeper商业公司同Linux内核开源社区合作关系结束，迫使Linux开源社区开发出自己的版本系统，他们对新的系统制订了若干目标：
  *  速度
  *  简单的设计
  *  对非线性开发模式的强力支持（允许成千上万个并行开发的分支）
  *  完全分布式
  *  有能力高效管理类似Linux内核一样的超大规模项目（速度和数据量）
  自2005年以来，Git日臻成熟，在高度易用的同时，仍然保留着初期设定的目标。

>##  1.3 起步- Git 基础

*  直接记录快照，而非差异比较。每次提交更新，或在Git中保存项目状态时，它主要对>当时的全部文件制作一个快照并保存这个快照的索引。如果文件没有修改，Git不再重新存
储该文件，而是只保留一个链接指向之前存储的文件。git对待数据更像是一个快照流。

*  近乎所有操作都是本地执行。
*  Git保证完整性。用以计算校验和的机制叫做SHA-1散列（hash,哈希），以此来索引，而不是文件名。  
*  Git一般只添加数据。
*  三种状态：
  *  已提交(committed) ： 数据已保存在本地数据库中。
  *  已修改(modified) ： 已修改了文件，但还没保存到数据库中。
  *  已暂存(staged) ： 对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。

*  由此引入Git项目的三个工作区域的概念：
  *  Git仓库 : git仓库目录是git用来保存项目的元数据和对象数据库的地方。从其它计算机克隆仓库时，拷贝的就是这里的数据。  
  *  工作目录 :  对项目某个版本独立提取出来的内容。从git仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改。  
  *  暂存区域 : 暂存区域是一个文件，保存了下次将提交的文件列表信息，一般在git仓库目录中。有时候也被称作“索引”，不过一般说法还是叫暂存区域。

*  基本的git工作流程如下：
  1.  在工作目录中修改文件。  
  2.  暂存文件，将文件的快照放入暂存区域。
  3.  提交更新，找到暂存区域的文件，将快照永久性存储到git仓库目录。
  *  如果git目录中保存着特定版本文件，就属于已提交状态。
  *  如果作了修改并已放入暂存区域，就属于已暂存状态。
  *  如果自上次取出后，作了修改但还没有放到暂存区域，就是已修改状态。

                    
>##  1.4 起步- 命令行 

*  命令行  可以使用命令行模式，也可以使用GUI模式，在命令行模式可以执行Git所有命令，而大多数GUI软件只实现了git所有功能的一个子集以降低操作难度。

>##  1.5 起步- 安装Git  

*  在Linux上安装
  *  二进制安装: `$ sudo yum install git`
  *  基于Debian的发行版上： `$ sudo apt-get install git`

*  在Mac上安装 最简单的方法是安装xcode command line tools，或GitHub for Mac网站上下载图形化git工具。

*  在windows上安装 官方网站下载

>##  1.6 起步- 初次运行Git前的配置

*  用户信息: 该命令只需要运行一次，之后在该系统上的任何操作，都会使用这些信息。

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
* 文本编辑器 配置默认文本编辑器，当Git需要你输入信息时会调用它。如果未配置，Git会使用操作系统默认的文本编辑器，通常是Vim。
`git config --global core.editor vi`

* 检查配置信息

 `git config --list` 列出所有Git配置
 `git config <key>` 某一项配置
  
>## 1.7 起步- 获取帮助

```
git help <verb>
git <verb> --help
man git-<verb>
```

>## 1.8 起步- 总结

你应该已经对 Git 是什么、Git 与你可能正在使用的集中式版本控制系统有何区别等问题有了基本的了解。 现在，在你的个人系统中应该也有了一份能够工作的 Git 版本。 是时候开始学习有关 Git 的基础知识了。










 
