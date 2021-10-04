# 搬移`getCharge()`函数

<br>

这暗示`getCharge()`应该移到`Mavie`类里去：

<br>

```java
class Movie...
    public double getCharge(int dayRented) {
        double result = 0;
        switch (_priceCode) {
            case REGULAR:
                result += 2;
                if (dayRented > 2) {
                    result += (dayRented - 2) * 1.5;
                }
                break;
            case NEW_RELEASE:
                result += dayRented * 3;
                break;
            case CHILDRENS:
                result += 1.5;
                if (dayRented > 3) {
                    result += (dayRented - 3) * 1.5;
                }
                break;
        }
        return result;
    }
```

<br>

为了让它得以运作，我必须把租期长度作为参数传递进去。

当然，租期长度来自`Rental`对象。

计算费用时需要两项数据：租期长度和影片类型。

为什么我选择将租期长度传给`Movie`对象，而不是将影片类型传给`Rental`对象呢？

因为本系统可能发生的变化是加入新影片类型，这种变化带有不稳定倾向。

如果影片类型有所变化，我希望尽量控制它造成的影响，所以选择在`Movie`对象内计算费用。

<br>

我把上述计费方法放进`Movie`类，然后修改`Rental`的`getcharge()`，让它使用这个新函数（图1—12和图1—13）

<br>



```java
class Rental...
    public double getCharge() {
        return _movie.getCharge(_dayRented);
    }
```











<br>

<br>

**IDEA重构 - `Ctrl + Alt + Shit + t`**

搬移函数心得 : 若函数被多处理引用，并且需要传递参数给搬移后的新函数，搬移将不好操作。

这时可以先抽取一个私有方法，这个方法体内如果包含私有成员，则添加参数，如下：

```java
    public double getCharge() {
        return getCharge(_dayRented);
    }

    private double getCharge(int _dayRented) {
        double result = 0;
        switch (_movie.getPriceCode()) {
            case Movie.REGULAR:
                result += 2;
                if (_dayRented > 2) {
                    result += (_dayRented - 2) * 1.5;
                }
                break;
            case Movie.NEW_RELEASE:
                result += _dayRented * 3;
                break;
            case Movie.CHILDRENS:
                result += 1.5;
                if (_dayRented > 3) {
                    result += (_dayRented - 3) * 1.5;
                }
                break;
        }
        return result;
    }
```

这个带参数的方法就比较方便搬移了。



<br>
