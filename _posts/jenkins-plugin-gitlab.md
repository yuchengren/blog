---
title: jenkins-plugin-gitlab
date: 2020-08-25 16:37:00
categories:
- jenkins
- plugins
---
### 一、简介
gitlab project代码提交或其他行为，触发jenkins任务的自动构建  
https://plugins.jenkins.io/gitlab-plugin/  
[参考博客](https://www.cnblogs.com/xiaoyaojinzhazhadehangcheng/articles/8465876.html)  
获取远程gitlab webhook 触发分支：$gitlabBranch
### 二、下载
jenkins->Manage Jenkins->Manage Plugins，选择Avaiable标签，filter框里输入 GitLab
### 三、添加gitlab认证凭证
1.获取gitlab api token  
gitlab->Settings->Access Tokens
![](/images/gitlab-access-token.png)
name,可以填127.0.0.1/jenkins类似ip/jenkins形式
选择
拷贝Your new personal access token，保存一下，如果丢失则找不回，需要删除重新新建
2.添加凭证  
jenkins->Mange Jenkins->Security Manage Credentials，鼠标悬浮global,右侧出现朝下小箭头，点击出现Add credentials
![](/images/jenkins-add-credentials-entrance.png)  
* API token填入在GitLab获取的access token
* ID可以写Gitlab的账户名
### 三、配置Gitlab连接凭证
jenkins->Mange Jenkins->Configure System, Gitlab栏目
![](/images/jenkins-gitlab-connect.png)  
* Connection name,填写连接名，若GitLab
* Gitlab host URL，填写GitLab的主页Url
* Credentials，选择上面添加的凭证
* Test Connection按钮,点击测试是否success
### 四、jenkins job配置 GitLab触发器
选取所需配置的jenkins任务，进入配置，找到Build Triggers栏目里,勾选GitLab webhook
![](/images/jenkins-job-triggers-GitLab.png)  
* GitLab webhook URL, GitLab项目设置webhook时所用
* Secret token,点击Generate按钮可生成
### 五、GitLab Project添加webhook
GitLab选取指定project后（要有Maintainer以上权限）
Settings-> Webhooks
* URL，填上面的GitLab webhook URL
* Secret Token，填上面jenkins job生成的  

添加该jenkins job的webhook后，可以点击Test,测试job是否会被自动触发







