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
the above code can work well, and it seems we only change a little code after new requirement comming, but there have a problem that is user only want change local pc execute command logical but also change the execute command on remote host code, so after we change code we need test the get_ethernet_ip_address keyword in two scenario (local and remote), how about use OOP to implement the above feature? let's see the code
上面的代码可以很好的工作, 看上去新的需求来后我们也只是很少的改动就可以实现功能, 但这里有一个问题:用户只是希望get_ethernet_ip_address这个keyword在本地执行时不需要ssh, 但我们确也改动了在remote执行的部分(有的人可能会说,我远程执行没改动啊, 还是调用的execute_shell_command啊, 但加入if else后就代表着这个代码已有改动,更何况python是动态脚本语言),所以在我们的代码改动后, 我们需要测试本地和远程两种场景.如果换成面向对象会怎么样? 请看代码

```python

# interface.py

from imp import HostAccess, SshConnection


class Interface(object):

    def __init__(self):
        self.ssh_con = None

    def setup(self, **kwargs):
        host_ip = kwargs.get('host')
        username = kwargs.get('username')
        password = kwargs.get('password')
        self.ssh_con = SshConnection(host_ip, username, password)
        self.ssh_con.connect()
        self.access_obj = HostAccess(self.ssh_con)

    def get_ethernet_ip_address(self, **kwargs):
        return self.access_obj.get_lmp_ip_addr()

    def teardown(self, **kwargs):
        self.ssh_con.disconnect()


# imp.py
import paramiko

class HostAccess(object):

    def __init__(self, connection):
        self.con = connection

    def get_ethernet_ip_addr(self, eth_name):
        result = ""
        stderr, stdout = self.con.exec_command("ifconfig {}".format(eth_name))
        pattern = r"(inet addr:\d{1,4}.\d{1,4}.\d{1,4}.\d{1,4})"
        for line in stdout.split('\n'):
            ret = re.search(pattern, line)
            if ret:
                result = ret.groups()[0]
        return result


class SshConnection(object):
    def __init__(self, host, port=22, username, password):
        self.host = host
        self.port = port
        self.username = username
        self.password = password
        self.con = None

    def connect(self):
        self.con = paramiko.SSHClient()
        self.con.set_missing_host_key_policy(paramiko.AutoAddPolicy())
        self.con.connect(self.host, self.port, self.username, self.password)

    def exec_command(self, command):
        stdin, stdout, stderr = self.con.exec_command(command)
        ret = stdout.read()
        return ret

    def disconnect(self):
        self.con.close()

```
we just use 3 class to implement this requirement, when user want local command not need ssh we only need add one class, the code as below:
上面就是我们用OOP之后写的代码,代码行数是多了,我们同时用了3个类来完成这个任务, 当本地执行命令不需要ssh时,我们只需要增加一个class, 代码如下

```python
# imp.py
import subprocess

class LocalSshConnection(object):

    def __init__(self):
        pass

    def connect(self):
        pass

    def disconnect(self):
        pass

    def exec_command(self, command):
        """ Execute command on locally.

        :param String command: command string
        """
        result = subprocess.check_output(cmd)
        return result

```
after we add this LocalSshConnection class, we only need change interface.py import sentence as below:

```python
from imp import HostAccess, SshConnection, LocalSshConnection

class Interface(object):

    def __init__(self):
        self.ssh_con = None

    def setup(self, **kwargs):
        host_ip = kwargs.get('host')
        username = kwargs.get('username')
        password = kwargs.get('password')
        ssh_con_dict = {'127.0.0.1': LocalSshConnection, 'localhost': LocalSshConnection}
        self.ssh_con = ssh_con_dict.get(host_ip, SshConnection)
        self.ssh_con.connect()
        self.access_obj = HostAccess(self.ssh_con)

    def get_ethernet_ip_address(self, **kwargs):
        return self.access_obj.get_lmp_ip_addr()

    def teardown(self, **kwargs):
        self.ssh_con.disconnect()

```
上面的代码我们虽然用字典的方式消除掉了if else语句, 但细心的读者会发现,我们之前的面向过程其实也可以用这个字典方式消除掉if else, 而我们的面向对象好像代码更长呢? 那它究竟的好处是什么呢? 从上面的面向过程和面向对象我们能清晰的看出, 我们需求变动的是ssh连接的变化, 而通过连接去执行对应命令和解析这块算法的地方是不需要变化的, 但面向过程中导致了这块地方也跟着变动了, 如果有了UT代码,这部分也需要跟着变化的,我们的需求不需要这块变动,显然是不合理的. 而面向对象后, 我们明显应对变化更灵活了,这就是OOP的好处!


-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>
