---
layout: post
title: "python clean code - open close principle"
date: 2018-02-04 15:00:40
description: Clean code is well-designed, well-written software.this article only show a simple open close principle example
image: 'https://raw.githubusercontent.com/wangliyao518/blog/gh-pages/assets/img/timg%20(3).jpg'
category: 'tutorial'
tags:
- clean code
- blog
- tutorial
twitter_text: how to write clean python code.
introduction: Welcome to CleanCode -- a website for developers who want to write good code.
---

Clean code is well-designed, well-written software. Clean code communicates well to the external customer and the internal customer; that is, to users who wish to accomplish a task with it, and to developers who wish to develop, maintain, revise, enhance or just plain understand it. This site is here to convey experiences learned--to empower you to help others learn--and to provide a plethora of free libraries in several languages. [clean code website](http://cleancode.sourceforge.net/)



## A Sneak View Of The Before Calculator Code
为了浅显易懂, 我还是以之前的计算机代码做为例子, 我们先来看看之前的代码

```python
def operate_fun(a, b, oper):
    a = float(a)
    b = float(b)
    if oper == '+':
        return a + b
    elif oper == '-':
        return a - b
    elif oper == '*':
        return a * b
    elif oper == '/':
        return a / b
    else:
        raise Exception("operation not supported!")
```
上面的代码匆匆一瞥也没什么不妥, 但当我们增加任何的需求时,都在一个函数里面改动, 就意味着需要测试+-*/所有的分支.比如说我们需要增加求幂的需求, 我们的代码会变成如下:

```python
def operate_fun(a, b, oper):
    a = float(a)
    b = float(b)
    if oper == '+':
        return a + b
    elif oper == '-':
        return a - b
    elif oper == '*':
        return a * b
    elif oper == '/':
        return a / b
    elif oper == '**'
        return a**b
    else:
        raise Exception("operation not supported!")
```

当用户比如要求除法小数点后取2位有效位时, 我们又会在elif中的 a/b 中 做文章, 如果是要求+-/* 都增加取有效位时, 明显我们需要更改所有的if 或者elif分支(而实则这里有共性) 


## open close
我们把上面的方法用面向对象的方法重写一些, 每种算法一个类, 由于他们都是算法类, 所以可以提取一个base的公共基类, 如果有求幂或者求根等新的算法要求, 我们只需要重新写写一个类即可, 所以扩展是开放的, 而在组装的接口处, 我们明显去掉了if -else逻辑, 只用到了字典的隐射, 在代码中, 我们要新增加一种算法, 只需要在字典中增加元素即可, 这个地方我们又是封闭的, 避免新需求导致这个地方引入if -else逻辑, 也就是新的算法引进时我们不需要测试之前的所有功能, 而且我们只需要保证新增加的类是正常可工作的,加入我们已测试过的"调度"模块它就能正常工作

```python
class base(object):

   def __init__(self, a, b, oper):
       self.a = float(a)
       self.b = float(b)
       self.oper = oper

   def operate(self):
       pass

class add(base):

    def operate(self):
        return self.a + self.b


class sub(base):

    def operate(self):
        return self.a - self.b

class mult(base):

    def operate(self):
        return self.a * self.b

class div(base):

    def operate(self):
        ret = self.a / self.b
        ret = '%0.2f'%ret
        return float(ret)

class square(base):

    def operate(self):
        return self.a ** self.b

def operate_fun(a, b, oper):
    operation_dict = {"+":add, "-":sub, "*":mult, "/":div}
    operation_dict['**'] = square
    return  operation_dict[oper](a, b, oper).operate()
```

如果我们是要增加一个common的需求, 比如小数点后取2位,这个需要对所有的算法都生效, 之前的代码, 只能去改所有的分支里面的代码, 但我们现在的代码, 明显可以只在一处改动, 所有的都会生效.代码改动如下:
```python
def operate_fun(a, b, oper):
    operation_dict = {"+":add, "-":sub, "*":mult, "/":div}
    operation_dict['**'] = square
    return round(float(eval("{}{}{}".format(float(a), oper, float(b)))), 2)
```

-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>
