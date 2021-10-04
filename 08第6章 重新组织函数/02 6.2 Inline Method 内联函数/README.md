# 6.2 Inline Method 内联函数

<br>

<center>一个函数的本体与名称同样清楚易懂。</center>

<br>

> **在函数调用点插入函数本体，然后移除该函数。**

<br>

```java
    int getRating() {
        return moreThanFiveLateDeliveries() ? 2 : 1;
    }

    boolean moreThanFiveLateDeliveries() {
        return _numberOfLateDeliveries > 5;
    }
```

<br>

<center>⇓</center>

<br>

```java
    int getRating() {
        return _numberOfLateDeliveries > 5 ? 2 : 1;
    }
```

<br>