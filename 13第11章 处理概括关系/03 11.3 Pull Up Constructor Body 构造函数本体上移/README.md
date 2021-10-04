# 11.3 Pull Up Constructor Body 构造函数本体上移

<br>

<center>你在各个子类中拥有一些构造函数，它们的本体几乎完全一致。</center>

<br>

> **在超类中新建一个构造函数，并在子类构造函数中调用它。**

<br>

```java
class Manager extends Employee...
    public Manager(String name, int id, int grade) {
        _name = name;
        _id = id;
        _grade = grade;
    }
```

<br>

<center>⇓</center>

<br>

```java
    public Manager(String name, int id, int grade) {
        super(name, id);
        _grade = grade;
    }
```

<br>

