---
title: Nginx重启的方法以及注意事项
slug: nginx-restart-method-and-precautions-zyhlkb
url: /post/nginx-restart-method-and-precautions-zyhlkb.html
date: '2023-10-26 17:17:03'
lastmod: '2023-11-15 14:23:08'
toc: true
tags:
  - Linux
  - Nginx
categories:
  - 技术分享
keywords: Linux,Nginx
isCJKLanguage: true
---



## 1.利用 linux 进程管理重启

```bash
ps -ef|grep nginx
```

将会列出 nginx 相关的进程号，如下所示

```bash
root@ubuntu:~# ps -ef|grep nginx
root      1773     1  0 May12 ?        00:00:00 nginx: master process nginx
nginx    22672  1773  0 01:58 ?        00:00:00 nginx: worker process
nginx    22673  1773  0 01:58 ?        00:00:00 nginx: worker process
root     23617 20075  0 02:29 pts/1    00:00:00 grep --color=auto nginx
```

之后再用 kil 命令即可终止 nginx 进程，再重新执行 nginx 即可

```bash
kill -9 pid
```

也可以多个同时终止

```bash
kill -9 1773 22672 
```

这样比较麻烦，而且这个过程中会中断服务的提供。那么有没有热配置，或者是不重启就可以生效呢？

答案当然是有的。那就是使用 nginx -s reload 命令。

## 2. nginx -s reload

s 代表的是向主进程发送信号。其中信号有 4 个，stop, quit, reopen, reload。

reload 就是重新加载的意思。`nginx -s reload`​ 命令，合起来的作用就是重新加载配置文件。使用此命令可以做到无缝切换服务

> 注意事项

* ​<span style="font-weight: bold;" data-type="strong">`nginx -s reload`</span>​ <span style="font-weight: bold;" data-type="strong"> 是平滑重启,不会强制结束正在工作的连接,需要等所有连接都结束才会重启。</span>
* <span style="font-weight: bold;" data-type="strong">强烈建议在使用</span> <span style="font-weight: bold;" data-type="strong">`nginx -s reload`</span>​<span style="font-weight: bold;" data-type="strong">时使用</span> <span style="font-weight: bold;" data-type="strong">`nginx -t`</span>​<span style="font-weight: bold;" data-type="strong">检查配置文件是否正确</span>

‍
