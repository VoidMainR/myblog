---
title: 关于使用Hexo创建个人博客CI调整
date: 2019-10-29 16:03:41
tags: 踩坑记录
---
&emsp;最近突然想做一个自己的博客主页，物色了一下最终选择了使用[hexo]("https://hexo.io/zh-cn/)框架。官网的教程和其他大佬的教程都已经很详细了，在这里我就不赘述了。  

&emsp;本文主要是解决官网关于使用Travis CI自动部署的一个坑。

&emsp;首先官方的hexo官方给的[github主页部署教程](https://hexo.io/zh-cn/docs/github-pages)一路走下去会发现一个问题就是Travis CI在构建的时候会在项目中创建一个gh-page分支，然而你去设置github Page的source的时候你会看到：
>User pages must be built from the master branch.  

&emsp;也就是说，github现在变了它不能够选其他分支了。那也不能不用CI啊，毕竟我这么懒~  所以我们可以稍微改造一下，把需要CI的代码，也就是hexo生成的项目带啊吗放在隔壁分支，然后修改官网给的.travis.yml  

官网给的是这个亚子的：
``` yml
sudo: false
language: node_js
node_js:
  - 10 # use nodejs v10 LTS
cache: npm
branches:
  only:
    - master # build master branch only
script:
  - hexo generate # generate static files
deploy:
  provider: pages
  skip-cleanup: true
  github-token: $GH_TOKEN
  keep-history: true
  on:
    branch: master
  local-dir: public
```

&emsp;我们需要做的是修改构建分支&修改目标分支，假如我们放hexo项目的分支叫hexoPrj，将文件改为:
``` yml
sudo: false
language: node_js
node_js:
  - 10 # use nodejs v10 LTS
cache: npm
branches:
  only:
    - hexoPrj # build master branch only
script:
  - hexo generate # generate static files
deploy:
  provider: pages
  skip-cleanup: true
  github-token: $GH_TOKEN
  keep-history: true
  target_branch: master
  on:
    branch: hexoPrj
  local-dir: public
```
这里我修改了编译分支，添加了一个参数target_branch来指定构建的目标分支，这样就可以愉快的使用CI来省去每次都要构建发布的麻烦了。其实还有很多参数可以用，想了解的可以移步[Travis官网的文档](https://docs.travis-ci.com/user/deployment/pages/)