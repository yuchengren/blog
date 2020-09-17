---
title: gitlab-配置
date: 2020-09-15
categories:
- gitlab
---
### 一、添加ssh公钥
①本机生成ssh keys
```
ssh-keygen -t rsa -C "qq513082359@gmail.com"
```
②找到本机的ssh公钥
~/.ssh/id_rsa.pub  
③Add an SSH key  
gitlab->settings->SSH keys  
