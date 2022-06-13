---
title: 【类型论】六、构造演算
date: 2022-03-01 15:14:09
categories: 小课堂
tags:
     - 函数式
     - 类型论
     - 教程
---

本文为*Type Theory and Formal Proof : An Introduction* 的笔记，纯个人向（

------

之前的类型系统包括了关于项和类型依赖关系的四种可能的组合，将它们结合起来就得到了 <img src="https://www.zhihu.com/equation?tex=\lambda {\rm C}" alt="\lambda {\rm C}" class="ee_img tr_noresize" eeimg="1"> ，称为**构造演算**（*Calculus of Constructions*），或者以它的发现者命名的  <img src="https://www.zhihu.com/equation?tex=\lambda\text{-Coquand}" alt="\lambda\text{-Coquand}" class="ee_img tr_noresize" eeimg="1"> （这也是Coq的neta）. 所以这个“C”有很多意思，比如它还可以是 <img src="https://www.zhihu.com/equation?tex=\lambda\text{-cube}" alt="\lambda\text{-cube}" class="ee_img tr_noresize" eeimg="1"> 的“c”. 

<!--more-->

技术上说， <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\lambda {\rm C}" alt="\lambda {\rm C}" class="ee_img tr_noresize" eeimg="1"> 之间只有一点不同，不过这足以把 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 拓展到 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm C}=\lambda{\rm 2}+\lambda \underline\omega +\lambda{\rm P}" alt="\lambda{\rm C}=\lambda{\rm 2}+\lambda \underline\omega +\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> . 不同点在形成规则 <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> 上，在 <img src="https://www.zhihu.com/equation?tex=\lambda {\rm P}" alt="\lambda {\rm P}" class="ee_img tr_noresize" eeimg="1"> 中是这样的：

<img src="https://www.zhihu.com/equation?tex=(form_{\lambda {\rm P}})\ \dfrac{\Gamma\ \vdash\ A:\ast\quad\Gamma,\ x:A\ \vdash\ B:s}{\Gamma\ \vdash\ \Pi x:A.\ B\ :\ s}
" alt="(form_{\lambda {\rm P}})\ \dfrac{\Gamma\ \vdash\ A:\ast\quad\Gamma,\ x:A\ \vdash\ B:s}{\Gamma\ \vdash\ \Pi x:A.\ B\ :\ s}
" class="ee_img tr_noresize" eeimg="1">

在 <img src="https://www.zhihu.com/equation?tex=\lambda {\rm P}" alt="\lambda {\rm P}" class="ee_img tr_noresize" eeimg="1"> 中这个规则的重点是：为了保证 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.\ B" alt="\Pi x:A.\ B" class="ee_img tr_noresize" eeimg="1"> 的居留元只能是项或者只依赖于*项*的类型（因为 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 是level 1的项），所以 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 的类型必须是 <img src="https://www.zhihu.com/equation?tex=\ast" alt="\ast" class="ee_img tr_noresize" eeimg="1"> 。但是当我们想要解除这个限制的时候，就刚好得到了我们想要的抽象：依赖与项或者*类型*的项和类型. 

这样就可以把 <img src="https://www.zhihu.com/equation?tex=A:\ast" alt="A:\ast" class="ee_img tr_noresize" eeimg="1"> 换成 <img src="https://www.zhihu.com/equation?tex=A:s" alt="A:s" class="ee_img tr_noresize" eeimg="1"> 了，得到 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm C}" alt="\lambda{\rm C}" class="ee_img tr_noresize" eeimg="1"> 的 <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> -规则：

<img src="https://www.zhihu.com/equation?tex=(form_{\lambda{\rm C}})\ \dfrac{\Gamma\ \vdash\ A:s_1\quad\Gamma,\ x:A\ \vdash\ B:s_2}{\Gamma\ \vdash\ \Pi x:A.\ B\ :\ s_2}
" alt="(form_{\lambda{\rm C}})\ \dfrac{\Gamma\ \vdash\ A:s_1\quad\Gamma,\ x:A\ \vdash\ B:s_2}{\Gamma\ \vdash\ \Pi x:A.\ B\ :\ s_2}
" class="ee_img tr_noresize" eeimg="1">

前提中 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 的 <img src="https://www.zhihu.com/equation?tex=s" alt="s" class="ee_img tr_noresize" eeimg="1"> 可以互不依赖（四种可能），而结论中的则是 <img src="https://www.zhihu.com/equation?tex=s_2" alt="s_2" class="ee_img tr_noresize" eeimg="1"> ，即 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 的类型，这可以理解因为：  
1. 从直觉上来说，如果 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 是个类型，那么抽象的（依赖）类型 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.\ B" alt="\Pi x:A.\ B" class="ee_img tr_noresize" eeimg="1"> 应该也是个类型；如果 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 是个kind，那么 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.\ B" alt="\Pi x:A.\ B" class="ee_img tr_noresize" eeimg="1"> 也应该是. （但这其实是不一定的，在一些更抽象的类型系统中， <img src="https://www.zhihu.com/equation?tex=\Pi x:A.\ B" alt="\Pi x:A.\ B" class="ee_img tr_noresize" eeimg="1"> 的类型可以和 <img src="https://www.zhihu.com/equation?tex=s_1" alt="s_1" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=s_2" alt="s_2" class="ee_img tr_noresize" eeimg="1"> 都不一样，这样的系统称为“**纯类型系统**”（*pure type systems，PTS*），其中它的类型变成了 <img src="https://www.zhihu.com/equation?tex=s_3" alt="s_3" class="ee_img tr_noresize" eeimg="1"> ，这样就形成了8种可能的组合 <img src="https://www.zhihu.com/equation?tex=(s_1,s_2,s_3)" alt="(s_1,s_2,s_3)" class="ee_img tr_noresize" eeimg="1"> ）.
2. 技术上说， <img src="https://www.zhihu.com/equation?tex=\lambda{\rm C}" alt="\lambda{\rm C}" class="ee_img tr_noresize" eeimg="1"> 的形成规则和 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm P}" alt="\lambda{\rm P}" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> 中对形成规则的形式是一致的. 

有了 <img src="https://www.zhihu.com/equation?tex=(form_{\lambda{\rm C}})" alt="(form_{\lambda{\rm C}})" class="ee_img tr_noresize" eeimg="1"> 规则，假设我们有一个函数 <img src="https://www.zhihu.com/equation?tex=\lambda x:A.\ b" alt="\lambda x:A.\ b" class="ee_img tr_noresize" eeimg="1"> ，由 <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> -规则得到它的类型为 <img src="https://www.zhihu.com/equation?tex=\Pi x:A.\ B" alt="\Pi x:A.\ B" class="ee_img tr_noresize" eeimg="1"> （那么 <img src="https://www.zhihu.com/equation?tex=b" alt="b" class="ee_img tr_noresize" eeimg="1"> 的类型也是 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> ），那么由形成规则 <img src="https://www.zhihu.com/equation?tex=A:s_1" alt="A:s_1" class="ee_img tr_noresize" eeimg="1"> ， <img src="https://www.zhihu.com/equation?tex=B:s_2" alt="B:s_2" class="ee_img tr_noresize" eeimg="1"> 有四种可能：

![2022-06-13 00-07-42 的屏幕截图](https://raw.githubusercontent.com/salty-Frankenstein/Markdown4Zhihu/master/Data/【类型论】六、构造演算/2022-06-13 00-07-42 的屏幕截图.png)

这四种可能在之前的四个类型系统中都可以实现，例如当 <img src="https://www.zhihu.com/equation?tex=(s_1,s_2)=(\square,\ast)" alt="(s_1,s_2)=(\square,\ast)" class="ee_img tr_noresize" eeimg="1"> ，对应 <img src="https://www.zhihu.com/equation?tex=\lambda 2" alt="\lambda 2" class="ee_img tr_noresize" eeimg="1"> 中依赖于类型的项.

##  <img src="https://www.zhihu.com/equation?tex=\lambda" alt="\lambda" class="ee_img tr_noresize" eeimg="1"> -立方体（ <img src="https://www.zhihu.com/equation?tex=\lambda\text{-cube}" alt="\lambda\text{-cube}" class="ee_img tr_noresize" eeimg="1"> ）

我们已经遇见过 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 这个最简单系统的三个拓展：

- 拓展依赖于类型的项： <img src="https://www.zhihu.com/equation?tex=\lambda 2" alt="\lambda 2" class="ee_img tr_noresize" eeimg="1"> 
- 拓展依赖于类型的类型： <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> 
- 拓展依赖于项的类型： <img src="https://www.zhihu.com/equation?tex=\lambda {\rm P}" alt="\lambda {\rm P}" class="ee_img tr_noresize" eeimg="1"> 

这三种可能性是互不依赖的，所以它们可以作为三个互相垂直的方向，得到一个类型系统的三维直角坐标：

![2022-06-13 00-18-53 的屏幕截图](https://raw.githubusercontent.com/salty-Frankenstein/Markdown4Zhihu/master/Data/【类型论】六、构造演算/2022-06-13 00-18-53 的屏幕截图.png)

结合这三种可能性就得到了上面提到的 <img src="https://www.zhihu.com/equation?tex=\lambda {\rm C}" alt="\lambda {\rm C}" class="ee_img tr_noresize" eeimg="1"> 。同样的，也可以将 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 结合其中的两个可能性，得到的系统分别为 <img src="https://www.zhihu.com/equation?tex=\lambda \omega" alt="\lambda \omega" class="ee_img tr_noresize" eeimg="1"> ， <img src="https://www.zhihu.com/equation?tex=\lambda {\rm P}2" alt="\lambda {\rm P}2" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\lambda {\rm P}\underline\omega" alt="\lambda {\rm P}\underline\omega" class="ee_img tr_noresize" eeimg="1"> . 这八个类型系统可以放在一个立方体上，也就是所谓的** <img src="https://www.zhihu.com/equation?tex=\lambda" alt="\lambda" class="ee_img tr_noresize" eeimg="1"> -立方体**（ <img src="https://www.zhihu.com/equation?tex=\lambda\text{-cube}" alt="\lambda\text{-cube}" class="ee_img tr_noresize" eeimg="1"> 或*Barendregt cube*）. 

![2022-06-13 00-34-08 的屏幕截图](https://raw.githubusercontent.com/salty-Frankenstein/Markdown4Zhihu/master/Data/【类型论】六、构造演算/2022-06-13 00-34-08 的屏幕截图.png)

![2022-06-13 00-34-13 的屏幕截图](https://raw.githubusercontent.com/salty-Frankenstein/Markdown4Zhihu/master/Data/【类型论】六、构造演算/2022-06-13 00-34-13 的屏幕截图.png)

Barendregt发现的最重要结论是这八个不同的类型系统可以只用一套简单的派生规则描述：除了三条初始规则（*initialisation rules*） <img src="https://www.zhihu.com/equation?tex=(sort)" alt="(sort)" class="ee_img tr_noresize" eeimg="1"> ， <img src="https://www.zhihu.com/equation?tex=(var)" alt="(var)" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=(weak)" alt="(weak)" class="ee_img tr_noresize" eeimg="1"> ，我们只需要对于 <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> 类型的形成规则 <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> ，替换规则 <img src="https://www.zhihu.com/equation?tex=(conv)" alt="(conv)" class="ee_img tr_noresize" eeimg="1"> 和每个lambda演算系统最重要的两条应用和抽象规则. 选择对应的 <img src="https://www.zhihu.com/equation?tex=(s_1,s_2)" alt="(s_1,s_2)" class="ee_img tr_noresize" eeimg="1"> ，就可以得到对应的类型系统：

![2022-06-13 00-36-24 的屏幕截图](https://raw.githubusercontent.com/salty-Frankenstein/Markdown4Zhihu/master/Data/【类型论】六、构造演算/2022-06-13 00-36-24 的屏幕截图.png)

##  <img src="https://www.zhihu.com/equation?tex=\lambda {\rm C}" alt="\lambda {\rm C}" class="ee_img tr_noresize" eeimg="1"> 的性质

**定义**  <img src="https://www.zhihu.com/equation?tex=\lambda{\rm C}" alt="\lambda{\rm C}" class="ee_img tr_noresize" eeimg="1"> 表达式集合 <img src="https://www.zhihu.com/equation?tex=\mathcal{E}" alt="\mathcal{E}" class="ee_img tr_noresize" eeimg="1"> 为

<img src="https://www.zhihu.com/equation?tex=\mathcal{E}=V\ |\ \square\ |\ \ast\ |\ (\mathcal{EE})\ |\ (\lambda V:\mathcal{E.E)}\ |\ (\Pi V:\mathcal{E.E})
" alt="\mathcal{E}=V\ |\ \square\ |\ \ast\ |\ (\mathcal{EE})\ |\ (\lambda V:\mathcal{E.E)}\ |\ (\Pi V:\mathcal{E.E})
" class="ee_img tr_noresize" eeimg="1">

### **自由变量引理** *（Free Variables Lemma）*

若 <img src="https://www.zhihu.com/equation?tex=\Gamma\ \vdash\ A:B" alt="\Gamma\ \vdash\ A:B" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=FV(A),FV(B)\subseteq {\rm dom}(\Gamma)" alt="FV(A),FV(B)\subseteq {\rm dom}(\Gamma)" class="ee_img tr_noresize" eeimg="1"> 



当一个上下文是一个可以派生的推断的一部分时，称它是**良形式的** *（well-formed）*. 

**定义** 上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 是良形式的，如果存在 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=\Gamma\ \vdash\ A:B" alt="\Gamma\ \vdash\ A:B" class="ee_img tr_noresize" eeimg="1"> .

### 引理*（Thinning, Permutation, Condensing）*

1. （Thinning）令 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 与 <img src="https://www.zhihu.com/equation?tex=\Gamma''" alt="\Gamma''" class="ee_img tr_noresize" eeimg="1"> 是上下文，使得 <img src="https://www.zhihu.com/equation?tex=\Gamma' \subseteq \Gamma''" alt="\Gamma' \subseteq \Gamma''" class="ee_img tr_noresize" eeimg="1"> . 若 <img src="https://www.zhihu.com/equation?tex=\Gamma' \vdash A:B" alt="\Gamma' \vdash A:B" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\Gamma''" alt="\Gamma''" class="ee_img tr_noresize" eeimg="1"> 是良形式的，则 <img src="https://www.zhihu.com/equation?tex=\Gamma'' \vdash A:B" alt="\Gamma'' \vdash A:B" class="ee_img tr_noresize" eeimg="1"> .
2. （Permutation）令 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 与 <img src="https://www.zhihu.com/equation?tex=\Gamma''" alt="\Gamma''" class="ee_img tr_noresize" eeimg="1"> 是上下文，使得 <img src="https://www.zhihu.com/equation?tex=\Gamma''" alt="\Gamma''" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 的一个permutation. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma' \vdash A:B" alt="\Gamma' \vdash A:B" class="ee_img tr_noresize" eeimg="1"> ，且 <img src="https://www.zhihu.com/equation?tex=\Gamma''" alt="\Gamma''" class="ee_img tr_noresize" eeimg="1"> 是良形式的，则 <img src="https://www.zhihu.com/equation?tex=\Gamma'' \vdash A:B" alt="\Gamma'' \vdash A:B" class="ee_img tr_noresize" eeimg="1"> .
3. （Condensing）若 <img src="https://www.zhihu.com/equation?tex=\Gamma',x:A,\Gamma''\ \vdash\ B:C" alt="\Gamma',x:A,\Gamma''\ \vdash\ B:C" class="ee_img tr_noresize" eeimg="1"> ，且 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 不在 <img src="https://www.zhihu.com/equation?tex=\Gamma''" alt="\Gamma''" class="ee_img tr_noresize" eeimg="1"> 、 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 或 <img src="https://www.zhihu.com/equation?tex=C" alt="C" class="ee_img tr_noresize" eeimg="1"> 中出现，则 <img src="https://www.zhihu.com/equation?tex=\Gamma,\Gamma''\vdash B:C" alt="\Gamma,\Gamma''\vdash B:C" class="ee_img tr_noresize" eeimg="1"> .

### 生成引理（Generation Lemma）

1. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash x:C" alt="\Gamma \vdash x:C" class="ee_img tr_noresize" eeimg="1"> ，则存在一个sort  <img src="https://www.zhihu.com/equation?tex=s" alt="s" class="ee_img tr_noresize" eeimg="1"> 和表达式 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=B=_\beta C" alt="B=_\beta C" class="ee_img tr_noresize" eeimg="1"> ， <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash B:s" alt="\Gamma\vdash B:s" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=x:B\in \Gamma" alt="x:B\in \Gamma" class="ee_img tr_noresize" eeimg="1"> .
2. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash MN:C" alt="\Gamma\vdash MN:C" class="ee_img tr_noresize" eeimg="1"> 则 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 有个 <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> 类型，即存在表达式 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash M:\Pi x:A.\ B" alt="\Gamma\vdash M:\Pi x:A.\ B" class="ee_img tr_noresize" eeimg="1"> ；进一步地， <img src="https://www.zhihu.com/equation?tex=N" alt="N" class="ee_img tr_noresize" eeimg="1"> 可以应用到这个 <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> 类型： <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash N:A" alt="\Gamma\vdash N:A" class="ee_img tr_noresize" eeimg="1"> ；最后，有 <img src="https://www.zhihu.com/equation?tex=C=_\beta B[x:=N]" alt="C=_\beta B[x:=N]" class="ee_img tr_noresize" eeimg="1"> .
3. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash \lambda x:A.\ b:C" alt="\Gamma\vdash \lambda x:A.\ b:C" class="ee_img tr_noresize" eeimg="1"> ，则存在一个sort  <img src="https://www.zhihu.com/equation?tex=s" alt="s" class="ee_img tr_noresize" eeimg="1"> 和表达式 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=C=_\beta \Pi x:A.\ B" alt="C=_\beta \Pi x:A.\ B" class="ee_img tr_noresize" eeimg="1"> ，其中 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash\Pi x:A.\ B:s" alt="\Gamma\vdash\Pi x:A.\ B:s" class="ee_img tr_noresize" eeimg="1"> 且进一步有 <img src="https://www.zhihu.com/equation?tex=\Gamma,x:A\vdash b:B" alt="\Gamma,x:A\vdash b:B" class="ee_img tr_noresize" eeimg="1"> . 
4. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash \Pi x:A.\ B:C" alt="\Gamma\vdash \Pi x:A.\ B:C" class="ee_img tr_noresize" eeimg="1"> ，则存在 <img src="https://www.zhihu.com/equation?tex=s_1" alt="s_1" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=s_2" alt="s_2" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=C\equiv s_2" alt="C\equiv s_2" class="ee_img tr_noresize" eeimg="1"> ，且进一步有 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash A:s_1" alt="\Gamma\vdash A:s_1" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\Gamma,x:A\vdash B:s_2" alt="\Gamma,x:A\vdash B:s_2" class="ee_img tr_noresize" eeimg="1"> .



**定义** 在 <img src="https://www.zhihu.com/equation?tex=\lambda {rm C}" alt="\lambda {rm C}" class="ee_img tr_noresize" eeimg="1"> 中一个表达式 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 是**合法的** *（legal）*，如果存在 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=N" alt="N" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash M:N" alt="\Gamma\vdash M:N" class="ee_img tr_noresize" eeimg="1"> 或 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash N:M" alt="\Gamma\vdash N:M" class="ee_img tr_noresize" eeimg="1"> （也就是不论 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 是可定型的还是可居留的）.

### 子表达式引理*（Subexpression Lemma）*

如果 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 是合法的，则所有 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 的子表达式是合法的.

### 替换上类型唯一性*（Uniqueness of Types up to Conversion）*

若 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash A:B_1" alt="\Gamma\vdash A:B_1" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash A:B_2" alt="\Gamma\vdash A:B_2" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=B_1=_\beta B_2" alt="B_1=_\beta B_2" class="ee_img tr_noresize" eeimg="1"> .

### 代换引理（Substitution Lemma）

令 <img src="https://www.zhihu.com/equation?tex=\Gamma',x:A,\Gamma''\vdash B:C" alt="\Gamma',x:A,\Gamma''\vdash B:C" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\Gamma'\vdash D:A" alt="\Gamma'\vdash D:A" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\Gamma',\Gamma''[x:=D]\vdash B[x:=D]:C[x:=D]" alt="\Gamma',\Gamma''[x:=D]\vdash B[x:=D]:C[x:=D]" class="ee_img tr_noresize" eeimg="1"> .

### Church-Rosser定理

Church-Rosser性质对 <img src="https://www.zhihu.com/equation?tex=\lambda{\rm C}" alt="\lambda{\rm C}" class="ee_img tr_noresize" eeimg="1"> 成立，即若 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 在 <img src="https://www.zhihu.com/equation?tex=\mathcal{E}" alt="\mathcal{E}" class="ee_img tr_noresize" eeimg="1"> 中， <img src="https://www.zhihu.com/equation?tex=M\twoheadrightarrow_\beta N_1" alt="M\twoheadrightarrow_\beta N_1" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=M\twoheadrightarrow_\beta N_2" alt="M\twoheadrightarrow_\beta N_2" class="ee_img tr_noresize" eeimg="1"> ，则存在 <img src="https://www.zhihu.com/equation?tex=N_3" alt="N_3" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=N_1 \twoheadrightarrow_\beta N_3" alt="N_1 \twoheadrightarrow_\beta N_3" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=N_2\twoheadrightarrow_\beta N_3" alt="N_2\twoheadrightarrow_\beta N_3" class="ee_img tr_noresize" eeimg="1"> . 

**推论** 设 <img src="https://www.zhihu.com/equation?tex=M,N" alt="M,N" class="ee_img tr_noresize" eeimg="1"> 在 <img src="https://www.zhihu.com/equation?tex=\mathcal{E}" alt="\mathcal{E}" class="ee_img tr_noresize" eeimg="1"> 中且 <img src="https://www.zhihu.com/equation?tex=M=_\beta N" alt="M=_\beta N" class="ee_img tr_noresize" eeimg="1"> ，则有 <img src="https://www.zhihu.com/equation?tex=L" alt="L" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=M\twoheadrightarrow_\beta L" alt="M\twoheadrightarrow_\beta L" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=N\twoheadrightarrow_\beta L" alt="N\twoheadrightarrow_\beta L" class="ee_img tr_noresize" eeimg="1"> .

### 主体归约引理*（Subject Reduction）*

若 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash A:B" alt="\Gamma\vdash A:B" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=A\twoheadrightarrow_\beta A'" alt="A\twoheadrightarrow_\beta A'" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash A':B" alt="\Gamma\vdash A':B" class="ee_img tr_noresize" eeimg="1"> .

### 强标准化定理/终止定理*（Strong Normalisation Theorem/Termination Theorem）*

所有合法的 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 都是强标准化的.



最后是类型论的三个主要问题：良类型性、类型检查和项的寻找，前两个是可判定的.

### 可判定性定理*（Decidability of Well-typedness and Type Checking）*

在 <img src="https://www.zhihu.com/equation?tex=\lambda {\rm}" alt="\lambda {\rm}" class="ee_img tr_noresize" eeimg="1"> 和它所有的子系统中，良类型性和类型检查问题都是可判定的.

也就是说，我们可以设计一个程序自动解决这些问题：给定一个项，或者是项和它的类型（有没有上下文都可以），程序可以找到是否存在这样的派生并给出. 

而对于项的寻找问题，除了 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\lambda\underline\omega" alt="\lambda\underline\omega" class="ee_img tr_noresize" eeimg="1"> 之外的系统中都是不可判定的。这也可以理解为，证明或证否任意数学命题的方法是不存在的，这个结论也就是著名的**丘奇-图灵不可判定定理** *（Church-Turing Undecidability Theorem）*. 
