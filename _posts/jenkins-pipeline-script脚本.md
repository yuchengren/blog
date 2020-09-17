---
title: jenkins-pipeline-script脚本
date: 2020-09-17
categories:
- jenkins
- pipeline
---
非平凡的规模和/或复杂性的 script 块应该被转移到[共享库](https://www.jenkins.io/zh/doc/book/pipeline/syntax/#shared-libraries%23)
```
pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
                script {
                    def browsers = ['chrome', 'firefox']
                    for (int i = 0; i < browsers.size(); ++i) {
                        echo "Testing the ${browsers[i]} browser"
                    }
                }
            }
        }
    }
}
```


