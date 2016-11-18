---
title: Git实操
date: 2016-11-13 17:46:29
tags:
- git实操
comments: true
categories:
- 工具箱
---


>### 感谢廖雪峰老师的教程，以下学习内容大部分是抄录廖老师官方网站上面的内容，实操多于理论，不管你们能不能看懂，反正我是懂了😝

***

>## 在Linux上安装Git

`yum install git`

 安装完成后进行设置：

```
git config --global user.name "your name"
git config --global user.email "email@."

```
>## 创建版本库

`git init`

>## 把文件添加到版本库

* 第一步：把文件添加到仓库 
  `git add 文件名或目录`

* 第二步: 把文件提交到仓库
 `git commit -m "本次提交说明"`

>## 查看仓库当前状态

`git status`
`git diff` 查看修改了什么内容
`git log` 显示从最近到最远提交的日志
2b93ef99一串是commit id(版本号) ，是SHA1计算出来的一个非常大的数字，用十六进制表示。  

>## 版本回退

`git reset` 
Git中，用HEAD表示当前版本，上一个版本是HEAD^,上上一个版本就是HEAD^^，当然往上100个版本可以写成HEAD-100
回退到上一个版本`git reset --hard HEAD^`
`git reflog` 记录每一次命令

版本号只需要填写前几位就可以了，Git会自动去找，当然也不能只写前一两位。
可通过`git reset --hard commit_id` 在版本的历史之间穿梭。

>## 工作区和暂存区

* 工作区：电脑里能看到的目录，一个文件夹就是一个工作区

* 版本库：工作区有个隐藏目录.git ，这个不算工作区，而是Git的版本库。
Git版本库里最重要的为stage的暂存区，Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD

 * 把文件往Git版本库里添加的时候，是分两步执行的：
   * 1：git add，把文件添加到暂存区
   * 2: git commit,把暂存区的所有内容提交到当前分支
创建Git版本库时，Git自动为我们创建了唯一一个master分支。

>## 管理修改

* Git跟踪并管理的是修改，而非文件。
git commit只负责把暂存区的修改提交。

* 撤销修改
`git checkout -- file` 把工作区的file修改撤销，让文件回到最近一次git commit或 git add时的状态

`git reset HEAD file` 可以把暂存区的修改撤销掉，重新放回工作区

>## 删除文件

`rm file` 删除工作区文件
`git checkout -- file` 从版本库恢复最新版到工作区，会丢失最近一次提交后修改的内容
`git rm file ` 然后 `git commit`  删除版本库文件

>## 远程仓库

Git是分布式版本控制系统，同一个git仓库，可以分布到不同的机器上。

就算是在同一台电脑上，只要在不同的目录，也可以克隆多个版本库，只是这样做没任何意义。

github 就是你的远程仓库

* 关联仓库
```
git remote add origin https://github.com/你的github账户名/仓库名.git
git push -u origin master
```
然后输入你的github用户名和密码

origin是git默认远程仓库名字，可以修改

把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支master推送到远程。
加上`-u`参数，git不但会把本地master分支内容推送到远程新的master分支，还会关联起来，在以后推送或者拉取时就可以简化命令。

只要本地作了提交，就可以通过命令
`git push origin master`
推送至github

>## 从远程库克隆

`git clone https://github.com/你的github账号名/仓库名.git`

>## 分支管理

每次提交，git都把它们串成一条时间线，这条时间线就是一个分支，在git里，这个分支叫主分支，即master分支，HEAD不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

创建分支
`git checkout -b 分支名字`
-b参数表示创建并切换。相当于两条命令:
```
git branch 分支名
git checkout 分支名
```

`git branch` 可以列出所有分支，当前分支前面会标一个*号

`git checkout 分支名` 切换分支

`git merge 分支名` 合并指定分支到当前分支。

`git branch -d 分支名` 合并完成后，可以删除分支

>## 解决冲突

当Git无法自动合并分支时，必须先解决冲突，然后再提交，合并完成。
`git log --graph` 命令可以看到分支合并图

>## 分支管理策略

* `git merge --no-ff -m "说明" 分支名` --no-ff参数，表示禁用Fast forward模式，不会丢失分支信息。

* master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活。

* 干活在新建分支（例子：dev）上，新建分支(dev)是不稳定的，到某个时候，比如1.0版本发布时，再把新建分支合并到master上，在master分支发布1.0版本。

* 小伙伴们每个人都在新建分支上干活，每个人都有自己的分支，时不时的往dev分支上合并就可以了。

* Git分支十分强大，在团队开发中应该充分应用。加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并看不出来曾经做过的合并。

>## Bug分支

每个Bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。
`git stash` 把当前工作现场“储藏”起来，等恢复现场后继续工作
`git stash list` 查看储藏起来的工作现场
`git stash apply` 恢复工作现场，但是恢复后，stash内容并不删除，需要使用`git stash drop`来删除
`git stash pop` 恢复的同时把stash内容也删除

>## Feature分支

添加一个新功能时，和修复Bug类似，新建一个feature分支，在上面开发，完成后，合并，然后删除feature分支
`git branch -D 分支名` 强行删除分支

>## 多人协作

`git remote` 查看远程库的信息
`git remote -v` 显示更详细的信息

* 推送分支
把该分支上的所有本地提交推送到远程库，推送时，要指定本地分支
`git push origin master`
如果要推送其他分支，比如dev，就改成：
`git push origin dev`
  * master 分支是主分支，因此要时刻与远程同步
  * dev 分支是开发分支，团队所有成员都要在上面工作，也需要与远程同步
  * bug 分支只用于在本地修复bug，没必要推送到远程上
  * feature 分支是否推送，取决于小伙伴合作在上面的开发

>## 标签管理

tag是一个让人容易记住的有意义的名字，它跟某个commit绑在一起

* 创建标签
切换到需要打标签的分支上，`git tag <name>` 就可以打一个新标签
例如`git tag v1.0`
`git tag` 查看所有标签

默认标签是打在最新提交的commit上的，给历史提交的commit id打标签`git tag <name> <commit id>`

`git shou <tigname>` 按字母排序列出标签信息

`git tag -a指定标签名 -m指定说明文字` 例如`git tag -a v0.1 -m "说明" commit id`

`git tag -s <tagname> -m "说明"` 用PGP签名标签

* 操作标签
`git tag -d v0.1` 删除本地标签
`git push origin <tagname> ` 推送某个标签到远程
`git push origin --tags` 一次性推送全部尚未推送到远程的本地标签
删除远程标签，需要先从本地删除，然后从远程删除。
远程删除标签:`git push origin :refs/tags/<tagname>`

>## 使用GitHub

* 在GitHub上，可以任意Fork开源仓库
* 自己拥有Fork后的仓库的读写权限
* 可以推送pull request给官方仓库来贡献代码

>## 自定义Git

`git config --global color.ui true` 让Git显示颜色

* 忽略特殊文件
在Git工作区的根目录下创建一个特殊的`.gitignore` 文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件
GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore
忽略文件的原则是：
* 忽略操作系统自动生成的文件，比如缩略图等；
* 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
* 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。
最后把`.gitignore`提交到git
`git add -f <file>` 强制添加到Git

>## 配置别名

`git config --global alias.st status` 简写命令`git status` 为`git st`

(完结)
