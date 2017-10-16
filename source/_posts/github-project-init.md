---
title: 新建github项目关联本地项目
date: 2017-10-13 16:07:26
tags: [git, github]
---

github上创建新的项目后，在本地拉取项目或者将本地的项目关联到建立的仓库。

```shell
# git clone git@github.com:xxxxxxxxx.git  
```

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

## 本地项目

```shell
# cd myProject
# git remote add origin git@github.com:xxxxx/xxxx/git
# git push origin master
```

