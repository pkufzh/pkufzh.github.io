---
title: 流体小白学习笔记（二）——可压缩流体基本方程组的无量纲化
excerpt: 对流体力学有所了解的小伙伴一定都听说过雷诺数、马赫数、普朗特数这些概念。那么，你知道这些“数”是如何被人们发现的吗？定义这些“数”的价值和意义何在？对方程组进行无量纲化又是什么意思？读完这篇笔记，相信你能够找到答案！
index_img: /img/posts/Cover_NS_Note_Nondimensionalization.jpg
date: 2022-08-11 18:00:00
updated:
tags:
- Fluid Mechanics
- Theory
categories:
- Shared Notes
- Articles
---

# 流体小白学习笔记（二）——可压缩流体基本方程组的无量纲化

**紧接上篇笔记，欢迎小伙伴们点赞、收藏、转发！O(∩_∩)O**

本文旨在介绍流体力学研究中的一把“利器”——**无量纲化**。

对流体力学有所了解的小伙伴一定都听说过雷诺数、马赫数、普朗特数这些所谓“无量纲数”的概念。那么，你知道这些数是如何被人们发现并定义的吗？这些数的价值和意义何在？读完本文，相信你能够找到答案！

## 一、量纲、无量纲化与量纲分析

**量纲（dimension）**是一个广泛的科学概念，在数学、物理、化学、计算机等各个学科具有重要意义。在数学上，量纲代表系统的自由度（degree of freedom），表示系统的维度大小，例如：线段的量纲为 1（dimension of one, 1D），欧几里得空间（Euclidean space）属于二维平面（2D），立方体、圆柱、球属于三维空间（3D）；在物理上，除空间量纲与时间量纲外，更广泛的量纲形成了一个抽象的参数空间，例如：七个基本物理量的量纲包括质量 $\mathcal{M}$，长度 $\mathcal{L}$，时间 $\mathcal{T}$，热力学温度 $\mathcal{\Theta}$，电流 $\mathcal{I}$，光强 $\mathcal{C}$ 和物质的量 $\mathcal{N}$。任何物理量的量纲均可采用基本物理量量纲通过组合得到，例如：密度 $\rho$ 的量纲为 $[\rho] = \mathcal{M} \mathcal{L}^{-3}$，对应国际标准单位（*SI*）为 $\text{kg} \cdot \text{m}^{-3}$；压强 $p$ 的量纲为 $[p] = \mathcal{M} \mathcal{L}^{-1} \mathcal{T}^{-2}$，对应 *SI* 为 $\text{kg} \cdot \text{m}^{-1} \cdot s^{-2}$。上述 $[\cdot]$ 代表取中括号内变量的量纲。

容易得到以下关于物理学量纲的两条基本定律成立：

- **量纲一致性定律：**每个在方程中相加的量的量纲必须一致。这也是验证方程是否成立的先决步骤。
- **量纲的幂次定律：**任何物理量的量纲公式都是基本量纲幂次单项式的形式，即满足物理量 $[X] = \mathcal{M}^{A} \mathcal{L}^{B} \mathcal{T}^{C} \mathcal{\Theta}^{D} \mathcal{I}^{E} \mathcal{C}^{F} \mathcal{N}^{G}$。

**无量纲化（nondimensionalization）**指通过适当的变量替换，从包含物理量的系统中部分或全部去除物理维度，使得变换后的系统中的部分或全部变量的量纲为 1。该过程可以简化具有复杂物理量的问题，并完成对关键物理信息的参数化。在一些物理系统中，**缩放（scaling）**与无量纲化意义相同，相对于系统原始变量，某些经过适当缩放的无量纲单位更容易进行测量与分析，而这些单位正是系统的固有属性，反映出系统的本质特征与内在规律。

无量纲化通常用以简化复杂的微分方程，当然这一过程也可以针对物理系统而不基于特定方程开展，这就是所谓**量纲分析（dimensional analysis）**[<sup>[1]</sup>](#refer-anchor-1)，这两者密切相关。量纲分析旨在分析与探求系统中多个物理量之间的关联，是研究物理问题的基本方法和有力武器，也促生了众多奠基性的物理学理论成果。限于篇幅，有关量纲分析及其相关故事，例如著名的白金汉 $\pi$ 定理（*Buckingham* $\pi$ theorem）[<sup>[2]</sup>](#refer-anchor-2)、泰勒（*G. I. Taylor*）仅凭照片估计原子弹当量等[<sup>[3]</sup>](#refer-anchor-3)，在此不再详述。有兴趣的小伙伴可以参阅相关资料与文献 ~

## 二、为什么要进行无量纲化？无量纲数是什么？

有的小伙伴可能会问：*我们生活中实际的物理系统都是有量纲的，因此能够直观感知质量、长度、时间等物理量的大小，也容易比较不同系统物理量之间的差异，而无量纲化似乎将系统变得抽象了，那么为什么还要对系统进行无量纲化呢？*

对于物理研究而言，对系统进行无量纲化能够带来以下好处：

- **无量纲化可以恢复并揭示系统的特征属性。**例如，对于一个简谐运动系统，若原始系统蕴含固有的谐振频率、时间常数等信息，则通过无量纲化可以恢复这些值，揭示系统的动力学特点。
- **无量纲化可以减少系统中所考虑变量的数量，**有利于直观比较各贡献项的相对大小，从而揭示系统的关键参数，方便进行简化。
- **无量纲后变量的量纲为 1，因此其数值与所选用的单位制无关**，采用纯数表示，便于进行对比。
- **最重要的是，无量纲化能够获得描述系统特征的无量纲数，利用无量纲数可以定义系统相似准则。**若确定两系统中控制某一过程的无量纲数相同，则可认为在此过程中两系统动力学规律相似。

例如，在流体力学研究中，对于基本方程组进行无量纲化，不仅可以简化方程形式，还能够获得众多无量纲数，而这些无量纲数通常具有深刻的物理意义，能够反映复杂流体系统的本质。因此，人们在流体力学各个范式的研究中，常常关注并采用无量纲方程形式，同时非常重视各个无量纲数的作用。**一个个无量纲数，看似简单，但常常具有“四两拨千斤”的威力！**

下面笔者以流体力学中的可压缩流体基本方程组为例，阐述对该方程组无量纲化的详细过程及其结果分析。

## 三、可压缩流体方程组无量纲化流程

### 有量纲的流体基本方程组

对于流体系统的无量纲化过程，其推导基础是有量纲形式的流体力学基本方程组。有关流体力学基本方程组的数学表达、物理含义及几种常见的变形形式，可以参考笔者本专栏的前一篇文章***《流体小白学习笔记（一）——流体力学基本方程组》***。首先给出有量纲的可压缩流体基本方程组，作为后续进行无量纲化的基础。

写成应力矢量形式的流体力学基本方程组为
$$
\begin{align}
\left\{\begin{array}{ll}
\frac{\partial \rho}{\partial t}+\nabla \cdot(\rho \mathbf{u})=0, & \text { 连续方程 } \\
\rho \frac{\mathrm{D} \mathbf{u}}{\mathrm{D} t}=\rho \boldsymbol{F}+\nabla \cdot \boldsymbol{P}, & \text { 运动方程 } \\
\rho \frac{\mathrm{D} e}{\mathrm{D} t}=\boldsymbol{P}: \boldsymbol{S}+ \nabla \cdot(\kappa \nabla T)+\rho \dot{q}, & \text { 能量方程 } \\
\boldsymbol{P}=-p \boldsymbol{I} + \boldsymbol{\Pi}=-p \boldsymbol{I}+2 \mu\left[\boldsymbol{S}-\frac{1}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right]+\mu^{\prime} (\nabla \cdot \mathbf{u}) \mathbf{I}, & \text { 本构方程 } \\
p=f(\rho, T), & \text { 状态方程 }
\end{array}\right. \label{eq001} \tag{1}
\end{align}
$$
上述方程组中各运算符号规则、变量含义及其英文表达以及热力学经验式（如 *Sutherland* 公式等）在专栏前文已有详细表述，在此不再重复给出。将本构方程代入运动方程与能量方程分别进行化简，考虑流动介质为完全气体，斯托克斯假设成立（即有 $\mu^{\prime} = 0$），且忽略流体体积力项 $F$ 与内部体积热源项 $\dot{q}$，即可得到微分形式的可压缩流体基本方程组
$$
\begin{align}
\left\{\begin{array}{ll}
\frac{\partial \rho}{\partial t}+\nabla \cdot(\rho \mathbf{u})=0, & \text { 连续方程 } \\
\rho \frac{\mathrm{D} \mathbf{u}}{\mathrm{D} t}=-\nabla p + \nabla \cdot (2 \mu \boldsymbol{S}) - \frac{2}{3} \nabla(\mu(\nabla \cdot \mathbf{u})), & \text { 运动方程 }  \\
\rho c_{p}\frac{\mathrm{D} T}{\mathrm{D} t} = \frac{\mathrm{D} p}{\mathrm{D} t} + \nabla \cdot(\kappa \nabla T) + \Phi & \text { 能量方程 } \\
\boldsymbol{P}=-p \boldsymbol{I} + \boldsymbol{\Pi}=-p \boldsymbol{I}+2 \mu\left[\boldsymbol{S}-\frac{1}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right], & \text { 本构方程 } \\
p = \rho R T, & \text { 状态方程 }
\end{array}\right. \label{eq002} \tag{2}
\end{align}
$$
注意到 $\nabla \cdot \boldsymbol{I} = \frac{\partial \delta_{i j}}{\partial x_{j}} = \frac{\partial}{\partial x_{i}} = \nabla$。容易证明，耗散函数 $\Phi$ 的表达式满足
$$
\begin{align}
\Phi = 2 \mu \boldsymbol{S} : \boldsymbol{S} - \frac{2}{3} \mu(\nabla \cdot \mathbf{u})^{2}
\end{align} = \frac{1}{2 \mu} \boldsymbol{\Pi} : \boldsymbol{\Pi}  \label{eq003} \tag{3}
$$
将变形速率张量 $\boldsymbol{S}$ 与偏应力张量 $\boldsymbol{\Pi}$ 采用速度矢量 $\mathbf{u}$ 或张量形式表示，即有
$$
\begin{align}
\boldsymbol{S} & = \frac{1}{2} \left[(\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T}\right] = \frac{1}{2} \left(\frac{\partial u_{i}}{\partial x_{j}} + \frac{\partial u_{j}}{\partial x_{i}}\right) \label{eq004} \tag{4} \\
\boldsymbol{\Pi} & = 2 \mu\left[\boldsymbol{S}-\frac{1}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right] = \mu \left[(\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right] = \mu \left(\frac{\partial u_{i}}{\partial x_{j}} + \frac{\partial u_{j}}{\partial x_{i}} - \frac{2}{3} \frac{\partial u_{k}}{\partial x_{k}} \delta_{i j}\right) \label{eq005} \tag{5} \\
\end{align}
$$
将张量 $\eqref{eq004}$ 与 $\eqref{eq005}$ 的原始矢量形式代入式 $\eqref{eq003}$ ，再代入方程组 $\eqref{eq002}$ 中，并展开物质导数与本构方程，可得**有量纲的可压缩流体基本方程组**
$$
\begin{align}
\left\{\begin{array}{ll}
\frac{\partial \rho^{\ast}}{\partial t^{\ast}}+\nabla^{\ast} \cdot(\rho^{\ast} \mathbf{u}^{\ast})=0, & \text { 连续方程 } \\
\rho^{\ast} \left[\frac{\partial \mathbf{u}^{\ast}}{\partial t^{\ast}} + (\mathbf{u}^{\ast} \cdot \nabla^{\ast}) \mathbf{u}^{\ast} \right] = - \nabla p^{\ast} + \nabla \cdot \left[\mu^{\ast} \left((\nabla^{\ast} \mathbf{u}^{\ast}) + (\nabla^{\ast} \mathbf{u}^{\ast})^{T} - \frac{2}{3} (\nabla^{\ast} \cdot \mathbf{u}^{\ast}) \boldsymbol{I}\right) \right], & \text { 运动方程 }  \\
\rho^{\ast} c_{p} \left[\frac{\partial T^{\ast}}{\partial t^{\ast}} + (\mathbf{u}^{\ast} \cdot \nabla^{\ast}) T^{\ast} \right] = \left[\frac{\partial p^{\ast}}{\partial t^{\ast}} + (\mathbf{u}^{\ast} \cdot \nabla^{\ast}) p^{\ast} \right] + \nabla^{\ast} \cdot(\kappa^{\ast} \nabla^{\ast} T^{\ast}) \\
\quad \quad \quad \quad \quad \quad \quad + \frac{\mu^{\ast}}{2}\left[(\nabla^{\ast} \mathbf{u}^{\ast}) + (\nabla^{\ast} \mathbf{u}^{\ast})^{T} - \frac{2}{3} (\nabla^{\ast} \cdot \mathbf{u}^{\ast}) \boldsymbol{I} \right] : \left[(\nabla^{\ast} \mathbf{u}^{\ast}) + (\nabla^{\ast} \mathbf{u}^{\ast})^{T} - \frac{2}{3} (\nabla^{\ast} \cdot \mathbf{u}^{\ast}) \boldsymbol{I} \right] & \text { 能量方程 } \\
\boldsymbol{P}^{\ast}=-p^{\ast} \boldsymbol{I} + \boldsymbol{\Pi}^{\ast}=-p^{\ast} \boldsymbol{I} + \mu^{\ast} \left[(\nabla^{\ast} \mathbf{u}^{\ast}) + (\nabla^{\ast} \mathbf{u}^{\ast})^{T} - \frac{2}{3} (\nabla^{\ast} \cdot \mathbf{u}^{\ast}) \boldsymbol{I} \right], & \text { 本构方程 } \\
p^{\ast} = \rho^{\ast} R T^{\ast}, & \text { 状态方程 }
\end{array}\right. \label{eq006} \tag{6}
\end{align}
$$

上述方程组中上标带 $\ast$ 号的物理量为有量纲变量。

### 方程组无量纲化流程

对一个物理系统（一般以微分方程组形式出现）进行无量纲化并提取特征无量纲数的一般流程如下：

- 引入参考特征量（有量纲），如特征长度 $L^{\ast}$、特征速度 $U^{\ast}$、特征时间 $t^{\ast}$、物理变量 $\rho^{\ast}, \; p^{\ast}, \; T^{\ast}, \; \mu^{\ast}, \; \kappa^{\ast}$ 的参考量等；
- 将原始方程组中的有量纲变量，根据参考特征量及其组合进行无量纲化（注意：无量纲方式通常不是唯一的），获得无量纲变量；
- 将无量纲变量代回原始方程组，整理并化简形式；
- 分析无量纲方程组中出现的参考特征量组合项，定义无量纲数，并分析其物理意义；
- 将各个无量纲数代回方程组中，重新整理方程形式，最终得到无量纲化的方程组。

下面对上述可压缩流体基本方程组 $\eqref{eq006}$ 进行无量纲化，无量纲后的各物理量上标不带 $\ast$ 号。

首先引入与流场相关的各参考特征量。引入特征长度 $L^{\ast}$、特征速度 $U_{\infty}^{\ast}$、特征时间 $t_{\infty}^{\ast} = L^{\ast} / U_{\infty}^{\ast}$、特征密度 $\rho_{\infty}^{\ast}$、特征温度 $T_{\infty}^{\ast}$、特征动力粘度 $\mu_{\infty}^{\ast}$、特征导热系数 $\kappa_{\infty}^{\ast}$，下标带 $\infty$ 的物理量为远场的流场变量。各无量纲变量形式如下
$$
x = \frac{x^{\ast}}{L^{\ast}}, \quad y = \frac{y^{\ast}}{L^{\ast}}, \quad z = \frac{z^{\ast}}{L^{\ast}}, \quad \nabla = L^{\ast} \nabla^{\ast}, \quad t = \frac{t^{\ast}}{t_{\infty}} = \frac{U_{\infty}^{\ast}}{L^{\ast}} t^{\ast}, \\
\rho = \frac{\rho^{\ast}}{\rho_{\infty}^{\ast}}, \quad p = \frac{p^{\ast}}{\rho_{\infty}^{\ast} U_{\infty}^{\ast 2}}, \quad \mathbf{u} = \frac{\mathbf{u}^{\ast}}{U_{\infty}^{\ast}}, \quad T = \frac{T^{\ast}}{T_{\infty}^{\ast}}, \quad \mu = \frac{\mu^{\ast}}{\mu_{\infty}^{\ast}}, \quad \kappa = \frac{\kappa^{\ast}}{\kappa_{\infty}^{\ast}}
\label{eq007} \tag{7}
$$
需要说明的是，对于原始变量参考特征量的构造，通常其组合形式与缩放系数不是唯一的，可能有多种方式。例如对于压强 $p$ 的变换也可采用 $p = p^{\ast} / (\rho_{\infty}^{\ast} U_{\infty}^{\ast 2} / 2)$，在此之所以不构造系数 $\frac{1}{2}$，是便于后续进行无量纲数的定义与分析。但是，无论采用何种无量纲变换形式，都必须满足组合特征量的量纲与原始变量对应。

将上述各无量纲变量形式代入有量纲的流体基本方程组，进一步整理与简化即可得到无量纲基本方程组，具体过程如下：

- **无量纲连续方程（nondimensional continuity equation）**

  将无量纲变量 $\eqref{eq007}$ 代入有量纲的连续方程
  $$
  \frac{\partial (\rho_{\infty}^{\ast} \rho)}{\partial \left(\frac{L^{\ast}}{U_{\infty}^{\ast}} t\right)} + \frac{1}{L^{\ast}} \nabla \cdot (\rho_{\infty}^{\ast} \rho U_{\infty}^{\ast} \mathbf{u}) = 0 \label{eq008} \tag{8}
  $$
  方程两边同乘 $L^{\ast} / \rho_{\infty}^{\ast} U_{\infty}^{\ast}$，化简可得
  $$
  \frac{\partial \rho}{\partial t} + \nabla \cdot(\rho \mathbf{u}) = 0 \label{eq009} \tag{9}
  $$
  可以观察到，连续方程的有量纲与无量纲形式相同，本质是体积微元内满足质量守恒，未引入特征无量纲数。

- **无量纲运动方程（nondimensional momentum equations）**

  将无量纲变量 $\eqref{eq007}$ 代入有量纲的运动方程
  $$
  \begin{align}
  \begin{split}
  \rho_{\infty}^{\ast} \rho & \left[\frac{\partial (U_{\infty}^{\ast} \mathbf{u})}{\partial (\frac{L^{\ast}}{U_{\infty}^{\ast}} t)} + \left(U_{\infty}^{\ast} \mathbf{u} \cdot \frac{1}{L^{\ast}} \nabla\right) (U_{\infty}^{\ast} \mathbf{u})\right] = \\
  & - \frac{1}{L^{\ast}} \nabla \left[(\rho_{\infty}^{\ast} U_{\infty}^{\ast}) p\right] \\
  & + \frac{1}{L^{\ast}} \nabla \cdot \left \{ \mu_{\infty}^{\ast} \mu \left[ \left(\frac{1}{L^{\ast}} \nabla\right) (U_{\infty}^{\ast} \mathbf{u}) + \left(\left(\frac{1}{L^{\ast}} \nabla\right) (U_{\infty}^{\ast} \mathbf{u})\right)^{T} - \frac{2}{3} \left(\frac{1}{L^{\ast}} \nabla\right) \cdot (U_{\infty}^{\ast} \mathbf{u}) \boldsymbol{I}\right] \right \}
  \end{split}
  \end{align}
  \label{eq010} \tag{10}
  $$
  方程两边同乘 $L^{\ast} / \rho_{\infty}^{\ast} U_{\infty}^{\ast 2}$，化简可得
  $$
  \rho\left[\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla) \mathbf{u} \right] = - \nabla p + \frac{\mu_{\infty}^{\ast}}{\rho_{\infty}^{\ast} U_{\infty}^{\ast} L^{\ast}}\nabla \cdot \left[\mu \left((\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I}\right) \right] \label{eq011} \tag{11}
  $$

  定义基于流场特征长度 $L^{\ast}$ 的无量纲的自由来流**雷诺数（Reynolds number）**
  $$
  \operatorname{Re}_{\infty} = \frac{\rho_{\infty}^{\ast} U_{\infty}^{\ast} L^{\ast}}{\mu_{\infty}^{\ast}} \label{eq012} \tag{12}
  $$
  将该无量纲数 $\eqref{eq012}$ 代入方程 $\eqref{eq011}$ 进一步整理无量纲运动方程为
  $$
  \rho\left[\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla) \mathbf{u} \right] = - \nabla p + \frac{1}{\operatorname{Re}_{\infty}}\nabla \cdot \left[\mu \left((\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I}\right) \right] \label{eq013} \tag{13}
  $$
  观察方程 $\eqref{eq013}$ 可知，考虑忽略体积力项的可压缩流动，无量纲运动方程仅包含一个无量纲数 $\operatorname{Re}_{\infty}$，**其物理意义为自由来流惯性力与粘性力之比**。容易知道，若当地（local）雷诺数较小时，流动的粘性效应占主要地位；反之，若当地雷诺数很大，例如趋于无穷时，流动的粘性效应可以忽略，此时惯性力占主导。

- **无量纲能量方程（nondimensional energy equation）**
  
  将无量纲变量 $\eqref{eq007}$ 代入有量纲的能量方程
  $$
  \begin{align}
  \begin{split}
  (\rho_{\infty}^{\ast} \rho) c_{p}^{\ast} & \left[\frac{\partial (T_{\infty}^{\ast} T)}{\partial \left(\frac{L^{\ast}}{U_{\infty}^{\ast}} t\right)} + \left(U_{\infty}^{\ast} \mathbf{u} \cdot \frac{1}{L^{\ast}} \nabla\right) (T_{\infty}^{\ast} T)\right] \\
  = & \left[\frac{\partial (\rho_{\infty}^{\ast} U_{\infty}^{\ast 2} \cdot p)}{\partial \left(\frac{L^{\ast}}{U_{\infty}^{\ast}} t\right)} + \left(U_{\infty}^{\ast} \mathbf{u} \cdot \frac{1}{L^{\ast}} \nabla\right) (\rho_{\infty}^{\ast} U_{\infty}^{\ast 2} \cdot p)\right] + \frac{1}{L^{\ast}} \nabla \cdot \left[\kappa_{\infty}^{\ast} \kappa \left(\frac{1}{L^{\ast}} \nabla (T_{\infty}^{\ast} T)\right)\right] \\
  + & \frac{1}{2} (\mu_{\infty}^{\ast} \mu) \left \{ \left(\frac{1}{L^{\ast}} \nabla\right) (U_{\infty}^{\ast} \mathbf{u}) + \left[\left(\frac{1}{L^{\ast}} \nabla\right) (U_{\infty}^{\ast} \mathbf{u}) \right]^{T} - \frac{2}{3} \left(\frac{1}{L^{\ast}} \nabla\right) \cdot (U_{\infty}^{\ast} \mathbf{u}) \boldsymbol{I} \right \} \\
  & \quad \quad \quad \; : \left \{ \left(\frac{1}{L^{\ast}} \nabla\right) (U_{\infty}^{\ast} \mathbf{u}) + \left[\left(\frac{1}{L^{\ast}} \nabla\right) (U_{\infty}^{\ast} \mathbf{u}) \right]^{T} - \frac{2}{3} \left(\frac{1}{L^{\ast}} \nabla\right) \cdot (U_{\infty}^{\ast} \mathbf{u}) \boldsymbol{I} \right \}
  \end{split}
  \end{align}
  \label{eq014} \tag{14}
  $$
  方程两边同乘 $L^{\ast} / c_{p}^{\ast} \rho_{\infty}^{\ast} U_{\infty}^{\ast} T_{\infty}^{\ast}$，化简可得
  $$
  \begin{align}
  \begin{split}
  \rho \left[\frac{\partial T}{\partial t} + (\mathbf{u} \cdot \nabla) T \right] & = \frac{U_{\infty}^{\ast}}{c_{p} T_{\infty}^{\ast}} \left[\frac{\partial p}{\partial t} + (\mathbf{u} \cdot \nabla) p \right] + \left(\frac{\mu_{\infty}^{\ast}}{\rho_{\infty}^{\ast} U_{\infty}^{\ast} L^{\ast}}\right) \cdot \left(\frac{\kappa_{\infty}^{\ast}}{c_{p}^{\ast} \mu_{\infty}^{\ast}}\right) \nabla\cdot(\kappa\nabla T) \\
  & + \frac{\mu}{2} \left(\frac{\mu_{\infty}^{\ast}}{\rho_{\infty}^{\ast} U_{\infty}^{\ast} L^{\ast}}\right) \cdot \left(\frac{U_{\infty}^{\ast 2}}{c_{p}^{\ast} T_{\infty}^{\ast}}\right) \left[(\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right] \\
  & \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \; \;: \left[(\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right]
  \end{split}
  \end{align}
  \label{eq015} \tag{15}
  $$
  
  
  定义以下两个新无量纲数：自由来流**马赫数（Mach number）**与**普朗特数（Prandtl number）**
  $$
  \begin{align}
  \operatorname{Ma}_{\infty} & = \frac{U_{\infty}^{\ast}}{a_{\infty}^{\ast}}, \label{eq016} \tag{16}\\
  \operatorname{Pr} & = \frac{\nu_{\infty}^{\ast}}{\alpha_{\infty}^{\ast}} = \frac{\frac{\mu_{\infty}^{\ast}}{\rho_{\infty}^{\ast}}}{\frac{\kappa_{\infty}^{\ast}}{c_{p}^{\ast} \rho_{\infty}^{\ast}}} = \frac{c_{p}^{\ast} \mu_{\infty}^{\ast}}{\kappa_{\infty}^{\ast}} \label{eq017} \tag{17}
  \end{align}
  $$
  
  其中，**马赫数是流体可压缩性的度量**，一般认为 $\operatorname{Ma} < 0.3$ 时流体不可压缩。流动速度可按照马赫数范围进行分类
  $$
  \begin{align}
  \begin{array}{l} 
  \left\{\begin{matrix} 
  \begin{split}
  \operatorname{Ma} < 0.8,  & \quad \text{Subsonic} \\
  0.8 < \operatorname{Ma} < 1.2, & \quad \text{Transonic} \\
  1.2 < \operatorname{Ma} < 5.0, & \quad \text{Supersonic} \\
  \operatorname{Ma} > 5.0, &  \quad \text{Hypersonic}
  \end{split}
  \end{matrix}\right.    
  \end{array} 
  \end{align}
  \label{eq018} \tag{18}
  $$
  **普朗特数的物理意义为动量扩散率与热扩散率的相对大小**，若 $\operatorname{Pr} \ll 1$，则在流体的能量传递过程中，热扩散占主导；若 $\operatorname{Pr} \gg 1$，则动量扩散占主导。气体的普朗特数一般接近 1（空气 $\operatorname{Pr} \approx 0.7$），说明在气体的能量传递过程中动量扩散与热扩散的量级接近。
  
  注意到，方程 $\eqref{eq015}$ 中的 $U_{\infty}^{\ast 2} / c_{p}^{\ast} T_{\infty}^{\ast}$ 项满足以下关系式
  $$
  \frac{U_{\infty}^{\ast 2}}{c_{p}^{\ast} T_{\infty}^{\ast}} = \frac{U_{\infty}^{\ast 2}}{\frac{1}{\gamma - 1} \gamma R T_{\infty}^{\ast}} = (\gamma - 1) \cdot \frac{U_{\infty}^{\ast 2}}{a_{\infty}^{\ast 2}} = (\gamma - 1) \operatorname{Ma}_{\infty}^{2} \label{eq019} \tag{19}
  $$
  
  观察方程 $\eqref{eq015}$ 中的各项系数的组合形式，将上述关系式 $\eqref{eq019}$ 以及三个无量纲数 $\eqref{eq012}, \eqref{eq016}, \eqref{eq017}$ 代入该方程可得
  $$
  \begin{align}
  \begin{split}
  \rho \left[\frac{\partial T}{\partial t} + (\mathbf{u} \cdot \nabla) T \right] & = (\gamma - 1) \operatorname{Ma}_{\infty}^{2}\left[\frac{\partial p}{\partial t} + (\mathbf{u} \cdot \nabla) p \right] + \frac{1}{\operatorname{Re} \operatorname{Pr}} \nabla\cdot(\kappa\nabla T) \\
  & + \frac{(\gamma - 1) \operatorname{Ma}_{\infty}^{2} \mu}{2 \operatorname{Re}_{\infty}} \left[(\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right] \\
  & \quad \quad \quad \quad \quad \quad \quad \;: \left[(\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right]
  \end{split}
  \end{align}
  \label{eq020} \tag{20}
  $$
  
  以上无量纲方程 $\eqref{eq020}$ 包含三个无量纲数 $\operatorname{Ma}_{\infty}, \; \operatorname{Re}_{\infty}, \; \operatorname{Pr}$。若保证这些无量纲数相同时，两个系统中能量传递的特征与规律一致。
  
- **无量纲状态方程（nondimensional equation of state）与内能、焓的无量纲表达式**

  将无量纲变量 $\eqref{eq007}$ 代入有量纲的状态方程
  $$
  \rho_{\infty}^{\ast} U_{\infty}^{\ast 2} \cdot p = (\rho_{\infty}^{\ast} \rho) R^{\ast} (T_{\infty}^{\ast} T) \label{eq021} \tag{21}
  $$
  方程两边同乘 $1 / (\rho_{\infty}^{\ast} U_{\infty}^{\ast 2})$ 可得
  $$
  p = \frac{R^{\ast} T_{\infty}^{\ast}}{U_{\infty}^{\ast 2}} \rho T = \frac{\rho T}{\frac{\gamma U_{\infty}^{\ast 2}}{\gamma R^{\ast} T_{\infty}^{\ast}}} = \frac{\rho T}{\gamma \frac{U_{\infty}^{\ast 2}}{a_{\infty}^{\ast 2}}} = \frac{\rho T}{\gamma \operatorname{Ma}_{\infty}^{2}} \label{eq022} \tag{22}
  $$
  上式 $\eqref{eq022}$ 即为无量纲的状态方程，可以观察到，无量纲后的气体常数为 $R = 1 / (\gamma \operatorname{Ma}_{\infty}^{2})$，则内能与焓的无量纲表达式分别如下
  $$
  \begin{align}
  e & = c_{v} T = \frac{1}{\gamma (\gamma - 1) \operatorname{Ma}_{\infty}^{2}} T \label{eq023} \tag{23}\\
  h & = c_{p} T = e + \frac{p}{\rho} = \frac{1}{(\gamma - 1) \operatorname{Ma}_{\infty}^{2}} T \label{eq024} \tag{24}
  \end{align}
  $$
  由此可见，相比有量纲表达式，无量纲的状态方程与热力学变量仅改变了常系数值，而形式不变。

- **无量纲萨瑟兰公式（nondimensional Sutherland's formula）**

  定义无量纲萨瑟兰温度 $C_{s} = S / T_{\infty}^{\ast}$，将无量纲变量 $\eqref{eq007}$ 代入有量纲公式（见专栏前文公式 (4)），可得无量纲公式
  $$
  \mu = T^{\frac{3}{2}} \left(\frac{1 + C_{s}}{T + C_{s}}\right) \label{eq025} \tag{25}
  $$

### 公式汇总与说明

综上推导，由方程 $\eqref{eq009}, \eqref{eq013}, \eqref{eq020}, \eqref{eq022}$，可汇总得**无量纲的可压缩流体基本方程组**如下
$$
\begin{align}
\left\{\begin{array}{ll}
\frac{\partial \rho}{\partial t} + \nabla \cdot(\rho \mathbf{u}) = 0, & \text { 无量纲连续方程 } \\
\rho\left[\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla) \mathbf{u} \right] = - \nabla p + \frac{1}{\operatorname{Re}_{\infty}}\nabla \cdot \left[\mu \left((\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I}\right) \right] , & \text { 无量纲运动方程 }  \\
\begin{split}
\rho \left[\frac{\partial T}{\partial t} + (\mathbf{u} \cdot \nabla) T \right] & = (\gamma - 1) \operatorname{Ma}_{\infty}^{2}\left[\frac{\partial p}{\partial t} + (\mathbf{u} \cdot \nabla) p \right] + \frac{1}{\operatorname{Re}_{\infty} \operatorname{Pr}} \nabla\cdot(\kappa\nabla T) \\
& + \frac{(\gamma - 1) \operatorname{Ma}_{\infty}^{2} \mu}{2 \operatorname{Re}} \left[(\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right] \\
& \quad \quad \quad \quad \quad \quad \quad \;: \left[(\nabla \mathbf{u}) + (\nabla \mathbf{u})^{T} - \frac{2}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right]
\end{split} & \text { 无量纲能量方程 } \\
p = \frac{\rho T}{\gamma \operatorname{Ma}_{\infty}^{2}}, \quad e = c_{v} T = \frac{1}{\gamma (\gamma - 1) \operatorname{Ma}_{\infty}^{2}} T, \quad h = c_{p} T = \frac{1}{(\gamma - 1) \operatorname{Ma}_{\infty}^{2}} T  & \text { 无量纲的状态方程、内能、焓 }
\end{array}\right. \label{eq026} \tag{26}
\end{align}
$$
以上所有流场变量均不带上标 $\ast$，表示均为已进行无量纲化后的变量形式，便于与原始有量纲上标带 $\ast$ 的变量区分。

值得注意的是，上述无量纲基本方程组中引入的三个无量纲数 $\operatorname{Ma}_{\infty}, \; \operatorname{Re}_{\infty}, \; \operatorname{Pr}$，在物理上能够清晰地反映有关流体惯性运动、粘性运动与能量传递的特征。**实际上，特征无量纲数是整个系统的关键。可以说，理解了无量纲数的物理图景，也就抓住了流体系统的本质。**对于流体基本方程组开展无量纲化的过程，本质是通过一种合理的尺度“缩放”，找到不同流体系统的共同特征与内在联系。

另外，流体的理论、实验与计算研究中也广泛采用无量纲方程形式。在许多经典的流体力学理论与解答中，对于不同流体方程的无量纲化通常是一种“规范流程”，更常作为理论分析的首个步骤，不可或缺。若两个具有相似边界条件的流体系统中无量纲数保持一致，则两系统具有动力学相似性，可认为流动规律相似，这也是风洞实验的基本原理与必需条件。同时，在通过 CFD 数值模拟各种流动时，也常求解无量纲化的流体力学基本方程组，这种做法既能够简化编程框架、降低数据前处理难度，也在一定程度上提升了计算的稳定性与鲁棒性。

## 结语

大家一定注意到，作为对方程组进行无量纲化获得的惊喜“硕果”，无量纲数大多数以人名命名。不管是以发现者命名，还是为纪念相关研究的伟大人物，所有无量纲数的背后，都凝结着人们的智慧与心血，都记录着振奋人心的传奇故事。事实上，在流体力学研究的璀璨星河中，许多未知的无量纲数仍在等待被学者们挖掘与探索，等待发挥它们的重要价值。

------

以上就是本文全部内容，如有疑问，敬请大家批评指正！

相应文章也将发布在我的 [知乎专栏](https://www.zhihu.com/column/c_1477306597446213634) 上。后续我会不定期更新本博客与专栏，欢迎大家关注！ 

------

## 参考文献

<div id="refer-anchor-1"></div>

- [1] Dimensional analysis https://en.wikipedia.ahmu.cf/wiki/Dimensional_analysis

<div id="refer-anchor-2"></div>

- [2] Buckingham π theorem [https://en.wikipedia.ahmu.cf/wiki/Buckingham_%CF%80_theorem](https://en.wikipedia.ahmu.cf/wiki/Buckingham_π_theorem)

<div id="refer-anchor-3"></div>

- [3] G. I. Taylor https://en.wikipedia.ahmu.cf/wiki/G._I._Taylorhttps://en.wikipedia.ahmu.cf/wiki/Buckingham

------


{% note info %}

<font size = 2.5>^_^ This is the END of the article. Thank you for reading! </font>

<font size = 2.5>If you think this article is helpful to you, do not hesitate to leave your comments!</font>

<font size = 2.5>Finished by <i><b>pkufzh (Small Shrimp)</b></i> on <i><b>2022/08/11</b></i> .</font>

{% endnote %}

<center><i> Who am I? A happy shrimp from Peking University! </i></center>
