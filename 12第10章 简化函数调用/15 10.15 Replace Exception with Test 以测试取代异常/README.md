# 10.15 Replace Exception with Test 以测试取代异常

<br>

<center>面对一个调用者可以预先检查的条件，你抛出了一个异常。</center>

<br>

> **修改调用者，使它在调用函数之前先做检查。**

<br>

```java
    double getValueForPeriod(int periodNumber) {
        try {
            return _values[periodNumber];
        } catch (ArrayIndexOutOfBoundsException e) {
            return 0;
        }
    }
```

<br>

<center>⇓</center>

<br>

```java
    double getValueForPeriod(int periodNumber) {
        if (periodNumber >= _values.length) return 0;
        return _values[periodNumber];
    }
```

<br>

