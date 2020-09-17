---
title: jenkins-pipeline-parameters
date: 2020-09-16
categories:
- jenkins
- pipeline
---
```
pipeline {
    agent any
    parameters { 
        string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
        booleanParam(name: 'DEBUG_BUILD', defaultValue: true, description: '')
        choice(name: 'CHOICES', choices: ['one', 'two', 'three'], description: '')
        text(name: 'DEPLOY_TEXT', defaultValue: 'One\nTwo\nThree\n', description: '')
       	file(name: 'FILE', description: 'Some file to upload') 
        password(name: 'PASSWORD', defaultValueAsSecret: 'SECRET', description: 'A secret password')
    }
}
```

