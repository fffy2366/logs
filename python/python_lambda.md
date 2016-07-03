# python入门之lambda表达式

## 一、lambda函数

### 1、lambda函数基础：

lambda函数也叫匿名函数，即，函数没有具体的名称,而用def创建的方法是有名称的。如下：
```
"""命名的foo函数"""
def foo():return 'beginman'  #Python中单行参数可以和标题写在一行
```
```
"""lambda关键字创建匿名函数,该表达式同以上函数"""
lambda:'beginman'  
```           
上面的只是简单的用lambda创建一个函数对象，并没有保存它也没有调用它，时刻会被回收了。这里我们保存并调用：
```
bar = lambda:'beginman'
print bar()      #beginman
```
从上面几个例子中，可易理解Python lambda语法：
```
lambda [arg1[,arg2,arg3....argN]]:expression
```
lambda语句中，冒号前是参数，可以有多个，用逗号隔开，冒号右边的返回值。lambda语句构建的其实是一个函数对象。
```
print lambda:'beginman'   #<function <lambda> at 0x00B00A30>
```
### 2、无参数

如果没有参数，则lambda冒号前面就没有，如以上例子。

### 3、有参数

```
def add(x,y):return x+y
add2 = lambda x,y:x+y
print add2(1,2)     #3

def sum(x,y=10):return x+y
sum2 = lambda x,y=10:x+y
print sum2(1)       #11
print sum2(1,100)   #101
```
## 二、lambda与def

上面的例子中，可知lambda函数只是创建简单的函数对象，是一个函数的单行版本，但是这种语句由于性能的原因，调用的时候绕过函数的栈分配。python lambda还有哪些和def不一样呢？

### 1 、python lambda会创建一个函数对象，但不会把这个函数对象赋给一个标识符，而def则会把函数对象赋值给一个变量。

如：
```
>>> def foo():return 'foo()'
>>> foo
<function foo at 0x011A34F0>
```
### 2、python lambda它只是一个表达式，而def则是一个语句。lambda表达式运行起来像一个函数，当被调用时创建一个框架对象。

## 三、lambda函数的用途

个人认为有以下：

### 1、对于单行函数，使用lambda可以省去定义函数的过程，让代码更加精简。

### 2、在非多次调用的函数的情况下，lambda表达式即用既得，提高性能

注意：如果for..in..if能做的，最好不要选择lambda


来自：http://www.cnblogs.com/BeginMan/p/3178103.html
