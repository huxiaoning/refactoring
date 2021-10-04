# 9.8 Introduce Assertion 引入断言

<br>

<center>某一段代码需要对程序状态做出某种假设。</center>

<br>

> **以断言明确表现这种假设。**

<br>

```java
    double getExpenseLimit() {
        // should have either expense limit or a primary project
        return (_expenseLimit != NULL_EXPENSE) ?
                _expenseLimit :
                _primaryProject.getMemberExpenseLimit();
    }
```

<br>

<center>⇓</center>

<br>

```java
    double getExpenseLimit() {
        Assert.isTrue(_expenseLimit != NULL_EXPENSE || _primaryProject != null);
        return (_expenseLimit != NULL_EXPENSE) ?
                _expenseLimit :
                _primaryProject.getMemberExpenseLimit();
    }
```

<br>

