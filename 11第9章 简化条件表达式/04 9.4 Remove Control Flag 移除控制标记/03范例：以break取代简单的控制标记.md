# 范例：以break取代简单的控制标记

<br>

下列函数用来检查一系列人名之中是否包含两个可疑人物的名字(这两个人的名字硬编码于代码中)：

```java
    void checkSecurity(String[] people) {
        boolean found = false;
        for (int i = 0; i < people.length; i++) {
            if (!found) {
                if (people[i].equals("Don")) {
                    sendAlert();
                    found = true;
                }
                if (people[i].equals("John")) {
                    sendAlert();
                    found = true;
                }
            }
        }
    }
```

这种情况下很容易找出控制标记：当变量`found`被赋予`true`时，搜索就结束。

我可以逐一引入`break`语句：

```java
    void checkSecurity(String[] people) {
        boolean found = false;
        for (int i = 0; i < people.length; i++) {
            if (!found) {
                if (people[i].equals("Don")) {
                    sendAlert();
                    break;
                }
                if (people[i].equals("John")) {
                    sendAlert();
                    found = true;
                }
            }
        }
    }
```

直到替换掉所有对`found`变量赋值的语句：

```java
    void checkSecurity(String[] people) {
        boolean found = false;
        for (int i = 0; i < people.length; i++) {
            if (!found) {
                if (people[i].equals("Don")) {
                    sendAlert();
                    break;
                }
                if (people[i].equals("John")) {
                    sendAlert();
                    break;
                }
            }
        }
    }
```

然后就可以把所有对控制标记的引用都去掉：

```java
    void checkSecurity(String[] people) {
        for (int i = 0; i < people.length; i++) {
            if (people[i].equals("Don")) {
                sendAlert();
                break;
            }
            if (people[i].equals("John")) {
                sendAlert();
                break;
            }
        }
    }
```



<br>

