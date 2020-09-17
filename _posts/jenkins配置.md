---
title: jenkins配置
date: 2020-08-25
categories:
- jenkins
---
### 一、环境变量配置
jenkins->系统管理->全局工具配置，
* git    /usr/local/git/bin/git (或如果配置有git的环境变量，直接git亦可)
* JAVA_HOME    /DevelopTools/java/jdk
* ANDROID_HOME   /DevelopTools/android/sdk
* gradle-5.6.4 /DevelopTools/android/gradle-5.6.4

### 二、添加凭据
1.SSH username and private key  
①找到本机私钥  
~/.ssh/id_rsa  
②jenkins->系统管理->Manage Credentials->全局凭据,  
添加凭据-SSH username and private key  
