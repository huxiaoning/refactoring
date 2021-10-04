# 9.7 Introduce Null Object 引入Null对象

<br>

<center>你需要再三检查某对象是否为null。</center>

<br>

> **将null值替换为null对象。 **

<br>

```java
        if (customer == null) plan = BillingPlan.basic();
        else plan = customer.getPlan();
```

<br>

<center>⇓</center>

<br>

![](https://box.kancloud.cn/2016-08-15_57b1b5aa3516f.gif)

<br>

