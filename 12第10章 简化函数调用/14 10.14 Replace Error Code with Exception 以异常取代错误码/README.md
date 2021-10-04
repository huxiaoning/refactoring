# 10.14 Replace Error Code with Exception 以异常取代错误码

<br>

<center>某个函数返回一个特定的代码，用以表示某种错误情况。</center>

<br>

> **改用异常。**

<br>

```java
    int withdraw(int amount) {
        if (amount > _balance)
            return -1;
        else {
            _balance -= amount;
            return 0;
        }
    }
```

<br>

<center>⇓</center>

<br>

```java
    void withdraw(int amount) throws BalanceException {
        if (amount > _balance) throw new BalanceException();
        _balance -= amount;
    }
```

<br>

