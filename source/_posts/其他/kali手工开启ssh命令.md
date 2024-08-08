---
title: kali手工开启ssh命令
layout: post
categories: Exploit
tags: exploit 操作系统 Linux kali
excerpt: kali手工开启ssh(端口22）命令操作方法
---



##  插入一个kali添加新root的命令

```
sudo passwd root
```

![images](https://img2022.cnblogs.com/blog/2786933/202203/2786933-20220325222259284-2063599498.png)


首先使用netstat -lnt查看一下当前kali开放的端口，如果没有开放22端口，我们需要手动开启22端口。

![images](https://img2022.cnblogs.com/blog/2786933/202203/2786933-20220325221025800-1826562903.png) 


##  第一步：开启kail 远程ssh，开启办法如下：

### 配置SSH参数

修改sshd_config文件，命令为：

```
vim /etc/ssh/sshd_config
```

![images](https://img2022.cnblogs.com/blog/2786933/202203/2786933-20220325221217828-2053701535.png)
 

将#PasswordAuthentication no的注释去掉，并且将NO修改为YES //kali中默认是yes

将PermitRootLogin without-password修改为PermitRootLogin yes

![images](https://img2022.cnblogs.com/blog/2786933/202203/2786933-20220325221419037-383768029.png)


##  第二步：启动SSH服务

命令为：
```
/etc/init.d/ssh start
```

或者
```
service ssh start
```


![images](https://img2022.cnblogs.com/blog/2786933/202203/2786933-20220325221624073-418461818.png)


查看SSH服务状态是否正常运行，命令为：
```
/etc/init.d/ssh status
```
或者
```
service ssh status
```
 
![images](https://img2022.cnblogs.com/blog/2786933/202203/2786933-20220325221539972-418734645.png)


##  第三步：设置系统自动启动SSH服务

### 系统自动启动SSH服务

```
update-rc.d ssh enable 
```

![images](https://img2022.cnblogs.com/blog/2786933/202203/2786933-20220325221730228-2086528238.png)
 
 
### 关闭系统自动启动SSH服务

``` 
update-rc.d ssh disabled
```

再次执行**netstat -lnt**命令则看到22端口成功启动

![images](https://img2022.cnblogs.com/blog/2786933/202203/2786933-20220325221820145-2130970474.png)

 之后就可以通过xshell远程登陆了！
