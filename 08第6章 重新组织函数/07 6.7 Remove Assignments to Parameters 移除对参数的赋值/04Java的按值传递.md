# Java的按值传递

<br>

Java使用按值传递的函数调用方式，这常常造成许多人迷惑。

在所有地点，Java都严格采用按值传递方式，所以下列程序：

```java
class Param {
    public static void main(String[] args) {
        int x = 5;
        triple(x);
        System.out.println("x after triple: " + x);
    }

    private static void triple(int arg) {
        arg = arg * 3;
        System.out.println("arg in triple: " + arg);
    }
}
```

会产生这样的输出：

```
arg in triple: 15
x after triple: 5
```

这段代码还不至于让人糊涂。

但如果参数中传递的是对象，就可能把人弄迷糊了。

如果我在程序中以`Date`对象表示日期，那么下列程序：

```java
class Param {
    public static void main(String[] args) {
        Date d1 = new Date("1 Apr 98");
        nextDateUpdate(d1);
        System.out.println("d1 after nextDay: " + d1);
        Date d2 = new Date("1 Apr 98");
        nextDateReplace(d2);
        System.out.println("d2 after nextDay: " + d2);
    }

    private static void nextDateUpdate(Date arg) {
        arg.setDate(arg.getDate() + 1);
        System.out.println("arg in nextDay: " + arg);
    }

    private static void nextDateReplace(Date arg) {
        arg = new Date(arg.getYear(), arg.getMonth(), arg.getDate() + 1);
        System.out.println("arg in nextDay: " + arg);
    }
}
```

产生的输出是：

```
arg in nextDay: Thu Apr 02 00:00:00 CST 1998
d1 after nextDay: Thu Apr 02 00:00:00 CST 1998
arg in nextDay: Thu Apr 02 00:00:00 CST 1998
d2 after nextDay: Wed Apr 01 00:00:00 CST 1998
```

从本质上说，对象的引用是按值传递的。

因此我可以修改参数对象的内部状态，但对参数对象重新赋值是没有意义的。

<br>

`Java 1.1`及其后版本允许将参数标示为`final`，从而避免函数中对参数赋值。

即使某个参数被标示为`final`，仍然可以修改它所指向的对象。

我总是把参数视为`final`，但是我得承认，我很少在参数列表中这样标示它们。

<br>

