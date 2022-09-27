---
title: 'hexo个人博客搭建，保姆级教学 '
date: 2022-09-20 11:46:30
tags: hexo
sticky: 1
cover: https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/wallpaper4.png
---
hexo个人博客搭建，保姆级教学

### 前期准备

node.js

git

### 安装步骤

#### 1安装hexo

``` 
npm install -g hexo-cli
```

检查是否安装成功

``` 
hexo -v
```

#### 2新建github仓库

作为hexo的服务器，装在github的仓库中

**注意** 仓库的名字是固定的：你github的名字.github.io

#### 3生成sshkeys

让github与本地进行绑定

git bash here

输入ssh，检查我们有没有安装过ssh

然后输入命令

ssh-keygen -t rsa -C "1031155817@qq.com"

![image-20220918153306169](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/image-20220918153306169.png)

按四次回车

打开下面那个全选

打开github新建keys

把钥匙放进去

然后确定是否绑定成功

ssh -T git@github.com

![image-20220918153517529](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/image-20220918153517529.png)

#### 4本地生成博客的具体内容

hexo init  --初始化博客

hexo s   --静态生成本地的hexo页面（打开了本地的服务器）

#### 5将博客发布到github

配置文件修改(_config.yml)

``` yml
deploy:
  type: git
  repository: 项目仓库的HTTPS链接
  branch: main
```

安装hexo-deployer-git自动部署发布工具:为博客安装上传插件

npm install hexo-deployer-git --save

hexo g

hexo d #上传