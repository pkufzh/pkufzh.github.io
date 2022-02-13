---
title: 有趣的流体小知识（二）——点涡系的稳定性与卡门涡街
excerpt: In fluid dynamics, a Kármán vortex street (or a von Kármán vortex street) is a repeating pattern of swirling vortices, caused by a process known as vortex shedding, which is responsible for the unsteady separation of flow of a fluid around blunt bodies.
date: 2022-02-13 16:04:11
updated:
tags:
- Fluid Mechanics
- Theory
categories:
- Shared Notes
- Bilibili Videos & Articles
---

# 卡门涡街 (von Kármán Vortex Street) 

**题目要求**

***卡门涡街 (von Kármán Vortex Street) 问题***

考虑一个按图 [1](#fig1) 所示排列的点涡系，其由两排强度相同、符号相反，水平间距相同 (均为 $a$)，错位排列的点涡列组成。两排点涡位于 $y = \pm \frac{b}{2}$ 直线上。<span id = "fig1"></span>

<img src="C:\Users\56333\Desktop\Dot_Vortice\1.png" label = "001" style="zoom:67%;" />

<div align = center>
	<font size = 2.5>
	图 1  题设点涡系示意图
	</font>
</div>

试解答以下问题：

a)  求 $z = \frac{a}{2} - \mathrm{i} \frac{b}{2}$ 处的点涡 $\alpha$ 速度；

b)  绘制流线。

**解答**

a)  首先写出点涡系的总复位势为

$$
\begin{aligned}
W(z)=\frac{\Gamma}{2 \pi \mathrm{i}} \ln \frac{\sin \left[\frac{\pi}{\alpha}\left(z-\frac{b}{2} \mathrm{i}\right)\right]}{\sin \left[\frac{\pi}{\alpha}\left(z+\frac{b}{2} \mathrm{i} -\frac{a}{2}\right)\right]}
\end{aligned}
\tag{1}
\label{eq1}
$$
则位于 $\mathbf{z} = \frac{a}{2} - \mathrm{i} \frac{b}{2}$ 处的点涡 $\alpha$ 被其他点涡诱导的复位势为
$$
\begin{aligned}
W_{\alpha}(z) = W(z) + \frac{\Gamma}{2 \pi \mathrm{i}} \ln \left(z+\frac{b}{2} \mathrm{i}-\frac{a}{2}\right)
\end{aligned}
\tag{2}
\label{eq2}
$$
结合以上两式，可得在点涡 $\alpha$ 处的诱导共轭复速度为
$$
\begin{aligned}
V_{\alpha}^{*}=U_{\alpha}-\mathrm{i} V_{\alpha}=\left.\frac{\mathrm{d}}{\mathrm{d} z}\left[W(z)+\frac{\Gamma}{2 z \mathrm{i}} \ln \left(z+\frac{b}{2} \mathrm{i}-\frac{a}{2}\right)\right]\right|_{z=-\frac{b}{2} \mathrm{i}+\frac{a}{2}}
\end{aligned}
\tag{3}
\label{eq3}
$$
进一步化简可得
$$
\begin{aligned}
\begin{split}
V_{\alpha}^{*} =U_{\alpha}-\mathrm{i} V_{\alpha} = & \left.\frac{\mathrm{d}}{\mathrm{d} z}\left[\frac{\Gamma}{2 \pi \mathrm{i}} \ln \frac{\sin \left[\frac{\pi}{\alpha}\left(z-\frac{b}{2} \mathrm{i}\right)\right]}{\sin \left[\frac{\pi}{\alpha}\left(z+\frac{b}{2} \mathrm{i} -\frac{a}{2}\right)\right]}+\frac{\Gamma}{2 z \mathrm{i}} \ln \left(z+\frac{b}{2} \mathrm{i}-\frac{a}{2}\right)\right]\right|_{z=-\frac{b}{2} \mathrm{i}+\frac{a}{2}} \\
= & \frac{\Gamma}{2 \pi \mathrm{i}}\left.\left\{\frac{\pi}{a} \cdot \frac{1}{\tan \left[\frac{\pi}{a}\left(z-\frac{b}{2} \mathrm{i}\right)\right]}-\frac{\pi}{a} \cdot \frac{1}{\tan \left[\frac{\pi}{a}\left(z+\frac{b}{2} \mathrm{i}-\frac{a}{2}\right)\right]}+\frac{1}{z+\frac{b}{2} \mathrm{i}-\frac{a}{2}}\right\}\right|_{z=-\frac{b}{2} \mathrm{i}+\frac{a}{2}}
\end{split}
\end{aligned}
\tag{4}
\label{eq4}
$$
由 $ z \to -\frac{b}{2} \mathrm{i}+\frac{a}{2} $ 时，有 $\tan \left[\frac{\pi}{a}\left(z+\frac{b}{2} \mathrm{i}-\frac{a}{2}\right)\right] \approx \frac{\pi}{a}\left(z+\frac{b}{2} \mathrm{i}-\frac{a}{2}\right)$，代入上式 $ \eqref{eq4} $，整理有
$$
\begin{aligned}
\begin{split}
V_{\alpha}^{*} = U_{\alpha}-\mathrm{i} V_{\alpha} & = \frac{\Gamma}{2 \pi \mathrm{i}}\left.\left\{\frac{\pi}{a} \cdot \frac{1}{\tan \left[\frac{\pi}{a}\left(z-\frac{b}{2} \mathrm{i}\right)\right]}\right\}\right|_{z=-\frac{b}{2} \mathrm{i}+\frac{a}{2}} \\
& = \frac{\Gamma}{2 \pi \mathrm{i}}\left\{\frac{\pi}{a} \cdot \frac{1}{\tan \left[\frac{\pi}{a}\left(\frac{a}{2} - b \mathrm{i} \right)\right]}\right\} \\
& = \frac{\Gamma}{2 \pi \mathrm{i}}\left\{\frac{\pi}{a} \cdot \frac{1}{\tan \left(\frac{\pi}{2} - \frac{\pi b \mathrm{i}}{a}\right)}\right\} \\
& = \frac{\Gamma}{2 a \mathrm{i}} \cdot \tan\left(\frac{\pi b \mathrm{i}}{a}\right) \\
& = \frac{\Gamma}{2 a \mathrm{i}} \cdot \frac{1}{- \mathrm{i}} \tanh \left(\frac{\pi b}{a}\right) \\
& = \frac{\Gamma}{2 a} \tanh \left(\frac{\pi b}{a}\right)
\end{split}
\end{aligned}
\tag{5}
\label{eq5}
$$
故在点涡 $\alpha$ 处的诱导速度为
$$
\begin{aligned}
V_{\alpha} = U_{\alpha} = \frac{\Gamma}{2 a} \tanh \left(\frac{\pi b}{a}\right).
\end{aligned}
\tag{6}
\label{eq6}
$$
b)  由放置在 $x$ 轴上，关于 $y$ 轴对称（原点布置一个点涡），强度相同，间距相同为 $a$ 的一排无穷多个点涡的流函数为 
$$
\begin{aligned}
\psi_{0} = \frac{1}{2 \mathrm{i}} \left[W_{0}(z) - W_{0}^{*}(z)\right] = - \frac{\Gamma}{4 \pi} \ln \frac{1}{2} \left(\cosh\frac{2 \pi y}{a} - \cos \frac{2 \pi x}{a}\right)
\end{aligned}
\tag{7}
\label{eq7}
$$
由坐标平移可得，上下两排点涡分别产生的流函数为
$$
\begin{aligned}
\psi_{1} =-\frac{\Gamma}{4 \pi} \ln \frac{1}{2}\left\{\cosh \left[\frac{2 \pi}{a}\left(y-\frac{b}{2}\right)\right]-\cos \left(\frac{2 \pi x}{a}\right)\right\}
\end{aligned}
\tag{8}
\label{eq8}
$$

$$
\begin{aligned}
\psi_{2} =\frac{\Gamma}{4 \pi} \ln \frac{1}{2}\left\{\cosh \left[\frac{2 \pi}{a}\left(y+\frac{b}{2}\right)\right]-\cos \left[\frac{2 \pi}{a}\left(x-\frac{a}{2}\right)\right]\right\}
\end{aligned}
\tag{9}
\label{eq9}
$$

由线性性质，叠加可得原点涡系的流函数最终形式为
$$
\begin{aligned}
	\begin{split}
		\psi &=\psi_{1}+\psi_{2} =-\frac{\Gamma}{4 \pi} \cdot \ln \left\{\frac{\cosh \left[\frac{2 \pi}{a}\left(y-\frac{b}{2}\right)\right]-\cos \left(\frac{2 \pi x}{a}\right)}{\cosh \left[\frac{2 \pi}{a}\left(y+\frac{b}{2}\right)\right]-\cos \left[\frac{2 \pi}{a}\left(x-\frac{a}{2}\right)\right]}\right\}.
        \end{split}
\end{aligned}
\tag{10}
\label{eq10}
$$
以上流函数定义在笛卡尔坐标系 $(x,y)$ 下。令其为常数 $\text{const}$，则可根据不同 $b / a$ 大小的情形，来绘制一系列流线簇。

下面采用 ***Mathematica*** 软件分别绘制 $b/a = 0.00, \;0.05, \;0.15, \;0.2806, \;0.35, \;0.50, \;1.00, \;1.50$ 六种情形下的流线分布，并设置 $a = 1, \; \Gamma = 1$，如图 [2](#fig2) 所示。可以观察到，该点涡系流线呈现在上下两排点涡间交替穿插的特点。随着 $b/a$ 增加，两排点涡间的流线扭曲程度逐渐趋缓。当 $b/a = 0$ 时，该点涡系退化为单排点涡系。值得注意的是，当 $b/a = 0.2806$ 时，该点涡系正是由 ***von Kármán*** 提出的**唯一能够保持无粘中性稳定**的情形，即为著名的**卡门涡街 (von Kármán Vortex Street)**。

**问题 1** 的完整 ***Mathematica*** 代码展示如下。

```mathematica
a = 1;
b = 0.2806;
Gamma0 = 1;
Phi = (-(Gamma0/(4 * Pi)))*
Log[(Cosh[(2*Pi)/a*(y - b/2)] - Cos[(2*Pi*x)/a])/(
Cosh[(2*Pi)/a*(y + b/2)] - Cos[(2*Pi)/a*(x - a/2)])];
graph1 = ContourPlot[Phi, {x, -2, 2}, {y, -1, 1}, 
PlotTheme -> "Detailed", AspectRatio -> Automatic, Contours -> 42, 
FrameLabel -> {x, y}, PerformanceGoal -> "Quality", ImageSize -> 500]
Export["AdFM_hw_2_2_4.pdf", graph1]
```
