---
title: jenkins-pipeline-简介
date: 2020-09-15
categories:
- jenkins
- pipeline
---
官方文档：https://jenkins.io/zh/doc/book/pipeline/  
美团介绍pipline：https://tech.meituan.com/2018/08/02/erp-cd-jenkins-pipeline.html  
完整实例知乎：https://zhuanlan.zhihu.com/p/51533506  
```
pipeline{ //流水线
    //agent指令是必需的，它指示 Jenkins 为流水线分配一个执行器和工作区,默认情况下，agent 指令确保源代码仓库被检出并在后续阶段的步骤中可被使用。
    agent any
    stages { //阶段
        stage('build'){
            steps{ //步骤
            }
        }
        stage('test'){
            steps{ //步骤
            }
        }
    }
}
```
