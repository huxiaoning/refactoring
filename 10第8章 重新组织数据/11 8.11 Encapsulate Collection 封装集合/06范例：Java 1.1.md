# 范例：Java 1.1

<br>

在很多地方，` Java 1.1`的情况和`Java 2`非常相似。

这里我使用同一个范例，不过集合改为`vector`[^1]：

```java
class Person...
    public Vector getCourses() {
        return _courses;
    }
    public void setCourses(Vector arg) {
        _courses = arg;
    }
    private Vector _courses;
```

同样地，我首先建立修改函数，并初始化`_courses`字段，如下所示：

```java
class Person...
    public void addCourse(Course arg) {
        _courses.addElement(arg);
    }
    public void removeCourse(Course arg) {
        _courses.removeElement(arg);
    }
    private Vector _courses = new Vector();
```

我可以修改`setCourses()`来初始化这个`vector`： 

```java
class Person...
    public void initializeCourses(Vector arg) {
        Assert.assertTrue(_courses.isEmpty());
        Enumeration e = arg.elements();
        while (e.hasMoreElements()) {
            addCourse((Course) e.nextElement());
        }
    }
```

然后，我修改取值函数调用点，让它们改用新建的修改函数。

于是下列代码：

```java
        kent.getCourses().addElement(new Course("Brutal Sarcasm", false));
```

就变成了:

```java
        kent.addCourse(new Course("Brutal Sarcasm", false));
```

最后一步需要有点改变，因为`Java 1.1`的`Vector`类并没有提供“不可修改版”：

```java
class Person...
    Vector getCourses() {
        return (Vector) _courses.clone();
    }
```

这样便完成了集合的封装。

此后，如果不通过`Person`提供的函数，谁也不能改变集合的元素。

<br>

[^1]: 因为`vector`属于`Java 1.1`，不属于`Java 2`，——译者注

