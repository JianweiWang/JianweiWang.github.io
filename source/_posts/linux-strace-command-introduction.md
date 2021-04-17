---
title: linux strace command introduction
date: 2019-05-27 23:23:02
tags: linux perf tools
---
## Linux strace 命令

### 简介
strace（trace system calls and signals）命令是linux系统下的一款调试利器，用来跟踪进程执行时的系统调用和所接收的信号。 在Linux世界，进程不能直接访问硬件设备，当进程需要访问硬件设备(比如读取磁盘文件，接收网络数据等等)时，必须由用户态模式切换至内核态模式，通过系统调用访问硬件设备。strace可以跟踪到一个进程产生的系统调用,包括参数，返回值，执行消耗的时间等。

<!--more-->

### 安装
Ubuntu系统已默认安装了strace，centos系列可以使用yum命令安装。当然，也可以直接通过源码安装，源码链接：https://github.com/strace/strace

### 常见用法
```shell
strace [-ACdffhikqrtttTvVxxy] [-ACdffhiqrtttTvVxxy] [-I n]
              [-b execve] [-e expr]... [-a column] [-o file] [-s strsize]
              [-X format] [-P path]... [-p pid]... { -p pid | [-D]
              [-E var[=val]]... [-u username] command [args] }

strace -c [-df] [-I n] [-b execve] [-e expr]... [-O overhead]
              [-S sortby] [-P path]... [-p pid]... { -p pid | [-D]
              [-E var[=val]]... [-u username] command [args] }

```

常见参数说明

```
1. -c -- count time, calls, and errors for each syscall and report summary
为每个系统调用计算时间、调用、错误，并报告摘要

2. -f -- follow forks, -ff -- with output into separate files
-f 跟踪fork的进程；-ff 把输出定向到独立的文件

3. -F -- attempt to follow vforks, -h -- print help message
-F 尝试跟踪vfork的进程，当今平台与-f功能相同；-h 打印帮助信息

4. -i -- print instruction pointer at time of syscall
在系统调用时，打印指令指针

5. -q -- suppress messages about attaching, detaching, etc.
抑制附加、分离等信息

6. -r -- print relative timestamp, -t -- absolute timestamp, -tt -- with usecs
-r 打印相对时间戳；-t 绝对时间戳；-tt 微秒

7. -T -- print time spent in each syscall, -V -- print version
-T 打印每个系统调用的时间花费；-V 打印版本

8. -v -- verbose mode: print unabbreviated argv, stat, termio[s], etc. args
-v 详细模式，打印非简略的参数、状态、termio[s]等

9. -x -- print non-ascii strings in hex, -xx -- print all strings in hex
-x 打印非ascii的字符串为16进制；-xx 打印所有的字符串为16进制

10. -a column -- alignment COLUMN for printing syscall results (default 40)
对系统调用结果对齐列（默认为40列）

11. -e expr -- a qualifying expression: option=[!]all or option=[!]val1[,val2]...
    options: trace, abbrev, verbose, raw, signal, read, or write
在-e后附表达式。一个合格的表达式：选项=[!]所有 或者 选项=[!]值1[,值2]....；可选项:跟踪、缩写、冗长、原始的东东、信号、读、写。

12. -o file -- send trace output to FILE instead of stderr
发送跟踪输出到文件，而不是stderr

13. -O overhead -- set overhead for tracing syscalls to OVERHEAD usecs
设置跟踪系统调用的最大时间

14. -p pid -- trace process with process id PID, may be repeated
跟踪值为ID的进程，可以重复多个哦(注：最多32个)

15. -s strsize -- limit length of print strings to STRSIZE chars (default 32)
限制打印字符串的最大长度，默认为32字节

16. -S sortby -- sort syscall counts by: time, calls, name, nothing (default time)
排序，以系统调用过程中的时间、或者调用名等作为排序项。

17. -u username -- run command as username handling setuid and/or setgid
以其他用户名或者组名运行命令

18. -E var=val -- put var=val in the environment for command
设置环境变量

19. -E var -- remove var from the environment for command
清除环境变量
```

更详细的用法可以用man strace获取。
