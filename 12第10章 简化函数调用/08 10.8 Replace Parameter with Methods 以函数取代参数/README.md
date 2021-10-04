# 10.8 Replace Parameter with Methods 以函数取代参数

<br>

<center>对象调用某个函数，并将所得结果作为参数，传递给另一个函数。而接受该参数的函数本身也能够调用前一个函数。</center>

<br>

> **让参数接受者去除该项参数，并直接调用前一个函数。**

<br>

```java
        int basePrice = _quantity * _itemPrice;
        discountLevel = getDiscountLevel();
        double finalPrice = discountedPrice(basePrice, discountLevel);
```

<br>

<center>⇓</center>

<br>

```java
        int basePrice = _quantity * _itemPrice;
        double finalPrice = discountedPrice(basePrice);
```

<br>

