---
title: jenkins-problem-配置
date: 2020-09-15
categories:
- jenkins
- problem
---
### 一、'Gradle build daemon disappeared unexpectedly(it may have been killed or may have crashed)
free -h 检查服务器剩余内存，项目中gradle.properties下的内存配置不能大于服务器可用内存
```
org.gradle.jvmargs=-Xmx2048M
org.gradle.daemon=false
```
从 Gradle 3.0 开始，Daemon 便默认开启的。它是一个长时间运行的后台进程，作用是在内存中存储构建信息，以便在之后的构建过程中复用信息提高构建速度。  
但是在文档中，也提到一句：If you run CI builds in ephemeral environments (such as containers) that do not reuse any processes, use of the Daemon will slightly decrease performance (due to caching additional information) for no benefit, and may be disabled. 大概的意思是如果通过CI（持续集成）进行项目构建，Daemon 就没多大作用了，反倒会因为存储额外的信息而降低系统性能，从而导致被停用。  
Jenkins 里停止使用 Daemon： 
```
./gradlew --no-daemon assembleDebug
```
### 二、git clone 错误：hudson.plugins.git.GitException: Failed to fetch from 
 Git Repository URL地址后加上.git 或升级git版本
### 三、错误: 找不到或无法加载主类 org.gradle.wrapper.GradleWrapperMain
The class GradleWrapperMain is inside the gradle-wrapper.jar, and Jenkins is unable to find it. I believe you forgot to check in the generated gradle-wrapper.jar   
方式一：项目里gradle/wrapper下放入gradle-wrapper.jar  
方式二：
```
task wrapper(type: Wrapper) {
    gradleVersion = '6.1.1' //we want gradle 6.1.1 to run this project
}
```
执行task: 
$ gradle wrapper
### 三、jenkins shell执行python文件报错 ImportError: No module named 项目中自定义的模块
方式一：在系统管理-系统设置中，设置全局变量 PYTHONPATH=python文件所在的工程路径  
方式二：shell脚本中 临时修改环境变量export PYTHONPATH=/PycharmProjects/pythonproject:$PYTHONPATH 
