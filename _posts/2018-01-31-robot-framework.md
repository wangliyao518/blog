---
layout: post
title: "robot framwork introduction"
date: 2018-01-30 22:26:40
image: 'https://raw.githubusercontent.com/wangliyao518/web/gh-pages/assets/img/timg.jpg'
description: Robot Framework is a generic test automation framework for acceptance testing and acceptance test-driven development (ATDD). It has easy-to-use tabular test data syntax and it utilizes the keyword-driven testing approach.
category: 'trainning'
tags:
- trainning
- tips
twitter_text: Robot Framework itself is open source software released under Apache License 2.0,nowadays sponsored by Robot Framework Foundation.
introduction: Robot Framework is a generic test automation framework for acceptance testing and acceptance test-driven development (ATDD)
---

Robot Framework is a generic test automation framework for acceptance testing and acceptance test-driven development (ATDD). It has easy-to-use tabular test data syntax and it utilizes the keyword-driven testing approach.Its testing capabilities can be extended by test libraries implemented either with Python or Java, and users can create new higher-level keywords from existing ones using the same syntax that is used for creating test cases.detail introduction you can refer[robot official website](http://robotframework.org/)


Intuitively when we take a persion we will describe head, neck, the upper part of the body, hand, the lower part of the body, leg, the robot is the same, it have head(settings), neck(variables), hand(suite setup and test setup), the upper part the the body(test cases), the lower part of the boday(keywords), leg(suite teardown and test teardown)。

当我们谈论一个人时，我们会直观的用头，脖子，上半身，手，下半身，脚来描绘他。robot类似，它也有头（就是settings部分），脖子（variables部分），手（suite setup和test setup），上半身（test cases部分），下半身（keywords部分），腿（suite teardown 和test teardown）


正如前文所说， it has easy-to-use tabular test data syntax，所以我们可以按照表格式方式来书写robot case， 自然我们就可以把robot case方便的保存为excel格式，html格式，txt格式， robot格式（其实robot格式和txt格式都是文本格式，我们推荐使用后缀为.robot格式） 

from tabular syntax view，robot structure like below：

## robot case structure
<table>
  <thead>
    <tr>
      <th>Table Name</th>
      <th>Used for</th>
      <th>Aliases</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Keywords Table</td>
      <td>creating user keyword from existing lower-level keywords</td>
      <td>keyword, keywords, userkeyword, userkeywords</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Settings Table</td>
      <td>import test libraries, resource files and variable files, defining metadata for test suite and test case</td>
      <td>setting, settings, metadata</td>
    </tr>
    <tr>
      <td>Variable Table</td>
      <td>defining variables that can use anywhere in test datas</td>
      <td>variable, variables</td>
    </tr>
    <tr>
      <td>Test Case Table</td>
      <td>creating test case from avaliable keywords</td>
      <td>Test Case, Test Cases</td>
    </tr>
  </tbody>
</table>

## robot case structure -- settings
<table>
  <thead>
    <tr>
      <th>Settings</th>
      <th> </th>
      <th> </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Documentaion</td>
      <td> </td>
      <td> </td>
    </tr>
    <tr>
      <td>Suite setup</td>
      <td>log</td>
      <td>this is suite setup step</td>
    </tr>
    <tr>
      <td>Suite teardown</td>
      <td>log</td>
      <td>this is suite teardown</td>
    </tr>
     <tr>
      <td>test setup</td>
      <td>log</td>
      <td>this is test setup</td>
    </tr>
     <tr>
      <td>test teardown</td>
      <td>log</td>
      <td>this is test teardown</td>
    </tr>
     <tr>
      <td>Force Tags</td>
      <td>LTE</td>
      <td>FSMR3</td>
    </tr>
     <tr>
      <td>Resource</td>
      <td>interface.robot</td>
      <td>#import robot library</td>
    </tr>
     <tr>
      <td>Library</td>
      <td>ta_files</td>
      <td>#import python library</td>
    </tr>
  </tbody>
</table>


A whole robot case like below: 

## robot case example

```robot
***settings***

Library    Process  #just for example

suite setup

suite teardown

test setup

test teardown


***variables***

${GLOBAL_VAR_1}    this is global variable example 


***test cases***


This is first example case

    user_own_example_keyword_1


This is seconde example case

    user_own_example_keyword_2


***keywords***


user_own_example_keyword_1


    log    'this is my example keyword 1'


user_own_example_keyword_2

    log    'this is my example keyword 2'

```

some people often tell me that they need ride or other tools to write robot case, otherwise they don't know how to write robot case, from the above example case, we can see that the robot case is just a text file, very easy to write, you can use vim, notepad and any others text editor. aannouncements need stick such as library some libraries, define the test case and keywords, you should at lease keep 2 blank between keyword and arguments, we recommend 4 blank(like python, robot also a language, write robot case is also programming)

经常有人告诉我他们一定要ride或者其它一些智能编写工具来编写robot case， 没有这些工具，他们好像就不知道怎么编写robot case了， 从上面的example case来看， robot case其实很简单，它就是一个文本文件， 你可以用vim，notepad或者任意的文本工具来编写， robot case的声明需要置顶，如library某个库，定义全局变量，定义robot case和定义keyword，这些都是置顶书写，在keyword和参数间，你至少应该保持2个空格以上，我们推荐一直使用4个空格（和python保持一直，良好的编程习惯，robot本身也是语言，开发robot case也是编程行为）。





HTML defines a long list of available inline tags, a complete list of which can be found on the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

- **To bold text**, use `<strong>`.
- *To italicize text*, use `<em>`.
- Abbreviations, like <abbr title="HyperText Markup Langage">HTML</abbr> should use `<abbr>`, with an optional `title` attribute for the full phrase.
- Citations, like <cite>&mdash; Thiago Rossener</cite>, should use `<cite>`.
- <del>Deleted</del> text should use `<del>` and <ins>inserted</ins> text should use `<ins>`.
- Superscript <sup>text</sup> uses `<sup>` and subscript <sub>text</sub> uses `<sub>`.

Most of these elements are styled by browsers with few modifications on our part.

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

Vivamus sagittis lacus vel augue rutrum faucibus dolor auctor. Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.

## Code

Cum sociis natoque penatibus et magnis dis `code element` montes, nascetur ridiculus mus.

```js
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
```

Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa.

## Lists

Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.

* Praesent commodo cursus magna, vel scelerisque nisl consectetur et.
* Donec id elit non mi porta gravida at eget metus.
* Nulla vitae elit libero, a pharetra augue.

Donec ullamcorper nulla non metus auctor fringilla. Nulla vitae elit libero, a pharetra augue.

1. Vestibulum id ligula porta felis euismod semper.
2. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
3. Maecenas sed diam eget risus varius blandit sit amet non magna.

Cras mattis consectetur purus sit amet fermentum. Sed posuere consectetur est at lobortis.

Integer posuere erat a ante venenatis dapibus posuere velit aliquet. Morbi leo risus, porta ac consectetur ac, vestibulum at eros. Nullam quis risus eget urna mollis ornare vel eu leo.

## Images

Quisque consequat sapien eget quam rhoncus, sit amet laoreet diam tempus. Aliquam aliquam metus erat, a pulvinar turpis suscipit at.

![placeholder](https://placehold.it/800x400 "Large example image")
![placeholder](https://placehold.it/400x200 "Medium example image")
![placeholder](https://placehold.it/200x200 "Small example image")

## Tables

Aenean lacinia bibendum nulla sed consectetur. Lorem ipsum dolor sit amet, consectetur adipiscing elit.



Nullam id dolor id nibh ultricies vehicula ut id elit. Sed posuere consectetur est at lobortis. Nullam quis risus eget urna mollis ornare vel eu leo.

-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>









