---
title: 'Failed to connect to github.com port 443 after 21092 ms: Timed out解决 '
date: 2022-09-26 12:46:30
tags:
---
Failed to connect to github.com port 443 after 21092 ms: Timed out解决

由于之前翻墙，clash把电脑设置了代理，导致传代码到github的时候报错。

因此解决方法是取消掉代理，然后再上传代码

~~~ 
git config --global https.proxy
~~~



~~~ 
git config --global --unset http.proxy
~~~

~~~ 
git config --global --unset https.proxy
~~~

