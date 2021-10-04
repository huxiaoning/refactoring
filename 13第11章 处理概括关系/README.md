# 第11章 处理概括关系

<br>

有一批重构手法专门用来处理类的概括关系(`generalization`，即继承关系)，其中主要是将函数上下移动于继承体系之中。

`Pull Up Field (320)`和`Pull Up Method (322)`都用于将特性向继承体系的上端移动，

`Push Down Method (328)`和`Push Down Field (329)`则将特性向继承体系的下端移动。

构造函数比较难以向上拉动，因此专门有一个`Pull Up Constructor Body (325)`处理它。

我们不会将构造函数往下推，因为`Replace Constructor with Factory Method (304)`通常更管用。

<br>

如果有若干函数大体上相同，只在细节上有所差异，可以使用`Form Template Method (345)`将它们的共同点和不同点分开。

<br>

除了在继承体系中移动特性之外，你还可以建立新类，改变整个继承体系。

`Extract Subclass (330)`、`Extract Superclass (336)`和`Extract Interface (341)`都是这样的重 构手法，它们在继承体系的不同位置构造出新元素。

如果你想在类型系统中标示一小部分函数，`Extract Interface (341)`特别有用。

如果你发现继承体系中的某些类没有存在必要，可以使用`Collapse Hierarchy (344)`将它们移除。

<br>

有时候你会发现继承并非最佳选择，你真正需要的其实是委托，那么，`Replace Inheritance with Delegation (352)`可以帮助你把继承改为委托。

有时候你又会想要做反向修改，此时就可使用`Replace Delegation with Inheritance (355)`。

<br>

