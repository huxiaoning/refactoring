# 9.2 Consolidate Conditional Expression 合并条件表达式

<br>

<center>你有一系列条件测试，都得到相同结果。</center>

<br>

> **将这些测试合并为一个条件表达式，并将这个条件表达式提炼成为一个独立函数。**

<br>

```java
    double disabilityAmount() {
        if (_seniority < 2) return 0;
        if (_monthsDisabled > 12) return 0;
        if (_isPartTime) return 0;
        // compute the disability amount
```

<br>

<center>⇓</center>

<br>

```java
    double disabilityAmount() {
        if (isNotEligibleForDisability()) return 0;
        // compute the disability amount
```

<br>

