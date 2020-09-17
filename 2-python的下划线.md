---
title:python的下划线
---

关于Python中的魔法函数.

Magic methods are a collection of pre-defined functional method from the python library functions that cannot be declared or called directly. Instead, these functions can be called or invoked by executing some other related methods in the code snippet. This type of methods are simple to use and implement, as it does not require specific or any kind of extra manual effort from the programmer. Hence it is named as the ‘Magic Method’

------------------------

Python is an interpreted, object-oriented programming which gives you the ability to write procedural code and/or object-oriented. As we know that creating Objects simplifies complicated data structures handling. In addition to that magic methods eases the ability to create object-oriented programming.
Python是一种解释的、面向对象的编程，它提供了编写过程代码和/或面向对象的能力。我们知道，创建对象简化了复杂的数据结构处理。此外，魔术方法简化了创建面向对象编程的能力

Before Diving into what is a magic method let’s understand why in the first place they are created?
在深入了解什么是魔法方法之前，让我们先了解一下为什么要创建它们

Below is one example of class one using a magic method and the other is without the magic method. In the first one __init__ magic method is used, which can be used to initialize more than one instance variable in one go. A class Sports is defined as taking two instance variables into account that is name and sport.

Both instance variables can be defined in one go using the __inti__ magic method. In case 2 the same thing is repeated but this time we are using a set method to initialize the instance variable. Here for 2 variables, we have to call this method twice.

~~~python
class Sports():
	def __init__(self,name,sport):
		self.name = name
		self.sport= sport
	def get_name(self):
		return self.name
	def get_sport(self):
		return self.sport

first = Sports('john','Game of Thrones')
print(first.get_name())
print(first.get_sport())

##output:  john  	Game of Thrones 

-------------------------------------------

class Sports():
	def set_name(self,name):
		self.name = name
	def set_sport(self,sport):
		self.sport= sport
	def get_name(self):
		return self.name
	def get_sport(self):
		return self.sport
		
second = Sports()
second.set_name('Messi')
second.set_sport('Soccer')

print(second.get_name())
print(second.get_sport())

##output: Messi  Soccer

~~~

在类中的内置的magic method有：

[魔法函数](res/内置函数.png)

### 下划线的使用说明

* 单个下划线用作接收无用变量
  
~~~python
In [1]: a, _ , _ = 1,2,3

In [2]: print(a)
1
~~~

* 单（多）个下划线作为模块内的变量（函数、类）名

在一个模块内定义了下划线开头（无论多少下划线）的变量、函数或类的话，当在别的文件中使用from module import *时，这些下划线变量不会被引用到文件内

以下几种情况还是可以把下划线变量import进来的

使用import module，此时还是可以使用module._name使用下划线变量
使用from module import _name，当然可以了
还有一种情况，当module中定义了__all__的话，且__all__中定义了下划线变量，则还是会import进来

* 类内的下划线开头的变量（函数）名

具体来说分为两种:类内单下划线开头的变量名（包括类变量与实例变量），类内双下划线开头的变量（函数）名

单下划线：
单下划线变量在没有使用@property 修饰符时，它与一般不带下划线的变量没有任何区别，可以随意的使用成员运算符.来引用或对它赋值。

~~~python
class Student():
    _school = 'xxxUniversity'
    def __init__(self, id):
        self._id = id

richard = Student(123)
print(richard._id)
print(richard._school)
# output： 123  xxxUniversity
# 加个下划线就仅仅是为了让它看起来不一样而已。实质跟普通变量没任何区别
~~~

使用了property修饰符,和C#中的属性样。

~~~python
class Student():
    _school = 'xxxUniversity'
    def __init__(self, id):
        self._id = id

    @property
    def id(self):
        print('get id')
        return self._id

    @id.setter
    def id(self, new_id):
        print('set id')
        if new_id < 0:
            pass
        else:
            self._id = new_id

richard = Student(123)
print(richard._id)

richard.id = 100
print(richard.id)

richard._id = 200
print(richard._id)
~~~

[执行结果](res/下划线_preoperty.png)

* 双下划线开头的类内变量与函数

双下划线开头的命名形式在 Python 的类成员中使用表示名字改编 (Name Mangling)，即如果有一 Test 类里有一成员 __x，那么 dir(Test) 时会看到 _Test__x 而非 __x。这是为了避免该成员的名称与子类中的名称冲突。但要注意这要求该名称末尾没有下划线。

在前面加上"__"，表示它是私有成员，我们不能直接访问。比如 “__xxx” 如果要访问得通过 _class__xxx 的方式进行访问.





































