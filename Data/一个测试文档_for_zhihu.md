本文为*Type Theory and Formal Proof : An Introduction* 的笔记，纯个人向（

------

## 简单类型（Simple types）

我们从一个**类型变量**（type variables）的无限集开始： <img src="https://www.zhihu.com/equation?tex=\mathbb{V}=\lbrace \alpha,\beta,\gamma,...\rbrace" alt="\mathbb{V}=\lbrace \alpha,\beta,\gamma,...\rbrace" class="ee_img tr_noresize" eeimg="1"> .

### 所有简单类型的集合 <img src="https://www.zhihu.com/equation?tex=\mathbb{T}" alt="\mathbb{T}" class="ee_img tr_noresize" eeimg="1"> 

1. 类型变量（Type variable）若 <img src="https://www.zhihu.com/equation?tex=\alpha \in \mathbb{V}" alt="\alpha \in \mathbb{V}" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\alpha \in \mathbb{T}" alt="\alpha \in \mathbb{T}" class="ee_img tr_noresize" eeimg="1"> 
2. 箭头类型（Arrow type）若 <img src="https://www.zhihu.com/equation?tex=\sigma,\tau \in \mathbb{T}" alt="\sigma,\tau \in \mathbb{T}" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=(\sigma \to \tau) \in \mathbb{T}" alt="(\sigma \to \tau) \in \mathbb{T}" class="ee_img tr_noresize" eeimg="1"> 

即  <img src="https://www.zhihu.com/equation?tex=\mathbb{T= V\ |\ T \to T}" alt="\mathbb{T= V\ |\ T \to T}" class="ee_img tr_noresize" eeimg="1">  .

记法：使用字母 <img src="https://www.zhihu.com/equation?tex=\alpha,\beta,..." alt="\alpha,\beta,..." class="ee_img tr_noresize" eeimg="1"> 表示 <img src="https://www.zhihu.com/equation?tex=\mathbb{V}" alt="\mathbb{V}" class="ee_img tr_noresize" eeimg="1"> 中的类型变量， <img src="https://www.zhihu.com/equation?tex=\sigma,\tau,..." alt="\sigma,\tau,..." class="ee_img tr_noresize" eeimg="1"> （有时也用 <img src="https://www.zhihu.com/equation?tex=A,B,..." alt="A,B,..." class="ee_img tr_noresize" eeimg="1"> ）表示一个简单类型. 最外侧的括号可以省略. 箭头是右结合的.

“项 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=\tau" alt="\tau" class="ee_img tr_noresize" eeimg="1"> ”，我们引入**定型陈述**（statements, or typing statements），形式为 <img src="https://www.zhihu.com/equation?tex=M:\tau" alt="M:\tau" class="ee_img tr_noresize" eeimg="1"> .

我们假设对于每个类型都有无穷的变量，且每个变量的类型都是唯一的，即若 <img src="https://www.zhihu.com/equation?tex=x:\sigma" alt="x:\sigma" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=x:\tau" alt="x:\tau" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\sigma \equiv \tau" alt="\sigma \equiv \tau" class="ee_img tr_noresize" eeimg="1"> .

对于lambda演算的构造方法，有：

1. 应用：若 <img src="https://www.zhihu.com/equation?tex=M:\sigma \to \tau" alt="M:\sigma \to \tau" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=N:\sigma" alt="N:\sigma" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=M\ N:\tau" alt="M\ N:\tau" class="ee_img tr_noresize" eeimg="1"> .
2. 抽象：若 <img src="https://www.zhihu.com/equation?tex=x:\sigma" alt="x:\sigma" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=M:\tau" alt="M:\tau" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\lambda x.M:\sigma \to \tau" alt="\lambda x.M:\sigma \to \tau" class="ee_img tr_noresize" eeimg="1"> 

### 可定型的项（Typable term）

我们说一个项 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 可定型，如果存在类型 <img src="https://www.zhihu.com/equation?tex=\sigma" alt="\sigma" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=M:\sigma" alt="M:\sigma" class="ee_img tr_noresize" eeimg="1"> .

## Church定型与Curry定型（Church-typing and Curry-typing）

对于定型，有两种方法：

### Church定型（Typing à la Church）

假设 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=\alpha \to \alpha" alt="\alpha \to \alpha" class="ee_img tr_noresize" eeimg="1"> ，且 <img src="https://www.zhihu.com/equation?tex=y" alt="y" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=(\alpha \to \alpha) \to \beta" alt="(\alpha \to \alpha) \to \beta" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=yx" alt="yx" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=\beta" alt="\beta" class="ee_img tr_noresize" eeimg="1"> . 然后 <img src="https://www.zhihu.com/equation?tex=z" alt="z" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=\beta" alt="\beta" class="ee_img tr_noresize" eeimg="1"> ，且 <img src="https://www.zhihu.com/equation?tex=u" alt="u" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=\gamma" alt="\gamma" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\lambda zu.z" alt="\lambda zu.z" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=\beta \to \gamma \to \beta" alt="\beta \to \gamma \to \beta" class="ee_img tr_noresize" eeimg="1"> . 所以，如果 <img src="https://www.zhihu.com/equation?tex=(\lambda zu.z)(yx)" alt="(\lambda zu.z)(yx)" class="ee_img tr_noresize" eeimg="1"> 是允许的，则有类型 <img src="https://www.zhihu.com/equation?tex=\gamma \to \beta" alt="\gamma \to \beta" class="ee_img tr_noresize" eeimg="1"> .

### Curry定型（Typing à la Curry）

对于lambda项 <img src="https://www.zhihu.com/equation?tex=M \equiv (\lambda zu.z)(yx)" alt="M \equiv (\lambda zu.z)(yx)" class="ee_img tr_noresize" eeimg="1"> ，假设变量 <img src="https://www.zhihu.com/equation?tex=x,y,z,u" alt="x,y,z,u" class="ee_img tr_noresize" eeimg="1"> 的类型并没有给出. 我们注意到 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 是一个 <img src="https://www.zhihu.com/equation?tex=\lambda zu.z" alt="\lambda zu.z" class="ee_img tr_noresize" eeimg="1"> 对 <img src="https://www.zhihu.com/equation?tex=yx" alt="yx" class="ee_img tr_noresize" eeimg="1"> 的应用，所以 <img src="https://www.zhihu.com/equation?tex=\lambda zu.z" alt="\lambda zu.z" class="ee_img tr_noresize" eeimg="1"> 应该有一个函数类型，比如 <img src="https://www.zhihu.com/equation?tex=A \to B" alt="A \to B" class="ee_img tr_noresize" eeimg="1"> ，且 <img src="https://www.zhihu.com/equation?tex=yx" alt="yx" class="ee_img tr_noresize" eeimg="1"> 必须有类型 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> ，所以 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> . 

 <img src="https://www.zhihu.com/equation?tex=\lambda zu.z:A \to B" alt="\lambda zu.z:A \to B" class="ee_img tr_noresize" eeimg="1"> 表明 <img src="https://www.zhihu.com/equation?tex=z:A" alt="z:A" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\lambda u.z:B" alt="\lambda u.z:B" class="ee_img tr_noresize" eeimg="1"> . 对于后一个类型陈述， <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 是一个 <img src="https://www.zhihu.com/equation?tex=\lambda" alt="\lambda" class="ee_img tr_noresize" eeimg="1"> 开头抽象的项，因此 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 具有函数类型 <img src="https://www.zhihu.com/equation?tex=B\equiv (C \to D)" alt="B\equiv (C \to D)" class="ee_img tr_noresize" eeimg="1"> ，且 <img src="https://www.zhihu.com/equation?tex=u:C,z:D" alt="u:C,z:D" class="ee_img tr_noresize" eeimg="1"> . 

而 <img src="https://www.zhihu.com/equation?tex=yx" alt="yx" class="ee_img tr_noresize" eeimg="1"> 是一个应用，因此一定有 <img src="https://www.zhihu.com/equation?tex=y:E \to F" alt="y:E \to F" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=x:E" alt="x:E" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=yx:F" alt="yx:F" class="ee_img tr_noresize" eeimg="1"> . 

我们有：

-  <img src="https://www.zhihu.com/equation?tex=x:E" alt="x:E" class="ee_img tr_noresize" eeimg="1"> 
-  <img src="https://www.zhihu.com/equation?tex=y:E\to F" alt="y:E\to F" class="ee_img tr_noresize" eeimg="1"> 
-  <img src="https://www.zhihu.com/equation?tex=z:A 且 z:D，所以A\equiv D" alt="z:A 且 z:D，所以A\equiv D" class="ee_img tr_noresize" eeimg="1"> 
-  <img src="https://www.zhihu.com/equation?tex=u:C" alt="u:C" class="ee_img tr_noresize" eeimg="1"> 
-  <img src="https://www.zhihu.com/equation?tex=B\equiv (C \to D)" alt="B\equiv (C \to D)" class="ee_img tr_noresize" eeimg="1"> 
-  <img src="https://www.zhihu.com/equation?tex=yx:A 且yz:F，所以A \equiv F" alt="yx:A 且yz:F，所以A \equiv F" class="ee_img tr_noresize" eeimg="1"> 

得到 <img src="https://www.zhihu.com/equation?tex=(*)\ x:E,y:E\to A,z:A,u:C" alt="(*)\ x:E,y:E\to A,z:A,u:C" class="ee_img tr_noresize" eeimg="1"> .

我们可以将变量 <img src="https://www.zhihu.com/equation?tex=x,y,z,u" alt="x,y,z,u" class="ee_img tr_noresize" eeimg="1"> 赋予“真实”的类型，填入 <img src="https://www.zhihu.com/equation?tex=(*)" alt="(*)" class="ee_img tr_noresize" eeimg="1"> 式的样板，如：

-  <img src="https://www.zhihu.com/equation?tex=x:\beta, y:\beta \to \alpha, z:\alpha,u:\delta, M:\delta \to \alpha" alt="x:\beta, y:\beta \to \alpha, z:\alpha,u:\delta, M:\delta \to \alpha" class="ee_img tr_noresize" eeimg="1"> 
-  <img src="https://www.zhihu.com/equation?tex=x:\alpha \to \alpha,y:(\alpha \to \alpha)\to \beta,z:\beta,u:\gamma,M:\gamma \to \beta" alt="x:\alpha \to \alpha,y:(\alpha \to \alpha)\to \beta,z:\beta,u:\gamma,M:\gamma \to \beta" class="ee_img tr_noresize" eeimg="1"> 
-  <img src="https://www.zhihu.com/equation?tex=x:\alpha,y:\alpha\to \alpha \to \beta, z:\alpha \to \beta,u:\alpha \to \alpha" alt="x:\alpha,y:\alpha\to \alpha \to \beta, z:\alpha \to \beta,u:\alpha \to \alpha" class="ee_img tr_noresize" eeimg="1"> 

我们对于绑定的变量直接给出类型，自由变量的类型称为**上下文**（context）.

对于项 <img src="https://www.zhihu.com/equation?tex=(\lambda zu.z)(yx)" alt="(\lambda zu.z)(yx)" class="ee_img tr_noresize" eeimg="1"> ， <img src="https://www.zhihu.com/equation?tex=z,u" alt="z,u" class="ee_img tr_noresize" eeimg="1"> 是绑定的，而 <img src="https://www.zhihu.com/equation?tex=x,y" alt="x,y" class="ee_img tr_noresize" eeimg="1"> 是自由的. 假设 <img src="https://www.zhihu.com/equation?tex=z:\beta" alt="z:\beta" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=u:\gamma" alt="u:\gamma" class="ee_img tr_noresize" eeimg="1"> ，我们记作 <img src="https://www.zhihu.com/equation?tex=(\lambda z:\beta.\lambda u:\gamma.z)(yx)" alt="(\lambda z:\beta.\lambda u:\gamma.z)(yx)" class="ee_img tr_noresize" eeimg="1"> .

对于此例的上下文，记作：

 <img src="https://www.zhihu.com/equation?tex=x:\alpha \to \alpha,y:(\alpha \to \alpha) \to \beta \ \vdash\  (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to \beta" alt="x:\alpha \to \alpha,y:(\alpha \to \alpha) \to \beta \ \vdash\  (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to \beta" class="ee_img tr_noresize" eeimg="1"> .

## Church的 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 的派生法则

### 预标注类型的lambda项（Pre-typed λ-terms, <img src="https://www.zhihu.com/equation?tex=\Lambda_\mathbb{T}" alt="\Lambda_\mathbb{T}" class="ee_img tr_noresize" eeimg="1"> ）

 <img src="https://www.zhihu.com/equation?tex=\Lambda_\mathbb{T}=V|(\Lambda_\mathbb{T}\Lambda_\mathbb{T})|(\lambda V:\mathbb{T}.\Lambda_\mathbb{T})" alt="\Lambda_\mathbb{T}=V|(\Lambda_\mathbb{T}\Lambda_\mathbb{T})|(\lambda V:\mathbb{T}.\Lambda_\mathbb{T})" class="ee_img tr_noresize" eeimg="1"> .

### 陈述，声明，上下文，推断（Statement, declaration, context, judgement）

1. **陈述**（statement）具有形式 <img src="https://www.zhihu.com/equation?tex=M:\sigma" alt="M:\sigma" class="ee_img tr_noresize" eeimg="1"> ，其中 <img src="https://www.zhihu.com/equation?tex=M \in \Lambda_\mathbb{T}" alt="M \in \Lambda_\mathbb{T}" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\sigma \in \mathbb{T}" alt="\sigma \in \mathbb{T}" class="ee_img tr_noresize" eeimg="1"> . 在陈述中，称 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 主体（subject）， <img src="https://www.zhihu.com/equation?tex=\sigma" alt="\sigma" class="ee_img tr_noresize" eeimg="1"> 为类型.
2. **声明**（declaration）是以变量为主体的陈述.
3. **上下文**（context）是一个对于*不同*主体的声明的列表.
4. **推断**（judgement）具有形式 <img src="https://www.zhihu.com/equation?tex=\Gamma \ \vdash \ M:\sigma" alt="\Gamma \ \vdash \ M:\sigma" class="ee_img tr_noresize" eeimg="1"> ，其中 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 是上下文，而 <img src="https://www.zhihu.com/equation?tex=M:\sigma" alt="M:\sigma" class="ee_img tr_noresize" eeimg="1"> 是陈述.

我们需要判断一个推断是否是可派生的，引入**派生系统 **（derivation system）.

**前提-结论格式**（premiss–conclusion format）：

 <img src="https://www.zhihu.com/equation?tex=\dfrac{前提1\ 前提2\ ...\ 前提n}{结论}" alt="\dfrac{前提1\ 前提2\ ...\ 前提n}{结论}" class="ee_img tr_noresize" eeimg="1"> 

由此给出Church的 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 的三条派生法则，以此建立Church的 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 的派生系统.

### Church的 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 的派生法则（Derivation rules for  <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> ）

 <img src="https://www.zhihu.com/equation?tex=(var)\qquad \Gamma\  \vdash\ x:\sigma 若x:\sigma\in \Gamma" alt="(var)\qquad \Gamma\  \vdash\ x:\sigma 若x:\sigma\in \Gamma" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(appl)\ \dfrac{\Gamma\ \vdash \ M:\sigma\to\tau\qquad \Gamma\ \vdash\ N:\sigma}{\Gamma\ \vdash\ MN:\tau}" alt="(appl)\ \dfrac{\Gamma\ \vdash \ M:\sigma\to\tau\qquad \Gamma\ \vdash\ N:\sigma}{\Gamma\ \vdash\ MN:\tau}" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(abst)\ \dfrac{\Gamma,x:\sigma\ \vdash\ M:\tau}{\Gamma \ \vdash\ \lambda x:\sigma.M:\sigma\to\tau}" alt="(abst)\ \dfrac{\Gamma,x:\sigma\ \vdash\ M:\tau}{\Gamma \ \vdash\ \lambda x:\sigma.M:\sigma\to\tau}" class="ee_img tr_noresize" eeimg="1"> 

基于派生系统可标注类型的项称**合法的**（legal）.

### 合法的 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 项（Legal  <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> -terms）

在 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中，一个预标注类型的lambda项 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 是**合法的**，如果存在上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 和类型 <img src="https://www.zhihu.com/equation?tex=\rho" alt="\rho" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash M:\rho" alt="\Gamma \vdash M:\rho" class="ee_img tr_noresize" eeimg="1"> .

## 类型论需要解决的几类问题

### 良类型性/可定型性（Well-typedness/Typability）

形如：

 <img src="https://www.zhihu.com/equation?tex=?\  \vdash\  项:\ ?" alt="?\  \vdash\  项:\ ?" class="ee_img tr_noresize" eeimg="1"> 

即判断一个项是否合法，如果合法则找到一个合适的上下文和类型，否则找出它出错的地方.

一个变体是**类型赋值**（Type Assignment），即给出上下文，只要找出项的类型：

 <img src="https://www.zhihu.com/equation?tex=上下文\ \vdash\ 项\ :\ ?" alt="上下文\ \vdash\ 项\ :\ ?" class="ee_img tr_noresize" eeimg="1"> .

### 类型检查（Type Checking）

 <img src="https://www.zhihu.com/equation?tex=上下文\ \overset{?}{\vdash}\ 项\ :\ 类型" alt="上下文\ \overset{?}{\vdash}\ 项\ :\ 类型" class="ee_img tr_noresize" eeimg="1"> 

给出上下文、项和类型，检查是否这个项（在这个上下文中）有这个类型.

### 项的寻找（Term Finding/Term Construction/Inhabitation）

 <img src="https://www.zhihu.com/equation?tex=上下文\ \vdash\ ?\ :\ 类型" alt="上下文\ \vdash\ ?\ :\ 类型" class="ee_img tr_noresize" eeimg="1"> 

给定上下文和类型，寻找是否存在合适的项.

##  <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中的良类型性

例：项 <img src="https://www.zhihu.com/equation?tex=M\equiv \lambda y:\alpha \to \beta .\lambda z:\alpha.yz" alt="M\equiv \lambda y:\alpha \to \beta .\lambda z:\alpha.yz" class="ee_img tr_noresize" eeimg="1"> 是否合法. 即找到上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 和类型 <img src="https://www.zhihu.com/equation?tex=\rho" alt="\rho" class="ee_img tr_noresize" eeimg="1"> ，使得 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash M:\rho" alt="\Gamma \vdash M:\rho" class="ee_img tr_noresize" eeimg="1"> .

首先 <img src="https://www.zhihu.com/equation?tex=\Gamma\equiv\emptyset" alt="\Gamma\equiv\emptyset" class="ee_img tr_noresize" eeimg="1"> 就可以，因为 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 中没有自由变量需要定型. 其次就是找到 <img src="https://www.zhihu.com/equation?tex=\rho" alt="\rho" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=(n)\quad \lambda y.\alpha \to \beta.\lambda z:\alpha.yz\ :\ ?" alt="(n)\quad \lambda y.\alpha \to \beta.\lambda z:\alpha.yz\ :\ ?" class="ee_img tr_noresize" eeimg="1"> 

由三条派生法则中，只有抽象法则 <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> 可以用，这样就变成了：
 <img src="https://www.zhihu.com/equation?tex=\quad\vdots\\" alt="\quad\vdots\\" class="ee_img tr_noresize" eeimg="1"> 
 <img src="https://www.zhihu.com/equation?tex=(m)\quad y:\alpha \to \beta\ \vdash\ \lambda z:\alpha.yz\ :\ ?" alt="(m)\quad y:\alpha \to \beta\ \vdash\ \lambda z:\alpha.yz\ :\ ?" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad \lambda y:\alpha\to \beta.\lambda z:\alpha.yz:\dots\qquad 对(m)用(abst)" alt="(n)\quad \lambda y:\alpha\to \beta.\lambda z:\alpha.yz:\dots\qquad 对(m)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

这样问题就变成了 <img src="https://www.zhihu.com/equation?tex=(m)" alt="(m)" class="ee_img tr_noresize" eeimg="1"> 中的 <img src="https://www.zhihu.com/equation?tex=?" alt="?" class="ee_img tr_noresize" eeimg="1"> . 需要找到 <img src="https://www.zhihu.com/equation?tex=\lambda z:\alpha.yz" alt="\lambda z:\alpha.yz" class="ee_img tr_noresize" eeimg="1"> 的类型，同样是 <img src="https://www.zhihu.com/equation?tex=\lambda" alt="\lambda" class="ee_img tr_noresize" eeimg="1"> ，重复上面的操作：

 <img src="https://www.zhihu.com/equation?tex=\quad\vdots" alt="\quad\vdots" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(l)\quad y:\alpha \to \beta,\ z:\alpha \ \vdash\  yz\ :\ ?" alt="(l)\quad y:\alpha \to \beta,\ z:\alpha \ \vdash\  yz\ :\ ?" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(m)\quad y:\alpha \to \beta \ \vdash\ \lambda z:\alpha.yz\ :\ \dots \qquad对(l)用(abst)" alt="(m)\quad y:\alpha \to \beta \ \vdash\ \lambda z:\alpha.yz\ :\ \dots \qquad对(l)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad \lambda y:\alpha\to \beta.\lambda z:\alpha.yz:\dots\qquad 对(m)用(abst)" alt="(n)\quad \lambda y:\alpha\to \beta.\lambda z:\alpha.yz:\dots\qquad 对(m)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

新的要定型的项是 <img src="https://www.zhihu.com/equation?tex=yz" alt="yz" class="ee_img tr_noresize" eeimg="1"> ，是一个应用，所以只能用应用法则 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> . 而 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> 有两个前提，所以现在有两个新目标：

 <img src="https://www.zhihu.com/equation?tex=\quad\vdots" alt="\quad\vdots" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(k_1)\quad y:\alpha \to \beta,\ z:\alpha \ \vdash\ y\ :\ ?_1" alt="(k_1)\quad y:\alpha \to \beta,\ z:\alpha \ \vdash\ y\ :\ ?_1" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=\quad \vdots" alt="\quad \vdots" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(k_2)\quad y:\alpha \to \beta,\ z:\alpha \ \vdash\ z\ :\ ?_2" alt="(k_2)\quad y:\alpha \to \beta,\ z:\alpha \ \vdash\ z\ :\ ?_2" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(l)\quad y:\alpha \to \beta,\ z:\alpha \ \vdash\  yz\ :\ \dots \qquad 对(k_1)和(k_2)用(appl)" alt="(l)\quad y:\alpha \to \beta,\ z:\alpha \ \vdash\  yz\ :\ \dots \qquad 对(k_1)和(k_2)用(appl)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(m)\quad y:\alpha \to \beta \ \vdash\ \lambda z:\alpha.yz\ :\ \dots \qquad对(l)用(abst)" alt="(m)\quad y:\alpha \to \beta \ \vdash\ \lambda z:\alpha.yz\ :\ \dots \qquad对(l)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad \lambda y:\alpha\to \beta.\lambda z:\alpha.yz:\dots\qquad 对(m)用(abst)" alt="(n)\quad \lambda y:\alpha\to \beta.\lambda z:\alpha.yz:\dots\qquad 对(m)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

现在的目标是 <img src="https://www.zhihu.com/equation?tex=y" alt="y" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=z" alt="z" class="ee_img tr_noresize" eeimg="1"> ，它们是简单的*变量*，因此用变量法则 <img src="https://www.zhihu.com/equation?tex=(var)" alt="(var)" class="ee_img tr_noresize" eeimg="1"> 就完了. 接下来对于 <img src="https://www.zhihu.com/equation?tex=(l)" alt="(l)" class="ee_img tr_noresize" eeimg="1"> 的项 <img src="https://www.zhihu.com/equation?tex=yz" alt="yz" class="ee_img tr_noresize" eeimg="1"> ，由于 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> 的条件满足了就可以得到它的类型 <img src="https://www.zhihu.com/equation?tex=\beta" alt="\beta" class="ee_img tr_noresize" eeimg="1"> . 接下来的项的类型也都可以这样得到.

最终得出的结论是我们找到了一个派生，说明 <img src="https://www.zhihu.com/equation?tex=\lambda y:\alpha \to \beta:\alpha.yz" alt="\lambda y:\alpha \to \beta:\alpha.yz" class="ee_img tr_noresize" eeimg="1"> 是合法的.

##  <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中的类型检查

例： <img src="https://www.zhihu.com/equation?tex=x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta\ \vdash\ (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta" alt="x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta\ \vdash\ (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta" class="ee_img tr_noresize" eeimg="1"> .

我们的目标是填入下面的点点点：

 <img src="https://www.zhihu.com/equation?tex=\quad\vdots" alt="\quad\vdots" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta\ \vdash\ (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta" alt="(n)\quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta\ \vdash\ (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta" class="ee_img tr_noresize" eeimg="1"> 

因为项 <img src="https://www.zhihu.com/equation?tex=(\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta" alt="(\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta" class="ee_img tr_noresize" eeimg="1"> 是一个应用项，我们使用应用法则 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> .

 <img src="https://www.zhihu.com/equation?tex=\quad\vdots" alt="\quad\vdots" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(m_1)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ \lambda z:\beta.\lambda u:\gamma.z\ :\ ?_1" alt="(m_1)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ \lambda z:\beta.\lambda u:\gamma.z\ :\ ?_1" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=\quad\vdots" alt="\quad\vdots" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(m_2)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ yx\ :\ ?_2" alt="(m_2)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ yx\ :\ ?_2" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta\ \vdash\ (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta \quad对(m_1)和(m_2)用(appl),(?)" alt="(n)\quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta\ \vdash\ (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta \quad对(m_1)和(m_2)用(appl),(?)" class="ee_img tr_noresize" eeimg="1"> 

因为 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> 法则只有在对应的类型匹配上了才成立，所以最后一行还留了个 <img src="https://www.zhihu.com/equation?tex=(?)" alt="(?)" class="ee_img tr_noresize" eeimg="1"> .

对于 <img src="https://www.zhihu.com/equation?tex=?_2" alt="?_2" class="ee_img tr_noresize" eeimg="1"> 可以用两次 <img src="https://www.zhihu.com/equation?tex=(var)" alt="(var)" class="ee_img tr_noresize" eeimg="1"> 法则然后 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> 法则解决，并且 <img src="https://www.zhihu.com/equation?tex=y" alt="y" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 的类型也匹配得上. 现在还剩：

 <img src="https://www.zhihu.com/equation?tex=\quad\vdots" alt="\quad\vdots" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(m_1)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ \lambda z:\beta.\lambda u:\gamma.z\ :\ ?" alt="(m_1)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ \lambda z:\beta.\lambda u:\gamma.z\ :\ ?" class="ee_img tr_noresize" eeimg="1"> 

对于两个 <img src="https://www.zhihu.com/equation?tex=\lambda" alt="\lambda" class="ee_img tr_noresize" eeimg="1"> 可以使用两次 <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> 法则解决，就得到了完整的派生：

 <img src="https://www.zhihu.com/equation?tex=(a) \quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta,\ z:\beta,\ u:\gamma \ \vdash\ x:\alpha" alt="(a) \quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta,\ z:\beta,\ u:\gamma \ \vdash\ x:\alpha" class="ee_img tr_noresize" eeimg="1"> 
 <img src="https://www.zhihu.com/equation?tex=(b) \quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta,\ z:\beta,\ u:\gamma \ \vdash\ y:(\alpha \to \alpha)\to \beta" alt="(b) \quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta,\ z:\beta,\ u:\gamma \ \vdash\ y:(\alpha \to \alpha)\to \beta" class="ee_img tr_noresize" eeimg="1"> 
 <img src="https://www.zhihu.com/equation?tex=(1) \quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta,\ z:\beta,\ u:\gamma \ \vdash\ z:\beta" alt="(1) \quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta,\ z:\beta,\ u:\gamma \ \vdash\ z:\beta" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(2)\quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta,\ z:\beta \ \vdash\ \lambda u:\gamma.z:\gamma \to \beta \quad 对(1)用(abst)" alt="(2)\quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta,\ z:\beta \ \vdash\ \lambda u:\gamma.z:\gamma \to \beta \quad 对(1)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(m_1)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ \lambda z:\beta.\lambda u:\gamma.z\ :\ \beta \to\gamma\to\beta \quad 对(2)用(abst)" alt="(m_1)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ \lambda z:\beta.\lambda u:\gamma.z\ :\ \beta \to\gamma\to\beta \quad 对(2)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(m_2)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ yx\ :\beta \quad 对(b)和(a)用(appl)" alt="(m_2)\  x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta \ \vdash\ yx\ :\beta \quad 对(b)和(a)用(appl)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta\ \vdash\ (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta \quad对(m_1)和(m_2)用(appl),(?)" alt="(n)\quad x:\alpha \to \alpha,\ y:(\alpha \to \alpha)\to \beta\ \vdash\ (\lambda z:\beta.\lambda u:\gamma.z)(yx):\gamma \to\beta \quad对(m_1)和(m_2)用(appl),(?)" class="ee_img tr_noresize" eeimg="1"> 

接下来只剩下检查 <img src="https://www.zhihu.com/equation?tex=(n)" alt="(n)" class="ee_img tr_noresize" eeimg="1">  的 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1">  的条件，显然满足了. 于是我们给出了这个推断的正确派生.

##  <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中项的寻找

在逻辑表达式中，我们有 <img src="https://www.zhihu.com/equation?tex=A \to B \to A" alt="A \to B \to A" class="ee_img tr_noresize" eeimg="1"> ，其中的 <img src="https://www.zhihu.com/equation?tex=\to" alt="\to" class="ee_img tr_noresize" eeimg="1"> 读作“蕴含”，这个命题是一个“重言式”. 这很显然，因为：如果A，那么（如果B那么A）.

我们可以用 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 形式化这个证明，把 <img src="https://www.zhihu.com/equation?tex=A\to B\to A" alt="A\to B\to A" class="ee_img tr_noresize" eeimg="1"> 作为一个类型，尝试找到一个在空上下文中的项：

 <img src="https://www.zhihu.com/equation?tex=(n)\quad ?\ :\ A\to B\to A" alt="(n)\quad ?\ :\ A\to B\to A" class="ee_img tr_noresize" eeimg="1"> 

需要一个 <img src="https://www.zhihu.com/equation?tex=\to" alt="\to" class="ee_img tr_noresize" eeimg="1"> 类型的项，所以首先用 <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> 法则：

 <img src="https://www.zhihu.com/equation?tex=(m)\quad x:A \ \vdash\ ?\ :\ B\to A" alt="(m)\quad x:A \ \vdash\ ?\ :\ B\to A" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad \dots\ :\ A\to B\to A\qquad 对(m)用(abst)" alt="(n)\quad \dots\ :\ A\to B\to A\qquad 对(m)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

现在仍然是一个 <img src="https://www.zhihu.com/equation?tex=\to" alt="\to" class="ee_img tr_noresize" eeimg="1"> 类型的项，引入新变量 <img src="https://www.zhihu.com/equation?tex=y" alt="y" class="ee_img tr_noresize" eeimg="1"> 重复这个过程：

 <img src="https://www.zhihu.com/equation?tex=(l)\quad x:A,\ y:B\ \vdash\ ?\ :\ A" alt="(l)\quad x:A,\ y:B\ \vdash\ ?\ :\ A" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(m)\quad x:A \ \vdash\ ?\ :\ B\to A\qquad 对(l)用(abst)" alt="(m)\quad x:A \ \vdash\ ?\ :\ B\to A\qquad 对(l)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad \dots\ :\ A\to B\to A\qquad 对(m)用(abst)" alt="(n)\quad \dots\ :\ A\to B\to A\qquad 对(m)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

现在 <img src="https://www.zhihu.com/equation?tex=?" alt="?" class="ee_img tr_noresize" eeimg="1"> 可以被 <img src="https://www.zhihu.com/equation?tex=(var)" alt="(var)" class="ee_img tr_noresize" eeimg="1"> 法则解决：

 <img src="https://www.zhihu.com/equation?tex=(1)\quad x:A,\ y:B\ \vdash\ x\ :\ A" alt="(1)\quad x:A,\ y:B\ \vdash\ x\ :\ A" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(2)\quad x:A \ \vdash\ \lambda y:B.\ x\ :\ B\to A\qquad 对(1)用(abst)" alt="(2)\quad x:A \ \vdash\ \lambda y:B.\ x\ :\ B\to A\qquad 对(1)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(3)\quad \lambda x:A.\ \lambda y:B.\ x\ :\ A\to B\to A\qquad 对(2)用(abst)" alt="(3)\quad \lambda x:A.\ \lambda y:B.\ x\ :\ A\to B\to A\qquad 对(2)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

就完成了. 

我们将命题看做类型，把命题的inhabitants作为*证明*：

 <img src="https://www.zhihu.com/equation?tex=假设x是命题A的证明，y是命题B的证明." alt="假设x是命题A的证明，y是命题B的证明." class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(1)\quad 那么x（仍）是A的证明." alt="(1)\quad 那么x（仍）是A的证明." class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(2)\quad y到x的函数是一个由B到A的证明，即\lambda y:B.\ x证明了B\to A这个蕴含." alt="(2)\quad y到x的函数是一个由B到A的证明，即\lambda y:B.\ x证明了B\to A这个蕴含." class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(3)\quad 所以，\lambda x:A.\lambda y:B\ x证明了A\to B\to A." alt="(3)\quad 所以，\lambda x:A.\lambda y:B\ x证明了A\to B\to A." class="ee_img tr_noresize" eeimg="1"> 

这一过程称**PAT-解释**（PAT-interpretation），“PAT”既指“命题作为类型”（propositions-as-types），又指“证明作为项”（proofs-as-term）. 

##  <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 的性质

### **定义域，子上下文，置换，投影**（Domain,  <img src="https://www.zhihu.com/equation?tex=\rm dom" alt="\rm dom" class="ee_img tr_noresize" eeimg="1"> , subcontext,  <img src="https://www.zhihu.com/equation?tex=\subseteq" alt="\subseteq" class="ee_img tr_noresize" eeimg="1"> , permutation, projection,  <img src="https://www.zhihu.com/equation?tex=\upharpoonright" alt="\upharpoonright" class="ee_img tr_noresize" eeimg="1"> ）

1. 如果 <img src="https://www.zhihu.com/equation?tex=\Gamma \equiv x_1 : \sigma_1,\dots,x_n:\sigma_n" alt="\Gamma \equiv x_1 : \sigma_1,\dots,x_n:\sigma_n" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 的**定义域**（domain）或 <img src="https://www.zhihu.com/equation?tex=\rm dom(\Gamma)" alt="\rm dom(\Gamma)" class="ee_img tr_noresize" eeimg="1"> 为列表 <img src="https://www.zhihu.com/equation?tex=(x_1,\dots,x_n)" alt="(x_1,\dots,x_n)" class="ee_img tr_noresize" eeimg="1"> .
2. 上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1">  的**子上下文**（subcontext），或 <img src="https://www.zhihu.com/equation?tex=\Gamma' \subseteq \Gamma" alt="\Gamma' \subseteq \Gamma" class="ee_img tr_noresize" eeimg="1"> ，如果 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 中所有的声明也在 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 中以相同次序出现.
3. 上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 是上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 的一个**置换**（permutation），如果所有在 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 中的声明也在 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 中出现，反之亦然.
4. 如果 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 是一个上下文， <img src="https://www.zhihu.com/equation?tex=\Phi" alt="\Phi" class="ee_img tr_noresize" eeimg="1"> 是一个变量的集合，则 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 在 <img src="https://www.zhihu.com/equation?tex=\Phi" alt="\Phi" class="ee_img tr_noresize" eeimg="1"> 上的**投影**（projection）或 <img src="https://www.zhihu.com/equation?tex=\Gamma \upharpoonright\Phi" alt="\Gamma \upharpoonright\Phi" class="ee_img tr_noresize" eeimg="1"> ，是 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 的一个子上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> ，满足 <img src="https://www.zhihu.com/equation?tex={\rm dom}(\Gamma') = {\rm dom}(\Gamma)\cap\Phi" alt="{\rm dom}(\Gamma') = {\rm dom}(\Gamma)\cap\Phi" class="ee_img tr_noresize" eeimg="1"> .

### **自由变量引理** *(Free Variables Lemma)*

若 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash L:\sigma" alt="\Gamma \vdash L:\sigma" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=FV(L)\subseteq {\rm dom}(\Gamma)" alt="FV(L)\subseteq {\rm dom}(\Gamma)" class="ee_img tr_noresize" eeimg="1"> .

这说明，如果 <img src="https://www.zhihu.com/equation?tex=L" alt="L" class="ee_img tr_noresize" eeimg="1"> 有类型，则所有在 <img src="https://www.zhihu.com/equation?tex=L" alt="L" class="ee_img tr_noresize" eeimg="1"> 中出现的自由变量 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 都有类型，且作为一条声明 <img src="https://www.zhihu.com/equation?tex=x:\sigma" alt="x:\sigma" class="ee_img tr_noresize" eeimg="1"> 记录在上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 中.

### 引理*(Thinning, Condensing, Permutation)*

1. （Thinning）令 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 与 <img src="https://www.zhihu.com/equation?tex=\Gamma''" alt="\Gamma''" class="ee_img tr_noresize" eeimg="1"> 是上下文，使得 <img src="https://www.zhihu.com/equation?tex=\Gamma' \subseteq \Gamma''" alt="\Gamma' \subseteq \Gamma''" class="ee_img tr_noresize" eeimg="1"> . 若 <img src="https://www.zhihu.com/equation?tex=\Gamma' \vdash M:\sigma" alt="\Gamma' \vdash M:\sigma" class="ee_img tr_noresize" eeimg="1"> 则 <img src="https://www.zhihu.com/equation?tex=\Gamma'' \vdash M:\sigma" alt="\Gamma'' \vdash M:\sigma" class="ee_img tr_noresize" eeimg="1"> .
2. （Condensing）若 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash M:\sigma" alt="\Gamma \vdash M:\sigma" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\Gamma \upharpoonright FV(M) \vdash M:\sigma" alt="\Gamma \upharpoonright FV(M) \vdash M:\sigma" class="ee_img tr_noresize" eeimg="1"> .
3. （Permutation）若 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash M:\sigma" alt="\Gamma \vdash M:\sigma" class="ee_img tr_noresize" eeimg="1"> ，且 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 的一个permutation，则 <img src="https://www.zhihu.com/equation?tex=\Gamma'" alt="\Gamma'" class="ee_img tr_noresize" eeimg="1"> 也是上下文，且 <img src="https://www.zhihu.com/equation?tex=\Gamma' \vdash M:\sigma" alt="\Gamma' \vdash M:\sigma" class="ee_img tr_noresize" eeimg="1"> .

- Thinning指一个上下文加上更多声明的扩展，即与*子上下文*相反. 
- Condensing指仅需要保留 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 中关于 <img src="https://www.zhihu.com/equation?tex=FV(M)" alt="FV(M)" class="ee_img tr_noresize" eeimg="1"> 的部分就可以得到 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 的类型.
- Permutation指上下文的顺序并不重要，上下文中的声明并没有相互依赖关系.

因此在 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中，也可以用集合代替列表定义上下文，集合上下文称**基**（bases）. 我们用列表因为对于更复杂的系统还会有依赖的声明，此时顺序就很重要.

### 生成引理（Generation Lemma）

1. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash x:\sigma" alt="\Gamma \vdash x:\sigma" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=x:\sigma \in \Gamma" alt="x:\sigma \in \Gamma" class="ee_img tr_noresize" eeimg="1"> .
2. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash MN:\tau" alt="\Gamma \vdash MN:\tau" class="ee_img tr_noresize" eeimg="1"> ，则存在类型 <img src="https://www.zhihu.com/equation?tex=\sigma" alt="\sigma" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash M:\sigma \to \tau" alt="\Gamma \vdash M:\sigma \to \tau" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash N:\sigma" alt="\Gamma \vdash N:\sigma" class="ee_img tr_noresize" eeimg="1"> .
3. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash \lambda x:\sigma.M:\rho" alt="\Gamma\vdash \lambda x:\sigma.M:\rho" class="ee_img tr_noresize" eeimg="1"> ，则存在 <img src="https://www.zhihu.com/equation?tex=\tau" alt="\tau" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=\Gamma,\ x:\sigma\vdash M:\tau" alt="\Gamma,\ x:\sigma\vdash M:\tau" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\rho \equiv \sigma \to \tau" alt="\rho \equiv \sigma \to \tau" class="ee_img tr_noresize" eeimg="1"> .

就对应了三条派生法则.

### 子项引理（Subterm Lemma）

若 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 是合法的，则 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 的所有子项都是合法的.

### 类型唯一性（Uniqueness of Types）

设 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash M:\sigma" alt="\Gamma \vdash M:\sigma" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash M : \tau" alt="\Gamma \vdash M : \tau" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\sigma \equiv \tau" alt="\sigma \equiv \tau" class="ee_img tr_noresize" eeimg="1"> .

### 可判定性定理

(Decidability of Well-typedness, Type Assignment, TypeChecking and Term Finding)

在 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中，以下问题都是可判定的：

1. Well-typedness（1a）Type Assignment
2. Type Checking
3. Term Finding

## 归约和 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 

对于 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中的beta归约，我们对代换的定义进行以下调整：

3.  <img src="https://www.zhihu.com/equation?tex=(\lambda y:\sigma.P)[x:=N]\equiv \lambda z:\sigma.(P^{y \to z}[x:=N])" alt="(\lambda y:\sigma.P)[x:=N]\equiv \lambda z:\sigma.(P^{y \to z}[x:=N])" class="ee_img tr_noresize" eeimg="1"> ，若 <img src="https://www.zhihu.com/equation?tex=\lambda z:\sigma.P^{y \to z}" alt="\lambda z:\sigma.P^{y \to z}" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda y:\sigma.P" alt="\lambda y:\sigma.P" class="ee_img tr_noresize" eeimg="1"> 的alpha变形使得 <img src="https://www.zhihu.com/equation?tex=z \notin FV(N)" alt="z \notin FV(N)" class="ee_img tr_noresize" eeimg="1"> .

此时我们有：

### 代换引理（Substitution Lemma）

设 <img src="https://www.zhihu.com/equation?tex=\Gamma',\ x:\sigma,\ \Gamma'' \vdash M:\tau" alt="\Gamma',\ x:\sigma,\ \Gamma'' \vdash M:\tau" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\Gamma' \vdash N:\sigma" alt="\Gamma' \vdash N:\sigma" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\Gamma',\Gamma'' \vdash M[x:=N]:\tau" alt="\Gamma',\Gamma'' \vdash M[x:=N]:\tau" class="ee_img tr_noresize" eeimg="1"> .

### 对 <img src="https://www.zhihu.com/equation?tex=\mathbb{\Lambda_T}" alt="\mathbb{\Lambda_T}" class="ee_img tr_noresize" eeimg="1"> 的单步beta归约（ <img src="https://www.zhihu.com/equation?tex=\to_\beta" alt="\to_\beta" class="ee_img tr_noresize" eeimg="1"> , for  <img src="https://www.zhihu.com/equation?tex=\mathbb{\Lambda_T}" alt="\mathbb{\Lambda_T}" class="ee_img tr_noresize" eeimg="1"> ）

1. (Basis)  <img src="https://www.zhihu.com/equation?tex=(\lambda x:\sigma.M)N\to_\beta M[x:=N]" alt="(\lambda x:\sigma.M)N\to_\beta M[x:=N]" class="ee_img tr_noresize" eeimg="1"> 
2. (Compatibility)同第一章定义

### Church–Rosser定理

在 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 上仍成立

### 主体归约引理（Subject Reduction）

若 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash \sigma : \rho" alt="\Gamma \vdash \sigma : \rho" class="ee_img tr_noresize" eeimg="1"> 且若 <img src="https://www.zhihu.com/equation?tex=L \twoheadrightarrow_\beta L'" alt="L \twoheadrightarrow_\beta L'" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\Gamma \vdash L':\rho" alt="\Gamma \vdash L':\rho" class="ee_img tr_noresize" eeimg="1"> .

即beta归约不影响类型性，且对项进行beta归约不影响项的类型. 

### 强标准定理/终止定理（Strong Normalisation Theorem/Termination Theorem）

所有合法的项 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 都是强标准化的.

## 结论

1.  <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中没有自应用（self-application）
2. Beta范式的存在性得以保证
3. 不是所有合法的项都有不动点