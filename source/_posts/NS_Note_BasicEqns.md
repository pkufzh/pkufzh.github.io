---
title: 流体小白学习笔记（一）——流体力学基本方程组
excerpt: 本文旨在给出流体力学基本方程组完整清晰的数学表达，包括流体力学领域最基本、最重要的控制方程——纳维-斯托克斯（Navier-Stokes, N-S）方程的具体形式，同时给出基本方程组的几种常见的变形与简化形式。
index_img: /img/posts/Cover_NS_Note_BasicEqns.jpg
date: 2022-07-07 20:00:00
updated:
tags:
- Fluid Mechanics
- Theory
categories:
- Shared Notes
- Articles
---

# 流体小白学习笔记（一）——流体力学基本方程组

## 前言

{% note success %}

前排提示：大量公式预警 ~ 本文干货多多，欢迎小伙伴们点赞、收藏、转发！O(∩_∩)O

{% endnote %}

流体力学是一门古老而优美的学科。艺术家们描绘的流转星空、奔腾江河，科学家们研究的跳跃液滴、飞舞浪花，工程师们设计的大型飞机、运载火箭……在日常生活与工业生产中，随处可见流体力学的身影。描述流动规律，捕捉流体特征，解决流动难题，成为流体力学工作者们的毕生追求。

**流体力学基本方程组，是整座流体力学大厦的基石。**理解并熟记基本方程组的数学表达与物理含义，是开展流体力学理论、实验和计算等各项研究的基础。

本文旨在给出流体力学基本方程组完整清晰的数学表达，包括流体力学领域最基本、最重要的控制方程——纳维-斯托克斯（Navier-Stokes, N-S）方程的具体形式，同时给出基本方程组的几种常见的变形与简化形式。相比其他类似科普文章，本文给出了更加详细的公式说明，适合相关专业人员阅读与收藏。

## 流体力学基本方程组的数学表达[<sup>[1]</sup>](#refer-anchor-1)

根据**质量守恒定律**、**动量定理**、**能量守恒定律**以及**黏性规律**，能够导出关于运动流体所需满足的三大基本方程：连续性方程（continuity equation）、运动方程（momentum equations）、能量方程（energy equation）。这些方程再加上本构方程（constitutive equations）、状态方程（equation of state, EOS）以及内能（internal energy）和熵（entropy）的表达式，便构成了流体力学的基本方程组。

下面直接给出微分形式的流体力学基本方程组。写成**应力矢量（stress vector）形式**的流体力学基本方程组为
$$
\begin{align}
\left\{\begin{array}{ll}
\frac{\partial \rho}{\partial t}+\nabla \cdot(\rho \mathbf{u})=0, & \text { 连续性方程 } \\
\rho \frac{\mathrm{D} \mathbf{u}}{\mathrm{D} t}=\rho \boldsymbol{F}+\nabla \cdot \boldsymbol{P}, & \text { 运动方程 } \\
\rho \frac{\mathrm{D} e}{\mathrm{D} t}=\boldsymbol{P}: \boldsymbol{S}+ \nabla \cdot(\kappa \nabla T)+\rho \dot{q}, & \text { 能量方程 } \\
\boldsymbol{P}=-p \boldsymbol{I} + \boldsymbol{\Pi}=-p \boldsymbol{I}+2 \mu\left(\boldsymbol{S}-\frac{1}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right)+\mu^{\prime} (\nabla \cdot \mathbf{u}) \mathbf{I}, & \text { 本构方程 } \\
p=f(\rho, T), & \text { 状态方程 }
\end{array}\right. \label{eq001} \tag{1}
\end{align}
$$
或写成应力张量（stress tensor）形式为
$$
\begin{align}
\left\{\begin{array}{ll}
\frac{\partial \rho}{\partial t} + \frac{\partial(\rho u_{i})}{\partial x_{i}} = 0,\\
\rho \frac{\mathrm{D} u_{i}}{\mathrm{D} \mathbf{t}} = \rho F_{i} + \frac{\partial p_{i j}}{\partial x_{j}},\\
\rho \frac{\mathrm{D} e}{\mathrm{D} \mathbf{t}} = p_{i j} s_{j i} + \frac{\partial}{\partial x_{i}}(\kappa \frac{\partial T}{\partial x_{i}}) + \rho \dot{q},\\
p_{i j} = - p \delta_{i j} + \pi_{i j} = - p \delta_{i j} + 2 \mu \left(s_{i j} - \frac{1}{3} s_{k k} \delta_{i j} \right) +\mu^{\prime}s_{k k} \delta_{i j},\\
p = f(\rho, T),\\
\end{array}\right. \label{eq002} \tag{2}
\end{align}
$$
其中，$i, j = 1, 2, 3$；速度矢量为 $\mathbf{u} = [u,v,w]^{T}$，$\boldsymbol{F}$ 为体积力项（volumetric force term），$\boldsymbol{P}$ 为应力张量（stress tensor），$\boldsymbol{\Pi}$ 为偏应力张量（deviatoric stress tensor），$\boldsymbol{S}$ 为变形速率张量（tensor of deformation rate, symmetric），$\boldsymbol{I}$ 为单位矩阵（identity matrix），$\dot{q}$ 为热源项，其代表由于辐射或其他原因在单位时间内传入单位质量流体的热量；$\rho$ 为密度，$p$ 为压强，$T$ 为热力学温度； $\mu$ 为剪切或动力黏性系数（shear / dynamic viscosity），也称为第一粘性系数（first coefficient of viscosity），$\mu^{\prime}$ 为体积或膨胀粘度（volume / bulk viscosity），$\kappa$ 为导热系数（thermal conductivity），这三个系数均与温度 $T$ 有关，且体积或膨胀粘度 $\mu^{\prime}$ 满足
$$
\begin{align}
\mu^{\prime} = \lambda + \frac{2}{3} \mu \label{eq003} \tag{3}
\end{align}
$$
其中，$\lambda$ 为第二黏性系数（second coefficient of viscosity）。若斯托克斯假设（Stoke's assumption）成立，则有 $\mu^{\prime} = 0$，而动力黏性系数 $\mu$ 可利用萨瑟兰公式（Sutherland's formula）进行估计，有以下关系式
$$
\begin{align}
\mu=\mu_{\text{ref}}\left(\frac{T}{T_{\text{ref}}}\right)^{\frac{3}{2}} \frac{T_{\text{ref}}+S}{T+S} \label{eq004} \tag{4}
\end{align}
$$
其中，$T_{\text{ref}}$ 为参考温度，$\mu_{\text{ref}}$ 为参考温度下的动力黏性系数，$S$ 为 Sutherland 温度。若考虑标准状态下的气体，则有 $T_{\text{ref}} = T_{0} = 273.15 \; \text{K}$，$\mu_{\text{ref}} = \mu_{0} = 1.716 \times 10^{- 5} \;\text{kg} \cdot \text{m}^{-1} \cdot \text{s}^{-1}$，$S = 110.4 \; \text{K}$。若考虑流动介质为完全气体（perfect gas），则状态方程与内能和焓的表达式可表示为
$$
\begin{align}
p & = \rho R T \label{eq005} \tag{5} \\
e & = c_{v} T \label{eq006} \tag{6} \\
h & = c_{p} T \label{eq007} \tag{7}
\end{align}
$$
其中，式 $\eqref{eq005}$ 为状态方程；式 $\eqref{eq006}$ 中 $e$ 为单位质量流体的内能，式 $\eqref{eq007}$ 中 $h$ 为单位质量流体的焓（enthalpy），并满足热力学关系式 $h = e +p / \rho$；$c_{v}$ 为定容比热（specific heat capacity at constant volume），$c_{p}$ 为定压比热（specific heat capacity at constant pressure），$R$ 为气体常数，一般取 $287 \; \text{J} \cdot \text{kg}^{-1} \cdot \text{K}^{-1}$。当流体温度不太高时，可近似认为 $c_{v}, c_{p}$ 为常数，满足
$$
\begin{align}
c_{v} = \frac{1}{\gamma - 1} R \label{eq008} \tag{8} \\
c_{p} = \frac{\gamma}{\gamma - 1} R \label{eq009} \tag{9}
\end{align}
$$
其中，$\gamma = c_{v} / c_{p}$ 称为比热比（specific heat capacity ratio）或绝热指数，对于空气 $\gamma \approx 1.4$。。另外，引入运动黏性系数（kinematic viscosity）$\nu$，热扩散系数（thermal diffusivity）$\alpha$，两者均可采用前述变量表示为如下形式
$$
\begin{align}
\nu & = \frac{\mu}{\rho} \label{eq010} \tag{10}\\
\alpha & = \frac{\kappa}{c_{p} \rho} \label{eq011} \tag{11}
\end{align}
$$
综上所述，列出的基本方程组 $\eqref{eq001}$ 由 12 个方程组成（包括 1 个连续性方程、3 个运动方程、1 个能量方程、6 个本构方程、1 个状态方程），可以用来确定 $\mathbf{u}, p, \rho, T, p_{xx}, p_{yy}, p_{zz}, p_{xy}, p_{yz}, p_{zx}$ 这 12 个未知数，且增加的热力学变量内能或焓都有额外的温度关联式成立。由此可见，该微分形式的流体力学基本方程组是封闭的，理论上可以直接求解。

现考虑基本方程组 $\eqref{eq001}$ 的另一种形式，若将本构方程代入运动方程与能量方程，则可消去应力张量 $\boldsymbol{P}$ 。首先考虑 $\eqref{eq001}$ 运动方程中的最后一项（应力散度项），有
$$
\begin{align}
\nabla \cdot \boldsymbol{P} &=\frac{\partial p_{i j}}{\partial x_{j}}=\frac{\partial}{\partial x_{j}}\left[-p \delta_{i j}+2 \mu\left(s_{i j}-\frac{1}{3} s_{k k} \delta_{i j}\right)+\mu^{\prime} s_{k k} \delta_{i j}\right] \\
&=-\frac{\partial p}{\partial x_{i}}+\frac{\partial}{\partial x_{j}}\left[2 \mu\left(s_{i j}-\frac{1}{3} s_{k k} \delta_{i j}\right)\right]+\frac{\partial}{\partial x_{j}}\left(\mu^{\prime} s_{k k} \delta_{i j}\right) \quad \quad \text{（张量形式）}\\
&=-\nabla p+2 \nabla \cdot(\mu \boldsymbol{S})-\frac{2}{3} \nabla(\mu(\nabla \cdot \mathbf{u}))+\nabla\left(\mu^{\prime}(\nabla \cdot \mathbf{u})\right) \quad \quad \; \; \;\text{（矢量形式）} \\ 
\end{align} \label{eq012} \tag{12}
$$
其中，$\nabla \cdot \boldsymbol{P}$ 表示为单位体积上应力张量的散度，物理含义是与面力等效的体力分布函数。将式 $\eqref{eq012}$ 代入式 $\eqref{eq001}$ 中的运动方程可得
$$
\begin{align}
\rho \frac{\mathrm{D} \mathbf{u}}{\mathrm{D} t}=\rho \boldsymbol{F}-\nabla p+2 \nabla \cdot(\mu \boldsymbol{S})-\frac{2}{3} \nabla(\mu(\nabla \cdot \mathbf{u}))+\nabla\left(\mu^{\prime}(\nabla \cdot \mathbf{u})\right) \label{eq013} \tag{13}
\end{align}
$$
由上文可知，第一与第二动力黏性系数 $\mu$ 与 $\mu^{\prime}$ 一般依赖于温度 $T$，但若考虑温差很小的流场，则可近似认为两个黏性系数为常数，此时上式可进一步化为
$$
\begin{align}
\rho \frac{\mathrm{D} \mathbf{u}}{\mathrm{D} t}=\rho \boldsymbol{F}-\nabla p + \mu \Delta \mathbf{u} + \left(\mu^{\prime} + \frac{1}{3} \mu\right) \nabla (\nabla \cdot \mathbf{u}) \label{eq014} \tag{14}
\end{align}
$$

其次，考虑 $\eqref{eq001}$ 中能量方程右式第一项（应力功率项），有

$$
\begin{align}
\boldsymbol{P} : \boldsymbol{S} & = p_{i j} s_{j i} = \left[- p \delta_{i j} + 2 \mu \left(s_{i j} - \frac{1}{3} s_{k k} \delta_{i j} \right) +\mu^{\prime}s_{k k} \delta_{i j}\right] s_{j i} \\
& = - p s_{k k} + 2 \mu \left(s_{i j} s_{j i} - \frac{1}{3} s_{k k}^{2}\right) + \mu^{\prime} s_{k k}^{2}  \quad \quad \quad \quad \quad \quad \quad \quad \quad \text{（张量形式）}\\
& = - p (\nabla \cdot \mathbf{u}) + 2 \mu \left(\boldsymbol{S} : \boldsymbol{S} - \frac{1}{3} (\nabla \cdot \mathbf{u})^{2}\right) + \mu^{\prime} (\nabla \cdot \mathbf{u})^{2} \\
& = - p (\nabla \cdot \mathbf{u}) + 2 \mu \boldsymbol{S} : \boldsymbol{S} + \left(\mu^{\prime} - \frac{2}{3} \mu\right) (\nabla \cdot \mathbf{u})^{2} \quad \quad \quad \quad \quad \quad \text{（矢量形式）} 
\end{align} \label{eq015} \tag{15}
$$
其中，$\boldsymbol{P} : \boldsymbol{S}$ 代表应力张量与变形速度张量的并矢，物理含义是由于流体变形后，应力（面力）所做的功的功率，其由三部分组成：第一部分是 $- p (\nabla \cdot \mathbf{u})$ ，代表当流体体积有相对膨胀或压缩时压强 $p$ 所做的功的功率；第二部分是 $2 \mu \boldsymbol{S} : \boldsymbol{S} - 2 \mu (\nabla \cdot \mathbf{u})^{2}/3$，代表由剪切黏性在单位时间内所耗散的机械能；第三部分是 $\mu^{\prime} (\nabla \cdot \mathbf{u})^{2}$，代表流体在膨胀时黏性在单位时间内所耗散的机械能。由黏性所耗散的机械能全部转化为热能，这是一个不可逆过程。令
$$
\begin{align}
\Phi = 2 \mu \boldsymbol{S} : \boldsymbol{S} + \left(\mu^{\prime} - \frac{2}{3} \mu\right) (\nabla \cdot \mathbf{u})^{2} \label{eq016} \tag{16}
\end{align}
$$
上式中的 $\Phi$ 称为耗散函数（dissipation function），其表征由于流体黏性而耗散的机械能。将式 $\eqref{eq016}$ 代入式 $\eqref{eq015}$ 可得
$$
\begin{align}
\boldsymbol{P} : \boldsymbol{S} = - p (\nabla \cdot \mathbf{u}) + \Phi \label{eq017} \tag{17}
\end{align}
$$
再将上式 $\eqref{eq017}$ 代入 $\eqref{eq001}$ 中的能量方程可得
$$
\begin{align}
\rho \frac{\mathrm{D} e}{\mathrm{D} t} + p (\nabla \cdot \mathbf{u})= \Phi+ \nabla \cdot(\kappa \nabla T)+\rho \dot{q} \label{eq018} \tag{18}
\end{align}
$$
 利用 $\eqref{eq001}$ 中的连续性方程可得
$$
\begin{align}
p (\nabla \cdot \mathbf{u}) = - \frac{p}{\rho} \frac{\mathrm{D} \rho}{\mathrm{D} t} = \rho p \frac{\mathrm{D}}{\mathrm{D} t} \left(\frac{1}{\rho}\right) \label{eq019} \tag{19}
\end{align}
$$
于是有
$$
\begin{align}
\rho \left[\frac{\mathrm{D} e}{\mathrm{D} t} + p \frac{\mathrm{D}}{\mathrm{D} t} \left(\frac{1}{\rho}\right)\right] = \Phi+ \nabla \cdot(\kappa \nabla T)+\rho \dot{q} \label{eq020} \tag{20}
\end{align}
$$
根据热力学第二定律（second law of thermodynamics）可得
$$
\begin{align}
T \mathrm{d}s = \mathrm{d} e + p \mathrm{d} \tau = \mathrm{d} e + p \mathrm{d} \left(\frac{1}{\rho}\right) = \mathrm{d} h - \frac{1}{\rho} \mathrm{d} p \label{eq021} \tag{21}
\end{align}
$$
其中，$s$ 为热力学定义的熵，$\tau = 1 / \rho$ 为单位质量流体的体积。则式 $\eqref{eq020}$ 可改写为
$$
\begin{align}
\rho \frac{\mathrm{D} h}{\mathrm{D} t} = \frac{\mathrm{D} p}{\mathrm{D} t} + \Phi + \nabla \cdot(\kappa \nabla T)+\rho \dot{q} \label{eq022} \tag{22}
\end{align}
$$
或
$$
\begin{align}
\rho T \frac{\mathrm{D} s}{\mathrm{D} t} = \Phi + \nabla \cdot(\kappa \nabla T)+\rho \dot{q} \label{eq023} \tag{23}
\end{align}
$$
因此，根据式 $\eqref{eq013}, \eqref{eq022}$ ，可进一步化简微分形式的流体力学基本方程组，最终得到
$$
\begin{align}
\left\{\begin{array}{ll}
\frac{\partial \rho}{\partial t}+\nabla \cdot(\rho \mathbf{u})=0, & \text { 连续性方程 } \\
\rho \frac{\mathrm{D} \mathbf{u}}{\mathrm{D} t}=\rho \boldsymbol{F}-\nabla p+2 \nabla \cdot(\mu \boldsymbol{S})-\frac{2}{3} \nabla(\mu(\nabla \cdot \mathbf{u}))+\nabla\left(\mu^{\prime}(\nabla \cdot \mathbf{u})\right) \\
\; \; \; \overset{\mu, \;\mu^{\prime} = \text{const.}}{=}\rho \boldsymbol{F}-\nabla p + \mu \Delta \mathbf{u} + \left(\mu^{\prime} + \frac{1}{3} \mu\right) \nabla (\nabla \cdot \mathbf{u}), & \text { 运动方程（Navier-Stokes 方程） } \\
\rho \frac{\mathrm{D} h}{\mathrm{D} t} = \frac{\mathrm{D} p}{\mathrm{D} t} + \Phi + \nabla \cdot(\kappa \nabla T)+\rho \dot{q} \\
or \quad \rho T \frac{\mathrm{D} s}{\mathrm{D} t} = \Phi + \nabla \cdot(\kappa \nabla T)+\rho \dot{q}, & \text { 能量方程 } \\
\boldsymbol{P}=-p \boldsymbol{I} + \boldsymbol{\Pi}=-p \boldsymbol{I}+2 \mu\left(\boldsymbol{S}-\frac{1}{3} (\nabla \cdot \mathbf{u}) \boldsymbol{I} \right)+\mu^{\prime} (\nabla \cdot \mathbf{u}) \mathbf{I}, & \text { 本构方程 } \\
p=f(\rho, T), & \text { 状态方程 }
\end{array}\right. \label{eq024} \tag{24}
\end{align}
$$
其中，耗散函数 $\Phi$ 由式 $\eqref{eq016}$ 确定。求解该封闭方程组时，可分步求解：首先不考虑本构方程，求解 $\mathbf{u}, p, \rho, T$；再将各流动变量代入本构方程中，即可得到应力张量的各个分量。方程组 $\eqref{eq024}$ 中的运动方程即称为**纳维-斯托克斯（Navier-Stokes, N-S）方程，这是流体力学领域最基本、最重要的控制方程，其本质是牛顿第二定律的一种变形**。

## 几种常见的变形与简化形式

下面给出微分形式的流体力学基本方程组的几种变形与简化形式。

**黏性不可压缩流体情形**

考虑流体处于不可压缩状态（一般认为流动马赫数 $Ma < 0.3$），则有 $\mathrm{D} \rho / \mathrm{D}t = 0$；由于流速较低时温差较小，一般可认为 $\mu$ 为常数，此时基本方程组变为
$$
\begin{align}
\left\{\begin{array}{ll}
\nabla \cdot \mathbf{u} = 0 \\
\rho \frac{\mathrm{D} \mathbf{u}}{\mathrm{D} t} = \rho \boldsymbol{F}-\nabla p + \mu \Delta \mathbf{u} \\
\rho \frac{\mathrm{D} h}{\mathrm{D} t} = \frac{\mathrm{D} p}{\mathrm{D} t} + \Phi + \nabla \cdot(\kappa \nabla T)+\rho \dot{q} \\
\boldsymbol{P}=-p \boldsymbol{I}+2 \mu \boldsymbol{S} \\
p = \rho R T
\end{array}\right. \label{eq025} \tag{25}
\end{align}
$$
其中，运动方程、能量方程与本构方程已经采用连续性方程得到的无散条件（$\nabla \cdot \mathbf{u} = 0$）进行化简。这里注意区分以下定义：

- **不可压缩流体**指的是流体微团的密度在随体运动中保持不变，即其随体导数为零，流体微团体积不变，而当地密度与流场密度梯度有可能发生变化；
- 定常（$\partial / \partial t = 0$）、不可压缩（$\mathrm{D} \rho / \mathrm{D}t = 0$）流体满足 $\mathbf{u} \cdot \nabla \rho = u_{i} \cdot \partial \rho/ \partial x_{i} = 0$；
- 均匀（$\partial \rho/ \partial x_{i} = 0$）、不可压缩（$\mathrm{D} \rho / \mathrm{D}t = 0$）的流体密度为常数，即有 $\rho = \text{const.}$。

**理想不可压缩流体情形（不可压缩型欧拉方程，imcompressible Euler equation）**

考虑流体为理想或无黏（$\mu = 0$）且不可压缩的，则可进一步化简式 $\eqref{eq025}$ 得到
$$
\begin{align}
\left\{\begin{array}{ll}
\nabla \cdot \mathbf{u} = 0 \\
\rho \frac{\mathrm{D} \mathbf{u}}{\mathrm{D} t} = \rho \boldsymbol{F}-\nabla p \\
\end{array}\right. \label{eq026} \tag{26}
\end{align}
$$
**理想可压缩流体情形（可压缩型欧拉方程，compressible Euler equation）**

考虑流体为理想绝热，即等熵（isentropic）的完全气体，此时基本方程组变为
$$
\begin{align}
\left\{\begin{array}{ll}
\frac{\partial \rho}{\partial t}+\nabla \cdot(\rho \mathbf{u})=0 \\
\rho \frac{\mathrm{D} \mathbf{u}}{\mathrm{D} t} = \rho \boldsymbol{F}-\nabla p \\
\frac{\mathrm{D} s}{\mathrm{D} t} = 0 \quad or \quad \frac{\mathrm{D}}{\mathrm{D} t} \left(\frac{p}{\rho^{\gamma}}\right) = 0 \\
p = \rho R T
\end{array}\right. \label{eq027} \tag{27}
\end{align}
$$
**特别适用于计算流体力学（Computational Fluid Dynamics, CFD）的守恒型（conservation）控制方程形式**[<sup>[2]</sup>](#refer-anchor-2)

*以下内容部分参考 John D. Anderson, JR. 《计算流体力学入门》2.10节。*守恒型的控制方程，包括连续性方程、动量方程、能量方程均可以表示成统一的形式，有助于简化和组织给定计算程序的逻辑结构。注意，守恒型控制方程的左端都有一个散度项（divergence），其涉及某些物理量的通量（flux），例如：

- 质量通量（mass flux）： $\rho \mathbf{u}$；
- $x, y, z$ 方向上的动量通量（momentum flux in $x, y, z$ - direction）：$\rho u \mathbf{u}, \rho v \mathbf{u}, \rho w \mathbf{u}$；
- 总能（内能 + 动能）通量（total energy flux）：$\rho \left(e + V^{2} / 2\right) \mathbf{u}$，其中 $V = \left | \mathbf{u} \right |$ 为速度矢量大小；

则可将基本方程组中的守恒型控制方程表示为统一的形式，在正交直角坐标系（三维）下，可由以下式子给出
$$
\begin{align}
\frac{\partial \mathbf{U}}{\partial t} + \frac{\partial \mathbf{F}_{1}}{\partial x} + \frac{\partial \mathbf{F}_{2}}{\partial y} + \frac{\partial \mathbf{F}_{3}}{\partial z} = \mathbf{J} + \frac{\partial \mathbf{F}_{V1}}{\partial x} + \frac{\partial \mathbf{F}_{V2}}{\partial y} + \frac{\partial \mathbf{F}_{V3}}{\partial z} \label{eq028} \tag{28}
\end{align}
$$
其中，$\mathbf{F}_{1}, \mathbf{F}_{2}, \mathbf{F}_{3}$ 代表无黏通量项（inviscid flux）； $\mathbf{F}_{V1}, \mathbf{F}_{V2}, \mathbf{F}_{V3}$ 代表黏性通量项（viscid flux）；$\mathbf{J}$ 代表源项（若体积力和热源被忽略，则该项为零）；$\mathbf{U}$ 为解向量，采用列向量表示的各项表达式如下：
$$
\begin{align}
\mathbf{U} & =
\begin{bmatrix}
\rho \\
\rho u \\
\rho v \\
\rho w \\
\rho \left(e + \frac{V^{2}}{2}\right)
\end{bmatrix}^{\mathrm{T}} \label{eq029} \tag{29}\\
\mathbf{F}_{1} & =
\begin{bmatrix}
\rho u \\
\rho u^{2} + p \\
\rho v u \\
\rho w u \\
\left[\rho \left(e + \frac{V^{2}}{2}\right) + p\right] u
\end{bmatrix}^{\mathrm{T}} \label{eq030} \tag{30} \\
\mathbf{F}_{2} & =
\begin{bmatrix}
\rho v \\
\rho u v \\
\rho v^{2} + p \\
\rho w v \\
\left[\rho \left(e + \frac{V^{2}}{2}\right) + p\right] v
\end{bmatrix}^{\mathrm{T}} \label{eq031} \tag{31} \\
\mathbf{F}_{3} & =
\begin{bmatrix}
\rho w \\
\rho u w \\
\rho v w \\
\rho w^{2} + p \\
\left[\rho \left(e + \frac{V^{2}}{2}\right) + p\right]w
\end{bmatrix}^{\mathrm{T}} \label{eq032} \tag{32}\\
\mathbf{F}_{V1} & =
\begin{bmatrix}
0 \\
\pi_{1 1} \\
\pi_{1 2} \\
\pi_{1 3} \\
u \pi_{1 1} + v \pi_{1 2} + w \pi_{1 3} + \kappa \frac{\partial T}{\partial x}
\end{bmatrix}^{\mathrm{T}} \label{eq033} \tag{33} \\
\mathbf{F}_{V2} & =
\begin{bmatrix}
0 \\
\pi_{2 1} \\
\pi_{2 2} \\
\pi_{2 3} \\
u \pi_{2 1} + v \pi_{2 2} + w \pi_{2 3} + \kappa \frac{\partial T}{\partial y}\\
\end{bmatrix}^{\mathrm{T}} \label{eq034} \tag{34} \\
\mathbf{F}_{V3} & =
\begin{bmatrix}
0 \\
\pi_{3 1} \\
\pi_{3 2} \\
\pi_{3 3} \\
u \pi_{3 1} + v \pi_{3 2} + w \pi_{3 3} + \kappa \frac{\partial T}{\partial z}
\end{bmatrix}^{\mathrm{T}} \label{eq035} \tag{35} \\
\mathbf{J} & =
\begin{bmatrix}
0 \\
\rho f_{x} \\
\rho f_{y} \\
\rho f_{z} \\
\rho (u f_{x} + v f_{y} + w f_{z}) + \rho \dot{q}
\end{bmatrix}^{\mathrm{T}} \label{eq036} \tag{36} \\
\end{align}
$$
其中，单位质量流体的内能 $e$ 可根据式 $\eqref{eq006}$ 计算，系统状态方程为 $\eqref{eq005}$；偏应力项 $\pi_{i j} = 2 \mu \left(s_{i j} - \frac{1}{3} s_{k k} \delta_{i j} \right) +\mu^{\prime}s_{k k} \delta_{i j}$，若考虑斯托克斯假设成立，则有 $\mu^{\prime} = 0$，故偏应力张量各分量在正交直角坐标系下的表达式为
$$
\begin{align}
\pi_{1 1} & = 2 \mu \frac{\partial u}{\partial x} - \frac{2}{3} \mu \left(\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial w}{\partial z}\right) \label{eq037} \tag{37} \\
\pi_{2 2} & = 2 \mu \frac{\partial v}{\partial y} - \frac{2}{3} \mu \left(\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial w}{\partial z}\right) \label{eq038} \tag{38} \\
\pi_{3 3} & = 2 \mu \frac{\partial w}{\partial z} - \frac{2}{3} \mu \left(\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial w}{\partial z}\right) \label{eq039} \tag{39} \\
\pi_{1 2} = \pi_{2 1} & = \mu \left(\frac{\partial v}{\partial x} + \frac{\partial u}{\partial y}\right) \label{eq040} \tag{40} \\
\pi_{2 3} = \pi_{3 2} & = \mu \left(\frac{\partial w}{\partial y} + \frac{\partial v}{\partial z}\right) \label{eq041} \tag{41} \\
\pi_{3 1} = \pi_{1 3} & = \mu \left(\frac{\partial u}{\partial z} + \frac{\partial w}{\partial x}\right) \label{eq042} \tag{42} \\
\end{align}
$$
将式 $\eqref{eq029} \sim \eqref{eq036}$ 各通量项的每一项代入式 $\eqref{eq028}$ 并相加，便可以重构整个流体力学基本方程组。注意，该非定常流动方程组考虑了流体的黏性与可压缩性。

在进行数值模拟时，若将整个流场进行网格离散，并给定边界条件与初始条件，则可以首先求得上述无黏通量与黏性通量中的各个分量，再通过时间推进方式数值求解得到每一个网格点的解向量 $\mathbf{U} = [U_{1}, U_{2}, U_{3}, U_{4}, U_{5}]^{\mathrm{T}}$，并最终能够很容易地得到该时刻该网格点上的原始变量 $[\rho, u, v, w, e]^{\mathrm{T}}$，即有
$$
\begin{align}
\rho & = U_{1} \label{eq043} \tag{43} \\
u & = \frac{U_{2}}{U_{1}} \label{eq044} \tag{44} \\
v & = \frac{U_{3}}{U_{1}} \label{eq045} \tag{46} \\
w & = \frac{U_{4}}{U_{1}} \label{eq047} \tag{47} \\
e & = \frac{U_{5}}{U_{1}} - \frac{u^{2} + v^{2} + w^{2}}{2} \label{eq048} \tag{48}
\end{align}
$$
迭代以上过程，直到各个网格处的流场变量收敛至预期值，最终能够获得整个流场变量信息。

值得注意的是，以上基本方程组均是有量钢的，而实际在通过 CFD 数值模拟各种流动时，常采用求解无**量纲化的流体力学基本方程组**，以提升计算的稳定性与鲁棒性。

***有关可压缩 Navier-Stokes 方程组无量纲化过程详见本专栏中的后续文章，敬请期待！***

------

以上就是本文全部内容，如有疑问，敬请大家批评指正！

相应文章也将发布在我的 [知乎专栏](https://www.zhihu.com/column/c_1477306597446213634) 上。后续我会不定期更新本博客与专栏，欢迎大家关注！ 

------

## 参考文献

<div id="refer-anchor-1"></div>

- [1] 吴望一. 流体力学 上册[M]. 北京大学出版社, 1982.

<div id="refer-anchor-2"></div>

- [2] John D. Anderson, JR. 计算流体力学入门[M]. 清华大学出版社, 2010.

------


{% note info %}

<font size = 2.5>^_^ This is the END of the article. Thank you for reading! </font>

<font size = 2.5>If you think this article is helpful to you, do not hesitate to leave your comments!</font>

<font size = 2.5>Finished by <i><b>pkufzh (Small Shrimp)</b></i> on <i><b>2022/07/07</b></i> .</font>

{% endnote %}

<center><i> Who am I? A happy shrimp from Peking University! </i></center>
