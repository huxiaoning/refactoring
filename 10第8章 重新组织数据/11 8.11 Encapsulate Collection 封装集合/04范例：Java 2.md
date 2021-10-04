# 范例：Java 2

<br>

假设有个人要去上课。

我们用一个简单的`Course`来表示“课程”：

```java
class Course...
    public Course(String name, boolean isAdvanced) {...}
    public boolean isAdvanced() {...}
```

我不关心课程其他细节。

我感兴趣的是表示“人”的`Person`：

```java
class Person...
    public Set getCourses() {
        return _courses;
    }
    public void setCourses(Set arg) {
        _courses = arg;
    }
    private Set _courses;
```

有了这个接口，我们就可以这样为某人添加课程：

```java
        Person kent = new Person();
        Set s = new HashSet();
        s.add(new Course("Smalltalk Programming", false));
        s.add(new Course("Appreciating Single Malts", false));
        kent.setCourses(s);
        Assert.assertEquals(2, kent.getCourses().size());
        Course refact = new Course("Refactoring", true);
        kent.getCourses().add(refact);
        kent.getCourses().add(new Course("Brutal Sarcasm", false));
        Assert.assertEquals(4, kent.getCourses().size());
        kent.getCourses().remove(refact);
        Assert.assertEquals(3, kent.getCourses().size());
```

如果想了解高级课程，可以这么做：

```java
        Iterator iter = person.getCourses().iterator();
        int count = 0;
        while (iter.hasNext()) {
            Course each = (Course) iter.next();
            if (each.isAdvanced()) {
                count++;
            }
        }
```

我要做的第一件事就是为`Person`中的集合建立合适的修改函数（即添加／移除函数），如下所示，然后编译：

```java
class Person...
    public void addCourse(Course arg) {
        _courses.add(arg);
    }
    public void removeCourse(Course arg) {
        _courses.remove(arg);
    }
```

如果像下面这样初始化`_courses`字段，我的人生会轻松得多：

```java
    private Set _courses = new HashSet();
```

接下来，我需要观察设值函数的调用者。

如果有许多地点大量运用了设值函数，就需要修改设值函数，令它调用添加/移除函数。

这个过程的复杂度取决于设值函数的被使用方式。

设值函数的用法有两种，最简单的情况就是：它被用来初始化集合。

换句话说，设值函数被调用之前，`_courses`是个空集合。

这种情况下只需修改设值函数，令它调用添加函数就行了：

```java
class Person...
    public void setCourses(Set arg) {
        Assert.isTrue(_courses.isEmpty());
        Iterator iter = arg.iterator();
        while (iter.hasNext()) {
            addCourse((Course) iter.next());
        }
    }
```

修改完毕后，最好以`Rename Method (273)`更明确地展示这个函数的意图。

```java
    public void initializeCourses(Set arg) {
        Assert.isTrue(_courses.isEmpty());
        Iterator iter = arg.iterator();
        while (iter.hasNext()) {
            addCourse((Course) iter.next());
        }
    }
```

更普通的情况下[^1]，我必须首先调用移除函数将集合中的所有元素全部移除，然后再调用添加函数将元素一一添加进去。

不过我发现这种情况很少出现（唔，愈是普通的情况，愈少出现）。

<br>

如果我知道初始化时，除了添加元素，不会再有其他行为，那么我可以不使用循环，直接调用`addAll()`函数：

```java
    public void initializeCourses(Set arg) {
        Assert.isTrue(_courses.isEmpty());
        _courses.addAll(arg);
    }
```

我不能直接把传入的`set`赋值给`_courses`字段，就算原本这个字段是空的也不行。

因为万一用户在把`set`传递给`Person`对象之后又去修改`set`中的元素，就会破坏封装。

我必须像上面那样创建`set`的一个副本。

<br>

如果用户仅仅只是创建一个`set`，然后使用设值函数[^2]，我可以让它们直接使用添加／移除函数，并将设值函数完全移除。

于是，以下代码：

```java
        Person kent = new Person();
        Set s = new HashSet();
        s.add(new Course("Smalltalk Programming", false));
        s.add(new Course("Appreciating Single Malts", false));
        kent.initializeCourses(s);
```

就变成了：

```java
        Person kent = new Person();
        kent.addCourse(new Course("Smalltalk Programming", false));
        kent.addCourse(new Course("Appreciating Single Malts", false));
```

接下来，我开始观察取值函数的使用情况。

首先处理“通过取值函数修改集合元素”的情况，例如：

```java
        kent.getCourses().add(new Course("Brutal Sarcasm", false));
```

这种情况下我必须加以改变，使它调用新的修改函数：

```java
        kent.addCourse(new Course("Brutal Sarcasm", false));
```

修改完所有此类情况之后，我可以让取值函数返回一个只读副本，用以确保没有任何一个用户能够通过取值函数修改集合：

```java
    public Set getCourses() {
        return Collections.unmodifiableSet(_courses);
    }
```

这样我就完成了对集合的封装。

此后，不通过`Person`提供的添加／移除函数，谁也不能修改集合内的元素。

<br>

[^1]: 指非上述所言对空集合设初值。——译者注
[^2]: 目前已改名为`initializeCourses()`。——译者注

