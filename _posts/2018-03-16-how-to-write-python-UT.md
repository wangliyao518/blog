---
layout: post
title: "how to write python UT"
description: do you know UT? do you know how to write a good UT?
image: 'https://raw.githubusercontent.com/wangliyao518/blog/gh-pages/assets/img/unittest.jpg'
category: 'python'
tags:
- python
- UT
- unittest
twitter_text: python UT test
introduction: do you know UT? do you know how to write a good UT?
---

## definition
Unit testing refers to the inspection and verification of the smallest testable unit in the software.For unit test in unit of meaning, in general, according to the actual situation to determine the specific meaning, such as unit refers to a function in C language, Java unit refers to a class, graphical software can refer to a window or a menu.In general, the unit is the smallest measured function module.I think unite you can refers to a function in python language.
单元测试，是指对软件中的最小可测试单元进行检查和验证。对于单元测试中单元的含义，一般来说，要根据实际情况去判定其具体含义，如C语言中单元指一个函数，Java里单元指一个类，图形化的软件中可以指一个窗口或一个菜单等。总的来说，单元就是人为规定的最小的被测功能模块, python中单元我认为也可以是一个函数

It is generally believed that in the era of structured programs, unit tests refer to functions as functions. In today's object-oriented era, unit tests refer to the units referred to as classes.In my practice, such as test units, high complexity, operability is poor, so still claims to function as a unit test test units, but can use a test class to organize all the test function of a class.Unit tests should not overemphasize object-oriented, because local code is still structured.Unit test workload is big, simple and practical efficiency is the hard truth.
一般认为，在结构化程序时代，单元测试所说的单元是指函数，在当今的面向对象时代，单元测试所说的单元是指类。以我的实践来看，以类作为测试单位，复杂度高，可操作性较差，因此仍然主张以函数作为单元测试的测试单位，但可以用一个测试类来组织某个类的所有测试函数。单元测试不应过分强调面向对象，因为局部代码依然是结构化的。单元测试的工作量较大，简单实用高效才是硬道理。



## simple

既然单元测试是针对函数,针对源码,那首先需要有源码, 那先让我们那些段ssh登录 host做操作的代码
Since the unit test is for the function, for the source code, you need to have the source code first, then let us SSH into the host to do the operation of the code.

```python
import re


class FsmAccess(object):

    def __init__(self, connection):
        self.con = connection

    def get_lmp_ip_address(self):
        result = ""
        stderr, stdout = self.con.exec_command("ifconfig eth3")
        pattern = r"(\d{1,4}.\d{1,4}.\d{1,4}.\d{1,4})"
        for line in stdout.split('\n'):
            ret = re.search(pattern, line)
            if ret:
                result = ret.groups()[0]
        return result

```
In view of the above get_lmp_ip_address function to write unit tests, we see it relies on an external component connection, and when the connection in the unit test should not be true, so we should replace it, we just rely on the connection exec_command function of the output results of the object, and then outputs a want to have our own operation results, our unit tests for the purpose of the get_lmp_ip_address also just in order to validate our the correct output value for the 'ifconfig' command parsing
针对上面get_lmp_ip_address函数写单元测试, 我们看到它依赖一个外部组件 connection, 而这个connection在单元测试时就不应该真实的执行, 所以我们应该把它替换掉, 我们只是依赖connection这个对象中的exec_command函数输出的结果,然后有我们自己的运算输出一个想要的结果, 我们的单元测试这个get_lmp_ip_address的目的也只是为了验证我们对这个'ifconfig' 命令输出值的正确解析

With the above understanding, we know that we need to replace exec_command, and we can make a fake object by ourselves without relying on the third-party module. The code is as follows.
有了上面的理解,我们知道了需要替换掉exec_command, 不依赖第三方模块情况下,我们可以自己造一个假的这个对象,代码如下

```python
import unittest
from fsm import FsmAccess

class MockConnection(object):

    def exec_command(self, command):
        return  0, 'eth3      Link encap:Ethernet  HWaddr 00:0F:BB:BA:99:CD  \ninet addr:10.0.2.2  Bcast:10.0.2.255  Mask:255.255.255.0\nUP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1\nRX packets:0 errors:0 dropped:0 overruns:0 frame:0\nTX packets:16 errors:0 dropped:0 overruns:0 carrier:0\ncollisions:0 txqueuelen:1000\nRX bytes:0 (0.0 B)  TX bytes:1152 (1.1 KiB)'

class TestKissConfigInterface(unittest.TestCase):

    def test_get_lmp_ip_add(self):
        mock_instant = MockConnection()
        fsm_instance = FsmAccess(connection=mock_instant)
        ret = fsm_instance.get_lmp_ip_address()
        self.assertEqual(ret, '10.0.2.2')

if __name__ == "__main__":
    unittest.main()
```
    
## mock
The UT can help us to test our function, but there is a problem is if we want to test a lot of functions and many are like get_lmp_ip_address there is external dependencies, we will need to write so many false classes and methods, so efficiency is very low, so there will be some tools or module, which is the mock and patch
上面的UT 完全可以帮我们测试我们的函数功能, 但有一个问题是如果我们要测试很多的函数而且很多函数也都和get_lmp_ip_address一样有外部依赖我们就需要写很多这样假的类和方法, 这样效率明显很低下, 于是就有一些工具或者模块的出现, 这就是mock和patch

```python
import unittest
from fsm import FsmAccess
from mock import Mock


class TestKissConfigInterface(unittest.TestCase):

    def test_get_lmp_ip_add(self):
        con_mock = Mock()
        con_mock.exec_command.return_value = 0, 'eth3      Link encap:Ethernet  HWaddr 00:0F:BB:BA:99:CD  \ninet addr:10.0.2.2  Bcast:10.0.2.255  Mask:255.255.255.0\nUP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1\nRX packets:0 errors:0 dropped:0 overruns:0 frame:0\nTX packets:16 errors:0 dropped:0 overruns:0 carrier:0\ncollisions:0 txqueuelen:1000\nRX bytes:0 (0.0 B)  TX bytes:1152 (1.1 KiB)'
        fsm_instance = FsmAccess(connection=con_mock)
        ret = fsm_instance.get_lmp_ip_address()
        self.assertEqual(ret, '10.0.2.2')

if __name__ == "__main__":
    unittest.main()
```

New test code above than it does not need to define a new class, only need to use a mock instantiating an object, then the mock object can be directly write our expectation function names and return values
上面新的测试代码比起上面不需要自己定义一个新类, 只需要用一个mock实例化一个对象,然后这个mock对象中就可直接写上我们的期望的函数名字和返回值

We also can use mock as below way
mock的方法还可以这样用

```python
import unittest
from fsm import FsmAccess
from mock import Mock


class TestKissConfigInterface(unittest.TestCase):

    def test_get_lmp_ip_add(self):
        fake_return_value = 0, 'eth3      Link encap:Ethernet  HWaddr 00:0F:BB:BA:99:CD  \ninet addr:10.0.2.2  Bcast:10.0.2.255  Mask:255.255.255.0\nUP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1\nRX packets:0 errors:0 dropped:0 overruns:0 frame:0\nTX packets:16 errors:0 dropped:0 overruns:0 carrier:0\ncollisions:0 txqueuelen:1000\nRX bytes:0 (0.0 B)  TX bytes:1152 (1.1 KiB)'
        fsm_instance = FsmAccess(connection=Mock())
        fsm_instance.con.exec_command = Mock(return_value=fake_return_value)
        ret = fsm_instance.get_lmp_ip_address()
        self.assertEqual(ret, '10.0.2.2')

if __name__ == "__main__":
    unittest.main()
```


## patch

we also can use patch to write UT case like below:

```python
import re


class FsmAccess(object):

    def __init__(self, connection):
        self._con = connection

    def con(self):
	    return self._con

    def get_lmp_ip_address(self):
        result = ""
        stderr, stdout = self.con.exec_command("ifconfig eth3")
        pattern = r"(\d{1,4}.\d{1,4}.\d{1,4}.\d{1,4})"
        for line in stdout.split('\n'):
            ret = re.search(pattern, line)
            if ret:
                result = ret.groups()[0]
        return result


import unittest
from fsm import FsmAccess
from mock import Mock, patch


class TestKissConfigInterface(unittest.TestCase):


    @patch('fsm.FsmAccess.con')
    def test_get_lmp_ip_add_patch(self, con_mock):
        con_mock.exec_command.return_value = (0, 'eth3      Link encap:Ethernet  HWaddr 00:0F:BB:BA:99:CD  \ninet addr:10.0.2.2  Bcast:10.0.2.255  Mask:255.255.255.0\nUP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1\nRX packets:0 errors:0 dropped:0 overruns:0 frame:0\nTX packets:16 errors:0 dropped:0 overruns:0 carrier:0\ncollisions:0 txqueuelen:1000\nRX bytes:0 (0.0 B)  TX bytes:1152 (1.1 KiB)')
        fsm_instance = FsmAccess(con_mock)
        ret = fsm_instance.get_lmp_ip_address()
        self.assertEqual(ret, '10.0.2.2')

if __name__ == "__main__":
    unittest.main()
```

- The majority of patch usage scenarios.
some people may like source code like below:

```
import paramiko
class FsmAccess(object):

    def __init__(self):
        pass

    def connect(self, host, port, username, password):
        self.con = paramiko.SSHClient()
        self.con.set_missing_host_key_policy(paramiko.AutoAddPolicy())
        self.con.connect(host, port, username, password)

    def get_lmp_ip_address(self):
        result = ""
        stderr, stdout = self.con.exec_command("ifconfig eth3")
        pattern = r"(\d{1,4}.\d{1,4}.\d{1,4}.\d{1,4})"
        for line in stdout.split('\n'):
            ret = re.search(pattern, line)
            if ret:
                result = ret.groups()[0]
        return result

    def disconnect(self):
        self.con.close()

```

I don't want to say whether this code write good enough, I just want talk how to use patch and to test connect function, I write the UT case like below:
我不想来评断上面代码是否写的够好, 我只是来谈谈这么使用patch, 以及如何来测试这个connect函数(get_lmp_ip_address已经讲过, 下面就比再写了)
```python

import unittest
from mock import Mock, patch


class TestFsm(unittest.TestCase):


    @patch('paramiko.SSHClient.set_missing_host_key_policy')
    @patch('paramiko.SSHClient.connect')
    def test_connect(self, con_mock, set_missing_host_key_policy_mock):
        fsm_instance = FsmAccess()
        fsm_instance.connect('127.0.0.1', 22, 'ute', 'ute')
        fsm_instance.con.set_missing_host_key_policy.assert_called()
        fsm_instance.con.connect.assert_called_with('127.0.0.1', 22, 'ute', 'ute')


if __name__ == "__main__":
    unittest.main()

```
Connect function in the absence of any of the above logic encapsulation, so UT code meaning is not very big, actually we do on the other hand is for the sake of coverage, but on the other hand are in order to guarantee the function call part of the key move not easily, the patch function is simple, the inside of the patch parameters is the statement we need to replace the function of "path", it will be in the corresponding def replaced by parameter represents the object in the test function, we didn't do this case parameters of any assignment or statement, so it is none
上面的connect函数由于没有任何的逻辑封装,所以UT代码其实意义不是很大, 我们确实一方面是为了覆盖率, 其实另外一方面也是为了保证这个函数关键的调用部分不被别人轻易移调, patch函数也很简单, patch里面的参数就是声明我们需要替代掉的函数'路径', 它会被对应def中测试函数中参数代表的对象所替换, 我们这个例子中参数没做任何的赋值或者声明, 所以它就是none


-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>
