---
layout: post
title: "some intresting bug and robot keyword bug"
description: what's the bug and did you find some bugs in your daily software? what's the robot keyword bug? is't the same thing with software bug? in this article I'll show you.
image: 'https://raw.githubusercontent.com/wangliyao518/blog/gh-pages/assets/img/bug.jpg'
category: 'bug'
tags:
- bug
- robot
- pronto

twitter_text: what's the bug and did you find some bugs in your daily software?
introduction: what's the bug and did you find some bugs in your daily software? what's the robot keyword bug?
---

What is the bug of the software? close your eye and think for three seconds, I'll give an official explanation:Bug is an English word, which means bug, defect, damage, poverty, eavesdropper, bug and so on. It is now known that some of the undiscovered defects or problems that are hidden in a computer system or program are known as bug (vulnerabilities).
什么是软件的bug？闭目思考三秒钟，我先给出官方的解释:bug是一个英文单词，本意是臭虫、缺陷、损坏、犯贫、窃听器、小虫等意思。现在人们将在电脑系统或程序中，隐藏着的一些未被发现的缺陷或问题统称为bug（漏洞）。

一般定义缺陷有以下5条原则(The general definition of defects has the following five principles.)：

    1. 软件未实现**产品说明书**要求的功能(The software does not realize the function of product specification.)。
    2. 软件出现**产品说明书**指明不应该出现的错误(The product specification indicates the error that should not appear.)。
    3. 软件实现了**产品说明书**未说明的功能(The software implements the unstated function of the product specification.)。
    4. 软件未实现**产品说明书**虽未明确提及但应该实现的目标(The software does not implement the target that the product specification does not explicitly mention but should be achieved.)。
    5. 软件难以理解，不易使用，运行速度慢，或者软件测试员认为最终用户会认为不好(The software is difficult to understand, not easy to use, slow to run, or the software tester thinks the end user will feel bad.)。



上面对bug的定义已算非常的清楚了, 5条原则中我们发现前4条中都提到了产品说明书, 可见产品说明书的重要, 也说这个产品说明书很多时候就是合同里面的内容, 这里面其实已经定义了软件需要做什么,应该有的各种功能, 所以有的时候对bug的测试也是对产品说明说的检视, 我也相信很多测试人员也经历过对产品说明书像测试软件本身一样不断反复的"咬文嚼字"检视.
The definition of the bug on the above is very clear, we found that the first four of five principles mentioned in the product description for the important of product manuals, instructions many times also said that the product is the content of the contract, there is already defined the software needs to be done, should be a variety of functions, so sometimes the bug testing is also said to the product description of review, I also believe that many testers have experienced for checking product specification as test software itself.

但很多奇怪的bug并非就和软件产品说明书有太多关系, 这个时候就是第5点发挥它重要作用的地方,这也就是为什么我们正规的软件开发公司一定需要专业的测试人员, 专业的测试人员应该从专业的测试角度思考问题, 他们是挑剔的用户
But a lot of strange bugs not software product manuals and have too much concern, at this time is 5 PM play its important role, that is why we must need the formal software development company professional testing personnel, professional testing personnel should be from a professional testing Angle thinking problem, they are picky about users


让我们看看下面几个很有意思的bug


## redundancy
差不多10年前的样子, 校内网(后来应该叫人人网)有点点像facebook在高校异常火爆, 校内网顺势在央视都做起了广告, 可能"设计师"们也想把登上央视这个"殊荣"传达给所有的用户, 所有在上了央视没多久后校内网在登录的首页左侧放上了自己上央视的这个广告.可能技术人员没觉得这个有任何的不妥,一是来展示自己的"殊荣", 二是可能来显示自己网站技术的进步--可能不再限制于只能上传图片了,接着网站视频也可嵌入了.
Almost a decade ago, xiaonei (later should call renren) have a little like facebook in university are booming, and conveniently in xiaonei to start advertising on CCTV, may be the "designer" also want to put across this "honor" on CCTV to all users, all in the CCTV didn't take long after the xiaonei on the front page of the login on the left side of the own CCTV on this AD was put on. Possible technical personnel didn't think this has any wrong, one is to show its own "honor", 2 it is possible to display their website technology - might no longer be confined to only upload pictures, then the web video can also be embedded.

如果用上面的软件测试原则的前4条来验证好像这里也没任何问题, 第5条来验证,如果"用户"不够很挑剔也没任何问题, 那么问题在哪里呢? 问题就在于有点点"画蛇添足"了! 为什么这么说呢?　请让我慢慢道来
If in the first four principles of software testing above to verify if there is no problem, article 5 to verify, if the customer is not very picky also didn't any problem, so where is the problem?The problem is that there are dots.Why do you say that?Please let me talk slowly.

首先, 让我们来剖析他们把这个视频放到网站首页的目的.
First of all, let's dissect the purpose of putting this video on the homepage of the website,


目的一可能是广告, 在央视中花了大价钱就是广告, 这个广告不容易啊, 自然还需要更加广而告之,如果真是出自这目的, 那就真是画蛇添足了, 为什么呢? 很明显啊, 用户都已经登录了你的页面, 都已经知道你这个网站了, 还需要吸引他们过来?这个广告只应该出现在其它网络流量入口比较大的地方.
The purpose of an advertisement may be, is advertising spent a large amount of money in the CCTV, this AD is not easy, natural also need more widely, if it is really from this purpose, that is really gild the lily, why?Obviously, the user has logged on to your page, and you already know your site, and you need to attract them?This advertisement should only appear in other network traffic entrance relatively big place.


目的二可能是告诉用户我们网站已经改良了,可以上传视频了, 如果真是这个目的, 我认为他这个做法也有点点偷工减料之嫌, 不应该拿着央视的广告来充数, 因为这个广告并未突出可以上传视频,而是让大家觉得人人网有家底可以在央视打广告.如果真是这个目的,还不如来个几帧动画来的更直观.
Goal 2 is probably tell users we have improved, you can upload the video, if it is really the purpose, that is I think he has little to cut corners, should not take a CCTV's advertising who sucks, because the AD did not highlight can upload video, but let everybody feel renren have money can in CCTV advertising. If it is really this purpose, it is better to have a few frame animation to more intuitive.


其次让我们来看看这个广告放在首页针对的客户, 登录校内网的都是在校大学生, 我所见到大学们都喜欢在上各种课时悄悄登录这个"交友"网站, 但这个视频上来后并未给他们添加喜悦,而是烦恼, 因为教室里面的所有人都一下听到声音.包括正在教课的老师. 有的用户可能也懵了"上次登录时都没有声音的啊!", 这样反而导致他们登录的频率会降低.
Second let's take a look at the ads on the front page for the customer, the login xiaonei are college students, the university are all like that I've seen in a variety of classes quietly login the "dating sites", but didn't add joy to their after this video, but the worry, because the inside of the classroom all hear the sound. Including teacher. Some users may also meng "last login has no sound!"That, in turn, will lead to lower frequency of login.

综上所看,他是不是有画蛇添足之感.当年我也针对测试给校内网发了很多求职信,并附上这个问题之我见, 只可惜在下才疏学浅实在不能登大雅之堂, 不过后来也没过多久他们自己也把这个视频从首页移除掉了
Overall look, whether or not he has the feeling of gild the lily. I also on the test sent xiaonei many cover letter, and attach the problem I have seen, but of the next pretty can't appeal, but then it wasn't long before they themselves also move the video from the home page removed





-----

Want to see something else added? <a href="https://github.com/wangliyao518/blog/issues/new">Open an issue.</a>
