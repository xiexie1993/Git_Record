# Git Andriod

## Andriod下搭建 Git服务

### Andriod 安装 Git



+ 1、下载软件包Gidder安装 （Gidder是一个提供git服务，可用于创建git项目，充当git服务）
    下载软件包Pocket Git 安装 （Pocket Git 是一个提供git客户端，可用于充当克隆和提交）
    下载软件包 QuickEdit或者Jota+ 安装 (文本编辑器)

+ 2、连接同一个网络
    + 在Gidder上设置开启应用设置基本参数（端口、用户名、密码、和相应权限）
        + a、建立用户
        + b、建仓库、分配仓库权限给用户

+ 3、客户端设置
    + a、windows7
        + step1:安装git
        + step2:进入 ~/.ssh/config (没有的话自己建立)

            ~~~
                方案一：（如果clone linux系统的Git会克隆不了，解决办法，方案二）
                    Host *.*.*.* 
                    KexAlgorithms +diffie-hellman-group1-sha1
                    HostkeyAlgorithms ssh-dss
                方案二：（建议方案）
                    Host *.*.*.* 
                    HostKeyAlgorithms +ssh-dss
            ~~~

   step3: 设置全局的用户（此步骤可不执行）
    git config --global user.name 'runoob'
    git config --global user.email test@runoob.com

        step4: 运行克隆命令  git clone  ssh://xiexie1993@192.168.31.124:2222/test.git

## 参考资料：

+ [笔记项目随身携带-android手机git服务器：gidder](https://blog.csdn.net/TaylorPotter/article/details/69808733)

+ [git push 报错，Unable to negotiate with XX: no matching host key type found.](https://help.aliyun.com/knowledge_detail/41978.html)

+ [Windows 7下Git SSH 创建Key的步骤（by 星空武哥）](https://blog.csdn.net/lsyz0021/article/details/52064829)

+ [git的基本使用(三)---修改git仓库地址的端口号](https://blog.csdn.net/u010041075/article/details/52981731)

+ [git status中文文件名编码问题解决](https://www.cnblogs.com/chen-cong/p/7679292.html)

