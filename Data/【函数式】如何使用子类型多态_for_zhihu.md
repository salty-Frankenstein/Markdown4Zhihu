---
title: 【函数式】如何使用子类型多态
date: 2021-06-05 13:18:58
categories: 杂记
tags:
     - 函数式
     - Haskell
     - 教程
---

最近在尝试用Haskell实现Peter Shirley的*Ray Tracing in a Weekend*一书，发现了这个问题，并琢磨出了一些解法，看起来像是发现了一种设计模式，不过不知道叫什么名字（

<!--more-->

# 子类型多态
我们知道，子类型多态是OOP中一个很好用的特性，它可以做到把满足子类型关系的值放在同一个数据结构中，统一对它们操作，实现多态的效果。在OOP中，常常用这一特性实现称为**接口**的抽象类，比如：  
```cpp
class Showable{
public:
  virtual X show(Y y, Z z) = 0;
};

class ShowA : public Showable{
public:
  ShowA(A a) {...}
  X f(Y y, Z z) {...}
  A a;
};

class ShowBC : public Showable{
public:
  ShowBC(B b, C c) {...}
  X f(Y y, Z z) {...}
  B b;
  C c;
};

list<Showable*> l = {ShowA(a), ShowBC(b, c)};
for(Showable* x : l){
  x->f(y, z);
}
```
由于`ShowA`，`ShowBC`都是`Showable`的子类型，都可以支持`show(y, z)`操作，所以可以把`ShowA`，`ShowBC`的值通过`Showable`类型进行统一操作。

# 尝试
在Haskell语言中，并没有提供上述OOP意义上的子类型多态。但是类似的对于接口的定义和实现，由typeclass这一特性提供：
```haskell
class Showable a where
  show :: a -> Y -> Z -> X

data ShowA = ShowA A
instance Showable ShowA where
  show (ShowA a) x y = ...

data ShowBC = ShowBC B C
instance Showable ShowBC where
  show (ShowBC b c) x y = ...

f :: Showable a => [a] -> F
f l = let x = map show l in ...
```
这是Haskell中经典的typeclass用法，对于f的参数可以是任意实现了`Showable`的类型的值，自动调用不同的`show`实现多态。

现在问题来了：
```haskell
la :: [ShowA]
la = [ShowA a1, ShowA a2] -- OK, f la

lb :: [ShowBC]
lb = [ShowBC b1 c1, ShowBC b2 c2] -- OK, f lb

l = la ++ lb  -- error
```
由于Haskell类型系统的规定，list中是不能存放不同类型的值的，而typeclass不是具体的类型，因此即使实现了同一个typeclass，不同类型的值也不能放在列表中统一操作。

# 再试试
既然是类型阻碍了我们，一般我们可以这么做：
```haskell
data ShowableT = SA ShowA | SB ShowBC

instance Showable ShowableT where
  show (SA a) = show a
  show (SB b) = show b

l = [SA (ShowA a), SB (ShowBC b c)]  -- OK, f l
```
在`A`和`B`外面再包一层类型，这样就是同一个类型了（   
类似的，比如要实现一个DSL的时候，可能有一些不同类型的表达式，就可以用这种方法把这些类型包成一个类型。  

但是这样，每增加一个对`Showable`的实现，都要在`ShowableT`中增加一种类型，不利于维护。于是更一般地，对于子类型多态（的模拟），可以这样做：  
```haskell
{-# LANGUAGE ExistentialQuantification #-}
class Showable_ a where
  show :: a -> Y -> Z -> X

data Showable = forall a. Showable_ a => Showable a
instance Showable_ Showable where
  show (Showable a) = show a

data ShowA = ShowA A
instance Showable_ ShowA where
  show (ShowA a) x y = ...

data ShowBC = ShowBC B C
instance Showable_ ShowBC where
  show (ShowBC b c) x y = ...

l :: [Showable]
l = [Showable (ShowA a), Showable (ShowBC b c)] -- OK
```
这一操作把typeclass包了一层类型，这样这一版本的`Showable`就类似于OOP版本里的抽象类了。这样实现就比较类似上面OOP风格的子类型多态了，可以在不同类型实现同一接口，也可以把实现了同一接口的类型放在一个数据结构里统一操作。

# 然后呢
这说明在Haskell里，嗯是要模拟出一种类似于接口类的编程范式也不是不行。然而这个写法构造数据的时候比较繁琐，且也可能影响性能。更重要的是，这个方法看起来太刻意了，不太像是正常的FP设计。

我意识到，我在一开始想模拟OOP的时候就中计了。正确的问法不应该是：“别人在OOP里写了个接口类和几个实现，我用FP该怎么写”，而是“别人用OOP的对象和子类型多态组织了这个计算需求，我用FP该怎么组织呢”。那么OOP中使用子类型多态到底解决了什么问题？  

其实OOP的哲学是`对象/数据.计算()`，其计算是绑定在数据上的，而子类型多态，即是把计算动态绑定到不同类型的数据上（对不同的数据施加不同的计算）。  
然而对于FP，其实计算（函数）就是数据，可以是`计算(数据)`或者就是`计算(计算)`。那么对于把计算**动态地**绑在不同数据上的需求，FP里应该怎么做呢？答案呼之欲出，那就是直接操作计算（函数）：

```haskell
data Showable = Showable { runShow :: Y -> Z -> X }
showA :: A -> Showable
showA a = Showable $ \y z -> ...

showBC :: B -> C -> Showable
showBC b c = Showable $ \y z -> ...

f :: [Showable] -> F
f l = let map runShow l in ...

l :: [Showable]
l = [showA a, showBC b c]  -- OK 
```

与上面OOP的设计对照，可以发现每个部分都可以对应：
- Showable是一个有`Y -> Z -> X`函数的接口，把它称为`runShow`
- `showA`由一个`A`类型数据，可以构造出一个具有`runShow`计算的数据
- `showBC`由一个`B`、一个`C`类型数据，可以构造出一个具有`runShow`计算的数据
- `showA`和`showBC`对`runShow`的具体实现则在构造`Showable`的函数中  
- OOP中会根据数据动态的绑定对应的计算，而在FP中，计算就是数据本身

从语法的角度说，类型`Showable`只有`Showable`这一个值构造子，但这里我们可以实现`showA`，`showB`这样的函数完成如OOP一样的不同“对象”的构造，从函数签名来看，它们也是`Showable`的构造子。如此，对于数据的构造就更加自然了。  

至少在本例中，两种方式是等价的，而第二种则更加FP。

可以说，这种对计算的直接操作才是FP中最精髓的设计模式，从各种高阶函数，`Reader`、`State`等Monad，到CPS变换对continuation的直接操作，都是以计算为数据这一设计的体现。这也体现出，FP基于一等函数的抽象是一种非常一般性的抽象，由这一最平平无奇的语言特性就可以模拟或者实现出其他语言各种千奇百怪的特性或者设计模式。
