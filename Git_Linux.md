# Git Linux

## Git 环境搭建

### CentOS 安装Git

+ 0、纲要：Git Gitosis（Git的权限管理套件，可不安装）

+ 1、安装Git

    + setp1： 执行安装命令 yum install -y git
    + setp2： 安装完后，执行命令 git --version ,查看 Git 版本
    + setp3： 服务器端创建 git 用户，用来管理 Git 服务，并为 git 用户设置密码(可不创建，直接使用root或其他已有的账号)
    + setp4：服务器端创建 Git 仓库，例子如下
    ~~~
       设置 /home/data/git/gittest.git 为 Git 仓库
       然后把 Git 仓库的 owner 修改为 git
           [root@localhost home]# mkdir -p data/git/gittest.git
           [root@localhost home]# git init --bare data/git/gittest.git
           Initialized empty Git repository in /home/data/git/gittest.git/
           [root@localhost home]# cd data/git/
           [root@localhost git]# chown -R git:git gittest.git/
    ~~~
   + setp5： 客户端 clone 远程仓库
        + a、windows 下载并安装Git for Windows 
        + b、进入 Git Bash 命令行客户端，创建项目地址（设置在 d:/wamp64/www/gittest_gitbash）并进入
        + c、进入 ~/.ssh/config (没有的话自己建立)，添加以下内容
            ~~~
                Host *.*.*.* 
                HostKeyAlgorithms +ssh-dss
            ~~~
        + d、执行 git clone ssh://用户名@IP地址：端口/仓库的绝对地址 ,按提示输入密码


+ 2、安装Git套件 (gitosis是Git下的权限管理工具，通过一个特殊的仓库（gitosis-admin.git）对Git权限进行管理。)
    + (1):服务端安装并配置gitosis
        + a、获取到安装包 
            ~~~
                root@wz:/home/git# git clone https://github.com/res0nat0r/gitosis
            ~~~
        + b、使用python进行安装
            

            ~~~
                先安装python-setuptools（如果已安装过可跳过）
                root@wz:/home/git# yum install python-setuptools

                root@wz:/home/git#          cd gitosis
                root@wz:/home/git/gitosis#  python setup.py install
            ~~~

+ 3、 上传客户端电脑生产的一个公钥,并使用git用户登陆初始化仓库

      + a、客户端主机生成秘钥
            ~~~
                ssh-keygen -t rsa
            ~~~
      + b、上传秘钥
            ~~~
                C:\Users\Administrator\.ssh>pscp -P 22 id_rsa.pub root@服务器IP:/home/git/keydir
                注：/home/git/keydir，需要先在服务器上创建，可不用keydir命名
            ~~~
       + c、重新初始化现存的 Git 版本库
            ~~~
                su – git
                gitosis-init < /home/git/.ssh/id_rsa.pub
                注：执行成功会出现提示， 重新初始化现存的 Git 版本库于 /home/git/repositories/gitosis-admin.git/
            ~~~
       + d、配置 Gitosis 的那个特殊 Git 仓库
          + (1)、post-update 脚本加上可执行权限：
            ~~~
                服务端执行：
                chmod 755 /home/git/repositories/gitosis-admin.git/hooks/post-update
            ~~~
          + 公钥的拥有者（公钥的拥有者的主机）克隆  gitosis-admin.git
            ~~~
                git clone git@192.168.10.12:/gitosis-admin.git
            ~~~

+ 4、通过修改gitosis-admin.git来管理git权限
       + a、访问管理员仓库gitosis-admin.git
       + b、添加用户通过在keydir目录中添加公钥（添加后commit即可），读写权限通过修改gitosis.conf文件（修改后commit即可）
       + 步骤例子：
          + （1）、 创建一个仓库（我们提交的代码提交到该仓库）

            ~~~
                cd /home/git/repositories
                mkdir runtime.git
                cd  runtime.git
                git init --bare
            ~~~

          + （2）、客户端主机生成秘钥，将公匙复制到服务器里的keydir目录里
          + （3）、 修改gitosis.conf文件，增加访问runtime.git仓库的权限，访问runtime.git仓库，修改如下：

            ~~~
              [gitosis]

              [group gitosis-admin]
              members = xie.zhenbin@szzftl.cn
              writable = gitosis-admin

              [group devloper]
              writable = runtime
              members = xie.zhenbin@szzftl.cn
              members = ZFTL_MGR@DESKTOP-ICBEVO9
            ~~~
            ~~~
            配置规则解释：
              [gitosis]

              [group gitosis-admin]            这是分组名， gitosis-admin 这个名字可以自取
              members = xie.zhenbin@szzftl.cn  这是该分组下的成员（成员名来自上传的rsa文件里的名字 #对应keydir下有一个 username.pub 公钥文件）
              writable = gitosis-admin         这是对应仓库名，代表这是这个分组对该仓库的权限有写的权限，只读权限写法为 readonly

              [group devloper]                   这是分组名 devloper 这个名字可以自取
              writable = runtime                 这代表这个分组对仓库runtime有写权限
              members = xie.zhenbin@szzftl.cn    这是该分组的成员之一，#对应keydir下有一个 username.pub 公钥文件
              members = ZFTL_MGR@DESKTOP-ICBEVO9 这是该分组的成员之一，#对应keydir下有一个 username.pub 公钥文件
            ~~~

+ 5、卸载gitosis
    + a.再次克隆Gitosis的Git仓库，然后安装它--record 选项​​：
      ~~~
        sudo python setup.py install --record uninstall.txt
        注： 这将产生包含所有已安装文件的文本文件。然后，只需删除它们。
        sudo cat uninstall.txt | sudo xargs rm -rf
      ~~~
    + b、删除git 用户，以及git 组：
      ~~~
          sudo userdel -f git
          sudo groupdel [git]
      ~~~

> 
+ windows系统出现 ssh-keygen 不是内部命令
~~~
解决方案：
    1、安装git for windows
    2、找到Git安装目录下的user/bin（ 默认安装的路径为 C:\Program Files\Git\usr\bin ）, 将其添加的系统环境变量中，保存
    3、关闭窗口，再打开新窗口执行
~~~

## 参考资料

+ [git在linux上的安装配置包括设置不同用户的权限](http://lib.csdn.net/article/linux/32861)

+ [在 Linux 下搭建 Git 服务器](https://www.cnblogs.com/dee0912/p/5815267.html)

+ [Unable to negotiate with XX.XX.XX.XX: no matching host key type found. Their offer: ssh-dss](https://blog.csdn.net/guoguo527/article/details/50504630)

+ [gitosis使用笔记](https://www.cnblogs.com/yshyee/p/4288465.html)

+ [Git服务器Gitosis架设指南](http://www.cnblogs.com/zhongkaiuu/articles/5092122.html)

+ [CentOS下的Git服务器：Gitosis](https://my.oschina.net/csensix/blog/184426)

+ [卸载 gitosis](https://serverfault.com/questions/91907/how-do-i-uninstall-gitosis)

+ [git bash 命令行有中文乱码的解决](https://blog.csdn.net/a13835198325/article/details/76460875)

+ [git status中文文件名编码问题解决](https://www.cnblogs.com/chen-cong/p/7679292.html)

