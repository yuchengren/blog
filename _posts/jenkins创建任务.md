---
title: jenkins创建任务
date: 2020-08-25 16:37:00
categories:
- jenkins
---
### 一、创建
主页->New Item  
1.输入名称，如build_online-AppSeller  
2.选择类型
* Freestyle project，构建一个自由风格的项目  
即界面式的设置配置、仓库、脚本代码等
* pipeline，流水线  
语法式的配置，即编写pipeline脚本  
3.Copy from  
可拷贝一个已有的项目，但名称不能重复  

### 二、自由风格样式任务
1.丢弃旧的构建（前提是安装有Configuration Slicing插件）
保持构建的天数 如14  
保持构建的最大个数 如50  
2.参数化的构建过程 勾选

3.源码管理git
* Repository URL,仓库地址
* Credentials，证书，可以添加账户密码型、SSH key类型
* 指定的分支

