# 1.4 运用多态取代与价格相关的条件逻辑

<br>

这个问题的第一部分是`switch`语句。

最好不要在另一个对象的属性基础上运用`switch`语句。

如果不得不使用，也应该在对象自己的数据上使用，而不是在别人的数据上使用。

<br>

```java
class Rental...
    public double getCharge() {
        double result = 0;
        switch (getMovie().getPriceCode()) {
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

