---
title: "Kali Linux 换国内镜像源"
layout: post
categories: Exploit
tags: Kali-Linux Linux 国内镜像源 mirrors
excerpt: kali linux换国内镜像源和报错处理方法
---
Kali Linux 是一个基于 Debian 的高级渗透测试和安全审计 Linux 发行版。为了加速更新和安装软件包的速度，尤其是对国内用户，使用国内的镜像源是一个非常有效的策略。以下是如何将 Kali Linux 的软件源更换为国内镜像源的步骤。

![images](https://pic1.zhimg.com/v2-1d3125ce66a3ec79b415bb80c913cfb9_1440w.jpg?source=172ae18b)

##  1.打开配置文件

### 首先，您需要打开 Kali Linux 的软件源列表文件 `sources.list`：

```
vim /etc/apt/sources.list
```

##  2.将国内镜像源信息写入到文件

![images](https://pic2.zhimg.com/v2-1688df7c8ed79e7d343760698c0e3f21_r.jpg)

##  3.更新软件源

```
sudo apt update
```

### 出现报错

![images](https://pic1.zhimg.com/80/v2-a168cbe222f8d81d0560f14877972cfc_1440w.webp)

### 解决方法删除以下目录

```
rm -rf /etc/apt/sources.list.d
```

### 下载数字签名

```
wget -O archive-key.asc https://archive.kali.org/archive-key.asc
```

### 安装数字签名

```
sudo apt-key add archive-key.asc
```

### apt update 更新成功

![images](https://pic4.zhimg.com/80/v2-bd8a149fbeb69ccb2901ad024bf8b0f3_1440w.webp)

##  附镜像源地址

中科大
```
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
```

阿里云
```
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
```

清华大学
```
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
```

浙大
```
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
```

东软大学
```
deb http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
deb-src http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
```

官方源
```
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib
```
