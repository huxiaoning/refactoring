# 6.6 Split Temporary Variable 分解临时变量

<br>

<center>你的程序有某个临时变量被赋值超过一次，它既不是循环变量，也不被用于收集计算结果。</center>

<br>

> **针对每次赋值，创造一个独立、对应的临时变量。**

<br>

```java
        double temp = 2 * _height * _width;
        System.out.println(temp);
        temp = _height * _width;
        System.out.println(temp);
```

<br>

<center>⇓</center>

<br>

```java
        final double perimeter = 2 * _height * _width;
        System.out.println(perimeter);
        final double area = _height * _width;
        System.out.println(area);
```

<br>

