---
title: OpenClash
layout: post
categories: Exploit 
tags: exploit openwrt Clash 科学上网
excerpt: OpenClash 安装和简单使用教程及常见错误解决
---

项目介绍

*   项目地址：[OpenClash](https://adao.me/go/aHR0cHM6Ly9naXRodWIuY29tL3Zlcm5lc29uZy9PcGVuQ2xhc2g=)
*   官方文档：[wiki](https://adao.me/go/aHR0cHM6Ly9naXRodWIuY29tL3Zlcm5lc29uZy9PcGVuQ2xhc2gvd2lraQ==)
*   Clash内核：[Clash](https://adao.me/go/aHR0cHM6Ly9naXRodWIuY29tL3Zlcm5lc29uZy9PcGVuQ2xhc2gvcmVsZWFzZXMvdGFnL0NsYXNo)
*   TUN模式内核：[clash\_tun](https://adao.me/go/aHR0cHM6Ly9naXRodWIuY29tL3Zlcm5lc29uZy9PcGVuQ2xhc2gvcmVsZWFzZXMvdGFnL1RVTi1QcmVtaXVt)
*   TUN游戏模式内核：[clash\_game](https://adao.me/go/aHR0cHM6Ly9naXRodWIuY29tL3Zlcm5lc29uZy9PcGVuQ2xhc2gvcmVsZWFzZXMvdGFnL1RVTg==) （移除游戏内核和模式，TUN内核功能更全）
*   历史版本下载：[下载](https://adao.me/go/aHR0cHM6Ly9naXRodWIuY29tL3Zlcm5lc29uZy9PcGVuQ2xhc2gvcmVsZWFzZXM=)

安装
--

### 安装环境

*   架构：MediaTek MT7621
*   固件版本：OpenWrt R20.8.27 / LuCI Master (git-20.223.26773-d18ef13)
*   内核版本：5.4.59

内容更新
----

### 2021.12.6

*   Openclash版本：v0.44.03-beta
*   重要功能建议配置修改

### 2021.6.15

*   小娱路由器只运行openclash时，可以稳定运行。
*   看到评论区好多人都提到ac2100，前段时间就买了一个，我这里测试运行，发现运行一段时间后就会出现断网的情况，进入后台发现OpenClash显示未运行，必须手动关闭或者启动后才会正常，说明ac2100运行OpenClash会更吃力一点，只能当做ap或者更换帕斯沃，帕斯沃基本正常，但是没有Openclash功能多，这些插件还是建议跑在软路由上面，就算是一百多块钱的也是能稳定运行的

### 进入后台

通过终端行进入

```
ssh [[email protected]](https://adao.me/cdn-cgi/l/email-protection)
```

如果不能正常登录，请检查密码是否正确或者后台ssh登录是否开启

### 依赖安装

1.  更新

```
opkg update
```

如更新错误，请检查系统-软件包-配置内地址是否可用  
小娱路由器软件源（MT7621）

```
src/gz openwrt_core https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/packages/
src/gz openwrt_base https://downloads.openwrt.org/snapshots/packages/mipsel_24kc/base/
src/gz openwrt_luci https://downloads.openwrt.org/snapshots/packages/mipsel_24kc/luci/
src/gz openwrt_packages https://downloads.openwrt.org/snapshots/packages/mipsel_24kc/packages
src/gz openwrt_routing https://downloads.openwrt.org/snapshots/packages/mipsel_24kc/routing
src/gz openwrt_telephony https://downloads.openwrt.org/snapshots/packages/mipsel_24kc/telephony
```

2.安装依赖 (v0.44.03-beta)  
coreutils-nohup, bash, iptables, dnsmasq-full, curl, ca-certificates, ipset, ip-full, iptables-mod-tproxy, iptables-mod-extra, libcap, libcap-bin, ruby, ruby-yaml, kmod-tun

按顺序安装以上依赖，每个依赖单独安装

无法安装 kmod-tun（显示内核版本不匹配）  
强制安装

```
opkg install kmod-tun --force-depends 
```

同样问题都可以使用以上方法解决

报错：opkg\_conf\_load: Could not lock /var/lock/opkg.lock: Resource temporarily unavailable.

```
rm -f /var/lock/opkg.lock
```

确认依赖安装成功后可进行后续的操作

主程序安装
-----

1.  进入tmp目录

```
cd /tmp/tmp/
```

1.  下载及安装ipk（v0.44.03-beta）

```
wget https://github.com/vernesong/OpenClash/releases/download/v0.44.03-beta/luci-app-openclash_0.44.03-beta_all.ipk
opkg install luci-app-openclash_0.44.03-beta_all.ipk
```

注意软件名根据下载版本更改

内核下载
----

1.  进入到内核目录（根据自己的硬件选择）

*   clash内核

```
cd /etc/openclash/core/
wget https://github.com/vernesong/OpenClash/releases/download/Clash/clash-linux-mipsle-softfloat.tar.gz
tar -zxvf clash-linux-mipsle-softfloat.tar.gz
chmod 777 clash
```

其他内核方法一致

安装完毕

配置设置
----

### 模式设置

推荐Fake-IP(TUN-混合)模式

### 常规设置

*   内核编译版本：linux-mipsle-softfloat

### DNS设置

*   本地DNS：启用
*   自定义上游DNS服务器：启用
*   勾选以下DNS  
    [](https://raw.githubusercontent.com/iadao/img/master/20200929141043.jpg#vwid=1964&vhei=1382)
    
    [](https://raw.githubusercontent.com/iadao/img/master/20200929141043.jpg#vwid=1964&vhei=1382)[![-w982](https://raw.githubusercontent.com/iadao/img/master/20200929141043.jpg#vwid=1964&vhei=1382)](https://raw.githubusercontent.com/iadao/img/master/20200929141043.jpg#vwid=1964&vhei=1382)
    
    \-w982
    

### 规则设置

[](https://raw.githubusercontent.com/iadao/img/master/20200929141033.jpg#vwid=1704&vhei=452)

[![-w852](https://raw.githubusercontent.com/iadao/img/master/20200929141033.jpg#vwid=1704&vhei=452)](https://raw.githubusercontent.com/iadao/img/master/20200929141033.jpg#vwid=1704&vhei=452)

\-w852

### 第三方规则订阅

[](https://raw.githubusercontent.com/iadao/img/master/20200929141030.jpg#vwid=844&vhei=498)

[![-w422](https://raw.githubusercontent.com/iadao/img/master/20200929141030.jpg#vwid=844&vhei=498)](https://raw.githubusercontent.com/iadao/img/master/20200929141030.jpg#vwid=844&vhei=498)

\-w422

### 服务器与策略组

[](https://raw.githubusercontent.com/iadao/img/master/20200929141036.jpg#vwid=1678&vhei=710)

[![-w839](https://raw.githubusercontent.com/iadao/img/master/20200929141036.jpg#vwid=1678&vhei=710)](https://raw.githubusercontent.com/iadao/img/master/20200929141036.jpg#vwid=1678&vhei=710)

\-w839

### 上传配置文件

自行研究

保存配置并应用

启动成功界面
------

[](https://raw.githubusercontent.com/iadao/img/master/20211206144421.jpg#vwid=3264&vhei=1664)

[![](https://raw.githubusercontent.com/iadao/img/master/20211206144421.jpg#vwid=3264&vhei=1664)](https://raw.githubusercontent.com/iadao/img/master/20211206144421.jpg#vwid=3264&vhei=1664)

新功能展示
-----

### 流媒体解锁

[](https://raw.githubusercontent.com/iadao/img/master/20211206144417.jpg#vwid=1798&vhei=712)

[![](https://raw.githubusercontent.com/iadao/img/master/20211206144417.jpg#vwid=1798&vhei=712)](https://raw.githubusercontent.com/iadao/img/master/20211206144417.jpg#vwid=1798&vhei=712)

### 在线订阅转换

[](https://raw.githubusercontent.com/iadao/img/master/20211206144418.jpg#vwid=1276&vhei=822)

[![](https://raw.githubusercontent.com/iadao/img/master/20211206144418.jpg#vwid=1276&vhei=822)](https://raw.githubusercontent.com/iadao/img/master/20211206144418.jpg#vwid=1276&vhei=822)

### 更加简单的版本更新

[](https://raw.githubusercontent.com/iadao/img/master/20211206144416.jpg#vwid=3078&vhei=616)

[![](https://raw.githubusercontent.com/iadao/img/master/20211206144416.jpg#vwid=3078&vhei=616)](https://raw.githubusercontent.com/iadao/img/master/20211206144416.jpg#vwid=3078&vhei=616)

### 上传文件类型增加，如备份文件上传

[](https://raw.githubusercontent.com/iadao/img/master/20211206144420.jpg#vwid=2806&vhei=490)

[![](https://raw.githubusercontent.com/iadao/img/master/20211206144420.jpg#vwid=2806&vhei=490)](https://raw.githubusercontent.com/iadao/img/master/20211206144420.jpg#vwid=2806&vhei=490)

### 增加Meta内核

> 介绍：[https://clashmeta.gitbook.io/meta/](https://adao.me/go/aHR0cHM6Ly9jbGFzaG1ldGEuZ2l0Ym9vay5pby9tZXRhLw==)

[](https://raw.githubusercontent.com/iadao/img/master/20220423185001.jpg#vwid=1370&vhei=980)

[![](https://raw.githubusercontent.com/iadao/img/master/20220423185001.jpg#vwid=1370&vhei=980)](https://raw.githubusercontent.com/iadao/img/master/20220423185001.jpg#vwid=1370&vhei=980)

* * *
