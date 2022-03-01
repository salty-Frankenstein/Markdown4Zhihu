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

- *依赖于项的项*：$\lambda_\to$.
- 依赖于项的项$+$*依赖于类型的项*：$\lambda2$.
- 依赖于项的项$+$*依赖于类型的类型*：$\lambda\underline{\omega}$.

显然有一个扩展缺失了：

- 依赖于项的项$+$*依赖于项的类型*：$\lambda{\rm P}$.

一个依赖于项的类型形如：
$$
\lambda x : A . M
$$
其中$M$是一个类型，$x$是一个项变量（那么$A$一定是个类型）. $\lambda x : A.M$这个抽象*依赖于*项$x$.与上文相应的，“一个依赖于项的*类型*”其实是一个以类型为值的函数（type-valued function）或称类型构造子（type constructor）.

下面从集合和命题两方面介绍依赖于项的类型的作用：

1. 对任意$n:nat$，设$S_n$为集合. 不严谨地说，每个集合可以看做一个类型，那么$\lambda n:nat.S_n$是依赖于项$n$的一个类型（构造子）. 也可以说$\lambda n:nat. S_n$是一个由项$n$映射到集合$S_n$的函数.

   另一个术语称为**类型家族**（family of types）（对于每个$n:nat$的类型）或称**索引类型**（indexed type）（以$n:nat$为索引）. 

   因为$n:nat$且$S_n:\ast$，所以$\lambda n:nat.S_n$有类型$nat\to\ast$.

   一个常用的例子是：设$\langle v_1,\cdots,v_n \rangle$为$n$个自然数的序列，则$V_n=\{\langle v_1,\cdots,v_n\rangle|v_i\in\mathbb{N}\}$是所有长度为$n$的自然数序列（向量），$\lambda n:nat.V_n$把$n$映射到所有长度为$n$的向量集合.

2. 对任意$n:nat$，设$P_n$为命题. 那么$\lambda n:nat.P_n$也是一个类型（构造子），依赖于项$n$. 也可以说$\lambda n:nat. P_n$是一个由项$n$映射到命题$P_n$的函数. 这样的函数表达了逻辑中称为**谓词**（predicate）的东西. 例如，设$P_n$为命题“$n$为质数”，$\lambda n:nat.P_n$则是一个自然数是质数的谓词. 

我们把这个扩展了依赖于项的类型的类型系统称为$\lambda{\rm P}$，其中的$\rm P$就是来自谓词（predicate）.

## $\lambda{\rm P}$的派生规则

$\lambda{\rm P}$的派生规则和$\lambda\underline{\omega}$很类似：
$$
(sort)\quad\emptyset\ \vdash\ \ast:\square\\
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
$$
与$\lambda\underline{\omega}$的主要不同在：

1. $\to$-类型的升级. 在$\lambda{\rm P}$的$(form)$，$(appl)$，$(abst)$规则里没有$\to$-类型$A\to B$，取而代之的是$\Pi$-类型$\Pi x:A.B$. 这是一种推广，因为这样$x$可以作为自由变量出现在$B$中. 因此我们不再需要一个固定的$A$类型到$B$类型的函数类型，而是一个输出类型依赖于从输入类型$A$中选出的值$x$的**依赖积**（dependent product）.
2. 输入类型的降级. 在$\lambda{\rm P}$中，我们有依赖于项的类型，但没有在$\lambda\underline{\omega}$中依赖于类型的类型，如$\Pi \alpha:\ast.\alpha\to\alpha$. 因此类型$\Pi x:A.B$在$\lambda P$中有“$x$是项”的性质，所以$A$的类型只能是$\ast$而不是$\square$. 对比$\lambda{\rm P}$和$\lambda\underline{\omega}$ 的$(form)$-规则.

注意在$\Pi x:A.B$中，$B$可能依赖于$x$：

对于$(form)$，我们需要扩展第二个前提的上下文，将$\Gamma$变为$\Gamma,\ x:A$.

对于$(appl)$，我们需要选择与$x$的输入值$N$对应的输出类型$B[x:=N]$.

注意规则中可以对不同level使用，例如$(form)$-规则：

1. $s=\ast$，则$A:\ast,\ B:\ast$且$\Pi x:A.B:\ast$
2. $s=\square$，则$A:\ast,\ B:\square$且$\Pi x:A.B:\square$

**表记**：在$\lambda{\rm P}$中，如果确定$x$不在$B$中自由出现，我们可以把$\Pi x:A.B$记作$A\to B$. 不过，正式地说，在$\lambda{\rm P}$中只有$\Pi$-类型，没有$\to$-类型.

> 如果$A$是有限类型，假设有两个元素$a_1,\ a_2$，那么$\Pi x:A.B$刚好就是$B[x:=a_1]\times B[x:=a_2]$，即笛卡尔积. 因此$\Pi$-类型既可以看成笛卡尔积的推广，也可以看成函数空间的推广（若$x\notin FV(B)$，则$\Pi x:A.B$就是$A\to B$）. 

## $\lambda{\rm P}$的派生例

$(1)\quad\emptyset\ \vdash\ \ast:\square\quad(sort)$

$(2)\quad A:\ast\ \vdash\ A:\ast\quad对(1)用(var)$

$(3)\quad A:\ast\ \vdash\ \ast:\square\quad对(1)和(1)用(weak)$

$(4)\quad A:\ast,\ x:A\ \vdash\ \ast:\square\quad对(3)和(2)用(weak)$

$(5)\quad A:\ast\ \vdash\ A\to\ast:\square\quad对(2)和(4)用(form)$

除了最后一行，其余的在$\lambda\underline{\omega}$中也可以派生. 第$(5)$行，我们派生出了超级类型$A\to\ast$，即$\Pi x:A.\ast$. 此时我们有了$\to$两边level不同的情况，这在$\lambda\underline{\omega}$中是不可能的. 注意$A\to\ast$是一个依赖于项的kind，而$P:A\to\ast$是一个依赖于项的类型，尽管它们依赖的项$x$看不到了，它在$\Pi x:A.\ast$里. 我们假设$P:A\to\ast$：

$(6)\quad A:\ast,\ P:A\to\ast\ \vdash\ P:A\to\ast\quad对(5)用(var)$

$(7)\quad A:\ast,\ P:A\to\ast\ \vdash\ A:\ast\quad对(2)和(5)用(weak)$

$(8)\quad A:\ast,\ P:A\to\ast\ \vdash\ \ast:\square对(3)和(5)用(weak)$

我们可以把$x$应用到$P$，得到类型$P\ x$：

$(9)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ x:A\quad对(7)用(var)$

$(10)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ P:A\to\ast\quad对(6)和(7)用weak$

$(11)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ P\ x:\ast\quad对(10)和(9)用(appl)$

我们可以构造一个“真正”的体里有变量$x$出现的依值类型$\Pi x:A.P\ x$：

$(12)\quad A:\ast,\ P:A\to\ast\ \vdash\ \Pi x:A.P\ x\quad对(7)和(11)用(form)$

我们可以证明$P\ x\to P\ x$也是可派生的，然后构造另一个$\Pi x:A.P\ x\to P\ x$.

$(13)\quad A:\ast,\ P:A\to\ast,\ x:A,\ y:P\ x\ \vdash\ P\ x:\ast\quad对(11)和(11)用(weak)$

$(14)\quad A:\ast,\ P:A\to\ast,\ x:A\ \vdash\ P\ x\to P\ x:\ast\quad对(11)和(13)用(form)$

$(15)\quad A:\ast,\ P:A\to\ast\ \vdash\ \Pi x:A.P\ x\to P\ x:\ast\quad对(7)和(14)用(form)$

最后我们可以得到$\Pi x:A.P\ x\to P\ x$类型下有项：

$(16)\quad A:\ast,\ P:A\to\ast,\ x:A,\ y:P\ x\ \vdash\ y:P\ x\quad对(11)用(var)$

$(17)\quad A:\ast,\ P:A\to\ast,\ x:A\ x\ \vdash\ \lambda y:P\ x.y:P\ x\to P\ x\quad对(16)和(14)用(abst)$

$(18)\quad A:\ast,\ P:A\to\ast\ \vdash\ \lambda x:A.\lambda y:P\ x.y:\Pi x:A.P\ x\to P\ x\quad对(17)和(15)用(abst)$

综上，我们得到了：

1. 良类型性：$\lambda x:A.\lambda y:P\ x.y$是良类型的.
2. 类型检查：检查了$A:\ast,\ P:A\to\ast\ \vdash\ \lambda x:A.\lambda y:P\ x.y:\Pi x:A.P\ x\to P\ x$
3. 项的寻找：找到了$\Pi x:A.P\ x\to P\ x$类型在上下文$A:\ast,\ P:A\to\ast$中的项.

## $\lambda{\rm P}$中的最小谓词逻辑

$\lambda{\rm P}$可以编码一个称为**最小谓词逻辑**（minimal predicate logic）的简单逻辑系统，它的逻辑操作只有**蕴含**（implication）和**全称量化**（universal quantification）. 这一谓词逻辑的基本实体有**命题**（propositions）、**集合**（sets）和**集合上的谓词**（predicates over sets）.

如前文所说，一个类型系统有PAT解释：

- 如果项$b$有类型$B$（即$b:B$），$B$解释为一个命题，则$b$可以解释为$B$的一个**证明**. 这样的项$b$在类型论中称为**证明对象**（proof object）.
- 而当命题$B$不存在居留元（没有$b$使得$b:B$），则$B$不存在证明，$B$为**假**.

### I. 集合

我们将一个集合$S$编码成一个类型，即$S:\ast$，集合的元素是项. 所以如果$a$是$S$的元素，则$a:S$，例如：

$nat:\ast,\ nat\to nat:\ast;\quad 3:nat,\ \lambda n:nat.n:nat\to nat$

### II. 命题

我们把命题也编码成类型. 所以如果$A$是命题，则$A:\ast$. 根据PAT-解释，这个$A$的居留元$p$编码了一个$A$的证明. 

### III. 谓词

一个谓词$P$是从一个集合$S$到所有命题集合的一个函数. 所以$P:S\to\ast$. 

如果$P$是$S$上的一个任意的谓词，即$P:S\to\ast$，则对每个$a:S$，都有$P\ a:\ast$. 所有的$P\ a$都是命题，即类型（level 2），所以每个$P\ a$都可能有居留元. 

- 如果$P\ a$下有居留元，即存在$t$使得$t:P\ a$，则这个谓词对$a$成立.
- 如果$P\ b$下没有居留元，则这个谓词对$b$不成立.

### IV. 蕴含

使用PAT-解释，我们可以把$\Rightarrow$编码成$\to$：

- $A\Rightarrow B$为真.
- 如果$A$为真，则$B$也为真.
- 如果$A$有居留元，则$B$也有居留元.
- 存在函数将$A$的居留元映射到$B$的居留元.
- 存在$f$使得$f:A\to B$.
- $A\to B$有居留元.

所以$A\Rightarrow B$和$A\to B$有居留元等价. 

我们可以通过$(appl)$-规则和$\Rightarrow$-消去、$(abst)$-规则和$\Rightarrow$-引入的对应关系免费获得蕴含的构造规则和消去规则. 

### V. 全称量化

考虑对于集合$S$上某个依赖于$x$的谓词$P$的全称量化$\forall_{x\in S}(P(x))$. 

- $\forall_{x\in S}(P(x))$为真.
- 对集合$S$中任意的$x$，命题$P(x)$为真.
- 对集合$S$中任意的$x$，类型$P\ x$下有居留元.
- 存在一个将每一个$S$中的$x$映射到$P\ x$ 居留元的函数（这个函数的类型是$\Pi x:X.P\ x$）.
- 存在$f$使得$f:\Pi x:S.P\ x$.
- $\Pi x:S.P\ x$有居留元.

与蕴含类似，我们将全称量化$\forall_{x\in S}(P(x))$编码为$\Pi$-类型$\Pi x:S.P\ x$.

同样地，$\forall$的构造和消去规则也可以看做$\lambda{\rm P}$中$(appl)$-和$(abst)$-规则的特例.

