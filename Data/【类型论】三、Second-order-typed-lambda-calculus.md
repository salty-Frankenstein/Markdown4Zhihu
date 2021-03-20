本文为*Type Theory and Formal Proof : An Introduction* 的笔记，纯个人向（

------

## 类型抽象和类型应用（Type-abstraction and type-application）

对于*抽象*这个过程，我们有项$M$，其中可能有自由变量$x$，假设$x$有类型$\sigma$，我们从$M$中抽象$x$，可以得到项$\lambda x : \sigma.M$，同时，所有在$M$中的自由变量$x$被绑定了，我们说：

*项$\lambda x:\sigma.M$依赖于项$x$*.

因此，$\lambda{\to}$中可以构造**依赖于项的项**（terms depending on terms）.

相应的是*应用*，对于$MN$的构造，我们可以把$M$应用到$N$，也得到一个项.

这称为*一阶*（first order）抽象，或一阶依赖，因为这个抽象是在项上进行的. 同时应用也是一阶的.

现在我们引入**依赖于类型的项**（terms depending on types），称*二阶*运算（*second order* operations）或二阶依赖（second order dependency）.

得到的这一系统称*二阶类型lambda演算（second order typed lambda calculus）*，或$\lambda 2$.

**例：**

首先考虑*恒等函数（identity function）*，在$\lambda{\to}$中并不存在，因为我们需要一个任意的类型$\alpha$，然后构造$f \equiv \lambda x:\alpha .x$. 但这样，在应用一个自然数类型$nat$的$M$时，我们不能构造$fM$，因为$\alpha \not \equiv nat$，类型不匹配. 

因此对于这样的万能类型，我们需要引入*另一层抽象*：

$\lambda \alpha:*.\lambda x:\alpha.x$.

这里变量$\alpha$的类型引入新记号$*$，指*所有类型的类型（the type of all types）*.

此时$\lambda \alpha:*.\lambda x:\alpha.x$也是一个项，但是一个*依赖于类型的项（term depending on a type）*. 这里依赖的类型是$\alpha$.

得到的这个项称为*多态（polymorphic）*恒等函数. 注意这还不是恒等函数本身，我们还需要进行一次（二阶）应用和Beta归约得到一个真正的恒等函数：

- $(\lambda \alpha :*\ \lambda x:\alpha . x)nat \to_\beta \lambda x:nat.x$，为自然数上的恒等函数
- $(\lambda \alpha :*\ \lambda x:\alpha . x)(nat\to bool) \to_\beta \lambda x:(nat\to bool).x$，为$nat\to bool$上的.

因此我们还需要增加二阶的抽象和应用，以及对于二阶项的Beta归约.

## $\Pi$类型（$\Pi$-types）

我们引入*二阶lambda抽象（second order $\lambda$-abstraction）*或*类型抽象（type-abstraction）*，例如：

$\lambda \alpha:*.\lambda x:\alpha.x$.

在$\lambda{\to}$中，我们猜想它的类型是：

$\lambda \alpha:*.\lambda x:\alpha.x\quad:\quad*\to(\alpha\to \alpha)$.

然而问题是在上面的二阶表达式中，类型$\alpha$变成了一个绑定的变量，我们有理由认为$\lambda \alpha:*.\lambda x:\alpha.x$与$\lambda \beta:*.\lambda x:\beta.x$相同. 然而$\lambda \alpha:*.\lambda x:\alpha.x:*\to(\alpha\to\alpha)$，但$\lambda \beta:*.\lambda x:\beta.x:*\to(\beta\to\beta)$，相同的项有了不同的类型. 这是由于，我们认为左侧的$\alpha$和$\beta$是绑定的变量，而右侧的是自由变量. 因此我们引入一种新绑定：*类型绑定（type-binder）* 或 $\Pi$*绑定*（$\Pi$*-binder*）. 一个将*任意*类型$\alpha$到类型为$\alpha\to\alpha$的函数的类型记作$\Pi\alpha:*.\alpha\to\alpha$.

我们简单推广$\alpha$变换，有$\Pi\alpha:*.\alpha\to\alpha\equiv_\alpha\Pi\beta:*.\beta\to\beta$. 此时我们有：
$$
\lambda \alpha:*.\lambda x:\alpha.x\quad:\quad\Pi\alpha:*\to(\alpha\to\alpha)\\

\equiv\quad\lambda \beta:*.\lambda x:\beta.x\quad:\quad\Pi\beta:*\to(\beta\to\beta)
$$

> 在数学中，$\Pi$用于乘积，而$\Pi$类型也称作积类型.

## 二阶抽象和应用法则（Second order abstraction and application rules）

### 二阶抽象法则（Second order abstraction rule）

$(abst_2)\ \dfrac{\Gamma,\ \alpha:*\ \vdash\ M:A}{\Gamma\ \vdash\ \lambda \alpha:*.M\ :\ \Pi\alpha:*.A}$

当上下文中$M$有类型$A$且$\alpha$有类型$*$，则$\lambda \alpha:\ *.\ M$有类型$\Pi\alpha:*\ .A$. 新的地方是：我们允许二阶声明在上下文中.

### 二阶应用法则（Second order application rule）

$(appl_2)\ \dfrac{\Gamma\ \vdash\ M\ :\ \Pi\alpha:*.\ A\qquad\Gamma\ \vdash\ B:*}{\Gamma\ \vdash\ MB\ :\ A[\alpha:=B]}$

## $\lambda2$系统（The system $\lambda2$）

以下是$\lambda2$的完整定义：

### $\lambda2$类型（$\lambda2$-types）

$\mathbb{T2=V|(T2\to T2)|(\Pi V:*.T2)}$，其中$\mathbb{V}$是类型变量集合.

### 二阶预定型项（Second order pre-typed $\lambda$-terms, $\lambda2$-terms, $\Lambda_\mathbb{T2}$）

$\mathbb{\Lambda_{T2}}=V|(\mathbb{\Lambda_{T2}\Lambda_{T2}})|(\Lambda_\mathbb{T2}\mathbb{T2})|(\lambda V:\mathbb{T2.\Lambda_{T2}})|(\lambda\mathbb{V}:*.\Lambda_\mathbb{T2})$.

此时我们有两种变量：对象变量（object variables）$V$（如$x,\ y,\ \dots$）和类型变量（type variables）$\mathbb{V}$（如$\alpha,\ \beta,\ \dots$）. 我们有一阶抽象$(\lambda V:\mathbb{T2.\Lambda_{T2}})$和二阶抽象$(\lambda\mathbb{V}:*.\Lambda_\mathbb{T2})$，一阶应用$(\mathbb{\Lambda_{T2}\Lambda_{T2}})$和二阶应用$(\Lambda_\mathbb{T2}\mathbb{T2})$.

### 陈述，声明（Statement, declaration）

1. *陈述（statement）*要么形如$M:\sigma$，其中$M\in\Lambda_\mathbb{T2}$且$\sigma:\mathbb{T2}$，要么形如$\sigma:*$，其中$\sigma \in \mathbb{T2}$.
2. *声明（declaration）*是一个以*项变量（type variable）*或*类型变量（term variable）*为主体的陈述.

在$\lambda{\to}$中，*上下文*只是一个项声明的列表. 在$\lambda2$中，所有变量在被使用之前必须声明. 所以，类型变量$\alpha$（具有类型$*$）这个声明必须先于$x:\alpha\to\alpha$这个声明. 

### $\lambda2$上下文、定义域（$\lambda2$-context; domain; ${\rm dom}$）

1. $\emptyset$是$\lambda2$上下文；${\rm dom(\emptyset)}=(\ )$，为空列表.
2. 若$\Gamma$是$\lambda2$上下文，$\alpha\in\mathbb{V}$且$\alpha\not\in{\rm dom}(\Gamma)$，则$\Gamma,\ \alpha:*$是$\lambda2$上下文.
3. 若$\Gamma$是$\lambda2$上下文，若$\rho \in \mathbb{T2}$使得对$\rho$中的所有自由变量$\alpha$都有$\alpha \in {\rm dom}(\Gamma)$且$x \not \in {\rm dom}(\Gamma)$，则$\Gamma,\ x:\rho$是$\lambda2$上下文.

> 此定义中蕴含了$\lambda2$上下文中的变量互不相同.

### $\lambda2$的$(var)$法则（Var-rule for $\lambda2$）

$(var)\quad \Gamma \vdash x:\sigma$，如果$\Gamma$是$\lambda2$上下文且$x:\sigma\in\Gamma$.

$\lambda2$的$(var)$法则也是没有**前提**的.

对于$\lambda2$的派生，我们现在有复用$\lambda{\to}$中的$(appl)$和$(abst)$，刚刚定义的$(var)$和新加入的$(appl_2)$和$(abst_2)$.

然而当使用这五条法则时，我们将无法使用到$(appl_2)$法则，因为它的第二个**前提**是$\Gamma\ \vdash\ B:*$，而我们没有规则使得有东西具有类型$*$（没有形如$\dots\ \vdash\ \dots\ :\ *$的**结论**）.

直觉告诉我们，$B:*$，只要$B$是个类型且我们已知所有$B$中的类型变量，因此有：

### $(form)$法则（Formation rule）

$(form)\quad\Gamma\ \vdash\ B:*$，如果$\Gamma$是$\lambda2$上下文，$B\in\mathbb{T2}$且所有在$B$中的自由类型变量都在$\Gamma$有声明.

> $(form)$法则虽然有三个条件，但也没有**前提**，可以作为派生树的叶子

于是$\lambda2$的所有派生法则：

$(var)\quad \Gamma \vdash x:\sigma$，如果$\Gamma$是$\lambda2$上下文且$x:\sigma\in\Gamma$.

$(appl)\ \dfrac{\Gamma\ \vdash\ M:\sigma\to\tau\quad\Gamma\ \vdash\ N:\sigma}{\Gamma\ \vdash\ MN:\tau}$

$(abst)\ \dfrac{\Gamma,\ x:\sigma\ \vdash\ M:\tau}{\Gamma\ \vdash\ \lambda x:\sigma.\ M\ :\ \sigma\to\tau}$

$(form)\quad\Gamma\ \vdash\ B:*$，如果$\Gamma$是$\lambda2$上下文，$B\in\mathbb{T2}$且所有在$B$中的自由类型变量都在$\Gamma$有声明.

$(appl_2)\ \dfrac{\Gamma\ \vdash\ M\ :\ \Pi\alpha:*.\ A\qquad\Gamma\ \vdash\ B:*}{\Gamma\ \vdash\ MB\ :\ A[\alpha:=B]}$

$(abst_2)\ \dfrac{\Gamma,\ \alpha:*\ \vdash\ M:A}{\Gamma\ \vdash\ \lambda \alpha:*.M\ :\ \Pi\alpha:*.A}$

### 合法的$\lambda2$项（Legal $\lambda2$-terms）

称$\mathbb{\Lambda_{T2}}$中的项$M$*合法*（legal），若存在$\lambda2$上下文$\Gamma$和$\mathbb{T2}$类型$\rho$使得$\Gamma\vdash M:\rho$.

## $\lambda2$中的派生例

试图派生$M\equiv\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)$.

即找到上下文$\Gamma$和类型$\rho$使得$\Gamma\vdash M:\rho$. 因为$M$没有自由项或类型变量，所有可以取$\Gamma\equiv\emptyset$，于是：

$(n)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\quad:\quad?$

下一个定型的项是“二阶$\lambda$”，因此使用$(abst_2)$.

$(m)\quad \alpha:*\ \vdash\ \lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ ?$

$(n)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ \dots\quad对(m)用(abst_2)$

新的目标是$\lambda f:\alpha\to\alpha.\ \dots$，是个普通的一阶抽象，使用$(abst)$：

$(k)\quad\alpha:*,\ f:\alpha\to\alpha,\ x:\alpha\ \vdash\ f(fx)\ :\ ?$

$(l)\quad\alpha:*,\ f:\alpha\to\alpha\ \vdash\ \lambda x:\alpha.f(fx)\ :\ \dots\quad对（k）用(abst)$

$(m)\quad\alpha:*\ \vdash\ \lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx)\ :\ \dots\quad对(l)用(abst)$

$(n)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ \dots\quad对(m)用(abst_2)$

剩下的就是一个$\lambda{\to}$ 的定型问题，于是给出简略版本：

$(1)\quad\alpha:*,\ f:\alpha\to\alpha,\ x:\alpha\ \vdash\ fx\ :\ \alpha$

$(2)\quad\alpha:*,\ f:\alpha\to\alpha,\ x:\alpha\ \vdash\ f(fx)\ :\ \alpha$

$(3)\quad\alpha:*,\ f:\alpha\to\alpha\ \vdash\ \lambda x:\alpha.f(fx)\ :\ type_1\quad对（2）用(abst)$

$(4)\quad\alpha:*\ \vdash\ \lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx)\ :\ type_2\quad对(3)用(abst)$

$(5)\quad\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(f\ x)\ :\ type_3\quad对(4)用(abst_2)$

最后填入$type_1$，$type_2$和$type_3$，使用$(abst)$和$(abst_2)$法则：

$type_1\equiv\alpha\to\alpha$

$type_2\equiv(\alpha\to\alpha)\to\alpha\to\alpha$

$type_3\equiv\Pi\alpha:*.(\alpha\to\alpha)\to\alpha\to\alpha$

填入第五行，结论是：

$(5)\quad\emptyset\vdash\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx):\Pi\alpha:*.(\alpha\to\alpha)\to\alpha\to\alpha$.

由Thinning引理（见下一节），我们可以得到，对于所有$\lambda2$上下文$\Gamma$：

$(6)\quad\Gamma\vdash\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx):\Pi\alpha:*.(\alpha\to\alpha)\to\alpha\to\alpha$.

假设我们有类型$nat$：

$(7)\quad\Gamma\vdash nat:*$

有$(6)$和$(7)$用$(appl_2)$：

$(8)\quad\Gamma\vdash(\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx))\ nat:(nat\to nat)\to nat\to nat$.

假设有：

$(9)\quad\Gamma\vdash suc\ :\ nat\to nat$，

对$(8)$和$(9)$用$(appl)$：

$(10)\quad\Gamma\vdash(\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx))\ nat \ suc:nat\to nat$.

有$\Gamma\vdash two:nat$，得到：

$(11)\quad\Gamma\vdash(\lambda\alpha:*.\lambda f:\alpha\to\alpha.\lambda x:\alpha.f(fx))\ nat \ suc\ two:nat$.

## $\lambda2$的性质

### Alpha替换/Alpha等价推广（α-conversion/α-equivalence, extended）

（1a）项变量重命名

$\lambda x:\sigma.M=_\alpha\lambda y:\sigma.M^{x\to y}$如果$y \not\in FV(M)$且$y$不是$M$中的绑定变量.

（1b）类型变量重命名

$\lambda \alpha:*.M=_\alpha \lambda\beta:*.M[\alpha:=\beta]$如果$\beta$不在$M$中出现，

$\Pi\alpha:*.M=_\alpha\Pi\beta:*.M[\alpha:=\beta]$如果$\beta$不在$M$中出现.

### $\mathbb{\Lambda_2}$项的单步Beta归约（One-step $\beta$-reduction, $\to_\beta$for $\mathbb{\Lambda_2}$-terms）

（1a）一阶：$(\lambda x:\sigma.M)N\to_\beta M[x:=N]$

（1b）二阶：$(\lambda \alpha:*.M)T\to_\beta M[\alpha:=T]$

### $\lambda2$中依然成立的引理

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

注意唯一不适用的引理是Permutation Lemma，因为对于上下文，后出现的声明可能依赖于前面的。而如果我们改成定义中的$\lambda2$上下文，则就仍然成立.

