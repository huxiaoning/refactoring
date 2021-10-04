# 11.11 Replace Inheritance with Delegation 以委托取代继承

<br>

<center>某个子类只使用超类接口中的一部分，或是根本不需要继承而来的数据。</center>

<br>

> **在子类中新建一个字段用以保存超类；调整子类函数，令它改而委托超类；然后去掉两者之间的继承关系。**

<br>

![image-20211001234136312](https://raw.githubusercontent.com/huxiaoning/img/master/image-20211001234136312.png)

<br>

