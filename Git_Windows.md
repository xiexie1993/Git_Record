# Git Windows

## Windows下搭建 Git服务

### Windows 7 安装 Git

### 问题与解决办法记录

+ windows环境下生成ssh keys
~~~
    1、首先你要安装Git工具
    2、运行Git Bash here
    3、输入指令，进入.ssh文件夹
        cd ~/.ssh/  
      如果提示 “ No such file or directory”，你可以手动的创建一个 .ssh文件夹即可
        mkdir ~/.ssh  
    4、配置全局的name和email，这里是的你github或者bitbucket的name和email
        git config --global user.name "xkwg"  
        git config --global user.email "xkwg@163.com"  
    5、生成key
        ssh-keygen -t rsa -C “email@163.com”  
      连续按三次回车，这里设置的密码就为空了，并且创建了key。
      最后得到了两个文件：id_rsa和id_rsa.pub
    6、打开Admin目录进入.ssh文件夹，用记事本打开id_rsa.pub，复制里面的内容添加到你github或者bitbucket ssh设置里即可
~~~


+ windows中git status中文文件名编码问题解决
    + 原因：  
    + 解决办法： 执行命令 git config --global core.quotepath false 将git配置变量 core.quotepath 设置为false，就可以解决中文文件名称在这些Git命令输出中的显示问题,

+ windows中git bash下中文乱码
    + 原因：  
    + 解决办法：（1）.在git bash下，右键出现下图，选择options；（2）选择"Text"；（3）将"Character set"设置为  zh_CN  UTF-8

## 参考资料

+ [git bash 命令行有中文乱码的解决](https://blog.csdn.net/a13835198325/article/details/76460875)

+ [git status中文文件名编码问题解决](https://www.cnblogs.com/chen-cong/p/7679292.html)

+ [window下配置SSH连接GitHub、GitHub配置ssh key](https://www.cnblogs.com/hukai46/p/5489631.html)

+ [GIT中文乱码问题解决方案](https://blog.csdn.net/xl_lx/article/details/78223349)