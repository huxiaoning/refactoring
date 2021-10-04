# 9.6 Replace Conditional with Polymorphism 以多态取代条件表达式

<br>

<center>你手上有个条件表达式，它根据对象类型的不同而选择不同的行为。</center>

<br>

> **将这个条件表达式的每个分支放进一个子类内的覆写函数中，然后将原始函数声明为抽象函数。**

<br>

```java
    double getSpeed() {
        switch (_type) {
            case EUROPEAN:
                return getBaseSpeed();
            case AFRICAN:
                return getBaseSpeed() - getLoadFactor() * _numberOfCoconuts;
            case NORWEGIAN_BLUE:
                return (_isNailed) ? 0 : getBaseSpeed(_voltag);
        }
        throw new RuntimeException("Should be unreachable");
    }
```

<br>

<center>⇓</center>

<br>

![image-20210925103011949](https://raw.githubusercontent.com/huxiaoning/img/master/image-20210925103011949.png)

<br>

