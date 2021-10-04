# 6.9 Substitute Algorithm 替换算法

<br>

<center>你想要把某个算法替换为另一个更清晰的算法。</center>

<br>

> **将函数本体替换为另一个算法。**

<br>

```java
    String foundPerson(String[] people) {
        for (int i = 0; i < people.length; i++) {
            if (people[i].equals("Don")) {
                return "Don";
            }
            if (people[i].equals("John")) {
                return "John";
            }
            if (people[i].equals("Kent")) {
                return "Kent";
            }
        }
        return "";
    }
```

<br>

<center>⇓</center>

<br>

```java
    String foundPerson(String[] people) {
        List candidates = Arrays.asList("Don", "John", "Kent");
        for (int i = 0; i < people.length; i++) {
            if (candidates.contains(people[i])) {
                return people[i];
            }
        }
        return "";
    }
```

<br>

