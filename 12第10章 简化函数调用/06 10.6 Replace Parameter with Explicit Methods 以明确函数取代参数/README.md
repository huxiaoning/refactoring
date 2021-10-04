# 10.6 Replace Parameter with Explicit Methods 以明确函数取代参数

<br>

<center>你有一个函数，其中完全取决于参数值而采取不同行为。</center>

<br>

> **针对该参数的每一个可能值，建立一个独立函数。**

<br>

```java
    void setValue(String name, int value) {
        if (name.equals("height")) {
            _height = value;
            return;
        }
        if (name.equals("width")) {
            _width = value;
            return;
        }
        Assert.shouldNeverReachHere();
    }
```

<br>

<center>⇓</center>

<br>

```java
    public void setHeight(int arg) {
        _height = arg;
    }
    public void setWidth(int arg) {
        _width = arg;
    }
```

<br>

