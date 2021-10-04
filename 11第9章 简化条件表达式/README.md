# 第9章 简化条件表达式

<br>

条件逻辑有可能十分复杂，因此本章提供一些重构手法，专门用来简化它们。

其中一项核心重构就是`Decompose Conditional (238)`，可将一个复杂 的条件逻辑分成若干小块。

这项重构很重要，因为它使得“分支逻辑”和“操作细节”分离。

<br>

本章的其余重构手法可用以处理另一些重要问题：

如果你发现代码中的多处测试有相同结果，应该实施`Consolidate Conditional Expression (240)`；

如果条件代码中有任何重复，可以运用`Consolidate Duplicate Conditional Fragments (243)`将重复成分去掉。

<br>

如果程序开发者坚持“单一出口”原则，那么为让条件表达式也遵循这一原则，他往往会在其中加入控制标记。

我并不特别在意“一个函数一个出口”的教条，

所以我使用`Replace Nested Conditional with Cuard Clauses (250)`标示出那些特殊情况， 

并使用`Remove Control Flag (245)`去除那些讨厌的控制标记。

<br>

较之于过程化程序而言，面向对象程序的条件表达式通常比较少，这是因为很多条件行为都被多态机制处理掉了。

多态之所以更好，是因为调用者无需了解条件行为的细节，因此条件的扩展更为容易。

所以面向对象程序中很少出现`switch`语句。

一旦出现，就应该考虑运用`Replace Conditional with Polymorphism (255)`将它替换为多态。

<br>

多态还有一种十分有用但鲜为人知的用途：通过`Introduce Null Object (260)`去除对于`null`值的检验。

<br>

