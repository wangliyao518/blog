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
twitter_text: a story about software bugs.
introduction: a story about software bugs.
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




## how to solve --how（怎么解决？）


-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>















