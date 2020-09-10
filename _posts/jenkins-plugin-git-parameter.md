---
title: jenkins-plugin-git-parameter
date: 2020-08-25 16:37:00
categories:
- jenkins
- plugins
---
### 一、简介
选择git分支、tag、version等
<br>https://plugins.jenkins.io/git-parameter/
<br>https://github.com/jenkinsci/git-parameter-plugin
### 二、pipeline语法
```
gitParameter name: 'BRANCH',
                type: 'PT_BRANCH',
                branchFilter: 'origin/(.*)',
                defaultValue: 'origin/develop',
                selectedValue: 'DEFAULT',
                sortMode: 'ASCENDING_SMART',
                description: '请选择分支',
                useRepository:'.*appname.git'
```
1.type
* Tag-为区分版本在代码中打上的标签
* Branch-代码分支
* Branch or Tag-以上两者的集合
* Revision-每个代码提交对应的id
* Pull Request

2.其他
* Branch-指定分支
* Branch Filter-分支过滤器，支持正则表达
* Tag Filter-标签过滤器
* Sort Mode-排序方式，顺序或倒序 ASCENDING_SMART/DESCENDING_SMART/ASCENDING/DESCENDING
* Default Value-缺省值，无匹配值时的默认值
* Selected Value-NONE，默认不选；TOP，默认选择第一个；DEFAULT，选择默认值
* Use repository-指定代码仓库
* Quick Filter-勾选之后，在构建时会在右侧显示过滤关键字输入框，输入关键字，可以过滤左侧的选项
* List Size 可见的数量
