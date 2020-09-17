---
title: jenkins-pipeline-parallel并行
date: 2020-09-16
categories:
- jenkins
- pipeline
---
声明式流水线的阶段可以在他们内部声明多隔嵌套阶段, 它们将并行执行。 注意，一个阶段必须只有一个 steps 或 parallel 的阶段。 嵌套阶段本身不能包含进一步的 parallel 阶段, 但是其他的阶段的行为与任何其他 stage 相同。任何包含 parallel 的阶段不能包含 agent 或 tools 阶段, 因为他们没有相关 steps。  
另外, 通过添加 failFast true 到包含 parallel`的 `stage 中， 当其中一个进程失败时，你可以强制所有的 parallel 阶段都被终止。
```
pipeline {
    agent any
    stages {
        stage('Parallel Stage') {
            when {
                branch 'master'
            }
            failFast true
            parallel {
                stage('Branch A') {}
                stage('Branch B') {}
            }
        }
    }
}
```

