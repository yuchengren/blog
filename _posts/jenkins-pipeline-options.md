---
title: jenkins-pipeline-options
date: 2020-09-16
categories:
- jenkins
- pipeline
---
options 指令允许从流水线内部配置特定于流水线的选项  
```
pipeline {
    agent any
    options {
        timeout(time: 1, unit: 'HOURS') 
    }
}
```
pipeline可用选项  
* buildDiscarder  
为最近的流水线运行的特定数量保存组件和控制台输出。
    ```
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: '14', artifactNumToKeepStr: '20', daysToKeepStr: '14', numToKeepStr: '20')
    }

    //daysToKeep: 构建记录将保存的天数
    //numToKeep: 最多此数目的构建记录将被保存
    //artifactDaysToKeep:比此早的发布包将被删除，但构建的日志、操作历史、报告等将被保留
    //artifactNumToKeep:最多此数目的构建将保留他们的发布包
    ```
* disableConcurrentBuilds  
http://www.baidu.com
不允许同时执行流水线。 可被用来防止同时访问共享资源等。例如：
    ```
    options { 
        disableConcurrentBuilds() 
    }
    ```
* overrideIndexTriggers  
允许覆盖分支索引触发器的默认处理。 如果分支索引触发器在多分支或组织标签中禁用, options { overrideIndexTriggers(true) } 将只允许它们用于促工作。否则, options { overrideIndexTriggers(false) } 只会禁用改作业的分支索引触发器。
* skipDefaultCheckout  
在`agent` 指令中，跳过从源代码控制中检出代码的默认情况。例如: options { skipDefaultCheckout() }
* skipStagesAfterUnstable  
一旦构建状态变得UNSTABLE，跳过该阶段。例如: options { skipStagesAfterUnstable() }
* checkoutToSubdirectory  
在工作空间的子目录中自动地执行源代码控制检出。例如: options { checkoutToSubdirectory('foo') }
* timeout  
设置流水线运行的超时时间, 在此之后，Jenkins将中止流水线。例如: options { timeout(time: 1, unit: 'HOURS') }
* retry  
在失败时, 重新尝试整个流水线的指定次数。 For example: options { retry(3) }
* timestamps  
预谋所有由流水线生成的控制台输出，与该流水线发出的时间一致。 例如: options { timestamps() }
### 可选的stage选项
* skipDefaultCheckout  
在 agent 指令中跳过默认的从源代码控制中检出代码。例如: options { skipDefaultCheckout() }
* timeout  
设置此阶段的超时时间, 在此之后， Jenkins 会终止该阶段。 例如: options { timeout(time: 1, unit: 'HOURS') }
* retry  
在失败时, 重试此阶段指定次数。 例如: options { retry(3) }
* timestamps  
预谋此阶段生成的所有控制台输出以及该行发出的时间一致。例如: options { timestamps() }


