---
title: Linux后台运行和查看后台进程的方法
slug: linux-background-running-and-viewing-the-background-process-method-zhs2a7
url: >-
  /post/linux-background-running-and-viewing-the-background-process-method-zhs2a7.html
date: '2023-10-26 16:27:56'
lastmod: '2023-11-15 14:55:39'
toc: true
categories:
  - 技术分享
isCJKLanguage: true
---



## 1.nohub 命令

​<span style="font-weight: bold;" data-type="strong">`nohup`</span>​<span style="font-weight: bold;" data-type="strong">英文全称 no hang up（不挂起），用于在系统后台不挂断地运行命令，退出终端不会影响程序的运行。</span> 英文全称 no hang up（不挂起），用于在系统后台不挂断地运行命令，退出终端不会影响程序的运行。

​<span style="font-weight: bold;" data-type="strong"></span>`nohup`<span style="font-weight: bold;" data-type="strong"></span>​<span style="font-weight: bold;" data-type="strong"></span>命令，在默认情况下（非重定向时），会输出一个名叫 nohup.out 的文件到当前目录下，如果当前目录的 nohup.out 文件不可写，输出重定向到 <span style="font-weight: bold;" data-type="strong"></span> 命令，在默认情况下（非重定向时），会输出一个名叫 nohup.out 的文件到当前目录下，如果当前目录的 nohup.out 文件不可写，输出重定向到  <span style="font-weight: bold;" data-type="strong">$HOME/nohup.out</span>​ <span style="font-weight: bold;" data-type="strong"></span> 文件中。<span style="font-weight: bold;" data-type="strong"></span>  文件中。

### <span style="font-weight: bold;" data-type="strong">使用权限</span>

<span style="font-weight: bold;" data-type="strong"></span>所有使用者<span style="font-weight: bold;" data-type="strong"></span>所有使用者

### <span style="font-weight: bold;" data-type="strong">语法格式</span>

```bash
 nohup Command [ Arg … ] [　& ]
```

### <span style="font-weight: bold;" data-type="strong">参数说明：</span>

<span style="font-weight: bold;" data-type="strong">Command</span>​ <span style="font-weight: bold;" data-type="strong"></span>：要执行的命令。<span style="font-weight: bold;" data-type="strong"></span> ：要执行的命令。

<span style="font-weight: bold;" data-type="strong">Arg</span>​ <span style="font-weight: bold;" data-type="strong"></span>：一些参数，可以指定输出文件。<span style="font-weight: bold;" data-type="strong"></span> ：一些参数，可以指定输出文件。

 <span style="font-weight: bold;" data-type="strong">&amp;</span>​ <span style="font-weight: bold;" data-type="strong"></span>：让命令在后台执行，终端退出后命令仍旧执行。<span style="font-weight: bold;" data-type="strong"></span> ：让命令在后台执行，终端退出后命令仍旧执行。

### <span style="font-weight: bold;" data-type="strong">实例</span>

<span style="font-weight: bold;" data-type="strong"></span>以下命令在后台执行当前目录下的java程序<span style="font-weight: bold;" data-type="strong"></span>以下命令在后台执行当前目录下的java程序

```bash
nohup java -jar ***.jar &
```

<span style="font-weight: bold;" data-type="strong"></span>这时我们打开 root 目录 可以看到生成了 nohup.out 文件。<span style="font-weight: bold;" data-type="strong"></span> 这时我们打开 root 目录 可以看到生成了 nohup.out 文件。

<span style="font-weight: bold;" data-type="strong"></span>如果要停止运行，你需要使用以下命令查找到 nohup 运行脚本到 PID，然后使用 kill 命令来删除：<span style="font-weight: bold;" data-type="strong"></span> 如果要停止运行，你需要使用以下命令查找到 nohup 运行脚本到 PID，然后使用 kill 命令来删除：

```bash
ps -aux | grep "***.jar"
```

<span style="font-weight: bold;" data-type="strong"></span>参数说明：<span style="font-weight: bold;" data-type="strong"></span> 参数说明：

* <span style="font-weight: bold;" data-type="strong">a</span>​ <span style="font-weight: bold;" data-type="strong"></span> : 显示所有程序<span style="font-weight: bold;" data-type="strong"></span> : 显示所有程序
* <span style="font-weight: bold;" data-type="strong">u</span>​ <span style="font-weight: bold;" data-type="strong"></span> : 以用户为主的格式来显示<span style="font-weight: bold;" data-type="strong"></span> : 以用户为主的格式来显示
* <span style="font-weight: bold;" data-type="strong">x</span>​ <span style="font-weight: bold;" data-type="strong"></span> : 显示所有程序，不区分终端机<span style="font-weight: bold;" data-type="strong"></span> : 显示所有程序，不区分终端机

<span style="font-weight: bold;" data-type="strong"></span>另外也可以使用 <span style="font-weight: bold;" data-type="strong"></span> 另外也可以使用 <span style="font-weight: bold;" data-type="strong">ps -def | grep &quot;runoob.sh</span>​ <span style="font-weight: bold;" data-type="strong"></span>&quot; 命令来查找。<span style="font-weight: bold;" data-type="strong"></span> " 命令来查找。

<span style="font-weight: bold;" data-type="strong"></span>找到 PID 后，就可以使用 kill PID 来删除。<span style="font-weight: bold;" data-type="strong"></span> 找到 PID 后，就可以使用 kill PID 来删除。

```
kill -9  进程号PID
```

<span style="font-weight: bold;" data-type="strong"></span>以下命令在后台执行 root 目录下的 <span style="font-weight: bold;" data-type="strong"></span> 以下命令在后台执行 root 目录下的 <span style="font-weight: bold;" data-type="strong"></span>runoob.sh<span style="font-weight: bold;" data-type="strong"></span> 脚本，并重定向输入到 runoob.log 文件：

```
nohup java -jar <span style="font-weight: bold;" data-type="strong">*.jar > </span>*.log 2>&1 &
```

<span style="font-weight: bold;" data-type="strong">2&gt;&amp;1</span> 解释：

将标准错误 2 重定向到标准输出 &1 ，标准输出 &1 再被重定向输入到 ***.log 文件中。

* 0 – stdin (standard input，标准输入)
* 1 – stdout (standard output，标准输出)
* 2 – stderr (standard error，标准错误输出)

## 2.screen 命令

​<span style="font-weight: bold;" data-type="strong">`screen`</span>​ 是一个在 Unix 和 Unix-like 操作系统中使用的终端复用工具，它允许用户在一个终端窗口中同时运行多个独立的终端会话。这个工具非常有用，因为它可以帮助您在同一个终端窗口中运行多个任务，而不必打开多个终端窗口。以下是一些常见的 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 命令和用法：

1. <span style="font-weight: bold;" data-type="strong">启动 </span>​<span style="font-weight: bold;" data-type="strong">`screen`</span>​ <span style="font-weight: bold;" data-type="strong"> 会话</span>​<span style="font-weight: bold;" data-type="strong"></span><span style="font-weight: bold;" data-type="strong"></span> ：

    ```bash
    screen
    ```

    运行这个命令后，您将进入一个新的 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话。在这个会话中，您可以执行命令，运行程序，然后将其分离（detach）以后台运行。
2. <span style="font-weight: bold;" data-type="strong">分离 </span>​<span style="font-weight: bold;" data-type="strong">`screen`</span>​ <span style="font-weight: bold;" data-type="strong"> 会话</span>​<span style="font-weight: bold;" data-type="strong"></span><span style="font-weight: bold;" data-type="strong"></span> ：  
    在 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话中，您可以使用以下组合键将会话分离到后台：Ctrl-a  
    这将让 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话继续在后台运行，而您可以回到原来的终端窗口。
3. <span style="font-weight: bold;" data-type="strong">列出 </span>​<span style="font-weight: bold;" data-type="strong">`screen`</span>​ <span style="font-weight: bold;" data-type="strong"> 会话</span>​<span style="font-weight: bold;" data-type="strong"></span><span style="font-weight: bold;" data-type="strong"></span> ：  
    要列出当前的 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话，您可以运行以下命令：

    ```bash
    screen -ls
    ```

    这将显示当前运行的 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话的列表。
4. <span style="font-weight: bold;" data-type="strong">重新连接到 </span>​<span style="font-weight: bold;" data-type="strong">`screen`</span>​ <span style="font-weight: bold;" data-type="strong"> 会话</span>​<span style="font-weight: bold;" data-type="strong"></span><span style="font-weight: bold;" data-type="strong"></span> ：  
    要重新连接到以前分离的 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话，使用以下命令，其中  <span style="font-weight: bold;" data-type="strong">`<session_name>`</span> ​ 是您要重新连接的会话的名称或 ID：

    ```bash
    screen -r <session_name>
    ```
5. <span style="font-weight: bold;" data-type="strong">创建具有自定义名称的 </span>​<span style="font-weight: bold;" data-type="strong">`screen`</span>​ <span style="font-weight: bold;" data-type="strong"> 会话</span>​<span style="font-weight: bold;" data-type="strong"></span><span style="font-weight: bold;" data-type="strong"></span> ：  
    您可以使用以下命令创建一个具有自定义名称的 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话：

    ```bash
    screen -S <session_name>
    ```

    这将创建一个新的 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话并为其指定名称。
6. <span style="font-weight: bold;" data-type="strong">结束 </span>​<span style="font-weight: bold;" data-type="strong">`screen`</span>​ <span style="font-weight: bold;" data-type="strong"> 会话</span>​<span style="font-weight: bold;" data-type="strong"></span><span style="font-weight: bold;" data-type="strong"></span> ：  
    要结束 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话，可以在会话中运行 <span style="font-weight: bold;" data-type="strong">`exit`</span>​ 命令，或者按下 <span style="font-weight: bold;" data-type="strong">`Ctrl-d`</span>​<span style="font-weight: bold;" data-type="strong"></span><span style="font-weight: bold;" data-type="strong"></span> 。
7. <span style="font-weight: bold;" data-type="strong">帮助</span>​<span style="font-weight: bold;" data-type="strong"></span><span style="font-weight: bold;" data-type="strong"></span> ：  
    如果需要查看更多 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 的命令和选项，可以在 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话中按下 <span style="font-weight: bold;" data-type="strong">`Ctrl-a ?`</span> ​，这将显示帮助信息。

​<span style="font-weight: bold;" data-type="strong">`screen`</span>​ 是一个非常强大的工具，特别适合在 SSH 连接中管理多个任务或会话。您可以在 <span style="font-weight: bold;" data-type="strong">`screen`</span>​ 会话中运行长时间运行的进程，然后分离会话，以便在稍后重新连接并查看输出。这对于远程服务器管理和维护非常有用。

‍
