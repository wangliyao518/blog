---
layout: post
title: "python intermediate training"
date: 2017-07-29 13:24:49
image: 'http://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_760/v1502208952/contact-post_gnaojy.png'
description: Lorem ipsum dolor sit amet, consectetur adipisicing elit.
category: 'python'
tags:
- python
- training
- blog
twitter_text: python intermediate training
introduction: python training include Decorator, how to write UT, Parallel Handling, web program
---


# Python Intermediate

![python](https://upload.wikimedia.org/wikipedia/commons/c/c3/Python-logo-notext.svg)
### <center>--by wang liyao (leo)<center> ###

## agenda  ##

- Functional programming
- Decorator
- Unit Testing
- Introspection
- Parallel Handling
- Web Development
- Reference
- Q&A






## Functional programming

![lambda](/files/images/lambda.png)

>it’s almost certainly ture that functional programming is the next big thing

--- Uncle Bob Martin


```python
# use function as parameter
def get_visit_ips(file_path, callback):
    with open(file_pth) as fp:
        return [callback(line) for line in fp]
```


```python
# return function
def cache(func):
    cached = {}
    def _func(attr, *args, **kwargs):
        if attr not in cached:
            cached[attr] = func(attr, *args, **kwargs)
        return cached[attr]
    
    return _func
        
```


```python
# lambda
lambda : True
```


```python
lambda x: x ** 2
```


```python
lambda x, y: x + y
```


```python
# map
map(lambda x: x ** 2, range(10))
```


```python
# reduce
reduce(lambda x, y: x + y, range(10))
```


```python
# filter
filter(lambda x: x % 2 == 0, range(10))
```

### Decorator

![Telecom Tree](/files/images/telecomtree.jpg)


```python
class MyDict(dict):
    @property
    def max(self):
        return max(self.values())

MyDict(a=1, b=2, c=3).max
```


```python
# cache wrapper
def cache(func):
    cached = {}
    def _f(*args):
        if args not in cached:
            result = func(*args)
            cached[args] = result
        else:
            print 'cache hint!'
        return cached[args]
    return _f

@cache
def sum_(*args):
    return sum(args)

print sum_(1,2,3)  ####cache(sum)()
print sum_(3,2,1)
```

    6
    6
    

### One more step


```python
# cache wrapper for function
import time

def cache(timeout):
    def _wrapped(func):
        cached_start = {}
        cached = {}
        def _f(*args):
            if args not in cached or ((time.time() - cached_start[args]) > timeout):
                result = func(*args)
                cached[args] = result
                cached_start[args] = time.time()
            else:
                print 'cache hint!'
            return cached[args]
        return _f
    return _wrapped

@cache(2)
def sum_(*nums):
    return sum(nums)

print sum_(1,2,3)
print sum_(1,2,3)
from time import sleep
sleep(2)
print sum_(1,2,3)
```

    6
    cache hint!
    6
    cache hint!
    6
    

### functools

>Tools for working with functions and callable objects


```python
# functools.partial
import functools

def echo(name, city, country):
    print '%s live in %s, %s' % (name, city, country)
    
f = functools.partial(echo, city='Hangzhou', country='China')

f('Tom and Jerry')
```

    Tom and Jerry live in Hangzhou, China
    


```python
# functools.wraps
import functools

def before_deco(f):
    #@functools.wraps(f)
    def wrapper(*args, **kwargs):
        print 'before'
        return f(*args, **kwargs)
    
    return wrapper

@before_deco
def test(name):
    print name
    
print test.func_name
```

    wrapper
    

### Practice


```python
# implement a to_int function, that convert hex string data to integer
# eg:
#     to_int('\xef')  ==> 239
#     to_int('\xef\x01')  ==> 61185
# NOTE: builtin function ord can return the integer ordinal of a one-character string

```

## Unit Testing


```python
# Unit Testing
import unittest

def to_int(data):
    sum = 1
    return sum 


class TestToInt(unittest.TestCase):
    def test_to_int_with_one_char_string(self):
        self.assertEqual(to_int('\x01'), 1)
    
    def test_to_int_with_two_chars_string(self):
        self.assertEqual(to_int('\xef\x01'), 61185)

suite = unittest.TestLoader().loadTestsFromTestCase(TestToInt)
unittest.TextTestRunner().run(suite)
```

    .
    ----------------------------------------------------------------------
    Ran 1 test in 0.001s
    
    OK
    




    <unittest.runner.TextTestResult run=1 errors=0 failures=0>




```python
# Unit Testing
import unittest

def to_int(data):
    sum = 0
    for index, num in enumerate(data[::-1]): 
        sum += ord(num)*16**(index*2) 
    return sum


class TestToInt(unittest.TestCase):
    def test_to_int_with_one_char_string(self):
        self.assertEqual(to_int('\x01'), 1)
    
    def test_to_int_with_two_chars_string(self):
        self.assertEqual(to_int('\xef\x01'), 61185)

suite = unittest.TestLoader().loadTestsFromTestCase(TestToInt)
unittest.TextTestRunner().run(suite)
```


```python
# Unit Testing
import unittest

def to_int(data):
    sum = reduce(lambda x,y : x + y, map(lambda x, y: ord(x)*(16**(y*2)), data[::-1], range(len(data))), 0)
    return sum

class TestToInt(unittest.TestCase):
    def test_to_int_with_one_char_string(self):
        self.assertEqual(to_int('\x01'), 1)
    
    def test_to_int_with_two_chars_string(self):
        self.assertEqual(to_int('\xef\x01'), 61185)

suite = unittest.TestLoader().loadTestsFromTestCase(TestToInt)
unittest.TextTestRunner().run(suite)
```

    ..
    ----------------------------------------------------------------------
    Ran 2 tests in 0.020s
    
    OK
    




    <unittest.runner.TextTestResult run=2 errors=0 failures=0>




```python
# mock
import time

def delay_print(msg, delay):
    time.sleep(delay)
    print msg
    
import unittest

time.sleep = lambda x: True

class TestDelayPrint(unittest.TestCase):
    def test_delay_print_empty_string(self):
        delay_print('', 5)
            
suite = unittest.TestLoader().loadTestsFromTestCase(TestDelayPrint)
unittest.TextTestRunner().run(suite)
```

    .

    
    

    
    ----------------------------------------------------------------------
    Ran 1 test in 0.003s
    
    OK
    




    <unittest.runner.TextTestResult run=1 errors=0 failures=0>



### One more step


```python
import unittest
from mock import Mock
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


class MockConnection(object):

    def exec_command(self, command):
        return  0, 'eth3      Link encap:Ethernet  HWaddr 00:0F:BB:BA:99:CD  \ninet address:10.0.1.2  Bcast:10.0.2.255  Mask:255.255.255.0\nUP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1\nRX packets:0 errors:0 dropped:0 overruns:0 frame:0\nTX packets:16 errors:0 dropped:0 overruns:0 carrier:0\ncollisions:0 txqueuelen:1000\nRX bytes:0 (0.0 B)  TX bytes:1152 (1.1 KiB)'

class TestFsmAccess(unittest.TestCase):
    
    def test_get_lmp_ip_add_not_use_Mock(self):
        mock_instant = MockConnection()
        fsm_instance = FsmAccess(connection=mock_instant)
        ret = fsm_instance.get_lmp_ip_address()
        self.assertEqual(ret, '10.0.1.2')

    def test_get_lmp_ip_address_use_mock(self):
        con_mock = Mock()
        con_mock.exec_command.return_value = 0, 'eth3      Link encap:Ethernet  HWaddr 00:0F:BB:BA:99:CD  \ninet address:10.0.1.2  Bcast:10.0.2.255  Mask:255.255.255.0\nUP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1\nRX packets:0 errors:0 dropped:0 overruns:0 frame:0\nTX packets:16 errors:0 dropped:0 overruns:0 carrier:0\ncollisions:0 txqueuelen:1000\nRX bytes:0 (0.0 B)  TX bytes:1152 (1.1 KiB)'
        fsm_instance = FsmAccess(connection=con_mock)
        ret = fsm_instance.get_lmp_ip_address()
        self.assertEqual(ret, '10.0.1.2')

    def test_get_lmp_ip_address_use_mock_return_value(self):
        fsm_instance = FsmAccess(connection=Mock())
        fsm_instance.con.exec_command = Mock(return_value=(0, 'eth3      Link encap:Ethernet  HWaddr 00:0F:BB:BA:99:CD  \ninet address:10.0.1.2  Bcast:10.0.2.255  Mask:255.255.255.0\nUP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1\nRX packets:0 errors:0 dropped:0 overruns:0 frame:0\nTX packets:16 errors:0 dropped:0 overruns:0 carrier:0\ncollisions:0 txqueuelen:1000\nRX bytes:0 (0.0 B)  TX bytes:1152 (1.1 KiB)'))
        ret = fsm_instance.get_lmp_ip_address()
        self.assertEqual(ret, '10.0.1.2')

    def test_get_lmp_ip_address_use_mock_return_value_new(self):
        fsm_instance = FsmAccess(connection=Mock())
        fsm_instance.con.exec_command = Mock(return_value=(0, 'eth3      Link encap:Ethernet  HWaddr 00:0F:BB:BA:99:CD  \ninet addr:10.0.1.2  Bcast:10.0.2.255  Mask:255.255.255.0\nUP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1\nRX packets:0 errors:0 dropped:0 overruns:0 frame:0\nTX packets:16 errors:0 dropped:0 overruns:0 carrier:0\ncollisions:0 txqueuelen:1000\nRX bytes:0 (0.0 B)  TX bytes:1152 (1.1 KiB)'))
        ret = fsm_instance.get_lmp_ip_address()
        self.assertEqual(ret, '10.0.1.2')

suite = unittest.TestLoader().loadTestsFromTestCase(TestFsmAccess)

unittest.TextTestRunner().run(suite)
```

    ....
    ----------------------------------------------------------------------
    Ran 4 tests in 0.017s
    
    OK
    




    <unittest.runner.TextTestResult run=4 errors=0 failures=0>



### Practice

> small change with the get_lmp_ip_address example, assume the output word address is addr

    def test_get_lmp_ip_address_with_new_output(self):
        fsm_instance = FsmAccess(connection=Mock())
        fsm_instance.con.exec_command = Mock(return_value=(0, 'eth3      Link encap:Ethernet  HWaddr 00:0F:BB:BA:99:CD  \ninet addr:10.0.1.2  Bcast:10.0.2.255  Mask:255.255.255.0\nUP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1\nRX packets:0 errors:0 dropped:0 overruns:0 frame:0\nTX packets:16 errors:0 dropped:0 overruns:0 carrier:0\ncollisions:0 txqueuelen:1000\nRX bytes:0 (0.0 B)  TX bytes:1152 (1.1 KiB)'))
        ret = fsm_instance.get_lmp_ip_address()
        self.assertEqual(ret, '10.0.1.2')

## Introspection

![introspection](/files/images/introspection.jpg)


```python
# dir
import os

print dir(os)
```


```python
# type
s = 'hello world'

print type(s)
```

> Everything is an object in Python.


```python
a = 5
print type(a)
print type(type(a))
```


```python
# hasattr
class DynamicObject(object):
    def __getattr__(self, attr):
        if attr in ('a', 'b', 'c'):
            return attr.upper()
        raise AttributeError

obj = DynamicObject()

print hasattr(obj, 'a')
print hasattr(obj, 'd')

```

### Practice


```python
# 1. implement a bash wrapper, so that I can call bash command like a class attribute
#
#     bash = BashWrapper()
#     bash.ping('10.69.69.124')
#     bash.ls('-l', '~')
#
# Write your code here
```


```python
import subprocess
class BashWrapper(object):
        fun_name = []
        def __getattr__(self, fun): 
            BashWrapper.fun_name.append(fun)
            setattr(self, fun, lambda args: subprocess.check_output('{} {}'.format(BashWrapper.fun_name[0], args),shell=True))
            return self.fun
              
bash = BashWrapper()
print bash.ping("-i 1 127.0.0.1")
```

    
    Pinging 127.0.0.1 with 32 bytes of data:
    Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
    Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
    Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
    Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
    
    Ping statistics for 127.0.0.1:
        Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
    Approximate round trip times in milli-seconds:
        Minimum = 0ms, Maximum = 0ms, Average = 0ms
    
    


```python
# one more step...
# 2. what about a bash wrapper module, so that I can call bash command like a module import
#     from bashwrapper import ping
#     ping('10.69.69.124')
#     from bashwrapper import ls
#     ls('-l', '~')
```

## Parallel Handling

![run](/files/images/run.png)


```python
# fetch content size from a series of web sites
import urllib
import time

urls = ['http://tdlte-report-server.china.nsn-net.net',
        'http://10.140.161.16/ta_doc/',
        'http://pypi.ute.inside.nsn.com']
begin = time.time()
for url in urls:
    print len(urllib.urlopen(url, proxies={}).read())
end = time.time()
print 'used time:', end-begin
```

    32234
    8614
    137994
    used time: 2.9279999733
    


```python
# introduce thread
from threading import Thread
import urllib
import time

urls = ['http://tdlte-report-server.china.nsn-net.net',
        'http://10.140.161.16/ta_doc/',
        'http://pypi.ute.inside.nsn.com']

class UrlFetchThread(Thread):
    def __init__(self, url, *args):
        super(UrlFetchThread, self).__init__(*args)
        self._url = url
        
    def run(self):
        print len(urllib.urlopen(self._url).read())

begin = time.time()
threads = map(UrlFetchThread, urls)
for t in threads:
    t.start()
    t.join()
end = time.time()
print 'used time:', end-begin
```

    32234
    2420
    2429
    used time: 2.75999999046
    


```python
# introduce multi process
from multiprocessing import Process
import urllib
import time

urls = ['http://tdlte-report-server.china.nsn-net.net',
        'http://10.140.161.16/ta_doc/',
        'http://pypi.ute.inside.nsn.com']

class UrlFetchProcess(Process):
    def __init__(self, url, *args):
        super(UrlFetchProcess, self).__init__(*args)
        self._url = url
        
    def run(self):
        print len(urllib.urlopen(self._url).read())
begin = time.time()        
processes = map(UrlFetchProcess, urls)
for p in processes:
    p.start()
    p.join()
end = time.time()
print 'used time:', end - begin
```

    used time: 2.54800009727
    


```python
# use Pool
import time
from multiprocessing import Pool
from multiprocessing.dummy import Pool as ThreadPool

urls = ['http://tdlte-report-server.china.nsn-net.net',
        'http://10.140.161.16/ta_doc/',
        'http://pypi.ute.inside.nsn.com']

def fetch_content(url):
    print len(urllib.urlopen(url).read())

print 'begin test!'
procss_start_time = time.time()
pool = Pool()
pool.map(fetch_content, urls)
pool.close()
pool.join()
procss_end_time = time.time()
print 'proces use time:', procss_end_time - procss_start_time

# -----------------------------------------
thread_start_time = time.time()
thread_pool = ThreadPool()
thread_pool.map(fetch_content, urls)
thread_pool.close()
thread_pool.join()
thread_end_time = time.time()
print 'thread use time:', thread_end_time - thread_start_time
```

    begin test!
    


```python
# introduce gevent
import gevent
from gevent import monkey
import time
monkey.patch_all()

urls = ['http://tdlte-report-server.china.nsn-net.net',
        'http://10.140.161.16/ta_doc/',
        'http://pypi.ute.inside.nsn.com']

def fetch_content(url):
    print len(urllib.urlopen(url).read())
begin = time.time()    
[gevent.spawn(fetch_content, url) for url in urls]

gevent.wait()
end = time.time()
print 'used time:', end - begin
```


```python
# Queue
from multiprocessing import Process, Queue
import time

def f(q, num):
    q.put([num, None, 'hello'])

if __name__ == '__main__':
    q = Queue()
    begin  = time.time()
    p1 = Process(target=f, args=(q, 12))
    p2 = Process(target=f, args=(q, 24))
    p1.start()
    p2.start()
    print q.get()
    print q.get()
    p1.join()
    p2.join()
    end = time.time()
    print 'used time:', end - begin
```

### Practice


```python
# (after class) implement a FAST ftp downloder 
# eg: download ftp://hztdltev01.china.nsn-net.net/esa_data/

```

## Web Development

![Python Web](/files/images/pyweb.png)


```python
# BaseHTTPServer and SimpleHTTPServer
# python -m SimpleHTTPServer 8080
from BaseHTTPServer import HTTPServer
from SimpleHTTPServer import SimpleHTTPRequestHandler

server = HTTPServer(('0.0.0.0', 8282), SimpleHTTPRequestHandler)

server.serve_forever()
```


```python
# with micro framework bottle.py
from bottle import route, run, template

@route('/hello/<name>')
def index(name):
    return template('<b>Hello {{name}}</b>!', name=name)

run(host='localhost', port=8181)
```

### Practice


```python
# implement a simple REST service for user operation using Python, 
#   you can store the user info into memory, DB or files.
#   the return data should be in JSON format, 
#     GET/POST/DELETE method should be supported
# Example:
#     GET  /api/users  ==> 
#         ['tom', 'jerry', 'lily']
#     POST  /api/users  ['james', 'terry']  ==>  
#         ['tom', 'jerry', 'lily', 'james', 'terry']
#     DELETE  /api/users/james  ==>  
#         ['tom', 'jerry', 'lily', 'terry']
from bottle import get, post, delete, response, run
import json

@get('/api/users')
def users():
    response.set_header('Content-Type', 'application/json')
    return json.dumps(['tom', 'jerry', 'lily'])

run(host='localhost', port=11111)
```

## Reference

* http://www.diveintopython.net/power_of_introspection/
* https://docs.python.org/2/library/inspect.html
* https://docs.python.org/2/howto/functional.html
* https://en.wikipedia.org/wiki/Functional_programming
* https://docs.python.org/2/library/functions.html#iter
* http://butunclebob.com/files/downloads/Prime%20Factors%20Kata.ppt
* https://blog.8thlight.com/uncle-bob/2013/05/27/TheTransformationPriorityPremise.html
* https://wiki.python.org/moin/Generators
* https://docs.python.org/2/library/threading.html
* https://docs.python.org/2/library/multiprocessing.html
* http://www.gevent.org/intro.html
* http://bottlepy.org/docs/dev/index.html
* http://api.mongodb.org/python/current/tutorial.html
* https://docs.python.org/2/library/simplehttpserver.html



-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>


