# 搬移`getFrequentRenterPoints()`函数



<br>

搬移`getcharge()`之后，我以相同手法处理常客积分计算。

这样我就把根据影片类型而变化的所有东西，都放到了影片类型所属的类中。以下是重构前的代码：

<br>

```java
class Rental...
    public int getFrequentRenterPoints() {
        if ((getMovie().getPriceCode() == Movie.NEW_RELEASE) && _dayRented > 1) {
            return 2;
        }
        return 1;
    }
```

<br>

![image-20210807191528576](https://raw.githubusercontent.com/huxiaoning/img/master/image-20210807191528576.png)

<br>

重构后的代码如下：

<br>

```java
class Rental...
    public int getFrequentRenterPoints() {
        return _movie.getFrequentRenterPoints(_dayRented);
    }

class Movie...
    public int getFrequentRenterPoints(int _dayRented) {
        if ((getPriceCode() == NEW_RELEASE) && _dayRented > 1) {
            return 2;
        }
        return 1;
    }
```

<br>

![image-20210807191903610](https://raw.githubusercontent.com/huxiaoning/img/master/image-20210807191903610.png)

