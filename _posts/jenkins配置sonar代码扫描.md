---
title: jenkins配置sonar代码扫描
date: 2020-09-15
categories:
- jenkins
---
### 一、配置步骤
参考
https://cloud.tencent.com/developer/article/1578435  
https://www.jianshu.com/p/5e4a145af439  
1. 系统管理-插件管理，搜索SonarQube Scanner插件，安装
2. 访问sonarqube，http://127.0.0.1:9000/account/security/,  
输入令牌名称jenkins，点击生成令牌如xxx
3. 菜单：凭据 —> 系统 -> 全局凭据 -> 添加凭据  
类型选择：Secret text，然后Secret中填入之前生成的Token，ID可写sonar-token
4. 配置sonarqube server  
系统管理-系统配置，SonarQube servers配置项增加SonarQube Server  
勾选Enable；name输入sonar；Server URL：http://127.0.0.1:9000，token选择上一步配置的sonar-token
5. 配置sonarqube scanner  
系统管理-全局工具配置-SonarQube Scanner,勾选自动安装或配置已安装的scanner路径  
Name:sonar-scanner-4.2.0  
SONAR_RUNNER_HOME:/DevelopTools/java/sonar-scanner  
6. 新建任务job-增加构建步骤-Excute SonarQube Scanner
Analysis properties
```
sonar.projectKey=$JOB_NAME
sonar.java.binaries=target/classes
```
```
sonar.projectKey=appName
sonar.projectName=appName
sonar.projectVersion=1.0
sonar.sources=src
sonar.java.binaries=target
sonar.language=java
```
### 二、报错解决
1. 
```
#org.sonar.squidbridge.api.AnalysisException: Please provide compiled classes of your project with 
#sonar.java.binaries property
sonar.java.binaries=target/classes
```