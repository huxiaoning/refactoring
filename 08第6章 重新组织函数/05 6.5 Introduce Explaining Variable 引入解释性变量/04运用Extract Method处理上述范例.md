# 运用Extract Method处理上述范例

<br>

面对上述代码，我通常不会以临时变量来解释其动作意图，我更喜欢使用Extract Method（110）。

让我们回到起点：

```java
    double price() {
        // price is base price - quantity discount + shipping
        return _quantity * _itemPrice -
                Math.max(0, _quantity - 500) * _itemPrice * 0.05 +
                Math.min(_quantity * _itemPrice * 0.1, 100.0);
    }
```

这一次我把底价计算提炼到一个独立函数中：

```diff
    double price() {
        // price is base price - quantity discount + shipping
+        return basePrice() -
                Math.max(0, _quantity - 500) * _itemPrice * 0.05 +
+                Math.min(basePrice() * 0.1, 100.0);
    }

    private double basePrice() {
        return _quantity * _itemPrice;
    }
```

我继续提炼，每次提炼出一个新函数。

最后得到下列代码：

```java
    double price() {
        return basePrice() - quantifyDiscount() + shipping();
    }

    private double quantifyDiscount() {
        return Math.max(0, _quantity - 500) * _itemPrice * 0.05;
    }

    private double shipping() {
        return Math.min(basePrice() * 0.1, 100.0);
    }

    private double basePrice() {
        return _quantity * _itemPrice;
    }
```



<br>

我比较喜欢使用Extract Method（110），因为同一对象中的任何部分，都可以根据自己的需要取用这些提炼出来的函数。

一开始我会把这些新函数声明为private；如果其他对象也需要它们，我可以轻易释放这些函数的访问限制。

我还发现，ExtractMethod（110）的工作量通常并不比Introduce Explaining Variable（124）来得大。

<br>

那么，应该在什么时候使用Introduce Explaining Variable（124）呢？

答案是：在 Extract Method（110）需要花费更大工作量时。

如果我要处理的是一个拥有大量局部变量的算法，那么使用Extract Method（110）绝非易事。

这种情况下就会使用IntroduceExplaining Variable （124）来理清代码，然后再考虑下一步该怎么办。

搞清楚代码逻辑之后，我总是可以运用Replace Temp with Query（120）把中间引入的那些解释性临时变量去掉。

况且，如果我最终使用Replace Method with Method Object（135），那么 中间引入的那些解释性临时变量也有其价值。

<br>

