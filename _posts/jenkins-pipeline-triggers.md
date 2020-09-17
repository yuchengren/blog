---
title: jenkins-pipeline-triggers
date: 2020-09-17
categories:
- jenkins
- pipeline
---
### cron
接收 cron 样式的字符串来定义要重新触发流水线的常规间隔
```
pipeline {
    agent any
    triggers {
        cron('45 9-16/2 * * 1-5') //从上午9:45开始每小时45分钟一次，每个工作日下午3:45结束
        cron('H(0-29)/10 * * * *')   //每小时上半场每十分钟一次（三次，也许在：04，：14，：24）
    }
}
```
**jenkins cron语法**([官网](https://en.wikipedia.org/wiki/Cron))  
每行包含由TAB或空格分隔的5个字段  
分钟|小时|DOM|月|DOW
-|-|-|-|-
一小时内的分钟数0-59|一天中的小时0-23|每月的某一天1-31</ td>|月1-12|星期几0-7，其中0和7是星期日
要为一个字段指定多个值，可以使用以下运算符。按优先顺序排列  
* \*指定所有有效值
* M-N 指定一系列值
* M-N/X或者按照指定范围或整个有效范围的*/X间隔步长X
* A,B,…,Z 枚举多个值  

为了允许定期计划的任务在系统上产生均匀负载，应尽可能使用符号H（“哈希”），集中固定时间刻执行，会使固定时间段cpu
及内存占用飙升
### pollSCM
接收 cron 样式的字符串来定义一个固定的间隔，在这个间隔中，Jenkins 会检查新的源代码更新。如果存在更改, 流水线就会被重新触发
```
triggers { pollSCM('H */4 * * 1-5') }
```
### upstream
接受逗号分隔的工作字符串和阈值。 当字符串中的任何作业以最小阈值结束时，流水线被重新触发
```
triggers { upstream(upstreamProjects: 'job1,job2', threshold: hudson.model.Result.SUCCESS) }
```



