---
title: Git学习笔记
date:
tags:
  - Git
categories:
  - [Git]
---

# Git学习笔记

## Git——世界上最先进的分布式版本控制系统

​		**学习git，可以去Git菜鸟** [Git菜鸟教程](https://www.runoob.com/git/git-tutorial.html)

## 一、Git简介

### 1、Git的诞生

Git是Linus花了两周时间自己用**C语言**写了一个分布式版本控制系统

### 2、分布式VS集中式

- 集中式版本控制系统，版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆
  - 最大缺点：必须联网才能工作
  - 其次，安全性较低，当中央服务器出了问题，所有人都没法工作
- 分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库。当你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了
  - 优点：避免了集中式的缺点

## 二、在windows上安装Git

从Git官网直接[下载安装程序](https://git-scm.com/downloads)，然后按默认选项安装即可

安装完成后，在开始菜单里找到“Git”  —>“Git Bash”，会跳出一个命令行窗口，说明Git安装成功

安装成功后，还需要最后一步设置，在命令行输入：

```xml
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

>因为Git是分布式版本控制系统，所以每个机器都必须自报家门：你的名字和你的Email地址

## 三、版本库的创建

版本库又称仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都可以跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以还原

假如你想管理某个目录里面的所有文件

你需要通过命令行cmd进入该目录下，通过`git init`命令把这个目录变成Git可以管理的仓库：

```xml
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

> 如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文

- 你会发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了

- 如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见

## 四、工作去和暂存区

工作区（Working Directory）：就是你在电脑里能看到的目录。

版本库（Repository）：工作区有一个隐藏目录.git，这个不算工作区，而是git的版本库。Git的版本库里村里很多东西，其中最重要的就是称为stage（或者交iudex）的暂存区。还有Git为什么自动创建的第一个分支master，以及指向master的一个指针叫HEAD

![Git工作流程](/img/Git工作流程.png)

## 五、远程仓库

### 1、从远程仓库克隆到本地库

[GitHub](https://github.com/)这个网站就是提供Git仓库托管服务的，只要注册一个GitHub账号，就可以免费获得Git远程仓库

远程库创建好后，可以用命令`git clone`克隆一个本地库

```xml
$ git clone git@github.com:perfect-code-hzy/supermall.git
```

> 注意把Git库的地址换成你自己的，然后进入你想要创建到的目录看看，已经有对应的文件了

### 2、项目从本地库推送到github远程库管理

1. github上创建git仓库为supermall
2. 创建项目：vue create supermall
3. `git init`初始化仓库
4. `git status`//查看当前库的状态
5. `git diff` //查看修改内容
6. `git add .` //把所有文件提交到暂存区，即本地库
7. `git commit -m '初始化项目'` //即此次提交的说明

以上是提交到本地仓库，以下是提交到github远程库

9. `git remote add origin https://github.com/JiangH156/JiangH156.github.io.git`//将本地仓库关联到远程仓库

10. `git remote -v` // 列出已关联的库，带有url

11. `git remote show JiangH156.github.io` //查看某一指定库

12. `git pull --rebase origin master` //当出现错误原因是github中的README.md文件不在本地代码目录中,通过该命令进行代码合并

13. `git push -u origin master` // 提交到远程库

14. 撤销修改

    场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`
    场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD < file >`，就回到了场景1，第二步按场景1操作
    场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，**不过前提是没有推送到远程库**

15. 删除文件

​		`git rm file` 用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

## 六、分支管理

你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作

#### 1、创建和合并分支（重点）

使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。

- 创建dev分支并切换到dev分支

```xml
git checkout -b dev
// 或者
git switch -c <dev>
```

- 创建并切换相当于两条命令（略）

```
git branch dev
git checkout dev 或者 git switch <dev>
```

- 查看分支

```
git branch
* dev 
  master
```

> 当前分支前面会标一个*号

- 当dev分支的工作完成，我们就可以合并分支到主分支

```
git checkout master    		//切换会master分支
git merge dev 		   		//把dev分支的工作成果合并到master分支上
git push 			   		//推送到远程仓库
```

- 远程仓库保存login分支

```
git checkout login			//切换login分支
git push -u origin login 	//推送到云端origin仓库的login分支
```

- 合并完成后，删除dev分支

```
git branch -d dev
```

#### 2、合并分支冲突（略）

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

用`git log --graph`命令可以看到分支合并图

#### 3、分支策略（略）

在实际开发中，我们应该按照几个基本原则进行分支管理：

- master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活
- 干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本
- 合并分支时，加上–no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并

```
$ git merge --no-ff -m "merge with no-ff" dev
```

- 合并后，我们用`git log`看看分支历史

```
$ git log --graph --pretty=oneline --abbrev-commit
*   e1e9c68 (HEAD -> master) merge with no-ff
|\  
| * f52c633 (dev) add merge
|/  
*   cf810e4 conflict fixed
...
```

#### 4、bug分支

当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它，但是，等等，当前正在dev上进行的工作还没有提交，但由于工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？

Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作
```
$ git stash
```

然后，用`git status`查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地**创建分支来修复bug**

```xml
切换到master分支
$ git checkout master
创建并切换修复bug的分支
$ git checkout -b issue-101
然后修复bug
$ vi readme.txt
提交文件
$ git add readme.txt
$ git commit -m 'fix bug 101'
切换到master分支
$ git checkout master
$ git merge --no-ff -m "merged bug fix 101" issue-101
删除修复bug的分支
$ git branch -d issue-101
$ git checkout dev
查看刚才存放的工作现场
$ git stash list
恢复工作现场
$ git stash pop
```

工作现场恢复的两个方法：

- 用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；
- 用`git stash pop`，恢复的同时把stash内容也删了

同样的bug，要在dev上修复，我们只需要把4c805e2 fix bug 101这个提交所做的修改“复制”到dev分支。

> 注意：我们只想复制4c805e2 fix bug 101这个提交所做的修改，并不是把整个master分支merge过来

为了方便操作，Git专门提供了一个cherry-pick命令，让我们能复制一个特定的提交到当前分支：

```xml
$ git branch
* dev
  master
$ git cherry-pick 4c805e2
```

#### 5、Feature分支

添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

一般删除用`-d`，有时会删除不掉。如要丢弃一个没有被合并过的分支，需要使用大写的`-D`参数

```
$ git branch -D feature-1
```

#### 6、多人协作

1. 分支推送
   - master分支是主分支，因此要时刻与远程同步；
   - dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
   - bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
   - feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
2. 工作模式
   - 首先，可以试图用`git push origin < branch-name >`推送自己的修改；
   - 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
   - 如果合并有冲突，则解决冲突，并在本地提交；
   - 没有冲突或者解决掉冲突后，再用`git push origin < branch-name >`推送就能成功！
   - 如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to < branch-name > origin/< branch-name >`。

#### 7、Rebase

多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后push的童鞋不得不先pull，在本地合并，然后才能push成功。这样会造成查看提交历史会出现很多分支。

- rebase操作可以把本地未push的分叉提交历史整理成直线；
- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比

## 七、标签管理

Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的

#### 1、创建标签

- 首先，切换到需要打标签的分支上，打标签即可

```xml
$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'
$ git tag v1.0
查看所有标签
$ git tag
v1.0
```

- 可以查看历史提交的commit id，为其打上标签

```xml
$ git log --pretty=oneline --abbrev-commit
12a631b (HEAD -> master, tag: v1.0, origin/master) merged bug fix 101
4c805e2 fix bug 101
e1e9c68 merge with no-ff
f52c633 add merge
cf810e4 conflict fixed
```

- 比方说要对`add merge`这次提交打标签，它对应的commit id是f52c633，敲入命令：

```xml
$ git tag v0.9 f52c633
查看标签信息：
$ git show <tagname>
还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
```

> 注意：标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。

#### 2、操作标签

创建的标签都只存储在本地，不会自动推送到远程。打错的标签可以在本地安全删除

```xml
删除标签
$ git tag -d v0.1
推送某个标签到远程
$ git push origin <tagname>
一次性推送全部尚未推送到远程的本地标签
$ git push origin --tags
如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
$ git tag -d v0.9
$ git push origin :refs/tags/v0.9
要看看是否真的从远程库删除了标签，可以登陆GitHub查看
```



## 九、Github和Gitee使用（重点）

#### 1、Github上搜索项目技巧

![Github搜索项目技巧](/img/Github搜索项目技巧.png)

## Git常用命令

### 链接 —> https://blog.csdn.net/halaoda/article/details/78661334

(注：该篇参考自https://blog.csdn.net/Best_arrangement/article/details/107745523)