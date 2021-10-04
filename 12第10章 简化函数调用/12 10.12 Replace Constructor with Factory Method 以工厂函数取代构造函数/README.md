# 10.12 Replace Constructor with Factory Method 以工厂函数取代构造函数

<br>

<center>你希望在创建对象时不仅仅是做简单的建构动作。</center>

<br>

> **将构造函数替换为工厂函数。**

<br>

```java
    Employee(int type) {
        _type = type;
    }
```

<br>

<center>⇓</center>

<br>

```java
    static Employee create(int type) {
        return new Employee(type);
    }
```

<br>

