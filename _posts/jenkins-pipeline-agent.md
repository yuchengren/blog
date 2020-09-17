---
title: jenkins-pipeline-agent
date: 2020-09-15
categories:
- jenkins
- pipeline
---
agent 部分指定了整个流水线或特定的部分, 将会在Jenkins环境中执行的位置，这取决于 agent 区域的位置。该部分必须在 pipeline 块的顶层被定义, 但是 stage 级别的使用是可选的。
### 参数
为了支持作者可能有的各种各样的用例流水线, agent 部分支持一些不同类型的参数。这些参数应用在`pipeline`块的顶层, 或 stage 指令内部。
* any  
在任何可用的代理上执行流水线或阶段。例如: agent any
* none  
当在 pipeline 块的顶部没有全局代理， 该参数将会被分配到整个流水线的运行中并且每个 stage 部分都需要包含他自己的 agent 部分。比如: agent none
* label  
在提供了标签的 Jenkins 环境中可用的代理上执行流水线或阶段。 例如: agent { label 'my-defined-label' }
* node  
agent { node { label 'labelName' } } 和 agent { label 'labelName' } 一样, 但是 node 允许额外的选项 (比如 customWorkspace )
* docker  
使用给定的容器执行流水线或阶段。该容器将在预置的 node上，或在匹配可选定义的`label` 参数上，动态的供应来接受基于Docker的流水线。 docker 也可以选择的接受 args 参数，该参数可能包含直接传递到 docker run 调用的参数, 以及 alwaysPull 选项, 该选项强制 docker pull ，即使镜像名称已经存在。 比如: agent { docker 'maven:3-alpine' } 或
```
agent {
    docker {
        image 'maven:3-alpine'
        label 'my-defined-label'
        args  '-v /tmp:/tmp'
    }
}
```
* dockerfile  
执行流水线或阶段, 使用从源代码库包含的 Dockerfile 构建的容器。为了使用该选项， Jenkinsfile 必须从多个分支流水线中加载, 或者加载 "Pipeline from SCM." 通常，这是源代码仓库的根目录下的 Dockerfile : agent { dockerfile true }. 如果在另一个目录下构建 Dockerfile , 使用 dir 选项: agent { dockerfile {dir 'someSubDir' } }。如果 Dockerfile 有另一个名称, 你可以使用 filename 选项指定该文件名。你可以传递额外的参数到 docker build ... 使用 additionalBuildArgs 选项提交, 比如 agent { dockerfile {additionalBuildArgs '--build-arg foo=bar' } }。 例如, 一个带有 build/Dockerfile.build 的仓库,期望一个构建参数 version:
```
agent {
    // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
    dockerfile {
        filename 'Dockerfile.build'
        dir 'build'
        label 'my-defined-label'
        additionalBuildArgs  '--build-arg version=1.0.2'
    }
}
```
### 常见选项
有一些应用于两个或更多 agent 的实现的选项。他们不被要求，除非特别规定  
* label  
一个字符串。该标签用于运行流水线或个别的 stage；  
该选项对 node, docker 和 dockerfile 可用, `node`要求必须选择该选项
* customWorkspace
一个字符串。在自定义工作区运行应用了 agent 的流水线或个别的 stage, 而不是默认值。 它既可以是一个相对路径, 在这种情况下，自定义工作区会存在于节点工作区根目录下, 或者一个绝对路径。比如:
    ```
    agent {
        node {
            label 'my-defined-label'
            customWorkspace '/some/other/path'
        }
    }
    ```
该选项对 node, docker 和 dockerfile 有用  
* reuseNode  
一个布尔值, 默认为false。 如果是true, 则在流水线的顶层指定的节点上运行该容器, 在同样的工作区, 而不是在一个全新的节点上。  
这个选项对 docker 和 dockerfile 有用, 并且只有当 使用在个别的 stage 的 agent 上才会有效。
    ``` 
    pipeline {
        agent { docker 'maven:3-alpine' } //在一个给定名称和标签(maven:3-alpine)的新建的容器上执行定义在流水线中的所有步骤 
        stages {
            stage('Example Build') {
                steps {
                    sh 'mvn -B clean verify'
                }
            }
        }
    }
    ```
### 阶段级别的 agent 部分
```
pipeline {
    agent none //确保 an Executor 没有被分配，强制 stage 部分包含他自己的 agent 部分
    stages {
        stage('Example Build') {
            agent { docker 'maven:3-alpine' } 
            steps {
                echo 'Hello, Maven'
                sh 'mvn --version'
            }
        }
        stage('Example Test') {
            agent { docker 'openjdk:8-jre' } 
            steps {
                echo 'Hello, JDK'
                sh 'java -version'
            }
        }
    }
}
```
