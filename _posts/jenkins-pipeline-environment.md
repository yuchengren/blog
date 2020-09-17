---
title: jenkins-pipeline-environment
date: 2020-09-16
categories:
- jenkins
- pipeline
---
1. 顶层流水线块中使用的 environment 指令将适用于流水线中的所有步骤。
2. 在一个 stage 中定义的 environment 指令只会将给定的环境变量应用于 stage 中的步骤。
3. environment 块有一个 助手方法 credentials() 定义，该方法可以在 Jenkins 环境中用于通过标识符访问预定义的凭证
    ```
    pipeline {
        agent any
        environment { 
            CC = 'clang'
        }
        stages {
            stage('Example') {
                environment { 
                    AN_ACCESS_KEY = credentials('my-prefined-secret-text') 
                }
                steps {
                    sh 'printenv'
                }
            }
        }
    }
    ```
4. 使用  
* 配置中url: env.REPOSITORY
* sh命令中 sh "${SCRIPT_PROJECT_ROOT}"
