---
title: jenkins-problem-GitPlugin访问https代码库失败
date: 2020-08-25
categories:
- jenkins
- problem
---
mac上出现jenkins job,clone https代码库失败
```
hudson.plugins.git.GitException: Failed to fetch from https://git.opendaylight.org/gerrit/p/integration.git
        at hudson.plugins.git.GitSCM.fetchFrom(GitSCM.java:627)
        at hudson.plugins.git.GitSCM.retrieveChanges(GitSCM.java:865)
        at hudson.plugins.git.GitSCM.checkout(GitSCM.java:890)
        at hudson.model.AbstractProject.checkout(AbstractProject.java:1415)
        at hudson.model.AbstractBuild$AbstractBuildExecution.defaultCheckout(AbstractBuild.java:652)
        at jenkins.scm.SCMCheckoutStrategy.checkout(SCMCheckoutStrategy.java:88)
        at hudson.model.AbstractBuild$AbstractBuildExecution.run(AbstractBuild.java:561)
        at hudson.model.Run.execute(Run.java:1678)
        at hudson.model.FreeStyleBuild.run(FreeStyleBuild.java:46)
        at hudson.model.ResourceController.execute(ResourceController.java:88)
        at hudson.model.Executor.run(Executor.java:231)
Caused by: hudson.plugins.git.GitException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
        at org.jenkinsci.plugins.gitclient.CliGitAPIImpl.checkCredentials(CliGitAPIImpl.java:2198)
        at org.jenkinsci.plugins.gitclient.CliGitAPIImpl.launchCommandWithCredentials(CliGitAPIImpl.java:1152)
        at org.jenkinsci.plugins.gitclient.CliGitAPIImpl.access$200(CliGitAPIImpl.java:87)
        at org.jenkinsci.plugins.gitclient.CliGitAPIImpl$1.execute(CliGitAPIImpl.java:266)
        at hudson.plugins.git.GitSCM.fetchFrom(GitSCM.java:625)
        ... 10 more
```
1.github使用的是DigiCert的证书，而opendaylight用的是StartCom的。StartCom颁发的证书是免费的。原因大概就是Java不信任这个CA。那么解决方法应该就是把这个CA添加到Java的信任列表。具体做法如下：  
1.首先要得到StartCom的证书文件（xxx.cer）。从哪里获得呢？既然浏览器能够正常访问，说明系统中是信任StartCom的证书的，所以先打开系统的证书管理界面。在Mac中是Keychain，打开之后找到StartCom的证书，然后右键导出成一个.cer文件，命名为startcom.cer。
2.cer文件导入到Java的运行时系统中
```
keytool -import -alias startcom  -keystore %JRE_HOME/lib/security/cacerts  -file startcom.cer
```
运行该命令时会提示输入密码，如果你没有改过的话密码是’changeit’,然后再运行下面的命令，就可以看到StartCom已经被加进去了。
```
keytool -list -keystore  %JRE_HOME/lib/security/cacerts  | less
```