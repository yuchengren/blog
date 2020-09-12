---
title: jenkins-problem-汇总
date: 2020-08-25 16:37:00
categories:
- jenkins
- problem
---
### 一、插件更新或下载失败  
打开 http://localhost:8080/jenkins/pluginManager/advanced， 将Upadate Site地址由https改为http;  
也可配置镜像地址 https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json  
### 二、AndroidStudio 安装jenkins control plugin
点击扳手设置，获取Crumb Data在浏览器中输入http://127.0.0.1:8080/jenkins/crumbIssuer/api/xml?tree=crumb ，
Test Connection若报错：CSRF enabled -> Missing or bad crumb data  
低版本jenkins,系统管理->全局安全配置，取消勾选 防止跨站点请求伪造Prevent Cross Site Request Forgery exploits  
高版本jenkins，参考https://issues.jenkins-ci.org/browse/JENKINS-61375
### 三、jenkins时间与系统时间不一致
Jenkins→系统管理→脚本命令行，输入
```
System.setProperty('org.apache.commons.jelly.tags.fmt.timeZone', 'Asia/Shanghai')
```