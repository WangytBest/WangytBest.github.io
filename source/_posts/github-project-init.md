---
title: git基础
date: 2017-10-13 16:07:26
tags: [git, github]
categories: [Git]
toc: true
thumbnail: http://cloud.xuww.wang/nianshaodeni.png
---

github上创建新的项目后，在本地拉取项目或者将本地的项目关联到建立的仓库。

```shell
# git clone git@github.com:xxxxxxxxx.git  
```

<!-- more -->
## 命令行新建一个新的仓库

```shell
# mkdir myProject
# cd myProject 
# echo '# my new project' >> README.md
# git init
# git add .
# git commit -m "first commit"
# git remote add origin git@github.com:xxxxxxxxx.git
# git push origin master
```

## 本地项目关联远程git仓库

```shell
# cd myProject
# git remote add origin git@github.com:xxxxx/xxxx/git
# git push origin master
```

# 本地分支关联远程分支

```shell
# git checkout test
# git remote add origin git@github.com:xxxx/test.git
```

## fatal
首次拉取代码失败

> git pull错误信息 : 
```shell
 * branch       master     -> FETCH_HEAD
 fatal: refusing to merge unrelated histories
```

解决：
```shell
# git pull origin master --allow-unrelated-histories
```

## 首次安装git设置
```shell
# git config -global user.nme "xxxxxx"
# git config -global user.email "xxxxxx@jd.com"
```

# 公钥密钥配置

```shell
# ssh-keygen -t rsa
```
会生成两个文件：`id_rsa`（密钥）和`id_rsa.pub`（公钥）
在github中设置公钥。
