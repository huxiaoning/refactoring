# 9.1 Decompose Conditional 分解条件表达式

<br>

<center>你有一个复杂的条件(if-then-else)语句。</center>

<br>

> **从if、then、else三个段落中分别提炼出独立函数。**

<br>

```java
        if (date.before(SUMMER_START) || date.after(SUMMER_END)) {
            charge = quantity * _winterRate + _winterServiceCharge;
        } else {
            charge = quantity * _summerRate;
        }
```

<br>

<center>⇓</center>

<br>

```java
        if (notSummer(date)) {
            charge = winterCharge(quantity);
        } else {
            charge = summerCharge(quantity);
        }
```

<br>

