# 11.10 Form TemPlate Method 塑造模板函数

<br>

<center>你有一些子类，其中相应的某些函数以相同顺序执行类似的操作，但各个操作的细节上有所不同。</center>

<br>

> **将这些操作分别放进独立函数中，并保持它们都有相同的签名，于是原函数也就变得相同了。然后将原函数上移至超类。**

<br>

![image-20211001191051634](https://raw.githubusercontent.com/huxiaoning/img/master/image-20211001191051634.png)

<br>

