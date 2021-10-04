# 10.7 Preserve Whole Object 保持对象完整

<br>

<center>你从某个对象中取出若干值，将它们作为某一次函数调用时的参数。</center>

<br>

> **改为传递整个对象。**

<br>

```java
        int low = daysTempRange().getLow();
        int high = daysTempRange().getHigh();
        withinPlan = plan.withinRange(low, high);
```

<br>

<center>⇓</center>

<br>

```java
        withinPlan = plan.withinRange(daysTempRange());
```

<br>

