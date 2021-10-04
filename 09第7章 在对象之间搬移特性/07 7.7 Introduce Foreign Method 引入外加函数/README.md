# 7.7 Introduce Foreign Method 引入外加函数

<br>

<center>你需要为提供服务的类增加一个函数，但你无法修改这个类。</center>

<br>

> **在客户类中建立一个函数，并以第一参数形式传入一个服务类实例。**

<br>

```java
        Date newStart = new Date(previousEnd.getYear(), previousEnd.getMonth(), previousEnd.getDate() + 1);
```

<br>

<center>⇓</center>

<br>

```java
        Date newStart = nextDay(previousEnd);

    private static Date nextDay(Date arg) {
        return new Date(arg.getYear(), arg.getMonth(), arg.getDate() + 1);
    }
```

<br>

