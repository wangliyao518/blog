---
layout: post
title: "how to write robot keyword with OOP"
description: Robot itself is also a programming language. It is a language for users to write demand stories. Demand story is like narration. It's a process oriented thing. We can easily write process case. Can robot also be written to object - oriented? Yes. It can be.
category: 'robot'
tags:
- design
- python
- robot
- OOP
image: 'https://res.cloudinary.com/dm7h7e8xj/image/upload/c_fill,h_399,w_760/v1501102987/sketch-fuel_eiwjbz.png'
twitter_text: write robot keyword with oop.
introduction: Robot itself is also a programming language. It is a language for users to write demand stories. Demand story is like narration. It's a process oriented thing. We can easily write process case. Can robot also be written to object - oriented? Yes. It can be.
---



## requirement
implement a keyword to execute shell command on remote linux pc
实现一个可以在远程linux系统的pc上执行shell 命令的keyword


## Procedural programming 
it's a very simple requirement, we can implement this task easily with procedural programming
上面的需求非常简单, 我们可以用面向过程的方式简单的实现, 代码如下:

```python
#interface.py

import paramiko
def execute_shell_command(cmd, host, username, password):
    ssh = paramiko.SSHClient()
    ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    ssh.connect(host, 22, username, password)
    stdin,stdout,stderr = ssh.exec_command(cmd)
    outmsg, errmsg = stdout.read(),stderr.read()
    return outmsg
    ssh.close()

```

## Requirement change

but one day, our customer need a new keyword "get ethernet port ip", the input arguments is ethernet name and output is ip address, we add code like below:

```python
#interface.py

import paramiko
import re

def get_ethernet_ip_address(eth_name, host, username, password):
    search_command = 'sudo ifconfig {}'.format(eth_name)
    result = execute_shell_command(search_command, host, username, password)
    pattern = r"inet addr:(\d{1,4}.\d{1,4}.\d{1,4}.\d{1,4})"
    for line in stdout.split('\n'):
        ret = re.search(pattern, line)
        if ret:
            result = ret.groups()[0]
    return result


def execute_shell_command(cmd, host, username, password):
    ssh = paramiko.SSHClient()
    ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    ssh.connect(host, 22, username, password)
    stdin,stdout,stderr = ssh.exec_command(cmd)
    outmsg, errmsg = stdout.read(),stderr.read()
    return outmsg
    ssh.close()

```

If one day user find get_ethernet_ip_address keyword use too much time when execute command in local pc, it seems not necessary via ssh execute local comand, so then we change our code as below:

```python
#interface.py

import paramiko
import subprocess
import re

def get_ethernet_ip_address(eth_name, host, username, password):
    search_command = 'sudo ifconfig {}'.format(eth_name)
    if host == '127.0.0.1' or host == 'localhost':
        result = execute_local_command(search_command)
    else:
        result = execute_shell_command(search_command, host, username, password)
    pattern = r"inet addr:(\d{1,4}.\d{1,4}.\d{1,4}.\d{1,4})"
    for line in stdout.split('\n'):
        ret = re.search(pattern, line)
        if ret:
            result = ret.groups()[0]
    return result


def execute_shell_command(cmd, host, username, password):
    ssh = paramiko.SSHClient()
    ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    ssh.connect(host, 22, username, password)
    stdin,stdout,stderr = ssh.exec_command(cmd)
    outmsg, errmsg = stdout.read(),stderr.read()
    return outmsg
    ssh.close()

def execute_local_command(cmd):
    result = subprocess.check_output(cmd)
    return result

```




## Object Oriented Programming
the above code can work well, and it seems we only change a little code after new requirement comming, but there have a problem that is user only want change local pc execute command logical but also change the execute command on remote host code, so after we change code we need test the get_ethernet_ip_address keyword in two scenario (local and remote)
上面的代码可以很好的工作, 看上去新的需求来后我们也只是很少的改动就可以实现功能, 但这里有一个问题:用户只是希望get_ethernet_ip_address这个keyword在本地执行时不需要ssh, 但我们确也改动了在remote执行的部分(有的人可能会说,我远程执行没改动啊, 还是调用的execute_shell_command啊, 但加入if else后就代表着这个代码已有改动,更何况python是动态脚本语言),所以在我们的代码改动后, 我们需要测试本地和远程两种场景.

## Code


```js
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
```



-----

Want to see something else added? <a href="https://github.com/poole/poole/issues/new">Open an issue.</a>
