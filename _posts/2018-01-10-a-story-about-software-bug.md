---
layout: post
title: "a story about software bugs"
date: 2018-01-10 23:20:45
image: 'http://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_760/v1502757949/o-sombra_xyw4wq.jpg'
description: This is a true story of a large software company, why did the bug occur, is the lack of unit testing, system testing? No TDD or ATDD? Are we missing RCA and EDA? I think maybe as a large company this aspect is very professional, I want to look at this from another angle
category: 'story'
tags:
- story
- software bug
twitter_text: from another angle to see one classic bug story.
introduction: from another angle to see one classic bug story.
---


## Background --what (背景)
A big software company is having an annual party, in which there is a raffle(which can be understood as the most important, since there are probably not many people interested in going there without a raffle). After all, we're a software company, so natural raffle can't be played with a note. We need a tall piece of software.
一个软件大公司要搞年会，年会上有一个环节--抽奖（其实也可以理解为最重要的环节，因为年会要是没有抽奖估计也没有多少人有兴趣去）。毕竟我们是做软件的公司嘛，所以自然抽奖也不能用抽纸条这些低级的玩法，我们需要一个高大上的软件来完成

So we started hiring people on the company forum to discuss the plan. After all, we are a very talented company, and we are very quick to recruit and have a very simple plan: 4 times lucky draw will be held, the names of the winning employees will be automatically removed from the list(meaning no cumulative winners), and the second and higher awards will need to be redrawn separately if the staff is not present. The list is also removed from the raffle list. First, A raffle guest draws out 5 tail numbers, in the 5 tail numbers of the staff all won the award the smallest "third award", then B raffle guest draws 100 "second award", then C raffle guest draws 50 "first award", The last D raffle guest draws from the legal list of the most fortunate 10 "Principal award"
于是在公司论坛上开始招兵买马，讨论方案。毕竟我们是人才济济的公司，很快人招齐了，方案也定好了，方案很简单：会进行4轮抽奖，每轮中奖的员工名字自动从抽奖名单中剔除（意味着不累计中奖），二等奖及其以上的奖项如果员工没到现场，需要重新单独抽取这个未到场的名额，未到场的名单也从抽奖名单中剔除，首先有A抽奖嘉宾抽取5个尾号出来，在这5个尾号之中的员工全部都中了奖最小的“三等级”，然后B抽奖嘉宾抽取100个“二等奖”，然后C抽奖嘉宾抽取50个“一等奖”，最后D抽奖嘉宾从合法的未中奖名单中抽取最幸运的10个“特等奖”


The process was quickly completed, several people tested and found no problems, resulting in the same name appearing twice on each of the winning screens at the time of the annual awards and tens of thousands of people watching this bug
程序很快就完成了，也经过了几个人的验收测试，没有发现任何问题，结果在年会开奖时刻，抽取一等奖时刻，同一个名字分别在中奖屏幕上出现两次，在场千万人一起见证了这个bug的产生



## Stakeholders 'response（各方反应）

All sides have opened the chart, the wechart groups are sending out the "obvious" bug screenshot, the "dark box" theory spread in the company，the software developer searched for the bug overnight, and the developer's boss explained to the company leaders overnight: "no software can say no bug, we have no conspiracy, developers are still looking for bugs overnight.
各方闹开了锅，各个微信群中都在发这“显而易见”bug的截图，“暗箱操作”论在公司传开了锅，软件的开发者连夜寻找bug的来源，开发者的上司连夜在公司领导群中解释：“无软件无bug，软件有bug，我们无黑幕，开发者连夜还在查bug”



## root cause --why（根因）
We have excellent programmers, and we quickly found out why, because the 50 first prize is a 10-screen display, only 5 screens per screen, the program was designed to be first prize 50 people complete the raffle after the 50 winning list from the legal candidates. It should be removed from the waiting list as long as it is shown to have won the lottery, and it is not removal that has resulted in two appearances on the screen
我们不愧是有着优秀的程序员，很快原因找到了，是因为50个一等奖是分10屏显示，每屏幕只实现5个，程序在设计之初是一等奖50个人全部抽奖完成后就把这50个中奖名单从合法的候选人中剔除。而正确的做法应该是只要显示已经中奖就应该从待抽奖名单中移除掉，也正是因为没有移除掉才导致有2次都出现在屏幕中现象的出现

In order to prove their innocence, the developer actively published the source code, also took out the duplicate winners have on relationship with him proof, also took out their own group above the second prize ratio. It's true: We don't have inside information and the program has bugs
为了证明自己的清白，开发者公布了源码，拿出了自己和中两次者没有任何关系的证明，也拿出了自己组内人员中二等奖以上的比例情况，这个是真实的：我们的确无内幕，程序有bug


Naturally, the developer apologizes for not having verified enough, and for having added a validation check
自然，开发者也道歉自己没验证充分，道歉自己应该加个合法性校验

We're a professional software company, and a lot of comments continue to come， too many people still question the algorithms in the code, diagram as below
面对开发者的解释，大家对“无内幕”表示认可，毕竟我们是专业的软件公司，很多的意见继续扑面而来, 大家还是质疑代码中的算法, 图示如下：
![placeholder](http://res.cloudinary.com/wangliyao518/image/upload/v1520338606/comments1_r26tav.png "comments 1 image")
![placeholder](http://res.cloudinary.com/wangliyao518/image/upload/v1520338606/comments2_wqvh8k.png "comments 2 image")

The real reason is that the random number from random. nextInt() in Java is a pseudo-random number, and the sequence is the same every time a new Random is created. If the list is unchanged and the probability of repetition is very high, the raffle is too unreasonable
实际原因是用的java里的random.nextInt()得到的随机数是伪随机数，每次new Random之后产生的序列都是一样的，如果名单没有变化，产生重复的概率非常高，这个抽奖程序写的太不合理了


## how to solve --how（怎么解决？）
A lot of experts have appeared on the above. what I want to say is if we only change the programming algorithm, we will be able to solve all of you 'concerns and doubts. Is the lottery procedure really fair?
上面已经出现了很多专家，大家分析的也非常有道理， 但我想说的是如果真的只改变编程算法，就一定能解决大家所有人的担心和疑惑，抽奖程序就真的公平了吗？


Many times we were MR zhuge after things happen, We found the pit now, and then our code did run away from the pit, but who could guarantee that there was no hidden pit? More importantly, even if there is no bug in the code, who is able to convince people who are not winning the prize that the software has no "back door".
很多时候我们都是事后诸葛, 我们发现现在有的这个坑，然后我们代码的确逃离了这个坑，但谁又能保证没有隐藏着的坑呢,更重要的是，即便代码中没有任何bug，谁又能让没中奖的人们信服这个软件没“后门”


We still can't let everyone believe that this software is fair, because if the software designers really want to cheat, can make the actual operation of the program is certainly not out of the code, you can specify who want the first prize in the prize, but not low to like big loophole appears above - and a name in two (operation you want to go to, I will no longer show here again)
我们还是不能让大家相信这个软件是公正的，因为如果软件设计者真心想要作弊，可以让实际运行的程序肯定不是公布出来的代码，可以指定想让谁中一等奖就中奖，而且不会低级到像上面出现的大漏洞--同时一个名字中两次（操作方式大家各自去想，我就不再这里添堵了）

So no matter who the author is, no matter how delicate the algorithm is, the problem is still unsolved. As a professional software company, as a RCA and EDA experts, it seems that no real solution is yet.
所以无论换成作者是谁，无论他的算法多么的精妙，问题还是没有解决，而作为专业的软件公司，作为做惯了RCA和EDA的兄弟们，好像依旧没想到真正的解决手段

In fact, there are many ways to solve the problem, we need to understand the code, technology is not a panacea, not a ready-made panacea can cure all diseases, so not only towards the technology in view of the problem, we must first see from the form, from the process point of view (this process is not only have to do UT, is not completely follow TDD, ATDD), since the code for who do not trust, then put a few scattered in different groups of people who do not know each other, or is the development, testing, implementation of separation, or at the same time some people developed the same product and finally we only choose the best one,This is the process of reducing the probability of cheating, like the government, only the supervision of all kinds of systems, the people believe that the heart of justice will improve.
其实问题的解决有很多手段，首先我们要明白，技术代码不是万能的，不是灵丹妙药能治百病，所以不能只朝着技术在看问题，我们首先要从形式上看，从流程上看（这个流程已不单纯只是有没有做UT，是不是完全遵循TDD， ATDD），既然代码放给谁去做都不放心，那放给几个分散在不同组的互相不认识的人来做呢，又或者是开发，测试，执行分离，又或者是同时要几个人开发出来的同样产品，最终工会一起选取最优的，这就是从流程上已经让作弊减少概率，就如政府一样，只有监督各种体制健全，权利分散，百姓相信公正之心才会提升

Secondly, since Python and git are so powerful now, we can also choose the python language to complete this procedure, using git to do the scene management, from the GIT version of clone when the draw, run the Python code site, everyone can clearly see the source code to run together, but also in the lottery before the GIT warehouse with all. Everyone can participate in the review, you can also manage the docker program with the public warehouse, completely transparent and increase the difficulty of the "back door", and notes the same reason, the high degree of difficulty,
其次，既然python 和git 现在这么强大，我们也可以选择python这样的语言来完成这样的程序，用git做管理，抽奖时现场从git clone 版本，现场运行python代码，所有人都可以清楚看到源码运行起来，而且在抽奖前，这个git仓库贡献出来，所有人都可以参与review，也可以用公共的docker仓库来管理程序，完全的透明公开又增加了“后门”的难度，这个就和纸币一样的道理，难度系数高了，假币也就少了


Finally, it also has a lot to do program design point, all programmers are smart people, have more good ideas than me, I will no longer give comments, the above comments is just my opinion, if have some wrong please tell me and forgive me
最后，程序的设计中的确也有很多可做之点，各位程序员们都是聪明之人，想出的点子都比我多，我就不再“班门弄斧”了，以上言论都是出自我的愚见，不对之处，贻笑大方之处还望海涵




-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>















