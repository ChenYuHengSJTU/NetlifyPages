# OS (NJU-JYY)

---

## Lecture1

+ `model` checker
+ **学习 “任何东西” 的现代方法**
  + 使用辅助工具加速探索
  + 数值/符号计算：numpy, sympy, sage, Mathematica, ...
  + 可视化：matplotlib
    + All-in-one: [Jupyter](http://jupyter.org/) (2017 ACM Software System Award)
    + Life is short; you need Python
+ **会编程，你就拥有全世界！**
  - 同样的方式可以模拟任何数字系统 (包括计算机系统)
  - 同时还体验了 UNIX 哲学
    - Make each program do one thing well
    - Expect the output of every program to become the input to another

---

+ 如果你阅读示例代码遇到困难，可以想一想今天的大语言模型已经可以 **“阅读理解” 程序**的行为 (不过也有错误的地方)。
+ `Take away message`
  + *[Harley Hahn's Guide to Unix and Linux](http://www.harley.com/books/sg3.html)*
  + 常用的`linux`工具
    + `ssh server`
    + 查找文档的工具，例如 tldr 和 man
    + UNIX 系统管理的基础工具，请 STFW
    + GNU Make
+ 提问
  + `stackoverflow`
  + `chatgpt`

---

## Lecture2

+ gcc 编译出来的文件一点也不小
  + objdump 工具可以查看对应的汇编代码
  + ` --verbose`可以查看所有编译选项 (真不少)
    + printf 变成了 puts@plt
  + `-Wl,--verbose`可以查看所有链接选项 (真不少)
    + 原来链接了那么多东西
    + 还解释了 end 符号的由来
  + `-static` 会链接 libc (大量的代码)
+ [程序设计语言的形式语义](https://hongjin-liang.github.io/teaching/semantics/index.html)
+ 简单 C 程序的状态机模型 (语义)
  + [真的有这种工具](https://cil-project.github.io/cil/) (C Intermediate Language) 和[解释器](https://gitlab.com/zsaleeba/picoc)

---

+ `xxd`指令查看文件（`binary code`）
+ [GNU Coreutils](https://www.gnu.org/software/coreutils/) 和 [GNU Binutils](https://www.gnu.org/software/binutils/) 
+  [busybox](https://www.busybox.net/) 和 [toybox](https://landley.net/toybox/about.html)
+ 系统/工具程序
  - bash, binutils, apt, ip, ssh, vim, tmux, jdk, python, ...
    - 这些工具的原理不复杂 (例如 apt 是 dpkg 的套壳)，但琐碎
    - [Ubuntu Packages](https://packages.ubuntu.com/) (和 apt-file 工具) 支持文件名检索
+ **未来我们身边的 AI 将会根本性地改变我们消化信息的方式：我试着让 ChatGPT 解释一段 `ls` 命令的 strace 输出。可以说它十分完美地 “消化” 了互联网上的文档，并把最重要、最相关的内容呈现给我们。**
+ **Take away message**
  + 理解操作系统的重要工具：gcc, binutils, gdb, strace
    
---

## Lecture3

+ `init.gdb` 大幅简化了修改代码-执行调试-观测结果的流程。在这类基础设施上的投入是绝对值得的
+ ****思考做事的方式、大胆地问出好的问题，并且小心地去求证****。
+ **花几分钟创建一个小工具：“构建理解工具”**
  - UNIX Philosophy
  - 把复杂的构建过程分解成流程 + 可理解的单点

---

## Lecture4

+ `python`建模

---

## Lecture5

+ [Ad hoc synchronization 引发了很多系统软件中的 bugs](https://www.usenix.org/events/osdi10/tech/full_papers/Xiong.pdf)

---

## Lecture6 & Lecture7

+ **计算思维:写个程序 (model checker) 来辅助**
  - 任何机械的思维活动都可以用计算机替代
  - AI 还可以替代启发式/经验式的决策

---

+ [godbolt.org](http://godbolt.org/)
+ 🌶️ [Lockless Patterns: An Introduction to Compare-and-swap](https://lwn.net/Articles/847973/)
+ 🌶️️🌶️ [Is Parallel Programming Hard, And, If So, What Can You Do About It?](https://cdn.kernel.org/pub/linux/kernel/people/paulmck/perfbook/perfbook.html) (perfbook)
+ 🌶️🌶️🌶️ [The Art of Multiprocessor Programming](https://www.sciencedirect.com/book/9780124159501/the-art-of-multiprocessor-programming)
+ [Benchmarking crimes](https://www.cse.unsw.edu.au/~gernot/benchmarking-crimes.html)
+ [An analysis of Linux scalability to many cores](https://www.usenix.org/conference/osdi10/analysis-linux-scalability-many-cores) (OSDI'10)

---

## Lecture8

+ **你以为最不可能出 bug 的地方，往往 bug 就在那躺着**
+ **UNIX 世界里你做任何事情都是在编程**
+ **输入/配置可以看成是程序的一部分**
+ 想要更好的体验？
  - GDB 本身也是一个编程语言
    - 它甚至支持 Python
    - 我们可以执行一些初始化代码 (-x)
  - 库函数也是代码
    - directory 命令增加源码路径
  - GDB 有许多前端
    - cgdb, pwndbg, vscode, ...
  - [RTFM](https://sourceware.org/gdb/current/onlinedocs/gdb.html/) - M 比 ChatGPT 好用在于它不需要 prompt 且全面

---

## Lecture9
