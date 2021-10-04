# 8.10 Encapsulate Field 封装字段

<br>

<center>你的类中存在一个public字段。</center>

<br>

> **将它声明为private，并提供相应的访问函数。**

<br>

```java
    public String _name;
```

<br>

<center>⇓</center>

<br>

```java
    private String _name;
    public String getName() {return _name;}
    public void setName(String arg) {_name = arg;}
```

<br>

