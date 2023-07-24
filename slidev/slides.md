---
theme: seriph
class: text-center
highlighter: shiki
---

# Harley Hahn's Guide to Unix and Linux

---

## 第一章 Unix简介

<hr>

Unix用起来很容易，但学起来很难

---

## 第二章 什么是Linux？什么是Unix？

### 什么是内核

+ 启动计算机的最后一个动作就是启动一个非常复杂的程序，称为内核
+ 内核所提供的基本服务
+ Linux相较于Unix使用了一个特殊的内核
+ Unix大多数使用单内核（还有一种内核：微内核）
<img class="absolute right-1 top-50 w-100 opacity-80"
src="https://raw.githubusercontent.com/ChenYuHengSJTU/NetlifyPages/unixguide/slidev/assets/kernel-1.png" alt="kernel" title="kernel"> 

### Unix=内核+实用工具

### GNU宣言摘录，GPL，（Free）BSD，System V

### 真命天子：Linus Torvalds

### Unix类型

+ Cygwin：Unix under Windows

---

## 第三章 Unix连接

---

### 主机和终端

理解控制台和终端的区别
+ 远程--终端
**SSH**

---

## 第四章 开始使用Linux

---

大多数人使用linux都是在访问一个共享的系统

### 注销

检查他人是否使用过您的Linux账户：last
+ last + username

---

## 第五章 Gui:图形用户界面

跟踪球

### X Window

+ 是一种可移植的，与硬件无关的窗口系统
+ 抽象层次
+ 窗口管理器与硬件之间的桥接器

### 桌面环境，桌面管理器

+ 桌面环境的选择

---

## 第六章 Unix工作环境

\<Alt-F4> 关闭窗口

\<Alt-Tab> 焦点切换

### 运行级别

### 多桌面/工作空间

+ 高效组织工作

### 配置文件

+ initlab
+ 有一些易用的程序可以帮助修改配置文件

### 系统启动或者停止时发生了什么事情

+ dmesg | less

---

## 第七章 Unix键盘使用

tty

### 修饰建：\<Ctrl>键
### Unix键盘信号

+ quit
    + \<Ctrl \>

### Bash：封闭eof信号

+ 因为^D会注销shell
+ IGNOREEOF=5
    + 忽略开头的^D多少次

### 显示键映射：stty -a
### 修改键映射：stty

---

### 新行字符的重要性

+ ^M:返回信号
+ ^J:换行信号，Unix中为新行字符
+ 每行以^M^J结束

---

## 第八章 能够立即使用的程序

+ which，type，whence
+ Unix提醒服务：calendar
+ 查看系统信息：uptime，hosttime，uname
+ 显示自己的信息：whoami，quota
+ 内置计算器bc

---

## 第九章 文档资料：Unix手册与info

+ man手册页指令
+ 联网进行搜寻
    + [man page online](http://man.he.net/)
    + [Linux man page](https://linux.die.net/man/)
+ whatis
+ apropos
    + 搜索单行命令描述
+ info：记录GNU工具
    + info和树，使用节点组织文档

---

## 第十章 命令语法

+ 输入多条命令
+ 命令语法
+ 空白符
+ 命令的描述形式

---

## 第十一章 shell

+ Bourne shell:sh,ksh,bash
+ C-shell:csh,tcsh
+ 临时改变shell

---

## 第十二章：使用shell：变量和选项

+ 环境变量和shell变量
+ shell选项

---

## 第十三章 使用shell：命令和定制

+ 非数字字母字符和元字符
+ 学习内部命令
+ 强引用，弱引用
+ 命令替换
+ 定制shell

---

## 第十四章 使用shell：初始化文件

+ .profile
+ .bash_profile

---

## 第十五章 标准I/O：重定向与管道

+ noclobber功能
+ 管道线分流：tee
+ 条件执行

---

## 第十六章 过滤器：简介和基本操作

+ 最有用的过滤器列表

---

## 第二十三章 Unix文件系统

+ 普通文件，目录，伪文件
    + 伪文件：特殊文件（设备文件），命名管道，proc文件
        + 硬件特殊文件，终端特殊文件:tty,伪设备特殊文件
+ 命名管道:mkfifo
+ <mark>proc文件系统</mark>
+ 根目录与usr目录
+ 存放程序文件的目录
+ 虚拟文件系统
    + 理解Unix文件系统与设备文件系统的差异
    + 基于磁盘的，网络文件，特殊用途文件系统

---

## 第二十四章 目录操作

+ rmdir
+ 使用目录栈：pushd，popd，dirs
+ ls
+ 掌握磁盘空间使用情况
+ dumpe2fs：检查超块
+ 文件管理器

---

## 第二十五章 文件操作

+ umask：改变文件权限
+ stat
+ locate数据库更新
+ find
    + 路径+测试+动作
+ xargs
    + 传入参数

---

## 第二十六章 进程和作业控制

+ init进程
+ 作业控制
    + 工具
    + 指定作业%
+ ps
+ top,prstat
+ fuser
+ kill
+ nice,renice
+ 守护进程
