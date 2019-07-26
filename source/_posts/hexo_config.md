---
title: hexo + webhook配置博客自动部署
date: 2019-07-27 02:18:35
tags:
---
## 配置hexo
{% asset_img hexo部署配置.jpg hexo部署配置图 %}


## 配置webhook
参考地址： {% link 利用Github的Webhook功能和Node.js完成项目的自动部署 https://www.jianshu.com/p/e4cacd775e5b 利用Github的Webhook功能和Node.js完成项目的自动部署 %}

另外需要注意的是 配置github中webhook时 需要选择content type 为application/json
{% link github-webhook-handler插件github地址 https://github.com/rvagg/github-webhook-handler#readme github-webhook-handler %}

这里贴出我自己的webhook配置
{% asset_img webhook1.png github的webhook配置 %}
服务器中：
{% asset_img webhook2.png 服务器的js和shell脚本 %}

## 原理
webhook ----> 相当于是你提交或者issue等给 git仓库  然后git仓库收到了你的请求  回调发送一个请求给你设置的地址(即我设置的7777端口的那个地址)
告知你 仓库有更新或者什么事件发生  然后你的7777端口的服务脚本接收到请求，触发本地写好的deploy.sh 调用git pull

hexo部署配置 是新建了published分支  然后commit 编译好的博客文件

## 注意事项
deploy.sh中的 git pull  嗯 建议是通过rsa来认证git的权限
命令如下:
{% codeblock %}
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
{% endcodeblock %}
上述操作完成后 会提示告知你 id_rsa的位置 然后复制id_rsa内容到github上
{% link Generating a new SSH key and adding it to the ssh-agent https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent  Generating a new SSH key and adding it to the ssh-agent %}

## 待更新
寻找更快写博客的方法？
linux中npm global的包，引用不到的问题？
git-hook的使用？

### end