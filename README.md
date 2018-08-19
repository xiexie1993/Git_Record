# git使用

## Git 介绍

+ Git是一个分布式版本控制系统。
+ Git是根据GPL分发的免费软件。
+ Git有一个名为stage的可变索引。
+ Git跟踪文件的变化。



## 一、环境

### Andriod手机

+ 软件：Gidder、Pocket Git



### PC电脑window

+ 软件：Git 



### 环境安装

+ 1、下载软件包安装

+ 2、连接同一个网络
    在Gidder上设置开启应用设置基本参数（端口、用户名、密码、和相应权限）
         a、建立用户
         b、建仓库、分配仓库权限给用户



+ 3、客户端设置

    + a、windows7
    ~~~
        step1:安装git
        step2:进入 ~/.ssh/config (没有的话自己建立)
                方案一：（如果clone linux系统的Git会克隆不了，解决办法，方案二）
                    Host *.*.*.* 
                    KexAlgorithms +diffie-hellman-group1-sha1
                    HostkeyAlgorithms ssh-dss
                方案二：（）
                    Host *.*.*.* 
                    HostKeyAlgorithms +ssh-dss
        step3: 设置全局的用户（此步骤可不执行）
             git config --global user.name 'runoob'
             git config --global user.email test@runoob.com
        step4: 运行克隆命令  git clone  ssh://xiexie1993@192.168.31.124:2222/test.git
    ~~~

> 参考资料：
>    笔记项目随身携带-android手机git服务器：gidder
>    https://blog.csdn.net/TaylorPotter/article/details/69808733



## 二、git使用

+ Git名词解释：
    + 工作区（Working Directory） ： 就是你在电脑里能看到的目录
    + 版本库（Repository）        ： 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
    + 暂存区（stage或者叫index）  ： Git的版本库里的很多文件之一
    + Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD



+ 使用步骤
    + 创建了远程仓库
    + 例1：Android手机的Gidder创建项目
    + 例2：linux上创建项目
    + 例3：GitHub上创建项目



+ 基本使用步骤
    + 克隆项目:    git clone <url>
    + 查看日志:    git log
    + 加入跟踪:    git add .
    + 查看状态：   git status
    + 提交:        git commit -m "<massage>"
    + 推送到远程:  git push
    + 远程拉取  :  git pull



+ 常用速查

    + 创建项目操作
        + 创建本地仓库
            + git init    在本目录下创建了一个空的仓库

        + 克隆项目
            + git clone [url]
                + git clone <本地系统绝对路径>                                      克隆本地仓库,例子 执行如下命令以创建一个本地仓库的克隆版本
                + git clone ssh://xiexie1993@github.com/xiexie1993/TestPrj001.git   克隆远端服务器上的仓库,例子： 
                + git clone git://github.com/schacon/grit.git mygrit                唯一的差别就是，现在新建的目录成了 mygrit

    + 项目创建之后的操作
        + git status                                        查看本地当前项目的文件状态
            + git status -s                                    查看简报
        + git add .                                         将所有文件上传提交到本地缓存区
        + git add  xx文件                                   之将“ xx文件 ”提交到本地暂存区
        + git commit -m "版本V1.0"                          写提交时的日志/备注信息，实际提交改动，改动已经提交到了 HEAD，但是还没到你的远端仓库
        + git push <仓库地址> <master>                      提交到远程， master 换成你想要推送的任何分支 ，也可以不填，不填默认 master
        + git pull <仓库地址>                               拉取远程代码
        + 

    + 分支操作
        + git branch                                        查看本地分支
        + git branch -a                                     查看所有分支（含远程）
        + git branch -r                                     查看所有远程分支
        + git branch -vv                                    查看当前分支所属
        + git branch test                                   创建分支（本地）
        + git push --set-upstream origin v1.5               将本地分支推送提交到之前未有名为v1.5的分支的远程
        + git push origin test                              把分支推到远程分支 
        + git checkout master                               切换分支到 master
        + git checkout test                                 切换分支到 test
        + git checkout -b <本地分支别名> origin/<分支名>    创建+切换分支,检出远程分支到本地工作区
        + git merge <name>                                  合并某分支到当前分支
        + git branch -d <name>                              删除本地分支
        + git branch -r -d origin/branch-name               删除远程分支（还未提交到远程仓库，执行删除远程的，只是在本地的仓库中执行，此如果git pull 还能拉取）
        + git push origin :branch-name                      配合上一条进行删除远程分支的提交



    + 回滚
        + git checkout -- <filename>                        替换本地改动，此命令会使用 HEAD 中的最新内容替换掉你的工作目录中的文件。已添加到缓存区的改动，以及新文件，都不受影响。(注意： -- 和 文件名之间必须有空格)
        + git fetch origin                                  丢弃你所有的本地改动与提交，可以到服务器上获取最新的版本并将你本地主分支指向到它
        + git reset --hard origin/master                    丢弃你所有的本地改动与提交，可以到服务器上获取最新的版本并将你本地主分支指向到它
        + git reset --hard <commit-hash-id>                 回滚到指定的版本
        + git reset HEAD~1                                  暂存区的目录树会被重写，最后一次提交的内容会被丢弃，但是工作区不受影响。
        + git reset --hard <commit-id>                      撤消上一次commit的内容(该操作会彻底回退到某个版本，本地的源码也会变为上一个版本的内容)
        + git revert HEAD                                   撤销前一次 commit
        + git reset --hard origin/master                    拉取远程内容强制覆盖本地文件

    + 对比
        + git log --stat                                       查阅最近的提交修改
        + git log -p <filename>                                该命令可以查看某个文件与上次提交的不同之处。
        + git diff <commit-hash-id> <commit-hash-id> --stat    Git查看两个版本之间修改了哪些文件
        + git log -p -2                                        查看最近2次的更新内容
        + git show <commit-hash-id>                            查看某次commit的修改内容

    + 修改
        +  git commit --amend                                可以查看并修改到本地最后一次commit（没有提交的远程的）修改其注释信息和修改内容

    + 其他
        +
        + git diff                                          对比改动
            + git diff                                           尚未缓存的改动
            + git diff –cached                                   查看已缓存的改动
            + git diff HEAD                                      查看已缓存的与未缓存的所有改动
            + git diff –stat                                     显示摘要而非整个 diff
        + git add -i                                        交互地添加文件至缓存区
        + git log                                           查看提交的日志信息
        + git config –list                                  查看配置信息
        + git reset HEAD                                    从缓存中移除文件,取消之前 git add 添加, 例子 git reset HEAD -- 文件名
        + git rm                                            从缓存以及工作目录删除文件,这与 git reset HEAD 将条目取消缓存是有区别的。 “取消缓存”的意思就是将缓存区恢复为我们做出修改之前的样子。 默认情况下，git rm file 会将文件从缓存区和你的硬盘中（工作目录）删除



## 三、 Git使用场景例子

### 创建与克隆场景

#### 场景：创建本地仓库
+ step1:  创建目录/新建目录并进入
+ step2： git init    在本目录下创建了一个空的仓库
+ step2： git init --bare 在本目录下创建一个所谓的裸仓库，之所以叫裸仓库是因为这个仓库只保存git历史提交的版本信息



#### 场景：克隆远程主机仓库
+ git clone [url]
    + step1:  创建目录/新建目录并进入
    + step2： 执行克隆命令，例子如下：
        ~~~
        git clone ssh://xiexie1993@github.com/xiexie1993/TestPrj001.git   克隆远端服务器上的仓库,例子： 
        git clone git://github.com/schacon/grit.git mygrit                唯一的差别就是，现在新建的目录成了 mygrit
        ~~~



#### 场景：克隆本地主机仓库

+ git clone <本地系统绝对路径或相对路径>                                      克隆本地仓库,例子 执行如下命令以创建一个本地仓库的克隆版本



### 分支类场景

#### 场景： 在最新的版本基础上创建本地分支，但进行工作，最后本地合并到本地主分支中，再从本地主分支推送到远程，远程没有dev分支

+ step1： 执行命令 git pull ,拉取更新到最新版本
+ step2： 执行命令 git branch -a ，查看远程和本地所有的分支
+ step3： 执行命令 git checkout -b <branch-name> ，示创建并切换分支
> 或者 
> + step3：   执行命令 git branch  <branch-name> ，创建本地分支（注意分支名称不能和已存在的分支相同）
> + step3.1： 执行命令 git checkout  <branch-name> ，切换本地分支
+ step4:  执行命令 git branch 查看当前分支  命令会列出所有分支，当前分支前面会标一个*号。
+ step5： 查看日志，查看文件状态，提交到本地分支里的命令 还是 git log 、git add . 、git commit -m "注释内容" （注意不要git push 推送 ）
+ step6： 在切换分支后在工作区进行的增删查改文件后，分支的工作完成 合并到本地默认主分支master，要进行合并，
+ step7： 执行命令 git checkout  master ，切换回master主分支
+ step8： 执行命令 git merge <branch-name> ,将分支合并到当前分支（有了第七步就是合并到master主分支）, 没有冲突就到第九步，有的话就解决冲突
+ step9： 执行命令 git branch -d <branch-name> ，删除本地分支

> 因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。

#### 场景： 在最新的版本基础上创建本地与远程分支dev分支，并将提交与推送到dev分支中（暂不合并到主分支master中）

+ step0： 执行命令 git pull ,拉取更新到最新版本
+ 实现方式1步骤：（本地和远程都没有dev分支）
    + step1： 执行命令 git branch -a ，查看远程和本地所有的分支
    + step2： 执行命令 git branch -a 创建本地分支  
    + step3： 执行命令 git checkout -b <branch-name> ，示创建并切换分支
    + step4： 这时已经切换到 dev 分支，可在工作区进行工作（增删改查删添移），
    + step5： 执行命令 先看状态 git status -s，再 git add .确保文件加入追踪，再看状态确认 git status -s ,再提交 进行暂存区git commit -m "注释内容" （注意：git push 推送 ）
    + step6： 执行命令 git push --set-upstream origin  <branch-name> ， 将本地分支推送提交到之前未有名为<branch-name> 分支的分支的远程
    + step7： 执行step6后，在分支工作，再要提交到远程只需 git push （但要注意推送时确保所在的分支）

+ 实现方式1步骤：（本地与远程都已经有了dev分支）
    + step1： 执行命令 git checkout <branch-name>  切换到本地分支
    + step2： 
    + step3： 

### 场景

#### 场景： 将dev分支合并到master主分支中，再将本地dev和远程分支删除


### 回滚类场景

#### 场景：只将本地的工作空间里的某个文件，回滚到最后（最新）一个版本

+ step0： 执行命令  git pull  拉取最新仓库版本
+ step1： 执行命令 git checkout -- <filename>



#### 场景：只将本地的工作空间里的某所有文件，回滚到最后（最新）一个版本

+ 方法一：
    + step1： 执行命令 git log ，查看最后版本的 commit-id，
    + setp2： 执行命令 git reset --hard <commit-id>,执行完本地仓库就已回滚到该版本



#### 场景：只将本地的工作空间里的某个文件，回滚到指定版本

+ step1：执行命令 



#### 场景：只将本地的仓库回滚到某个版本

+ step0： 执行命令  git pull  拉取最新仓库版本
+ step1： 执行命令 git log ，查看版本的 commit-id，
+ setp2： 执行命令 git reset --hard <commit-id>,执行完本地仓库就已回滚到该版本



#### 场景： 删除远程的最后一次提交

+ step0： 执行命令  git pull  拉取最新仓库版本
+ step1： 执行命令  git revert HEAD^
+ step2： 执行命令  git log ,查看是否还有提交记录
+ step2： 执行命令  git push origin master -f ,-f 参数是强制提交，因为reset之后本地库落后于远程库一个版本，因此需要强制提交

> 注：一个被删除的提交会在删除30天后，且运行 git gc 以后，被永久丢弃
> 依据此命令可以回滚到最初的版本
> 在本地提交后的未删除.git重新拉取，时如果还记得commit是可以取回来的，执行 git reset --hard <commit-id>



#### 场景：将远程和本地的仓库全回都滚到之前的某个版本

+ step1： 执行命令



### 修改类场景

#### 场景：修改刚更新commit）但未提交到远程的版本

+ step1： 执行命令 git commit --amend ,执行完该命令会打开vim的编辑器界面，在默认打开的文件里，修改对应注释信息，保存（vim的使用）
+ setp2： 执行命令 git log 看是否注释信息已修改



#### 场景：修改已提交到远程的最后一版的注释信息

+ step1：

### 场景：Bug修改

+ step0：
+ step1：
+ step1：



### 合并分支类场景

#### 场景：本地更新最新代码，依据最新版本创建分支，在分支上提交更新版本，主分支无新版本时，合并（不会出现冲突）

+ step0： 执行命令  git pull  拉取最新仓库版本
+ step1： 执行命令  git checkout <branch-name>  切换到分支（没有分支的话需要创建）
+ step2： 在分支上修改，提交
+ step3： 执行命令  git checkout master  切换回主分支master
+ step4： 执行命令  git merge <branch-name>  将分支合并到主分支master
+ step5： 执行命令  git log --graph  看到分支合并图
+ step6： 执行命令  git branch -d <branch-name>  删除分支
+ step6： 执行命令  提交，推送

### 查看对比类场景

#### 场景：查看各个版本的文件变化简表

+ step0:  执行命令  git pull  拉取最新仓库版本
+ step1:  执行命令  git log --pretty=oneline --stat --graph ,可以看到各个版本和分支合并图，和对应版本的文件变化概览
+ 或 step1:  执行命令  git log --stat --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit 

#### 场景：查看某个指定文件的提交历史记录

+ step0:  执行命令  git pull  拉取最新仓库版本
+ step1:  执行命令 git log --pretty=oneline <filename>  ,会打印出来的就是针对文件的所有的改动历史，每一行最前面的那一长串数字就是每次提交形成的哈希值
+ step2:  执行命令 git show <git提交版本号/哈希值> <filename> ，可以直接查看该文件的修改详情，不要看该版本号其他文件的修改

#### 场景：查看分支合并的图

+ step0:  执行命令  git pull  拉取最新仓库版本
+ step1:  执行命令  git log --graph  ，查看分支合并图
+ 或 step1:  执行命令  git log --graph --pretty=oneline --abbrev-commit
+ 或 step1:  执行命令  git log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit ，查看分支合并图并设置成相应显示格式


### 多远程类场景

#### 场景： 提交推送时有两个地址存放仓库（只是用于备份）推送时要提交到两个地方

+ 此处操作步骤只是推送时要提交到两个地方
+ step0:  执行命令  git pull  拉取最新仓库版本
+ step1:  执行命令  git log --graph  ，查看分支合并图
+ step2:  执行命令  git remote -v 查看远程库信息
+ step3:  执行命令  git remote add <别名> <path> 关联一个新的远程库
+ step4:  执行命令  git push -u <别名> master   提交到对应的远程库 (两个库如果有不相关会出现冲突，新增远程库最好是新的空库)

#### 场景： 删除远程提交地址
+ step0:  执行命令  git remote -v 查看远程库信息
+ step1:  执行命令  git remote rm <别名> 移除现在有的远程服务器<别名>

#### 场景： 合并两个远程库（不相关）

+ 方法一：
    + step0:  down下第三方库；
    + step1:  以本地git为源，添加到当前git的remote中；
    + step2:  更新仓库，出现两个不同根的分支；
    + step3:  git checkout 两个分支，本从新命名；
    + step4:  使用gitbash, 执行 git merge remoteRepo master - -allow-unrelated-histories 进行合并；
    + step5:  git push 到远程仓库(将remoteRepo 合并到master上)。

+ 方法二：
    + step0:  down 下两个git仓库。
    + step1:  将两个git仓库在本地checkout。
    + step2:  若要将repo1 merge到repo2上，需要执行 git - -rebase repo2 repo1, 
    + step3:  其意义为：将repo2 作为repo1的新基线。
    + step4:  执行此操作，需要将当前branch设置为：repo2
    + step5:  如下： repo1: svn_master,repo2:git_master

## 命令详解

* git log [<options>] [<revision range>] [[--] <path>]

    + 用法例子：
        + git log          会列出所有历史记录，最近的排在最上方，显示提交对象的哈希值，作者、提交日期、和提交说明。
        + git log --graph  命令可以看到分支合并图。
        + git log -p       按补丁显示每个更新间的差异，比下一条- -stat命令信息更全
        + git log --stat： 显示每次更新的修改文件的统计信息，每个提交都列出了修改过的文件，以及其中添加和移除的行数，并在最后列出所有增减行数小计

* git reflog 

* git checkout

* git branch

* git reset

* git revert

* git tag

* git show

* git config

* git rebase

* git stash

* git add

* git rm

* git mv

* git pull

* git push

* git commit

* git init

* git clone

* git remote

* git fetch

* git archive

> 详细参考 
> [Git - git-log Documentation](https://git-scm.com/docs/git-log)
> [git log命令全解析，打log还能这么随心所欲！](https://www.cnblogs.com/bellkosmos/p/5923439.html)
> [linux命令在线中文手册 git](http://linux.51yip.com/search/git)

### 问题与解决办法记录

+ windows中git status中文文件名编码问题解决
    + 原因：  
    + 解决办法： 执行命令 git config --global core.quotepath false 将git配置变量 core.quotepath 设置为false，就可以解决中文文件名称在这些Git命令输出中的显示问题,


## 参考资料

+ [Git 基础 - 取得项目的 Git 仓库](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E5%8F%96%E5%BE%97%E9%A1%B9%E7%9B%AE%E7%9A%84-Git-%E4%BB%93%E5%BA%93)

+ [Git教程 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743256916071d5996b3aed534aaab22a0db6c4e07fd0000)

+ [git - 简易指南](http://www.bootcss.com/p/git-guide/)

+ [Git详细使用教程](https://blog.csdn.net/tgbus18990140382/article/details/52886786)

+ [Git-查看远程分支、本地分支、创建分支](https://www.cnblogs.com/yongdaimi/p/7600052.html)

+ [git如何合并远程2个分支](https://blog.csdn.net/tmacsky/article/details/78795894)

+ [Git撤销&回滚操作](https://blog.csdn.net/ligang2585116/article/details/71094887)

+ [Git Pro深入浅出（二）](https://blog.csdn.net/ligang2585116/article/details/51816372#t7)

+ [git代码回滚的几种方式](https://segmentfault.com/a/1190000011983449)

+ [使用git查看修改记录](https://blog.csdn.net/u011559046/article/details/79296801)

+ [聊下 git rebase -i](https://www.cnblogs.com/wangiqngpei557/p/5989292.html)

+ [Git 基础 - 打标签](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)

+ [Git reset 撤销本地/远程提交版本](https://blog.csdn.net/qq_28018283/article/details/77877986)

+ [三种清除Git提交历史的方法](https://blog.csdn.net/yiifaa/article/details/78603410)

+ [GIT 删除指定COMMIT提交](https://blog.csdn.net/u013630349/article/details/78755286)

+ [git checkout 命令详解](https://www.cnblogs.com/kuyuecs/p/7111749.html)

+ [Git 基础再学习之：git checkout -- file](https://www.cnblogs.com/Calvino/p/5930656.html)

+ [git如何回滚远程仓库](https://www.cnblogs.com/iloveyou-sky/p/6534409.html)

+ [找回Git中丢失的Commit](https://www.jianshu.com/p/8b4c95677ee0)

+ [创建与合并分支](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840038939c291467cc7c747b1810aab2fb8863508000)

+ [廖雪峰的官方网站 git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

+ [git bash 命令行有中文乱码的解决](https://blog.csdn.net/a13835198325/article/details/76460875)

+ [git status中文文件名编码问题解决](https://www.cnblogs.com/chen-cong/p/7679292.html)

+ [Git知识总览(一) 从 git clone 和 git status 谈起](https://www.cnblogs.com/ludashi/p/8052739.html)

+ [git学习------>如何用git log命令来查看某个指定文件的提交历史记录](https://blog.csdn.net/ouyang_peng/article/details/50126603)

+ [5 Git 基础 - 远程仓库的使用](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8)

+ [Git 同时与多个远程库互相同步](https://www.cnblogs.com/hongdada/p/7573923.html)

+ [合并两个git仓库](https://blog.csdn.net/kasteluo/article/details/73330656?utm_source=itdadao&utm_medium=referral)