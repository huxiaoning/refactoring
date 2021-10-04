# 6.7 Remove Assignments to Parameters 移除对参数的赋值

<br>

<center>代码对一个参数进行赋值。</center>

<br>

> **以一个临时变量取代该参数的位置。**

<br>

```java
    int discount(int inputVal, int quantity, int yearToDate) {
        if (inputVal > 50) inputVal -= 2;
```

<br>

<center>⇓</center>

<br>

```java
    int discount(int inputVal, int quantity, int yearToDate) {
        int result = inputVal;
        if (inputVal > 50) result -= 2;
```

<br>

