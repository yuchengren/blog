---
title: jenkins安装
date: 2020-08-25 16:37:00
categories:
- jenkins
---
### 前言
以linux上部署tomcat+jenkins为例
### 一、下载
1.下载[tomcat](https://tomcat.apache.org/download-90.cgi)  
2.[jenkins下载地址]((https://jenkins.io/zh/download/))  
选择Generic Java package(.war)，右键复制链接地址  
进入到tomcat/webapps下,下载jenkins.war
```
wget http://mirrors.jenkins.io/war-stable/2.249.1/jenkins.war 
```
3.启动tomcat(前提是安装好jdk和配置好jdk的环境变量)
```
cd tomcat/bin
startup.sh
```
### 二、初始化
1.打开 http://127.0.0.1:8080/jenkins  
注意ip修改为自己服务器的ip  
2.首次进入，出现Unlock Jenkins的初始化密码弹窗
根据红色提示路径文件 /当前用户目录/.jenkins/secrets/initialAdminPassword，拷贝密码填入Administrator password输入框，点击continue  
3.初始化缓冲后，**自定义jenkins**弹窗出现  
选项，安装推荐的插件和选择插件来安装
如果有插件备份（已安装的jenkins,~/.jenkins/plugins目录里的hpi文件),或进入jenkins再手动选择插件安装，可选择插件来安装；  
选择 安装推荐的插件，最好配有外网代理，否则会比较慢，还会出现部分插件下载失败  
4.进入Create First Admin User,
![](/images/jenkins-plugins-download.png),创建一个初始账户，如admin/123456  
5.进入Instance Configuration,指定Jenkins根链接，使用默认的即可
### 三、插件([下载地址](http://updates.jenkins-ci.org/download/plugins/))
1.**安装**，主页->Manage Jenkins->Manage Plugins，选择Avaiable标签，filter框里输入你想安装的插件名称  
如中文化插件,搜索Localization，勾选Locale plugin和Localization: Chinese (Simplified),点击直接安装；若安装完插件jenkins重启后，仍未中文生效，则可在主页->Manage Jenkins->Configure System,找到Locale栏目，设置Default Language，en为英文，zh_CN为简体中文，zh_TW为繁体中文，并勾选Ignore browser preference and force this language to all users  
2.**上传**，Manage Plugins,选择标签**Advanced**，Upload Plugin,选择从插件下载地址下载的插件，点击upload


