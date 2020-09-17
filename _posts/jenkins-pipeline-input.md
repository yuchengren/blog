---
title: jenkins-pipeline-input
date: 2020-09-16
categories:
- jenkins
- pipeline
---
stage 的 input 指令允许你使用 input step提示输入。 在应用了 options 后，进入 stage 的 agent 或评估 when 条件前， stage 将暂停。 如果 input 被批准, stage 将会继续。 作为 input 提交的一部分的任何参数都将在环境中用于其他 stage。
### 配置项
* message  
必需的。 这将在用户提交 input 时呈现给用户
* id  
input 的可选标识符， 默认为 stage 名称
* ok  
`input`表单上的"ok" 按钮的可选文本
* submitter  
可选的以逗号分隔的用户列表或允许提交 input 的外部组名。默认允许任何用户
* submitterParameter  
环境变量的可选名称。如果存在，用 submitter 名称设置
* parameters  
提示提交者提供的一个可选的参数列表。 更多信息参见 [parameters](https://www.jenkins.io/zh/doc/book/pipeline/syntax/#parameters)
    ```
    pipeline {
        agent any
        stages {
            stage('Example') {
                input {
                    message "Should we continue?"
                    ok "Yes, we should."
                    submitter "alice,bob"
                    parameters {
                        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                    }
                }
                steps {
                    echo "Hello, ${PERSON}, nice to meet you."
                }
            }
        }
    }
    ```

