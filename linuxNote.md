文件系统：
rootfs:根文件系统
FHS:linux
/boot: 系统启动相关的文件，如内核、initrd,以及grub(bootloader)
/dev: 设备文件，一切皆文件
	设备文件：
		块设备：随机访问，按一个一个的数据块访问，例如硬盘
		字符设备：线性访问，有次序的，一个字符一个字符输入的设备，例如键盘
/etc: 配置文件主要存放路径，大部分都是纯文本文件
/home: 用户的家目录，默认为/home/USERNAME
/lib:库文件
	静态库: .a
	动态库: windows:.dll linux:.so（shared object）
	/lib/modules:内核模块文件
/media:挂载点目录,移动设备
/mnt:挂载点目录，额外的临时文件系统
/opt:可选目录，第三方程序的安装目录
/proc:伪文件系统，内核映射文件
/sys:伪文件系统，跟硬件设备相关的属性映射文件
/tmp:临时文件，/var/tmp
/var:可变化的文件
/bin:binary,可执行文件，用户命令
/sbin:管理命令

/usr: universal shared read-only,只读文件
	/usr/bin
	/usr/sbin
	/usr/lib
/usr/local:
	/usr/local/bin
	/usr/local/sbin
	/usr/local/lib

命名规则：不能使用/当文件名

文件管理
目录管理
ls
cd
pwd
mkdir:创建空目录
	-p:
	-v:verbose
/root/x/y/z

/mnt/test/x/m,y
mkdir -pv /mnt/test/x/m /mnt/test/y
mdkir -pv /mnt/test/{x/m,y}

~USERNAME
命令行展开：
/mnt/test2/
a_b,a_c,d_b,d_c
(a+d)(b+c)=ab+ac+db+dc
{a,d}_{b,c}

# tree: 查看目录树
删除目录： rmdir (remove directory)
在Linux下目录和文件是不能同名的

文件创建和删除
#touch 
	-a
	-m
	-t
	-c CCYYMMHHhhmm.ss
文件数据：
	数据
	元数据
nano FILE
file FILE ：显示文件内容的类型
文本查看类：
cat,tac
more

less
	SPACE
	b
	ENTER
	k
	/
	?
	n
	N
head

tail
	-f:follow
cut
	-d
	-f
tr

文本统计命令：
wc:word counter
	-l:行数
	-w:单词数
	-c:字符数
文本排序：sort
	-r
	-n
	-t:指定字段分隔符
	-k #:指定排序的字段
grep,egrep,fgrep
grep:根据模式搜索文本，并将符合模式的文本行显示出来
Pattern:文本字符和正则表达式的元字符组合而成匹配条件

grep [options] PATTERN [FILE...]
	-i
	--color
	-v:显示没有被模式匹配到的行
	-o:只显示被模式匹配到的字符串
*:任意长度的任意字符
？:任意单个字符
[]:
[^]:

正则表达式：REGular EXPression,REGEXP
元字符:
.:匹配任意单个子符

匹配次数（贪婪模式）：
*:匹配其前面的字符任意次
a,b,ab,aab,acb,adb,amnb
a*b
a.*b
.*:任意长度的任意字符
？:匹配其前面的字符1次或0次
\{m,n\}:匹配其前面的字符至少m次，至多n次
	\{1,\}
	\{0,3\}
位置锚定：
^:锚定行首，此字符后面的任意内容必须出现在行尾
&:锚定行尾，此字符前面的任意内容必须出现在行尾
^$:空白行
\<或\b：锚定词尾，其后面的任意字符必须作为单词首部出现
\>或\b：锚定词尾，其后面的任意字符必须作为单词尾部出现
\<root\>

REGEXP:REGular EXPression
Pattern:
正则表达式：
Basic REGEXP:基本
Extended REGEXP:扩展

基本正则表达式：
.:
[]:
[^]:
次数匹配：

.:
?:0或1次
\{m,n\}:至少m次，至多n次

.*:
锚定：
^:
$:
\<,\b
\>,\b
\(\)
\1,\2,\3,...

grep:使用基本正则表达式定义的模式来过滤文本的命令
	-i:无视大小写
	-v:反向匹配
	-o:只显示匹配到的字符串
	--color:显示颜色
	-E:使用扩展的正则表达式
	-A #:after 
	-B #:before
	-C #:context
	
扩展正则表达式：
字符匹配：
.
[]
[^]

次数匹配：
*:
?:
+:匹配其前面的字符至少1次
{m,n},不需要使用\

位置锚定：
^
$
\<
\>

分组：
():分组,不需要使用\
\1,\2,\3,...

或者：
|: or

egrep --color '\<([1-9]|[1-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])\>
egrep --color '\<[0-255].[0-255].[0-255].[0-255]\>'

本地变量：
VARNAME=VALUE:作用域为整个bash进程

局部变量：
Local VARNAME=VALUE:作用域为当前代码段

环境变量：作用域为当前shell进程及其子进程

export VARNAME=VALUE

VARNAME=VALUE
export VARNAME
“导出”
位置变量：
$1,$2,...
特殊变量：
	$?:上一个命令的执行状态返回值
程序执行，可能有两类返回值：
	程序执行结果
	程序状态返回代码（0-255）
		0:正确执行
		1-255:错误执行， 1，2，127系统预留
输出重定向：
>:覆盖重定向
>>:追加重定向
2>:错误覆盖重定向
2>>:错误追加重定向
&>:同时重定向

撤销变量：
unset VARNAME
查看当前shell中变量：
set

查看当前shell中的环境变量：
printenv
env
export

/dev/null :软件设备，bit bucket,数据黑洞

脚本在执行时会启动一个子shell进程：
	命令行中启动的脚本会继承当前shell环境变量
	系统自动执行的脚本（非命令行启动）就需要自我定义需要的环境变量


bash中如何实现条件判断？
条件测试类型：

	整数测试
		-gt：大于
		-le：小于等于
		-ne：不等于
		-eq：等于
		-ge：大于等于
		-lt：小于
	字符测试：
	==：测试是否相等，相等为真，不等为假
	！=：测试是否不等，不等为真，空则为假
	>
	<
	-n string:测试指定字符串是否为空，空则真，不空则假
	-z string:测试指定字符是否不空，不空为真，空则假
	文件测试
	-e
	-f
	-d
	-r
	-w
	-x

条件测试的表达式：
[ expression ]
[[ expression ]]
test expression

变量名称：
	1，只能包含字母，数字和下划线，并且不能以数字开头
	2，不应该跟系统中已有的环境变量重名
	3，名字最好有意义
bash变量的类型：
	本地变量（局部变量）
	环境变量
	位置变量:$1,$2,...
	特殊变量:
		$?:
		$#:参数个数
		$*:参数列表
		$@:参数列表
！id user1 && useradd user1 && {echo 'user1' | passwd --stdin user1 } || echo 'user1 exists'

文件测试：
	-e FILE: 测试文件是否存在
	-f FILE: 测试文件是否为普通文件
	-d FILE: 测试指定路径是否为目录
	-r FILE: 测试当前用户对指定文件是否有读取权限
	-w FILE: 写入权限
	-x FILE: 执行权限

组合测试条件
-a:与关系
-o:或关系
！：非关系
[ -e /etc/inittab ]
[ -x /etc/rc.d/rc/sysinit ]

测试脚本是否由语法错误：
bash -n 脚本，测试脚本
bash -x 脚本：单步执行

定义脚本退出状态码：
exit:退出脚本
exit #
如果脚本没有明确定义退出状态码，那么，最好执行的一条命令的退出码即为脚本的退出状态码

sed基本用法：
sed:Stream Editor
	行编辑器（全屏编辑器：vi）

sed:模式空间
默认不编辑原文件，仅对模式空间中的数据做处理

sed [options] 'AddressCommand' file ...
	-n:静默模式，不再默认显示模式空间中的内容
	-i:直接修改源文件
	-e:SCRIPT -e SCRIPT:可以同时执行多个SCRIPT
	-f:/PATH/TO/SED_SCRIPT
		sed -f /path/to/scripts(保存的都是脚本文件) file
	-r:表示使用扩展正则表达式
Address:
1,StartLine,EndLine
	比如1，100
2，/RegExp/
	/^root/
3,/pattern1/,/pattern2/
	第一次被pattern1匹配到的行开始，至第一次被pattern2匹配到的行结束，这中间的所有行
4,LineNumber
	指定的行
5，StartLine,+N
	从StartLine开始，向后的N行
Command:
	d:删除符合条件的行
	p:显示符合条件的行
	a \string:在指定行后面追加新行，内容为string。
		\n可以用于换行
	i \string:在指定行前面添加新行，内容为string。
	r FILEPATH:将指定的文件的内容添加至符合条件的行处
	w FILEPATH:将地址指定的范围内的行另存至指定的文件中
	s/pattern/string/修饰符:查找并替换，默认只替换每行中第一次被模式匹配到的字符串
		加修饰符
			g:全局替换
			i:忽略字符大小写
	s///: s###,s@@@
		\(\),\1,\2
	l..e:like-->liker
	     love-->lover
	     like-->Like
	     love-->Love
	&:引用模式匹配整个串
字符测试：
==：测试是否相等
！=：测试是否不等
>
<
-n string:测试指定字符串是否为空，空则真，不空则假
-s string:测试指定的字符串是否不空，不空为真，空则为假

for (i=0,i<=100,i++){
	sum=sum+i
}

循环：进入条件，退出条件
for
while
until
for 变量 in 列表;do
 循环体
done

for i in 1 2 3 4 5 6 7 8 9 10;do
	加法运算
done
遍历完成之后，退出
如何生成列表：
{1..100}
seq [起始数 [步进长度]] 结束数

1,...,100

运行程序
设备管理
软件管理
进程管理
网络管理

vim编辑器
文本编辑器，字处理器
ASCII
nano sed

	vi:Visual Interface
	vim:Vi improve

vi和nano一样，都是全屏编辑器，是模式化编辑器
vim模式：
	编辑模式（命令模式）
	输入模式
	末行模式
一，打开文件：
#vim /path/to/somefile
	vim +#:打开文件，并定位于第#行
	vim +:打开文件，定位至最后一行
	vim +/PATTERN: 打开文件，定位至第一次被PATTERN匹配到的行的行首
	默认处于编辑模式
二，关闭文件：
	1，末行模式关闭文件
		:q :不保存退出
		:wq :保存并退出 --> :x
		:q! :不保存并退出
		:w:保存
		:w!:强行保存

	2,编辑模式下退出
		Ctrl+ZZ:保存并退出

三，移动光标
	1，逐字符移动：
		h:左
		l:右
		j:下
		k:上
		#h:移动#个字符
	2，以单词为单位移动
	w:移至下一个单词的词首
	e:跳至当前或者下一个单词的词尾
	b:跳至当前或前一个单词的词首
		以上命令都支持命令后跟数字
	3，行内跳转：
		0:绝对行首
		^:行首的第一个非空白字符
		$:绝对行尾
	4，行间跳转：
		#G：表示直接跳转至第#行
		G：跳转到最末尾
		末行模式下，直接给出行号回车即可
四，翻屏
Ctrl+f:向下翻一屏
Ctrl+b:向上翻一屏

Ctrl+d:向下翻半屏
Ctrl+u:向上翻半屏

五，删除单个字符
	x:删除光标所在处的单个字符
	#x:删除光标坐在处及向后的共$个字符
六，删除命令：d
	d命令跟跳转命令组合使用
	#dw,#de,#db

	dd:删除当前光标所在行
	#dd:删除包括当前光标所在行在内的#行
	末行模式下：
	StartAdd,EndADDd
		.:表示当前行
		$:最后一行
		+#:向下的#行
七，粘贴命令
p（小写）:如果删除或复制为整行内容，则粘贴至光标所在行的下方，如果复制或删除的内容为非整行，则粘贴至光标所在字符的后面
P:（大写）如果删除或复制为整行内容，则粘贴至光标所在行的上方，如果复制或删除的内容为非整行，则粘贴至光标所在字符的前面

八，复制命令 y yank
	y:用法同d命令

九，修改：先删除内容，再转换为输入模式
	c:用法同d命令

十，替换：r
	R:替换模式

十一，
	1，撤销编辑操作
		u:undo 表示撤销前一次的编辑操作，连续u命令可撤销此前的n次操作，vim编辑器可以保存最近的50次操作
		#u:直接撤销最近#次操作
	2，还原最近一次的撤销操作：Ctrl+r

十二，重复前一次编辑操作
	.
十三，可视化模式
	v/V
	v:按字符选取
	V:按矩形块选取
十四，查找
	/PATTERN n/N
	?PATTERN n/N
十五，查找并替换（需要在末行模式下）
	s命令：
		ADDR1,ADDR2s@PATTERN@string@gi
		(g,表示全局替换 / i,表示忽略字母大小写)
1,$
%:表示全文

十六，如何使用vim编辑多个文件
	vim FILE1 FILE2 FILE3
	:next 切换至下一个文件
	:prev 切换至前一个文件
	:last 切换至最后一个文件
	:first 切换至第一个文件
	退出
	:qa 全部退出

十七，分屏显示文一个文件

	Ctrl+w,s:水平拆分窗口
	Ctrl+w,v:垂直拆分窗口
	在窗口间切换光标：
	Ctrl+w,ARROW

十八，分窗口显示多个文件

	vim -o :表示水平分割显示
	vim -O :垂直分割显示

十九，将当前文件的部分内容另存为另外一个文件
	末行模式下使用w命令
	:w
	:ADDR1,ADDR2w /PATH/to/somewhere

二十，将另外一个文件的内容填充在当前文件中
	:r /path/to/somefile

二十一，跟shell交互
	:！COMMAND

二十二，高级话题
1，显示或取消显示行号
	:set number
	:set nu

	:set nonu

2,显示忽略或区分字符大小写
	:set ignorecase
	:set ic
	
	:set noignorecase

3,设置自动缩进
:set autoindent
:set ai
:set noai
4,查找到的文本高亮显示或取消
:set hlsearch
:set nohlsearch
5,语法高亮
:syntax on
:syntax off



bash:
1，命令历史，命令实例
2，管道，重定向
3，命令别名
4，命令行编辑
5，命令行展开
6，文件名统配
7，变量
8，编程

命令行编辑：
光标跳转：
Ctrl+a:跳到命令行首
Ctrl+e:跳到命令行尾
Ctrl+u:删除光标以前的
Ctrl+k:删除光标以后的
Ctrl+<-:向前跳一个单词
Ctrl+->:向后跳一个单词
history:查看命令历史
history -c:清空命令历史
history -d n:删除第n个命令历史
history -d n m:从第n个开始删除m个命令历史
~/.bash_history:命令历史保存文件
history -w:保存命令历史至历史文件

环境变量
PATH：命令搜索路径
HISTSIZE：命令历史大小，默认是1000条 echo $HISTSIZE 1000
命令历史的使用技巧：
！n:执行命令历史中的第n条命令
！-n：执行命令历史中的倒数第n条命令
！！：执行刚刚执行的上一条命令
！command:执行命令历史中最近一个以command字符串开头的命令
！$可以引用上一个命令的最后一个参数，按下ESC后松开，再按. ，ALT+.

命令别名：
alias CMDALIAS=COMMAND [options] [arguments]
在shell中定义的别名仅在当前shell生命周期中有效；别名的有效范围为当前shell进程，对于其他shell进程是无效的
unalias CMDALIAS unalias cl
\CMD
命令替换：$(COMMAND),反引号：`COMMAND`
把命令中某个子命令替换为其执行结果的过程
file-2013-02-28-14-53-31.txt

bash支持的引号:
``:命令替换
“”:弱引用，可以实现变量替换
'':强引用，不完成变量替换

文件名通配，globbing
*:任意长度的字符串
？:任意单个字符
[]:匹配指定范围内的任意单个字符
	[abc],[a-m],[a-z],[A-Z],[0,9],[a-zA-Z]
[^]:匹配指定范围以外的任意单个字符

 [[:alpha:]]*[[:space:]]*[[:alpha:]]

用户，组，权限

权限：r,w,x

文件：
r:可读,可以使用类似cat等命令查看文件内容
w:可写，可以编辑或删除此文件
x:可执行，executable,可以在命令提示符下当作命令提交给内核运行

目录：
r:可以对此目录执行ls以列出内部的所有文档
w:可以在此目录创建文件
x:可以使用cd切换进此目录，也可以使用ls -l查看内部文件的详细信息

用户：UID,etc/passwd
组：GID,/etc/group

影子口令：
用户：/etc/shadow
组：/etc/gshadow

用户类别：
管理员组：
普通组：
	系统组：
	一般组：

用户组类别：
	私有组：创建用户时，如果没有为用户指定其所属的组，系统会自动为其创建一个与用户名同名的组
	基本组：
	附加组，额外组：

访问权限模型：访问者（有自己的owner和group权限）->通过进程（有自己的owner和group权限）->访问的目标文件（有自己的owner和group权限）

/etc/passwd 解析

account :登录名
password:密码
UID:用户ID
GID:基本组ID
comment:注释
HOME DIR:家目录
SHELL:用户的默认shell

/etc/shadow 解析

account :登录名
encrypted password:加密过的密码
$1 表示是MD5加密的密码

加密方法：
	对称加密：加密和解密使用同一个密码
	公钥加密：每个密码都成对出现，一个为公钥（public key），一个为私钥(secret key),公钥加密只能用与之匹配的私钥解密
	单项加密,散列加密

用户管理命令：
		
添加用户：useradd/adduser
删除用户：userdel
修改用户：usermod
用管理员给用户设置密码：passwd username
修改用户shell:chsh
查看用户的ID之类的信息：id
改变用户各种外围属性的命令：chage

组管理命令：
groupadd,groupdel,groupmod,gpasswd

权限管理:
chown,chgrp,chmod,umask 

useradd [options] USERNAME

-u UID 
-g GID
-G GID
-c "COMMENT"
-d /path/to/directory
-s shelldir=/etc/shells /bin/bash
useradd -s /sbin/nologin user5
-m --create-home -k
-M 不为用户创建家目录

userdel [option] USERNAME
	-r:同时删除用户的家目录 //userdel删除用户时默认并不会删除用户的家目录

环境变量：
PATH
HISTSIZE
SHELL

id：查看用户的帐号属性信息
	-u
	-g
	-G
	-n
finger:查看用户帐号信息
finger USERNAME

//修改用户帐号属性
usermod
	-u UID
	-g GID
	-a -G GID:不使用-a选项，否则会覆盖此前的附加组
	-c 注释 comment
	-d 为用户指定新的家目录 用户无法访问旧的家目录里的文件 -m 移动旧的文件至家目录当中
	-s shell
	-l loginname
	-e --expiredate:用户账户过期时间
	-f inactivate 非活动时间
	-L 锁定用户帐号 类似于禁用
	-U 解锁帐号
	-r :添加一个系统用户，系统用户通常都不能登录，且没有家目录
chsh:改用户的默认shell
chfn:修改用户的comment信息

密码管理：
passwd USERNAME
	--stdin:标准输入读取密码（键盘）
	-d:删除用户密码
	-l
	-u
pwck:检查用户帐号完整性

组管理：
创建组：groupadd
groupadd
	-g GID
	-r :添加一个系统组
groupmod
	-g GID
	-n GRPNAME	
	-l loginname
groupdel

gpasswd GRPNAME:为组添加密码
	
newgrp GRPNAME <---> exit 临时切换（登录）到新组，可以退出

newgrp操作只涉及到三个方面：passwd,shadow,group  可以不用useradd而手动编辑这三个文件来添加用户

chage
	-d:最近一次的修改时间
	-E:过期时间
	-I:非活动时间
	-m:最短使用期限
	-M:最长使用期限
	-W:警告时间

权限管理：
r:
	文件:可以使用cat,more或其他命令来查看其内容 
	目录:可以对此目录使用ls命令，但不能切换（cd）进此目录,也不能使用ls -l
w:	
	文件：可以编辑、删除此文件
	目录：可以在此目录中创建文件
x:
	文件：可以执行，可以提交给内核来判断其执行方式，并且将其运行起来或者为之启用一个新的进程
	目录：可以对其使用cd或者ls -l来查看里面每一个文件的详细属性信息

三类用户：
	u:user
	g:group
	o:除了u、g之外的其他用户

chown:改变文件属主
# chown USERNAME file,...
	-R:修改目录及其内部文件的属主
	--reference=/path/to/somefile file,...
chown USERNAME:GRPNAME file,...
chown :GRPNAME file,...(只改变文件的属组，注意前面要带上:)
chown USERNAME.GRPNAME file,...

chgrp:改变文件属组
#chgrp USERNAME file,...

chgrp:修改文件的权限

修改三类用户的权限
	chmod MODE file,...
		-R
		--reference=/path/to/somefile file,...
修改某类用户或者某些类用户权限
	u,g,o,a
	chmod 用户类别=MODE file,...
修改某类的用户某位或某些位权限
	chmod u-x /tmp/abc
	chmod u+x,g-x /tmp/abc
	chmod a+x /tmp/abc
	chmod -x /tmp/abc
	chmod +x /tmp/abc

练习：
1,新建一个没有家目录的用户openstack
2,复制/etc/skel为/home/openstack
3,改变/home/openstack及其内部文件的属主属组均为openstack
4,/home/opnestack及其内部的文件，属组和其他用户没有任何访问权限

umask:遮罩码
普通文件：666-umask
普通目录：777-umask
->文件默认不可具有执行权限，如果计算得出的权限数值中有执行权限，则权限数值默认+1
# umask
# umask 022

022
002

站在用户登录的角度来说，SHELL的类型
登录式shell:
	正常通常某终端登录
	su - USERNAME
	su -l USERNAME
非登录式shell:
	su USERNAME
	图形终端下打开命令窗口
	自动执行的shell脚本

bash的配置文件：
全局配置
	/etc/profile,/etc/profile.d/*.sh,/etc/banshrc
个人配置
	~/.bash_profile,~/.bashrc

profile类的文件：
	设定环境变量
	定义命令别名

bashrc类的文件：
	设定本地变量
	定义命令别名

登录式shell如何读取配置文件
/etc/profile -->/etc/profile.d/*.sh --> ~/.bash_profile --> ~/.bashrc --> /etc/bashrc

非登录式shell如何配置文件
~/.bashrc --> /etc/bashrc --> /etc/profile.d/*.sh

su - :完全切换，读取用户的环境配置文件
su :半切换，不读取用户的环境配置文件

INPUT设备：
OUTPUT设备：

系统设定
	默认输出设备：标准输出，STDOUT,1
	默认输入设备：标准输入，STDIN,0
	标准错误输出：STDERR,2

标准输入：键盘
标准输出和错误输出：显示器

I/O重定向：

Linux:
>:覆盖输出
>>:追加输出

set -C:禁止对已经存在文件使用覆盖重定向
	强制覆盖输出，则使用>|
set +C:关闭上述功能

2>:重定向错误输出
2>>:追加方式

&>:重定向标准输出或错误输出至同一个文件

<:输入重定向
<<:Here Document

管道：
passwd --stdin

文件查找：
locate:
	非实时，模糊匹配，查找是根据全系统文件数据库进行的
#updatedb,手动生成文件数据库

find:
	实时
	精确
	支持众多查找标准
	遍历指定目录中的所有文件完成查找，速度慢

find查找路径 查找标准 查找到以后的处理运作

	查找路径：默认为当前目录
	查找标准：默认为指定路径下的所有文件
	处理运作：默认为显示

匹配标准：
-name 'FILENAME':对文件名作精确匹配
	文件名通配：
		*:任意长度的任意字符
		?:
		[]
	-iname 'FILENAME':文件名匹配时不区分大小写
	-regex PATTERN:基于正则表达式进行文件名匹配
	-user USERNAME
	-group GROUPNAME
	-uid UID:根据UID查找
	-gid GID:根据GID查找
	-nouser:查找没有属主的文件
	-nogroup:查找没有属组的文件
-type
	f:普通文件
	d
	c
	b
	l
	p
	s
-size
	[+|-]
	#M
	#G
组合条件：
-a
-o
-not

-mtime
-ctime
-atime

-perm MODE:精确匹配
	/MODE:任意一位匹配即可满足条件
	-MODE：文件权限能完全包含此MODE时才符合条件

	-644
	644:rw-r--r--
	755:rwxr-xr-x
	750:rwxr-x---
	find ./ -perl -001
动作:
	-print:显示
	-ls:类似ls -l的形式显示每一个文件的详细
	-ok COMMAND {} \;每一次操作都需要用户确认
	-exec COMMAND {} \;

特殊权限
passwd:s

SUID:运行某程序时，相应进程的属主是程序文件自身的属主，而不是启动者
	chmod u+s FILE
	chmod u-s FILE
	如果FILE本身原来就有执行权限，则SUID显示为s;否则显示s
SGID:运行某程序时，相应进程的属组是程序文件自身的属组，而不是启动者所属的基本组
	chmod g+s FILE
	chmod g-s FILE
	develop team,hadoop,hbase,hive
	/tmp/project/
	develop
Sticky:在一个公共目录，每个都可以创建文件，删除自己的文件，但不能删除别人的文件
	chmod o+t DIR
	chmod o-t DIR
	000
	001
	...
	110
	111
	chmod 5755 /backup/test
	umask 0022
	umask

几个命令：
w
who
每隔5秒钟，就来查看hadoop是否已经登录，如登录，显示用户登录历史及系统重启历史

sleep

whoami

last,显示/var/log/wtmp文件，显示用户登录历史及系统重启历史
	-n #:显示最近#次的相关信息
lastb,显示/var/log/btmp文件，显示用户错误的登录尝试
	-n #:显示最近#次的相关信息
lastlog,显示每一个用户最近一次的成功登录信息
	-u USERNAME:显示特定用户最近的登录信息

basename
	$0:执行脚本时的脚本路径及名称
mail

hostname:显示主机名

如果当前主机的主机名不是www.magedu.com,就将其改为www.magedu.com
如果当前主机的主机名是localhost,就将其改为www.magedu.com
如果当前主机的主机名为空，或者为（none）,或者为localhost，就将其改名为www.magedu.com
[ -z `hostname` ] || [ `hostname` == '(none)' -o `hostname` == 'localhost' ] && hostname www.magedu.com

生成随机数
RANDOM:0-32768

终端类型：
	console:控制台
	pty:物理终端
	tty#:虚拟终端
	ttys#:串行终端
	pts/#:伪终端

ln [-s -v] SRC DEST
硬链接：
	1，只能对文件创建，不能应用于目录
	2，不能跨文件系统
	3，创建硬链接会增加文件被链接的次数
du
	-s
	-h
df:

链接
设备文件：
	b:按块为单位，随机访问的设备，硬盘
	c:按字符为单位，线性设备，键盘
/dev
	主设备号 (major number)
		标识设备类型
	次设备号 (minor number)
		标识同一种类型中不同设备
mknod
mknod [OPTION] ... NAME TYPE [MAJOR MINOR]
	-m MODE

硬盘设备的设备文件名：
IDE,ATA:hd
SATA:sd
SCSI:sd
USB:sd
	a,b,c,... 来区别同一种类型下的不同设备
IDE:
第一个IDE口：主，从
	/dev/hda,/dev/hdb
第二个IDE口：主，从
	/dev/hdc,/dev/hdd

sda,sdb,sdc,...

hda:
	hda1:第一个主分区
	hda2:
	hda3:
	hda4:
	hda5:第一个逻辑分区
查看当前系统识别了几块硬盘：
fdisk -l [/dev/to/some_device_file]
管理磁盘分区：
fdisk /dev/sda
p:显示当前硬件的分区，包括没保存的改动
n:创建新分区
d:删除一个分区
w:保存退出
q:不保存退出
t:修改分区类型
	L:
l:显示所支持的所有类型

partprobe


文件系统管理
重新创建文件系统会损坏原有文件
mkfs:make file system
	-t FSTYPE
mkfs -t ext2 = mkfs.ext2
mkfs -t ext3 = mkfs.ext3

专门管理ext系列文件：
mke2fs
-j:创建ext3类型文件系统
-b BLOCK_SIZE:指定块大小，默认为4096,可用取值为1024,2048或4096
-L LABEL:指定分区卷标
-m #:指定预留给超级用户的块数百分比
-i #:用于指定为多少字节的空间创建一个inode，默认为8192,这里给出的数值应该为块大小的2^n倍
-N #:指定inode个数
-F:强制创建文件系统
-E:用户指定额外文件系统属性
blkid:查询或查看磁盘设备的相关属性
	UUID
	TYPE
	LABEL
e2label:用于查看或定义卷标
	e2label 设备文件 卷标：设定卷标	
tune2fs:调整文件系统的相关属性
	-j:不损害原有数据，将ext2升级为ext3
	-L LABEL:设定或修改卷标
	-m #:调整预留百分比
	-r #:指定预留块数
	-o:设定默认挂载选项
		acl
	-c #:指定挂载次数达到#次之后进行自检，0或-1表示关闭此功能
	-i #:每挂载使用多少天后进行自检，0或-1表示关闭此功能
	-l:显示超级块中的信息

dumpe2fs:显示文件属性信息
	-h:只显示超级块中的信息

fsck:检查并修复linux文件系统
	-t FSTYPE:指定文件系统类型
	-a:自动修复

e2fsck:专用于修复ext2/ext3文件系统
	-f:强制检查
	-p:自动修复
挂载：将新的文件系统关联至当前根文件系统
卸载：将某文件系统与当前根文件系统的关联关系预以移除
mount:挂载
mount 设备 挂载点
	设备：
		设备文件：/dev/sda5
		卷标：LABEL=""
		UUID:UUID=""
	挂载点：目录
		要求：
			1，此目录没有被其他进程使用
			2，目录得事先存在
			3，目录中的原有文件将会暂时隐藏

mount:显示当前系统已经挂载的设备及挂载点

mount [options] [-o options] DEVICE MOUNT_POINT
	-a:表示挂载/etc/fstab文件中定义的所有文件系统
	-n:默认情况下，mount命令每挂载一个设备，都会把挂载的设备信息保存至/etc/mtab文件
	-t FSTYPE:指定正在挂载设备上的文件系统类型，不使用此选项时，mount会调用blkid命令获取对应文件系统的类型
	-r:只读挂载，挂载光盘时常用此选项
	-w:读写挂载
	-o:指定额外的挂载选项，也即指定文件系统启用的属性
		remount:重新挂载当前文件系统
		ro:挂载为只读
		rw:读写挂载

挂载完成后，要通过挂载点访问对应文件系统上的文件

umount:卸载某文件系统
	umount 设备
	umount 挂载点
	卸载注意事项：
		挂载的设备没有进程使用

创建交换分区:
mkswap /dev/sda8 
	-L LABEL
swapon /dev/sda8
	-a:启用所有定义在/etc/fstab文件中的交换设备
swapoff /dev/sda8
回环设备
loopback,使用软件来模拟实现硬件
创建一个镜像文件，120G
dd命令：
	if=数据来源
	of=数据存储目标
	bs=1
	count=2
seek=#:创建数据文件时，跳过的空间大小
dd if=/dev/sda of=/mnt/usb/mbr.backup bs=512 count=1
dd if=/mnt/usb/mbr.backup of=/dev/sda bs=512 count=1
dd if=/dev/zero of=/var/swapfile bs=1M count=1024
/dev/null
mount命令，可以挂载iso镜像
mount DEVICE MOUNT_POINT
	-o loop:挂载本地回环设备
wget ftp://172.16.0.1/pub/isos/rhci-5.8-1.iso

mount /dev/sda5 /mnt/test

文件系统的配置文件/etc/fstab
	OS在初始时，会自动挂载此文件中定义的每个文件系统
要挂载的设备	挂载点		文件系统类型	挂载选项	转储频率（每多少天做一次完全备份）		文件系统检测次序（只有根可以为1）
/dev/sda5	/mnt/test	ext3		defaults	0				0

mount -a:挂载/etc/fstab文件中定义的所有文件系统

fuser:验证进程正在使用的文件或套接字文件
	-v: 查看某文件上正在运行的进程
	-k: kill
	-m: mount_point
	fuser -km MOUNT_POINT:终止正在访问此挂载点的所有进程
文件系统访问控制列表
setfacl
	-b   Remove all
	-m
	-x

压缩、解压缩命令
压缩格式：gz,bz2,xz,zip,Z

压缩算法：算法不同，压缩比也会不同
compress: FILENAME.Z
uncompress

gzip: .gz
	gzip /PATH/TO/SOMEFILE:压缩完成后会删除原文件
		-d:
		-#:1-9,指定压缩比，默认为:6
gunzip:
	gunzip /PATH/TO/SOMEFILE.gz:解压完成后会删除原文件
zcat /PATH/TO/SOMEFILE.gz: 不解压的情况，查看文本文件的内容

bzip2: .bz2
比gzip有更大压缩比的压缩工具
xz: .xz

zip:
	zip FILENAME.zip FILE1 FILE2 ...，既能归档又能压缩
	unzip FILENAME.zip
archive:归档，归档本身并不意味着压缩tar

tar:归档工具，.tar
	-c:创建归档文件
	-f:FILE.tar:操作的归档文件
	-x:展开归档
	--xattrs:归档时，保留文件的扩展属性信息
	-t:不展开归档，直接查看归档了哪些文件
	
	-zcf:归档并调用gzip压缩
	-zxf:调用gzip解压缩并展开归档
	
	-jcf:调用bzip2
	-jxf:
	
	-Jcf:调用xz
	-Jxf:

RAID:

级别：仅代表磁盘组织方式不同，没有上下之分
0:	条带
	性能提升：读，写
	冗余能力：无（容错能力）
	空间利用率：nS
	至少需要两块
1:	镜像
	性能表现：写性能下降，读性能提升
	冗余能力：有
	空间利用率：1/2
	至少需要两块
2:
3:
4:
5:
	性能表现：读，写提升
	冗余能力：有
	空间利用率：(n-1)/n
	至少需要3块
10:
	性能表现：读，写提升
	冗余能力：有
	空间利用率1/2
	至少需要4块
01:
	性能表现：读，写提升
	冗余能力：有
	空间利用率1/2
	至少需要4块
50:
	性能表现：读，写提升
	冗余能力：有
	空间利用率(n-2)/n
	至少需要6块
jbod:
	性能表现：无提升
	冗余能力：无
	空间利用率：100%
	至少需要两块

逻辑RAID
/dev/md0
/dev/md1

md
mdadm:将任何块设备做成RAID
模式化的命令：
	创建模式
		-C
			专用选项：
				-l:级别
				-n:设备个数
				-a { yes | no }：自动为其创建设备文件
				-c:CHUNK大小
	管理模式
		--add,--del
	监控模式
		-F
	增长模式
		-G
	装配模式
		-A

查看RAID阵列的详细信息
madam -D /dev/md#
	--detail
停止阵列：
	madam -S /dev/md#
	--stop

watch:周期性地执行指定命令，并以全屏方式显示结果
	-n #:指定周期长度，默认为2,单位为秒
	watch -n # 'COMMAND'
mke2fs:指定条带大小

路由

Linux:网络属于内核的功能

RHEL5: /etc/modprobe.conf
alias

RHEL6: /etc/udev/rules.d/70-persitent-net.rules

网络服务：
RHEL5: /etc/init.d/network {start|stop|restart|status}
RHEL6: /etc/init.d/NetworkManager {start|stop|restart|status}
网关：
route
	add:添加
		-host:主机路由
		-net:网络路由
			-net 0.0.0.0
route add -net|-host| DEST gw NEXTHOP
route add default gw NEXTHOP

	del:删除
	-host
	-net
	route del -net 10.0.0.0/8
	toute del -net 0.0.0.0
	route del default
	
	以上命令做出的改动重启网络服务或主机后失效
	
查看：
	route -n:以数字形式显示各主机或端口等相关信息
网络配置文件：
/etc/sysconfig/network
网络接口配置文件：
/etc/sysconfig/network-scripts/ifcfg-INTERFACE_NAME

DEVICE=:关联的设备名称，要与文件名的后半部“INTERFACE_NAME”保持一致
BOOTPROTO={static|none|dhcp|bootp}：引导协议，要使用静态地址，使用static
IPADDR=:IP地址
NETMASK=:子网掩码
GATEWAY=:设定默认网关
ONBOOT=:开机时是否自动激活此网络接口
HWADDR=:硬件地址，要与硬件中的地址保持一致
USERCTL={yes|no}:是否允许普通用户控制此接口
PEERDNS={yes|no}:是否在BOOTPROTO为dhcp时接受由DHCP服务器指定的DNS地址

不会立即生效，但重启网络服务或主机都会生效

路由：
/etc/sysconfig/network-scripts/route-ethX
添加格式一：
DEST	via	NEXTHOP
添加格式二：
ADDRESS0=
NETMASK0=
GATEWAY0=

DNS服务器指定方法只有一种：
/etc/resolve.conf
nameserver DNS_IP_1
nameserver DNS_IP_2

指定本地解析：
/etc/hosts

主机IP		主机名			主机别名
172.16.0.1	www.example.com		www

配置主机名：
hostname HOSTNAME

立即生效，但不是永久有效

/etc/ysconfig/network
HOSTNAME=

ip
	link:网络接口属性
	addr:协议地址
	route:路由
link
	show
		ip -s link show
	set
		ip link set DEV {up|down}
	addr
一块网卡可以使用多个地址：
网络设备可以别名：
etho
	ethX:Y,eth0:0,eth0:1
配置方法：
	ifconfig ethX:X IP/NETMASK
	/etc/sysconfig/network-scripts/ifcfg-ethX:Y
	DEVICE-ethX:Y
	
	非主要地址不能使用DHCP动态获取
/boot
/etc
/usr
/var
/dev
/lib
/tmp
/bin
/sbin
/proc
/sys
/mnt
/media
/home
/root
/misc
/opt
/srv

/usr/share/man
/etc,/bin /sbin, /lib
	系统启动就需要用到的程序，这些目录不能挂载额外的分区，必须在根文件系统的分区上
/proc /sys：
	不能单独分区，默认为空
/dev：
	设备，不能单独分区
/root：
	不能单独分区
/var：
	建议单独分区
/boot:内核,initrd(initramfs)
	内核：
软件包管理器的核心功能：
1，制作软件包
2，安装，卸载，升级，查询，校验

Redhat,SUSE,Debian

Redhat,SUSE:RPM
	Redhat Package Manager
	RPM is Package Manager
Debian:dpt

依赖关系

前端工具：
后端工具：RPM,dpt

yum: Yellowdog Update Modifier
rpm命令：
	rpm:
		数据库：/var/lib/rpm
	rpmbuild:

安装，查询，卸载，升级，校验，数据库的重建等工作

rpm命名：
包：组成部分
	主包：
		bind-9.7.1-1.el5.i586.rpm
	子包：
		bing-libs-9.7.1-1.el5.i586.rpm
		bind-utils-9.7.1-1.el5.i586.rpm
包名格式：
	name-version-release.arch.rpm
	bind-major.minor.release-release.arch.rpm

主版本号：重大改进
次版本号：某个子功能发生重大变化
发行号：修正了部分bug,调整了一点功能

bind-9.7.1.tar.gz	

rpm包：
	二进制格式
		rpm包作者下载源程序，编译配置完成后，制作成rpm包
		bind-9.7.1-1.noarch.rpm
		bind-9.7.1-1.ppc.rpm
rpm:
1,安装
rpm 	-i /PATH/TO/PACKAGE_FILE
	-h:以#显示进度:每个#表示2%
	-v:显示详细过程
	-vv:更详细的过程，含有debug信息

rpm -ivh /PATH/TO/PACKAGE_FILE
	--nodeps:忽略依赖关系
	--replacepkgs:重新安装，替换原有安装
	--force:强行安装，可以实现重装或降级
2，查询
rpm	-q PACKAGE_NAME:查询指定的包是否已经安装
	-q --scripts PACKAGE_NAME:查询指定包中包含的脚本
	-qa	:查询已安装的所有包
	-qi PACKAGE_NAME:查询指定包的说明信息
	-ql PACKAGE_NAME:查询指定包安装后生成的文件列表
	-qc PACKAGE_NAME:查询指定包安装的配置文件
	-qd PACKAGE_NAME:查询指定包安装的帮助文件
	-qf /path/to/somefile:查询指定的文件是由哪个rpm包生成的

3,升级
rpm -Uvh /PATH/TO/NEW_PACKAGE_FILE:如果装有老版本的，则升级；否则，则安装
rpm -Fvh /PATH/TO/NEW_PACKAGE_FILE:如果装有老版本的，则升级；否则，退出
	--oldpackage:降级
4,卸载
rpm -e PACKAGE_NAME
	--nodeps
5,校验
	rpm -V PACKAGE_NAME
6,重建数据库
	rpm
		--rebuilddb:重建数据库，一定会重新建立
		--initdb:初始化数据库，没有才建立，有就不用建立
7,校验来源合法性，以及软件包完整性
加密类型：
	对称：加密解密使用同一个密钥
	公钥：一对儿密钥，公钥，私钥，公钥隐含于私钥中，可以提取出来，并公开出去
	
# ls /etc/pki/rpm-gpg/

	RPM-GPG-KEY-redhat-release

rpm -K /PAPT/TO/PACKAGE_FILE
	dsa,gpg:验证来源合法性，也即验证签名，可以使用--nosignature,略过此项
	sha1,md5:验证软件包完整性，可以使用--nodigest,略过此项

rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release:导入密钥文件

primary.xml.gz
	所有RPM包的列表
	依赖关系
	每个RPM安装生成的文件列表
filelists.xml.gz
	当前仓库中所以RPM包的所有文件列表
other.xml.gz
	额外信息，RPM包的修改日志

repomd.xml
记录的是上面三个文件的时间戳和检验和

comps*.xml: RPM包分组信息

	{Server,VT,Cluster,ClusterStorage}


如何为yum定义repo文件
	[Repo_ID]
	name=Description
	baseurl=
		ftp://
		http://
		file://
	enabled={1|0}
	gbgcheck={1|0}
	gpgkey=

yum [options] [command] [package ...]

list:列表
	支持glob
	all
	available:可用的，仓库中有但尚未安装的
	installed:已经安装的
	updates:可用的升级

clean:清理缓存

	[ packages | headers | metadata | dbcache | all ]

repolist:显示repo列表及其简要信息
	all
	enabled: 默认
	disabled
install:安装
yum install PACKAGE_NAME

update: 升级
update_to: 升级为指定版本

remove | erase :卸载

info:

provides | whatprovides: 查看指定的文件或特性是由哪个包安装生成的

groupinfo
grouplist
groupinstall
groupremove
groupupdate

/media/cdrom/{Server,VT,Cluster,ClusterStorage}

如何创建yum仓库:
createrepo

http://172.16.0.1/yum/{server,VT}

RPM安装:
	二进制格式:
	源程序-->编译-->二进制格式
		有些特性是编译时就选定的，如果编译未选定此特性，将无法使用
		rpm包的版本会落后于源码包，甚至落后很多：bind-9.8.7,bind-9.7.2
定制:手动编译安装

编译环境，开发环境
开发库，开发工具

Linux: C,
GNU: C

c,c++:
gcc: GNU C Complier,C
g++:

make: 项目管理工具
	makefile: 定义了make (gcc.g++) 按何种次序去编译这些源程序文件中的源程序
automake,--> makefile.in --> makefile
autoconf,--> configure

100个可选择特性
make install

编译安装的三步骤
# tar
# cd
#./configure
	--help
	--prefix=/path/to/somewhere
	--sysconfdir=/PATH/TO/CONFFILE_PATH
	功能：1,让用户选定编译特性 2,检查编译环境
# make
# make install

# tar xf tengine-1.4.2.tar.gz
# cd tengine.1.4.2
# ./configure --prefix=/usr/local/tengine --conf-path=/etc/tengine/tengine.conf
# make
# make install


# /usr/local/tengine/sbin/nginx
1,修改PATH环境变量，以能识别此程序的二进制文件路径
	1，修改/etc/profile文件
	2，在/etc/profile.d/目录建立一个以.sh为名称后缀的文件，在里面定义export PATH=$PATH:/path/to/somewhere
2，默认情况下，系统搜索库文件的路径/lib,/usr/lib;要增添额外搜寻路径
	在/etc/ld.so.conf.d/中创建以.conf为后缀名的文件，而后把要增添的路径直接写至此文件中
	# ldconfig 通知系统重新搜寻库文件
		-v:显示重新搜寻库的过程
3，头文件：输出给系统
	默认：/usr/include
	增添头文件搜寻路径，使用链接进行：
		/usr/local/tengine/include/	/usr/include
		两种方式：
		ln -s /usr/local/tengine/include/*	/usr/include/
		ln -s /usr/local/tengine/include	/usr/include/tengine
4,man文件路径：安装在--prefix指定的目录下的man目录：/usr/share/man
	1,man -M /PATH/TO/MAN_DIR COMMAND
	2,在/etc/man.config中添加一条MANPATH
netstat命令：
	-r: 显示路由表
	-n: 以数字方式显示

	-t:建立的tcp连接
	-u:显示udp连接
	-l:显示监听状态的连接
	-p:显示监听指定的套接字的进程号与进程名

perl,java,python

进程及作业管理

Uninterruptible sleep:不可中断的睡眠
Interruptible sleep:可中断睡眠

kernel:
init:

COW: Copy On Write,写时复制

100-139:用户可控制
0-99:内核调整
数字越小优先级越高

O：
O(1)
O(N)
O(logn)
O(n^2)
O(2^n)

init：进程号为1

ps:Process State
	system V SysV风格 - 
	BSD
	a:所有与终端有关的进程
	u:
	x:所有与终端无关的进程
进程的分类：
	跟终端相关的进程
	跟终端无关的进程
进程状态：
	D：不可中断的睡眠
	R：运行或就绪
	S：可中断的睡眠
	T：停止
	Z：僵死
	
	<:高优先级进程
	N:低优先级进程
	+：前台进程组中的进程
	l:多线程进程
	s:会话进程首进程

pstree
pgrep
top
vmstat
free
kill
pkill
bg
fg

<:高优先级的进程
N:低优先级的进程
多线程进程
前台进程组中的进程
会话进程的领导者

top:
	M:根据驻留内存大小进行排序
	P:根据CPU使用百分比进行排序
	T:根据累计时间进行排序
	
	l:是否显示平均负载和启动时间
	t:是否显示进行和CPU状态相关信息
	m:是否显示内存相关信息
	
	c:是否显示完整的命令行信息
	q:退出top
	k:终止某个进程
top
	-d:指定延迟时长，单位是秒
	-b:批模式
	-n #:在批模式下，共显示多少批

重要的信号：
1，SIGHUP:让一个进程不要重启，就可以重读其配置文件
2，SIGINT:Ctrl+c:中断一个进程
9，SIGKILL:杀死一个进程
15，SIGTERM:终止一个进程，默认信号

指定一个信号：
	信号号码：kill PID
	信号名称:kill -SIGKILL
	信号名称简写：kill -KILL
kill PID
killall COMMAND

调整nice值：
调整已经启动的进程的nice值
renice -n NI COMMAND

前台作业：占据了命令提示符
后台作业：启动之后，释放命令提示符，后续的操作在后台完成

前台-->后台：
	Ctrl+z:把正在前台的作业送往后台
	COMMAND &:让命令在后台执行
bg:让后台的因为Ctrl+z而停止作业继续运行
	bg [[%]JOBID]

jobs:查看后台的所有作业
	作业号，不同于进程号
		+:命令将默认操作的作业
		-:命令将第二个默认操作的作业
fg:将后台的作业调回前台
	fg [[%]JOBID]

PC: OS(linux)
POST-->BIOS(Boot eSquence)-->MBR(bootloader,446)-->kernel-->initrd-->(ROOTFS)/sbin/init

内核设计风格：
Redhat,SUSE
核心：动态加载 内核模块
内核：/lib/modules/"内核版本号命令的目录"/
vmlinuz-2.6.32
/lib/modules/2.6.32/

5:ramdisk-->initrd
6:ramfs-->initramfs

单内核：Linux (LWP)
	核心：ko(kernel object)
	

	so()

微内核：Windows，Solaris(线程)

启动的服务不同：
	运行级别：0-6
		0:halt
		1:single user mode,直接以管理员身份切入,	s,S,single
		2:multi user mode,no NFS
		3:multi user mode,text mode
		4:reserved
		5:multi user mode,graphic mode
		6:reboot

详解启动过程
	bootloader(MBR)
		LILO:Linux LOader
		GRUB:GRand Unified Bottloader
			Stage1:MBR
			Stage1_5:
			Stage2:/boot/grub/

[root@www ~]# cat /etc/grub.conf 
# grub.conf generated by anaconda
#
# Note that you do not have to rerun grub after making changes to this file
# NOTICE:  You have a /boot partition.  This means that
#          all kernel and initrd paths are relative to /boot/, eg.
#          root (hd0,0)
#          kernel /vmlinuz-version ro root=/dev/mapper/VolGroup-lv_root
#          initrd /initrd-[generic-]version.img
#boot=/dev/sda
default=0 # 设定默认启动的title的编号，从0开始
timeout=5 # 等待用户选择的超时时长，单位是秒
splashimage=(hd0,0)/grub/splash.xpm.gz # 指定grub的背景图片
hiddenmenu	# 隐藏菜单

password redhat
password --md5 PASSWORD

title Red Hat Enterprise Linux (2.6.32-279.el6.x86_64)	# 内核标题，或操作系统名称，字符串，可自由修改
	root (hd0,0)	# 内核文件所在的设备：对grub而言，所有类型硬盘一律为hd#,n hd#,#表示第几个磁盘,最后的n表示对应磁盘的分区
	kernel /vmlinuz-2.6.32-279.el6.x86_64 ro root=/dev/mapper/VolGroup-lv_root rd_NO_LUKS LANG=en_US.UTF-8 rd_NO_MD rd_LVM_LV=VolGroup/lv_swap SYSFONT=latarcyrheb-sun16 crashkernel=auto rd_LVM_LV=VolGroup/lv_root  KEYBOARDTYPE=pc KEYTABLE=us rd_NO_DM rhgb quiet
	# 内核文件路径，及传递给内核的参数
	initrd /initramfs-2.6.32-279.el6.x86_64.img # ramdisk文件路径

查看运行级别：
runlevel:
who -r:
查看内核release号：
	uname -r

安装grub stage1:
# grub
grub> root (hd0,0)
grub> set (hd0)

安装grub第二种方式：
# grub-install --root-directory=/path/to/boot,s_parent_dir /PATH/TO/DEVICE

grub> find
grud> root (hd#,N)
grub> kernel /PATH/TO/KERNEL_FILE
grub> initrd /PATH/TO/ININRD_FILE
grub> boot

Kernel 初始的过程： 
1，设备探测
2，驱动初始化（可能会从initrd（redhat6:initramfs）文件中装载驱动模块）
3，以只读方式挂载根文件系统
4，装载第一个进程init (PID:1)

/sbin/init: (/etc/inittab)
	upstart: ubuntu,d-bus,event-driven
	systemd:
id:runlevels:action:process
id:标识符
runlevels:在哪个级别下运行
action:在什么情况下运行
process:要运行什么程序

[ /etc/inittab ],[ /etc/rc.d/rc.sysinit ]

id:3:initdefault:

si::sysinit:/etc/rc.d/rc.sysinit

ACTION:
initdefault:设定默认运行级别
sysinit:系统初始化
wait:等待级别切换至此级别时执行

/etc/rc.d.rc/sysinit完成的任务
1，激活udev和selinux
2，根据/etc/sysctl.conf文件，来设定内核参数
3，设定系统时钟
4，装载键盘映射
5，启用交换分区
6，设置主机名
7，根文件系统检测，并以读写方式重新挂载
8，激活RAID和LVM设备
9，启用磁盘配额
10，根据/etc/fstab,检查并挂载其他文件系统
11，清理过期的锁和PID文件

for I in /etc/rc3.d/K*;do
	$I stop
done

for I in /etc/rc3.d/S*;do
	$I start
done

##:关闭或启动的优先次序，数据越小越优先被选定
先关闭以K开头的服务，后启动以S开头的服务

 /etc/rc.d/init.d , /etc/init.d

服务类脚本：
	start

	SysV: /etc/rc.d/init.d
		start|stop|restart|status
		reload|configtest

chkconfig
# chkconfig:runlevels SS KK

runlevels: -表示，没有级别默认为S*开头的链接
	当chkconfig命令来为此脚本在rc#.d目录创建链接时，runlevels表示默认创建为S*开头的链接，除此之外的级别默认创建为K*开头的链接
	s后面的启动优先级为SS所表示的数字：K后面关闭优先次序为KK所表示的数字
# description:用于说明此脚本的简单功能：\,续行

chkconfig --list:查看所有独立守护服务的启动设定，独立守护进程
	chkconfig --list SERVICE_NAME

chkconfig -add SERVICE_NAME

chkconfig -del SERVICE_NAME

chkconfig --level RUNLEVELS SERVICE_NAME {on|off}
	如果省略级别指定，默认为2345级别

/etc/rc.d/rc.local:系统最后启动的一个服务，准确说，应该执行的一个脚本

/etc/inittab的任务：
1，设定默认运行级别
2，运行系统初始化脚本
3，运行指定运行级别对应的目录下的脚本
4，设定Ctrl+Alt+Del组合键的操作
5，定义UPS电源在电源故障/恢复时的操作
6，启动虚拟终端（2345级别）
7，启动图形终端（5级别）

守护进程的类型：
	独立守护进程
	xinetd:超级守护进程，代理人
		瞬时守护进程，不需要管理至运行级别


核心：/boot/vmlinuz-version
内核模块(ko):/lib/modules/version/

内核设计：
	单内核
		模块化设计
	微内核
装载模块：
	insmod
	modprobe
www.kernel.org

用户空间访问，监控内核的方式：
/proc, /sys

伪文件系统

/proc/sys:此目录中的文件很多是可写的
/sys/:某些文件可写

设定内核参数值的方法：
echo VALUE > /proc/sys/TO/SOMEFILE
sysctl -w kernel.hostname=

能立即生效，但无法永久生效

永久有效：/etc/sysctl.conf
修改文件完成之后，执行如下命令可立即生效
sysctl -p
sysctl -a:显示所有内核参数及其值

内核模块管理：
lsmod:查看
modprobe MOD_NAME:装载某模块
modprobe -r MOD_NAME
modeinfo MOD_NAME:查看模块的具体信息
insmod /PATH_TO_MODULE_FILE:装载模块，需要指定模块路径
rmmod MOD_NAME
depmod /PATH_TO_MODULES_DIR:

内核中的功能除了核心功能之外，在编译时，大多功能都有三种选择：
1，不使用此功能
2，编译成内核模块
3，编译进内核

如何手动编译内核：
make gconfig:Gnome桌面环境使用，需要安装图形开发库组，Gnome Software Development
make kconfig:KDE桌面环境使用，需要安装图形开发库

make menuconfig:

make
make modules_install
make install

screen命令：
screen -ls:显示已经建立的屏幕
screen:直接打开一个新的屏幕
Ctrl+a,d:拆除屏幕
screen -r ID:还原回某屏幕
exit:退出

二次编译时清理，清理前如果有需要，请备份配置文件.config:
make clean
make mrproper

grub-->kernel-->initrd-->ROOTFS(/sbin/init,/bin/bash)

mkinitrd initrd文件路径 内核版本号

mkinitrd /boot/initrd-`uname -r`.img `uname -r`


__________________________________________________________________
__________________________________________________________________


系统安装过程：
anaconda: stage2.img

text, GUI

kickstart: 三部分
命令段：

	必备命令
		keyboard us
		lang
		timezone
		rootpw --iscripted
		selinux --disabled --permissive
		authconfig --useshadow
		bootloader --location
		clearpart --initlabel --linux
		firewall --disabled
		firstboot --disabled
		text|graphical
		key --skip
	可选命令

软件包选择段， %packages
脚本段
	%pre
	%post

ks=http://
ks=cdrom://

安装过程中，boot提示符中可以使用的命令：
	askmethod
	dd

	ip=
	netmask=
	gateway=
	dns=
	
	ks=
	
	rescue:进入紧急救援模式

mkisofs -R -b isolinux/isolinux.bin -no-emul-boot -boot-load-size 4 -boot-info-table -o boot.iso iso/

常见的系统故障排除：

1，确定问题的故障特征
2，重现故障
3，使用工具收集进一步的信息
4，排除不可能的原因
5，定位故障：
	从简单的问题入手
	一次尝试一种方式

1，备份原文件
2，尽可能借助于工具

可能会出现的故障：

1，管理员密码忘记
2，系统无法正常启动
	a,grub损坏（MBR损坏，grub配置文件丢失）
	b,系统初始化故障（某文件系统无法正常挂载，驱动不兼容等）
		grub: 编辑模式
		emergency
	c,服务故障
	d,用户无法登录系统（mingetty,bash程序故障）
3，命令无法运行.export PATH=/data/bin
	退出当前登录，另启终端，重新登录
4，编译过程无法继续（开发环境缺少基本组件）

MBR损坏：
1，借助别的主机修复
2，使用紧急救援模式
	a,boot.iso
	b,使用完整的系统安装光盘
	boot:Linux rescue
		/mnt/sysimage

grub配置文件丢失：

grub> root (hd0,0)
grub> kernel /vmlinuz- ro root=/dev/vol0/root rhgb quiet
grub> initrd /initrd-
grub> boot

grub.conf

default=0
timeout=10
title RHEL 5.8
	root (hd0,0)
	kernel /vmlinuz-2.6.18-308.el5 ro root=/dev/vol0/root quiet
	initrd /

kernel panic:内核恐慌

另外的故障：
	把默认级别设定为0或6: -->进入单用户模式，编辑inittab文件
	/etc/rc.d/rc3.d -->进入单用户模式，修改目录系统
	某个服务故障导致启动停止，如sendmail配置文件时间戳检查无法通过 -->进入交互式模式















