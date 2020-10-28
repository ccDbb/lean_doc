## mac电脑下载python新版本安装后python快捷方式指向的还是老版本

mac电脑自带python，其版本比较低，比如我的版本为python2.7，这是就需要升级python。

#### 1，升级步骤（简略说一下，不懂得可以参考https://www.runoob.com/python/python-install.html网站来操作）

1. 去官网下载python最新版版，之后按照提示一步步按照


2. 修改host，如果你的电脑装了base shell你就可以直接执行`export PATH="$PATH:/usr/local/bin/python `

   假如你下载的包为3.8版本，但是你现在执行python -V发现出现的还是2.7
####  2，解决python -V还是显示老版本的问题
1. 首先echo $path 打印下看下path下python路径。
2. 打开/usr/local/bin路径下检查你装的python的版本

![image-20200421222144509](/Users/zhangwenbin/Library/Application Support/typora-user-images/image-20200421222144509.png)



对比第一步中打印出来的路径地址是否一致，如果不一致修改成你想要的版本，比如

`export PATH="$PATH:/usr/local/bin/python`3

3. 这时候你会发现python -V还不是最新的版本。而如果用python3 -V才会出现新的版本。原因是python这个名字已经指向了老版本，所以即使你修改了路径依然不生效。

4. 这时候我们可以通过别名的方式来设置一下`alias python=/usr/local/bin/python3.8`

   现在再试python3  -V你会发现终于出现正确的版本啦。

