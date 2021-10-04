# 范例：以return 返回控制标记

<br>

本项重构的另一种形式将使用`return`语句。

为了阐述这种用法，我把前面的例子稍加修改，以控制标记记录搜索结果：

```java
    void checkSecurity(String[] people) {
        String found = "";
        for (int i = 0; i < people.length; i++) {
            if (found.equals("")) {
                if (people[i].equals("Don")) {
                    sendAlert();
                    found = "Don";
                }
                if (people[i].equals("John")) {
                    sendAlert();
                    found = "John";
                }
            }
        }
        someLaterCode(found);
    }
```

在这里，变量`found`做了两件事：它既是控制标记，也是运算结果。

遇到这种情况，我喜欢先把计算`found`变量的代码提炼到一个独立函数中：

```java
    void checkSecurity(String[] people) {
        String found = foundMiscreant(people);
        someLaterCode(found);
    }

    String foundMiscreant(String[] people) {
        String found = "";
        for (int i = 0; i < people.length; i++) {
            if (found.equals("")) {
                if (people[i].equals("Don")) {
                    sendAlert();
                    found = "Don";
                }
                if (people[i].equals("John")) {
                    sendAlert();
                    found = "John";
                }
            }
        }
        return found;
    }
```

然后以`return`语句取代控制标记：

```java
    String foundMiscreant(String[] people) {
        String found = "";
        for (int i = 0; i < people.length; i++) {
            if (found.equals("")) {
                if (people[i].equals("Don")) {
                    sendAlert();
                    return "Don";
                }
                if (people[i].equals("John")) {
                    sendAlert();
                    found = "John";
                }
            }
        }
        return found;
    }
```

最后完全去掉控制标记：

```java
    String foundMiscreant(String[] people) {
        for (int i = 0; i < people.length; i++) {
            if (people[i].equals("Don")) {
                sendAlert();
                return "Don";
            }
            if (people[i].equals("John")) {
                sendAlert();
                return "John";
            }
        }
        return "";
    }
```

即使不需要返回某值，也可以用`return`语句来取代控制标记。

这时候你只需要一个空的`return`语句就行了。

<br>

当然，如果以此办法去处理带有副作用的函数，会有一些问题。

所以我需要先以`Separate Query from Modifier (279)`将函数副作用分离出去。

稍后你会看到这方面的例子。

<br>

