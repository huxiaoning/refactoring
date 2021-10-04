# 6.5 Introduce Explaining Variable 引入解释性变量

<br>

<center>你有一个复杂的表达式。</center>

<br>

> **将该复杂表达式（或其中一部分）的结果放进一个临时变量，**
> **以此变量名称来解释表达式用途。**

<br>

```java
        if ((platform.toUpperCase().indexOf("MAC") > -1) &&
                (browser.toUpperCase().indexOf("IE") > -1) &&
                wasInitialized() && resize > 0) {
            // do something
        }
```

<br>

<center>⇓</center>

<br>

```java
        boolean isMacOs = platform.toUpperCase().indexOf("MAC") > -1;
        boolean isIEBrowser = browser.toUpperCase().indexOf("IE") > -1;
        boolean wasResized = resize > 0;
        if (isMacOs && isIEBrowser && wasInitialized() && wasResized) {
            // do something
        }
```

<br>

