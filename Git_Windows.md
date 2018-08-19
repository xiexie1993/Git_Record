# Git Windows

## Windows下搭建 Git服务

### Windows 7 安装 Git

### 问题与解决办法记录

+ windows中git status中文文件名编码问题解决
    + 原因：  
    + 解决办法： 执行命令 git config --global core.quotepath false 将git配置变量 core.quotepath 设置为false，就可以解决中文文件名称在这些Git命令输出中的显示问题,

## 参考资料

+ [git bash 命令行有中文乱码的解决](https://blog.csdn.net/a13835198325/article/details/76460875)

+ [git status中文文件名编码问题解决](https://www.cnblogs.com/chen-cong/p/7679292.html)

+ [window下配置SSH连接GitHub、GitHub配置ssh key](https://www.cnblogs.com/hukai46/p/5489631.html)

+ [GIT中文乱码问题解决方案](https://blog.csdn.net/xl_lx/article/details/78223349)