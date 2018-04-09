---
layout: post
title: "python basic training"
date: 2018-01-06 18:00:40
image: 'https://raw.githubusercontent.com/wangliyao518/web/gh-pages/assets/img/97cce39fa7f1bfe59fe245c4ff92620c.png'
description: talk is cheap, show me the code    -- Linus Torvalds
category: 'training'
tags:
- training
- tips
twitter_text: python knowledge sharing.
introduction: we will reveal python basic knowledge
---


# Python Basic


### <center>--by wang liyao <center> ###

# agenda 

- Python History.
- Why Python?
- Work in Python
- Stdandard Type
- python operators
- Basic program
- Function
- Python file I/O
- Regular Expression
- class
- Reference






# Python History




## A Sneak View Of The History.



It was a Dutch programmer, Guido Van Rossum(吉多·范罗苏姆), who wrote Python as a hobby programming project back in the late 1980s. Since then it has grown to become one of the most polished languages of the computing world.

## What Led Guido To Create Python?

In his own words, Guido revealed the secret behind the inception of Python. He started working on it as a weekend project utilizing his free time during Christmas in Dec’1989. He originally wanted to create an interpreter, a descendant of the ABC programming language which he was a contributing developer. And we all know that it was none other than Python which gradually transformed into a full-fledged programming language

## How The Name Python Came About?

Guido initially thought the Unix/C hackers to be the target users of his project. And more importantly, he was fond of watching the famous comedy series [The Monty Python’s Flying Circus]. Thus, the name Python struck his mind as not only has it appealed to his taste but also to his target users.

### List Of Known Python Releases.

<style>
table {
    width: 100%;
    max-width: 65em;
    border: 1px solid #dedede;
    margin: 15px auto;
    border-collapse: collapse;
    empty-cells: show;
}
table th {
    font-weight: bold; /*加粗*/
    text-align: center !important; /*内容居中，加上 !important 避免被 Markdown 样式覆盖*/
    background: rgba(158,188,226,0.2); /*背景色*/
}
table td {
  height: 105px; /*统一每一行的默认高度*/
  border: 1px solid #dedede; /*内部边框样式*/
  padding: 0 30px; /*内边距*/
}
</style>
<table>
  <thead>
    <tr>
      <th>Python Version</th>
      <th>Date of Release</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Python v0.1.0 (The First Edition)</td>
      <td>1990</td>
    </tr>
    <tr>
      <td>Python v0.9.5 (Macintosh support)</td>
      <td>2nd Jan’1992</td>
    </tr>
    <tr>
      <td>Python v1.0.0</td>
      <td>26th Jan’1994</td>
    </tr>
    <tr>
      <td>Python v1.1.0</td>
      <td>26th Jan’1994</td>
    </tr>
    <tr>
      <td>Python v1.2.0</td>
      <td>Apr’1995</td>
    </tr>
    <tr>
      <td>Python v1.3.0</td>
      <td>Oct’1995</td>
    </tr>
    <tr>
      <td>Python v1.4.0</td>
      <td>Oct’1996</td>
    </tr>
     <tr>
      <td>Python v1.5.0	3rd</td>
      <td>Jan’1998</td>
    </tr>
    <tr>
      <td>Python v1.6.0 (Latest updated version)</td>
      <td>5th Sep’2000</td>
    </tr>
    <tr>
      <td>Python v2.0.0 (Added list comprehensions)</td>
      <td>16th Oct’2000</td>
    </tr>
    <tr>
      <td>Python v2.7.0 (Latest updated version)</td>
      <td>3rd Jul’2010</td>
    </tr>
    <tr>
      <td>Python v3.0.0	3rd</td>
      <td>Dec’2008</td>
    </tr>
    <tr>
      <td>Python v3.6.X (Latest updated versio)</td>
      <td>Mar’2017 and continued.</td>
    </tr>
  </tbody>
</table>

# Why Python?



>Life is short, you need Python. “人生苦短，我用Python” --by [Bruce Eckel](http://sebsauvage.net/python/)

![life_is_short_you_need_python.jpg](attachment:life_is_short_you_need_python.jpg)

## python use scenario
![python_applicaton.png](attachment:python_applicaton.png)





## use python company and market situation

![python_org.png](attachment:python_org.png)
        

# Work in Python

## Work in Python
- install
- Edit
- Debug

## Install 
- ** Cpython **
- ** Jython **
- ** IronPy  thon ** 
- ** Pypy **



### Install python On Your System



- If you're running Windows: the most stable Windows downloads are available from the [Python for Windows page](https://www.python.org/downloads/windows/).

- If you're running Windows XP: the guide to installing ActivePython is at [Python on XP: 7 Minutes To "Hello World!".MeDo](http://www.richarddooling.com/index.php/2006/03/14/python-on-xp-7-minutes-to-hello-world/) has two videos for installing and getting started with Python on a Windows XP machine - this series talks you through the Python, [ActivePython](https://wiki.python.org/moin/ActivePython) and [SciPy](https://wiki.python.org/moin/SciPy) distributions.

- If you are using a Mac, see the [Python for Mac OS X page](https://www.python.org/downloads/mac-osx/). MacOS 10.2 (Jaguar), 10.3 (Panther), 10.4 (Tiger) and 10.5 (Leopard) already include various versions of Python.

- For Red Hat, install the python2 and python2-devel packages.

- For Debian or Ubuntu, install the python2.x and python2.x-dev packages.

- For Gentoo, install the '=python-2.x*' ebuild (you may have to unmask it first).

- For other systems, or if you want to install from source, see the [general download page](http://www.python.org/download/).

### verify Python version



```python

#Python 2.7  vs Python3
$ python –version
Python 2.7.12

import sys
print sys.version_info
print sys.version

```

## Edit
- eclipse
- pycharm
- VIM/Emacs/Notepad++
- Jupyter
- [codepad](http://codepad.org/)
- ** [pythonanywhere](https://www.pythonanywhere.com/) **


##  Debug

- print
- python inspect
- pdb
- logging



### print

print in python 2 print() in python 3 print str(A)


```python
print 'hello world'

print 'hello world',

print "中国"

print '%x' % 18
print '%o' % 18
```

### [Print Formatter](https://blog.csdn.net/zanfeng/article/details/52164124)


```python
strHello = "the length of (%s) is %d" %('Hello World',len('Hello World'))
print strHello


```


```python
nHex = 0x20
#%x --- hex 十六进制
#%d --- dec 十进制
#%o --- oct 八进制
 
print "nHex = %x,nDec = %d,nOct = %o" %(nHex,nHex,nHex)
```


```python
import math
#default
print "PI = %f" % math.pi
#width = 10,precise = 3,align = left
print "PI = %10.3f" % math.pi
#width = 10,precise = 3,align = rigth
print "PI = %-10.3f" % math.pi
#前面填充字符
print "PI = %06d" % int(math.pi)
 
#输出结果
#PI = 3.141593
#PI =      3.142
#PI = 3.142
#PI = 000003
#浮点数的格式化，精度、度和
```


### formatter type
- 'b' - 二进制。将数字以2为基数进行输出。
- 'c' - 字符。在打印之前将整数转换成对应的Unicode字符串。
- 'd' - 十进制整数。将数字以10为基数进行输出。
- 'o' - 八进制。将数字以8为基数进行输出。
- 'x' - 十六进制。将数字以16为基数进行输出，9以上的位数用小写字母。
- 'e' - 幂符号。用科学计数法打印数字。用'e'表示幂。
- 'g' - 一般格式。将数值以fixed-point格式输出。当数值特别大的时候，用幂形式打印。
- 'n' - 数字。当值为整数时和'd'相同，值为浮点数时和'g'相同。不同的是它会根据区域设置插入数字分隔符。
- '%' - 百分数。将数值乘以100然后以fixed-point('f')格式打印，值后面会有一个百分号。


```python
### [example](https://blog.csdn.net/ztf312/article/details/47173575)
# 打印字符串  
print ("His name is %s" % ("Aviad"))  
#His name is Aviad  
# 打印整数  
print ("He is %d years old" % (25))  
#He is 25 years old<pre name="code" class="python">print ("He is %d years old" % (25))  
#He is 25 years old  
# 打印浮点数  
print ("His height is %f m" % (1.83))  
#His height is 1.83 m  
# 打印浮点数（指定保留小数点位数）  
print ("His height is %.2f m" % (1.83))  
#His height is 1.83 m"print "His height is ", format(1.83, '.2f'), "m"  
# 指定占位符宽度  
print ("Name:%10s Age:%8d Height:%8.2f" % ("Aviad",25,1.83))  
#Name:Aviad Age: 25 Height: 1.83  
# 指定占位符宽度（左对齐）  
print ("Name:%-10s Age:%-8d Height:%-8.2f" % ("Aviad",25,1.83))  
#Name:Aviad Age:25 Height:1.83  
# 指定占位符（用0或者空格当占位符）  
print ("Name:%-10s Age:%08d Height:%08.2f" % ("Aviad",25,1.83))  
#Name:Aviad Age:00000025 Height:00001.83  
# 调用format函数,format(数值, '格式')  
print('test:{0:10f}'.format(math.pi))  
#test: 3.141593#若输出位数小于10，则默认右对齐。若输出位数大于宽度，则按实际位数输出format(0.0015,'.2e')  
#1.50e-03# 格式化指示符  
print '6:\t|{0:b}'.format(3)  
print '7:\t|{0:c}'.format(3)  
print '8:\t|{0:d}'.format(3)  
print '9:\t|{0:o}'.format(3)  
print '10:\t|{0:x}'.format(3)  
print '11:\t|{0:e}'.format(3.75)  
print '12:\t|{0:g}'.format(3.75)  
print '13:\t|{0:n}'.format(3.75) #浮点数  
print '14:\t|{0:n}'.format(3) #整数  
print '15:\t|{0:%}'.format(3.75)
```

what is %r in print ?

what is print in python 2.* ?

### python inspect


```python
import this
```

#### help()

#### vars()

#### dir()

#### inspect


```python
from collections import namedtuple
import inspect 
print(inspect.getsource(namedtuple))

```

### [pdb](https://docs.python.org/3/library/pdb.html) 

用pdb调试有多种方式可选：

1. 命令行启动目标程序，加上-m参数，这样调用myscript.py的话断点就是程序的执行第一行之前
python -m pdb myscript.py

2. 在Python交互环境中启用调试
```python
import pdb
import mymodule
pdb.run(‘mymodule.test()’)
```

3. 比较常用的，就是在程序中间插入一段程序，相对于在一般IDE里面打上断点然后启动debug，不过这种方式是hardcode的
```python
if __name__ == "__main__":
a = 1
import pdb
pdb.set_trace()
b = 2
c = a + b
print (c)
```

### [logging](https://docs.python.org/3/library/logging.html)


#### basic useage

```python
import logging
logging.basicConfig(level = logging.INFO,format = '%(asctime)s - %(name)s - %(levelname)s - %(message)s')
logger = logging.getLogger(__name__)

logger.info("Start print log")
logger.debug("Do something")
logger.warning("Something maybe fail.")
logger.info("Finish")
```


logging.basicConfig函数各参数：
filename：指定日志文件名；
filemode：和file函数意义相同，指定日志文件的打开模式，'w'或者'a'；
format：指定输出的格式和内容，format可以输出很多有用的信息，

参数：作用
%(levelno)s：打印日志级别的数值
%(levelname)s：打印日志级别的名称
%(pathname)s：打印当前执行程序的路径，其实就是sys.argv[0]
%(filename)s：打印当前执行程序名
%(funcName)s：打印日志的当前函数
%(lineno)d：打印日志的当前行号
%(asctime)s：打印日志的时间
%(thread)d：打印线程ID
%(threadName)s：打印线程名称
%(process)d：打印进程ID
%(message)s：打印日志信息
datefmt：指定时间格式，同time.strftime()；
level：设置日志级别，默认为logging.WARNNING；
stream：指定将日志的输出流，可以指定输出到sys.stderr，sys.stdout或者文件，默认输出到sys.stderr，当stream和filename同时指定时，stream被忽略；

#### logging file


```python
import logging
logger = logging.getLogger(__name__)
logger.setLevel(level = logging.INFO)
handler = logging.FileHandler("log.txt")
handler.setLevel(logging.INFO)
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
handler.setFormatter(formatter)
logger.addHandler(handler)

logger.info("Start print log")
logger.debug("Do something")
logger.warning("Something maybe fail.")
logger.info("Finish")
```

#### loggoing to console and file


```python
import logging
logger = logging.getLogger(__name__)
logger.setLevel(level = logging.INFO)
handler = logging.FileHandler("log.txt")
handler.setLevel(logging.INFO)
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
handler.setFormatter(formatter)

console = logging.StreamHandler()
console.setLevel(logging.INFO)

logger.addHandler(handler)
logger.addHandler(console)

logger.info("Start print log")
logger.debug("Do something")
logger.warning("Something maybe fail.")
logger.info("Finish")
```

# Standard Type


## Standard Type
- Booleans
- int
- string
- list
- tuple
- DIctionary

## Standard Type

A boolean is such a data type that almost every programming language has, and so is Python. Boolean in Python can have two values – True or False. These values are constants and can be used to assign or compare boolean values. Follow a simple example given below.
```
condition = False
if condition == True:
    print("You can continue with the prpgram.")
else:
    print("The program will end here.")
```
While making boolean conditions in Python, we can skip the explicit comparison in our code. And we’ll still get the same behavior.
```
condition = False
if condition:
    print("You can continue with the prpgram.")
else:
    print("The program will end here.")
```



In some cases, the boolean constants “True” and “False” might also act as numbers.
```
>>> A, B = True + 0, False + 0
>>> print(A, B)
1 0
>>> type(A), type(B)
(<class 'int'>, <class 'int'>)
```


```python
# What is the answer below?
print True/1
print True%1
print "True==1", True==1
print "False==0", False==0
print "True==2",True==2
print "True==hello", True == "hello"
if "hello":
    print 'yes, hello!'
if "":
    print "yes, empty!"
if " ":
    print 'yes, blank'
if 2:
    print "yes, 2!"
print (1)==True
print (1, )==True
if (0):
    print '(0) yes'
if (0,):
    print '(0,) yes'

```

## Standard Type




### int


- 10, 0b10, 010, 0x10

- int ()
- long() in python 2

- size of int
** 32/64 bits in python 2
** No limit in python 3

## Standard Type


### String
- char in sequences

```python
a = "Hello World"
b = 'Python is groovy'

c = "This is a long string \
which is splitted in tow lines"

d = '''Content-type: text/html
<h1> Hello World </h1>
Click <a href="https://www.python.org">here</a>.
'''
```


### String
#### indexing

### 0, 1, 2, 3...-3, -2, -1
```python
a = "Hello World"

b = a[4]
```

#### Slicing [start:end:stride]
```python
e = a[3:8]
print 'e:', e
f = a[1:9:2]
print "f:", f
c = a[:5]
print "c:", c
d = a[6:]
print 'd:', d
```
#### string1 + string 2 -> "string1 string2"
```python
print "hello" + "nokia"
```
#### update -- String is immutable so it can not be changed after creation
```python
a = "string1"
b = a + "tail"
print b, id(a), id(b)
```



### String
- split, join

s = 'a,b,c,d,e'
l = s.split(',')        # l == [‘a’, ‘b’, ‘c’, ‘d’, ‘e’]
s = '|'.join(l)         # s == 'a|b|c|d|e'

- str()
- len()  --  no recommended 
- ‘’.startswith(‘All’), endswith(‘OK’)
- “”.find(‘the’), “”.rfind(‘end’)
- “”.count(“a”)
- “”.isalnum(), “”.upper(), “”.lower()
- “”.strip()
- “”.replace(‘old’, ‘new’, max_times)




### string modulus: s % d
- s: format string
- d: a collection of objects in a tuple or dict

```python
x = 34
y = 32
s1 = "The value of x, y is %d %d" % (x, y)

d = {'x':13, 'y':1.54321, 'z’: 'world'}
r = "%(x)d %(y).2f" % d # r = "13 1.54"
```

### string

** Exercise: **

Giving a string “I am from Nokia”. Get these values with string operations.
1. the third char 
2. every 4th char 

## Standard Type

### List

- create
- indexing
- slicing
- unpacking
- update


### list
- create
```python
empty_list = []
another_empty_list = list()
Weekdays = ['Monday','Tuesday','Wednesday','Thursday','Friday']
```
- Indexing
```python
print Weekdays[0], Weekdays[-1]
```
- slicing
```python
print Weekdays[2:-1]
```
- Unpacking
```python
first_name, second_name = ["san", "zhang"]
a, b, c = [1, [2, 3]]  #??
```

- update
```python
names = []
names[0] = "Jeff” #???
names[0:2] = ['Mike', 'Tom', 'Mary'] ##???
names.append("Paula"), names.pop(), names.pop(0)
names.insert(2, "Thomas")
del names[0]      #Item deletion
del names[0:2]    #Slice deletion
a = [1,2,3] + [4,5] # Result is [1,2,3,4,5]
```

### list

- ‘john’ in [‘Chico’, ’Coach’, ’john’]
- list.sort(), list.sort(reverse=True)
- sorted(list)
- len()
- =, copy(), list(), [:]

```python
a = [1, 2, 3]
b = a
c = copy.copy(a)
d = list(a)
e = a[:]
```



```python
import copy
a = [1, 2, 3]
b = a
c = copy.copy(a)
d = copy.deepcopy(a)
e = list(a)
f = a[:]
id(a), id(b), id(c), id(d), id(e), id(f)
```

### Exercise!


-  Create a list named ‘things’ with ‘mozzarella’, ‘cinderella’, and ‘salmonella’.
    1. Capitalize all in ‘things’
    2. Sorting ‘things’ from ‘z’ to ‘a’


```python
strs = ['mozzarella', 'cinderella', 'salmonella']
for s in strs:
    print s.capitalize()
    s = s[0].upper() + s[1:]
    print s

strs.sort(reverse=True)
print strs

print sorted(strs, reverse=True)

```

## Standard Type
 

### tuple

- Constant list
    (    )
    tuple()
```python
marx_tuple = "Groucho", 'Chico', 'Harpo'
a, b, c = marx_tuple
```




### Exercise

Switch value of variables: ‘password’, ‘icecream’ in one statement


```python
b, a = 'password', 'icecream'
print (a, b)
```

## Standard Type

### Dictionary


A dictionary in Python is an unordered collection of key-value pairs. It’s a built-in mapping type in Python where keys map to values. These key-value pairs provide an intuitive way to store data.

- Why Need A Dictionary?
- Creating A Dictionary
- Accessing Dictionaries Elements With Keys
- Dictionaries Methods To Access Elements
- Modifying A Dictionary (Add/Update/Delete)

#### Why Need A Dictionary?

The dictionary solves the problem of efficiently storing a large data set. Python has made the dictionary object highly optimized for retrieving data.

#### Creating A Dictionary

Python syntax for creating dictionaries use braces {} where each item appears as a pair of keys and values. The key and value can be of any Python data types.
```
sample_dict = {'key':'value', 'jan':31, 'feb':28, 'mar':31}
type(sample_dict)
sample_dict
```

#### Accessing Dictionaries Elements With Keys
Dictionaries act like a database. Here, we don’t use a number to get a particular index value as we do with a list. Instead, we replace it with a key and then use the key to fetch its value.
```
>>> sample_dict['jan']
31
>>> sample_dict['feb']
28
>>> sample_dict.get('mar')
31
```



#### Dictionaries Methods To Access Elements

Python exposes following built-in dictionary functions.

- keys() – It isolates the keys from a dictionary.
- values() – It isolates the values from a dictionary.
- items() – It returns the items in a list style of (key, value) pairs.
```
>>> sample_dict.keys()
dict_keys(['mar', 'key', 'jan', 'feb'])
>>> sample_dict.values()
dict_values([31, 'value', 31, 28])
>>> sample_dict.items()
dict_items([('mar', 31), ('key', 'value'), ('jan', 31), ('feb', 28)])
```


#### Modifying A Dictionary (Add/Update/Delete)

Since the dictionary object is mutable, so we can call add, update and delete operations on a dictionary object.

See the below example for more clarity on how to modify a dictionary.
```
>>> sample_dict['feb'] = 29
>>> sample_dict
{'mar': 31, 'key': 'value', 'jan': 31, 'feb': 29}
>>> sample_dict.update({'apr':30})
>>> sample_dict
{'apr': 30, 'mar': 31, 'key': 'value', 'jan': 31, 'feb': 29}
>>> del sample_dict['key']
>>> sample_dict
{'apr': 30, 'mar': 31, 'jan': 31, 'feb': 29}
>>> lot = [('green', 'ground'), ('red', 5), ('blue', ['sky', 'sea'])]
>>>dlot = dict(lot)
>>> dlot
{'blue': ['sky', 'sea'], 'green': 'ground', 'red': 5}
>>> list(dlot.items())
[('blue', ['sky', 'sea']), ('green', 'ground'), ('red', 5)]
```

### Exercise

- Create a English-French dictionary named ‘e2f’, ‘dog’ is ‘chien’, ‘cat’ is ‘chat’, ‘walrus’ is ‘morse’
    1. Get French of ‘walrus’
    2. Create f2e dictionary from e2f



```python
e2f = {'dog':'chien', 'cat':'chat','walrus':'morse'}
print e2f['walrus']

f2e = dict(zip(e2f.values(), e2f.keys()))
print f2e

```

##  python operators
- What Are Built-In Python Operators?
- Arithmetic Operators
- Comparison Operators
- Logical Operators

### What Are Built-In Python Operators?
Like many programming languages, Python reserves some special characters for acting as operators. Every operator has a pre-defined action like addition, multiplication to manipulate data and variables. The variables passed as input to an operator are known as operands. We also recommend you to read about keywords in Python.
```
>>> 7%4
3
>>> 7+4-2
9
>>>2*(3+4)
14
```


### Arithmetic Operators
With arithmetic operators, we can do various arithmetic operations like addition, subtraction, multiplication, division, modulus, exponent, etc. Python provides multiple ways for arithmetic calculations like eval function, declare variable & calculate, or call functions.

The table below outlines the built-in arithmetic operators in Python.

![_auto_0](attachment:_auto_0)


#### Example


```python
a=7
b=4

print('Sum : ', a+b)
print('Subtraction : ', a-b)
print('Multiplication : ', a*b)
print('Division (float) : ', a/b)
print('Division (floor) : ', a//b)
print('Modulus : ', a%b)
print('Exponent : ', a**b)
print('Division (float) : ', 7.0/4)
print('Division (floor) : ', 7.0//4)

```

### Comparison Operators

In Python programming, comparison operators allow us to determine whether two values are equal or if one is greater than the other and then make a decision based on the result.

The table below outlines the built-in comparison operators in Python.

![_auto_0](attachment:_auto_0)

#### Example


```python
a=7
b=4

print('a > b is',a>b)

print('a < b is',a<b)

print('a == b is',a==b)

print('a != b is',a!=b)

print('a >= b is',a>=b)

print('a <= b is',a<=b)
```

### Logical Operators

The logical Python operators enable us to make decisions based on multiple conditions. The operands act as conditions that can result in a true or false value. The outcome of such an operation is either true or false (i.e., a Boolean value).

However, not all of these operators return a boolean result. The ‘and’ and ‘or’ operators do return one of their operands instead of a pure boolean value. Whereas the ‘not’ operator always gives a real boolean outcome.

Refer the below table and the example to know how these operators work in Python.

![_auto_0](attachment:_auto_0)

#### example


```python
a=7
b=4

# Result: a and b is 4
print('a and b is',a and b)

# Result: a or b is 7
print('a or b is',a or b)

# Result: not a is False
print('not a is',not a)
```

### Bitwise Operators

Bitwise Python operators process the individual bits of integer values. They treat them as sequences of binary bits.

We can use bitwise operators to check whether a particular bit is set. For example, IoT applications read data from the sensors based on a specific bit is set or not. In such a situation, these operators can help.

![_auto_0](attachment:_auto_0)

#### Example-

Let’s consider the numbers 4 and 6 whose binary representations are ‘00000100’ and ‘00000110’. Now, we’ll perform the AND operation on these numbers.


```python
a=4
b=6

#Bitwise AND: The result of 'a & b' is 4
print('a & b is',a & b)
```

The above result is the outcome of following AND (‘&’) operation.
![_auto_0](attachment:_auto_0)


## Basic program
- variables
- condition expresson
- Loop




### variables
- nameing
- assignment with =
- copy with copy()

### variables
- naming


- (a-z), (A-Z), (0-9), (_)
- Not Startswith (0-9)

### assignment with =


```python
principal = 1000
rate = 0.05
numyears = 5
year = 1
```

### copy with copy()



```python
A = {'dog':'chien', '1':[1,2,3], 'dict':{'walrus':"morse"}}
B = A
C = A.copy()
A['dog'] = 'Kitty'
A['1'].append(6)
print id(A), A
print id(B), B
print id(C), C

```

Before understanding shallow and deep copies, first understand how variables are stored in Python;
The type of a variable is a binary reference and an address reference.
All of python's variables are objects, the storage of variables, the way the address is referenced, the memory address that the value of a variable is stored, not the only one of the variable itself.

![_auto_0](attachment:_auto_0)

```python
 >>> str_1 = 'abc'
 >>> id(str_1)
 4300773168
 >>> str_2 = str_1
 >>> id(str_2)
 4300773168
```
![_auto_0](attachment:_auto_0)

```
>>> str_1 = 123
>>> id(str_2)
 4300773168
>>> id(str_1)
4297541792
```
![_auto_0](attachment:_auto_0)

```python
>>> list_1 =[1,2,3]
>>> id(list_1)
4320183368
>>> list_1.append(9)
>>> list_1[2] = 22
>>> list_1.pop(2)
3
>>> print(list_1,id(list_1))
[1, 2, 22, 5, 6, 9] 4320183368
```
![_auto_0](attachment:_auto_0)



### copy
浅拷贝: 不管是多么复杂的数据结构，浅拷贝只会拷贝第一层.
```python
import copy
list_1 = [1,2,['a','b','c'],3]
list_2 = list_1[:]
# list_2 = copy.copy(list_1)浅拷贝的另一种方式
list_1[2][1] = 'kk'
print(list_1,list_2,id(list_1[2]),id(list_2[2]))
[1, 2, ['a', 'kk', 'c'], 3]  [1, 2, ['a', 'kk', 'c'], 3] 4330513736 4330513736
```
![_auto_0](attachment:_auto_0)

### deep copy
.深拷贝: 深拷贝会完全复制原变量的所有数据，在内存中生成一套完全一样的内容，我们对这两个变量中的一个进行任意修改都不会影响另一个变量。
```python
import copy
list_1 = [1,2,['a','b','c'],3]
list_2 = copy.deepcopy(list_1)
list_1[2][1] = 'kk'
print(list_1,list_2,list_1[2],list_2[2])
[1, 2, ['a', 'kk', 'c'], 3]  [1, 2, ['a', 'b', 'c'], 3] 4330513736 4330512584
```

### Condition Expression



```python
if a < b:
    print "Computer says Yes"
else:
    print "Computer says No"

if suffix == ".htm":
    content = "text/html"
elif suffix == ".jpg":
    content = "image/jpeg"
else:
    print("Unknown content type")


```

- is, ==, !=, <, <=, >, >=, in, not


```python
if product == "game" and not (age < 4 or age > 8) \
   or kind == "pirate memory":
    print "I'll take it!“

if a is b:
    a += c
else:
    b -= c
if a is not b:
    print True
    
```

```python
if not something == ‘’:
    …
else:
    …

if something:
    …
else:
    …
```

### Exercise
- Write down a condition expression only when ‘package_build’ starts with ‘dx’, ‘sg’ or ‘ms’ and doesn’t end with ‘001’, print out ‘successful’; otherwise print out ‘failed’


```python
package_build = ''
if (package_build.startswith('dx') or \
    package_build.startswith('sg') or \
    package_build.startswith('ms')) and \
    not package_build.endswith('001'):
    print 'successful'
else:
    print 'Failed'

```

### Loop


```python
numbers = [1,3,5, 6]
position = 0
while position < len(numbers):
    number = numbers[position]
    if number % 2 == 0:
        print 'Found Even number', number
        break
    position += 1
else:
    print "No even number found"

```


```python
if not find_even_number(numbers):
    print ‘No even number found’

def find_even_number(numbers)
    position = 0 
    while position < len(numbers):
        number = numbers[position]
        if number % 2 == 0:
            print ‘Found Even number’, number
            return True
        position += 1

```

### Iterator


```python
for pos, num in enumerate(numbers):
    print pos, num

for key in dict:
    print dict[key]

for key, value in dict.items():
    print key, value

for key, value in dict.iteritems():
    print key, value

```

### Exercise
Traverse dictionary ‘students’ to find all ‘male’ and older than 18, if found, return name list
Student = {‘Emily’: ‘female:29:normal’, ‘David’: ’male:28:normal’, ‘James’: ‘male:17:normal’}



```python
# Answers
students = {'Emily': 'female:29:normal', 'David':'male:28:normal','James':'male:17:normal'}

names = []
for name, value in students.items():
    age = value.split(':')[1]
    if int(age) > 18:
        names.append(name)

print names

[name for name, value in students.items() if int(value.split(':')[1]) > 18]

```

## function
- What is a function in Python?
- The return statement
- How Function works in Python?
- Scope and Lifetime of variables
- Python Built-in Function
- Variable Function Arguments








### What is a function in Python?
In Python, function is a group of related statements that perform a specific task.

Functions help break our program into smaller and modular chunks. As our program grows larger and larger, functions make it more organized and manageable.

Furthermore, it avoids repetition and makes code reusable.


```python
def function_name(parameters):
    """docstring"""
    statement(s)
```

### what is function in python?

Above shown is a function definition which consists of following components.

    1. Keyword def marks the start of function header.
    2. A function name to uniquely identify it. Function naming follows the same rules of writing identifiers in Python.
    3. Parameters (arguments) through which we pass values to a function. They are optional.
    4. A colon (:) to mark the end of function header.
    5. Optional documentation string (docstring) to describe what the function does.
    6. One or more valid python statements that make up the function body. Statements must have same indentation level (usually 4 spaces).
    7. An optional return statement to return a value from the function.

### Example of a function


```python
def greet(name):
	"""This function greets to
	the person passed in as
	parameter"""
	print("Hello, " + name + ". Good morning!")
```

### How to call a function in python?

Once we have defined a function, we can call it from another function, program or even the Python prompt. To call a function we simply type the function name with appropriate parameters.
```python
>>> greet('Paul')
Hello, Paul. Good morning!
```


### The return statement
The return statement is used to exit a function and go back to the place from where it was called.

** Syntax of return **
```python
return [expression_list]
```
This statement can contain expression which gets evaluated and the value is returned. If there is no expression in the statement or the return statement itself is not present inside a function, then the function will return the None object.

For example:
```python
>>> print(greet("May"))
Hello, May. Good morning!
None
```
	
Here, None is the returned value.


```python
# example of return
def absolute_value(num):
	"""This function returns the absolute
	value of the entered number"""

	if num >= 0:
		return num
	else:
		return -num

# Output: 2
print(absolute_value(2))

# Output: 4
print(absolute_value(-4))
```

### How Function works in Python?

![python-how-function-works_1.jpg](attachment:python-how-function-works_1.jpg)

### Scope and Lifetime of variables

Scope of a variable is the portion of a program where the variable is recognized. Parameters and variables defined inside a function is not visible from outside. Hence, they have a local scope.

Lifetime of a variable is the period throughout which the variable exits in the memory. The lifetime of variables inside a function is as long as the function executes.

They are destroyed once we return from the function. Hence, a function does not remember the value of a variable from its previous calls.

Here is an example to illustrate the scope of a variable inside a function.


```python
def my_func():
	x = 10
	print("Value inside function:",x)

x = 20
my_func()
print("Value outside function:",x)
```

### Python Built-in Function
The Python interpreter has a number of functions that are always available for use. These functions are called built-in functions. For example, print() function prints the given object to the standard output device (screen) or to the text stream file.

In Python 3.6 (latest version), there are 68 built-in functions. They are listed below alphabetically along with brief description.

https://www.programiz.com/python-programming/methods/built-in

### Variable Function Arguments

Function arguments can have default values in Python.

We can provide a default value to an argument by using the assignment operator (=). Here is an example.

```python
def greet(name, msg = "Good morning!"):
   """
   This function greets to
   the person with the
   provided message.

   If message is not provided,
   it defaults to "Good
   morning!"
   """

   print("Hello",name + ', ' + msg)

greet("Kate")
greet("Bruce","How do you do?")
```


In this function, the parameter name does not have a default value and is required (mandatory) during a call.

On the other hand, the parameter msg has a default value of "Good morning!". So, it is optional during a call. If a value is provided, it will overwrite the default value.

Any number of arguments in a function can have a default value. But once we have a default argument, all the arguments to its right must also have default values.

This means to say, non-default arguments cannot follow default arguments. For example, if we had defined the function header above as:
```python
def greet(msg = "Good morning!", name):
```
We would get an error as:
```python
SyntaxError: non-default argument follows default argument
```
    

#### Python Keyword Arguments

Python allows functions to be called using keyword arguments. When we call functions in this way, the order (position) of the arguments can be changed. Following calls to the above function are all valid and produce the same result.
```python
>>> # 2 keyword arguments
>>> greet(name = "Bruce",msg = "How do you do?")

>>> # 2 keyword arguments (out of order)
>>> greet(msg = "How do you do?",name = "Bruce") 

>>> # 1 positional, 1 keyword argument
>>> greet("Bruce",msg = "How do you do?") 
```
As we can see, we can mix positional arguments with keyword arguments during a function call. But we must keep in mind that keyword arguments must follow positional arguments.

#### Python Arbitrary Arguments

Sometimes, we do not know in advance the number of arguments that will be passed into a function.Python allows us to handle this kind of situation through function calls with arbitrary number of arguments.

In the function definition we use an asterisk (*) before the parameter name to denote this kind of argument. Here is an example.


```python
def greet(*names):
   """This function greets all
   the person in the names tuple."""

   # names is a tuple with arguments
   for name in names:
       print("Hello",name)

greet("Monica","Luke","Steve","John")
```


```python
def greet_main(salutatory, *names):
    print(salutatory)
    greet(*names)


def greet(*names):
   """This function greets all
   the person in the names tuple."""

   # names is a tuple with arguments
   for name in names:
       print("Hello",name)

greet_main("welcome", "Monica","Luke","Steve","John")

name_list = ("welcome", "wang","leo","li","yao")
greet(*name_list)

```

### **kwargs


```python

def foo(arg1, *tupleArg, **dictArg):
    print "arg1=",arg1          #arg1=leason
    print "tupleArg=",tupleArg  #()
    print "dictArg=",dictArg    #[]
foo("leason", 'python', 'shell', 'ruby', duration=1.5, trainer='leo')
```


```python
# 接收不定长参数**kwargs
def fun_var_kwargs(arg1, **kwargs):  
    print "arg1:", arg1  
    for key in kwargs:  
        print "%s: %s" % (key, kwargs[key])
fun_var_kwargs(arg1=1, arg2=2, arg3=3) # **kwargs可以当作容纳多个key和value的dict

kwargs = {"arg_3": -3, "arg_2": -2} # dictionary
fun_var_kwargs(-1, **kwargs)  

```

## Python file I/O

- What is a file?
- How to open a file?
- How to close a file Using Python?
- How to write to File Using Python?
- How to read files in Python?
- Python File Methods

### what is a file

File is a named location on disk to store related information. It is used to permanently store data in a non-volatile memory (e.g. hard disk).

Since, random access memory (RAM) is volatile which loses its data when computer is turned off, we use files for future use of the data.

When we want to read from or write to a file we need to open it first. When we are done, it needs to be closed, so that resources that are tied with the file are freed.

Hence, in Python, a file operation takes place in the following order.

    1. Open a file
    2. Read or write (perform operation)
    3. Close the file

### How to open a file?
Python has a built-in function open() to open a file. This function returns a file object, also called a handle, as it is used to read or modify the file accordingly.
```python
>>> f = open("test.txt")    # open file in current directory
>>> f = open("C:/Python33/README.txt")  # specifying full path
```

We can specify the mode while opening a file. In mode, we specify whether we want to read 'r', write 'w' or append 'a' to the file. We also specify if we want to open the file in text mode or binary mode.

The default is reading in text mode. In this mode, we get strings when reading from the file.

On the other hand, binary mode returns bytes and this is the mode to be used when dealing with non-text files like image or exe files.


<table border="1">
	<caption>Python File Modes</caption>
	<tbody>
		<tr>
			<th>Mode</th>
			<th>Description</th>
		</tr>
		<tr>
			<td>&#39;r&#39;</td>
			<td>Open a file for reading. (default)</td>
		</tr>
		<tr>
			<td>&#39;w&#39;</td>
			<td>Open a file for writing. Creates a new file if it does not exist or truncates the file if it exists.</td>
		</tr>
		<tr>
			<td>&#39;x&#39;</td>
			<td>Open a file for exclusive creation. If the file already exists, the operation fails.</td>
		</tr>
		<tr>
			<td>&#39;a&#39;</td>
			<td>Open for appending at the end of the file without truncating it. Creates a new file if it does not exist.</td>
		</tr>
		<tr>
			<td>&#39;t&#39;</td>
			<td>Open in text mode. (default)</td>
		</tr>
		<tr>
			<td>&#39;b&#39;</td>
			<td>Open in binary mode.</td>
		</tr>
		<tr>
			<td>&#39;+&#39;</td>
			<td>Open a file for updating (reading and writing)</td>
		</tr>
	</tbody>
</table>

r只读，r+读写，不创建

w新建只写，w+新建读写，二者都会将文件内容清零

（以w方式打开，不能读出。w+可读写）

w+与r+区别：

r+：可读可写，若文件不存在，报错；w+: 可读可写，若文件不存在，创建

r+与a+区别：
r+进行了覆盖写。以a,a+的方式打开文件，附加方式打开

```python
fd = open("1.txt",'w+')  
fd.write('123')  
fd = open("1.txt",'r+')  
fd.write('456')  
fd = open("1.txt",'a+')  
fd.write('789')
# output 456789
```

```python
f = open("test.txt")      # equivalent to 'r' or 'rt'
f = open("test.txt",'w')  # write in text mode
f = open("img.bmp",'r+b') # read and write in binary mode
```

Moreover, the default encoding is platform dependent. In windows, it is 'cp1252' but 'utf-8' in Linux.

So, we must not also rely on the default encoding or else our code will behave differently in different platforms.

Hence, when working with files in text mode, it is highly recommended to specify the encoding type.
```python
f = open("test.txt",mode = 'r',encoding = 'utf-8')
```

### How to close a file Using Python?

When we are done with operations to the file, we need to properly close the file.

Closing a file will free up the resources that were tied with the file and is done using Python close() method.

Python has a garbage collector to clean up unreferenced objects but, we must not rely on it to close the file.


```python

f = open("test.txt",encoding = 'utf-8')
# perform file operations
f.close()

```

This method is not entirely safe. If an exception occurs when we are performing some operation with the file, the code exits without closing the file.

A safer way is to use a try...finally block.
```python
try:
   f = open("test.txt",encoding = 'utf-8')
   # perform file operations
finally:
   f.close()
```

This way, we are guaranteed that the file is properly closed even if an exception is raised, causing program flow to stop.

The best way to do this is using the with statement. This ensures that the file is closed when the block inside with is exited.

We don't need to explicitly call the close() method. It is done internally.

```python
with open("test.txt",encoding = 'utf-8') as f:
   # perform file operations
```

### How to write to File Using Python?

We need to be careful with the 'w' mode as it will overwrite into the file if it already exists. All previous data are erased.

Writing a string or sequence of bytes (for binary files) is done using write() method. This method returns the number of characters written to the file.

```python
with open("test.txt",'w',encoding = 'utf-8') as f:
   f.write("my first file\n")
   f.write("This file\n\n")
   f.write("contains three lines\n")
```
This program will create a new file named 'test.txt' if it does not exist. If it does exist, it is overwritten.

We must include the newline characters ourselves to distinguish different lines.


### How to read files in Python?
To read a file in Python, we must open the file in reading mode.

There are various methods available for this purpose. We can use the read(size) method to read in size number of data. If size parameter is not specified, it reads and returns up to the end of the file.


```python
>>> f = open("test.txt",'r',encoding = 'utf-8')
>>> f.read(4)    # read the first 4 data
'This'

>>> f.read(4)    # read the next 4 data
' is '

>>> f.read()     # read in the rest till end of file
'my first file\nThis file\ncontains three lines\n'

>>> f.read()  # further reading returns empty sting
''
```

We can change our current file cursor (position) using the seek() method. Similarly, the tell() method returns our current position (in number of bytes).


```python
>>> f.tell()    # get the current file position
56

>>> f.seek(0)   # bring file cursor to initial position
0

>>> print(f.read())  # read the entire file
This is my first file
This file
contains three lines
```

### We can read a file line-by-line using a for loop. This is both efficient and fast.


```python

>>> for line in f:
...     print line,
...
This is my first file
This file
contains three lines

```

The lines in file itself has a newline character '\n'.

Moreover, the print() end parameter to avoid two newlines when printing.

Alternately, we can use readline() method to read individual lines of a file. This method reads a file till the newline, including the newline character


```python
>>> f.readline()
'This is my first file\n'

>>> f.readline()
'This file\n'

>>> f.readline()
'contains three lines\n'

>>> f.readline()
''
```

Lastly, the readlines() method returns a list of remaining lines of the entire file. All these reading method return empty values when end of file (EOF) is reached.


```python

>>> f.readlines()
['This is my first file\n', 'This file\n', 'contains three lines\n']

```

### Python File Methods
<table border="1">
	<caption>Python File Methods</caption>
	<tbody>
		<tr>
			<th>Method</th>
			<th>Description</th>
		</tr>
		<tr>
			<td>close()</td>
			<td>Close an open file. It has no effect if the file is already closed.</td>
		</tr>
		<tr>
			<td>detach()</td>
			<td>Separate the underlying binary buffer from the <code>TextIOBase</code> and return it.</td>
		</tr>
		<tr>
			<td>fileno()</td>
			<td>Return an integer number (file descriptor) of the file.</td>
		</tr>
		<tr>
			<td>flush()</td>
			<td>Flush the write buffer of the file stream.</td>
		</tr>
		<tr>
			<td>isatty()</td>
			<td>Return <code>True</code> if the file stream is interactive.</td>
		</tr>
		<tr>
			<td>read(<var>n</var>)</td>
			<td>Read atmost <var>n</var> characters form the file. Reads till end of file if it is negative or <code>None</code>.</td>
		</tr>
		<tr>
			<td>readable()</td>
			<td>Returns <code>True</code> if the file stream can be read from.</td>
		</tr>
		<tr>
			<td>readline(<var>n</var>=-1)</td>
			<td>Read and return one line from the file. Reads in at most <var>n</var> bytes if specified.</td>
		</tr>
		<tr>
			<td>readlines(<var>n</var>=-1)</td>
			<td>Read and return a list of lines from the file. Reads in at most <var>n</var> bytes/characters if specified.</td>
		</tr>
		<tr>
			<td>seek(<var>offset</var>,<var>from</var>=<code>SEEK_SET</code>)</td>
			<td>Change the file position to <var>offset</var> bytes, in reference to <var>from</var> (start, current, end).</td>
		</tr>
		<tr>
			<td>seekable()</td>
			<td>Returns <code>True</code> if the file stream supports random access.</td>
		</tr>
		<tr>
			<td>tell()</td>
			<td>Returns the current file location.</td>
		</tr>
		<tr>
			<td>truncate(<var>size</var>=<code>None</code>)</td>
			<td>Resize the file stream to <var>size</var> bytes. If <var>size</var> is not specified, resize to current location.</td>
		</tr>
		<tr>
			<td>writable()</td>
			<td>Returns <code>True</code> if the file stream can be written to.</td>
		</tr>
		<tr>
			<td>write(<var>s</var>)</td>
			<td>Write string <var>s</var> to the file and return the number of characters written.</td>
		</tr>
		<tr>
			<td>writelines(<var>lines</var>)</td>
			<td>Write a list of <var>lines</var> to the file.</td>
		</tr>
	</tbody>
</table>

## Regular Expression
- Special Character
- Regular Expression with Python
- Match vs search
- sub
- Repeat, special character
- compile
- greedy and non-greedy


### Special Character
![_auto_0](attachment:_auto_0)

### Special Character
![_auto_0](attachment:_auto_0)

### Re module
- Compile  
    compile(pattern,flags=0) 
    parse pattern return regular object
- Match  
    match(pattern,string, flags=0)
- Search  
    search(pattern,string, flags=0)
- Findall  
    findall(pattern,string[,flags]) 
    return a match obj list
- Sub 
    sub(pattern, repl, string, max=0)
- Groups  
    groups() 
    return all match elements in a tuple


### match VS search
```python
>>>M = re.match(“foo”, “foo”)
>>>if m is not None:
…        m.group()                           #’foo’
>>> m =re.match(‘foo’, ‘food on the table’)  #match succeed
>>> m.group()                               #’foo’
>>>m = re.search(‘foo’, ‘seafood’).group()
>>>m = re.match(‘foo’, ‘seafood’).group()

```

### Sub  and subn
```python
>>>re.sub('X', 'Mr. Smith', 'attn: X\n\nDear X,\n’)
'attn: Mr. Smith\012\012Dear Mr. Smith,\012’

>>>re.subn('X', 'Mr. Smith', 'attn: X\n\nDear X,\n')
('attn: Mr. Smith\012\012Dear Mr. Smith,\012', 2)

>>>print re.sub('X', 'Mr. Smith', 'attn: X\n\nDear X,\n')
attn: Mr. Smith
Dear Mr. Smith,
>>> re.sub('[ae]', 'X', 'abcdef')
```


### repeat, special character
```python
>>> patt = '\w+@(\w+\.)?\w+\.com'
>>> re.match(patt, 'nobody@xxx.com').group()
'nobody@xxx.com'
>>> re.match(patt, 'nobody@www.xxx.com').group()
‘’nobody@www.xxx.com’

>>> patt = '\w+@(\w+\.)*\w+\.com'
>>> re.match(patt, 'nobody@www.xxx.yyy.zzz.com').group()
'nobody@www.xxx.yyy.zzz.com'
```

### compile
use compile
```python
import re
some_text = 'a, b,,,,c d'
reObj = re.compile('[, ]+')
reObj.split(some_text)
```
not use compile
```python
import re
some_text = 'a,b,,,,c d'
re.split('[, ]+',some_text)
```

### greedy and non-greedy
- Regular expressions are usually used to find matching strings in text.In Python, the quantifiers are greedy (or, in a few languages, non-greedy), always trying to match as many characters as possible;Non-greed, on the other hand, always tries to match as few characters as possible.In the "*", "?","+","{m,n}", plus?To turn greed into non-greed.


```python

import re
s="This is a number 234-235-22-423"
r=re.match(".+(\d+-\d+-\d+-\d+)",s)
print r.group(1)

r = re.match(".+?(\d+-\d+-\d+-\d+)",s)
print r.group(1)

#reObj = re.compile('.+?(\d+-\d+-\d+-\d+)')
#print reObj.match(s).group(1)

```


```python

import re
print re.match(r"aa(\d+)","aa2343ddd").group(1)
print re.match(r"aa(\d+?)","aa2343ddd").group(1)
print re.match(r"aa(\d+)ddd","aa2343ddd").group(1) 
print re.match(r"aa(\d+?)ddd","aa2343ddd").group(1)

```

## class
- Class Definition
- Inheritance
- variable
- Encapsulation
- Polymorphism
- Special  Properties


### Class definition
```python
class Account(object):
  def __init__(self,name,balance):
    self.name = name
    self.balance = balance
  
  def deposit(self,amt):
    self.balance = self.balance + amt
  
  def withdraw(self,amt):
    self.balance = self.balance - amt
a = Account(“Guido", 5000.00)
print a.balance
a.deposit(200)
print a.balance

```

### Inheritance

Inheritance is a way of creating new class for using details of existing class without modifying it. The newly formed class is a derived class (or child class). Similarly, the existing class is a base class (or parent class).


```python
# Use of Inheritance in Python

# parent class
class Bird(object):
    
    def __init__(self):
        print("Bird is ready")

    def whoisThis(self):
        print("Bird")

    def swim(self):
        print("Swim faster")

# child class
class Penguin(Bird):

    def __init__(self):
        # call super() function
        super(Penguin, self).__init__()
        print("Penguin is ready")

    def whoisThis(self):
        print("Penguin")

    def run(self):
        print("Run faster")

peggy = Penguin()
peggy.whoisThis()
peggy.swim()
peggy.run()
```

### Multi-Inheritance


```python
class P1(): 
   def foo(self):           
       print 'p1-foo' 
 
class P2(): 
   def foo(self): 
       print 'p2-foo' 

   def bar(self): 
       print 'p2-bar' 
 
class C1 (P1, P2): 
   pass  
 
class C2 (P1, P2): 
   def bar(self): 
       print 'C2-bar'   
 
class D(C1, C2): 
   pass 

d=D() 
d.foo() # 输出 p1-foo 
d.bar() # 输出 p2-bar 

#实例d调用foo()时，搜索顺序是 D => C1 => P1
#实例d调用bar()时，搜索顺序是 D => C1 => P1 => P2
#换句话说，经典类的搜索方式是按照“从左至右，深度优先”的方式去查找属性。d先查找自身是否有foo方法，没有则查找最近的父类C1里是否有该方法，如果没有则继续向上查找，直到在P1中找到该方法，查找结束
```


```python
class P1(object): 
   def foo(self):           
       print 'p1-foo' 
 
class P2(object): 
   def foo(self): 
       print 'p2-foo' 
   def bar(self): 
       print 'p2-bar' 
 
class C1 (P1,P2): 
   pass  
 
class C2 (P1,P2): 
   def bar(self): 
       print 'C2-bar'   
 
class D(C1,C2): 
   pass 

d=D() 
d.foo() # 输出 p1-foo 
d.bar() # 输出 p2-bar

# 实例d调用foo()时，搜索顺序是 D => C1 => C2 => P1
# 实例d调用bar()时，搜索顺序是 D => C1 => C2
# 可以看出，新式类的搜索方式是采用“广度优先”的方式去查找属性。

```

### variable
- class variable
- instance variable
- local variable
- private variable
- protect variable




```python
class Account(object):
  bank_blance = 0                     # class variable

  def __init__(self, name, balance, age=30):
      self._name = name
      self.__age = age
      self.balance = balance
      Account.bank_blance += self.balance

  def deposit(self,amt):
      self.balance = self.balance + amt
      Account.bank_blance += amt

  def withdraw(self,amt):
      self.balance = self.balance - amt
      Account.bank_blance -= self.balance

  def get_age(self):
      return self.__age

a = Account('Guido', 5000.00)
print "guido's balance:", a.balance
print "bank blance:", Account.bank_blance
a.deposit(200)
print "guido's balance:", a.balance
print 'bank blance:', Account.bank_blance

b = Account('leo', 50.00)
print "leo's balance:", b.balance
print "bank blance:", Account.bank_blance
a.deposit(20)
print "leo's balance:", b.balance
print 'bank blance:', Account.bank_blance
print b._name   # instance can visit protect variable
try:
    print b.__age  # instance can't visit piravte variable
except AttributeError:
    print 'AttributeError'
print 'get age:', b.get_age()

```


```python
class Account(object):
  bank_blance = 0                     # class variable

  def __init__(self, name, balance, age=30):
      self._name = name
      self.__age = age
      self.balance = balance
      Account.bank_blance += self.balance

  def deposit(self,amt):
      self.balance = self.balance + amt
      Account.bank_blance += amt

  def withdraw(self,amt):
      self.balance = self.balance - amt
      Account.bank_blance -= self.balance

  def __set_vip(self):
      print 'account vip'

  def _get_age(self):
      print 'get self.__age:',self.__age
      return self.__age

class ChinaBankAccount(Account):

    def __init__(self, id, name, balance, age):
       super(ChinaBankAccount, self).__init__(name, balance, age)
       self.__id = id

    def get_id(self):
        print 'child can visit parent _name:', self._name
        self._name = "wang"
        print 'after modify:', self._name
        self.__age = '31'
        print 'after modify __age:', self.__age
        try:
            self.__set_vip()   # can't visit parent's __ method
        except AttributeError:
            print 'AttributeError'    
        return self.__id

    #def __set_vip(self):
    #    print 'ChinaBankAccount vip'

china_bank_customer =  ChinaBankAccount(1001, 'leo', 1000, 30)
print china_bank_customer._name
print china_bank_customer.get_id()
print china_bank_customer._get_age()  #not recommend , _ means is not API


```


```python
class A(object):

        def __init__(self, x):
                self.__a = 2
                self.x = x

        def __b(self):
                self.x = 3
        def __c__(self):
            print 'self.x:',self.x

a = A(2)
print a.x
print a.__c__()
```


```python
class A(object): 
    def __method(self): 
        print "I'm a method in A" 
    def method(self): 
        self.__method()
a = A() 
a.method()

class B(A): 
    def __method(self): 
        print "I'm a method in B" 

b = B() 
b.method()
b._B__method()  # never use this!! please!

```

### Encapsulation

Using OOP in Python, we can restrict access to methods and variables. This prevent data from direct modification which is called encapsulation. In Python, we denote private attribute using underscore as prefix i.e single “ _ “ or double “ __“.


```python
class Computer:

    def __init__(self):
        self.__maxprice = 900

    def sell(self):
        print("Selling Price: {}".format(self.__maxprice))

    def setMaxPrice(self, price):
        self.__maxprice = price

c = Computer()
c.sell()

# change the price
c.__maxprice = 1000
c.sell()

# using setter function
c.setMaxPrice(1000)
c.sell()
```

In the above program, we defined a class Computer. We use __init__() method to store the maximum selling price of computer. We tried to modify the price. However, we can’t change it because Python treats the __maxprice as private attributes. To change the value, we used a setter function i.e setMaxPrice() which takes price as parameter.

### Polymorphism

Polymorphism is an ability (in OOP) to use common interface for multiple form (data types).

Suppose, we need to color a shape, there are multiple shape option (rectangle, square, circle). However we could use same method to color any shape. This concept is called Polymorphism.


```python
class Parrot:

    def fly(self):
        print("Parrot can fly")
    
    def swim(self):
        print("Parrot can't swim")

# class Penguin:''[]

    def fly(self):
        print("Penguin can't fly")
    
    def swim(self):
        print("Penguin can swim")

# common interface
def flying_test(bird):
    bird.fly()

#instantiate objects
blu = Parrot()
peggy = Penguin()

# passing the object
flying_test(blu)
flying_test(peggy)
```

In the above program, we defined two classes Parrot and Penguin. Each of them have common method fly() method. However, their functions are different. To allow polymorphism, we created common interface i.e flying_test() function that can take any object. Then, we passed the objects blu and peggy in the flying_test() function, it ran effectively.



### Special  Properties


__name__ 
__doc__ 
__bases__
__dict__
__module__ 
__class__ 
__init__
__new__
__del__
__str__




```python

class TestClass(object):
    """this is test class"""
    def __str__(self):
        return "Test!"
test = TestClass()
print "this is {}".format(test)
print TestClass.__name__
print TestClass.__doc__, TestClass.__name__, TestClass.__bases__
print test.__doc__, test.__class__

```


```python
class TestClass(object):
    """this is test class"""
    def __str__(self):
        return "Test!"

    def output(self):
        print self.__doc__, self.__str__, self.__class__
    
test = TestClass()
test.output()
```

#### what is __new__ 


```python
class Person(object):
    """Silly Person"""
 
    def __new__(cls, name, age):
        print '__new__ called.'
        return super(Person, cls).__new__(cls, name, age)
 
    def __init__(self, name, age):
        print '__init__ called.'
        self.name = name
        self.age = age
 
    def __str__(self):
        return '<Person: %s(%s)>' % (self.name, self.age)
 
if __name__ == '__main__':
    piglei = Person('piglei', 24)
    print piglei
```


```python
class PositiveInteger(int):
    def __init__(self, value):
        super(PositiveInteger, self).__init__(self, abs(value))
 
i = PositiveInteger(-3)
print i
```


```python
class PositiveInteger(int):
    def __new__(cls, value):
        return super(PositiveInteger, cls).__new__(cls, abs(value))
 
i = PositiveInteger(-3)
print i
```

####   \__new\__  usage scenario


```python
class Singleton(object):
    def __new__(cls):
        # 关键在于这，每一次实例化的时候，我们都只会返回这同一个instance对象
        if not hasattr(cls, 'instance'):
            cls.instance = super(Singleton, cls).__new__(cls)
        return cls.instance
 
obj1 = Singleton()
obj2 = Singleton()
 
obj1.attr1 = 'value1'
print obj1.attr1, obj2.attr1
print obj1 is obj2
```

## Reference

* http://www.techbeamers.com/python-operators-tutorial-beginners/
* https://docs.python.org/2/library/inspect.html
* https://www.programiz.com/python-programming/
* http://python.jobbole.com/86506/
* https://www.cnblogs.com/nomorewzx/p/4203829.html
* https://blog.csdn.net/drdairen/article/details/51134816
* https://www.cnblogs.com/yizhenfeng168/p/6985020.html




-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>









