---
theme: seriph
class: text-center
transition: slide-left
fonts:
  sans: 'Roboto'
  serif: 'Roboto Slab'
  mono: 'Fira Code'
---

# Quantum Computation

---

## 基础补充

---

<v-click>

### 狄拉克符号

</v-click>

<v-click depth="2">

### Bloch sphere, Bloch representation

+ |$\psi$> = $cos(\frac{\theta}{2})|0$> + $e^{i\phi}sin(\frac{\theta}{2})|1$>  

### 哥本哈根解释
  
</v-click>

---

## 量子力学引论

---

### 线性代数

定义在复空间上

+ 酉矩阵
  + $UU^{\dagger}=I$
+ 复空间上定义的向量
+ A为Hermite矩阵 : $A=A^{\dagger}$
+ 线性算子，正规算子，Hermite算子
  + 注意线性算符的一些性质，如果将线性算符理解为旋转（同一空间），那么夹角保持不变
  + 正规算子的谱分解
    + 一个正规算符 $A$（normal operator）是一个线性算符如果其满足$AA^{\dagger}=A^{\dagger}A$.
+ 张量积
  + 定义
  + 是量子计算有指数级加速的原因：$2^n$状态
  + 理解由张量积定义的多量子比特体系
    + 求变换矩阵的时候也要使用

---

### 量子力学假设

+ 假设1--状态空间公理
  + 状态空间---Hilbert空间（复内积向量空间.）
+ 假设2--演化公理
  + 演化：酉变换，一个仅依赖于t1和t2的酉算子U
  + 假设$2^{'}$ : 薛定谔方程
+ 假设3--测量公理
  + 量子测量
    + 测量算子 -- （类似于H？）
    + 投影测量
    + POVM测量
    + 相位

---

+ 假设4--复合系统公理
  + 复合系统：张量积
  + 量子纠缠
    + 考虑一个两个量子比特的系统，如果两个量子比特是被准备的，并且是孤立的，则它们分别构成两个封闭系统，则复合系统的状态可以写为张量积。
    + 但是如果允许两个粒子进行交互，则称为纠缠的，不能表示为张量积的形式 -- （形式上不可拆分，如$\ket{\psi}=\frac{1}{\sqrt2}\ket{0}+\frac{1}{\sqrt2}\ket{1}$
    + 也反应在$<LM>-<L><M>$不为零上

---

#### 密度算子

---

#### EPR与Bell不等式

---

## 第四章 量子线路

### 单量子比特运算

+ 单量子比特门（1-Qubit Gates）：作用在一个二维量子系统上的任意酉算符。
  + Pauli矩阵(X,Y,Z门)，H门，S门，T门
  + 联系Bloch表示
+ 单量子比特的z-y分解
+ 推论：任意酉门，有$U=e^{i\alpha}AXBXC$,$ABC=I$

---

### 受控运算

+ 控制U门
+ CNOT门
+ 注意求张量积

---

### 测量

---

### 通用量子门

+ 一组量子门被称为是通用的，即这组门的量子线路可以以任意精度近似任意（$\epsilon-close$）的酉运算
  + ex，Hadamard，相位，受控非门，$\frac{\pi}{8}$门

---

#### 两级酉门是通用的

#### 单量子比特门和受控非门是通用的

#### 近似任意酉门一般是难的

---

## 量子Fourier变换及其应用

+ 重要应用：相位估计，近似酉算子在某些场合的特征值

---

### 量子Fourier变换

+ 定义
  + 离散型和量子型
    + $\ket{j} \rightarrow \frac{1}{\sqrt{N}}\sum_{j=0}^{N-1}e^{\frac{2\pi ijk}{N}}\ket{k}$ 
  + 性质：是酉变换
  + 举例：三量子比特Fourier变换

---

### 相位估计

+ $U\ket{u} =e^{2\pi i \varphi}\ket{u}$
  + $\varphi 未知，估计\varphi$
+ 准备
  + 制备状态$\ket{u}$
  + 两个寄存器
    + 第一个寄存器包含$t$个初态为$\ket{0}$的量子比特
      + 如何选择$t$
    + 第二个寄存器$\ket{u}$，包含存储$\ket{u}$所需要的量子比特
+ 过程
  + 首先对$t$比特的$\ket{0}$应用H门,制备$\frac{1}{\sqrt2}\ket{0} + \frac{1}{\sqrt2}\ket{1}$
  + 然后依次对$t$比特和$\ket{u}$应用受控$U^{2^{j}}$门，一共$\Theta(t^2)步$
    + 关键步骤:$U(\frac{1}{\sqrt2}\ket{0} + \frac{1}{\sqrt2}\ket{1})\ket{u} = (\frac{1}{\sqrt2}\ket{0} + e^{2\pi i \varphi}\frac{1}{\sqrt2}\ket{1})\ket{u}$
  + 三个步骤
+ (1-$\epsilon$)近似

---

## 量子搜索算法

### 量子搜索算法

+ Grover算法：$O(\sqrt{N})$
  + 关注指标
  + $1 \le M \le N$
    + M:解数量 $f(x)=1$
    + N(假设$N=2^n$) $f(x)=0$
+ oracle
  + $\ket{x}\ket{q} \xrightarrow{O} \ket{x}\ket{q \oplus f(x)}
  + $\ket{q}$需要被初始化为$\ket{+} = \frac{1}{\sqrt2}\ket{0} - \frac{1}{\sqrt2}\ket{1}$

---

+ 过程
  + $H^{\oplus } + O(\sqrt(N))Grover$
  + Grover: $oracle + H^{\oplus n}$ + 相位变化 + $H^{\oplus n}$
  + 其中，相移酉算子$2\ket{0}\bra{0} - I$
  + Grover酉算子 $2\ket{\varphi}\bra{\varphi} - I$
+ 几何可视化
  + 设
    + $\ket{\alpha} \equiv \frac{1}{\sqrt{N-M}}\sum_{x}^{''}\ket{x}$
    + $\ket{\beta} \equiv \frac{1}{\sqrt{M}}\sum_{x}^{'}\ket{x}$
    + 由内积为0，$\ket{\alpha} \perp \ket{\beta}$
  + $\ket{\varphi} = cos\frac{\theta}{2}\ket{\alpha}+sin\frac{\theta}{2}\ket{\beta}$
  + $G\ket{\varphi} = cos\frac{3\theta}{2}\ket{\alpha}+sin\frac{3\theta}{2}\ket{\beta}$
