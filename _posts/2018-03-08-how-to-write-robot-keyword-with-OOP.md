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

def get_ethernet_ip_address(eth_name):
    search_command = 'sudo ifconfig {}'.format(eth_name)
    result = execute_shell_command(search_command)
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

If user add new requirement such as fetch some thing from some file in the remote host, we can implement it easily just refer the above example




## Object Oriented Programming
the above code can work well, 

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
