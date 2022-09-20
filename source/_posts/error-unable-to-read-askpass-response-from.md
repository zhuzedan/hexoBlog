---
title: 'error: unable to read askpass response from '' '
date: 2022-09-20 12:46:30
tags:
---
### error: unable to read askpass response from '' 

今天上班跟平常一样pull代码，发现竟然拉不下来。

![image-20220920095815254](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/%20img/image-20220920095815254.png)

上网查询后得到解决方案

打开自己项目根目录的.git文件，打开config文件

![image-20220920100042312](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/%20img/image-20220920100042312.png)

修改url的内容

修改前

![image-20220920100148285](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/%20img/image-20220920100148285.png)

修改

http://用户名(或者你的邮箱):密码@192.168.....

修改后

``` 
url = http://zhuzedan:zzd@192.168.2.18:2017/tianyige/v2/admin_antdv.git
```

再次拉取代码，成功！

![image-20220920100610104](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/%20img/image-20220920100610104.png)
