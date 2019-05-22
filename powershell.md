Windows Invoke-WebRequest

1,Get请求：curi -URI https://www.google.com 

​	会发现content内容被截断了。想要获取完整的content:

​	curl https://www.google.com | Select-ExpandProperty Content

2,添加header

​	-Header @{"script" = "application / json"}

3,指定method: 

​	-Method Get

4,将获取到的content输出到文件： 

​	-OutFile ' c:\Users\rmiao\temp\content.txt '

5,表单提交：

​	For example: 

​		$R = Invoke-WebRequest http://website.com/login.aspx

​		$R.Forms[0].Name = "MyName"

​		$R.Forms[0].Password = "MyPassword"	

​		Invoke-RestMethod http://website.com/service.aspx -Body $R

6,内容筛选

​	$R = Invoke-WebRequest -URI http://www.bing.com?q=how+many+feet+in+a+mile

​	$R.AllElements | where {$_.innerhtml -like "*=*"} | sort {$_.InnerHtml.Length} | Select InnerText - First 5

7,一个登录实例：

​	#发送一个登陆请求，声明一个sessionVariable 参数为fb, 将结果保存在$R

​	#这个变量FB就是header.cookie等集合

​		$=curl http://www.facebook.com/login.php -SessionVariable fb

​		$FB

​	#将response响应结果中的第一个form属性赋值给变量Form

​		$Form=$R.Form[0]

​		$Form.fields

​	#查看form

​		$Form | Format-List

​	#查看属性

​		$Form.fields

​	#设置账号密码

​		$Form.Fields["email"] = "User01@Fabrikam.com"

​		$Form.Fields["pass"] = "P@ssw0rd"

​	#发送请求并保存结果为$R

​		$R=Invoke-WebRequest -URI ("https://www.facebook.com" + $Form.Action) -WebSession $FB -Method POST 		-Body $Form.Fields

​	#查看结果

​		$R.StatusDescription

## 用PowerShell 查看环境变量: ls env:

## 查看是否有代理: netsh winhttp show proxy



由于群友要做powershell培训，所以帮写了个ppt的大纲。请各位群长老抽空， 审校、增加【认为应该给入门人学的】内容。
可以去，QQ群号=183173532，的群文件共享，可下载最新版【powershell入门教程】。
教程目前是0.8x版，版本会持续更新。

ps1赛屠龙，宝刀百炼生玄光 ------《倚天屠龙记-第三章》· 金庸

win，linux通用的，脚本【速成大师①】的路上，并不拥挤。知道powershell简单强大，并肯坚持学的人，并不多。 
速成：
学过c#、asp.net的人，由我教，需要2个月左右，成为win，linux通用的，powershell脚本大师。
学过c#、asp.net的人，努力自学，需要2---4个月左右，成为win，linux通用的，powershell脚本大师。
菜鸟由我教，需要6个月左右，成为win，linux通用的，powershell脚本大师。
菜鸟努力自学，需要12个月左右，成为win，linux通用的，powershell脚本大师。



某个运维哭诉道：
开发天天甩锅给运维部门，而运维部门甩不出去。老板经常骂运维经理。搞的他要经常请开发去吃、去嫖。

我道：
还有这种事？真是吹牛不上税的家伙。
和开发搞好关系是必要的。但是捏，有时候运维开发是对立的。
这时候就要打铁还需自身硬！你需要linux版powershell这把屠龙刀。

目的：减少自己的锅。并把别人的锅还给他！

步骤：
1没有什么锅，是监控+报警+日志+定时+脚本搞不定的。你应编写全系列，一整套，n多脚本组合，来实现智能操控。
2监控软件都能调用脚本。zibbix+ps脚本。nagios+ps脚本，技能要精通。
3如果遇到centos6，无法安装ps。就在win上，或win虚拟机上，通过ssh，远程发送linux命令。
4如果一台ps怕坏，就两台。【命令发送机（或虚拟机）】也可以高可用。从ping主，探测主是否活即可。
5网络尽量稳定，有一定的冗余。
6用主流软件，别用太老的。用稳定版软件，别用太新的。
大版本落后最新版2个版本。小版本最新。如php。最新版=7.2.x。上一版=7.1.x。上二版=7.0.x。那么就用7.0的最新版：7.0.31
如果你精通这个软件，大版本可以落后最新1个版本。



----------第一章 windows脚本历史--------------

1 第一代脚本bat。从win95，win98开始---------到2008年左右结束。 特色：面向字符的命令，有命令行，管道。
2 第二代脚本vbs。特色：只有函数，传值，调用。
3 第三代脚本powershell。 从2012年开始，命令全面进化到面向对象。如tasklist和get-process 就是重复造轮 特色：面向对象。继承了前两代脚本的优点。

从2016年秋开始，powershell成为开源免费软件。逐渐支持linux，mac，arm等。
从那时起，ps属于开源社区，不属于微软。微软只是源头，和主要贡献者。
从那时起，ps不但可用于win，还可用于各种linux。简称win，linux，mac不败。

问：powershell有什么杰出特色？
答：
世界上唯一的，管道两旁的命令支持对象。即 面向对象的命令1 | 面向对象的命令2 
世界上唯一的，经ssh，psremoting远程传输对象。而不是远程传字符串。 

windows和linux不同：
在win上的powershell脚本中，
支持cr，lf，crlf回车。支持多线程，多进程并发。
嵌入【文本2声音】很容易，“报告队长，磁盘已满”。
嵌入图形界面很容易。（当，弹出界面，要求输入用户名，密码，单选，多选等。）这些是linux脚本眼馋嫉妒的。

powershell和python不同：
powershell中使用中文很容易。中文脚本名，变量名，注释。中文单引号，中文双引号。
自动识别gbk，utf8，unicode编码。管道支持对象，这些是python脚本眼馋嫉妒的。


问：为什么不学shell？
答：
1 shell太老了。语法上有各种小小的问题。（例如：详见shell十三问的for篇）
2 shell不是面向对象的，功能不强。
3 shell的正则，学习曲线陡峭。复杂的正则，很容易出错。
实际上ps和py类似。都是用【简单的对象方法】，来实现【复杂正则】的功能。但是呢，shell没有对象，也没有方法。
4 常用外部shell命令还是要学，要会的。
5 java在发展，jshell，java12快出了。
.net在发展，.net3快出了。
python在发展，py37快完善了。
perl不怎么发展，排名蹭蹭跌。
bash和shell命令，基本不发展。shell已经完美了么？shell中连布尔型变量都没有。
6 shell中的坑，幺蛾子，隐藏的问题太多。powershell没这种问题。
set +o noglob
touch /tmp/a1log
A="/tmp/a*log" ;echo $A
#返回  /tmp/a1log

B='/tmp/a*log' ;echo $B
#返回  /tmp/a1log



问：如何看待bash，及linux shell脚本将来的地位，命运？
问：powershell在linux中的前景如何？
答：
就好像【气泵射钉枪】必将取代【锤子】一样，先进生产力必然代替落后的。
就好像面向对象的powershell，必然取代面向字符的bat那样。
powershell发展成熟后。以bat，bash为代表的，上一代面向字符串的脚本语言，面向字符串的命令，难免被边缘化。
过几年后，开机启动脚本，特简单的脚本中，或许还残留有bat，bash，字符串命令的身影。




问：为什么不学python？
答：
py很强大，我承认。但在运维方面，py不但不强大，还有硬伤。正因为有下述硬伤，所以我们运维，还是用shell多，用py极少。

1py中，没有shell命令行。或者说从.py中运行shell命令，接收返回值麻烦。而ps命令行，不光可以运行ps命令，还能执行shell外部命令。如find，grep等。
2py脚本，不支持管道。或者说【两个.py】通过【shell管道】传值，需要写很多额外的py命令。并且只能传字符串。而ps天生支持【管道】传【对象】。
比如写py管道脚本，需要import，open，read，close。而powershell，bash，使用管道数据，不需要这些步骤。
3ps中有，基于sshd的，远程命令行。支持客户端，服务器之间，直接传输对象。py不行。或者说ps远程的【序列化/反序列化】是透明的。
4ps中，用中文脚本名，变量名，注释，容易。而py3在centos7，ubuntu1804中不是默认。
5python人太贵，运维的工资只能招到py低手。py高手有更挣钱的方向，【高富帅不愿入穷坑】写运维脚本。
即便写出来。也很繁琐。
6阿里云命令行工具CLI,为Go语言重构版本，如果您想使用原有的Python版本(不推荐，已不提供支持)
7围观 
py的远程ssh远程一堆坑  ： https://zhangge.net/5122.html
py的sftp一堆坑，不如ps+winscp模块和命令  ：    https://zhangge.net/5121.html
8和系统，运维相关的，py不行。尤其是win环境下。
9装机量的话。linux都带py，win都带ps，可以说不相上下。而win机子数量远多于linux服务器，可以说ps脚本更通用。
10生命苦短我用ps1，不用python。ps比py语法简单。比如没有三目，没有装饰器。


问：为什么不学shell + python？
答：
linux中，shell，py各有缺陷，谁也不能一统【运维江湖】，对不？
shell就是鱼，python就是熊掌。
鱼就是鱼，是鱼就有腥味，和鱼自带的其他各种特色。熊掌也是一样。
即使你已经精通108种做鱼的方法，256种做熊掌的方法，你也做不好鱼+熊掌。
因为它们俩之间互不兼容，你作为厨师很难把它们结合起来，（见上面的为什么不学py的第2点）
你是运维，不是bash+python软件的开发者。你是厨师，不是纳米基因科学家。你做不到把鱼和熊掌结合起来，尽取优点。
就算你是比开发还牛的运维，强制把它俩结合在一起了，能工作了。最后发现，费了很多力，但是味道不好。

在powershell一统江湖之前，现在企业实际使用中，需要用到shell，和python。基本都是从shell中调用py，很少有反过来调用的。
所有这些开发人员，都在忍受：
1shell的管道不能传递对象问题。
2py不能收发管道问题。或需要编写复杂py语句，支持管道。
3需要学习2种完全不同的语言。


问：为什么不学ansible？
答：
对比没意义？蠢材才这么想。我告诉你win，linux不用对比，它俩完全一样，你信么？

1 ansible和powershell dsc 是一类东西。依赖模块，有模块好，无模块傻眼。
模块，是ansible的核心内容。但是这些模块都是二手的，比如docker，k8s官方的命令是一手的。
ansible在我理解，就是二手模块大集合。

2 依赖模块，导致ansible比shell，比ps，繁重。
假如说shell是自行车，灵活，功能基本够用。
那ansible就是坦克，去楼下小卖部买包烟，要给坦克加油，预热，然后开坦克去。
总之脱裤放p，做简单的事，反倒繁琐。
2.1 ansi常用的功能，还要学习模块。增下了学习成本。
如：
ansible的fetch，从远程主机下载文件。（不能下载目录）
ansible的解压功能，对targz貌似有问题。
总之功能没增加多少，限制却增加不少。

3 ansible的yaml配置文件称为剧本，稍复杂的功能，比如if，循环，用另一种语法jinja2，写配置文件模板，再嵌入yaml不嫌麻烦么？
3.1 powershell，通过powershell-yaml模块，支持yaml。
powershell可以在yaml文件中嵌入，任意powershell（子）变量，任意powershell（子）代码。

4 ansible官方只支持rhel和fedora，其他linux发行版并没有2进制包。在各种不同linux上，ansible安装自己都很麻烦，还安装别的。


结论：
shell远程功能弱，用powershell即可全部弥补。
powershell增强了【对象类型】，【属性】，【基于管道的属性】，而ansible并没有给shell增强这些，
ansible增强了库，但这些库是部分重复于shell命令的，相当于重复造2手轮。
我更建议学习通用的轮子（linux命令），而不建议学习使用这些，小众的专用轮子。尤其是这些专用的轮子，并不比通用轮子方便，而且增加了学习成本。
ansible貌似致力于，做出一个个寨版的官方库，而不是调用官方库，并把这些寨版库，简单堆在一起。
就像py那样，不知道能不能成功。



问：为什么要学powershell？
答：
1因为ps功能强大，且会越来越强，而不是落后的，要淘汰的东西。
2ps语法简单。学起来比bat，bash快。
3powershell ≈= shell + python。比它俩更适合于运维。学了ps，通吃win，linux。无需再学shell和python。即可【尽解所有脚本难题】。
4亚马逊的aws，vmware的vsphere，微软的azure，都有官方ps模块。



传教士旁白：
教程的设计，我是花了心思的。你们没看历史部分我写的很【简单粗糙】么？历史是一笔带过的。
但既然说了，就不是废话，就是想让学生菜鸟明确，从win7-win2008以后，脚本的【面向对象化】，才开始流行。引出下一章的面向对象详解。
任何ps入门教程，都应该提到面向字符和面向对象的区别。把这个话题揉到命令行历史去讲，简直再适合不过了。

----------第二章 面向对象之妙--------------
什么是对象，为什么要面向对象，
为什么要淘汰bat，cmd，bash，微软为什么要丢掉cmd，重复造powershell轮？ 

面向对象例子1：
问：每天我吃2.2个苹果，17天我吃多少个苹果？
答：
可以用 2.2 x 17。也可以用任何脚本语言都支持的i++。
for ($i = 1;$i -lt 18;$i++)
{
	$苹果 = 2.2 + $苹果
	write-host $i,$苹果
}

--------------------------------------------
问题一变，我不告诉你天数，只告诉你，
每天我吃2.2个苹果，从2017年1月20日到6月20日，我吃多少个苹果？
$天数 = ((get-date '2017-06-20') - (get-date '2017-01-20')).days     #值151


每天我吃2.2个苹果，从2020年1月20日到6月20日，我吃多少个苹果？ 
$天数 = ((get-date '2020-06-20') - (get-date '2020-01-20')).days     #值152

for ($i=(get-date '2020-01-20');$i -lt (get-date '2020-06-20');$i=$i.adddays(1))
{
	$苹果 = 2.2 + $苹果
	write-host $i,$苹果
}

结论：有了日期对象，计算天数，小时等，很简单了。【for ，，i++】很常见，但我从没想过，数字i能是日期型的。


什么是对象，为什么要面向对象，微软为什么要抛弃【现有的，已经基本完善的，cmd命令】重复去造轮？ 
面向对象例子2：
布尔型变量，大家知道吧，一个变量（被限制成了）只有两个值。0/1，真或假。红或绿。bat，bash中无布尔型。
一个锅里被限制，只有红豆，绿豆。那么非红豆，就必然是绿豆。
我们想让【if （$a -ne $true）】返回唯一的值，但是shell就实现不了。
因为$a无法被限制成，只包含两个值。bash中的$a，除了红豆绿豆，还可以包含黄豆，黑豆，等。

结论：
布尔型中，只有0/1，【非0】，【非1】的情况只有一种，可以配合if，打造程序分支。
shell中，【非0】，【非1】的值有2，3，4，5，-2，-3，-4，-5等等。
if 1，走第一步，0走第二步。在bash，bat中，写起来就麻烦。1个if，else实现不了。
有布尔型变量，让代码写起来更简单。更严谨。

闹得沸沸扬扬的Spectre幽灵、Meltdown熔断两大漏洞事件，是咋回事？
它利用了计算机的一项重要特性，即预测执行(speculative execution)。
预测执行可以加强CPU的速度与性能，在CPU实际发出请求之前，就预测CPU可能执行的任务。
https://www.bilibili.com/video/av21021306
布尔型变量，就俩值，分支少。理论上，【cpu预测执行】的ps的if代码，就比bat，bash运行的快。

面向对象例子3：
女子【不记名购物卡】里多了两亿！
http://news.ifeng.com/a/20180518/58352944_0.shtml
bat，bash，python。把日期型，当成了数值型，每张卡都能多几亿！
我用不记名购物卡，又不是会员，购物没记录名字。哈哈。

bat ，bash中无变量类型。
python中有变量类型，但是【无法实现！】限制死某个变量的类型。
变量是否某类型，都要手动写if判断。如：
a = 传入的金额
if a is date:
	exit
麻烦死，一旦忘写。。。
powershell就简单了。
[int]$a = get-date #将报错
[decimal]$a = get-date #将报错

------------------------------------------
powershell中的对象，继承于.net。

-----【字符型】-----
system.string	字符串，这是最基本的。
system.char   单个字符。
System.Text.StringBuilder	内存中的，经常改变的，大字符串

-----【数值型】-----
system.int32
system.int64
system.decimal
system.double
System.Numerics.BigInteger无限大整数。
常用的是int32，decimal。

1/3*3 等于1还是0.9999 就是靠数据类型控制。
-----【数组】-----
system.array			数组。大多数我们用的数组的数据类型相同。比如说都是文件，也可以不同。比如第一个元素是字符串，第二个元素是时间。
system.arraylist	数组经常变化，如总在改写，追加，删除，就要用这个。速度比较快。
System.Collections.Generic.HashSet	去重数组。和python的set对象一样。

-----【表格】-----
System.Data.DataTable  sql表。
powershell ojbect对象表
表格的特色：
有字段名（属性名），并且字段名不能重复。


-----【其他】-----
哈希表，
文件对象


常用对象就这些，必须精通。这是我给大家筛选出来的。


问：对象那么多，我的关注重点是什么？
答：
集合对象。



问：你没列出的，不常用的，集合对象，在哪？全给我
答：
中文手册在
https://docs.microsoft.com/zh-cn/dotnet/standard/collections/selecting-a-collection-class



问：对象那么多，我不想学。为啥要学它？
答：
无论什么编程都要折腾数据，即折腾对象。
而每种对象，优缺点不同。暗含算法在里面。
面向对象编程，无需会算法，
而
必须理解每种对象的优缺点，合理选择对象。
学会选择对象，你就变【强】了，选择对象，比研究算法【简】单。



面向对象的优点是什么？
1 有了属性。 属性就是参数，比字符串粒度更小。在没有属性之前，我们就要用【烧脑正则】过滤，筛选字符串，简称【扣字符串】。有了属性就不用了。
2 有了方法。 方法就是程序，就是代码。无需自己重复编写。bat肯定是不行，没有方法，有也是个人写的，不可靠，不敢用。
方法可以是自己编写的ps函数，自己编写的ps类中的方法。
自己编写的方法，可以临时【并入】到第三方类中。
自己编写的方法，可以临时【并入】到.net类中。


问：面向对象的缺点是什么？
答：
1传教士在向用winxp的人传授powershell时。那人说，powershell不好，对象太占内存，他说的是对的。
cmd中我用dir返回100个文件名（字符串）。powershell中我用dir返回100个文件对象，powershell占用的内存多。
但今时不同往日：
1.1不必要的内容不要存在变量中。或者用完立马销毁，减少内存占用。
例如：
$a = dir 存放100个文件的目录  #返回100个文件对象，占内存多。
$a = (dir 存放100个文件的目录).name  #返回100个字符串，虽然省内存，但文件的属性方法也没了。


1.2内存大大滴够用了。因为cpu性能已经上不去了，我们正在疯狂加大内存，企图以空间换时间。
1.3我们更想要强大的功能，这年头面向对象是最基本的。py，php，java，.net，c++哪个不是面向对象的？

2.net虚拟机,运行慢的情况。
2.1 第一次运行慢。
2.2 刚开机运行慢。
这个问题在win7中存在，在win10中完全不存在了。
有计划任务，在计算机空闲时，定时循环优化虚拟机。
就好像大热天，你去饭店吃饭，叫瓶凉啤酒。python说我现给你冰镇。.net说我把一小时前冰镇的拿给你。
.net预先建立了线程池，用于加速代码。提前整理好了堆、栈、内存，用于加速数据。
这种优化是系统级别的，这种优化导致python永远达不到的性能。除非py也搞这么一个服务。


总结：
1对象比字符串粒度更大，更占内存。
2面向对象多了方法，功能更强。
3属性比字符串粒度更小，用起来极其方便。避免了【狂用烧脑正则去过滤】字符串！
4尽量不要在1000次以上的循环中，用管道。

===狂用烧脑正则去过滤例子，bat版的ping默认网关===
@echo off&setlocal enabledelayedexpansion
echo 正在查找默认网关...

for /f "usebackq delims=" %%i in (`ipconfig /all`) do (
echo %%i|find /i "gateway">nul||echo %%i|find "默认网关">nul
if "!errorlevel!"=="0" (
for /f "tokens=2 delims=:" %%a in ("%%i") do for /f "delims= " %%m in ("%%a") do set ipgate=%%m
)
)

echo 默认网关是:!ipgate!
===========ping默认网关.ps1============
$默认网关 = (get-netroute -DestinationPrefix 0.0.0.0/0).NextHop
& ping.exe $默认网关 

# Test-Connection $默认网关
=======================



问：什么时候应该用对象？
答：
需要方法，属性的时候。占95%。方法属性给了我们极大的便利。请看例子：


问：linux下用powershell统计文本行数，是不是这样写啊？
Get-Content xxx.txt | Measure-Object -Line
答：
$a = Get-Content xxx.txt #返回一个数组，数组有.count或.length属性 。
$a.length或(Get-Content xxx.txt ).length



问：什么时候，不需要使用对象？
答：
不需要方法，属性的时候。占5%，请看例子：

删除一个目录的需求。
用【rd /s 目录名】即可，没必要非用【Remove-Item -Recurse 目录名】

弹出u盘的需求。
用【mountvol 盘符: /d】即可。




问：即然面向对象这么好，那么这些对象都是从哪里来的？
答：从.net库中来。


---------- 第三章 .net 简介 --------------


问：.net 核心分为几个版本分支？
答：
目前是三个版本。
.net 2.0        最新版.net 3.51
.net 4.0				最新版.net 4.72
.net core 2.x		最新版.net core 2.2   苹果系统，linux系统，嵌入式系统。 .net core 2.3，3.0得2020年才能成熟。 



问：.net 有几个功能分支？
答：
桌面分支				在.net中。包含winform。用于开发桌面窗口。
声音库
asp.net				在.net和.net core中。web服务器功能库。用于开B/S的web服务器。
f#						在.net和.net core中。包含数学库，三角函数库等。
powershell		powershell本质是.net的分支。在.net和.net core中。包含脚本文件等常用系统管理接口。



问：.net程序（c#程序）如何连接mysql服务器？
答：
去mysql官网下载.net语言的连接器。
mysql-connector-net-6.9.9-noinstall.zip--->v4.5--->MySql.Data.dll
给.net增加 MySql.Data 类，增加了数据库接口。



结论：
必须安装最新版本的.net库。winxp的机子先安装.net 3.51，win7和win2008的机子，先安装.net 4.7以上。

.net已经存在很多年了，比支持.net的软件比支持java的少不了多少。所有.net的分支，接口（数据库，微信等。）
那些dll，那些类库，powershell都可以调用。和c#编写的exe完全相同。



问：.net兼容库都在哪里？？
答：
https://www.nuget.org/



问：除了.net库的分支接口，java库的分支接口，powershell自己的库（模块）都有什么呢？
答：
请看下一章

---------- 第四章 powershell常用的 内置库，外置库，第三方库 --------------

传教士帮白：
这章没法讲，只是罗列库和手册。把此章节收藏。走马观花地看了这些库，就知道powershell都能干啥了。



win2012手册地址：（最常用的ad模块）
https://docs.microsoft.com/zh-cn/previous-versions/windows/powershell-scripting/dn249523(v=wps.630)
ad用户组管理，dhcp，dns，打印机，文件共享，iis，磁盘，网卡，



exchange2016
https://docs.microsoft.com/zh-cn/powershell/module/exchange/active-directory/add-adpermission?view=exchange-ps
Active Directory 12	 
反垃圾邮件和反恶意软件 59  
客户端访问 100
扩展代理 4
电子邮件地址和通讯簿 37
联合身份验证和混合配置  31
高可用性  22
邮件流  85
邮箱  74
邮箱数据库  23
邮箱服务器  4
移动和迁移  43
组织  9
权限  30
策略和合规性  89
安全性  
服务器运行状况、监视和性能  
共享和协作  
统一消息  
用户和组  



sqlserver2014，2016，2017 
https://docs.microsoft.com/zh-cn/sql/powershell/sql-server-powershell?view=sql-server-2017



lync2015，skype
https://docs.microsoft.com/zh-cn/powershell/module/skype/?view=skype-ps




SharePoint2016
https://docs.microsoft.com/en-us/powershell/module/sharepoint-server/?view=sharepoint-ps



亚马逊虚拟机aws，
http://docs.aws.amazon.com/powershell/latest/reference/Index.html

微软虚拟机Azure，hyper-v，

vmware vSphere企业级的虚拟机。
https://code.vmware.com/web/dp/tool/vmware-powercli/11.0.0
https://code.vmware.com/docs/7336/cmdlet-reference

客户机：
服务，进程，日志，注册表，文件目录，远程管理。定时任务。



网络：
ftp，邮件，ssh连接linux服务器的客户端插件。


文本：
xml，html，cvs，json，excel等。


excel
https://docs.microsoft.com/zh-CN/office/vba/api/overview/excel


文本2语音


图形界面。


微软脚本中心
https://gallery.technet.microsoft.com/scriptcenter/


powershell软件源官网---powershell官方库。
https://www.powershellgallery.com


其他牛x库，都在github。另外，传教士群中定期发表【藏脚阁】之【牛x法宝】，都是好用的powershell第三方库。


---------- 第五章 入门必学必会 帮助命令的使用--------------

问：.net最新版本是多少？
答：
4.72


问：powershell最新版本是多少？
答：
win上，不和linux互联的话，是5.1版。
和linux互联，需要在win，linux上安装powershell core。最新版是6.1.x



问：如何升级powershell？
答：
1 对于win10，win2016，win2019你啥也不用做。
2 对于win7，win2008r2，win2012r2，你必须升级。
把.net升到最新版，即4.72。
把ps升级到最新版，即5.1。
升级文件，已经整理好，放在了群共享中。按照顺序安装1，2，3，4打头的软件即可。



问：powershell 6.x有啥新功能？
答：
6还在持续完善中，新功能我会在群里，不定期分享。
分享的时候都会带上一本书的样子，标明ps秘籍和版本。



问：谁应该用powershell 6.x？
答：
1 linux用户。或需要win-linux互联的用户。则必须用6.x版。
2 遇到ps5.1的bug的用户。具体问问群主，6是否fix掉了你遇到的bug。
3 发烧友，或想学新版功能的人。
4 除上面3点之外的，win用户，企业级用户，基本【不必要】安装，使用powershell 6.x。



问：如何看待powershell 6.x？
答：
1 6.x基本上可以认为是给linux用的。
2 powershell 6.x 增加了少许库，语法。变更了少许功能。修正了少许bug。
3 版本。目前来讲，使用稳定的6.1.x稳定版足矣。2019年底前，powershell 6.2.0稳定版能发布。但是建议使用2020年发布的6.2.3及以上的版本。
4 linux中的powershell 6.x最大的问题，是缺少库。
4.1 第三方库，基本是win，linux通用的。这样的库也越来越多了。
4.2 win中的很多好用的库，命令，还没有linux版。



问：如何知道powershell版本？
答：
$PSVersionTable



问：如何列出本地模块？
答：
get-module -ListAvailable


问：只知道命令的一部分，如何查找命令？
答：
get-command  *service*



问：知道命令，如何列出所有参数？
答：
get-help write-host -Parameter *
show-command write-host


问：知道参数，但不知道哪个命令有此参数，如何查找有此参数的所有命令？
答：
例子：想知道哪个命令有encoding参数，就用
get-command -ParameterName encoding



问：如何从命令行获取某命令帮助？
答：
get-help get-date

get-help get-date  -Examples		命令例子
get-help get-date  -online			在线手册




问：命令返回的对象里，有啥属性方法，如何得知？
答：
"abc"  | get-member
get-date | get-member



问：中文的.net类的手册在哪？
答：
msdn。最基本的字符串的属性和方法，的手册在。
https://msdn.microsoft.com/zh-cn/library/system.string.aspx



问：天天有分享，周周脚本题，的powershell学习研究群在哪？
答：
QQ群号=183173532
名称=powershell交流群


问：powershell 手册？
答：
QQ群号=183173532 ---》 群文件共享中  ---》 微软PowerShell2.0官方中文手册.chm


问：powershell学习分享网站？
答：
www.pstips.net


问：$()是啥？
答：
是一个无变量名的变量，偷懒了。没有变量名，你无法看到【变量名，和其中的值】，不好调试。
$()和()的作用基本相同。即括号内的表达式，优先计算。如此说来，这两个和linux的【 `xxx命令` 】的作用差不多。


问：$()和()有啥区别？
答：
有时候，某些泛型变量，某些属性，你不想用变量名保存，就得用$()。
你用(),只能返回类似于System.Collections.Generic，而不是值。

在bash中想省事，不想用变量名保存结果，而是直接输出计算结果。但是呢，累吐血也没算出来2+3
请看bash代码：
2+3
2 + 3
(2 + 3)
((2 + 3))
`2 + 3`

echo 2+3
echo 2 + 3
echo (2 + 3)
echo ((2 + 3))
echo `2 + 3`

eval 2+3
eval 2 + 3
而python，powershell算2+3无此问题。

在ps中，包括我，还是经常用这种偷懒方法的。
偷懒，和不偷懒，的对比：

$a = get-date
$a.day
====下面开始偷懒====
(get-date).day 或 $(get-date).day





问：$_是啥？
答：
1  $_ 是 xxx命令 | foreach-object {} 中的枚举。
2 $_是一个无变量名的变量，偷懒了。


问：传教士，你为啥不建议使用$_ ？
答：
偷懒节省变量名的意思是，全国10亿人，5亿叫张三，5亿叫刘德华。。。 把每个变量都放在，同一个变量名中，不好调试。
尤其是在两个管道，或更多管道的情况下。
请看：
新浪娱乐2018年7月13日讯，北京市第一中级人民法院发布了一则审判快讯，
案件为【军旅歌手乌兰托娅-蒙古族】，起诉，【《套马杆》原唱者乌兰托娅-蒙古族】公然使用其姓名，利用其知名度恶意盗用、冒用其姓名，要求被告停止使用其姓名并赔礼道歉、赔偿损失。
法院驳回了原告的诉讼请求。法院判乌兰托娅败诉，而乌兰托娅赢。结果乌兰托娅不服，又起诉，二审维持原判。


问：传教士你为啥不建议使用 | foreach-object {}
答：
1  用 | foreach-object确实很方便，我也用。但很慢，不建议在1000次以上的循环中用。
此乃鱼与熊掌不可兼得，切记！
2 在 | foreach-object {} 中使用break，会打断整个脚本。
3 在 | foreach-object {} 中使用使用return,会变成continue。
4 在 | foreach-object {} 中使用continue，会不管用。
5 如果必须用，就要在每个管道前后，分别调试。然后再组合。



问：传教士你建议用啥？
答：
foreach ($单个枚举元素 in $数组) { $单个枚举元素.xxx属性 }


---------- 第六章 常用命令的介绍 --------------

文件,目录对象介绍：
第一个要学的命令就是dir，powershell没有find。
问：为什么要用powershell的dir【即Get-ChildItem】，而不用cmd的dir？
答：
get-childitem d:\xxx  
-file  #过滤，只输出文件
-Directory  #过滤，只输出目录
-Hidden  #过滤，只输出隐藏
-Recurse #包含子目录
-Depth #目录深度




问：文件的常用属性是什么？
答：
$文件 = dir a:\pscode\temp183\aaa.txt
$文件.FullName   #全路径属性
$文件.name				#文件名和扩展名
.BaseName   #文件名
.Extension  #扩展名
.LastWriteTime #返回最后写入时间属性
.Length		#文件字节长度
.DirectoryName #父目录



问：如何测试文件，目录是否存在？
答：
test-path  d:\xxx\yyy.txt
test-path /xxx/yyy.txt
test-path /xxx/yyy  -pathtype Container  #测试是否有此目录
test-path /xxx/yyy  -pathtype Leaf  #测试是否有此文件



问：如何拆分目录，文件？
答：
Split-Path -Path "C:\Test\Logs\*.log" -Leaf -Resolve #返回所有文件名即
Pass1.log
Pass2.log

Split-Path -Path "C:\Test\Logs\*.log" 
返回：C:\Test\Logs\



问：如何合并目录，文件？
答：
1 join-path
2 直接用构造字符串的方法：
$目录名= '/root'
$目录名加文件名 = "$目录名/abc/def.txt"
#返回
/root/abc/def.txt



问：神马是文件，目录的-LiteralPath？
答：
不包含正则，通配符的。不会被正则转义的路径。和py的r'字符串'类似。
test-path  -Path e:\电影\[神秘博士][第十季]第6集_bd.mp4    #返回假，因为有[]
test-path  -LiteralPath e:\电影\[神秘博士][第十季]第6集_bd.mp4  #返回真



问：【基于字符的外部命令】，如何把返回值，按行为单位，分成数组？
答：
$a = @(ipconfig)
$a[8]  #第9行
$a,$b,$c = 1,2,3
$d = 1..9



问：如何把文件拆分成行？后放入一个数组？
答：
$a = Get-Content a:\pscode\temp183\aaa.txt -ReadCount 0


问：如何把一行拆分成单个字符？
答：
3种方法：
$行 = 'abcd汉字efg'
foreach ($行中提取单个字符的办法1 in $行.GetEnumerator())
{
    $行中提取单个字符的办法1
}

foreach ($行中提取单个字符的办法2 in $行.ToCharArray())
{
    $行中提取单个字符的办法2
}

for ($i = 0;$i -lt $行.length;$i++)
{
    $行.chars($i)
}


for ($i = 0;$i -lt $行.length;$i++)
{
    $行[$i] #支持负数
}



问：如何把【字符串】拆分成【数组】？
答：
一般用-split。复杂的用上述的for办法。





问：如何把【数组】合并成【字符串】？
答：
一般用-join



问：如何把【字符串】和【变量】进行合并？
答：
字符串和变量合并，需要双引号，或@""@。单引号不行，会把$转义。

$a = 1
$ab = 2
echo "xxx$abyyy" #无法判断是$a还是$ab。

可以用下列3种方法，来合并字符串和变量：
echo "xxx${a}byyy" 
echo "xxx$($a)byyy" 
"xxx{0}byyy"  -f $a 
echo ("xxx"+$a+"byyy")


问：你为什么要教这些方法？
答：
合并后的字符串。有可能传递给-f，convertfrom-string，进行下一步处理，
但是对此2命令来说，输入字符串若含有大话括号，需要转义，得改变源内容。




问：
$a = 1
$字符串 = "xxx${a}byyy" 
echo $字符串 #xxx1byyy
$a = 2
那么此时，$字符串的值是xxx1byyy，还是xxx2byyy ？
答：
是xxx1byyy，变量值变化后，原来组合的字符串值不变，你需要重新组合字符串。




问：打开一个文件，作为一个大字符串，存入整个一个变量？
答：
$a = Get-Content a:\pscode\temp183\aaa.txt -raw




问：
如何运行命令？
如何运行脚本？
脚本在.txt .cfg中，如何运行？
如何后台运行命令？

答：
在当前进程中运行，可以用：
a.ps1
get-content b.txt | Invoke-Expression

在子进程中运行，可以用：
古有cmd /c "命令 参数"
今有powershell /c  "命令 参数"  ,
或 powershell -c  "命令 参数" ,
或 powershell -command  "命令 参数" ,
linux中用： /usr/bin/pwsh -c "命令  参数"
父进程如果是powershell，就可以用大花括号：powershell -command  {命令} ,

不运行命令，而运行脚本的话，就用：
powershell -file  "d:\脚本.ps1"  -字符串参数1 '字符串a'  -数字参数2 1234
/usr/bin/pwsh -file '/tmp/a.ps1'

在【后台！】运行powershell.exe，或其他exe：
start-process -path 你的任务.exe -ArgumentList '-你的参数1 aaaa  -参数2 1234'

注意：运行ps命令或脚本，没必要通过cmd来调用。直接这样用即可：
操作系统（或你的进程中）---运行--->powershell.exe----->运行ps命令和ps脚本。







问：我想用另一个本地用户运行脚本，但powershell没有runas。exe 类似的命令咋办？
答：
powershell中有各种session呀。
ip+端口+用户名+密码=一个session，我只需更换用户名，更换密码，就可以更换权限。因为权限绑定在用户上。
同理，我只需要建立n个session使用，无需切换用户。
最主要的new-pssession，中有-Credential参数，输入用户密码，这不是跟runas。exe一样么？还有什么SmbSession。
所以我觉得powershell没有必要用runas。exe。
你只要用那些带session，带Credential的命令即可呀，对不？

查看参数名中，含【Credential】名的命令：
get-command -ParameterName Credential

查看命令中，含【session】字符的命令：
get-command *session*


问：如何用powershell发邮件？
答：
$附件 = Get-ChildItem '/tmp/aaaa.tar.gz'
$HTML邮件内容 =
@'
<p>
	<span style="font-family:Microsoft YaHei;font-size:18px;">html信件内容</span>
</p>
'@

Send-MailMessage   -Subject "主题"       `
-From  "你的hotmail账户@hotmail.com"   -To  "你的qq邮箱@qq.com"   `
-SmtpServer   "smtp.live.com"  -Port 587  -UseSsl    -Credential  "你的hotmail账户@hotmail.com"  `
-Attachments $附件 -BodyAsHTML -body $HTML邮件内容


上面的代码，保存成带有bom头的a.ps1文件。
win中用：
powershell.exe -file d:\你的目录\a.ps1 

linux中用：
/usr/bin/pwsh -file /你的目录/a.ps1 


注意：
1win，linux中的powershell中用Send-MailMessage发邮件，需要免费email账户，无需自建smtp服务器。
2登录QQ的smtp服务器，默认被关了，需要在web设置中开启smtp。
3登录QQ的smtp服务器，用xxx@QQ.com + 你的qq密码 + 上述命令 发邮件是不行的。因为为了qq密码安全，腾讯要求独立的邮箱密码。  
4win7自带ps2.0。而3.0和以上版本才支持port参数。总之1升级到.net最新版4.72升级ps到最新版5.1。 
更多参数，详见手册：
https://docs.microsoft.com/zh-cn/powershell/module/Microsoft.PowerShell.Utility/Send-MailMessage?view=powershell-5.1

5现在各大运营商，提高了发邮件的门槛：
5.1win，linux，黑客软件中搭建出来的“黑smtp服务器”，都被阻拦了。
5.2买个域名，并对此做个MX解析。“就不会被当作垃圾邮件的时代”也过去了。买域名太容易，建黑客网站太容易。
5.3运营商只对【大email服务提供者】，【ip建立白名单】。






问：监控win cpu，磁盘，网络，io等。
答：
性能监视器或
Get-Counter 从本地和远程计算机上获取性能计数器数据。

问：如何查看有哪些计数器项目？
答：
都是手册上的东西。
查有哪些大类用：
Get-Counter -ListSet * | Sort-Object CounterSetName | Format-Table CounterSetName


比如我现在已经知道是磁盘大类是（PhysicalDisk)了，再查磁盘中有那些小类，用：
(Get-Counter -ListSet PhysicalDisk).Paths




问：如何查看日志？
答：
事件查看器，或
get-eventlog



问：如何执行字符串？
答：
$cmd1 = 'xxxx'
Invoke-Expression $cmd1



问：powershell是否支持winxp？win2003？
答：
是。
1安装.net3.5 并重启，必要。
2安装.net4.0 。非必要。
3安装powershell最新版的2.0。
具体见群共享。



问：powershell传送文件，有哪些方式？
答：
http方式：Start-BitsTransfer  winscp的webdav
ftp方式：winscp（支持文件同步）
sftp方式：winscp（支持文件同步），Posh-SSH模块
sshfs方式：严格来说，也属于上面。但毕竟有了盘符目录，比上面的感觉简单。
文件共享，samba方式：copy-item，robocopy（支持文件同步）
iscsi方式：使用用户名+密码，影射某个ip上的，iscsi磁盘后，copy-item
微软官方的，powershell remoting+Just Enough Administration 引擎：copy-item -tosession -FromSession 
https://msdn.microsoft.com/zh-cn/powershell/wmf/5.1/jea-improvements
在 Windows 7 上使用 JEA 时，虚拟帐户仍不受支持。

第三方的 powershell remoting：
https://github.com/pldmgg/misc-powershell/tree/master/MyModules/WinRM-Environment
中有Receive-ItemFromRemoteHost，Send-ItemToRemoteHost，用于传文件。

另外有人提出了【cmd+psexec】，我看了一下，本质上是【用命令，跑到远程机子上，调用net share建立共享。】
道理和文件共享，samba，是一样的。
高版本win中【命令】和【作用】都有替代的ps命令，顾【cmd+psexec】在低版本win上或许是鸡头神器，
而在powershell脚本大帝的宫殿（即高版本win）中，只能是孤单躺在角落中的凤尾花瓶。

powershell dsc：中的file模块，xrobocopy模块。


问：什么是命令交互？
答：
简单理解为，服务器 《——————》客户机 之间聊天。特色是：
长连接+交谈

ssh在没有except的情况下，也是和ps一样，不支持交互。



问：有哪些交互命令？
答：
ftp，nslookup，telnet等。





问：powershell服务器，客户机之间，（命令，变量）交互，交谈，控制，有哪些方式？
答：
所有这些都是通过，叫通ip，端口，用户，密码来访问。
1 老的。wmi+psexec。
2 ssh。
3 ps-remoting。
4 powershell-web-server。 基于浏览器的b/s方式。









那么好，单个命令我们已经学会不少了，下面我们来看powershell脚本的执行。


---------- 第七章 ps1脚本编写，调试，运行 --------------
脚本是命令语句的组合和叠加。脚本就是胶水，四处去找别人调用，四处找轮子组装汽车。而不是做轮子，给别人用。



菜鸟问：如何写脚本？
老鸟答：
1 必须搞清楚问题细节。例如：做月饼。
2 解题思路也基本完成。面粉和水，放入馅，蒸。老司机=先有解题思路后开车，新司机=路没搞明白，四处瞎撞，乱折腾。
3 使用什么命令，变量。加五仁，放入模子，挤压。
4 先粗写，写个大概。最好有旧代码可以抄。
5 调试通过。
6 详细写。考虑出错情况，加上错误代码，错误信息。去掉容易出错，不容易兼容的代码。改写性能不佳的代码。
到这一步为止，好的脚本可能不好看，但该的很好用了。
7 精雕细琢。重构，把重复使用的代码段，写成函数。重写变量名，使人能一眼看懂。格式化好代码，搞好缩进。


问：powershell最普遍的问题是什么？
答：
1经统计，大概有40%问题，是由于低版本的bug引起的。
所以说提问之前，应升级.net版本到最新的v4.72。升级ps版本到最新的5.1。这些文件群共享都有。
就因为你懒惰，不升级，遇到了bug。你提问，大家再研究，最后发现是由于没升级造成的。
需要花费10倍的时间和精力！！！花费这些时间和精力，是毫无必要的！

2经统计，大概有30%问题，是由于win7，win2008，没有命令和库引起的。win7将被淘汰，微软不给win7发布新库，我也没法子。
所以说提问之前，尽量升级到win10。

3大概40%的问题，都是以前分享，解决过的。请珍惜群友身份，必须注意看已经分享过的内容！





问：编写ps1用什么ide？
答：
最最推荐使用visual studio code，加上powershell插件。
特色：
语法提示，命令提示，参数提示。自动完成，代码格式化，缩进选择空格还是tab，文件编码设置。
有插件名叫ftp-sync，可以在win的vscode中编写ps1脚本，保存时，自动同步到linux目录中。


ise，powergui：
这两个和vscode相比，无语法提示。有命令、参数提示。简称【瘸了1条腿】


不建议使用：
这3个和vscode相比，无语法提示，无命令提示。简称【瘸了2条腿】

nodepad++       只有代码高亮，颜色差。
Sublime Text    只有代码高亮，颜色差，高亮关键字过时。
atom            只有代码高亮，颜色差。  





问：调试ps1用什么工具？如何单步运行脚本？如何在脚本的某行上，下断点？如何在图形界面中观察变量的值？
答：
win上建议使用powergui调试。生平不用火车头，纵然英雄，ps脚本也蹦吧报错！
linux上只有一个调试工具即vscode。



问：如何在powershell.exe中，边执行，边观看脚本调用过程，并显示变量值？类似于sh -x 那样？
答：
1 在powershell.exe中敲入命令：（放在脚本的第一行也行，第n行也行，放哪就从哪显示）
set-psdebug   -Trace  2
2 运行脚本。


问：如何脚本中，关键语句后，进入调试状态？
答：
1+2 #关键语句
Wait-Debugger #作用：1+2 执行完毕后，进入调试器。用exit退出调试器。
3+4 #后续语句







问：代码格式化，用什么工具？
答：
该缩进的都缩进，等号都对齐。
建议用powershell ise + ise 插件 【ISESteroids】

安装：
Install-Module -Name ISESteroids

ise中运行：
Start-Steroids





问：让代码颜色漂亮，用什么工具？
答：
1 用上面的工具把代码格式化好。
2 用群共享中，powershell_ise目录下，传教士diy的配色2016版。
3 抓图。世界上最赏心悦目，颜色漂亮的powershell代码产生了。

上述ide全都是中文的。




问：如何使用powershell-ise？
答：
1 不建议在ise中，编写脚本。没有语法提示。建议用vscode编写脚本。
2 不建议在ise中，调试脚本。不会清空上次的变量，导致问题。建议用powergui调试脚本。
3 用了【传教士diy的，ise配色2016版】后，建议在ise中，看代码。颜色好。
4 用了ise插件【ISESteroids】后，建议用ise格式化代码。
5 建议在ise中看命令帮助，即ise右上角的按钮。




问：如何给脚本起名？xxx.ps1
答：
建议用2---3个字母打头，剩下用中文文件名。即【bf备份所有旧文件_并删除10天前的.ps1】
这样先打【bf】，然后再打tab即可补全脚本名。


问：.ps1脚本，应该保存成什么编码？
答：
bom头+utf16le编码。或bom头utf8编码。
ps1脚本中，支持中文变量名，中文参数名，中文函数名等。
在普通电脑上，使用记事本，保存成unicode即可。
建议使用vscode保存，方便设置编码类型。


问：脚本中，一行太长怎么办？
答：
1一行尽量只有一个表达式。
2命令行太长，可以用放在行尾的【1左面的`符号】折行。并把相关的参数放在同一行。请看：
new-vm  -cpu 2核   -内存 1000mb  -磁盘 10gb  `
-内网ip 1.1 -外网ip 2.2    `
-系统 w2016  
3运算符号后面，无需加`即可折行。
如：
1+
2

如：
get-process notepad |
stop-process





问：如何开启powershell脚本运行权限？
答：
echo 下面代码，在管理员权限cmd中运行，在管理员权限powershell中运行均可。
echo 如果使用powershell remoting远程。本机，远程机，都要用管理员权限运行一遍。
"C:\WINDOWS\system32\windowspowershell\v1.0\powershell.exe" -command "Set-ExecutionPolicy -ExecutionPolicy Unrestricted"
"C:\WINDOWS\syswow64\windowspowershell\v1.0\powershell.exe" -command "Set-ExecutionPolicy -ExecutionPolicy Unrestricted"
& "C:\WINDOWS\system32\windowspowershell\v1.0\powershell.exe" -command "Set-ExecutionPolicy -ExecutionPolicy Unrestricted"
& "C:\WINDOWS\syswow64\windowspowershell\v1.0\powershell.exe" -command "Set-ExecutionPolicy -ExecutionPolicy Unrestricted"
pause



问：火车头（powergui）有什么缺点？
答：
无法设置背景颜色。



问：你所使用的，vscode模块有哪些？
答：
powershell，vscode-icons，sftp



问：你所使用的，vscode配置文件内容是什么？
答：
文件位于：
C:\Users\你的用户名\AppData\Roaming\Code\User\settings.json
{
	"editor.fontFamily": "Microsoft YaHei Mono",
	"editor.fontWeight": "bold",
	"editor.fontSize": 25,
	"editor.tabSize": 4,
	"editor.insertSpaces": false,
	"editor.emptySelectionClipboard": false,
	"window.title": "${activeEditorLong}",
	"files.encoding": "utf16le",
	"files.eol": "\r\n",
	"files.defaultLanguage": "powershell",
	"window.reopenFolders": "all",
	"editor.formatOnSave": true,
	"editor.formatOnPaste": true,
	"editor.formatOnType": true,
	"editor.wrappingIndent": "indent", //回车后缩进
	"editor.renderIndentGuides": true, //显示缩进竖线
	"files.trimTrailingWhitespace": true, //保存时去除行尾空格
	"powershell.codeFormatting.openBraceOnSameLine": false, //大花括号后换行。
	"powershell.codeFormatting.newLineAfterOpenBrace": true, //大花括号后换行。
	"powershell.codeFormatting.newLineAfterCloseBrace": true, //大花括号后换行。
	"powershell.codeFormatting.whitespaceBeforeOpenBrace": true, //大花括号左面插入空格。
	"powershell.codeFormatting.whitespaceBeforeOpenParen": true, //圆括号左面插入空格。
	"powershell.codeFormatting.whitespaceAroundOperator": true, //运算符之间插入空格。
	"powershell.codeFormatting.whitespaceAfterSeparator": false, //逗号，分毫后插入空格。
	"powershell.codeFormatting.ignoreOneLineBlock": false, //if true,单行中的if else 不会被格式化。
	"powershell.codeFormatting.alignPropertyValuePairs": true, //哈希表中等号对齐
	"powershell.codeFormatting.preset" : "Allman", // if else 格式化样式
	"workbench.colorTheme": "Monokai",
	"powershell.integratedConsole.showOnStartup": false,
	"terminal.integrated.shell.windows": "C:\\Windows\\Sysnative\\WindowsPowerShell\\v1.0\\powershell.exe",
	"terminal.integrated.fontSize": 22,
	"terminal.integrated.cursorStyle": "line",
	"terminal.integrated.cursorBlinking": true,
	"workbench.iconTheme": "vscode-icons"
}



问：如何使用，带有插件的，绿色版vscode？
答：
下载zip版本，并设置相关目录。详见这里：
https://code.visualstudio.com/docs/editor/portable


问：如何使用vscode在linux中调试powershell脚本？
问：如何在linux中，安装vscode。并在win中远程使用？
问：如何在linux中，单步执行，断点执行，powershell脚本？
答：
1在linux中安装vscode。
https://code.visualstudio.com/docs/setup/linux

sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo yum install code
mkdir ~/vscode

2 如果你喜欢用linux桌面。则安装linux虚拟机 + 图形界面，如gnome。
vscode窗口显示在，linux虚拟机的桌面中。

3 如果你喜欢用win桌面。可以使用win + x11图形软件。
也就是说win加，linux虚拟机（建议至少2~3GB虚拟机内存）加，linux版ps（或c++，php等你的开发语言），加linux版vscode。但是【linux版vscode窗口】显示在win中。
经我测试，xmanager5不灵。但是vsxsrv这软件可以，而且配置简单。

官网：
https://sourceforge.net/projects/vcxsrv/

3.1 下载安装vcxsrv，运行XLaunch。

3.2 选multipe windows ---》start a programe ---》start programe on remote computer。
在“remote programe”输入框，输入：
code --user-data-dir="/root"

在“Connect to computer”输入框，输入：
你的linux的ip地址

在“login as user”输入框，输入：
你的linux账户名，如root

在“password”输入框，输入：
你的linux密码

下一步 ---》保存 ---》文件名为：vscode.xlaunch

3.3 双击“vscode.xlaunch”文件，这是一个xml文本文件，选文件关联，关联给XLaunch。以后双击此文件，即可运行vscode。

3.4 成功看到vscode英文窗口。此时注意win防火墙，允许XLaunch通过。vscode中安装模块，重新运行，则变成中文vscode。




问：vscode有什么缺点？
答：
调试功能慢，有时死锁。
没有工具栏，没有按钮
代码格式化，有不少格式坏的地方。



问：vscode有什么常用快捷键？
答：
ctrl + k，然后ctrl + 0 #折叠代码。不展开所有，大花括号。
ctrl + k，然后ctrl + c #行注释
ctrl + k，然后ctrl + u #除掉行注释
点中变量名后，ctrl + shift + l #一次性修改所有变量名
选中n行后，shift + alt + a #块注释，再按取消



问：ise有什么缺点？
答：
无法选择编码保存，转换编码。
缩进为【空格】，【tab】两者都有。在其他文本编辑软件中，显示缩进错乱。不能显示缩进格式是tab，还是空格。
状态栏中没有编码，回车说明。
脚本执行完毕后，变量值没有清空。



问：编写脚本有什么忌讳？
答：
忌讳一行流，把所有东西都往一行塞。尤其是初学者。
程序本来就是【把问题无限拆分，拆到足够小，足够简单，并解决】的过程。
写5行代码，比写1行代码，简单5倍，甚至10倍。
建议把表达式尽量拆分开，用多行。每行用最短的，最简单的表达式。
这样方便调试，也方便插入删除代码。

我发现即使使用【狂拆行流】这样，小脚本也大都10---30行。
ps函数大都30-50行，超过50行的函数不多。
ps脚本大都100-200行，超过200行的脚本不多。

【狂拆行流】能让菜鸟迅速成为【脚本大师】，
而【一行流】就是在菜鸟进步路上的【坑爹瘪三】！爹都得被坑，何况菜鸟？

当然了，菜鸟如果进步成熟手后，可以在【狂拆行流】的基础上进行合理的组合。
使脚本每个步骤逻辑清晰。



问：给脚本传参数，有什么忌讳？
答：
如果输入数据是数组，那么尽量编写拆分数组的脚本。
把数组拆分成为一条数据后，存放于数据库，文件，csv文件，文件流等地方。

拆分数组代码，和只干活代码一定要分开。分为一个脚本中的两段代码，或两个脚本。

只干活脚本，只接受一条数据。不建议接受数组。
只干活脚本，不建议参数太多，如超过20个
只干活脚本，不建议参数太大，如超过xxMB
只干活脚本，很容易实现多线程并发，多进程并发。从而达到占用多核cpu，多io。

脚本想要模块化，尽量拆分成【读取】，【拆分】，【传输】，【处理】，【传输】，【写入】等部分。

---------- 第八章 实战 演练 --------------
群友6504748，自己编写这部分。

5、实例一：开启和关闭服务
6、实例二：控制防火墙（打开关闭，规则）
7、实例三：设置策略（密码策略为例）



---------- 第九章 这些额外的选学课 你感兴趣吗？--------------
powershell脚本，命令行参数传值，并绑定变量的例子
http://www.cnblogs.com/piapia/p/5910255.html




让powershell同时只能运行一个脚本（进程互斥例子）
http://www.cnblogs.com/piapia/p/5647205.html



powershell字符界面的，powershell加WPF界面的，2048游戏
http://www.cnblogs.com/piapia/p/5531945.html


powershell中的两只爬虫
http://www.cnblogs.com/piapia/p/5367556.html



PowerShell脚本：随机密码生成器
http://www.cnblogs.com/piapia/p/5184114.html



powershell 递归 算法 的例子
http://www.cnblogs.com/piapia/archive/2013/01/29/2881011.html



【PowerShell语音计算器】
http://www.cnblogs.com/piapia/archive/2012/10/20/2731506.html



1 列出所有efs加密文件。2解密所有efs加密文件
http://www.cnblogs.com/piapia/p/4702514.html
是为系统管理员，网管员编写的工具。
某员工离职后，他的磁盘假设有一万个文件（目录），其中efs加密的文件目录有3个。资源管理器中，这三个文件是绿色的。
但你要是（一万个目录）挨个点开看，是不是绿色，要累死。
这时网管用员工的win账户，登录员工ｐｃ机，用此脚本，即可列出所有ｅｆｓ加密文件。


---------- 第十章 请提问--------------
各位卿家，有事启奏，无事退朝。



----------第十一章 linux篇--------------
既然win中有了bash，那linux中有powershell也很正常，合理竞争，是件好事，受益的是用户。你想不竞争也不行。有摩擦正常，看开些。
win只有图形优势，而linux命令行不是比win命令行强大很多吗？你怕啥呀？





powershell比bash的优势总结：
1本地ps命令之间，ps函数之间，管道之间，基于ssh的远程【传对象值！】而不是字符串。甚至和数据库，图像接口之间，对象直传。
1.1用ps时可选择内存对象（如stringbuilder，arraylist，各种集合）作为缓存。
多线程还可以选择【线程安全型变量】，性能佳。丰俭由人，更灵活。而awk是个黑盒，无法操控。

2多线程方面。现有多线程，计时器。将来会有workflow多进程，使开发简单高效。
3转义符设计的比bash，python好。有面向对象方法，转义好。下详。
4支持csv，xml，json等。支持的数据格式比bash多。
5有where-object，group-object。分组筛选功能强，不用自己编码，这条算吗？
6容易学，容易改，算吗？ps语句简单标准，比bash脚本容易看懂。方法的使用，比烧脑正则容易学。
7ide中文，功能强，算吗？极大提高脚本编写速度。
8ps的语言内置的，调试功能强，算吗？

9linux癌症。
9.1 部分linux命令有【回车符】支持不全的问题。ps支持cr，lf，crlf。
9.2 linux中有数据对齐的癌症，ps中没有。下详。
9.3 面向字符脚本，必须要扣字符串，这是癌症。而面向对象脚本不用，完成同样的功能太省事了。如curl和Invoke-WebRequest
当然，现在linux中的ps命令，还不全，将来会越来越全。

10linux中就别用中文？即使在linux中，ps对中文的支持也和win中一样。你敢不赞？
10.1引号：支持中文单双引号，作为引号。
10.2空格：设置为空格，tab键，全角空格，都能正确运行。----bash无法识别中文空格，即全角空格。 
10.3支持中文函数名，中文变量名。
10.4 findstr,grep都不支持编码。select-string有-encoding参数。凡是和编码，中文相关的问题无忧。

写这些的目的：
有些懂.net的程序员进入linux，他们不懂linux命令行，或许会觉得linux命令行多么神器+先进。
我写这些就是想告诉他们，linux命令行是真落后，.net才最牛。


传教士道：只要能装上powershell的linux版本，只需要ps1脚本，不需要sh脚本。
解释：
1 简单来讲，bash中只有语法，没有命令和库。
2 bash只有1%的语法功能，powershell实现不了。这很正常，世界上没有两片叶子是完全一样的。
这意味着你只需要ps1脚本，不需要sh。
3 bash太老了，同样的功能，powershell都能实现，还能省时间，如万个空for，powershell要节省90%的时间。
4 即学用/usr/bin/powershell 代替/usr/bin/bash。其他linux命令，管道，旧的功夫等，用法完全和在bash中一样。
5 逐渐用面向对象的，简单强大的，powershell命令和库，代替烧脑的linux命令，或者两者都用。---这是总的原则，总纲。



问：目前哪些linux能安装上powershell？
答：
◦Windows 10 IoT Core(arm32的cpu，本质上是win，树莓派硬件上的win10) 
◦Raspbian Stretch(arm32的cpu，树莓派官方操作系统Raspbian，基于大便，所以叫树莓便。）
◦MAC OS X 10.11
◦Ubuntu 14.04/16.04/18.04
◦Debian 8.x/9.x 
◦CentOS 7.x/RHEL 7.x/Fedora26及更高版本
◦open SUSE 42及以上/SUSE Linux Enterprise Server 12 SP2及以上
◦Docker。LINUX发行版中，安装容器dockerd，docker中运行powershell。
◦Arch Linux （arch linux 没有版本号）
◦Linux AppImage 容器(portable application single binary)  https://github.com/probonopd/AppImageKit
◦Kali Linux
◦alpine Linux       这是docker专用的，轻量级linux发行版

安装方法：
https://docs.microsoft.com/zh-cn/powershell/scripting/setup/installing-powershell-core-on-linux?view=powershell-6



问：目前哪些linux，可以通过snap包方式安装powershell？
答：
◦Arch Linux/Fedora/elementary OS/OpenSuSE/Solus/Gentoo Linux/Debian/Linux Mit/Manjaro/OpenEmbedded/Yocto/OpenWrt/Raspbian等任何支持snap包的发行版

安装方法： （建议使用预览版，功能比较新，也没啥不稳定的）
snap install powershell –classic   #安装稳定版
snap install powershell-preview –classic #安装预览版



centos7及以上，安装powershell:
curl -o /etc/yum.repos.d/microsoft.repo  https://packages.microsoft.com/config/rhel/7/prod.repo 
sudo yum remove -y powershell #删除旧版 
sudo yum install -y powershell
pwsh -c 'mkdir -p "$env:HOME/.config/powershell" '
pwsh -c 'Add-Content  -Value "Set-PSReadlineOption -EditMode Windows" -LiteralPath $profile '
pwsh -c 'Add-Content  -Value "`nSubsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile" -LiteralPath /etc/ssh/sshd_config '



ubuntu1604：
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/16.04/prod.list
sudo apt-get update
sudo apt-get remove -y powershell #删除旧版 
sudo apt-get install -y powershell
pwsh -c 'mkdir  -p  "$env:HOME/.config/powershell" '
pwsh -c 'Add-Content  -Value "Set-PSReadlineOption -EditMode Windows" -LiteralPath $profile '
pwsh -c 'Add-Content  -Value "`nSubsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile" -LiteralPath /etc/ssh/sshd_config '


ubuntu1804：
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
sudo apt-get update
sudo apt-get remove -y powershell #删除旧版 
sudo apt-get install -y powershell
pwsh -c 'mkdir -p "$env:HOME/.config/powershell" '
pwsh -c 'Add-Content  -Value "Set-PSReadlineOption -EditMode Windows" -LiteralPath $profile '
pwsh -c 'Add-Content  -Value "`nSubsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile" -LiteralPath /etc/ssh/sshd_config '



debian9：
sudo apt-get update
sudo apt-get install curl gnupg apt-transport-https
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list'
sudo apt-get update
sudo apt-get remove -y powershell #删除旧版 
sudo apt-get install -y powershell
pwsh -c 'mkdir -p "$env:HOME/.config/powershell" '
pwsh -c 'Add-Content  -Value "Set-PSReadlineOption -EditMode Windows" -LiteralPath $profile '
pwsh -c 'Add-Content  -Value "`nSubsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile" -LiteralPath /etc/ssh/sshd_config '


for alpine 3.8 linux的，powershell core 6.1 正式版，发布啦！
同时
基于alpine 3.8 发行版的，powershell docker image，发布啦！

目的：
从【基于alpine发行版的，container中】，用powershell，
管理宿主机上的文件，
管理宿主机上的进程，
甚至
管理宿主机上的docker 容器，
管理宿主机上的docker image，

用法：
在宿主机上：
mkdir /powershell
docker run -it --pid=host -v /powershell:/mnt    mcr.microsoft.com/powershell:alpine-3.8
然后用powershell命令，读写container中 /mnt 下的文件即可。



问：大家都在哪些linux发行版，版本中，用powershell？
答：
根据从微软powerbi网站得来的统计结果。比例不含win，只含linux。
https://msit.powerbi.com/view?r=eyJrIjoiYTYyN2U3ODgtMjBlMi00MGM1LWI0ZjctMmQ3MzE2ZDNkMzIyIiwidCI6IjcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0NyIsImMiOjV9&pageName=ReportSection5

1redhat7/centos7。占比25.35%
2ubuntu。占比44.42%
3debian。占比13.77%
这3种占83%




问：为什么说win的命令行powershell，已经比linux强？
答：
1 win中的命令已经进化成面向对象的powershell。linux还不行。从win7开始，到win2012r2为止，进化结束。

2 从前我听说unix，linux命令多，很强大。但现在我告诉你，powershell命令比linux命令，至少多十倍。反正我这辈子是学不全了。

3 linux的更依赖图形，命令太少。而win命令比linux多很多。
3.1 linux中任何一款，邮件服务器中的命令，比exchange多，比exchange全？比exchange方便？
3.2 linux的dns服务器bind，不如win的dns命令方便。bind有给某个域中，域名添加ipv4的a记录的【命令】吗？还不是依赖web图形？
有人说用nsupdate。那还不是搞个文本，再运行文本。和用sed替换【dns区域文件】，然后在reload【dns区】有何区别呢？

4 新版win中，或者说是powershell中，都是【撸命令+参数】。而linux大都还在【sed撸文本】。
4.1 以给网卡配ip为例。
nmcli connection add type ethernet con-name NEW_STATIC ifname eno1234567 ip4 192.168.1.111 gw4 192.168.1.1，
不比用sed撸ifcfg-eth0文件方便么？

5 任何语言都要处理数据，脚本也一样。powershell有了对象的帮助，处理起数据来，比awk更得心应手。神马csv，excel，xml，json
sql表，nosql表。html等。
6 powershell用本地对象，远程对象带来了简单强大。并不是要替换linux所有命令，某些命令不返回数据，用powershell用linux命令雷同。
用哪个其实无所谓，况且linux下powershell可能命令不全。你是为了简单强大，不必为了powershell而powershell。




问：powershell如何实现【sed -i "s/要查找的内容/替换成/g" 文件名】？
答：
即打开文件，替换，保存文件。下列命令，测试通过：
$f = '/etc/selinux/config'
@(Get-Content $f) -replace 'SELINUX=enforcing','SELINUX=disabled' |Set-Content -path $f



问：为什么说linux中，用sed人越来越少了？
答：
论点1：awk可以代替sed，但sed不能代替awk。
sed即，简单查找替换。awk有for之类的可以实现复杂处理。

论点2：awk用的是标准正则，sed的正则和sed部分相同，部分不同。
学了sed就代表脑中两套不兼容的正则标准相互打架。

论点3：sed一行流代码很天书，难写，他人难改，难调试。为了少打几个字不值得。

论点4：多年以前，以【天书为原则】的perl，和【以简单为原则】的python不相上下。
现在perl被评为最令人讨厌的语言。市场占有率也不行了。




问：那么说学awk就对了？
答：
学powershell比学awk简单。
powershell用【split再split】，【if再if】，where-object，string.substing(),string[-3]等。
把字符串问题层层分解。比awk正则简单。




问：powershell中可以使用管道和awk吗？
答：
powershell中完全可以调用awk，和bash中完全相同。旧的武功，完全都灵。



问：用powershell的话，如何实现【awk '{print $3}'】功能？
答：
($行 -split "\s+|\t+")[0]  #第1列
($行 -split "\s+|\t+")[2]  #第3列	

Get-Content /xxx/yyy.txt | foreach-object {$_.split()[2]}    #awk '{print $3}'


问：用powershell的话，如何实现【awk -f a.awk file】功能？
答：
本质上，这是一个使用了管道的过滤功能。在powershell中，这叫做【过滤器】或者叫【筛选器】。
而powershell支持命令+管道+过滤器的组合。如 命令1 | 过滤器1 | 命令2 | 过滤器2 | 过滤器3
filter 过滤器1 
{
这里写入n行代码，实现类似awk的功能
}


问：awk，sed的癌症是什么？
答：
xml，或html。 ------------这是别人总结的，我只是转帖。他说：
文本包含HTML代码，用awk、sed 等工具时，就需要考虑极其复杂的转义等情况，出错概率很大。还不如用c自己从头搞。






问：powershell中有【xargs】吗？
答：
没有。
管道中使用的pipe变量名为：【$psitem】，它的别名为【$_】。
powershell用foreach-object和$_，来实现xargs的功能。这比xargs好很多，请看：

论点：
1管道前后直接传递数组，比字符串容易。无需切割。
2传递属性，比数组简单。

论据和说明：
假设我用ls |xargs 会返回5个文件，我分别取文件名和长度。这实际上是 5x2 个行列数组。我要使用这个二维数组中的数据。
第一维数据，xargs会切割每行出来5。第二维数据，xargs默认-d'\n'，切割空格用xargs -d' '。
而ps无需切割字符串，直接出数组。
$a = @((1,2,3),(4,5,6))
$a |ForEach-Object { $_[0] } #输出1，4

同理，Get-ChildItem | ForEach-Object { $_.name } #输出5个文件的文件名。




问：powershell中有【<】【<<】【<<<】号吗？
答：
没有。
或许从右到左的【<】符号反人类思维。powershell很多命令都给他改成了从左到右的。
如get-random < (1..100)在powershell中不合法，合法的应该是get-random -inputobject (1..100),或1..100 |get-random
只有不到1%的奇葩命令【必须】依赖【<】符号，这时可以通过在powershell中调用cmd，或在linux版powershell中调用bash来实现。
如$a = bash -x "命令1 < 命令2" #linux
如$a = cmd -c "命令1 < 命令2" #cmd





问：如何从win客户机的powershell中，经ssh协议，连接到linux的sshd服务器的bash中？
答：
用powershell + 第三方ssh客户端库PoshSSH（install-module PoshSSH即可） + ip + 端口 + 用户名 + 密码，组合成一个连接，并向这个连接发命令。代码如下：
$连接1 = New-SSHSession -ComputerName 1.1.1.1 -Port 22 -Credential aaaa  #将提示输入密码
$要返回的内容 = Invoke-SSHCommand -Command {cat /etc/issue} -SSHSession $连接1
$要返回的内容


问：经过ssh协议连接的，服务器，客户端，【都】是powershell有何好处？
答：
1好处是可以直接传输对象，无需经过序列化步骤。（对象--->转化为类似于json字符串--->传输到远端--->字符串转会对象）。
假如远程shell是bash，则连接用字符串，ps门派的【面向对象武功】全都废了。
2多线程。后台线程跑，不占用当前线程。而linux的ssh连接，是多进程的。
2.1对于100个以上的任务，多线程能省很多内存，即ps更适合大批量任务。
2.2对于100个以上的任务，多进程切换代价高。
比如每隔10秒，给100个线程分发任务，让线程去联网干活。
如果用主线程sleep 10，然后再告诉线程，第1个线程得到任务的时间，和第100个差不多。时间比多进程准。
3我们可以随时从session中【半路断开跑出来】，执行别的ps代码，函数，还可以【随时回session中去】。脚本写起来更灵活，调试方便。
4session带来了多个用户，不同的用户可以有不同的服务器权限。
5强大的powershell JEA。（正在开发实现中）



问：如何从客户机的powershell中，经ssh协议，连接到sshd服务器的powershell中？
答：
服务器端：
指定默认shell为powershell即可。具体：
	linux：
		1在linux服务器端，安装powershell。
	  2编辑【/etc/ssh/sshd_config】文件。加入下列行
		PasswordAuthentication yes
		Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
		后，重启sshd服务器。
	win：
用openssh。帮助在：   https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShellCommandOption -Value "/c" -PropertyType String -Force


客户机端：
	win，linux：
		安装powershell6.0后，多了-HostName参数，-UserName参数，用于连接sshd。
$连接2 = New-PSSession -HostName 1.1.1.1 -UserName root  #手动输入密码或用-KeyFilePath 选项
#注意 ：从安全的角度，不支持保存密码+自动登录。每次必须手动输入密码。用key没这问题。
$要返回的内容 = Invoke-Command -Command {cat /etc/issue} -Session $连接2
$要返回的内容




问：powershell经过ssh，远程运行命令，比bash强在哪？
答：
=============linux远程命令 & ps远程命令 对比例子============
任意sh ---> ssh ---> linux上的bash：
ssh aaa@1.1.1.1 "以用户aaa权限执行的，命令xxx"


win，linux中的powershell ---> ssh ---> linux上的powershell：
$a = 1
[scriptblock]$备份命令 = 
{
	Get-Date
	$b = $using:a + 2 #引用客户机变量，需要用$using:
}

$连接1 = New-PSSession -HostName 1.1.1.1 -UserName root  #手动输入密码或用-KeyFilePath 选项。还需要修改/etc/ssh/sshd_config
invoke-command -ScriptBlock { $备份命令 } -Session $连接1
============================================================
bash的远程命令，简单直接。就好像我左手这盘蛋炒饭，简单解饿，但是不够强。更适用于 简单远程命令场合。
你再看看我右手这盘盖饭好在哪？答：生菜垫底，萝卜雕花围边。
bash远程传递的是【字符串】，powershell传递的是【代码块】。特色是【对象垫底，大花括号围边】。

字符串传递到远程时，经常需要要转义。代码块不用。
代码块，支持多行，格式化，使代码美观。
变量名，函数名支持中文。

代码块中，支持引用客户端变量，一律加上【$using:】，即客户机上的【$a】,在服务器上叫【$using:a】
代码块中，支持引用服务器端变量，即服务器上的【$a】,在服务器还上叫【$a】
即使变量重名，两个$a也绝不会弄混。
强类型变量，在远程使用，无需序列化/反序列化。这点py不行。java不行。

ps用大花括号包围代码，不用单双引号，代码嵌套很容易。
而代码嵌套容易，使的ps的ssh远程，从server1（跳板机，堡垒机）经ssh进入server2，再ssh进入server3，进入33层ssh server执行命令很容易。而shell难。

远程代码天生不老稳定的，有时没反应，或卡住，或中途断了。遇到此情形，每行ps代码都可以在外面套上try-cacth，比shell更稳。

批量ssh，ps采用【多线程】，比bash用【多进程】快，时间准，省内存。



问：本地脚本和远程脚本有何区别？如何编写远程脚本？
答：
由于下述限制颇多，顾应尽量少用【直接】远程调用。多用【进入远程机子后】的本地调用。

1 模块化。要把远程任务，分成n个独立的单元。
我们编写的本地脚本，有时候没分的这么清楚。但远程脚本，就要分成n个脚本，或n个函数。

2 每个单元让它返回$true,或false。
我们要改造本地脚本，人为让每个单元能返回$true,或false。
好让我们远程判断每个单元是否执行成功。

3 对于偶尔会失败的任务，根据上述返回$true,或false，把脚本改造成，有一定循环次数。
令脚本的每个单元，都让它形成闭环。
本地脚本中的本地命令，大都是不报错即成功。
对于bash这就尴尬了，癌症无解。powershell有try+catch解决这问题。

4 每个单元让它，在远程机子上，写入log。log中带上日期时间。

5 每个单元，甚至！每个命令，必须！设定超时时间。

郭德纲说过，远程脚本，天生不老稳定的；）
本地脚本中的本地命令，大都不具备超时选项，远程运行时卡住就完了。
解决这个问题的最佳实践，是用多线程，和计时器。

把单元放入后台线程，然后主线程sleep n秒。超时就kill掉。
这是笨办法，好在简单，bash也能实现。但bash没有线程，只有进程。

powershell中，无需使用此笨办法。powershell有计时器。计时器是多线程的。
new一个计时器对象，并绑定代码后，你就可以-开始计时器-停止计时器-调整计时周期。

现在我们假定一个任务，前3次必然卡住超时，第4次必然成功。
那么我们只需在任务代码中，加上停止计时器的代码。并启动计时器即可。

则前3次运行到卡住代码，超时后被计时器重启。最后1次通过了卡住代码，运行了计时器停止代码。

这涉及到了两个线程之间传值，和控制。
而bash多进程，进程之间传值控制，不如线程之间方便。
所以说【多线程，计时器，是给命令加上超时选项的最佳实践】。

这里面还有一个细节。若你用ps的远程线程，来运行【代码单元】。可以起一个线程名，作为超时kill的标识符。
但是对于bash，就不能用进程名了。你需要一个标明进程是唯一的方法。
这种方法是有，但是又要加不少代码。在这里就不做展开详谈了。









总结：
win客户机上的powershell，经ssh，连linux服务器上的bash，传字符串：目前需要第三方模块，当然这是官方库中的模块，用install-module PoshSSH即可。
win客户机上的powershell，经ssh，连linux服务器上的powershell，传对象：1linux服务器安装ps。2需要编辑/etc/ssh/sshd_config文件。3win客户机装ps6，4客户机装ssh.exe等。


linux客户机上的bash，经ssh，连win服务器上的cmd，传字符串：在win上安装sshd即可，多年前早已实现。
linux客户机上的powershell，经ssh，连win服务器上的powershell，传对象：1win服务器安装sshd.exe等。2需要编辑/etc/ssh/sshd_config文件。3linux客户机装ps6


linux客户机上的powershell，经ssh，连linux服务器上的powershell，传对象：1linux服务器安装ps。2需要编辑/etc/ssh/sshd_config文件


win客户机，经过ps-remoting，连linux服务器。已经实现这个功能。不推荐。
linux客户机，经过ps-remoting，连win服务器。未实现此功能。
win客户机，经过ps-remoting，连win服务器。需要在服务器上开启服务。在客户机上信任服务器。教程略。



问：神马是远程传值？
答：
叫通ip，端口，用户名，密码。然后从【脚本客户端】发送数据到【脚本服务端】，然后反之传送数据。
expect命令就是典型的远程传值。



问：powershell中有expect命令吗？
答：
1有。对于某些奇葩，偏门的应答需求，有第三方模块。
2没有。powershell不使用expect命令。而使用远程传【对象】值！请看下面



问：linux+ssh如何远程传值？
答：
a=123
ssh aaa@127.0.0.1 bash -c "'echo $a'"
ssh aaa@127.0.0.1 bash -s a.sh


问：【powershell+ssh远程连接法】和linux自带的ssh远程连接最大的区别是什么？
答：
bash+ssh远程只能传字符串。powershell能远程传对象。请看：


问：客户机为win，服务端为linux，如何经ssh，远程传【对象】值？
答：
使用了powershell官方库，从linux服务器，给win客户机传对象。
$连接3 = New-PSSession -HostName 192.168.1.1 -UserName root  #将提示输入密码
$要返回的内容 = Invoke-Command -Command {  (get-date).adddays(3) } -Session $连接3
$要返回的内容.year
#------------------分割线------------------------
从win客户机，给linux服务器传对象。计算完后，再传回来。
$win客户端变量1 = get-date
write-host $win客户端变量1
$连接4 = New-PSSession -HostName 192.168.168.73 -UserName root  #将提示输入密码
$win客户端变量2_此值是从linux服务器返回的 = Invoke-Command -Command {  $a = $using:win客户端变量1 ; $a.AddDays(3) } -Session $连接4 
#传教士：不能直接用  $using:win客户端变量1.AddDays(3)
$win客户端变量2_此值是从linux服务器返回的.year




问：客户机为linux，服务端为win，如何经ssh，如何远程传值？
答：
同上


问：powershell中有su，runas命令吗？怎么用powershell运行另外一个用户的命令？
答：
没有。
在powershell中，运行linux本地命令和管道毫无障碍。如：
ssh aaa@127.0.0.1 "以用户aaa权限执行的，命令xxx"  
sshpass -p user_password ssh aaa@192.168.1.1
或者用远程连接session的方法。



问：powershell的ssh客户端，如何自动输入密码（即免密）
答：
就像putty永远不能保存密码。安全和方便永远不可兼得。
xshell永远可以保存密码。人家有商业公司作为支持，作为保安，并且保存密码的算法要总变。
ps core 6目前用密码连接linux，需要每次手动输入密码。密钥对可以不用输入密码。我个人建议用密钥对+ssh-keygen的高安全方案。
但如果需要控制的sshd机子多了，就很麻烦。
解决方案有这么几个：
1在linux发行版上安装sshpass，最可信。建议10%有高安全需求的企业用。
aaa=222
sshpass -p 密码   ssh win用户名@服务器ip "write-host ($aaa+11)"
返回233
2在win上安装cygwin版的sshpass。
3用第三方ssh模块Install-Module -Name SSHSessions。或者winscp。建议90%普通用户用。


问：如何使用win版ssh客户端？
答：
在win10-Build-17134版本中，已经集成了win版ssh客户端。C:\Windows\System32\OpenSSH
可以直接在powershell中用ssh.exe root@ip

没有集成服务器端！如需用服务器端，还得安装。安装教程：
https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH
服务器端软件，默认解压目录    c:\Program Files\openssh
服务器端配置，默认存放目录   C:\ProgramData\ssh


问：powershell的ssh客户端，如何部署密钥对？
答：
1在linux发行版上安装ssh-copy-id，最可靠。
或者使用群里，我编写的ssh-copy-id3.ps1
2用win版的ssh-mount-drive，加copy。 



问：powershell中有【grep】吗？？
答：
powershell中用select-string命令。
单从编码的角度，select-string=聪明，grep=傻 + 有硬伤  :mrgreen:
有bom头时，select-string 自动识别文件编码类型。
无bom头时，无需像linux+grep那样，改变shell环境，无需按某编码另存文件。只需要根据文件编码的不同，指定-encoding参数。 
而grep没这功能，即有【无法指定文件编码类型】的硬伤。
当然grep也不是一无是处，grep有些参数，有额外独特的功能，select-string没有，这就是grep比select-string强的地方。



问：powershell中有【eval】吗？
答：
powershell中用Invoke-Expression来执行字符串。



问：powershell中有【tail -f】吗？就是可以实时的把某个文件新产生的行输出。
答：
Get-Content D:\a.txt -Tail 10 -ReadCount 0 -Wait



问：我想用小键盘的同时，还想要256色终端，那么xshell应该如何设置？
答：
终端---》终端类型---》【putty-256color】或【export TERM=putty-256color】
终端---》键盘---》default或linux。

Eterm-256color可以
gnome-256color不行
konsole-256color不行
putty-256color可以
powershell 传教士 原创分享 2017-02-15
rxvt-256color不行
screen-256color不行
st-256color可以
vte-256color不行
xterm-256color不行
用SecureCRT道理一样




问：shell和python谁更强大？
答：
各有所长，可以互补。但是却无法互补。下面详述。


问：为什么说linux版的powershell，更适合于运维人员用来写脚本？（比linux版python）
答：
1 python有的面向对象功能，linux版powershell都有。

2 python没有命令行。
2.1 python无法成为ssh默认终端，linux版powershell可以。参见章节：《两台带有sshd的linux机子？怎么用powershell连接并发送命令？》
2.2 python中使用shell命令（awk，grep等），非常麻烦。需要增加很多py语法和代码。linux版powershell运行awk这些命令和bash一样。

3 python没有管道。让n个【命令行程序】之间传值，非常麻烦。需要增加很多py语法和代码。linux版powershell有管道，运行awk这些命令和bash一样。

4 python有版本2，版本3不兼容的癌症!问题。linux版powershell没有这样的问题。
4.1 这些问题包含编码问题。

结论：
shell命令如grep等，对编码支持本就不好，不如powershell在家上上述4.1的编码问题。再加上上述2，3点。
令linux人痛不欲生，顾很少有人在py中用外部命令。【py命令库】和【shell命令】死不往来，基本无法互补。而linux版ps就不同了。




问：为什么说powershell的转义，比shell要好？比python好？
答：
1 powershell是面向对象的，属性返回的是直接可用的数据。比面向字符脚本语言（bat，shell）需要扣字符串的情况要少很多。
天生遇到【需要转义的内容】就少。
2 字符串查找替换，powershell中有不需要转义的，.net类中的方法。如：
[string]$a = 'abc\\def'
$b = $a.replace('\\','当')
#返回：【abc当def】
判断ip是否合法，可以用IPAddress类中的TryParse()方法。 
总之我的建议是，尽量多用.net类方法，尽量少用正则，或者只用简单正则。
3 powershell内部用【`】作为转义符。【`】比【\】更不常用，作为转义符冲突少很多。
3.1 在编写数据库的脚本的时候，【`】的冲突就多了。
如【`table`】 会和【`t】冲突，如【`biao`】会和【`b】冲突，后来我用【`表`】解决的。
3.2【`】比python的【\】强。python需要在路径前面加上r，如r'c:\xxx\xxx'。太不爽啦，ps没这问题。
4 ps字符串查找替换，有正则引擎，兼容linux，也是用【\】作为转义符。
不过，有专门的字符串转义函数【[Regex]::Escape()】，先转义后进行查找替换，代码可读性高。
$转义前的原始字符串 = '\+\&*|]'
$转义后的字符串 = [Regex]::Escape($转义前的原始字符串)
-------------
脚本例子
[string]$a = 'abc\\def'
$转义前的原始字符串 = '\'
$转义后的字符串 = [Regex]::Escape($转义前的原始字符串) #【\】--->【\\】
$b = [Regex]::replace($a,$转义后的字符串,'当')
$b #返回【abc当当def】 
-------------
5 bash和awk，各自有for，各自有转义。组合起来，很容易甲影响乙，甲吞掉乙。
遇到【'】，【"】，【\】，【*】也很容易出问题。                                                            '
这就像穿了两层秋裤，你拉动一层，另一层也跟着动，你需要费脑筋去关注他俩的兼容。
此乃癌症，很难解决。
但是捏，这问题也是可以在一定程度上避免。这需要写shell的人改正臭毛病。
【把awk代码单独放在.awk文件中，而不是放在命令行中】
powershell没有此问题，放在命令行，放在脚本中，没啥影响。



问：
powershell脚本调用，和linux bash脚本调用，有啥区别？
a.ps1调用b.ps1，b.ps1调用c.ps1。即a.ps1中有一句【& .\b.ps1】。
和
a.sh调用b.sh，b.sh调用c.sh。即a.sh中有一句【b.sh】。


答：
把"a $id"这句代码放入a.ps1，把 "b $id"这句代码放入b.ps1。
把echo "a $$ $PPID"这句代码放入a.sh，把echo "b $$ $PPID"这句代码放入b.sh。假设每个sh都有执行权限。

结论：
powershell用子线程，执行脚本。所有子线程共用一个$id的powershell进程。
bash用单独的子进程，执行脚本。
单独的进程隔离好，单独的线程并发代价小，还有【$global:】全局变量作用域，可以共享变量。【function global:函数名】全局函数域，可以共享代码。



问：linux中，后台运行powershell脚本，和后台运行bash脚本有何异同？
答：
1powershell后台，分为多线程后台（*-job命令），和多进程后台（基于workflow）两种。
目前linux中，暂时没有实现workflow，顾这里只对比【linux+powershell+job】和【bash的后台脚本】

2powershell，*-job命令，启动方法：
2.1 start-job xxx.ps1
2.2 powershell中：xxx.ps1 &  #这里的&即start-job的别名。是ps6中新增的功能。

3bash中的启动方法：
powershell -command "xxx1.ps1 &;xxx2.ps1 &" & #即启动一个后台进程powershell，然后在powershell里启动两个后台线程。

4和bash相同的，终端软件中的启动方法：（putty，xshell）
powershell -command "xxx1.ps1 &;xxx2.ps1 &" &
exit #必须用exit退出终端软件，而不能点x，关闭窗口。

结论：
它俩之间的差别，主要在bash脚本是多进程后台，powershell脚本是多进程+多线程后台。
基本不能前后台切换。



问：为什么说“一旦使用powershell，即可告别没完没了的【数据对齐】烦恼”？
答：
1 linux命令行世界是存在这个烦恼的。我个人认为，这是linux命令行固有的癌症。这个烦恼在powershell是不存在的。

2.1 从原理上来讲，linux使用字符串，即裸数据+格式（空格，tab）。
2.2 powershell使用属性，只有裸数据，没有格式，使用时现组合。即裸数据和格式分离。
正是这个差别，使得（假设有某个命令，ps版和linux版功能相同）ps能做到对齐完美，linux做不到。
正是由于这个方案，使得powershell简单强大死你！
2.3 等ps版命令完善后，同样的命令，只要有ps版的，就不用linux自带的。嗯，逐渐从温饱过度到小康。

那么，如何组合的捏？
3.1 对于字符界面，用【xxx |format-table】，【xxx |format-list】组合。
3.2 win上自带图形。可用【xxx |Out-GridView】，【xxx |format-list-grid】
3.3 可以自定义很多新套，老套，安全x。就好像天冷套穿秋裤一样。根据天气和数据的显示需求，找套来用，或者自己做套来用。

结论：
后端中小量数据用csv格式来存储，或者用更好的格式excel来存储。大量数据用各种数据库来存储。
前端用powershell来显示，告别没完没了的【对齐】烦恼！




问：如何在win下编写ps1，win下调试ps1，linux上自动同步保存ps1，linux下运行ps1？
答：
vscode有插件名叫sftp，可以在win的vscode中编写ps1脚本，保存时，自动同步到linux目录中。


问：如何在win中读写linux文件目录？
答：
有几种sshfs软件。现介绍一种如下：
1 下载安装稳定版的winfsp。
https://github.com/billziss-gh/winfsp/releases/

2 下载安装稳定版的win-sshfs
https://github.com/billziss-gh/sshfs-win/releases/

3 用【无管理员权限的】powershell.exe,运行下列脚本。（cmd中不灵）
cd  'c:\Program Files\SSHFS-Win\bin\'
$env:PATH='C:\Program Files\SSHFS-Win\bin'
echo '你的密码' | sshfs.exe  root@192.168.2.3:/  y:  -o StrictHostKeyChecking=no -o password_stdin

4 成功。可以在cmd.exe，powershell.exe，win的文件管理器中访问linux文件。
支持虚拟机。若kill掉sshfs.exe，则盘符映射结束。若需调整细节。可运行：
c:
cd  "\Program Files\SSHFS-Win\bin\"
sshfs.exe -h
来研究命令行的参数。




问：脚本如何读写【当前进程】中的环境变量？
答：
通用设置：
1 /etc/profile中存储的是，本机环境变量
2 用户家目录下的.bashrc中存储的是，用户环境变量
3 在当前进程中，设定环境变量，子进程中有，父进程无。
4 在当前进程中，显示所有环境变量，的命令：env
5 powershell的profile在  /用户家目录/.config/powershell/Microsoft.PowerShell_profile.ps1
可以在这里，变量存档。

bash：
export A=B #设置
echo $A #读取



csh，tcsh：
setenv A B #设置
echo $A #读取



powershell：
$env:A = 'b' #设置
$env:A #读取


问：a、b两个脚本之间，传值，传多个值。应该如何做？
答：
bat和bash非常喜欢用环境变量，来干这件事。



玩linux得用shell，玩shell得用环境变量。不用不行么？用了有什么不良后果？
为什么powershell不喜欢用环境变量？
为什么powershell没有source命令？
答：
bash不用环境变量不行。因为bash中没有【脚本外变量作用域】。
脚本1，脚本2，想公用变量a，那么变量a存哪？只能存在环境变量中。
而ps不同，ps有【$global:a】

$global:			变量的【全局】作用域，位于$script外部。位于powershell.exe内部，所以也可以叫做进程内最大的作用域。一般用于多线程，多脚本公用变量。
$script:			变量的【脚本】作用域，xxx.ps1脚本内部，在脚本外部无法访问。一旦脚本执行完成，或中途经exit 1等数字退出后，【$script:yyy】这个xxx.ps1中所有的变量，就都没用了，将变成【尸体变量】交给垃圾回收。


powershell【$global:】的优点：
powershell照样可以用一个脚本，如脚本a.ps1，来存储多个变量的值，运行这个脚本来传值。
虽然powershell也可以用【win环境变量】、【linux环境变量】、来传值，
powershell自己有全局变量作用域【$global:】更好用！可以存储对象等变量。
所以说【a脚本的_配置文件b.ps1】就相当于.ini。

环境变量的缺点：
但是环境变量只能存储少量数据，只能是字符数字。
在脚本中使用【环境变量】，传递多个值，是一把双刃剑。
读【环境变量】，造成了脚本的依赖。甚至形成a脚本依赖b，b依赖c，c依赖a，互相依赖的死循环。
powershell的【$global:变量作用域】在powershell.exe之内，这很环保，不会污染【环境】，
而shell会，你的任务脚本结束时，需要额外编写清理环境变量的代码，比较麻烦。不清理，造成了后续依赖脚本的错误执行。

---------------------------------
设计故事：bat，bash，powershell三人，打劫环境变量。

一个漆黑的夜晚，bat，bash，powershell三人，出去打劫。把美女【环境变量】堵在胡同里。
色狼bat，bash，道：“举起腿来，劫色”。

。。。此处省去三万字。。。

bat，bash，“写入”环境变量后。问powershell，你为什么不来写入（劫色）？

powershell笑道：“我自备充气【$global:】，变量作用域，此域中支持对象，用之方便，不用求人。。。”


global变量作用域【$global:abc = 1】中存储，n个脚本公用的变量。

-故事完-
---------------------------------


问：powershell有哪些变量作用域？
答：
$global:			变量的【全局】作用域，位于$script外部。位于powershell.exe内部，所以也可以叫做进程内最大的作用域。一般用于多线程，多脚本公用变量。
$script:			变量的【脚本】作用域，xxx.ps1脚本内部，在脚本外部无法访问。一旦脚本执行完成，或中途经exit 1等数字退出后，【$script:yyy】这个xxx.ps1中所有的变量，就都没用了，将变成【尸体变量】交给垃圾回收。
$local:				变量的【本地】作用域，可以用在比【$script:】小，但比【$private:】大。可以有多个local作用域。
$private:			变量的【私有】作用域，位于函数，workflow内部。在函数，workflow外无法读写。
编号作用域:		0表示当前，1表示父。2表示爷，以此类推。

全局 > 脚本 > 本地 > 本地 > 本地 > 函数，类，私有

旁白：bash 没有脚本外部的，变量作用域，即没有【$global:】，所以没法公用变量，只能同过source，把公用变量写入父进程的环境变量。


问：在win + 终端软件(如putty)，登录linux后。使用linux版powershell，如何开启按【esc键】删除整行？
答：
mkdir "$env:HOME/.config/powershell" 
Add-Content  -Value 'Set-PSReadlineOption -EditMode Windows' -LiteralPath $profile 




问：在管道前后面，在循环中，本来可以用linux外部命令，你为什么不用？却非要用ps命令？
答：
1 新建多个空文本文件，ps大约快touch 10倍？！何解？
http://bbs.chinaunix.net/thread-4264777-1-1.html

2 百万简单循环耗时，powershell为bash的3.4%，或者反过来说bash耗时是powershell的28倍。
http://bbs.chinaunix.net/thread-4255981-1-1.html


问：如何在.ps1脚本中，嵌入shell命令？
答：
永远不要用bash和.sh，里面坑太多。只需要在linux版powershell的.ps1脚本中，用bash执行字符串即可。
=====================
$bashcmd =
@'
echo '我是bash命令'
echo '命令中可以有单引号'
echo "命令中可以有双引号"
echo '如需解析变量，则用这种括号，注意头尾必须换行'
echo '@\"'
echo '$a'
echo '\"@'
'@
$powershell变量 = /usr/bin/bash -c $bashcmd
#需要转义，有点不好
=====================
或
$powershell变量 = 
@'
echo '我是bash命令'
echo '命令中可以有单引号'
echo "命令中可以有双引号"
echo '如需解析变量，则用这种括号，注意头尾必须换行'
echo '@"'
echo '$a'
echo '"@'
'@ | /usr/bin/bash
#不需要转义，推荐
=====================





问：powershell读取文本不乱码，靠什么？
答：
1 靠bom头，来识别utf16le和utf8。
2 win中文版中，靠get（set）-content命令中的参数-encoding default来识别不带bom头的文本，成为gbk。
2.1问：但是linux版，默认是zh-ch.utf-8的。所以linux中，不带-encoding default参数了。
那么说，linux中，读取gbk编码文件，如何指明编码？
2.1答：简单，请看：

$gbk = [System.Text.Encoding]::GetEncoding("gbk") 
#这样也行 $gbk2 = [System.Text.Encoding]::GetEncoding(936) 
Get-Content /powershell/2017-12-29-gbk.txt -Encoding $gbk #或$gbk2


3把一个文件，由a编码，转换到b编码。设置目标编码也是一个道理。




问：powershell如何跟，php页面，相互传值，传参数？
答：
php--->调用--->shell(powershell):
shell_exec("./chuanzhi.sh  $zhi1 $zhi2");
shell_exec("pwsh -file ./chuanzhi.ps1  $zhi1 $zhi2");

===================
shell(powershell)--->调用--->php:
#!/usr/bin/env pwsh
/usr/bin/php  /var/www/chuanzhi.php 400 700

chuanzhi.php
$argv[0];          	#powershell脚本名称
$zhi1=$argv[1];			#值1
$zhi2=$argv[2];			#值2



问：如何根据zabbix监控结果，调用powershell处理脚本？
答：
1服务端安装zabbix-get检测工具
yum install zabbix-get

2脚本命令行：
$a = zabbix_get -s 192.168.123.45 -p 80 -k 'proc.num[httpd]'
if ($a -eq 'xxx') {echo '监控到故障1234，下面启动删库跑路程序 ^_^' }



问：为啥docker用户，docker运维，也要学习linux版的powershell？
答：
1
你使用docker，k8s难免要编写yaml编排文件。yaml是文本，不是脚本，
不支持变量，而powershell可以让 .yaml，.yml《---》【ps哈希表变量】互相转换。

安装：
Install-Module -Name powershell-yaml #win，linux通用

教程：
https://github.com/cloudbase/powershell-yaml/

例子：
========.yaml文件开始===========
apiVersion: v1
kind: Pod
spec:
  containers:
  - command:
    - kube-scheduler
    - --address=127.0.0.1
    - --kubeconfig=/etc/kubernetes/scheduler.conf
    - --leader-elect=true
    image: k8s.gcr.io/kube-scheduler-amd64:v1.11.0
    imagePullPolicy: IfNotPresent
    livenessProbe:
=========.yaml文件结束==========


=========ps脚本开始==========
#脚本目的：修改镜像字符串为“它为yaml谋幸福，呼儿嗨哟，它是运维大救星”，当然也可以改别的项目。yaml本身就是树形结构的变量，shell不行。
Import-Module -Name powershell-yaml 

$输入yaml模版文件 = 'a:\pscode\TEMP_2018\temp154\kube-scheduler.yaml'
$输出yaml成品文件 = 'a:\pscode\TEMP_2018\temp154\xxx.yaml'
$yaml字串1 = Get-Content $输入yaml模版文件  -raw
$yaml对象 = ConvertFrom-Yaml $yaml字串1
write-host $yaml对象.spec.containers[0].image #返回 k8s.gcr.io/kube-scheduler-amd64:v1.11.0

$yaml对象.spec.containers[0].image = '它为yaml谋参数化，呼儿嗨哟，它是运维大救星，等立个灯~'
$yaml字串2 = Convertto-Yaml $yaml对象
Set-Content -LiteralPath $输出yaml成品文件 -Value $yaml字串2
=========ps脚本结束==========


2 powershell管理json方便。json字符串《---》【ps哈希表变量】之间互相转换。
就用convertfrom-json,convertto-json。
3 powershell管理容器，镜像方便。支持管道，属性。参见：
巧用linux版powershell，
管理linux下docker的，
image 和 container
https://www.cnblogs.com/piapia/p/8651332.html





问：powershell容器镜像（image），的仓库在哪里？
答：
1docker hub官方image仓库。
2微软image仓库，即mcr.microsoft.com  。



问：powershell的镜像（image）有哪些分类？
答：
1 Ubuntu 16.04版
2 centos 7版
3 win nano版



问：powershell的镜像（image）如何pull？
答：
docker pull mcr.microsoft.com/powershell:ubuntu-16.04
docker pull mcr.microsoft.com/powershell:centos-7


问：docker版powershell使用方式是？
答：
1用【powershell容器】管理【宿主机】。
1.1 通过docker -v 映射目录后。让docker中的powershell，访问、管理【宿主父linux】的文件。
1.2 让docker中的powershell，访问、管理【宿主父linux】的进程。
自从Docker 1.5之后，docker run命令引入了--pid=host参数来支持使用宿主机PID名空间来启动容器进程，
这样可以方便的实现容器内应用和宿主机应用之间的交互：比如利用容器中的工具监控和调试宿主机进程。


2用【powershell容器】管理【docker数据卷】【n个容器，共享一个docker数据卷】中的文件。
注意，共享数据卷的读写，立马生效。
通过给【powershell容器】映射【docker数据卷】。
docker run --mount type=volume source=powershell所在的卷名字 destination=/容器内目录 volume-driver=默认值是local


3【powershell容器】通过ip+sshd，访问【容器a】，或另一台虚拟机。
在【容器a】上安装sshd后。通过ssh连接，或docker mount sshfs访问。
docker run --mount type=volume source=powershell所在的卷名字 destination=/容器内目录 volume-driver=vieux/sshfs
而通过sshd发送ps -ef，kill等命令，即可管理【容器a】中的进程。

4 在【容器a】中，通过ssh客户端，加目标ip+sshd端口，访问安装在win中的，全功能的，powershell虚拟机。
需要在win中安装sshd。


问：powershell如何助力jenkins多节点远程任务？
答：
jenkins就是脚本的web前端。
本地作为jenkins主机。远程的系统作为jenkins节点机。操作系统可以是win，linux任意组合。
从本地的powershell，通过ssh连接到远程的win或linux，比bash容易。
1 自动传复杂嵌套代码，
2 【$using:本地变量名】传变量，
3 send-mailmessage发邮件，
4 scp，sftp传文件，



问：在jenkins的哪里用？
答：
在
jenkins---》构建---》execute shell。
或
jinkins---》Publish Over SSH插件的exec command中运行：
/usr/bin/pwsh -f /你的项目路径/a.ps1 -参数1 'aaa' -参数2 123
或win下用：
powershell.exe -file d:\你的路径\a.ps1 -参数1 'aaa' -参数2 123




----------后记篇--------------
问：如何快速成为中级用户?
答：
1精研.net集合类
2精研集合方法。即linq中的方法。
https://msdn.microsoft.com/zh-cn/library/system.linq.enumerable(v=vs.110).aspx



