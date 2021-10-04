# 6.1 Extract Method 提炼函数

<br>

<center>你有一段代码可以被组织在一起并独立出来。</center>

<br>

> **将这段代码放进一个独立函数中，并让函数名称解释该函数的用途。**

<br>

```java
    void printOwing(double amount) {
        printBanner();

        // print details
        System.out.println("name:" + _name);
        System.out.println("amount:" + amount);
    }
```

<br>

<center>⇓</center>

<br>

```java
    void printOwing(double amount) {
        printBanner();
        printDetails(amount);
    }

    private void printDetails(double amount) {
        System.out.println("name:" + _name);
        System.out.println("amount:" + amount);
    }
```

<br>

