---
title: jenkins-pipeline-when
date: 2020-09-17
categories:
- jenkins
- pipeline
---
when 指令允许流水线根据给定的条件决定是否应该执行阶段。 when 指令必须包含至少一个条件。 如果 when 指令包含多个条件, 所有的子条件必须返回True，阶段才能执行  
注意：默认stage中的when在agent后执行，可以通过beforeAgent修改
```
pipeline {
    agent any
    stages {
        stage('Example Deploy') {
            when {
                beforeAgent true
                expression { BRANCH_NAME ==~ /(production|staging)/ }
                anyOf {
                    environment name: 'DEPLOY_TO', value: 'production'
                    environment name: 'DEPLOY_TO', value: 'staging'
                }
            }
    }
}
```
### 内置条件
* branch  
当正在构建的分支与模式给定的分支匹配时，执行这个阶段, 例如: when { branch 'master' }。注意，这只适用于多分支流水线。
* environment  
当指定的环境变量是给定的值时，执行这个步骤, 例如: when { environment name: 'DEPLOY_TO', value: 'production' }
* expression  
当指定的Groovy表达式评估为true时，执行这个阶段, 例如: when { expression { return params.DEBUG_BUILD } }
* not  
当嵌套条件是错误时，执行这个阶段,必须包含一个条件，例如: when { not { branch 'master' } }
* allOf  
当所有的嵌套条件都正确时，执行这个阶段,必须包含至少一个条件，例如: when { allOf { branch 'master'; environment name: 'DEPLOY_TO', value: 'production' } }
* anyOf  
当至少有一个嵌套条件为真时，执行这个阶段,必须包含至少一个条件，例如: when { anyOf { branch 'master'; branch 'staging' } }




