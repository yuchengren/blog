---
title: jenkins-plugin-汇总
date: 2020-08-25 16:37:00
categories:
- jenkins
- plugins
---
### 一、Configuration Slicing（丢弃旧的构建）
1.全局设置
jenkins->Manage Jenkins->Uncategorized栏目下Configuration Slicing,设置保留的天数和最大保留的数量
* Discard Old Builds Slicer - Days to keep artifacts
* Discard Old Builds Slicer - Days to keep builds
* Discard Old Builds Slicer - Max # of builds to keep
* Discard Old Builds Slicer - Max # of builds to keep with artifacts

2.任务中单独设置
task->configure，勾选Discard old builds

### 二、python
Python/Python Wrapper

### 三、Git Parameter
选择git分支、tag、version等
### 四、Extended Choice Paramater
多选
### 五、Generic Webhook Trigger
网络回调钩子
### 六、Build environment
查看构建的环境变量，菜单Compare environment

### 七、build user vars
https://plugins.jenkins.io/build-user-vars-plugin/  
任务中获取jenkins用户的信息
```
steps{
    wrap([$class: 'BuildUser']){
        echo "full name is $BUILD_USER" //全名
        echo "user id is $BUILD_USER_ID"
        echo "user email is $BUILD_USER_EMAIL"
    }
}
```
