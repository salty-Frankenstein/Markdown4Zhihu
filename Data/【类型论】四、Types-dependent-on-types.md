---
title: 【类型论】四、Types dependent on types
date: 2021-03-22 19:00:00
categories: 小课堂
tags:
     - 函数式
     - 类型论
     - 教程
---

本文为*Type Theory and Formal Proof : An Introduction* 的笔记，纯个人向（

------
## 类型构造子

之前我们从*项*$\lambda x:\sigma.x$中由类型变量抽象出$\lambda \alpha:\ast.\lambda x:\alpha.x$. 类似的，我们也可以从*类型*上抽象. 如类型$\beta\to\beta,\ \gamma\to\gamma,\ (\gamma\to\beta)\to(\gamma\to\beta),\ \dots$，都有$\Diamond\to\Diamond$这样的结构.

我们引入一种表达式表示这个结构：$\lambda\alpha:\ast.\alpha\to\alpha$，它本身不是一个类型，但是一个*值*为类型的函数，因此称为**类型构造子**（type constructor）。喂给它东西，我们能得到类型：

$(\lambda\alpha:\ast.\alpha\to\alpha)\beta\qquad\to_\beta\quad\beta\to\beta$

$(\lambda\alpha:\ast.\alpha\to\alpha)\gamma\qquad\to_\beta\quad\gamma\to\gamma$

$(\lambda\alpha:\ast.\alpha\to\alpha)(\gamma\to\beta)\qquad\to_\beta\quad(\gamma\to\beta)\to(\gamma\to\beta)$

同理我们也可以构造$\lambda\alpha:\ast.\lambda\beta:\ast.\alpha\to\beta$.

那么，这些类型构造子的*类型*是什么呢？$\lambda\alpha:\ast.\alpha\to\alpha$是一个将$\alpha$映射到$\alpha\to\alpha$的函数，因为$\alpha:\ast$且$\alpha\to\alpha:\ast$，我们有：

$\lambda\alpha:\ast.\alpha\to\alpha\ :\ \ast\to\ast$. 因此我们需要一个“超类型”$\ast\to\ast$.

同理有：

$\lambda\alpha:\ast.\lambda\beta:\ast.\alpha\to\beta\ :\ \ast\to(\ast\to\ast)$.

这一推广称**依赖于类型的类型**（types depending on types），这一系统称$\lambda\underline\omega$，包括$\ast$和带箭头的$\ast$称**kind**. 所有kind的集合是：

$\mathbb{K=\ast\ \mid\ (K\to K)}$.

箭头的结合性与简单类型一致.

定义**所有kind的类型**（type of all kinds）记作$\square$，如$\ast:\square$、$\ast\to\ast:\square$等等. 

### 构造子，真构造子，sort（Constructor, proper constructor, sort）

1. 若$\kappa:\square$且$M:\kappa$则$M$是**构造子**（constructor），若$\kappa\not\equiv\ast$，则$M$是**真构造子**（proper constructor）.
2. **sort**的集合为$\lbrace\ast,\ \square\rbrace$.

我们保留符号$s$作为sort的元变量（即$s$表示$\ast$或$\square$）.

### Levels

level 1：项

level 2：构造子（即类型和真构造子）

level 3：kinds

level 4：即$\square$.

由此我们可以写出**推断链**（judgement chains）如$t:\sigma:\ast\to\ast$，甚至$t:\sigma:\ast\to\ast:\square$. 当$\sigma$是一个真构造子，则它下面没有值：$\sigma:\kappa:\square$，其中例如$\kappa\equiv\ast\to\ast$. 

## $\lambda\underline\omega$中的Sort规则和var规则

$\lambda\underline\omega$是$\lambda{\to}$的另一种推广：

- $\lambda2=\lambda{\to}$加上 依赖于类型的**项**（*terms*-depending-on-types）
- $\lambda\underline\omega=\lambda{\to}$加上 依赖于类型的**类型**（*types*-depending-on-types）

### Sort规则（Sort-rule）

$(sort)\quad\emptyset\ \vdash\ \ast\ :\ \square$.

接下来我们想要所有出现在上下文中的声明都是可以从这个上下文中派生的. 在$\lambda{\to}$和$\lambda2$中，我们使用$(var)$规则. 在$\lambda\underline{\omega}$中，我们要结合上下文的声明和构造的可派生性. 这是因为$\lambda\underline{\omega}$的类型更加复杂，我们需要确保类型都是良形式的, 此时一个类型的推断与否不再是由一个外在的集合，而是由推断和它的上下文自身决定. 在当前的类型系统下的要求更严格一些，我们要求出现在推断中的类型必须都能被形式地派生出来.

因此，只有在$A$类型可以被推断的时候，我们可以用一个声明$x:A$扩展一个上下文，且可以被推断的类型可以出现在level 2或者3上，也就是一个类型或者kind. 由此得到：
### Var规则（Var-rule）

$(var)\quad\dfrac{\Gamma\ \vdash\ A:s}{\Gamma,\ x:A\ \vdash\ x:A}$，若$x\notin \Gamma$.

**前提**是$A$为type（$s\equiv\ast$）或kind（$s\equiv\square$）. $x$既可能是个项变量，也可能是个类型变量. $(var)$规则允许我们由声明$x:A$延伸上下文$\Gamma$，并将他作为这个延伸上下文的陈述.

现在的问题是我们仅允许上下文的最后一个声明作派生，但：

$(?_1)\ \alpha:\ast,\ x:\alpha\ \vdash\ \alpha:\ast$

$(?_2)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \alpha:\ast$

这些暂时是无法派生的，甚至：

$(?_3)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \beta:\ast$

也不行，因为我们还不能得到$（?_3）$需要的前提

$(?_4)\ \alpha:\ast\ \vdash\ \ast:\square$

因此我们引入：

## $\lambda\underline\omega$弱化规则（weakening rule）

### 弱化规则（Weakening rule）

$(weak)\ \dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ C:s}{\Gamma,\ x:C\ \vdash\ A:B}$，若$x\notin\Gamma$.

如果我们派生出$\Gamma\ \vdash\ A:B$这个推断（第一个前提），那么我们可以通过在这个上下文$\Gamma$的末尾增加任意的一条声明将其弱化.

弱化规则对上下文的扩展只允许在最后，可以证明任意的扩展也都是可以的，也就是说Thinning Lemma对$\lambda\underline\omega$也成立.

这样$(?_1)$就可以这样派生：

$\dfrac{\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square}{(2)\ \alpha:\ast\ \vdash\ \alpha:\ast}(var)\qquad\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square}{(2)\ \alpha:\ast\ \vdash\ \alpha:\ast}(var)}{(4)\ \alpha:\ast,\ x:\alpha\ \vdash\ \alpha:\ast}(weak)$

$(?_2)$和$(?_4)$的派生如下：

$\dfrac{\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square}{(2)\ \alpha:\ast\ \vdash\ \alpha:\ast}(var)\qquad\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square\quad(1)\ \emptyset\ \vdash\ \ast:\square}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}(weak)}{(6)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \alpha:\ast}(weak)$

$(?_3)$：

$\dfrac{\dfrac{(1)\ \emptyset\ \vdash\ \ast：\square\quad(1)\ \emptyset\ \vdash\ \ast:\square}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}(weak)}{(7)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \beta:\ast}(var)$

## $\lambda\underline\omega$的形成规则（Formation rule）

在$\lambda 2$中，基于$\lambda 2$类型$\mathbb{T}2$，我们有$(form)$规则来构造上下文中的类型. 同样的，对于更加复杂的$\lambda\underline{\omega}$，我们需要一个真的有前提有结论的派生规则来构造类型.

### 形成规则（Formation rule）

$(form)\ \dfrac{\Gamma\ \vdash\ A:s\quad\Gamma\ \vdash\ B:s}{\Gamma\ \vdash\ A\to B:s}$

这包含了所有的types和kinds. （注意到$\lambda\underline{\omega}$中没有$\Pi$-类型）

例如：

对于$s\equiv\ast$：

$\dfrac{\dfrac{\cdots}{(6)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \alpha:\ast}\quad\dfrac{\cdots}{(7)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \beta:\ast}}{(8)\ \alpha:\ast,\ \beta:\ast\ \vdash \alpha \to\beta :\ast}(form)$

对于$s\equiv\square$：

$\dfrac{\dfrac{\cdots}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}\quad\dfrac{\cdots}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}}{(9)\ \alpha:\ast\ \vdash\ \ast\to\ast:\square}(form)$

## $\lambda\underline\omega$的应用和抽象规则（Application and abstraction rules）
$(appl)\ \dfrac{\Gamma\ \vdash\ M:A\to B\quad\Gamma\ \vdash\ N:A}{\Gamma\ \vdash\ M\ N:B}$

$(abst)\ \dfrac{\Gamma,\ x:A\ \vdash\ M:B\quad\Gamma\ \vdash\ A\to B:s}{\Gamma\ \vdash\ \lambda x:A.\ M:A\to B}$  

不同的是，在抽象规则中必须保证$A\to B$是一个良形式的类型.

在引入$\lambda\underline{\omega}$的$\beta$-归约之前，先引入下例的派生：

$(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta\quad\to_\beta\quad\beta\to\beta$

对于左边：

$(10)\quad\beta:\ast\ \vdash\ \ast:\square\quad对(1)和(1)用(weak)$

$(11)\quad\beta:\ast,\ \alpha:\ast\ \vdash\ \alpha:\ast\quad对(10)用(var)$

$(12)\quad\beta:\ast,\ \alpha:\ast\ \vdash\ \alpha\to\alpha:\ast\quad对(11)和(11)用(form)$

$(13)\quad\beta:\ast\ \vdash\ \ast\to\ast:\square\quad对(10)和(10)用(form)$

$(14)\quad\beta:\ast\ \vdash\ \lambda\alpha:\ast.\ \alpha\to\alpha:\ast\to\ast\quad对(12)和(13)用(abst)$

$(15)\quad\beta:\ast\ \vdash\ \beta:\ast\quad对(1)用(var)$

$(16)\quad\beta:\ast\ \vdash\ (\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta:\ast\quad对(14)和(15)用(appl)$

对于右边：

$(17)\quad\beta:\ast\ \vdash\ \beta\to\beta:\ast\quad对(15)和(15)用(form)$

## 替换规则（Conversion rules）
对于上面的例子，有

$\beta:\ast,\ x:(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta\ \vdash\ x:(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta$

我们想要得到：

$\beta:\ast,\ x:(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta\ \vdash\ x:\beta\to\beta$  

我们需要一个推广的$\beta$-替换，使得若$M:B$且$B=_\beta B'$，则$M:B'$（$B$和$B'$都是良形式的）.  
### 替换规则（Conversion rule）
$(conv)\ \dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ B':s}{\Gamma\ \vdash\ A:B'}\quad若B=_\beta B'$

第二个前提是必要的，考虑对任意$M$，$\beta \to \gamma =_\beta (\lambda\alpha: \ast.\ \beta\to\gamma)\ M$. 左边的$\beta\to\gamma$是良形式的，但当$M$没有$*$类型，右边的$(\lambda\alpha: \ast.\ \beta\to\gamma)\ M$就不是. 

例如：

$\dfrac{(18)\ \Gamma\ \vdash\ x:(\lambda \alpha: \ast .\ \alpha\to\alpha)\ \beta\quad(19)\ \Gamma\ \vdash\ \beta \to \beta:\ast}{(20)\ \Gamma\ \vdash\ x:\beta\to\beta}\ (conv)$

至此所有的$\lambda\underline{\omega}$的规则：

$$
(sort)&\ \emptyset\ \vdash\ \ast:\square\\
\ \\
(var)&\ \dfrac{\Gamma\ \vdash\ A:s}{\Gamma,\ x:A\ \vdash\ x:A}\quad若x\notin\Gamma \\
\ \\
(weak)&\ \dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ C:s}{\Gamma,\ x:C\ \vdash\ A:B}\quad若x\notin\Gamma\\
\ \\
(form)&\ \dfrac{\Gamma\ \vdash\ A:s\quad\Gamma\ \vdash\ B:s}{\Gamma\ \vdash\ A\to B:s}\\
\ \\
(appl)&\ \dfrac{\Gamma\ \vdash\ M:A\to B\quad \Gamma\ \vdash\ N:A}{\Gamma\ \vdash\ M\ N:B}\\
\ \\
(abst)&\ \dfrac{\Gamma,\ x:A\ \vdash\ M:B\quad\Gamma\ \vdash\ A\to\ B:s}{\Gamma\ \vdash\ \lambda x:A.\ M\ :\ A\to B}\\
\ \\
(conv)&\ \dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ B':s}{\Gamma\ \vdash\ A:B'}\quad若B=_\beta B'
$$

## $\lambda\underline{\omega}$的性质
$\lambda\underline{\omega}$系统满足之前系统的大部分性质，除了需要对类型唯一性作一些调整：类型不一定字面上唯一，但在替换意义上唯一.

### 替换上类型的唯一性

$若\Gamma\vdash A :B_1 且 \Gamma\vdash A:B_2，则B_1=_\beta B_2$.  

