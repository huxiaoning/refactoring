# 9.3 Consolidate Duplicate Conditional Fragments 合并重复的条件片段

<br>

<center>在条件表达式的每个分支上有着相同的一段代码。</center>

<br>

> **将这段重复代码搬移到条件表达式之外。**

<br>

```java
        if (isSpecialDeal()) {
            total = price * 0.95;
            send();
        } else {
            total = price * 0.98;
            send();
        }
```

<br>

<center>⇓</center>

<br>

```java
        if (isSpecialDeal()) {
            total = price * 0.95;
        } else {
            total = price * 0.98;
        }
        send();
```

<br>

