---
title: jenkins-plugin-extended-choice-paramater
date: 2020-08-25 16:37:00
categories:
- jenkins
- plugins
---
### 一、简介
多选  
https://plugins.jenkins.io/extended-choice-parameter/
### 二、pipeline语法
```
extendedChoice(
                defaultValue: '',
                description: '打包消息需要@的人',
                multiSelectDelimiter: ',',
                name: 'AT_PERSONS',
                quoteValue: false,
                saveJSONParameterToFile: false,
                type: 'PT_CHECKBOX',
                propertyFile: "/PycharmProjects/jenkins.properties",
                propertyKey: 'AT_PHONES',
                descriptionPropertyFile: "/PycharmProjects/jenkins.properties",
                descriptionPropertyKey: 'AT_NAMES',
//                 value: '10086,10016',
//                 descriptionPropertyValue: '移动,联通',
                visibleItemCount: 8)
```
1.type
* PT_SINGLE_SELECT 下拉列表式-单选
* PT_MULTI_SELECT 下拉列表式-多选
* PT_TEXTBOX
* PT_CHECKBOX
* PT_RADIO
* PT_HIDDEN  

2.其他