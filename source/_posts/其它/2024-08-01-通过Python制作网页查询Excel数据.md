---
title: 通过Python制作网页查询Excel数据
layout: post
categories: Exploit
tags: exploit python 编程 后端
excerpt: 通过Python制作网页查询Excel数据 实现简易网页可视化查询
---



###  通过Python制作网页查询Excel数据

## 1.Excel文件：D:\Python_Project\test\奖牌榜.xlsx，和Python代码在同一目录

![images](https://img2020.cnblogs.com/blog/1837851/202201/1837851-20220108230252678-173634989.png)


![images](https://img2020.cnblogs.com/blog/1837851/202201/1837851-20220108230317990-1607828126.png) 


## 2.代码test2.py：

```
import flask
import pandas as pd
from flask import request

app = flask.Flask(__name__)

@app.route("/query", methods=["GET", "POST"])
def query_info():
    df = pd.read_excel("奖牌榜.xlsx")

    medal_data = pd.DataFrame()
    country_name = request.form.get("country_name", "")
    if country_name:
        medal_data = df.query(f"国家 == '{country_name}'")

    return f"""
        <html><body style="text-align:center">
        <h3>查询奖牌信息</h3>

        <form action="/query" method="post">
            国家：<input type="text" name="country_name" value="{country_name}">
            <input type="submit" name="submit" value="查询">
        </form>

        <center> %s </center>
        </body></html>
    """ % medal_data.to_html(index=False)


app.run(host="0.0.0.0", port=9999)
``` 
 

## 3.运行：

![images](https://img2020.cnblogs.com/blog/1837851/202201/1837851-20220108230337990-1292105602.png)

## 4.验证：

（1）查看9999端口的占用情况：
    ```
    netstat -ano | findstr "9999"
    ```
    
（2）查看PID对应的进程：
    ```
    tasklist | findstr "1480"
    ```
    
![images](https://img2020.cnblogs.com/blog/1837851/202201/1837851-20220108230348502-1066586872.png)


（3）浏览器访问：192.168.0.100:9999/query

![images](https://img2020.cnblogs.com/blog/1837851/202201/1837851-20220108230403509-1223871112.png)


![images](https://img2020.cnblogs.com/blog/1837851/202201/1837851-20220108230410500-256908978.png)

 
![images](https://img2020.cnblogs.com/blog/1837851/202201/1837851-20220108230416238-1249719073.png) 

 

##  备注：

## 1、Excel文件需要和python代码放在同一目录下才可以使用相对路径表示

## 2、/query为浏览器访问时输入的路径

## 3、IP地址192.168.0.100为Windows本机内网IP地址

## 4、app.run(host="0.0.0.0", port=9999)：监听本机所有地址的9999端口

## 5、程序执行过程中其它依赖软件包的安装方法：

（1）“文件”-->“设置”-->“项目：当前项目”-->“Python解释器”-->“+”进行软件包安装

（2）通过CMD命令提示符使用pip命令进行安装，需要注意的是，PyCharm中的环境和pip所在的环境可能不是同一个环境，pip安装的软件包可能在Python的原生环境中，而PyCharm中所用的却是虚拟环境（PyCharm在安装过程中会提示用户是否安装虚拟环境），需要将pip安装好的软件包拷贝至虚拟环境中才能生效。

## 6、PyCharm中软件包安装慢的解决方法：

“文件”-->“设置”-->“项目：当前项目”-->“Python解释器”-->“+”-->“管理仓库”-->“+”-->添加阿里云的仓库地址https://mirrors.aliyun.com/pypi/simple/

## 7、如果是在Linux中执行代码：

（1）后台运行：
    ```
    nohup /usr/bin/python -u /python/test/test2.py &
    ```
    
（2）查看9999端口的占用情况： 
    ```
    ss -tunlp | grep 9999
    ```
