# 8.9 Replace Magic Number with Symbolic Constant 以字面常量取代魔法数

<br>

<center>你有一个字面数值，带有特别含义。</center>

<br>

> **创造一个常量，根据其意义为它命名，并将上述的字面数值替换为这个常量。**

<br>

```java
    double potentialEnergy(double mass, double height) {
        return mass * 9.81 * height;
    }
```

<br>

<center>⇓</center>

<br>

```java
    double potentialEnergy(double mass, double height) {
        return mass * GRAVITATIONAL_CONSTANT * height;
    }
    static final double GRAVITATIONAL_CONSTANT = 9.81;
```

<br>

