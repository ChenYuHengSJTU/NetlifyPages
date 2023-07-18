---
highlighter: shiki
---

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

## Lecture9 并发控制：同步(1)

+ 掌握生产者-消费者问题：可以解决99%的并发控制问题
+ 并发：小心！
    + 压力测试 + 观察输出结果
    + 自动观察输出结果：pc-check.py
    + 未来：copilot 观察输出结果，并给出修复建议

---

#### 条件变量：理想与实现之间的折中

一把互斥锁 + 一个 “条件变量” + 手工唤醒

+ wait(cv, mutex) 💤
    + 调用时必须保证已经获得 mutex
    + wait 释放 mutex、进入睡眠状态
    + 被唤醒后需要重新执行 lock(mutex)
+ signal/notify(cv) 💬
    + 随机私信一个等待者：醒醒
    + 如果有线程正在等待 cv，则唤醒其中一个线程
+ broadcast/notifyAll(cv) 📣
    + 叫醒所有人
    + 唤醒全部正在等待 cv 的线程

---

```c
void Tproduce() {
  mutex_lock(&lk);
  if (!CAN_PRODUCE) cond_wait(&cv, &lk);
  printf("("); count++; cond_signal(&cv);
  mutex_unlock(&lk);
}
void Tconsume() {
  mutex_lock(&lk);
  if (!CAN_CONSUME) cond_wait(&cv, &lk);
  printf(")"); count--; cond_signal(&cv);
  mutex_unlock(&lk);
}
```
等待条件满足时
```c
mutex_lock(&mutex);
while (!COND) {
  wait(&cv, &mutex);
}
assert(cond);  // 互斥锁保证条件成立
mutex_unlock(&mutex);
```
条件满足时
```c
mutex_lock(&mutex);
// 任何可能使条件满足的代码
broadcast(&cv);
mutex_unlock(&mutex);
```

---

+ cond_wait(cv, lk) 释放互斥锁 lk 并进入睡眠状态。注意被唤醒时，cond_wait 会重新试图获得互斥，直到获得互斥锁后才能返回。
+ cond_signal(cv) 唤醒一个在 cv 上等待的线程
+ cond_broadcast(cv) 唤醒所有在 cv 上等待的线程

#### Others
+ ASCII Art

---

## Lecture10 并发控制：同步(2)

<hr>

### 信号量：一种条件变量的特例

```c
void P(sem_t *sem) { // wait
  wait_until(sem->count > 0) {
    sem->count--;
  }
}

void V(sem_t *sem) { // post (signal)
  atomic {
    sem->count++;
  }
}
```

正是因为条件的特殊性，信号量不需要 broadcast:
+ P 失败时立即睡眠等待
+ 执行 V 时，唤醒任意等待的线程

---

#### Take-away Message
+ 抛开 workload 谈优化就是耍流氓

---

## Lecture11 真实世界的并发编程

<hr>

### Take-away Messages
+ 计算图并发编程的真实应用场景
    + 高性能计算 (注重任务分解)：生产者-消费者 (MPI/OpenMP)
    + 数据中心 (注重系统调用)：线程-协程 (Goroutine)
    + 人工智能：高性能计算 + 数据中心
    + 人机交互 (注重易用性)：事件-流图 (Promise)
+ 编程工具的发展突飞猛进
    + 开源社区和人工智能彻底改变了计算机科学的学习方式
    + 选择你的主力现代编程语言：Modern C++, Rust, Javascript, Scala/Kotlin/Java, ...

---

## Lecture12 真实世界的并发Bug

<hr>

#### 死锁产生的必要条件

#### 数据竞争
用锁保护好共享数据，消灭一切数据竞争

不同的线程同时访问同一内存，且至少有一个是写

“内存” 可以是地址空间中的任何内存
+ 可以是全部变量
+ 可以是堆区分配的变量
+ 可以是栈

“访问” 可以是任何代码
+ 可能发生在你的代码里
+ 可以发生在框架代码里
+ 可能是一行你没有读到过的汇编代码
+ 可能时一条 ret 指令

---

### Take-away Message
人类本质上是 sequential creature，因此总是通过 “块的顺序执行” 这一简化模型去理解并发程序，也相应有了两种类型的并发 bugs：
+ Atomicity violation，本应原子完成不被打断的代码被打断
+ Order violation，本应按某个顺序完成的未能被正确同步

---

## Lecture13 并发Bug的应对

<hr>

### 死锁的应对

+ Bullshit
+ Lock ordering
    + 避免循环等待

虽然不太愿意承认，但始终假设自己的代码是错的

(因为机器永远是对的)

### 防御性编程

+ 把程序需要满足的条件用 assert 表达出来。
+ 使用宏明确变量含义

---

### 自动运行时检查

<hr>

#### Lockdep: 运行时 Lock Ordering 检查

+ Lockdep 的实现
    + Since Linux Kernel 2.6.17, also in OpenHarmony!

#### ThreadSanitizer: 运行时的数据竞争检查

---

#### 更多的Sanitizers

现代复杂软件系统必备的支撑工具

+ [ AddressSanitizer](https://clang.llvm.org/docs/AddressSanitizer.html)(asan); ([paper](https://www.usenix.org/conference/atc12/technical-sessions/presentation/serebryany)): 非法内存访问
    + Buffer (heap/stack/global) overflow, use-after-free, use-after-return, double-free, ...
    + Linux Kernel 也有[kasan](https://www.kernel.org/doc/html/latest/dev-tools/kasan.html) 
+ [ThreadSanitizer](https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html)(tsan): 数据竞争
+ [MemorySanitizer](https://clang.llvm.org/docs/MemorySanitizer.html) (msan): 未初始化的读取
+ [UBSanitizer](https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html)(ubsan): undefined behavior
    + Misaligned pointer, signed integer overflow, ...
    + Kernel 会带着 -fwrapv 编译
+ IntelliSanitize

各类 sanitizer 给我们带来的启发是：如果我们能清楚地追溯到问题产生的本源，我们就总是能找到好的应对方法——甚至是我们可以构造低配版的 “近似” sanitizer，它们在暗中帮助你实现 fail-fast 的程序，从而减轻你调试问题的负担。

---

## Lecture14 多处理器系统与中断

<hr>

### 中断：奠定操作系统 “霸主地位” 的机制

操作系统内核 (代码)

+ 想开就开，想关就关

应用程序

+ 对不起，没有中断
    + 在 gdb 里可以看到 flags 寄存器 (FL_IF)
    + [CLI — Clear Interrupt Flag](https://www.felixcloutier.com/x86/cli)        
        + #GP(0) If CPL is greater than IOPL and less than 3
        + 试一试 asm volatile ("cli");
+ 死循环也可以被打断

### [50行实现操作系统内核](https://jyywiki.cn/OS/2023/slides/14.3.slides)

---

## Lecture15 操作系统上的进程

<hr>

### fork 
阅读程序，写出运行结果
```c
for (int i = 0; i < 2; i++) {
  fork();
  printf("Hello\n");
}
```
状态机视角帮助我们严格理解程序行为

+ ./a.out
+ ./a.out | cat
    + 计算机系统里没有魔法
    + (无情执行指令的) 机器永远是对的

---

### 结束程序执行的三种方法
exit 的几种写法 (它们是不同)

+ exit(0) - stdlib.h 中声明的 libc 函数
    + 会调用 atexit
+ _exit(0) - glibc 的 syscall wrapper
    + 执行 “exit_group” 系统调用终止整个进程 (所有线程)
        + 细心的同学已经在 strace 中发现了
    + 不会调用 atexit
+ syscall(SYS_exit, 0)
    + 执行 “exit” 系统调用终止当前线程
    + 不会调用 atexit

---

## Take-away Message

因为 “程序 = 状态机”，操作系统上进程 (运行的程序) 管理的 API 很自然地就是状态机的管理。在 UNIX/Linux 世界中，这是通过以下三个最重要的系统调用实现的：
+ fork: 对当前状态机状态进行完整复制
+ execve: 将当前状态机状态重置为某个可执行文件描述的状态机
+ exit: 销毁当前状态机

---

## Lecture16 Linux操作系统

<hr>

> Hello, everybody out there using minix – I’m doing a (free) operating system (just a hobby, won’t be big and professional like gnu) for 386(486) AT clones. This has been brewing since April, and is starting to get ready.
>
>                                       —— Linus Torvalds (时年 21 岁)

### Linux 的 “两面”

#### Kernel

+ 加载第一个进程
    + 相当于在操作系统中 “放置一个位于初始状态的状态机”
    + Single user model (高权限)
+ 包含一些进程可操纵的操作系统对象
+ 除此之外 “什么也没有”
    + Linux 变为一个中断 (系统调用) 处理程序

---

#### Linux Kernel 系统调用上的发行版和应用生态

+ 系统工具 coreutils, binutils, systemd, ...
+ 桌面系统 Gnome, xfce, Android
+ 应用程序 file manager, vscode, ...

### [构建最小Linux系统](https://jyywiki.cn/OS/2023/slides/16.2.slides)

### Take-away Message

我们从 CPU Reset 后的 “硬件初始状态” 到操作系统加载完 init 进程后的 “软件初始状态”，从此以后，计算机系统中的一切都是由应用程序主导的，<mark>操作系统只是提供系统调用这一服务接口</mark>。正是系统调用 (包括操作系统中的对象) 这个稳定的、向后兼容的接口随着历史演化和积累，形成了难以逾越的技术屏障，在颠覆性的技术革新到来之前，另起炉灶都是非常困难的。

---

## Lecture17 Linux进程的地址空间

<hr>

### 查看进程的地址空间
pmap (1) - report memory of a process

+ Claim: pmap 是通过访问 procfs (/proc/) 实现的
+ 如何验证这一点？

查看进程的地址空间

+ 等程序运行起来后 (gdb)，使用 pmap 命令查看地址空间
+ 地址空间是若干连续的 “内存段”
    + “段” 的内存可以根据权限访问
    + 不在段内/违反权限的内存访问 触发 SIGSEGV

---

### 操作系统提供查看进程地址空间的机制

RTFM: /proc/[pid]/maps (man 5 proc)

+ 进程地址空间中的每一段
    + 地址 (范围) 和权限 (rwxsp)
    + 对应的文件: offset, dev, inode, pathname
        + TFM 里有更详细的解释
    + 和 readelf (-l) 里的信息互相验证

#### RTFM (5 proc): 我们发现的宝藏
+ vdso (7): Virtual system calls: 只读的系统调用也许可以不陷入内核执行。
+ 无需陷入内核的系统调用
    + 例子: gettimeofday (2)
    + [RTFSC](https://elixir.bootlin.com/linux/latest/source/lib/vdso/gettimeofday.c#L49) (非常聪明的实现)

---

### 进程地址空间管理

```c
// 映射
void *mmap(void *addr, size_t length, int prot, int flags,
           int fd, off_t offset);
int munmap(void *addr, size_t length);

// 修改映射权限
int mprotect(void *addr, size_t length, int prot);
```

本质：在状态机状态上增加/删除/修改一段可访问的内存

+ mmap: 可以用来申请内存 (MAP_ANONYMOUS)，也可以把文件 “搬到” 进程地址空间中

##### Memory-Mapped File: 一致性
如果把页面映射到文件

修改什么时候生效？

请查阅手册，看看操作系统是如何规定这些操作的行为的

例如阅读 msync (2)

这才是操作系统真正的复杂性

---

### [入侵进程地址空间](https://jyywiki.cn/OS/2023/slides/17.3.slides)

一些入侵进程地址空间的例子

+ 调试器 (gdb)
    + gdb 可以任意观测和修改程序的状态
+ Profiler (perf)
    + 合理的需求，操作系统就必须支持 → Ask GPT!
    + [Intel Processor Trace](https://perf.wiki.kernel.org/index.php/Perf_tools_support_for_Intel%C2%AE_Processor_Trace)

---

## Lecture18

<hr>

代码里的细节
+ Guidelines
    + [Google](https://google.github.io/styleguide/cppguide.html), [GNU](https://www.gnu.org/prep/standards/html_node/Writing-C.html), [CERT-C](https://wiki.sei.cmu.edu/confluence/display/c/SEI+CERT+C+Coding+Standard)

Programming for fun

+ [The International Obfuscated C Code Contest](https://www.ioccc.org/)
    + 写出绝对不可读，但又绝对可用的代码
    + [一个程序的诞生](https://jyywiki.cn/pages/OS/img/ioccc-spoiler.html)

---

### 计算机系统公理

1. 机器永远是对的
    + (ICS PA/OS Labs: 怕是不用多说了)
2. 未测代码永远是错的
    + (ICS PA/OS Labs: 怕是不用多说了)
3. 让你感到不适的 tedious 工作，一定有办法提高效率
    + 推论：我们应该分辨出什么工作是 tedious 的


“三省吾身：滚去编程了吗？写测试用例了吗？回看自己的工作流程了吗？”

+ AI 构建学习阶梯
+ 在方方面面强迫我们三省吾身
+ 人类文明进入新纪元

---

## Lecture19 系统调用和 UNIX Shell

<hr>

### 阅读代码

应该如何阅读代码？

+ strace
    + 适当的分屏和过滤
    + AI 使阅读文档的成本大幅降低
+ gdb
    + AskGPT: How to debug a process that forks children processes in gdb?
        + AI 也可以帮你解释 (不用去淘文档了)
    + 以及，定制的 visualization
        + 对于 Shell，我们应该显示什么？

---

## Lecture20 C标准库和实现

<hr>

### 应该怎么学习

C 是 “高级汇编”，一定有为嵌入式设备实现的简化 libc

+ uclibc, [newlib](https://sourceware.org/newlib/), [bionic](https://github.com/aosp-mirror/platform_bionic), ...
+ 今天的选择：[musl](https://musl.libc.org/)
    + musl-gcc 静态编译

### [libc基本功能](https://jyywiki.cn/OS/2023/slides/20.2.slides)
+ [Freestanding环境](https://en.cppreference.com/w/cpp/freestanding)

### [操作系统对象与环境](https://jyywiki.cn/OS/2023/slides/20.3.slides)

environ (7)

+ 我们也可以实现自己的 env.c
    + 问题来了：environ 是谁赋值的？
    + 是时候请出我们的老朋友 watch point 了

---

### [动态内存管理](https://jyywiki.cn/OS/2023/slides/20.4.slides)

##### 如何分配一大段内存

直接问操作系统要就好啦

+ 用 MAP_ANONYMOUS 申请，想多少就有多少
    + 超过物理内存上限都行
+ workload
+ 现实世界中的malloc/free

### Take-away Message

在系统调用和语言机制的基础上，libc 为我们提供了开发跨平台应用程序的 “第一级抽象”。在此基础上构建起了万千世界：C++ (扩充了 C 标准库)、Java、浏览器世界……今天，C 语言在应用开发方面有很多缺陷，但仍然为 “第一级抽象” 提供了一个有趣的范本：

+   [C is not a low-level language](https://dl.acm.org/doi/pdf/10.1145/3209212)
+   [C isn't a programming language any more](https://gankra.github.io/blah/c-isnt-a-language/)

---

## Lecture21 可执行文件和加载(1)

<hr>

### 静态加载和链接

##### 在操作系统上实现 ELF Loader
加载器 (loader) 的职责

+ 解析数据结构
+ 创建进程初始状态
    + argv, envp, ...
    + 再一次，System V ABI
+ 跳转执行

代码示例

+ 能正确处理参数/环境变量 env.c

---

### <mark>[动态链接和加载](https://jyywiki.cn/OS/2023/slides/21.3.slides)</mark>

+ [Semantic Versioning](https://semver.org/)

---

## Lecture22 可执行文件和加载(2)

<hr>

### [动态链接与加载原理](https://jyywiki.cn/OS/2023/slides/22.1.slides)

### [ELF动态链接与加载](https://jyywiki.cn/OS/2023/slides/22.2.slides)

### [LD_PRELOAD](https://jyywiki.cn/OS/2023/slides/22.3.slides)

+ 能否链接我们 “修改” 过的 libc？
    + 我们就不用像修改器那样 “入侵” 地址空间了

LD_PRELOAD: 在加载之前 preload

+ 利用动态链接特性：符号先到先占坑
+ 先加载一个自己的库，占据符号
 
其他操作系统上的 Hooking

---

## Lecture23 应用视角的操作系统 (回顾)

<hr>

###  ️[🌶️ 状态机：建模理解程序的世界](https://jyywiki.cn/OS/2023/slides/23.3.slides)

#### Trace和调试器
+ strace/gdb
+ 我们甚至可以完整记录程序的执行
    + [rr](https://dl.acm.org/doi/10.1145/3386277), QEMU, ...

#### 性能优化和Profiler

> Premature optimization is the root of all evil. (D. E. Knuth)

Linux Kernel perf (支持硬件 PMU)

+ perf list, perf stat (-e), perf record, perf report

##### 实际中的性能优化

+ [The Flame Graph](https://cacm.acm.org/magazines/2016/6/202665-the-flame-graph/fulltext)

---

#### Model Checker 和 Verifier

一些真正的 model checkers

+ TLA+ by Leslie Lamport;
+ Java PathFinder (JFP) 和 SPIN

---

## Lecture24 进程的实现

<hr>

+ VR眼镜

进程在操作系统中的实现是简单又复杂的。从简单来说，进程就是带有独立地址空间的线程；通过硬件提供的分页机制，就能给线程戴上 “VR 眼镜”，使得看到的内存并不是真实的内存。同时，进程也是复杂的：我们可以借助虚拟内存实现 demand paging、copy-on-write fork 等有趣的机制；而如何调度系统中的进程，在现代多处理器时代也显得愈加复杂。

---

## Lecture27 设备驱动程序与文件系统

<hr>

### [目录树管理](https://jyywiki.cn/OS/2023/slides/27.4.slides)

+ 遍历目录
    + c
    + Python库
+ 链接


