# 修改`amountFor()`方法内的变量名称

<br>

现在，我已经把原来的函数分为两块，可以分别处理它们。我不喜欢`amountFor()`内的某些变量名称，现在正是修改它们的时候。

<br>

现在，我已经把原下面是原本的代码：

```java
    private double amountFor(Rental each) {
        double thisAmount = 0;
        switch (each.getMovie().getPriceCode()) {
            case Movie.REGULAR:
                thisAmount += 2;
                if (each.getDayRented() > 2) {
                    thisAmount += (each.getDayRented() - 2) * 1.5;
                }
                break;
            case Movie.NEW_RELEASE:
                thisAmount += each.getDayRented() * 3;
                break;
            case Movie.CHILDRENS:
                thisAmount += 1.5;
                if (each.getDayRented() > 3) {
                    thisAmount += (each.getDayRented() - 3) * 1.5;
                }
                break;
        }
        return thisAmount;
    }
```

<br>

下面是改名后的代码：

```java
    private double amountFor(Rental aRental) {
        double result = 0;
        switch (aRental.getMovie().getPriceCode()) {
            case Movie.REGULAR:
                result += 2;
                if (aRental.getDayRented() > 2) {
                    result += (aRental.getDayRented() - 2) * 1.5;
                }
                break;
            case Movie.NEW_RELEASE:
                result += aRental.getDayRented() * 3;
                break;
            case Movie.CHILDRENS:
                result += 1.5;
                if (aRental.getDayRented() > 3) {
                    result += (aRental.getDayRented() - 3) * 1.5;
                }
                break;
        }
        return result;
    }
```

<br>

放一张对比图

![image-20210807000753444](https://raw.githubusercontent.com/huxiaoning/img/master/image-20210807000753444.png)

就是把`each`改成`aRental`、`thisAmount`改成`result`。

<br>

改名之后，我需要重新编译并测试，确保没有破坏任何东西。

<br>

更改变量名称是值得的行为吗？绝对值得。

好的代码应该清楚表达出自己的功能，变量名称是代码清晰的关键。

如果为了提高代码的清晰度，需要修改某些东西的名字，那么就大胆去做吧。

只要有良好的查找/替换工具，更改名称并不困难。

语言所提供的强类型检查以及你自己的测试机制会指出任何你遗漏的东西。记住：



> 任何一个傻瓜都能写出计算机可以理解的代码。唯有写出人类容易理解的代码，才是优秀的程序员。



<br>

代码应该表现自己的目的，这一点非常重要。

阅读代码的时候，我经常进行重构。

这样，随着对程序的理解逐渐加深，我也就不断地把这些理解嵌入代码中，这么一来才不会遗忘我曾经理解的东西。

<br>

<br>

**IDEA重构 - `Shit + F6`**

