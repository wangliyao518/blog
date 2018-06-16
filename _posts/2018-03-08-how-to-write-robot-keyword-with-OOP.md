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



## one kill processes example

上面的代码相对于robot 来说还算是"底层"的robot keyword代码了, 底层代码应该OOP, 这个应该是大多人都非常认可的. 我们再来看一个稍微上一层"用户层面"keyword的例子.
假设用户有一个需求, 就是要实现一个kill 进程的keyword, 参数应该就是"进程名"的参数列表.
需求很容易, 经验丰富的我们很容易就实现了代码
```python
import subbprocess
def kill_process(*process_list):
    for each_process in process_list:
        ppid = subprocess.check_output("ps -ef |grep {} |grep -v grep |awk -F ' ' '{print $2}'".format(each_process))
        ret = subbprocess.call('sudo kill - 9 {}'.format(ppid))

```

有一天, 我们用户想通过这个keyword 去kill kibana进程, 通过传入kibana发现没生效. 事后我们发现原来kibana进程名字不叫kibana而是叫node. 于是我们修改上面的代码如下

```python
import subbprocess
def kill_process(*process_list):
    for each_process in process_list:
        if each_p_process == 'kibana':
            each_process = 'node'
        ppid = subprocess.check_output("ps -ef |grep {} |grep -v grep |awk -F ' ' '{print $2}'".format(each_process))
        ret = subbprocess.call('sudo kill - 9 {}'.format(ppid))
```
好像微小的改动就实现了我们的功能, 但上面代码有一个问题, 就是所有的其它进程名也都会先判断进程名是否等于"kibana", 为了这个kibana的例外, 我们代码块中增加了代码, 这个代码是影响着所有的process, 如果还有其它的一些例外进程, 我们会在这个代码块中增加很多的elif语句.

好的, 我们把代码改成如下:

```python
import subbprocess

class Process(object):
    def __init__(self, name):
        self.process_name = name
    def pid(self):
        return subprocess.check_output("ps -ef |grep {} |grep -v grep |awk -F ' ' '{print $2}'".format(process_name))
    def start(self):
        pass
    def stop(self):
        subbprocess.call('sudo kill - 9 {}'.format(self.pid))

class KibanaProcess(object):
    
    def __init__(self, name):
        self.process_nme = 'node'

class ProcessFactory(object):
    
    def get_process_instant(self, name):
        if name == "kibana":
            return KibanaProcess(name)
        return Process(name)
        

class ProcessControl(object):
    
    def __init__(self, process_name_list):
        self.ppid = None
        self.process_name_list = process_name_list

    def stop(self):
        for process_name in self.process_name_list:
            ProcessFactory().get_process_instant(process_name).stop()

def kill_process(*process_list):
    ProcessControl(process_list).stop()
                
```


## another capture logs example

再举一个抓各种log的例子, 假设我们已经有了各种抓log的底层keyword, 但有一天用户有一个需求, 是要求提供一个common的抓各种log的keyword, 这些log包含有syslog, ttitrace的log, aamessage的log. (syslog, ttitrace, aamessage log 由于都是数据流形式, 所以分别有start和stop两个对应的keyword).

由于几种log 都已经有对应的底层keyword, 我们很容易就实现了这个common的功能, 伪代码如下:

```python

def start_capture_common_logs(syslog=True, ttitrace=True, aatrace=True):
    start_syslog(syslog_save_path)
    start_ttitrace(ttitrace_save_path)
    start_aaMessageTrace(aatrace_save_path)

def stop_capture_common_logs():
    stop_syslog()
    stop_ttitrace()
    stop_aaMessageTrace()    

```

非常简单,我们很快就实现了需求,而且只要底层的几个start和sop keyword能够正常工作, 上面的common keyword也就可以正常工作.
我们现现在来稍微改变下需求, 由于aatrace消息底层的keyword是提供了message 过滤的profile文件, 可能每个component关心的message是不一样的, 也就是不同component的用户需要提供不同的profile文件.
按照面向过程式编程, 我们很容易写出如下的代码
```python
def start_capture_common_logs(syslog=True, ttitrace=True, aatrace=True, aatrace_profile=default_profile.txt):
    start_syslog()
    start_ttitrace()
    start_aaMessageTrace(aatrrace_profile)

```

看上去实现也非常的容易, 我们只是增加了参数然后传入了底层的函数就实现了对应的功能, 但这里有一个问题, 我们发现前面的3个参数都是布尔类型, 都是用户可通过这个来置是否要抓对应的log, 而最后一个参数很前面几个不是一类, 而且最后一个参数究竟对应前面那个的proflie呢? 我们只有通过名字来区分. 如果有一天syslog也有profile, 我们也只能取一个profile名字, 而且调用时千万不能误调用.  





-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>
