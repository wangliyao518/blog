---
layout: post
title: "simple ATDD and TDD example"
description: A calculator robot keyword add, subtract, multiply and divide difficult? This article is how how to use ATDD and TDD to finishi this task.
image: 'http://res.cloudinary.com/dm7h7e8xj/image/upload/v1504810464/hello-world-vue_ibatoy.jpg'
category: 'tutorial'
tags:
- ATDD
- TDD
- robot
- python
twitter_text: use ATDD and TDD to write robot keyword.
introduction: Write a robot keyword have add, subtract, multiply and divide is entry-level programming, is also suitable for used this as a ATDD and TDD demonstration, perhaps more simpler more easier to understand, but the task is really so simple? May we take things too simple, we are programmers, we should be more professional
---


## what's ATDD

- First, ATDD is not a test methodology, but a development methodology
首先，ATDD不是一种测试方法论，而是一种开发方法论。

- The people involved in UTDD are just developers, so does ATDD involve testers only?No, products, development, and testing all need to be involved in ATDD
UTDD涉及的人员仅仅是开发人员，那么ATDD仅仅涉及测试人员吗？不是，产品、开发、测试都需要参与到ATDD中来。

- Team need to demand in the ATDD activities define the desired quality standards and acceptance conditions, in order to make clear and agreed acceptance test plan (including a series of test scenarios) to drive the product development and test script code.在
ATDD活动中团队需要就需求定义出期望的质量标准和验收细则，以明确而且达成共识的验收测试计划（包含一系列测试场景）来驱动产品的代码开发和测试脚本开发。

- ATDD must be based on test automation and continuous integration.ATDD一定是基于测试自动化和持续集成的。

![ATDD CYCLE](https://raw.githubusercontent.com/wangliyao518/blog/gh-pages/assets/img/ATDD_CYCLEpng.png)

just like TDD 'red-green-refactor', ATDD also have similar process(see above). 和TDD的“红-绿-重构”类似，ATDD的流程也是类似的思路（如上图）。
- discuss and clarify stage 讨论澄清阶段
    全组参与的针对需求和方案的讨论
    大家产出对需求和方案共同的理解
    通过明确验收测试方式澄清我们的实现方案
    验收测试方式将被自动化
- develop stage 开发阶段
    用明确具体的验收测试方式来指导开发工作
    验收测试的自动化和特性的开发可以并行开展
    全组成员对验收测试的自动化负责，而不仅仅是测试人员
    最终，我们的产品实现能让所有的自动化测试通过
- deliver stage 交付阶段
    我们要保证之前迭代所有的自动化验收测试能在新交付上通过
    给所有利益相关者演示我们的新特性
    收集反馈，讨论改进


## ATDD benefit
- Generally speaking, we believe that the benefits of ATDD are.一般来说，我们认为ATDD的好处有：

    1. A unified understanding of business needs. 大家对业务需求的统一理解
    2. Describe requirements in natural language. 通过自然语言来描述需求
    3. it Is a requirement or instance that can be run. 是可以运行的需求或实例
    4. It's a living document. 是活着的文档



## first write robot case
The easier it is, the easier it is to say, let's start with the simplest example of adding and subtracting the calculator.Don't think it's too easy, just sit back, and you'll find out what's going on with us. You can't even write such a small program, so you have a lot of bugs in your hands?
**越简单越能说明问题, 我们从最简单的加减乘除计算器例子开始, 不要以为它太简单, 耐着性子往后看, 你会发现我们是怎么回事, 连这么小的程序都写不好, 亲手产生了好多的bug**


The user's requirement is to write a calculator keyword with addition and subtraction and multiplication.
用户的需求就是写一个加减乘除的计算器keyword

ok, let's start create robot case first, the robot case should like below:


```robot
*** Settings ***
Library     user_calculator


*** Test Cases ***
Test calculator addition example
    ${result}    operate_fun    ${1}    ${2}    +
    should be equal    ${result}    ${3}

Test calculator subtraction example
    ${result}    operate_fun    ${3}    ${2}    -
    should be equal    ${result}    ${1}

Test calculator multiply example
    ${result}    operate_fun    ${1}    ${2}    *
    should be equal    ${result}    ${2}

Test calculator division example
    ${result}    operate_fun    ${4}    ${2}    /
    should be equal    ${result}    ${2}

```

this robot case should be writen by entity tester but should be reach an agreement with the developer, then the developer can begin to coding, the developer also should use TDD method, so they should write the UT case first, may be like below:

```python
import unittest
from user_calculator.interface import operate_fun


class TestCalculator(unittest.TestCase):

    def test_operate_fun_add(self):
        result = operate_fun(1, 2, '+')
        self.assertEqual(result, 3)

    def test_operate_fun_sub(self):
        result = operate_fun(3, 2, '-')
        self.assertEqual(result, 1)

    def test_operate_fun_multiply(self):
        result = operate_fun(3, 2, '*')
        self.assertEqual(result, 6)

    def test_operate_fun_div(self):
        result = operate_fun(6, 2, '/')
        self.assertEqual(result, 3)

if __name__ == "__main__":
    unittest.main()

```

It's too easy, then we write source code like below:
```python
def operate_fun(a, b, oper):
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
Everything looks very simple, UT pass, robot case can pass. 一切看上去都非常的简单, UT pass了, robot case也可以pass了

But often the bug is often reveal out between our negligence, actually this is not simple, only we put it to anything to do, also will be more beautiful, otherwise may be terrible. 但往往"大意失荆州", bug往往也是在我们疏忽之间流露出去的, 其实这个真不简单, 任何事情只有我们把它用心来做了,也才会更加的美丽,不然可能糟糕透了

The above case looks like UT is covered enough, and the robot case function coverage seems to be also available. Do they all pass the pass to make sure there are no bugs?Not too!In fact, the above code has leaked a lot of bugs in our eyes, so let me add a few cases to you.
上面的case看上去UT 覆盖够了, robot case功能覆盖好像也有了, 他们都pass了就真的保证了没有bug? 非也! 实则上面的代码在我们"众目睽睽" 之下流出了很多bug, 让我随便给你增加几个case看看

```robot
Test calculator addition example 1
    ${result}    operate_fun    1    2    +
    should be equal    ${result}    3

Test calculator addition example 2
    ${result}    operate_fun    1    2    +
    should be equal    ${result}    ${3}  


Test calculator addition example 3
    ${result}    operate_fun    ${5}    ${2}    /
    should be equal    ${result}    ${2.5}  

```

Try my new test case, how about the result? Are we too careless? In fact, I can write a lot of test cases, and I can test a lot of bugs. I don't want to continue to elaborate in this blog, anyone interesting can try to add more case to find the more bugs
试试我run新增加的测试用例, 结果怎么样? 怎么样?　我们是不是太过大意呢？ 其实还可以写很多测试用例出来, 还可以测试出很多的bug, 我不想在这个bug中继续阐述, 有兴趣的同学可以自行脑补

With bugs, we have ATDD and TDD without fear of modifying the code, which is the benefit of ATDD and TDD, and for bugs, we add test cases.
出现了bug, 我们有ATDD 和TDD 就不用担心害怕修改代码, 这就是ATDD和TDD的好处, 针对bug, 我们增补测试用例

上面的robot case已经增加了, 我们这里好像也可以不用增加python部分的UT代码,它好似已经覆盖了. 勤快点的同学可以增加下UT代码, 如下:

```python
    def test_operate_fun_add_2(self):
        result = operate_fun('1', '2', '+')
        self.assertEqual(result, 3)

    def test_operate_fun_div_2(self):
        result = operate_fun(5, 2, '/')
        self.assertEqual(result, 2.5)
```

接着轮到修改源码了, 经验丰富的程序员一下发现了, 我们只需要把传入进来的类型全部float转换下就可以了, 如果经验不够丰富可能直接就用int转换了, int转换要是没有测试帮助写刚才那个5/2=2.5的测试用例, 明显一个bug又流露出去了 
所以修改后的源码如下:
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

Is it okay to bug later?Naturally or not, I add another test case. 这样之后bug 是不是就好啦? 自然还是非也, 我再增加一个测试用例
```robot
Test calculator addition example 3
    ${result}    operate_fun    '1'    '2'    +
    should be equal    ${result}    '12'
```

You will find that the problem is again, the user's usage scenario is a normal scene, we have no reason to oppose him, all right!With ATDD and TDD, we can continue to add UT and modify the source code, so we can continue to play with the above method. I will not continue to write for the time being.
你会发现, 问题又出现了, 用户的这个使用场景是一个正常的场景, 我们没理由反对他, 好吧! 有了ATDD和TDD, 我们可以继续增加UT 和修改源码, 我们就可以继续按刚才上面方式玩下去. 我暂时不继续写下去.

TDD and ATDD actually also one of the great benefits when we refactor our code with quality assurance, this is a safety belt, we source for procedural too much, we should think of some way to get it object oriented, or to add an operation such as a new type need to change the main code
其实TDD 和ATDD的一大好处还有当我们重构我们的代码时 有了质量上的保证, 这就是一个保险带, 我们上面的源码太面向过程化了, 我们应该想办法让它面向对象, 不然比如新增加一种运算类型时都需要去改主题

With this ATDD, we can refactor this source code and let's it's more clean code, and I'm going to introduce it in another article.
有了这个ATDD ,如何把这个源码写得更clean code, 我准备在另外一篇文章中介绍

-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>
