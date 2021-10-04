# 1.3 分解并重组statement

第一个明显引起我注意的就是长得离谱的`statement()`。

每当看到这样长长的函数，我就想把它大卸八块。

要知道，代码块愈小，代码的功能就愈容易管理，代码的处理和移动也就愈轻松。

<br>

本章重构过程的第一阶段中，我将说明如何把长长的函数切开，并把较小块的代码移至更合适的类。

我希望降低代码重复量，从而使新的`(打印HTML详单用的)`函数更容易撰写。

<br>

第一个步骤是找出代码的逻辑泥团并运用`Extract Method (110)`。

本例一个明显的逻辑泥团就是switch语句，把它提炼到独立函数中似乎比较好。

<br>

和任何重构手法一样，当我提炼一个函数时，我必须知道可能出什么错。

如果提炼得不好，就可能给程序引入bug。

所以重构之前我需要先想出安全做法。

由于先前我已经进行过数次这类重构，所以我已经把安全步骤记录于后面的重构列表中了。

<br>

首先我得在这段代码里找出函数内的局部变量和参数。

我找到了两个， `each`和`thisAmount`，前者并未被修改，后者会被修改。

**任何不会被修改的变量都可以被我当成参数传入新的函数**，至于会被修改的变量就需格外小心。

**如果只有一个变量会被修改，我可以把它当作返回值。**

`thisAmount`是个临时变量，其值在每次循环起始处被设为0，并且在`switch`语句之前不会改变，所以我可以直接把新函数的返回值赋给它。

<br>

下面两页展示了重构前后的代码。

重构前的代码在左页，重构后的代码在右页。

凡是从函数提炼出来的代码，以及新代码所做的任何修改，只要我觉得不是明显到可以一眼看出，就以粗体字标示出来特别提醒你。

本章剩余部分将延续这种左右比对形式。
<br>

这里贴出重构前的代码

```java
    public String statement() {
        double totalAmount = 0;
        int frequentRenterPoints = 0;
        Enumeration rentals = _rentals.elements();
        String result = "Rental Record for " + getName() + "\n";
        while (rentals.hasMoreElements()) {
            double thisAmount = 0;
            Rental each = (Rental) rentals.nextElement();
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
            frequentRenterPoints++;
            if ((each.getMovie().getPriceCode() == Movie.NEW_RELEASE) && each.getDayRented() > 1) {
                frequentRenterPoints++;
            }
            result += "\t" + each.getMovie().getTitle() + "\t" + String.valueOf(thisAmount) + "\n";
            totalAmount += thisAmount;
        }
        result += "Amount owed is " + String.valueOf(totalAmount) + "\n";
        result += "You earned " + String.valueOf(frequentRenterPoints) + " frequent renter points";
        return result;
    }
```

<br>

重构后的代码

```java
    public String statement() {
        double totalAmount = 0;
        int frequentRenterPoints = 0;
        Enumeration rentals = _rentals.elements();
        String result = "Rental Record for " + getName() + "\n";
        while (rentals.hasMoreElements()) {
            Rental each = (Rental) rentals.nextElement();
            double thisAmount = amountFor(each);
            frequentRenterPoints++;
            if ((each.getMovie().getPriceCode() == Movie.NEW_RELEASE) && each.getDayRented() > 1) {
                frequentRenterPoints++;
            }
            result += "\t" + each.getMovie().getTitle() + "\t" + String.valueOf(thisAmount) + "\n";
            totalAmount += thisAmount;
        }
        result += "Amount owed is " + String.valueOf(totalAmount) + "\n";
        result += "You earned " + String.valueOf(frequentRenterPoints) + " frequent renter points";
        return result;
    }
    
    private int amountFor(Rental each) {
        int thisAmount = 0;
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

放一张对比图

<img src="https://raw.githubusercontent.com/huxiaoning/img/master/image-20210806224153813.png" alt="image-20210806224153813"  />

<br>



每次做完这样的修改，我都要编译并测试。

这一次起头不算太好——测试失败了，有两条测试数据告诉我发生了错误。

一阵迷惑之后我明白了自己犯的错误。我愚蠢地将`amountFor()`的返回值类型声明为`int`,而不是`double`.

<br>

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

我经常犯这种愚蠢可笑的错误，而这种错误往往很难发现。

在这里， Java无怨无尤地把`double`类型转换为`int`类型，而且还愉快地做了取整动作`[Java Spec]`。

还好此处这个问题很容易发现，因为我做的修改很小，而且我有很好的测试。

借着这个意外疏忽，我要阐述重构步骤的本质：由于每次修改的幅度都很小，所以任何错误都很容易发现。你不必耗费大把时间调试，哪怕你和我一样粗心。

<br>

> 重构技术就是以微小的步伐修改程序。如果你犯下错误，很容易便可发现它。

<br>

由于我用的是Java，所以我需要对代码做一些分析，决定如何处理局部变量。

如果拥有相应的工具，这个工作就超级简单了。 

`Smaltalk`的确拥有这样的工具：`Refactoring Browser`。

运用这个工具，重构过程非常轻松，我只需标示出需要重构的代码，在菜单中选择`Extract Method`，输入新的函数名称，一切就自动搞定。

而且工具决不会像我那样犯下愚蠢可笑的错误。我非常盼望早日出现`Java`版本的重构工具！

<br>

本书写作于1999年。十年之后，各种主要的`Java IDE`都已经提供了良好的重构支持。—译者注



<br>

<br>

**IDEA重构 - `Ctrl + Alt + Shit + t`**



![image-20210807002444173](https://raw.githubusercontent.com/huxiaoning/img/master/image-20210807002444173.png)
