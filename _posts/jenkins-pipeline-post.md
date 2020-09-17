
---
title: jenkins-pipeline-post
date: 2020-09-17
categories:
- jenkins
- pipeline
---
post 部分定义一个或多个steps ，这些阶段根据流水线或阶段的完成情况而 运行
### Conditions
* always  
无论流水线或阶段的完成状态如何，都允许在 post 部分运行该步骤。
* changed  
只有当前流水线或阶段的完成状态与它之前的运行不同时，才允许在 post 部分运行该步骤
* failure  
只有当前流水线或阶段的完成状态为"failure"，才允许在 post 部分运行该步骤, 通常web UI是红色。
* success  
只有当前流水线或阶段的完成状态为"success"，才允许在 post 部分运行该步骤, 通常web UI是蓝色或绿色。
* unstable  
只有当前流水线或阶段的完成状态为"unstable"，才允许在 post 部分运行该步骤, 通常由于测试失败,代码违规等造成。通常web UI是黄色。
* aborted  
只有当前流水线或阶段的完成状态为"aborted"，才允许在 post 部分运行该步骤, 通常由于流水线被手动的aborted。通常web UI是灰色
```
pipeline {
    agent any
    stages {
        stage('Example') {
            steps {}
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
    }
}
```


