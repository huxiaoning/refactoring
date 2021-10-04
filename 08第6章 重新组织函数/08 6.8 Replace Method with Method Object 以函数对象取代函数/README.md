# 6.8 Replace Method with Method Object 以函数对象取代函数

<br>

<center>你有一个大型函数，其中对局部变量的使用使你无法采用Extract Method (110)。</center>

<br>

> **将这个函数放进一个单独对象中，如此一来局部变量就成了对象内的字段。**
>
> **然后你可以在同一个对象中将这个大型函数分解为多个小型函数。**

<br>

```java
 class Order...
   double price() {
       double primaryBasePrice;
       double secondaryBasePrice;
       double tertiaryBasePrice;
       // long computation;
       ...
   }
```

<br>

<center>⇓</center>

<br>

![](https://raw.githubusercontent.com/huxiaoning/img/master/20210831214418.png)

<br>

