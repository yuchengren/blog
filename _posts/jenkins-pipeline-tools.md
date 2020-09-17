---
title: jenkins-pipeline-tools
date: 2020-09-17
categories:
- jenkins
- pipeline
---
支持工具maven、jdk、gradle
```
pipeline {
    agent any
    tools {
        //The tool name must be pre-configured in Jenkins under Manage Jenkins → Global Tool Configuration
        maven 'apache-maven-3.0.1' 
        gradle 'gradle-4.9'
        jdk 'jdk8'
    }
    stages {
        stage('Example') {
            steps {
                sh 'mvn --version'
                sh "./gradlew app:clean"
                sh "./gradlew app:assemble${FLAVOR}${BUILD_TYPE}"
            }
        }
    }
}
```


