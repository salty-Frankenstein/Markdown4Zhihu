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

之前我们从*项* <img src="https://www.zhihu.com/equation?tex=\lambda x:\sigma.x" alt="\lambda x:\sigma.x" class="ee_img tr_noresize" eeimg="1"> 中由类型变量抽象出 <img src="https://www.zhihu.com/equation?tex=\lambda \alpha:\ast.\lambda x:\alpha.x" alt="\lambda \alpha:\ast.\lambda x:\alpha.x" class="ee_img tr_noresize" eeimg="1"> . 类似的，我们也可以从*类型*上抽象. 如类型 <img src="https://www.zhihu.com/equation?tex=\beta\to\beta,\ \gamma\to\gamma,\ (\gamma\to\beta)\to(\gamma\to\beta),\ \dots" alt="\beta\to\beta,\ \gamma\to\gamma,\ (\gamma\to\beta)\to(\gamma\to\beta),\ \dots" class="ee_img tr_noresize" eeimg="1"> ，都有 <img src="https://www.zhihu.com/equation?tex=\Diamond\to\Diamond" alt="\Diamond\to\Diamond" class="ee_img tr_noresize" eeimg="1"> 这样的结构.

我们引入一种表达式表示这个结构： <img src="https://www.zhihu.com/equation?tex=\lambda\alpha:\ast.\alpha\to\alpha" alt="\lambda\alpha:\ast.\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> ，它本身不是一个类型，但是一个*值*为类型的函数，因此称为**类型构造子**（type constructor）。喂给它东西，我们能得到类型：

 <img src="https://www.zhihu.com/equation?tex=(\lambda\alpha:\ast.\alpha\to\alpha)\beta\qquad\to_\beta\quad\beta\to\beta" alt="(\lambda\alpha:\ast.\alpha\to\alpha)\beta\qquad\to_\beta\quad\beta\to\beta" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(\lambda\alpha:\ast.\alpha\to\alpha)\gamma\qquad\to_\beta\quad\gamma\to\gamma" alt="(\lambda\alpha:\ast.\alpha\to\alpha)\gamma\qquad\to_\beta\quad\gamma\to\gamma" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(\lambda\alpha:\ast.\alpha\to\alpha)(\gamma\to\beta)\qquad\to_\beta\quad(\gamma\to\beta)\to(\gamma\to\beta)" alt="(\lambda\alpha:\ast.\alpha\to\alpha)(\gamma\to\beta)\qquad\to_\beta\quad(\gamma\to\beta)\to(\gamma\to\beta)" class="ee_img tr_noresize" eeimg="1"> 

同理我们也可以构造 <img src="https://www.zhihu.com/equation?tex=\lambda\alpha:\ast.\lambda\beta:\ast.\alpha\to\beta" alt="\lambda\alpha:\ast.\lambda\beta:\ast.\alpha\to\beta" class="ee_img tr_noresize" eeimg="1"> .

那么，这些类型构造子的*类型*是什么呢？ <img src="https://www.zhihu.com/equation?tex=\lambda\alpha:\ast.\alpha\to\alpha" alt="\lambda\alpha:\ast.\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> 是一个将 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> 映射到 <img src="https://www.zhihu.com/equation?tex=\alpha\to\alpha" alt="\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> 的函数，因为 <img src="https://www.zhihu.com/equation?tex=\alpha:\ast" alt="\alpha:\ast" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\alpha\to\alpha:\ast" alt="\alpha\to\alpha:\ast" class="ee_img tr_noresize" eeimg="1"> ，我们有：

 <img src="https://www.zhihu.com/equation?tex=\lambda\alpha:\ast.\alpha\to\alpha\ :\ \ast\to\ast" alt="\lambda\alpha:\ast.\alpha\to\alpha\ :\ \ast\to\ast" class="ee_img tr_noresize" eeimg="1"> . 因此我们需要一个“超类型” <img src="https://www.zhihu.com/equation?tex=\ast\to\ast" alt="\ast\to\ast" class="ee_img tr_noresize" eeimg="1"> .

同理有：

 <img src="https://www.zhihu.com/equation?tex=\lambda\alpha:\ast.\lambda\beta:\ast.\alpha\to\beta\ :\ \ast\to(\ast\to\ast)" alt="\lambda\alpha:\ast.\lambda\beta:\ast.\alpha\to\beta\ :\ \ast\to(\ast\to\ast)" class="ee_img tr_noresize" eeimg="1"> .

这一推广称**依赖于类型的类型**（types depending on types），这一系统称 <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> ，包括 <img src="https://www.zhihu.com/equation?tex=\ast" alt="\ast" class="ee_img tr_noresize" eeimg="1"> 和带箭头的 <img src="https://www.zhihu.com/equation?tex=\ast" alt="\ast" class="ee_img tr_noresize" eeimg="1"> 称**kind**. 所有kind的集合是：

 <img src="https://www.zhihu.com/equation?tex=\mathbb{K=\ast\ \mid\ (K\to K)}" alt="\mathbb{K=\ast\ \mid\ (K\to K)}" class="ee_img tr_noresize" eeimg="1"> .

箭头的结合性与简单类型一致.

定义**所有kind的类型**（type of all kinds）记作 <img src="https://www.zhihu.com/equation?tex=\square" alt="\square" class="ee_img tr_noresize" eeimg="1"> ，如 <img src="https://www.zhihu.com/equation?tex=\ast:\square" alt="\ast:\square" class="ee_img tr_noresize" eeimg="1"> 、 <img src="https://www.zhihu.com/equation?tex=\ast\to\ast:\square" alt="\ast\to\ast:\square" class="ee_img tr_noresize" eeimg="1"> 等等. 

### 构造子，真构造子，sort（Constructor, proper constructor, sort）

1. 若 <img src="https://www.zhihu.com/equation?tex=\kappa:\square" alt="\kappa:\square" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=M:\kappa" alt="M:\kappa" class="ee_img tr_noresize" eeimg="1"> 则 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 是**构造子**（constructor），若 <img src="https://www.zhihu.com/equation?tex=\kappa\not\equiv\ast" alt="\kappa\not\equiv\ast" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 是**真构造子**（proper constructor）.
2. **sort**的集合为 <img src="https://www.zhihu.com/equation?tex=\lbrace\ast,\ \square\rbrace" alt="\lbrace\ast,\ \square\rbrace" class="ee_img tr_noresize" eeimg="1"> .

我们保留符号 <img src="https://www.zhihu.com/equation?tex=s" alt="s" class="ee_img tr_noresize" eeimg="1"> 作为sort的元变量（即 <img src="https://www.zhihu.com/equation?tex=s" alt="s" class="ee_img tr_noresize" eeimg="1"> 表示 <img src="https://www.zhihu.com/equation?tex=\ast" alt="\ast" class="ee_img tr_noresize" eeimg="1"> 或 <img src="https://www.zhihu.com/equation?tex=\square" alt="\square" class="ee_img tr_noresize" eeimg="1"> ）.

### Levels

level 1：项

level 2：构造子（即类型和真构造子）

level 3：kinds

level 4：即 <img src="https://www.zhihu.com/equation?tex=\square" alt="\square" class="ee_img tr_noresize" eeimg="1"> .

由此我们可以写出**推断链**（judgement chains）如 <img src="https://www.zhihu.com/equation?tex=t:\sigma:\ast\to\ast" alt="t:\sigma:\ast\to\ast" class="ee_img tr_noresize" eeimg="1"> ，甚至 <img src="https://www.zhihu.com/equation?tex=t:\sigma:\ast\to\ast:\square" alt="t:\sigma:\ast\to\ast:\square" class="ee_img tr_noresize" eeimg="1"> . 当 <img src="https://www.zhihu.com/equation?tex=\sigma" alt="\sigma" class="ee_img tr_noresize" eeimg="1"> 是一个真构造子，则它下面没有值： <img src="https://www.zhihu.com/equation?tex=\sigma:\kappa:\square" alt="\sigma:\kappa:\square" class="ee_img tr_noresize" eeimg="1"> ，其中例如 <img src="https://www.zhihu.com/equation?tex=\kappa\equiv\ast\to\ast" alt="\kappa\equiv\ast\to\ast" class="ee_img tr_noresize" eeimg="1"> . 

##  <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> 中的Sort规则和var规则

 <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 的另一种推广：

-  <img src="https://www.zhihu.com/equation?tex=\lambda2=\lambda{\to}" alt="\lambda2=\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 加上 依赖于类型的**项**（*terms*-depending-on-types）
-  <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega=\lambda{\to}" alt="\lambda\underline\omega=\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 加上 依赖于类型的**类型**（*types*-depending-on-types）

### Sort规则（Sort-rule）

 <img src="https://www.zhihu.com/equation?tex=(sort)\quad\emptyset\ \vdash\ \ast\ :\ \square" alt="(sort)\quad\emptyset\ \vdash\ \ast\ :\ \square" class="ee_img tr_noresize" eeimg="1"> .

接下来我们想要所有出现在上下文中的声明都是可以从这个上下文中派生的. 在 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 中，我们使用 <img src="https://www.zhihu.com/equation?tex=(var)" alt="(var)" class="ee_img tr_noresize" eeimg="1"> 规则. 在 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 中，我们要结合上下文的声明和构造的可派生性. 这是因为 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 的类型更加复杂，我们需要确保类型都是良形式的, 此时一个类型的推断与否不再是由一个外在的集合，而是由推断和它的上下文自身决定. 在当前的类型系统下的要求更严格一些，我们要求出现在推断中的类型必须都能被形式地派生出来.

因此，只有在 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 类型可以被推断的时候，我们可以用一个声明 <img src="https://www.zhihu.com/equation?tex=x:A" alt="x:A" class="ee_img tr_noresize" eeimg="1"> 扩展一个上下文，且可以被推断的类型可以出现在level 2或者3上，也就是一个类型或者kind. 由此得到：
### Var规则（Var-rule）

 <img src="https://www.zhihu.com/equation?tex=(var)\quad\dfrac{\Gamma\ \vdash\ A:s}{\Gamma,\ x:A\ \vdash\ x:A}" alt="(var)\quad\dfrac{\Gamma\ \vdash\ A:s}{\Gamma,\ x:A\ \vdash\ x:A}" class="ee_img tr_noresize" eeimg="1"> ，若 <img src="https://www.zhihu.com/equation?tex=x\notin \Gamma" alt="x\notin \Gamma" class="ee_img tr_noresize" eeimg="1"> .

**前提**是 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 为type（ <img src="https://www.zhihu.com/equation?tex=s\equiv\ast" alt="s\equiv\ast" class="ee_img tr_noresize" eeimg="1"> ）或kind（ <img src="https://www.zhihu.com/equation?tex=s\equiv\square" alt="s\equiv\square" class="ee_img tr_noresize" eeimg="1"> ）.  <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 既可能是个项变量，也可能是个类型变量.  <img src="https://www.zhihu.com/equation?tex=(var)" alt="(var)" class="ee_img tr_noresize" eeimg="1"> 规则允许我们由声明 <img src="https://www.zhihu.com/equation?tex=x:A" alt="x:A" class="ee_img tr_noresize" eeimg="1"> 延伸上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> ，并将他作为这个延伸上下文的陈述.

现在的问题是我们仅允许上下文的最后一个声明作派生，但：

 <img src="https://www.zhihu.com/equation?tex=(?_1)\ \alpha:\ast,\ x:\alpha\ \vdash\ \alpha:\ast" alt="(?_1)\ \alpha:\ast,\ x:\alpha\ \vdash\ \alpha:\ast" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(?_2)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \alpha:\ast" alt="(?_2)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \alpha:\ast" class="ee_img tr_noresize" eeimg="1"> 

这些暂时是无法派生的，甚至：

 <img src="https://www.zhihu.com/equation?tex=(?_3)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \beta:\ast" alt="(?_3)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \beta:\ast" class="ee_img tr_noresize" eeimg="1"> 

也不行，因为我们还不能得到 <img src="https://www.zhihu.com/equation?tex=（?_3）" alt="（?_3）" class="ee_img tr_noresize" eeimg="1"> 需要的前提

 <img src="https://www.zhihu.com/equation?tex=(?_4)\ \alpha:\ast\ \vdash\ \ast:\square" alt="(?_4)\ \alpha:\ast\ \vdash\ \ast:\square" class="ee_img tr_noresize" eeimg="1"> 

因此我们引入：

##  <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> 弱化规则（weakening rule）

### 弱化规则（Weakening rule）

 <img src="https://www.zhihu.com/equation?tex=(weak)\ \dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ C:s}{\Gamma,\ x:C\ \vdash\ A:B}" alt="(weak)\ \dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ C:s}{\Gamma,\ x:C\ \vdash\ A:B}" class="ee_img tr_noresize" eeimg="1"> ，若 <img src="https://www.zhihu.com/equation?tex=x\notin\Gamma" alt="x\notin\Gamma" class="ee_img tr_noresize" eeimg="1"> .

如果我们派生出 <img src="https://www.zhihu.com/equation?tex=\Gamma\ \vdash\ A:B" alt="\Gamma\ \vdash\ A:B" class="ee_img tr_noresize" eeimg="1"> 这个推断（第一个前提），那么我们可以通过在这个上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 的末尾增加任意的一条声明将其弱化.

弱化规则对上下文的扩展只允许在最后，可以证明任意的扩展也都是可以的，也就是说Thinning Lemma对 <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> 也成立.

这样 <img src="https://www.zhihu.com/equation?tex=(?_1)" alt="(?_1)" class="ee_img tr_noresize" eeimg="1"> 就可以这样派生：

 <img src="https://www.zhihu.com/equation?tex=\dfrac{\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square}{(2)\ \alpha:\ast\ \vdash\ \alpha:\ast}(var)\qquad\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square}{(2)\ \alpha:\ast\ \vdash\ \alpha:\ast}(var)}{(4)\ \alpha:\ast,\ x:\alpha\ \vdash\ \alpha:\ast}(weak)" alt="\dfrac{\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square}{(2)\ \alpha:\ast\ \vdash\ \alpha:\ast}(var)\qquad\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square}{(2)\ \alpha:\ast\ \vdash\ \alpha:\ast}(var)}{(4)\ \alpha:\ast,\ x:\alpha\ \vdash\ \alpha:\ast}(weak)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(?_2)" alt="(?_2)" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=(?_4)" alt="(?_4)" class="ee_img tr_noresize" eeimg="1"> 的派生如下：

 <img src="https://www.zhihu.com/equation?tex=\dfrac{\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square}{(2)\ \alpha:\ast\ \vdash\ \alpha:\ast}(var)\qquad\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square\quad(1)\ \emptyset\ \vdash\ \ast:\square}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}(weak)}{(6)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \alpha:\ast}(weak)" alt="\dfrac{\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square}{(2)\ \alpha:\ast\ \vdash\ \alpha:\ast}(var)\qquad\dfrac{(1)\ \emptyset\ \vdash\ \ast:\square\quad(1)\ \emptyset\ \vdash\ \ast:\square}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}(weak)}{(6)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \alpha:\ast}(weak)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(?_3)" alt="(?_3)" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=\dfrac{\dfrac{(1)\ \emptyset\ \vdash\ \ast：\square\quad(1)\ \emptyset\ \vdash\ \ast:\square}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}(weak)}{(7)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \beta:\ast}(var)" alt="\dfrac{\dfrac{(1)\ \emptyset\ \vdash\ \ast：\square\quad(1)\ \emptyset\ \vdash\ \ast:\square}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}(weak)}{(7)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \beta:\ast}(var)" class="ee_img tr_noresize" eeimg="1"> 

##  <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> 的形成规则（Formation rule）

在 <img src="https://www.zhihu.com/equation?tex=\lambda 2" alt="\lambda 2" class="ee_img tr_noresize" eeimg="1"> 中，基于 <img src="https://www.zhihu.com/equation?tex=\lambda 2" alt="\lambda 2" class="ee_img tr_noresize" eeimg="1"> 类型 <img src="https://www.zhihu.com/equation?tex=\mathbb{T}2" alt="\mathbb{T}2" class="ee_img tr_noresize" eeimg="1"> ，我们有 <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> 规则来构造上下文中的类型. 同样的，对于更加复杂的 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> ，我们需要一个真的有前提有结论的派生规则来构造类型.

### 形成规则（Formation rule）

 <img src="https://www.zhihu.com/equation?tex=(form)\ \dfrac{\Gamma\ \vdash\ A:s\quad\Gamma\ \vdash\ B:s}{\Gamma\ \vdash\ A\to B:s}" alt="(form)\ \dfrac{\Gamma\ \vdash\ A:s\quad\Gamma\ \vdash\ B:s}{\Gamma\ \vdash\ A\to B:s}" class="ee_img tr_noresize" eeimg="1"> 

这包含了所有的types和kinds. （注意到 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 中没有 <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> -类型）

例如：

对于 <img src="https://www.zhihu.com/equation?tex=s\equiv\ast" alt="s\equiv\ast" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=\dfrac{\dfrac{\cdots}{(6)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \alpha:\ast}\quad\dfrac{\cdots}{(7)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \beta:\ast}}{(8)\ \alpha:\ast,\ \beta:\ast\ \vdash \alpha \to\beta :\ast}(form)" alt="\dfrac{\dfrac{\cdots}{(6)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \alpha:\ast}\quad\dfrac{\cdots}{(7)\ \alpha:\ast,\ \beta:\ast\ \vdash\ \beta:\ast}}{(8)\ \alpha:\ast,\ \beta:\ast\ \vdash \alpha \to\beta :\ast}(form)" class="ee_img tr_noresize" eeimg="1"> 

对于 <img src="https://www.zhihu.com/equation?tex=s\equiv\square" alt="s\equiv\square" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=\dfrac{\dfrac{\cdots}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}\quad\dfrac{\cdots}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}}{(9)\ \alpha:\ast\ \vdash\ \ast\to\ast:\square}(form)" alt="\dfrac{\dfrac{\cdots}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}\quad\dfrac{\cdots}{(5)\ \alpha:\ast\ \vdash\ \ast:\square}}{(9)\ \alpha:\ast\ \vdash\ \ast\to\ast:\square}(form)" class="ee_img tr_noresize" eeimg="1"> 

##  <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> 的应用和抽象规则（Application and abstraction rules）
 <img src="https://www.zhihu.com/equation?tex=(appl)\ \dfrac{\Gamma\ \vdash\ M:A\to B\quad\Gamma\ \vdash\ N:A}{\Gamma\ \vdash\ M\ N:B}" alt="(appl)\ \dfrac{\Gamma\ \vdash\ M:A\to B\quad\Gamma\ \vdash\ N:A}{\Gamma\ \vdash\ M\ N:B}" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(abst)\ \dfrac{\Gamma,\ x:A\ \vdash\ M:B\quad\Gamma\ \vdash\ A\to B:s}{\Gamma\ \vdash\ \lambda x:A.\ M:A\to B}" alt="(abst)\ \dfrac{\Gamma,\ x:A\ \vdash\ M:B\quad\Gamma\ \vdash\ A\to B:s}{\Gamma\ \vdash\ \lambda x:A.\ M:A\to B}" class="ee_img tr_noresize" eeimg="1">   

不同的是，在抽象规则中必须保证 <img src="https://www.zhihu.com/equation?tex=A\to B" alt="A\to B" class="ee_img tr_noresize" eeimg="1"> 是一个良形式的类型.

在引入 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 的 <img src="https://www.zhihu.com/equation?tex=\beta" alt="\beta" class="ee_img tr_noresize" eeimg="1"> -归约之前，先引入下例的派生：

 <img src="https://www.zhihu.com/equation?tex=(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta\quad\to_\beta\quad\beta\to\beta" alt="(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta\quad\to_\beta\quad\beta\to\beta" class="ee_img tr_noresize" eeimg="1"> 

对于左边：

 <img src="https://www.zhihu.com/equation?tex=(10)\quad\beta:\ast\ \vdash\ \ast:\square\quad对(1)和(1)用(weak)" alt="(10)\quad\beta:\ast\ \vdash\ \ast:\square\quad对(1)和(1)用(weak)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(11)\quad\beta:\ast,\ \alpha:\ast\ \vdash\ \alpha:\ast\quad对(10)用(var)" alt="(11)\quad\beta:\ast,\ \alpha:\ast\ \vdash\ \alpha:\ast\quad对(10)用(var)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(12)\quad\beta:\ast,\ \alpha:\ast\ \vdash\ \alpha\to\alpha:\ast\quad对(11)和(11)用(form)" alt="(12)\quad\beta:\ast,\ \alpha:\ast\ \vdash\ \alpha\to\alpha:\ast\quad对(11)和(11)用(form)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(13)\quad\beta:\ast\ \vdash\ \ast\to\ast:\square\quad对(10)和(10)用(form)" alt="(13)\quad\beta:\ast\ \vdash\ \ast\to\ast:\square\quad对(10)和(10)用(form)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(14)\quad\beta:\ast\ \vdash\ \lambda\alpha:\ast.\ \alpha\to\alpha:\ast\to\ast\quad对(12)和(13)用(abst)" alt="(14)\quad\beta:\ast\ \vdash\ \lambda\alpha:\ast.\ \alpha\to\alpha:\ast\to\ast\quad对(12)和(13)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(15)\quad\beta:\ast\ \vdash\ \beta:\ast\quad对(1)用(var)" alt="(15)\quad\beta:\ast\ \vdash\ \beta:\ast\quad对(1)用(var)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(16)\quad\beta:\ast\ \vdash\ (\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta:\ast\quad对(14)和(15)用(appl)" alt="(16)\quad\beta:\ast\ \vdash\ (\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta:\ast\quad对(14)和(15)用(appl)" class="ee_img tr_noresize" eeimg="1"> 

对于右边：

 <img src="https://www.zhihu.com/equation?tex=(17)\quad\beta:\ast\ \vdash\ \beta\to\beta:\ast\quad对(15)和(15)用(form)" alt="(17)\quad\beta:\ast\ \vdash\ \beta\to\beta:\ast\quad对(15)和(15)用(form)" class="ee_img tr_noresize" eeimg="1"> 

## 替换规则（Conversion rules）
对于上面的例子，有

 <img src="https://www.zhihu.com/equation?tex=\beta:\ast,\ x:(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta\ \vdash\ x:(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta" alt="\beta:\ast,\ x:(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta\ \vdash\ x:(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta" class="ee_img tr_noresize" eeimg="1"> 

我们想要得到：

 <img src="https://www.zhihu.com/equation?tex=\beta:\ast,\ x:(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta\ \vdash\ x:\beta\to\beta" alt="\beta:\ast,\ x:(\lambda\alpha:\ast.\ \alpha\to\alpha)\ \beta\ \vdash\ x:\beta\to\beta" class="ee_img tr_noresize" eeimg="1">   

我们需要一个推广的 <img src="https://www.zhihu.com/equation?tex=\beta" alt="\beta" class="ee_img tr_noresize" eeimg="1"> -替换，使得若 <img src="https://www.zhihu.com/equation?tex=M:B" alt="M:B" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=B=_\beta B'" alt="B=_\beta B'" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=M:B'" alt="M:B'" class="ee_img tr_noresize" eeimg="1"> （ <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=B'" alt="B'" class="ee_img tr_noresize" eeimg="1"> 都是良形式的）.  
### 替换规则（Conversion rule）
 <img src="https://www.zhihu.com/equation?tex=(conv)\ \dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ B':s}{\Gamma\ \vdash\ A:B'}\quad若B=_\beta B'" alt="(conv)\ \dfrac{\Gamma\ \vdash\ A:B\quad\Gamma\ \vdash\ B':s}{\Gamma\ \vdash\ A:B'}\quad若B=_\beta B'" class="ee_img tr_noresize" eeimg="1"> 

第二个前提是必要的，考虑对任意 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> ， <img src="https://www.zhihu.com/equation?tex=\beta \to \gamma =_\beta (\lambda\alpha: \ast.\ \beta\to\gamma)\ M" alt="\beta \to \gamma =_\beta (\lambda\alpha: \ast.\ \beta\to\gamma)\ M" class="ee_img tr_noresize" eeimg="1"> . 左边的 <img src="https://www.zhihu.com/equation?tex=\beta\to\gamma" alt="\beta\to\gamma" class="ee_img tr_noresize" eeimg="1"> 是良形式的，但当 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 没有 <img src="https://www.zhihu.com/equation?tex=*" alt="*" class="ee_img tr_noresize" eeimg="1"> 类型，右边的 <img src="https://www.zhihu.com/equation?tex=(\lambda\alpha: \ast.\ \beta\to\gamma)\ M" alt="(\lambda\alpha: \ast.\ \beta\to\gamma)\ M" class="ee_img tr_noresize" eeimg="1"> 就不是. 

例如：

 <img src="https://www.zhihu.com/equation?tex=\dfrac{(18)\ \Gamma\ \vdash\ x:(\lambda \alpha: \ast .\ \alpha\to\alpha)\ \beta\quad(19)\ \Gamma\ \vdash\ \beta \to \beta:\ast}{(20)\ \Gamma\ \vdash\ x:\beta\to\beta}\ (conv)" alt="\dfrac{(18)\ \Gamma\ \vdash\ x:(\lambda \alpha: \ast .\ \alpha\to\alpha)\ \beta\quad(19)\ \Gamma\ \vdash\ \beta \to \beta:\ast}{(20)\ \Gamma\ \vdash\ x:\beta\to\beta}\ (conv)" class="ee_img tr_noresize" eeimg="1"> 

至此所有的 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 的规则：


<img src="https://www.zhihu.com/equation?tex=\begin{align}
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
\end{align}
" alt="\begin{align}
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
\end{align}
" class="ee_img tr_noresize" eeimg="1">

##  <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 的性质
 <img src="https://www.zhihu.com/equation?tex=\lambda\underline{\omega}" alt="\lambda\underline{\omega}" class="ee_img tr_noresize" eeimg="1"> 系统满足之前系统的大部分性质，除了需要对类型唯一性作一些调整：类型不一定字面上唯一，但在替换意义上唯一.

### 替换上类型的唯一性

 <img src="https://www.zhihu.com/equation?tex=若\Gamma\vdash A :B_1 且 \Gamma\vdash A:B_2，则B_1=_\beta B_2" alt="若\Gamma\vdash A :B_1 且 \Gamma\vdash A:B_2，则B_1=_\beta B_2" class="ee_img tr_noresize" eeimg="1"> .  

