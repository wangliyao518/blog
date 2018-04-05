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


和TDD的“红-绿-重构”类似，ATDD的流程也是类似的思路（如上图）。
- 讨论澄清阶段
    全组参与的针对需求和方案的讨论
    大家产出对需求和方案共同的理解
    通过明确验收测试方式澄清我们的实现方案
    验收测试方式将被自动化
- 开发阶段
    用明确具体的验收测试方式来指导开发工作
    验收测试的自动化和特性的开发可以并行开展
    全组成员对验收测试的自动化负责，而不仅仅是测试人员
    最终，我们的产品实现能让所有的自动化测试通过
- 交付阶段
    我们要保证之前迭代所有的自动化验收测试能在新交付上通过
    给所有利益相关者演示我们的新特性
    收集反馈，讨论改进


## ATDD benefit
- 一般来说，我们认为ATDD的好处有：

    1. 大家对业务需求的统一理解
    2. 通过自然语言来描述需求
    3. 是可以运行的需求或实例
    4. 是活着的文档



## first write robot case


```js
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
```



## Images

Quisque consequat sapien eget quam rhoncus, sit amet laoreet diam tempus. Aliquam aliquam metus erat, a pulvinar turpis suscipit at.

![placeholder](https://placehold.it/800x400 "Large example image")
![placeholder](https://placehold.it/400x200 "Medium example image")
![placeholder](https://placehold.it/200x200 "Small example image")



-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>
