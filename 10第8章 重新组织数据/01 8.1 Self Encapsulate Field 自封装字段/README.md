# 8.1 Self Encapsulate Field 自封装字段

<br>

<center>你直接访问一个字段，但与字段之间的耦合关系逐渐变得笨拙。</center>

<br>

> **为这个字段建立取值／设值函数，并且只以这些函数来访问字段。**

<br>

```java
    private int _low, _high;
    boolean includes(int arg) {
        return arg >= _low && arg <= _high;
    }
```

<br>

<center>⇓</center>

<br>

```java
    private int _low, _high;
    boolean includes(int arg) {
        return arg >= getLow() && arg <= getHigh();
    }
    int getLow() {return _low;}
    int getHigh() {return _high;}
```

<br>

