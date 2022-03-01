---
title: 【类型论】五、Types dependent on terms
date: 2021-11-01 19:58:23
categories: 小课堂
tags:
     - 函数式
     - 类型论
     - 教程
---

本文为*Type Theory and Formal Proof : An Introduction* 的笔记，纯个人向（

------

之前我们遇到了以下的依赖关系：

- *依赖于项的项*： <img src="https://www.zhihu.com/equation?tex=\lambda_\to" alt="\lambda_\to" class="ee_img tr_noresize" eeimg="1"> .
- 依赖于项的项 <img src="https://www.zhihu.com/equation?tex=+" alt="+" class="ee_img tr_noresize" eeimg="1"> *依赖于类型的项*： <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> .
- 依赖于项的项 <img src="https://www.zhihu.com/equation?tex=+" alt="+" class="ee_img tr_noresize" eeimg="1"> *依赖于类型的类型*： <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> .

显然有一个扩展缺失了：

- 依赖于项的项 <img src="https://www.zhihu.com/equation?tex=+" alt="+" class="ee_img tr_noresize" eeimg="1"> *依赖于项的类型*： <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> .

一个依赖于项的类型形如：

<img src="https://www.zhihu.com/equation?tex=\lambda x : A . M
" alt="\lambda x : A . M
" class="ee_img tr_noresize" eeimg="1">
其中 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 是一个类型， <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 是一个项变量（那么 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 一定是个类型）.  <img src="https://www.zhihu.com/equation?tex=\lambda x : A.M" alt="\lambda x : A.M" class="ee_img tr_noresize" eeimg="1"> 这个抽象*依赖于*项 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> .与上文相应的，“一个依赖于项的*类型*”其实是一个以类型为值的函数（type-valued function）或称类型构造子（type constructor）.

下面从集合和命题两方面介绍依赖于项的类型的作用：

1. 对任意 <img src="https://www.zhihu.com/equation?tex=n:nat" alt="n:nat" class="ee_img tr_noresize" eeimg="1"> ，设 <img src="https://www.zhihu.com/equation?tex=S_n" alt="S_n" class="ee_img tr_noresize" eeimg="1"> 为集合. 不严谨地说，每个集合可以看做一个类型，那么 <img src="https://www.zhihu.com/equation?tex=\lambda n:nat.S_n" alt="\lambda n:nat.S_n" class="ee_img tr_noresize" eeimg="1"> 是依赖于项 <img src="https://www.zhihu.com/equation?tex=n" alt="n" class="ee_img tr_noresize" eeimg="1"> 的一个类型（构造子）. 也可以说 <img src="https://www.zhihu.com/equation?tex=\lambda n:nat. S_n" alt="\lambda n:nat. S_n" class="ee_img tr_noresize" eeimg="1"> 是一个由项 <img src="https://www.zhihu.com/equation?tex=n" alt="n" class="ee_img tr_noresize" eeimg="1"> 映射到集合 <img src="https://www.zhihu.com/equation?tex=S_n" alt="S_n" class="ee_img tr_noresize" eeimg="1"> 的函数.

   另一个术语称为**类型家族**（family of types）（对于每个 <img src="https://www.zhihu.com/equation?tex=n:nat" alt="n:nat" class="ee_img tr_noresize" eeimg="1"> 的类型）或称**索引类型**（indexed type）（以 <img src="https://www.zhihu.com/equation?tex=n:nat" alt="n:nat" class="ee_img tr_noresize" eeimg="1"> 为索引）. 

   因为 <img src="https://www.zhihu.com/equation?tex=n:nat" alt="n:nat" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=S_n:\ast" alt="S_n:\ast" class="ee_img tr_noresize" eeimg="1"> ，所以 <img src="https://www.zhihu.com/equation?tex=\lambda n:nat.S_n" alt="\lambda n:nat.S_n" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=nat\to\ast" alt="nat\to\ast" class="ee_img tr_noresize" eeimg="1"> .

   一个常用的例子是：设 <img src="https://www.zhihu.com/equation?tex=\langle v_1,\cdots,v_n \rangle" alt="\langle v_1,\cdots,v_n \rangle" class="ee_img tr_noresize" eeimg="1"> 为 <img src="https://www.zhihu.com/equation?tex=n" alt="n" class="ee_img tr_noresize" eeimg="1"> 个自然数的序列，则 <img src="https://www.zhihu.com/equation?tex=V_n=\{\langle v_1,\cdots,v_n\rangle|v_i\in\mathbb{N}\}" alt="V_n=\{\langle v_1,\cdots,v_n\rangle|v_i\in\mathbb{N}\}" class="ee_img tr_noresize" eeimg="1"> 是所有长度为 <img src="https://www.zhihu.com/equation?tex=n" alt="n" class="ee_img tr_noresize" eeimg="1"> 的自然数序列（向量）， <img src="https://www.zhihu.com/equation?tex=\lambda n:nat.V_n" alt="\lambda n:nat.V_n" class="ee_img tr_noresize" eeimg="1"> 把 <img src="https://www.zhihu.com/equation?tex=n" alt="n" class="ee_img tr_noresize" eeimg="1"> 映射到所有长度为 <img src="https://www.zhihu.com/equation?tex=n" alt="n" class="ee_img tr_noresize" eeimg="1"> 的向量集合.

2. 对任意 <img src="https://www.zhihu.com/equation?tex=n:nat" alt="n:nat" class="ee_img tr_noresize" eeimg="1"> ，设 <img src="https://www.zhihu.com/equation?tex=P_n" alt="P_n" class="ee_img tr_noresize" eeimg="1"> 为命题. 那么 <img src="https://www.zhihu.com/equation?tex=\lambda n:nat.P_n" alt="\lambda n:nat.P_n" class="ee_img tr_noresize" eeimg="1"> 也是一个类型（构造子），依赖于项 <img src="https://www.zhihu.com/equation?tex=n" alt="n" class="ee_img tr_noresize" eeimg="1"> . 也可以说 <img src="https://www.zhihu.com/equation?tex=\lambda n:nat. P_n" alt="\lambda n:nat. P_n" class="ee_img tr_noresize" eeimg="1"> 是一个由项 <img src="https://www.zhihu.com/equation?tex=n" alt="n" class="ee_img tr_noresize" eeimg="1"> 映射到命题 <img src="https://www.zhihu.com/equation?tex=P_n" alt="P_n" class="ee_img tr_noresize" eeimg="1"> 的函数. 这样的函数表达了逻辑中称为**谓词**（predicate）的东西. 例如，设 <img src="https://www.zhihu.com/equation?tex=P_n" alt="P_n" class="ee_img tr_noresize" eeimg="1"> 为命题“ <img src="https://www.zhihu.com/equation?tex=n" alt="n" class="ee_img tr_noresize" eeimg="1"> 为质数”， <img src="https://www.zhihu.com/equation?tex=\lambda n:nat.P_n" alt="\lambda n:nat.P_n" class="ee_img tr_noresize" eeimg="1"> 则是一个自然数是质数的谓词. 

我们把这个扩展了依赖于项的类型的类型系统称为 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> ，其中的 <img src="https://www.zhihu.com/equation?tex=\rm P" alt="\rm P" class="ee_img tr_noresize" eeimg="1"> 就是来自谓词（predicate）.

##  <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 的派生规则

 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 的派生规则和 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 很类似：

<img src="https://www.zhihu.com/equation?tex=(sort)\quad\emptyset\ \vdash\ \ast:\square\\
\ \\
(var)\quad\dfrac{\Gamma\ \vdash\ A:s}{\Gamma,\ x:A\ \vdash\ x:A}\quad 若x\notin \Gamma\\
\ \\
(weak)\quad\dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ C:s}{\Gamma,\ x:C\ \vdash\ A:B}\quad 若 x\notin \Gamma\\
\ \\
(form)\quad\dfrac{\Gamma\ \vdash\ A:\ast\quad\Gamma,\ x:A\ \vdash\ B:s}{\Gamma\ \vdash\ \Pi x:A.B:s}\\
\ \\
(appl)\quad\dfrac{\Gamma\ \vdash\ M:\Pi x:A.B\quad\Gamma\ \vdash\ N:A}{\Gamma\ \vdash\ M\ N\ :\ B[x:=N]}\\
\ \\
(abst)\quad\dfrac{\Gamma,\ x:A\ \vdash\ M:B\quad\Gamma\ \vdash\ \Pi x:A.B:s}{\Gamma\ \vdash\ \lambda x:A.M:\Pi x:A.B}\\
\ \\
(conv)\quad\dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ B':s}{\Gamma\ \vdash\ A:B'}\quad 若B=_\beta B'
" alt="(sort)\quad\emptyset\ \vdash\ \ast:\square\\
\ \\
(var)\quad\dfrac{\Gamma\ \vdash\ A:s}{\Gamma,\ x:A\ \vdash\ x:A}\quad 若x\notin \Gamma\\
\ \\
(weak)\quad\dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ C:s}{\Gamma,\ x:C\ \vdash\ A:B}\quad 若 x\notin \Gamma\\
\ \\
(form)\quad\dfrac{\Gamma\ \vdash\ A:\ast\quad\Gamma,\ x:A\ \vdash\ B:s}{\Gamma\ \vdash\ \Pi x:A.B:s}\\
\ \\
(appl)\quad\dfrac{\Gamma\ \vdash\ M:\Pi x:A.B\quad\Gamma\ \vdash\ N:A}{\Gamma\ \vdash\ M\ N\ :\ B[x:=N]}\\
\ \\
(abst)\quad\dfrac{\Gamma,\ x:A\ \vdash\ M:B\quad\Gamma\ \vdash\ \Pi x:A.B:s}{\Gamma\ \vdash\ \lambda x:A.M:\Pi x:A.B}\\
\ \\
(conv)\quad\dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ B':s}{\Gamma\ \vdash\ A:B'}\quad 若B=_\beta B'
" class="ee_img tr_noresize" eeimg="1">
与 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 的主要不同在：

1.  <img src="https://www.zhihu.com/equation?tex=\to" alt="\to" class="ee_img tr_noresize" eeimg="1"> -类型的升级. 在 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 的 <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> ， <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> ， <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> 规则里没有 <img src="https://www.zhihu.com/equation?tex=\to" alt="\to" class="ee_img tr_noresize" eeimg="1"> -类型 <img src="https://www.zhihu.com/equation?tex=A\to B" alt="A\to B" class="ee_img tr_noresize" eeimg="1"> ，取而代之的是 <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> -类型 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.B" alt="\Pi x:A.B" class="ee_img tr_noresize" eeimg="1"> . 这是一种推广，因为这样 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 可以作为自由变量出现在 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 中. 因此我们不再需要一个固定的 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 类型到 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 类型的函数类型，而是一个输出类型依赖于从输入类型 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 中选出的值 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 的**依赖积**（dependent product）.
2. 输入类型的降级. 在 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 中，我们有依赖于项的类型，但没有在 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 中依赖于类型的类型，如 <img src="https://www.zhihu.com/equation?tex=\Pi \alpha:\ast.\alpha\to\alpha" alt="\Pi \alpha:\ast.\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> . 因此类型 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.B" alt="\Pi x:A.B" class="ee_img tr_noresize" eeimg="1"> 在 <img src="https://www.zhihu.com/equation?tex=\lambda P" alt="\lambda P" class="ee_img tr_noresize" eeimg="1"> 中有“ <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 是项”的性质，所以 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 的类型只能是 <img src="https://www.zhihu.com/equation?tex=\ast" alt="\ast" class="ee_img tr_noresize" eeimg="1"> 而不是 <img src="https://www.zhihu.com/equation?tex=\square" alt="\square" class="ee_img tr_noresize" eeimg="1"> . 对比 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1">  的 <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> -规则.

注意在 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.B" alt="\Pi x:A.B" class="ee_img tr_noresize" eeimg="1"> 中， <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 可能依赖于 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> ：

对于 <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> ，我们需要扩展第二个前提的上下文，将 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 变为 <img src="https://www.zhihu.com/equation?tex=\Gamma,\ x:A" alt="\Gamma,\ x:A" class="ee_img tr_noresize" eeimg="1"> .

对于 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> ，我们需要选择与 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 的输入值 <img src="https://www.zhihu.com/equation?tex=N" alt="N" class="ee_img tr_noresize" eeimg="1"> 对应的输出类型 <img src="https://www.zhihu.com/equation?tex=B[x:=N]" alt="B[x:=N]" class="ee_img tr_noresize" eeimg="1"> .

注意规则中可以对不同level使用，例如 <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> -规则：

1.  <img src="https://www.zhihu.com/equation?tex=s=\ast" alt="s=\ast" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=A:\ast,\ B:\ast" alt="A:\ast,\ B:\ast" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.B:\ast" alt="\Pi x:A.B:\ast" class="ee_img tr_noresize" eeimg="1"> 
2.  <img src="https://www.zhihu.com/equation?tex=s=\square" alt="s=\square" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=A:\ast,\ B:\square" alt="A:\ast,\ B:\square" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.B:\square" alt="\Pi x:A.B:\square" class="ee_img tr_noresize" eeimg="1"> 

**表记**：在 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 中，如果确定 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 不在 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 中自由出现，我们可以把 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.B" alt="\Pi x:A.B" class="ee_img tr_noresize" eeimg="1"> 记作 <img src="https://www.zhihu.com/equation?tex=A\to B" alt="A\to B" class="ee_img tr_noresize" eeimg="1"> . 不过，正式地说，在 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 中只有 <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> -类型，没有 <img src="https://www.zhihu.com/equation?tex=\to" alt="\to" class="ee_img tr_noresize" eeimg="1"> -类型.

> 如果 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 是有限类型，假设有两个元素 <img src="https://www.zhihu.com/equation?tex=a_1,\ a_2" alt="a_1,\ a_2" class="ee_img tr_noresize" eeimg="1"> ，那么 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.B" alt="\Pi x:A.B" class="ee_img tr_noresize" eeimg="1"> 刚好就是 <img src="https://www.zhihu.com/equation?tex=B[x:=a_1]\times B[x:=a_2]" alt="B[x:=a_1]\times B[x:=a_2]" class="ee_img tr_noresize" eeimg="1"> ，即笛卡尔积. 因此 <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> -类型既可以看成笛卡尔积的推广，也可以看成函数空间的推广（若 <img src="https://www.zhihu.com/equation?tex=x\notin FV(B)" alt="x\notin FV(B)" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.B" alt="\Pi x:A.B" class="ee_img tr_noresize" eeimg="1"> 就是 <img src="https://www.zhihu.com/equation?tex=A\to B" alt="A\to B" class="ee_img tr_noresize" eeimg="1"> ）. 

##  <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 的派生例

 <img src="https://www.zhihu.com/equation?tex=(1)\quad\emptyset\ \vdash\ \ast:\square\quad(sort)" alt="(1)\quad\emptyset\ \vdash\ \ast:\square\quad(sort)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(2)\quad A:\ast\ \vdash\ A:\ast\quad对(1)用(var)" alt="(2)\quad A:\ast\ \vdash\ A:\ast\quad对(1)用(var)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(3)\quad A:\ast\ \vdash\ \ast:\square\quad对(1)和(1)用(weak)" alt="(3)\quad A:\ast\ \vdash\ \ast:\square\quad对(1)和(1)用(weak)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(4)\quad A:\ast,\ x:A\ \vdash\ \ast:\square\quad对(3)和(2)用(weak)" alt="(4)\quad A:\ast,\ x:A\ \vdash\ \ast:\square\quad对(3)和(2)用(weak)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(5)\quad A:\ast\ \vdash\ A\to\ast:\square\quad对(2)和(4)用(form)" alt="(5)\quad A:\ast\ \vdash\ A\to\ast:\square\quad对(2)和(4)用(form)" class="ee_img tr_noresize" eeimg="1"> 

除了最后一行，其余的在 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 中也可以派生. 第 <img src="https://www.zhihu.com/equation?tex=(5)" alt="(5)" class="ee_img tr_noresize" eeimg="1"> 行，我们派生出了超级类型 <img src="https://www.zhihu.com/equation?tex=A\to\ast" alt="A\to\ast" class="ee_img tr_noresize" eeimg="1"> ，即 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.\ast" alt="\Pi x:A.\ast" class="ee_img tr_noresize" eeimg="1"> . 此时我们有了 <img src="https://www.zhihu.com/equation?tex=\to" alt="\to" class="ee_img tr_noresize" eeimg="1"> 两边level不同的情况，这在 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 中是不可能的. 注意 <img src="https://www.zhihu.com/equation?tex=A\to\ast" alt="A\to\ast" class="ee_img tr_noresize" eeimg="1"> 是一个依赖于项的kind，而 <img src="https://www.zhihu.com/equation?tex=P:A\to\ast" alt="P:A\to\ast" class="ee_img tr_noresize" eeimg="1"> 是一个依赖于项的类型，尽管它们依赖的项 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 看不到了，它在 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.\ast" alt="\Pi x:A.\ast" class="ee_img tr_noresize" eeimg="1"> 里. 我们假设 <img src="https://www.zhihu.com/equation?tex=P:A\to\ast" alt="P:A\to\ast" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=(6)\quad A:\ast,\ P:A\to\ast\ \vdash\ P:A\to\ast\quad对(5)用(var)" alt="(6)\quad A:\ast,\ P:A\to\ast\ \vdash\ P:A\to\ast\quad对(5)用(var)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(7)\quad A:\ast,\ P:A\to\ast\ \vdash\ A:\ast\quad对(2)和(5)用(weak)" alt="(7)\quad A:\ast,\ P:A\to\ast\ \vdash\ A:\ast\quad对(2)和(5)用(weak)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(8)\quad A:\ast,\ P:A\to\ast\ \vdash\ \ast:\square对(3)和(5)用(weak)" alt="(8)\quad A:\ast,\ P:A\to\ast\ \vdash\ \ast:\square对(3)和(5)用(weak)" class="ee_img tr_noresize" eeimg="1"> 

我们可以把 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 应用到 <img src="https://www.zhihu.com/equation?tex=P" alt="P" class="ee_img tr_noresize" eeimg="1"> ，得到类型 <img src="https://www.zhihu.com/equation?tex=P\ x" alt="P\ x" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=(9)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ x:A\quad对(7)用(var)" alt="(9)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ x:A\quad对(7)用(var)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(10)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ P:A\to\ast\quad对(6)和(7)用weak" alt="(10)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ P:A\to\ast\quad对(6)和(7)用weak" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(11)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ P\ x:\ast\quad对(10)和(9)用(appl)" alt="(11)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ P\ x:\ast\quad对(10)和(9)用(appl)" class="ee_img tr_noresize" eeimg="1"> 

我们可以构造一个“真正”的体里有变量 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 出现的依值类型 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.P\ x" alt="\Pi x:A.P\ x" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=(12)\quad A:\ast,\ P:A\to\ast\ \vdash\ \Pi x:A.P\ x\quad对(7)和(11)用(form)" alt="(12)\quad A:\ast,\ P:A\to\ast\ \vdash\ \Pi x:A.P\ x\quad对(7)和(11)用(form)" class="ee_img tr_noresize" eeimg="1"> 

我们可以证明 <img src="https://www.zhihu.com/equation?tex=P\ x\to P\ x" alt="P\ x\to P\ x" class="ee_img tr_noresize" eeimg="1"> 也是可派生的，然后构造另一个 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.P\ x\to P\ x" alt="\Pi x:A.P\ x\to P\ x" class="ee_img tr_noresize" eeimg="1"> .

 <img src="https://www.zhihu.com/equation?tex=(13)\quad A:\ast,\ P:A\to\ast,\ x:A,\ y:P\ x\ \vdash\ P\ x:\ast\quad对(11)和(11)用(weak)" alt="(13)\quad A:\ast,\ P:A\to\ast,\ x:A,\ y:P\ x\ \vdash\ P\ x:\ast\quad对(11)和(11)用(weak)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(14)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ P\ x\to P\ x:\ast\quad对(11)和(13)用(form)" alt="(14)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ P\ x\to P\ x:\ast\quad对(11)和(13)用(form)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(15)\quad A:\ast,\ P:A\to\ast\ \vdash\ \Pi x:A.P\ x\to P\ x:\ast\quad对(7)和(14)用(form)" alt="(15)\quad A:\ast,\ P:A\to\ast\ \vdash\ \Pi x:A.P\ x\to P\ x:\ast\quad对(7)和(14)用(form)" class="ee_img tr_noresize" eeimg="1"> 

最后我们可以得到 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.P\ x\to P\ x" alt="\Pi x:A.P\ x\to P\ x" class="ee_img tr_noresize" eeimg="1"> 类型下有项：

 <img src="https://www.zhihu.com/equation?tex=(16)\quad A:\ast,\ P:A\to\ast,\ x:A,\ y:P\ x\ \vdash\ y:P\ x\quad对(11)用(var)" alt="(16)\quad A:\ast,\ P:A\to\ast,\ x:A,\ y:P\ x\ \vdash\ y:P\ x\quad对(11)用(var)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(17)\quad A:\ast,\ P:A\to\ast,\ x:A\ x\ \vdash\ \lambda y:P\ x.y:P\ x\to P\ x\quad对(16)和(14)用(abst)" alt="(17)\quad A:\ast,\ P:A\to\ast,\ x:A\ x\ \vdash\ \lambda y:P\ x.y:P\ x\to P\ x\quad对(16)和(14)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(18)\quad A:\ast,\ P:A\to\ast\ \vdash\ \lambda x:A.\lambda y:P\ x.y:\Pi x:A.P\ x\to P\ x\quad对(17)和(15)用(abst)" alt="(18)\quad A:\ast,\ P:A\to\ast\ \vdash\ \lambda x:A.\lambda y:P\ x.y:\Pi x:A.P\ x\to P\ x\quad对(17)和(15)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

综上，我们得到了：

1. 良类型性： <img src="https://www.zhihu.com/equation?tex=\lambda x:A.\lambda y:P\ x.y" alt="\lambda x:A.\lambda y:P\ x.y" class="ee_img tr_noresize" eeimg="1"> 是良类型的.
2. 类型检查：检查了 <img src="https://www.zhihu.com/equation?tex=A:\ast,\ P:A\to\ast\ \vdash\ \lambda x:A.\lambda y:P\ x.y:\Pi x:A.P\ x\to P\ x" alt="A:\ast,\ P:A\to\ast\ \vdash\ \lambda x:A.\lambda y:P\ x.y:\Pi x:A.P\ x\to P\ x" class="ee_img tr_noresize" eeimg="1"> 
3. 项的寻找：找到了 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.P\ x\to P\ x" alt="\Pi x:A.P\ x\to P\ x" class="ee_img tr_noresize" eeimg="1"> 类型在上下文 <img src="https://www.zhihu.com/equation?tex=A:\ast,\ P:A\to\ast" alt="A:\ast,\ P:A\to\ast" class="ee_img tr_noresize" eeimg="1"> 中的项.

##  <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 中的最小谓词逻辑

 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 可以编码一个称为**最小谓词逻辑**（minimal predicate logic）的简单逻辑系统，它的逻辑操作只有**蕴含**（implication）和**全称量化**（universal quantification）. 这一谓词逻辑的基本实体有**命题**（propositions）、**集合**（sets）和**集合上的谓词**（predicates over sets）.

如前文所说，一个类型系统有PAT解释：

- 如果项 <img src="https://www.zhihu.com/equation?tex=b" alt="b" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> （即 <img src="https://www.zhihu.com/equation?tex=b:B" alt="b:B" class="ee_img tr_noresize" eeimg="1"> ）， <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 解释为一个命题，则 <img src="https://www.zhihu.com/equation?tex=b" alt="b" class="ee_img tr_noresize" eeimg="1"> 可以解释为 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 的一个**证明**. 这样的项 <img src="https://www.zhihu.com/equation?tex=b" alt="b" class="ee_img tr_noresize" eeimg="1"> 在类型论中称为**证明对象**（proof object）.
- 而当命题 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 不存在居留元（没有 <img src="https://www.zhihu.com/equation?tex=b" alt="b" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=b:B" alt="b:B" class="ee_img tr_noresize" eeimg="1"> ），则 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 不存在证明， <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 为**假**.

### I. 集合

我们将一个集合 <img src="https://www.zhihu.com/equation?tex=S" alt="S" class="ee_img tr_noresize" eeimg="1"> 编码成一个类型，即 <img src="https://www.zhihu.com/equation?tex=S:\ast" alt="S:\ast" class="ee_img tr_noresize" eeimg="1"> ，集合的元素是项. 所以如果 <img src="https://www.zhihu.com/equation?tex=a" alt="a" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=S" alt="S" class="ee_img tr_noresize" eeimg="1"> 的元素，则 <img src="https://www.zhihu.com/equation?tex=a:S" alt="a:S" class="ee_img tr_noresize" eeimg="1"> ，例如：

 <img src="https://www.zhihu.com/equation?tex=nat:\ast,\ nat\to nat:\ast;\quad 3:nat,\ \lambda n:nat.n:nat\to nat" alt="nat:\ast,\ nat\to nat:\ast;\quad 3:nat,\ \lambda n:nat.n:nat\to nat" class="ee_img tr_noresize" eeimg="1"> 

### II. 命题

我们把命题也编码成类型. 所以如果 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 是命题，则 <img src="https://www.zhihu.com/equation?tex=A:\ast" alt="A:\ast" class="ee_img tr_noresize" eeimg="1"> . 根据PAT-解释，这个 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 的居留元 <img src="https://www.zhihu.com/equation?tex=p" alt="p" class="ee_img tr_noresize" eeimg="1"> 编码了一个 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 的证明. 

### III. 谓词

一个谓词 <img src="https://www.zhihu.com/equation?tex=P" alt="P" class="ee_img tr_noresize" eeimg="1"> 是从一个集合 <img src="https://www.zhihu.com/equation?tex=S" alt="S" class="ee_img tr_noresize" eeimg="1"> 到所有命题集合的一个函数. 所以 <img src="https://www.zhihu.com/equation?tex=P:S\to\ast" alt="P:S\to\ast" class="ee_img tr_noresize" eeimg="1"> . 

如果 <img src="https://www.zhihu.com/equation?tex=P" alt="P" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=S" alt="S" class="ee_img tr_noresize" eeimg="1"> 上的一个任意的谓词，即 <img src="https://www.zhihu.com/equation?tex=P:S\to\ast" alt="P:S\to\ast" class="ee_img tr_noresize" eeimg="1"> ，则对每个 <img src="https://www.zhihu.com/equation?tex=a:S" alt="a:S" class="ee_img tr_noresize" eeimg="1"> ，都有 <img src="https://www.zhihu.com/equation?tex=P\ a:\ast" alt="P\ a:\ast" class="ee_img tr_noresize" eeimg="1"> . 所有的 <img src="https://www.zhihu.com/equation?tex=P\ a" alt="P\ a" class="ee_img tr_noresize" eeimg="1"> 都是命题，即类型（level 2），所以每个 <img src="https://www.zhihu.com/equation?tex=P\ a" alt="P\ a" class="ee_img tr_noresize" eeimg="1"> 都可能有居留元. 

- 如果 <img src="https://www.zhihu.com/equation?tex=P\ a" alt="P\ a" class="ee_img tr_noresize" eeimg="1"> 下有居留元，即存在 <img src="https://www.zhihu.com/equation?tex=t" alt="t" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=t:P\ a" alt="t:P\ a" class="ee_img tr_noresize" eeimg="1"> ，则这个谓词对 <img src="https://www.zhihu.com/equation?tex=a" alt="a" class="ee_img tr_noresize" eeimg="1"> 成立.
- 如果 <img src="https://www.zhihu.com/equation?tex=P\ b" alt="P\ b" class="ee_img tr_noresize" eeimg="1"> 下没有居留元，则这个谓词对 <img src="https://www.zhihu.com/equation?tex=b" alt="b" class="ee_img tr_noresize" eeimg="1"> 不成立.

### IV. 蕴含

使用PAT-解释，我们可以把 <img src="https://www.zhihu.com/equation?tex=\Rightarrow" alt="\Rightarrow" class="ee_img tr_noresize" eeimg="1"> 编码成 <img src="https://www.zhihu.com/equation?tex=\to" alt="\to" class="ee_img tr_noresize" eeimg="1"> ：

-  <img src="https://www.zhihu.com/equation?tex=A\Rightarrow B" alt="A\Rightarrow B" class="ee_img tr_noresize" eeimg="1"> 为真.
- 如果 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 为真，则 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 也为真.
- 如果 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 有居留元，则 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 也有居留元.
- 存在函数将 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 的居留元映射到 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 的居留元.
- 存在 <img src="https://www.zhihu.com/equation?tex=f" alt="f" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=f:A\to B" alt="f:A\to B" class="ee_img tr_noresize" eeimg="1"> .
-  <img src="https://www.zhihu.com/equation?tex=A\to B" alt="A\to B" class="ee_img tr_noresize" eeimg="1"> 有居留元.

所以 <img src="https://www.zhihu.com/equation?tex=A\Rightarrow B" alt="A\Rightarrow B" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=A\to B" alt="A\to B" class="ee_img tr_noresize" eeimg="1"> 有居留元等价. 

我们可以通过 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> -规则和 <img src="https://www.zhihu.com/equation?tex=\Rightarrow" alt="\Rightarrow" class="ee_img tr_noresize" eeimg="1"> -消去、 <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> -规则和 <img src="https://www.zhihu.com/equation?tex=\Rightarrow" alt="\Rightarrow" class="ee_img tr_noresize" eeimg="1"> -引入的对应关系免费获得蕴含的构造规则和消去规则. 

### V. 全称量化

考虑对于集合 <img src="https://www.zhihu.com/equation?tex=S" alt="S" class="ee_img tr_noresize" eeimg="1"> 上某个依赖于 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 的谓词 <img src="https://www.zhihu.com/equation?tex=P" alt="P" class="ee_img tr_noresize" eeimg="1"> 的全称量化 <img src="https://www.zhihu.com/equation?tex=\forall_{x\in S}(P(x))" alt="\forall_{x\in S}(P(x))" class="ee_img tr_noresize" eeimg="1"> . 

-  <img src="https://www.zhihu.com/equation?tex=\forall_{x\in S}(P(x))" alt="\forall_{x\in S}(P(x))" class="ee_img tr_noresize" eeimg="1"> 为真.
- 对集合 <img src="https://www.zhihu.com/equation?tex=S" alt="S" class="ee_img tr_noresize" eeimg="1"> 中任意的 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> ，命题 <img src="https://www.zhihu.com/equation?tex=P(x)" alt="P(x)" class="ee_img tr_noresize" eeimg="1"> 为真.
- 对集合 <img src="https://www.zhihu.com/equation?tex=S" alt="S" class="ee_img tr_noresize" eeimg="1"> 中任意的 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> ，类型 <img src="https://www.zhihu.com/equation?tex=P\ x" alt="P\ x" class="ee_img tr_noresize" eeimg="1"> 下有居留元.
- 存在一个将每一个 <img src="https://www.zhihu.com/equation?tex=S" alt="S" class="ee_img tr_noresize" eeimg="1"> 中的 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 映射到 <img src="https://www.zhihu.com/equation?tex=P\ x" alt="P\ x" class="ee_img tr_noresize" eeimg="1">  居留元的函数（这个函数的类型是 <img src="https://www.zhihu.com/equation?tex=\Pi x:X.P\ x" alt="\Pi x:X.P\ x" class="ee_img tr_noresize" eeimg="1"> ）.
- 存在 <img src="https://www.zhihu.com/equation?tex=f" alt="f" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=f:\Pi x:S.P\ x" alt="f:\Pi x:S.P\ x" class="ee_img tr_noresize" eeimg="1"> .
-  <img src="https://www.zhihu.com/equation?tex=\Pi x:S.P\ x" alt="\Pi x:S.P\ x" class="ee_img tr_noresize" eeimg="1"> 有居留元.

与蕴含类似，我们将全称量化 <img src="https://www.zhihu.com/equation?tex=\forall_{x\in S}(P(x))" alt="\forall_{x\in S}(P(x))" class="ee_img tr_noresize" eeimg="1"> 编码为 <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> -类型 <img src="https://www.zhihu.com/equation?tex=\Pi x:S.P\ x" alt="\Pi x:S.P\ x" class="ee_img tr_noresize" eeimg="1"> .

同样地， <img src="https://www.zhihu.com/equation?tex=\forall" alt="\forall" class="ee_img tr_noresize" eeimg="1"> 的构造和消去规则也可以看做 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 中 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> -和 <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> -规则的特例.

