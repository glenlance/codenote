vscode 笔记

格式化代码快捷键：
    Windows： Ctrl + K + F
    Windows：Shift + Alt + F
    Mac： Shift + Option + F
    Ubuntu： Ctrl + Shift + I


General

    ctrl+shift+p,f1 打开命令面板
    
    ctrl+p 快速打开，转到文件
    
    ctrl+shift+n 打开新窗口实力
    
    ctrl+, 用户设置
    
    ctrl+k ctrl+s 键盘快捷键
    
    ctrl+x 剪切一行
    
    ctrl+c 复制一行
    
    alt+up/down 向上或者向下移动一行
    
    shift+alt+up/down 向上或者向下复制一行
    
    ctrl+enter 在当前行下一行插入一行
    
    ctrl+shift+enter 在当前行上一行插入一行
    
    ctrl+shift+\ 跳转到对应的括号
    
    ctrl + ]/[ 缩进或取消缩进
    
    home/end 跳转到一行的开始和结尾
    
    ctrl+up/down 向上或者向下滚动行
    
    alt+PgUp/PgDn 向上或者向下滚动页面
    
    ctrl+shift+[ 折叠一个区域
    
    ctrl+shift+] 展开一个区域
    
    ctrl+k ctrl+[ 折叠所有子区域
    
    ctrl+k ctrl+] 展开所有子区域
    
    ctrl+k ctrl+0 折叠所有区域
    
    ctrl+k ctrl+j 展开所有区域
    
    ctrl+k ctrl+c 添加行注释
    
    ctrl+k ctrl+u 移除行注释
    
    ctrl+/ 打开行注释
    
    shift+alt+a 打开块注释
    
    alt+z 打开word wrap

Navigation

    ctrl+t 打开所有所有符号
    
    ctrl+g 跳转到行
    
    ctrl+p 跳转到行
    
    ctrl+shift+O 跳转到符号
    
    ctrl+shift+m 打开问题面板
    
    F8 跳转到下一个错误或者警告
    
    shift+F8 跳转到前一个错误或者警告
    
    ctrl+shift+tab Navigate editor group history
    
    alt+left/right 回去/向前
    
    ctrl+m toggle tab moves focus

Search and replace

    ctrl+F 查找
    
    ctrl+H 替换
    
    f3/shift+f3 查找下一个/上一个
    
    alt+enter 选择所有查找匹配的内容
    
    ctrl+d Add selection to next find match
    
    ctrl+k ctrl+d move last selection to next find match
    
    alt+C/R/W 打开或者 关闭大小写敏感 / regex / whole word

Muti-cursor and selection

    alt+click 插入光标
    
    ctrl+alt+up/down 向上插入光标或者向下插入光标
    
    ctrl+u undo last cursor operation
    
    shift+alt+i 在选中的所有行的末尾插入光标
    
    ctrl+l 选中当前行
    
    ctrl+shift+l 选中当前所选内容的所有匹配项
    
    ctrl+f2 选中当前单词的所有匹配项
    
    shift+alt+left 展开所选内容
    
    shift+alt+right 折叠所选内容
    
    shift+alt+(drag mouse) 列选择
    
    ctrl+shift+alt(arrow key) 列选择
    
    ctrl+shift+alt+PgUp/PgDn 列选择

Rich languages editing

    ctrl+space 触发建议
    
    ctrl+shift+space 触发参数提示
    
    shift+alt+f 格式化文档
    
    ctrl+k ctrl+f 格式化选中内容
    
    f12 跳转到定义
    
    alt+f12 peek definition
    
    ctrl+k f12 在侧边栏打开定义
    
    ctrl+. quick fix 
    
    shift+f12 打开引用
    
    f2 rename symbol
    
    ctrl+k ctrl+x 去掉后面的空格
    
    ctrl+k m 改变文件语言

Editor management

    ctrl+f4, ctrl+w 关闭编辑器
    
    ctrl+k f 关闭文件夹
    
    ctrl+\ 分离编辑器
    
    ctrl+1/2/3 Focus into 1st, 2nd or 3nd editor group
    
    ctrl+k ctrl+left/right Focus into previous/next group
    
    ctrl+shift+PgUp/PgDn 向左/向右移动编辑器
    
    ctrl+k left/right 移动活动的编辑器组

File management 

    ctrl+n 新文件
    
    ctrl+o 打开文件
    
    ctrl+s 保存文件
    
    ctrl+shift+s 保存
    
    ctrl+k s 保存全部
    
    ctrl+f4 关闭
    
    ctrl+k ctrl+w 关闭全部
    
    ctrl+shift+t 重新打开关闭的编辑器
    
    ctrl+k enter 保持编辑器先前打开的编辑器模式
    
    ctrl+tab 打开前一个tab
    
    ctrl+shift+tab 关闭先前的tab
    
    ctrl+k p 复制活动文件路径
    
    ctrl+k r 在资源管理器显示活动文件
    
    ctrl+k o 在新的窗口实例打开活动文件

Display

    f11 开/关 全屏
    
    shift+alt+0 开/关 编辑器布局（水平/垂直）
    
    ctrl+ =/- 放大/缩小
    
    ctrl+b 开/关 侧边栏显示
    
    ctrl+shift+e 显示资源管理器/ 切换目标
    
    ctrl+shift+f 显示搜索
    
    ctrl+shift+g 显示 source control
    
    ctrl+shift+d 显示debug
    
    ctrl+shift+x 显示扩展
    
    ctrl+shift+h replace in files
    
    ctrl+shift+j 开/关搜索详情
    
    ctrl+shift+u 打开输出面板
    
    ctrl+shift+v 打开markdown 预览
    
    ctrl+k v 在侧边打开markdown 预览
    
    ctrl+k z Zen Mode

Debug

    f9 开/关 断点
    
    f5 开始/结束
    
    shift+f5 结束
    
    f11 / shift+f11 步进/步退
    
    f10 单步执行

Integrated

    ctrl+` 显示集成终端
    
    ctrl+shift+` 创建新终端
    
    ctrl+c 复制selection
    
    ctrl+up/down 向上/向下 滚动
    
    shift+PgUp/PgDn 向上/向下 滚动页面
    
    ctrl+home/end 滚动到顶部/底部



##     如何设置 snippet:

​		这里提供了两种方法：

​		1，文件 > 首选项 > 用户代码片段，选择进入目的语言的代码段设置文件；

​		2，通过快捷键 [ ctrl + shift + p ] 打开命令窗口( all command window )，输入[ snippet ]，通过候			  选栏中的选项进入目的语言的代码段设置文件。









