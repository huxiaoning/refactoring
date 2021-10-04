# 范例：使用Self-Encapsulation

<br>

如果有很多函数已经使用了`_interestRate`字段，我应该先运用`Self Encapsulate Field (171)` (自我封装)：

```java
public class Account {
    private AccountType _type;
    private int _interestRate;

    double interestForAmount_days(double amount, int days) {
        return getInterestRate() * amount * days / 365;
    }

    public void setInterestRate(int arg) {
        this._interestRate = arg;
    }

    public int getInterestRate() {
        return _interestRate;
    }
}
```

这样，在搬移字段之后，我就只需要修改访问函数：

```java
    double interestForAmount_days(double amount, int days) {
        return getInterestRate() * amount * days / 365;
    }

    public void setInterestRate(int arg) {
        _type.setInterestRate(arg);
    }

    public int getInterestRate() {
        return _type.getInterestRate();
    }
```

以后若有必要，我可以修改访问函数的用户，让它们使用新对象。

`Self EncapsulateField (171)`使我得以保持小步前进。

如果我需要对类做许多处理，保持小步前进是有帮助的。

特别值得一提的是：首先使用`Self Encapsulate Field (171)`使我得以更轻松使用`Move Method (142)`将函数搬移到目标类中。

如果待搬移函数引用了字段的访问函数，那些引用点是无需修改的。

<br>

