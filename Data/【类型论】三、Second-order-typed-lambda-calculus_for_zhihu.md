本文为*Type Theory and Formal Proof : An Introduction* 的笔记，纯个人向（

------

## 类型抽象和类型应用（Type-abstraction and type-application）

对于*抽象*这个过程，我们有项 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> ，其中可能有自由变量 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> ，假设 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=\sigma" alt="\sigma" class="ee_img tr_noresize" eeimg="1"> ，我们从 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 中抽象 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> ，可以得到项 <img src="https://www.zhihu.com/equation?tex=\lambda x : \sigma.M" alt="\lambda x : \sigma.M" class="ee_img tr_noresize" eeimg="1"> ，同时，所有在 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 中的自由变量 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> 被绑定了，我们说：

*项 <img src="https://www.zhihu.com/equation?tex=\lambda x:\sigma.M" alt="\lambda x:\sigma.M" class="ee_img tr_noresize" eeimg="1"> 依赖于项 <img src="https://www.zhihu.com/equation?tex=x" alt="x" class="ee_img tr_noresize" eeimg="1"> *.

因此， <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中可以构造**依赖于项的项**（terms depending on terms）.

相应的是*应用*，对于 <img src="https://www.zhihu.com/equation?tex=MN" alt="MN" class="ee_img tr_noresize" eeimg="1"> 的构造，我们可以把 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 应用到 <img src="https://www.zhihu.com/equation?tex=N" alt="N" class="ee_img tr_noresize" eeimg="1"> ，也得到一个项.

这称为*一阶*（first order）抽象，或一阶依赖，因为这个抽象是在项上进行的. 同时应用也是一阶的.

现在我们引入**依赖于类型的项**（terms depending on types），称*二阶*运算（*second order* operations）或二阶依赖（second order dependency）.

得到的这一系统称*二阶类型lambda演算（second order typed lambda calculus）*，或 <img src="https://www.zhihu.com/equation?tex=\lambda 2" alt="\lambda 2" class="ee_img tr_noresize" eeimg="1"> .

**例：**

首先考虑*恒等函数（identity function）*，在 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中并不存在，因为我们需要一个任意的类型 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> ，然后构造 <img src="https://www.zhihu.com/equation?tex=f \equiv \lambda x:\alpha .x" alt="f \equiv \lambda x:\alpha .x" class="ee_img tr_noresize" eeimg="1"> . 但这样，在应用一个自然数类型 <img src="https://www.zhihu.com/equation?tex=nat" alt="nat" class="ee_img tr_noresize" eeimg="1"> 的 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 时，我们不能构造 <img src="https://www.zhihu.com/equation?tex=fM" alt="fM" class="ee_img tr_noresize" eeimg="1"> ，因为 <img src="https://www.zhihu.com/equation?tex=\alpha \not \equiv nat" alt="\alpha \not \equiv nat" class="ee_img tr_noresize" eeimg="1"> ，类型不匹配. 

因此对于这样的万能类型，我们需要引入*另一层抽象*：

 <img src="https://www.zhihu.com/equation?tex=\lambda \alpha:*.\lambda x:\alpha.x" alt="\lambda \alpha:*.\lambda x:\alpha.x" class="ee_img tr_noresize" eeimg="1"> .

这里变量 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> 的类型引入新记号 <img src="https://www.zhihu.com/equation?tex=*" alt="*" class="ee_img tr_noresize" eeimg="1"> ，指*所有类型的类型（the type of all types）*.

此时 <img src="https://www.zhihu.com/equation?tex=\lambda \alpha:*.\lambda x:\alpha.x" alt="\lambda \alpha:*.\lambda x:\alpha.x" class="ee_img tr_noresize" eeimg="1"> 也是一个项，但是一个*依赖于类型的项（term depending on a type）*. 这里依赖的类型是 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> .

得到的这个项称为*多态（polymorphic）*恒等函数. 注意这还不是恒等函数本身，我们还需要进行一次（二阶）应用和Beta归约得到一个真正的恒等函数：

-  <img src="https://www.zhihu.com/equation?tex=(\lambda \alpha :*\ \lambda x:\alpha . x)nat \to_\beta \lambda x:nat.x" alt="(\lambda \alpha :*\ \lambda x:\alpha . x)nat \to_\beta \lambda x:nat.x" class="ee_img tr_noresize" eeimg="1"> ，为自然数上的恒等函数
-  <img src="https://www.zhihu.com/equation?tex=(\lambda \alpha :*\ \lambda x:\alpha . x)(nat\to bool) \to_\beta \lambda x:(nat\to bool).x" alt="(\lambda \alpha :*\ \lambda x:\alpha . x)(nat\to bool) \to_\beta \lambda x:(nat\to bool).x" class="ee_img tr_noresize" eeimg="1"> ，为 <img src="https://www.zhihu.com/equation?tex=nat\to bool" alt="nat\to bool" class="ee_img tr_noresize" eeimg="1"> 上的.

因此我们还需要增加二阶的抽象和应用，以及对于二阶项的Beta归约.

##  <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> 类型（ <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> -types）

我们引入*二阶lambda抽象（second order  <img src="https://www.zhihu.com/equation?tex=\lambda" alt="\lambda" class="ee_img tr_noresize" eeimg="1"> -abstraction）*或*类型抽象（type-abstraction）*，例如：

 <img src="https://www.zhihu.com/equation?tex=\lambda \alpha:*.\lambda x:\alpha.x" alt="\lambda \alpha:*.\lambda x:\alpha.x" class="ee_img tr_noresize" eeimg="1"> .

在 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中，我们猜想它的类型是：

 <img src="https://www.zhihu.com/equation?tex=\lambda \alpha:*.\lambda x:\alpha.x\quad:\quad*\to(\alpha\to \alpha)" alt="\lambda \alpha:*.\lambda x:\alpha.x\quad:\quad*\to(\alpha\to \alpha)" class="ee_img tr_noresize" eeimg="1"> .

然而问题是在上面的二阶表达式中，类型 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> 变成了一个绑定的变量，我们有理由认为 <img src="https://www.zhihu.com/equation?tex=\lambda \alpha:*.\lambda x:\alpha.x" alt="\lambda \alpha:*.\lambda x:\alpha.x" class="ee_img tr_noresize" eeimg="1"> 与 <img src="https://www.zhihu.com/equation?tex=\lambda \beta:*.\lambda x:\beta.x" alt="\lambda \beta:*.\lambda x:\beta.x" class="ee_img tr_noresize" eeimg="1"> 相同. 然而 <img src="https://www.zhihu.com/equation?tex=\lambda \alpha:*.\lambda x:\alpha.x:*\to(\alpha\to\alpha)" alt="\lambda \alpha:*.\lambda x:\alpha.x:*\to(\alpha\to\alpha)" class="ee_img tr_noresize" eeimg="1"> ，但 <img src="https://www.zhihu.com/equation?tex=\lambda \beta:*.\lambda x:\beta.x:*\to(\beta\to\beta)" alt="\lambda \beta:*.\lambda x:\beta.x:*\to(\beta\to\beta)" class="ee_img tr_noresize" eeimg="1"> ，相同的项有了不同的类型. 这是由于，我们认为左侧的 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\beta" alt="\beta" class="ee_img tr_noresize" eeimg="1"> 是绑定的变量，而右侧的是自由变量. 因此我们引入一种新绑定：*类型绑定（type-binder）*或* <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> 绑定（ <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> -binder）*. 一个将*任意*类型 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> 到类型为 <img src="https://www.zhihu.com/equation?tex=\alpha\to\alpha" alt="\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> 的函数的类型记作 <img src="https://www.zhihu.com/equation?tex=\Pi\alpha:*.\alpha\to\alpha" alt="\Pi\alpha:*.\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> .

我们简单推广 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> 变换，有 <img src="https://www.zhihu.com/equation?tex=\Pi\alpha:*.\alpha\to\alpha\equiv_\alpha\Pi\beta:*.\beta\to\beta" alt="\Pi\alpha:*.\alpha\to\alpha\equiv_\alpha\Pi\beta:*.\beta\to\beta" class="ee_img tr_noresize" eeimg="1"> . 此时我们有：

<img src="https://www.zhihu.com/equation?tex=\lambda \alpha:*.\lambda x:\alpha.x\quad:\quad\Pi\alpha:*\to(\alpha\to\alpha)\\

\equiv\quad\lambda \beta:*.\lambda x:\beta.x\quad:\quad\Pi\beta:*\to(\beta\to\beta)
" alt="\lambda \alpha:*.\lambda x:\alpha.x\quad:\quad\Pi\alpha:*\to(\alpha\to\alpha)\\

\equiv\quad\lambda \beta:*.\lambda x:\beta.x\quad:\quad\Pi\beta:*\to(\beta\to\beta)
" class="ee_img tr_noresize" eeimg="1">

> 在数学中， <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> 用于乘积，而 <img src="https://www.zhihu.com/equation?tex=\Pi" alt="\Pi" class="ee_img tr_noresize" eeimg="1"> 类型也称作积类型.

## 二阶抽象和应用法则（Second order abstraction and application rules）

### 二阶抽象法则（Second order abstraction rule）

 <img src="https://www.zhihu.com/equation?tex=(abst_2)\ \dfrac{\Gamma,\ \alpha:*\ \vdash\ M:A}{\Gamma\ \vdash\ \lambda \alpha:*.M\ :\ \Pi\alpha:*.A}" alt="(abst_2)\ \dfrac{\Gamma,\ \alpha:*\ \vdash\ M:A}{\Gamma\ \vdash\ \lambda \alpha:*.M\ :\ \Pi\alpha:*.A}" class="ee_img tr_noresize" eeimg="1"> 

当上下文中 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=A" alt="A" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=*" alt="*" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\lambda \alpha:\ *.\ M" alt="\lambda \alpha:\ *.\ M" class="ee_img tr_noresize" eeimg="1"> 有类型 <img src="https://www.zhihu.com/equation?tex=\Pi\alpha:*\ .A" alt="\Pi\alpha:*\ .A" class="ee_img tr_noresize" eeimg="1"> . 新的地方是：我们允许二阶声明在上下文中.

### 二阶应用法则（Second order application rule）

 <img src="https://www.zhihu.com/equation?tex=(appl_2)\ \dfrac{\Gamma\ \vdash\ M\ :\ \Pi\alpha:*.\ A\qquad\Gamma\ \vdash\ B:*}{\Gamma\ \vdash\ MB\ :\ A[\alpha:=B]}" alt="(appl_2)\ \dfrac{\Gamma\ \vdash\ M\ :\ \Pi\alpha:*.\ A\qquad\Gamma\ \vdash\ B:*}{\Gamma\ \vdash\ MB\ :\ A[\alpha:=B]}" class="ee_img tr_noresize" eeimg="1"> 

##  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 系统（The system  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> ）

以下是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 的完整定义：

###  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 类型（ <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> -types）

 <img src="https://www.zhihu.com/equation?tex=\mathbb{T2=V|(T2\to T2)|(\Pi V:*.T2)}" alt="\mathbb{T2=V|(T2\to T2)|(\Pi V:*.T2)}" class="ee_img tr_noresize" eeimg="1"> ，其中 <img src="https://www.zhihu.com/equation?tex=\mathbb{V}" alt="\mathbb{V}" class="ee_img tr_noresize" eeimg="1"> 是类型变量集合.

### 二阶预定型项（Second order pre-typed  <img src="https://www.zhihu.com/equation?tex=\lambda" alt="\lambda" class="ee_img tr_noresize" eeimg="1"> -terms,  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> -terms,  <img src="https://www.zhihu.com/equation?tex=\Lambda_\mathbb{T2}" alt="\Lambda_\mathbb{T2}" class="ee_img tr_noresize" eeimg="1"> ）

$\mathbb{\Lambda_{T2}}=
V|

(\mathbb{\Lambda_{T2}\Lambda_{T2}})|

(\Lambda_\mathbb{T2}\mathbb{T2})|

(\lambda V:\mathbb{T2.\Lambda_{T2}})|

(\lambda\mathbb{V}:*.\Lambda_\mathbb{T2})$.

此时我们有两种变量：对象变量（object variables） <img src="https://www.zhihu.com/equation?tex=V" alt="V" class="ee_img tr_noresize" eeimg="1"> （如 <img src="https://www.zhihu.com/equation?tex=x,\ y,\ \dots" alt="x,\ y,\ \dots" class="ee_img tr_noresize" eeimg="1"> ）和类型变量（type variables） <img src="https://www.zhihu.com/equation?tex=\mathbb{V}" alt="\mathbb{V}" class="ee_img tr_noresize" eeimg="1"> （如 <img src="https://www.zhihu.com/equation?tex=\alpha,\ \beta,\ \dots" alt="\alpha,\ \beta,\ \dots" class="ee_img tr_noresize" eeimg="1"> ）. 我们有一阶抽象 <img src="https://www.zhihu.com/equation?tex=(\lambda V:\mathbb{T2.\Lambda_{T2}})" alt="(\lambda V:\mathbb{T2.\Lambda_{T2}})" class="ee_img tr_noresize" eeimg="1"> 和二阶抽象 <img src="https://www.zhihu.com/equation?tex=(\lambda\mathbb{V}:*.\Lambda_\mathbb{T2})" alt="(\lambda\mathbb{V}:*.\Lambda_\mathbb{T2})" class="ee_img tr_noresize" eeimg="1"> ，一阶应用 <img src="https://www.zhihu.com/equation?tex=(\mathbb{\Lambda_{T2}\Lambda_{T2}})" alt="(\mathbb{\Lambda_{T2}\Lambda_{T2}})" class="ee_img tr_noresize" eeimg="1"> 和二阶应用 <img src="https://www.zhihu.com/equation?tex=(\Lambda_\mathbb{T2}\mathbb{T2})" alt="(\Lambda_\mathbb{T2}\mathbb{T2})" class="ee_img tr_noresize" eeimg="1"> .

### 陈述，声明（Statement, declaration）

1. *陈述（statement）*要么形如 <img src="https://www.zhihu.com/equation?tex=M:\sigma" alt="M:\sigma" class="ee_img tr_noresize" eeimg="1"> ，其中 <img src="https://www.zhihu.com/equation?tex=M\in\Lambda_\mathbb{T2}" alt="M\in\Lambda_\mathbb{T2}" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\sigma:\mathbb{T2}" alt="\sigma:\mathbb{T2}" class="ee_img tr_noresize" eeimg="1"> ，要么形如 <img src="https://www.zhihu.com/equation?tex=\sigma:*" alt="\sigma:*" class="ee_img tr_noresize" eeimg="1"> ，其中 <img src="https://www.zhihu.com/equation?tex=\sigma \in \mathbb{T2}" alt="\sigma \in \mathbb{T2}" class="ee_img tr_noresize" eeimg="1"> .
2. *声明（declaration）*是一个以*项变量（type variable）*或*类型变量（term variable）*为主体的陈述.

在 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中，*上下文*只是一个项声明的列表. 在 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 中，所有变量在被使用之前必须声明. 所以，类型变量 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> （具有类型 <img src="https://www.zhihu.com/equation?tex=*" alt="*" class="ee_img tr_noresize" eeimg="1"> ）这个声明必须先于 <img src="https://www.zhihu.com/equation?tex=x:\alpha\to\alpha" alt="x:\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> 这个声明. 

###  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文、定义域（ <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> -context; domain;  <img src="https://www.zhihu.com/equation?tex={\rm dom}" alt="{\rm dom}" class="ee_img tr_noresize" eeimg="1"> ）

1.  <img src="https://www.zhihu.com/equation?tex=\emptyset" alt="\emptyset" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文； <img src="https://www.zhihu.com/equation?tex={\rm dom(\emptyset)}=(\ )" alt="{\rm dom(\emptyset)}=(\ )" class="ee_img tr_noresize" eeimg="1"> ，为空列表.
2. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文， <img src="https://www.zhihu.com/equation?tex=\alpha\in\mathbb{V}" alt="\alpha\in\mathbb{V}" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=\alpha\not\in{\rm dom}(\Gamma)" alt="\alpha\not\in{\rm dom}(\Gamma)" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\Gamma,\ \alpha:*" alt="\Gamma,\ \alpha:*" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文.
3. 若 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文，若 <img src="https://www.zhihu.com/equation?tex=\rho \in \mathbb{T2}" alt="\rho \in \mathbb{T2}" class="ee_img tr_noresize" eeimg="1"> 使得对 <img src="https://www.zhihu.com/equation?tex=\rho" alt="\rho" class="ee_img tr_noresize" eeimg="1"> 中的所有自由变量 <img src="https://www.zhihu.com/equation?tex=\alpha" alt="\alpha" class="ee_img tr_noresize" eeimg="1"> 都有 <img src="https://www.zhihu.com/equation?tex=\alpha \in {\rm dom}(\Gamma)" alt="\alpha \in {\rm dom}(\Gamma)" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=x \not \in {\rm dom}(\Gamma)" alt="x \not \in {\rm dom}(\Gamma)" class="ee_img tr_noresize" eeimg="1"> ，则 <img src="https://www.zhihu.com/equation?tex=\Gamma,\ x:\rho" alt="\Gamma,\ x:\rho" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文.

> 此定义中蕴含了 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文中的变量互不相同.

###  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 的 <img src="https://www.zhihu.com/equation?tex=(var)" alt="(var)" class="ee_img tr_noresize" eeimg="1"> 法则（Var-rule for  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> ）

 <img src="https://www.zhihu.com/equation?tex=(var)\quad \Gamma \vdash x:\sigma" alt="(var)\quad \Gamma \vdash x:\sigma" class="ee_img tr_noresize" eeimg="1"> ，如果 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文且 <img src="https://www.zhihu.com/equation?tex=x:\sigma\in\Gamma" alt="x:\sigma\in\Gamma" class="ee_img tr_noresize" eeimg="1"> .

 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 的 <img src="https://www.zhihu.com/equation?tex=(var)" alt="(var)" class="ee_img tr_noresize" eeimg="1"> 法则也是没有**前提**的.

对于 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 的派生，我们现在有复用 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1"> 中的 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> ，刚刚定义的 <img src="https://www.zhihu.com/equation?tex=(var)" alt="(var)" class="ee_img tr_noresize" eeimg="1"> 和新加入的 <img src="https://www.zhihu.com/equation?tex=(appl_2)" alt="(appl_2)" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=(abst_2)" alt="(abst_2)" class="ee_img tr_noresize" eeimg="1"> .

然而当使用这五条法则时，我们将无法使用到 <img src="https://www.zhihu.com/equation?tex=(appl_2)" alt="(appl_2)" class="ee_img tr_noresize" eeimg="1"> 法则，因为它的第二个**前提**是 <img src="https://www.zhihu.com/equation?tex=\Gamma\ \vdash\ B:*" alt="\Gamma\ \vdash\ B:*" class="ee_img tr_noresize" eeimg="1"> ，而我们没有规则使得有东西具有类型 <img src="https://www.zhihu.com/equation?tex=*" alt="*" class="ee_img tr_noresize" eeimg="1"> （没有形如 <img src="https://www.zhihu.com/equation?tex=\dots\ \vdash\ \dots\ :\ *" alt="\dots\ \vdash\ \dots\ :\ *" class="ee_img tr_noresize" eeimg="1"> 的**结论**）.

直觉告诉我们， <img src="https://www.zhihu.com/equation?tex=B:*" alt="B:*" class="ee_img tr_noresize" eeimg="1"> ，只要 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 是个类型且我们已知所有 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 中的类型变量，因此有：

###  <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> 法则（Formation rule）

 <img src="https://www.zhihu.com/equation?tex=(form)\quad\Gamma\ \vdash\ B:*" alt="(form)\quad\Gamma\ \vdash\ B:*" class="ee_img tr_noresize" eeimg="1"> ，如果 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文， <img src="https://www.zhihu.com/equation?tex=B\in\mathbb{T2}" alt="B\in\mathbb{T2}" class="ee_img tr_noresize" eeimg="1"> 且所有在 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 中的自由类型变量都在 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 有声明.

>  <img src="https://www.zhihu.com/equation?tex=(form)" alt="(form)" class="ee_img tr_noresize" eeimg="1"> 法则虽然有三个条件，但也没有**前提**，可以作为派生树的叶子

于是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 的所有派生法则：

 <img src="https://www.zhihu.com/equation?tex=(var)\quad \Gamma \vdash x:\sigma" alt="(var)\quad \Gamma \vdash x:\sigma" class="ee_img tr_noresize" eeimg="1"> ，如果 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文且 <img src="https://www.zhihu.com/equation?tex=x:\sigma\in\Gamma" alt="x:\sigma\in\Gamma" class="ee_img tr_noresize" eeimg="1"> .

 <img src="https://www.zhihu.com/equation?tex=(appl)\ \dfrac{\Gamma\ \vdash\ M:\sigma\to\tau\quad\Gamma\ \vdash\ N:\sigma}{\Gamma\ \vdash\ MN:\tau}" alt="(appl)\ \dfrac{\Gamma\ \vdash\ M:\sigma\to\tau\quad\Gamma\ \vdash\ N:\sigma}{\Gamma\ \vdash\ MN:\tau}" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(abst)\ \dfrac{\Gamma,\ x:\sigma\ \vdash\ M:\tau}{\Gamma\ \vdash\ \lambda x:\sigma.\ M\ :\ \sigma\to\tau}" alt="(abst)\ \dfrac{\Gamma,\ x:\sigma\ \vdash\ M:\tau}{\Gamma\ \vdash\ \lambda x:\sigma.\ M\ :\ \sigma\to\tau}" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(form)\quad\Gamma\ \vdash\ B:*" alt="(form)\quad\Gamma\ \vdash\ B:*" class="ee_img tr_noresize" eeimg="1"> ，如果 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文， <img src="https://www.zhihu.com/equation?tex=B\in\mathbb{T2}" alt="B\in\mathbb{T2}" class="ee_img tr_noresize" eeimg="1"> 且所有在 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 中的自由类型变量都在 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 有声明.

 <img src="https://www.zhihu.com/equation?tex=(appl_2)\ \dfrac{\Gamma\ \vdash\ M\ :\ \Pi\alpha:*.\ A\qquad\Gamma\ \vdash\ B:*}{\Gamma\ \vdash\ MB\ :\ A[\alpha:=B]}" alt="(appl_2)\ \dfrac{\Gamma\ \vdash\ M\ :\ \Pi\alpha:*.\ A\qquad\Gamma\ \vdash\ B:*}{\Gamma\ \vdash\ MB\ :\ A[\alpha:=B]}" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(abst_2)\ \dfrac{\Gamma,\ \alpha:*\ \vdash\ M:A}{\Gamma\ \vdash\ \lambda \alpha:*.M\ :\ \Pi\alpha:*.A}" alt="(abst_2)\ \dfrac{\Gamma,\ \alpha:*\ \vdash\ M:A}{\Gamma\ \vdash\ \lambda \alpha:*.M\ :\ \Pi\alpha:*.A}" class="ee_img tr_noresize" eeimg="1"> 

### 合法的 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 项（Legal  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> -terms）

称 <img src="https://www.zhihu.com/equation?tex=\mathbb{\Lambda_{T2}}" alt="\mathbb{\Lambda_{T2}}" class="ee_img tr_noresize" eeimg="1"> 中的项 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> *合法*（legal），若存在 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\mathbb{T2}" alt="\mathbb{T2}" class="ee_img tr_noresize" eeimg="1"> 类型 <img src="https://www.zhihu.com/equation?tex=\rho" alt="\rho" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash M:\rho" alt="\Gamma\vdash M:\rho" class="ee_img tr_noresize" eeimg="1"> .

##  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 中的派生例

试图派生 <img src="https://www.zhihu.com/equation?tex=M\equiv\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)" alt="M\equiv\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)" class="ee_img tr_noresize" eeimg="1"> .

即找到上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> 和类型 <img src="https://www.zhihu.com/equation?tex=\rho" alt="\rho" class="ee_img tr_noresize" eeimg="1"> 使得 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash M:\rho" alt="\Gamma\vdash M:\rho" class="ee_img tr_noresize" eeimg="1"> . 因为 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 没有自由项或类型变量，所有可以取 <img src="https://www.zhihu.com/equation?tex=\Gamma\equiv\emptyset" alt="\Gamma\equiv\emptyset" class="ee_img tr_noresize" eeimg="1"> ，于是：

 <img src="https://www.zhihu.com/equation?tex=(n)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\quad:\quad?" alt="(n)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\quad:\quad?" class="ee_img tr_noresize" eeimg="1"> 

下一个定型的项是“二阶 <img src="https://www.zhihu.com/equation?tex=\lambda" alt="\lambda" class="ee_img tr_noresize" eeimg="1"> ”，因此使用 <img src="https://www.zhihu.com/equation?tex=(abst_2)" alt="(abst_2)" class="ee_img tr_noresize" eeimg="1"> .

 <img src="https://www.zhihu.com/equation?tex=(m)\quad \alpha:*\ \vdash\ \lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ ?" alt="(m)\quad \alpha:*\ \vdash\ \lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ ?" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ \dots\quad对(m)用(abst_2)" alt="(n)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ \dots\quad对(m)用(abst_2)" class="ee_img tr_noresize" eeimg="1"> 

新的目标是 <img src="https://www.zhihu.com/equation?tex=\lambda f:\alpha\to\alpha.\ \dots" alt="\lambda f:\alpha\to\alpha.\ \dots" class="ee_img tr_noresize" eeimg="1"> ，是个普通的一阶抽象，使用 <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=(k)\quad\alpha:*,\ f:\alpha\to\alpha,\ x:\alpha\ \vdash\ f(fx)\ :\ ?" alt="(k)\quad\alpha:*,\ f:\alpha\to\alpha,\ x:\alpha\ \vdash\ f(fx)\ :\ ?" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(l)\quad\alpha:*,\ f:\alpha\to\alpha\ \vdash\ \lambda x:\alpha.f(fx)\ :\ \dots\quad对（k）用(abst)" alt="(l)\quad\alpha:*,\ f:\alpha\to\alpha\ \vdash\ \lambda x:\alpha.f(fx)\ :\ \dots\quad对（k）用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(m)\quad\alpha:*\ \vdash\ \lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx)\ :\ \dots\quad对(l)用(abst)" alt="(m)\quad\alpha:*\ \vdash\ \lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx)\ :\ \dots\quad对(l)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(n)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ \dots\quad对(m)用(abst_2)" alt="(n)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ \dots\quad对(m)用(abst_2)" class="ee_img tr_noresize" eeimg="1"> 

剩下的就是一个 <img src="https://www.zhihu.com/equation?tex=\lambda{\to}" alt="\lambda{\to}" class="ee_img tr_noresize" eeimg="1">  的定型问题，于是给出简略版本：

 <img src="https://www.zhihu.com/equation?tex=(1)\quad\alpha:*,\ f:\alpha\to\alpha,\ x:\alpha\ \vdash\ fx\ :\ \alpha" alt="(1)\quad\alpha:*,\ f:\alpha\to\alpha,\ x:\alpha\ \vdash\ fx\ :\ \alpha" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(2)\quad\alpha:*,\ f:\alpha\to\alpha,\ x:\alpha\ \vdash\ f(fx)\ :\ \alpha" alt="(2)\quad\alpha:*,\ f:\alpha\to\alpha,\ x:\alpha\ \vdash\ f(fx)\ :\ \alpha" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(3)\quad\alpha:*,\ f:\alpha\to\alpha\ \vdash\ \lambda x:\alpha.f(fx)\ :\ type_1\quad对（2）用(abst)" alt="(3)\quad\alpha:*,\ f:\alpha\to\alpha\ \vdash\ \lambda x:\alpha.f(fx)\ :\ type_1\quad对（2）用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(4)\quad\alpha:*\ \vdash\ \lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx)\ :\ type_2\quad对(3)用(abst)" alt="(4)\quad\alpha:*\ \vdash\ \lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx)\ :\ type_2\quad对(3)用(abst)" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=(5)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ type_3\quad对(4)用(abst_2)" alt="(5)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ type_3\quad对(4)用(abst_2)" class="ee_img tr_noresize" eeimg="1"> 

最后填入 <img src="https://www.zhihu.com/equation?tex=type_1" alt="type_1" class="ee_img tr_noresize" eeimg="1"> ， <img src="https://www.zhihu.com/equation?tex=type_2" alt="type_2" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=type_3" alt="type_3" class="ee_img tr_noresize" eeimg="1"> ，使用 <img src="https://www.zhihu.com/equation?tex=(abst)" alt="(abst)" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=(abst_2)" alt="(abst_2)" class="ee_img tr_noresize" eeimg="1"> 法则：

 <img src="https://www.zhihu.com/equation?tex=type_1\equiv\alpha\to\alpha" alt="type_1\equiv\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=type_2\equiv(\alpha\to\alpha)\to\alpha\to\alpha" alt="type_2\equiv(\alpha\to\alpha)\to\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> 

 <img src="https://www.zhihu.com/equation?tex=type_3\equiv\Pi\alpha:*.(\alpha\to\alpha)\to\alpha\to\alpha" alt="type_3\equiv\Pi\alpha:*.(\alpha\to\alpha)\to\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> 

填入第五行，结论是：

 <img src="https://www.zhihu.com/equation?tex=(5)\quad\emptyset\vdash\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx):\Pi\alpha:*.(\alpha\to\alpha)\to\alpha\to\alpha" alt="(5)\quad\emptyset\vdash\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx):\Pi\alpha:*.(\alpha\to\alpha)\to\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> .

由Thinning引理（见下一节），我们可以得到，对于所有 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文 <img src="https://www.zhihu.com/equation?tex=\Gamma" alt="\Gamma" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=(6)\quad\Gamma\vdash\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx):\Pi\alpha:*.(\alpha\to\alpha)\to\alpha\to\alpha" alt="(6)\quad\Gamma\vdash\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx):\Pi\alpha:*.(\alpha\to\alpha)\to\alpha\to\alpha" class="ee_img tr_noresize" eeimg="1"> .

假设我们有类型 <img src="https://www.zhihu.com/equation?tex=nat" alt="nat" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=(7)\quad\Gamma\vdash nat:*" alt="(7)\quad\Gamma\vdash nat:*" class="ee_img tr_noresize" eeimg="1"> 

有 <img src="https://www.zhihu.com/equation?tex=(6)" alt="(6)" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=(7)" alt="(7)" class="ee_img tr_noresize" eeimg="1"> 用 <img src="https://www.zhihu.com/equation?tex=(appl_2)" alt="(appl_2)" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=(8)\quad\Gamma\vdash(\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx))\ nat:(nat\to nat)\to nat\to nat" alt="(8)\quad\Gamma\vdash(\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx))\ nat:(nat\to nat)\to nat\to nat" class="ee_img tr_noresize" eeimg="1"> .

假设有：

 <img src="https://www.zhihu.com/equation?tex=(9)\quad\Gamma\vdash suc\ :\ nat\to nat" alt="(9)\quad\Gamma\vdash suc\ :\ nat\to nat" class="ee_img tr_noresize" eeimg="1"> ，

对 <img src="https://www.zhihu.com/equation?tex=(8)" alt="(8)" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=(9)" alt="(9)" class="ee_img tr_noresize" eeimg="1"> 用 <img src="https://www.zhihu.com/equation?tex=(appl)" alt="(appl)" class="ee_img tr_noresize" eeimg="1"> ：

 <img src="https://www.zhihu.com/equation?tex=(10)\quad\Gamma\vdash(\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx))\ nat \ suc:nat\to nat" alt="(10)\quad\Gamma\vdash(\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx))\ nat \ suc:nat\to nat" class="ee_img tr_noresize" eeimg="1"> .

有 <img src="https://www.zhihu.com/equation?tex=\Gamma\vdash two:nat" alt="\Gamma\vdash two:nat" class="ee_img tr_noresize" eeimg="1"> ，得到：

 <img src="https://www.zhihu.com/equation?tex=(11)\quad\Gamma\vdash(\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx))\ nat \ suc\ two:nat" alt="(11)\quad\Gamma\vdash(\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx))\ nat \ suc\ two:nat" class="ee_img tr_noresize" eeimg="1"> .

##  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 的性质

### Alpha替换/Alpha等价推广（α-conversion/α-equivalence, extended）

（1a）项变量重命名

 <img src="https://www.zhihu.com/equation?tex=\lambda x:\sigma.M=_\alpha\lambda y:\sigma.M^{x\to y}" alt="\lambda x:\sigma.M=_\alpha\lambda y:\sigma.M^{x\to y}" class="ee_img tr_noresize" eeimg="1"> 如果 <img src="https://www.zhihu.com/equation?tex=y \not\in FV(M)" alt="y \not\in FV(M)" class="ee_img tr_noresize" eeimg="1"> 且 <img src="https://www.zhihu.com/equation?tex=y" alt="y" class="ee_img tr_noresize" eeimg="1"> 不是 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 中的绑定变量.

（1b）类型变量重命名

 <img src="https://www.zhihu.com/equation?tex=\lambda \alpha:*.M=_\alpha \lambda\beta:*.M[\alpha:=\beta]" alt="\lambda \alpha:*.M=_\alpha \lambda\beta:*.M[\alpha:=\beta]" class="ee_img tr_noresize" eeimg="1"> 如果 <img src="https://www.zhihu.com/equation?tex=\beta" alt="\beta" class="ee_img tr_noresize" eeimg="1"> 不在 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 中出现，

 <img src="https://www.zhihu.com/equation?tex=\Pi\alpha:*.M=_\alpha\Pi\beta:*.M[\alpha:=\beta]" alt="\Pi\alpha:*.M=_\alpha\Pi\beta:*.M[\alpha:=\beta]" class="ee_img tr_noresize" eeimg="1"> 如果 <img src="https://www.zhihu.com/equation?tex=\beta" alt="\beta" class="ee_img tr_noresize" eeimg="1"> 不在 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 中出现.

###  <img src="https://www.zhihu.com/equation?tex=\mathbb{\Lambda_2}" alt="\mathbb{\Lambda_2}" class="ee_img tr_noresize" eeimg="1"> 项的单步Beta归约（One-step  <img src="https://www.zhihu.com/equation?tex=\beta" alt="\beta" class="ee_img tr_noresize" eeimg="1"> -reduction,  <img src="https://www.zhihu.com/equation?tex=\to_\beta" alt="\to_\beta" class="ee_img tr_noresize" eeimg="1"> for  <img src="https://www.zhihu.com/equation?tex=\mathbb{\Lambda_2}" alt="\mathbb{\Lambda_2}" class="ee_img tr_noresize" eeimg="1"> -terms）

（1a）一阶： <img src="https://www.zhihu.com/equation?tex=(\lambda x:\sigma.M)N\to_\beta M[x:=N]" alt="(\lambda x:\sigma.M)N\to_\beta M[x:=N]" class="ee_img tr_noresize" eeimg="1"> 

（1b）二阶： <img src="https://www.zhihu.com/equation?tex=(\lambda \alpha:*.M)T\to_\beta M[\alpha:=T]" alt="(\lambda \alpha:*.M)T\to_\beta M[\alpha:=T]" class="ee_img tr_noresize" eeimg="1"> 

###  <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 中依然成立的引理

- Free Variables Lemma
- Thinning Lemma
- Condensing Lemma
- Generation Lemma
- Subterm Lemma
- Uniqueness of Types
- Substitution Lemma
- Church–Rosser Theorem
- Subject Reduction
- Strong Normalisation Theorem

注意唯一不适用的引理是Permutation Lemma，因为对于上下文，后出现的声明可能依赖于前面的。而如果我们改成定义中的 <img src="https://www.zhihu.com/equation?tex=\lambda2" alt="\lambda2" class="ee_img tr_noresize" eeimg="1"> 上下文，则就仍然成立.

