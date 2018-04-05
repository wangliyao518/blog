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
上面的代码匆匆一瞥也没什么不妥, 但当我们增加任何的需求时,都在一个函数里面改动, 就意味着需要测试+-*/所有的分支.




-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>
