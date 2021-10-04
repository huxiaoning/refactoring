# 6.4 Replace Temp with Query 以查询取代临时变量

<br>

<center>你的程序以一个临时变量保存某一表达式的运算结果。</center>

<br>

> **将这个表达式提炼到一个独立函数中。将这个临时变量的所有引用点替换为对新函数的调用。**
>
> **此后，新函数就可被其他函数使用。**

<br>

```java
        double basePrice = _quantity * _itemPrice;
        if (basePrice > 1000D) {
            return basePrice * 0.95D;
        } else {
            return basePrice * 0.98D;
        }
```

<br>

<center>⇓</center>

<br>

```java
        if (basePrice() > 1000D) {
            return basePrice() * 0.95D;
        } else {
            return basePrice() * 0.98D;
        }
...
    private double basePrice() {
        return _quantity * _itemPrice;
    }
```

<br>

