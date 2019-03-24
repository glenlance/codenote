bootstrap
    元素颜色
        primary
        secondary
        success
        danger
        warning
        info
        light
        dark
        muted
        white

    文本样式
        font-weight-normal: 字体不加粗
        display-4:字体大小，区别于<h1> <h2> 用于高亮显示
        bg-light: 背景色是light
        text-center: 文本居中
        text-left/right: 文本左右对齐
        bg-dark/text-white: 背景色是深色，前景色是白色
    英文转换
        text-lowercase
        text-uppercase
        text-capitalize 首字母大写
    元素Size变更
        w-*: 宽度%的设定，w-25:表示占父元素25%宽度
        h-*: 高度%的设定，h-25:表示占父元素25%高度

    padding和margin的使用

        p:padding: 叫做余白
        m:margin: 边框
        location: 上下左右，
        size: 表示尺寸

        * [p|m][location]-[size]

        location:
            t,b,l,r
                t:top
                b:bottom
                l:left
                r:right
            x,y
                x:lr:表示左右,left/right
                y:tb:表示上下,top/bottom

            
        size:
            0
            1:0.25rem
            2:0.5rem 
            3:1.0rem
            4:1.5rem
            5:3.0rem
            auto

            # rem 是个啥？
                以根元素为基准，按照比例设定子元素的大小的单位
                参考网页：
                https://developer.mozzilla.org/zh-CN/docs/web/css/length

        

        案例：
            <div class="my-container pt-3 pl-3">
                pt-3:表示上余白是3(=1.0rem),pl-3:表示左余白是3

            <div class="bg-primary w-50 h-50 pt-1 pl-2">
                
            <div class="my-container px-3 py-3">
                px-3: 表示左右余白都是3，py-3：表示上下余白都是3

            <div class="bg-success w-100 h-100">

        按钮的各种设定
            btn-*
            <button class="btn btn-primary btn-sm">yes</button> : 分别是btn基础类，btn颜色，btn大小

        网格系统
            col-*
            12列布局
            <div class="container">
                <div class="row mb-3">
                    <div class="col-4 bg-danger">
        
        理解响应式布局
            屏幕大小的的划分
                下面都是根据宽度
                    超小(Extra small)
                        <576px
                        .col-*
                    小(Small)
                        >=576px
                        .col-sm-*
                    中(Medium)
                        >=768px
                        .col-md-*
                    大(Large)
                        >=9920x
                        .col-lg-*
                    超大(Extra large)
                        >=1200px
                        .col-xl-*
        
            课题：基本的在网页上定义行的方式，但还不具备响应式功能：
                <div class="container">
                    <div class="row">
                        <div class="col bg-danger">
            
        制作响应式网页

            col-*
            col-sm-*
            col-md-*
            col-lg-*
            col-xl-*

            Bootstrap has a wide range of responsive margin and padding utility classes. They work for all breakpoints:
            xs (<=576px), sm (>=576px), md (>=768px), lg (>=992px) or xl (>=1200px))
            The classes are used in the format:

            {property}{sides}-{size} for xs & {property}{sides}-{breakpoint}-{size} for sm, md, lg, and xl.

                m - sets margin

                p - sets padding

                t - sets margin-top or padding-top

                b - sets margin-bottom or padding-bottom

                l - sets margin-left or padding-left

                r - sets margin-right or padding-right

                x - sets both padding-left and padding-right or margin-left and margin-right

                y - sets both padding-top and padding-bottom or margin-top and margin-bottom

            blank - sets a margin or padding on all 4 sides of the element

                0 - sets margin or padding to 0

                1 - sets margin or padding to .25rem (4px if font-size is 16px)

                2 - sets margin or padding to .5rem (8px if font-size is 16px)

                3 - sets margin or padding to 1rem (16px if font-size is 16px)

                4 - sets margin or padding to 1.5rem (24px if font-size is 16px)

                5 - sets margin or padding to 3rem (48px if font-size is 16px)

                auto - sets margin to auto

                https://getbootstrap.com/docs/4.0/utilities/spacing/

                <div class="row">
                    <div class="col-12 col-md-6 bg-danger">
                    <div class="d-none d-md-block col-md-6 bg-primary">

                    mb-3 : 表示margin-bottom=3
                    lang="zh-cmn-Hans"
                    name="viewport" 意思是多屏幕的显示
            
            特殊section的使用
                section标记
            完成特殊section
                实现响应式布局
                col-md-*
                order-md-*



bootstrap 3

    媒体对象
        https://v3.bootcss.com/components/#media
    
        .media
        .media-left
        .media-object
        .media-body
        .media-heading
        .media-right
        .media-top | middle | bottom

            <div class="media">
                <div class="media-left">
                    <a href="#">
                    <img class="media-object" src="..." alt="...">
                    </a>
                </div>
                <div class="media-body">
                    <h4 class="media-heading">Media heading</h4>
                    ...
                </div>
            </div>

    列表组

        list-group
        list-group-item
        list-group-item-color:

            color: success, info, danger, ...

            <ul class="list-group">
            <li class="list-group-item">Cras justo odio</li>
            <li class="list-group-item">Dapibus ac facilisis in</li>
            <li class="list-group-item">Morbi leo risus</li>
            <li class="list-group-item">Porta ac consectetur ac</li>
            <li class="list-group-item">Vestibulum at eros</li>
            </ul>

            徽章列表组：

            <ul class="list-group">
            <li class="list-group-item">
                <span class="badge">14</span>
                Cras justo odio
            </li>
            </ul>

            链接列表组：

            <div class="list-group">
            <a href="#" class="list-group-item active">
                Cras justo odio
            </a>
            <a href="#" class="list-group-item">Dapibus ac facilisis in</a>
            <a href="#" class="list-group-item">Morbi leo risus</a>
            <a href="#" class="list-group-item">Porta ac consectetur ac</a>
            <a href="#" class="list-group-item">Vestibulum at eros</a>
            </div>

            按钮列表组：

            <div class="list-group">
            <button type="button" class="list-group-item">Cras justo odio</button>
            <button type="button" class="list-group-item">Dapibus ac facilisis in</button>
            <button type="button" class="list-group-item">Morbi leo risus</button>
            <button type="button" class="list-group-item">Porta ac consectetur ac</button>
            <button type="button" class="list-group-item">Vestibulum at eros</button>
            </div>

            被禁用：

            <div class="list-group">
            <a href="#" class="list-group-item disabled">
                Cras justo odio
            </a>
            <a href="#" class="list-group-item">Dapibus ac facilisis in</a>
            <a href="#" class="list-group-item">Morbi leo risus</a>
            <a href="#" class="list-group-item">Porta ac consectetur ac</a>
            <a href="#" class="list-group-item">Vestibulum at eros</a>
            </div>

            情景类列表组：

            <ul class="list-group">
            <li class="list-group-item list-group-item-success">Dapibus ac facilisis in</li>
            <li class="list-group-item list-group-item-info">Cras sit amet nibh libero</li>
            <li class="list-group-item list-group-item-warning">Porta ac consectetur ac</li>
            <li class="list-group-item list-group-item-danger">Vestibulum at eros</li>
            </ul>
            <div class="list-group">
            <a href="#" class="list-group-item list-group-item-success">Dapibus ac facilisis in</a>
            <a href="#" class="list-group-item list-group-item-info">Cras sit amet nibh libero</a>
            <a href="#" class="list-group-item list-group-item-warning">Porta ac consectetur ac</a>
            <a href="#" class="list-group-item list-group-item-danger">Vestibulum at eros</a>
            </div>

            定制内容列表组：

            <div class="list-group">
            <a href="#" class="list-group-item active">
                <h4 class="list-group-item-heading">List group item heading</h4>
                <p class="list-group-item-text">...</p>
            </a>
            </div>

    面板

        .panel 
        .panel-primary
        .panel-heading
        .panel-title
        .panel-body
        .panel-footer

            <div class="panel panel-primary">
                <div class="panel-heading">
                    <div class="panel-title">
                        <h1>百度新闻</h1>
                    </div>
                </div>
                <div class="panel-body">
                    <h2>some text</h2>
                    <h2>some text</h2>
                    <h2>some text</h2>
                    <h2>some text</h2>
                    <h2>some text</h2>
                    <h2>some text</h2>
                </div>
                <div class="panel-footer">
                    <p></p>
                </div>
            </div>

        

        把表格和面板结合：

            div class="container">
                <h1 class='page-header'>Bootstrap框架</h1>
                <div class="col-md-6">
                    <div class="panel panel-info">
                        <div class="panel-heading">
                            <div class="panel-title">
                                <span><b>百度新闻</b></span>
                            </div>
                        </div>
                        <div class="panel-body">
                        <table class='table table-striped table-hove table-bordered'>
                        <tr>
                            <th>id</tr>
                            <th>username</th>
                            <th>password</th>
                        </tr>
                            (tr>td{$$$}*3)*5
                            <tr>
                                <td>001</td>
                                <td>002</td>
                                <td>003</td>
                            </tr>
                            <tr>
                                <td>001</td>
                                <td>002</td>
                                <td>003</td>
                            </tr>
                            <tr>
                                <td>001</td>
                                <td>002</td>
                                <td>003</td>
                            </tr>
                            <tr>
                                <td>001</td>
                                <td>002</td>
                                <td>003</td>
                            </tr>
                            <tr>
                                <td>001</td>
                                <td>002</td>
                                <td>003</td>
                            </tr>
                        </table>
                        </div>  // 把panel-body 包的这一层去掉就可以无缝对接了

                    </div>
                </div>
            </div>

            如果嫌弃<h*> 标签字体太大，可以用<span><b>text</b></span>

        well
        well-lg
        well-sm

        取消bootstrap的响应式：
            .container{
            width: 970px !important;
            max-width: none !important;
        }

    移动设备优先

        为了确保适当的绘制和触屏缩放，需要在 <head> 之中添加 viewport 元数据标签。

        <meta name="viewport" content="width=device-width, initial-scale=1">

        在移动设备浏览器上，通过为视口（viewport）设置 meta 属性为 user-scalable=no 可以禁用其缩放（zooming）功能。这样禁用缩放功能后，用户只能滚动屏幕，就能让你的网站看上去更像原生应用的感觉。注意，这种方式我们并不推荐所有网站使用，还是要看你自己的情况而定！

        <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">

    
    布局容器

        .container 类用于固定宽度并支持响应式布局的容器。

            <div class="container">
            </div>
            .container-fluid 类用于 100% 宽度，占据全部视口（viewport）的容器。

            <div class="container-fluid">
            </div>

    栅格系统

        bootstrap里面的内外边距最喜欢用15px 这个值

        col-md-4 col-md-offset-4 : offset 表示空四个位置

        通过使用.col-md-push-* 和.col-md-pull-* 类就可以很容易的改变列(column)的顺序。


    引用

        默认样式的引用：

            将任何html元素包裹在<blockquote>中即可表现为引用样式。对于直接引用，我们建议用<p>标签。
            <blockquote>
                <p>Lorem ipsum dolor sit amet.consectetur adipiscing elit. Integer posure erat a ante.</p>
            </blockquote>

    地址：

        <address></address>

    排版：
        1.标题(.page-header)
        2.中心内容
            通过添加 .lead 类可以让段落突出显示。
        3.mark 标记
        4.del 删除线

    列表：

        无样式列表：list-unstyle

        内联列表：<ul class="list-inline">
                    <li>...</li>
                 </ul>
                 通过设置display: inline-block; 并添加少量的内补(padding),将所有元素放置于同一行。

    文本对齐 

        text-left
        text-center
        text-right
        text-justify
        text-nowrap

    表格

        .table
        .table-striped : 给表格隔行加条纹
        .table-bordered : 给原本只是行显示的table添加格子，变成真正的表格
        .table-hover: 给表格添加略过每行时的效果
        .table-condensed

        表格颜色：
            <tr class="info"></tr>
            .info
            .success
            .active
            .warning
            .danger

    按钮

        .btn
        .btn-color
        .btn-link
        .btn-block: 通过给按钮添加.btn-block类可以将其拉伸至父元素100%的宽度，而且按钮也变为了块级(block)元素

        <img src="holder.js/100%x300"></img> : 使用bootstrap 官方提供的holder.js探测位置大小

        用按钮的.btn-block制作用户的个人中心

            <div class="container">
                <h1 class='page-header'>用户个人中心</h1>
                    <div class="row">
                        <div class="col-md-2">
                            <button class='btn btn-primary btn-block'>bs按钮</button>
                            <button class='btn btn-primary btn-block'>bs按钮</button>
                            <button class='btn btn-primary btn-block'>bs按钮</button>
                            <button class='btn btn-primary btn-block'>bs按钮</button>
                            <button class='btn btn-primary btn-block'>bs按钮</button>
                            <button class='btn btn-primary btn-block'>bs按钮</button>
                        </div>
                        
                        <div class="col-md-10">
                            <img src="holder.js/100%x300"></img>
                        </div>
                    </div>

                </div>
            </div>

            有好多元素都可以被做成按钮：

                    <button class='btn btn-primary btn-block btn-lg'>个人信息</button>
                    <a class='btn btn-primary btn-block btn-lg' href=''>个人信息</a>
                    <input type='button' class='btn btn-primary btn-block btn-lg' value='个人信息>
                    <input type='reset' class='btn btn-primary btn-block btn-lg' value='个人信息>

            
        2016.5.24-Bootstrap框架

        Bootstrap学习大纲：
        1.css样式

            1)栅格系统
            2)排版
            3)代码
            4)表格 
            5)表单
            6)按钮 
            7)图片 
            8)辅助类
            9)响应式工具

        2.css组件

            1)glyphicons图标
            2)下拉菜单
            3)按钮组 
            4)输入框组
            5)导航
            6)导航条
            7)路径导航
            8)分页
            9)标签
            10)徽章 
            11)巨幕
            12)页头
            13)缩略图
            14)警告框
            15)进度条
            16)媒体对象
            17)列表组
            18)面板
            19)响应式嵌入内容
            20)Well


        3.js插件

            1)模态框
            2)下拉菜单
            3)滚动监听
            4)标签页
            5)工具提示
            6)弹出框
            7)警告框
            8)按钮 
            9)折叠效果
            10)幻灯片效果
            11)固定侧边栏


        Css样式 

            图片

                <img src="..." alt="..." class="img-rounded"> 方形图片
                <img src="..." alt="..." class="img-circle"> 圆形图片
                <img src="..." alt="..." class="img-thumbnail"> 缩略图 , 图片所在的轮廓加了少量 padding 或者说图片加了margin
            辅助类 
            响应式工具 
            表单 

        
            .container 是页面最大的容器

                <div class="container">
                    <h1 class='page-header'>Bootstrap框架</h1> 标题
                </div>

        文本颜色

            text-muted 哑灰色
            text-color

        背景颜色 

            bg-color

            &times; 转义字符，表示x号

            <span class="close">&times;</span> 给元素添加x号
            <span class="caret">&times;</span> 给元素添加下三角
            <button class="btn btn-primary">更多<span class='caret'></span></button> : 给按钮添加更多
            给元素添加 class="pull-right" 可以把元素拉到父元素里面的右边位置

        快速浮动

            通过添加一个类，可以将任意元素向左或向右浮动。!important 被用来明确 CSS 样式的优先级。这些类还可以作为 mixin（参见 less 文档） 使用。

            <div class="pull-left">...</div>
            <div class="pull-right">...</div>
            // Classes
            .pull-left {
            float: left !important;
            }
            .pull-right {
            float: right !important;
            }

            // Usage as mixins
            .element {
            .pull-left();
            }
            .another-element {
            .pull-right();
            }

                不能用于导航条组件中
                排列导航条中的组件时可以使用这些工具类：.navbar-left 或 .navbar-right 。 参见导航条文档以获取更多信息。


            让内容块居中

                为任意元素设置 display: block 属性并通过 margin 属性让其中的内容居中。下面列出的类还可以作为 mixin 使用。

                <div class="center-block">...</div>
                // Class
                .center-block {
                display: block;
                margin-left: auto;
                margin-right: auto;
                }

                // Usage as a mixin
                .element {
                .center-block();
                }

            清除浮动

                通过为父元素添加 .clearfix 类可以很容易地清除浮动（float）。这里所使用的是 Nicolas Gallagher 创造的 micro clearfix 方式。此类还可以作为 mixin 使用。

                <!-- Usage as a class -->
                <div class="clearfix">...</div>
                // Mixin itself
                .clearfix() {
                &:before,
                &:after {
                    content: " ";
                    display: table;
                }
                &:after {
                    clear: both;
                }
                }

                // Usage as a mixin
                .element {
                .clearfix();
                }

            元素居中

                有两种方式：
                    1. margin:0,auto
                    2. class="center-block"

            元素隐藏显示

                class="hide"
                class="show"

            下拉菜单 

                .dropdown
                .dropup
                .dropdown-menu
                .dropdown-menu-left/right
                .dropdown-header
                .divider
                [data-toggle="dropdown"]
            


                <div class="container">
                    <h1 class='page-header'>Bootstrap框架</h1>
                    <div class="dropdown pull-right">
                        <button class="btn btn-primary" date-toggle="dropdown">更多课程<span class="caret"></span></button>

                        <ul class='dropdown-menu dropdown-menu-right">
                            <li class='dropdown-header'>周一事项</li>
                            <li><a href="">百度</a></li>
                            <li><a href="">百度</a></li>
                            <li class='divider'></li>
                            <li class='dropdown-header'>周二事项</li>
                            <li><a href="">百度</a></li>
                            <li><a href="">百度</a></li>
                        </ul>
                    </div>
                </div>

            按钮组 

                .btn
                .btn-group
                .btn-toolbar
                .btn-group-lg 
                .btn-group-vertical
                .dropdown-toggle 
                .btn-group-justified : 两端对齐按钮组
                <div class="btn-group">
                    <button class="btn btn-info'>百度</button>
                    <button class="btn btn-info'>百度</button>
                    <button class="btn btn-info'>百度</button>
                    <button class="btn btn-info'>百度</button>
                    <button class="btn btn-info'>百度</button>
                </div>

                两端对齐按钮组

                    <div class="btn-group btn-group-justified" role="group" aria-label="...">
                    <div class="btn-group" role="group">
                        <button type="button" class="btn btn-default">Left</button>
                    </div>
                    <div class="btn-group" role="group">
                        <button type="button" class="btn btn-default">Middle</button>
                    </div>
                    <div class="btn-group" role="group">
                        <button type="button" class="btn btn-default">Right</button>
                    </div>
                    </div>

            表单

                登录表单

                        <div class="col-md-8">
                            <form action="">
                                <div class="from-group">
                                    <label for="">用户名：</label>
                                    <input type="text" class='form-control'>
                                </div>
                        </div>

                        <div class="form-group">
                            <label for="">密码：</label>
                            <input type="text" class="form-control">
                        </div>

                        <div class="form-group">
                            <label for="">留言：</label>
                            <textarea name="" id="" cols="30" rows="10" class='form-control'>
                            </textarea>
                        </div>

                        <div class="form-control">
                            <label for="">城市：</label>
                            <select name="" id="" class="form-control">
                            <option value="">北京</option>
                            <option value="">北京</option>
                            <option value="">北京</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label for="">爱好：</label>
                            <input type="checkbox" name="" id="">篮球
                            <input type="checkbox" name="" id="">篮球
                            <input type="checkbox" name="" id="">篮球
                            <input type="checkbox" name="" id="">篮球
                        </div>

                        <div class="form-group">
                        <label for="">爱好：</label>
                        <div class="checkbox">
                            <label>
                                <input type="checkbox" name="" id="">篮球
                            </label>
                        </div>

                        <div class="form-group">
                            <label for="">文件上传:</label>
                            <input type="file" name="" id="">
                        </div>

                        <div class='form-group'>
                            <input type="submit" value="ok" class="btn btn-primary">
                            <input type="reset" value="cancel" class='btn btn-danger'>
                        </div>
                    
                    
                    class="radio" : 单选框
                        要想单选框只选中一个，名字 name="" 必须相同
                    class="checkbox" : 复选框

                
            内联表单

                在最外层的<form></form>加上 class="form-inline" 表单就会变成内联表单


            输入框组 

                .input-group
                .input-group-addon

            水平表单

                .control-label
                .form-horizontal

            内联多选框/单选框

                .checkbox-inline
                .radio-inline

            下拉列表菜单

                multiple

            静态控件

                .form-contrl-static

                    如果需要在表单中将一行纯文本和label元素放置于同一行，为<p>元素添加.form-control-static 类即可

            禁用/只读表单

                [disabled]: 这个不能讲只读元素的值传递给后端
                [readonly]: 这个可以将只读元素的值传递给后端

                给一组元素设置禁用属性，使用<fieldset></fieldset>把这一组元素包起来，然后给这个fieldset设置禁用

                    <filedset>
                        <legend></legend>
                    </fieldset>

            表单校验状态

                .has-success
                .has-warning
                .has-error
                .has-feedback
                .glyphicon
                .glyphicon-ok
                .glyphicon-warning-sign 
                .glyphicon-remove 
                .form-control-feedback
                .input-lg
                .help-block
                只有这三种
                上面三种属性后面加上.has-feedback 然后再配合 <span class="glyphicon glyphicon-ok form-control-feedback"></span> 可以给每种校验状态添加对应的图标
                可以用.help-block 为表单校验状态添加辅助文本

            表单大小

                class='form-control input-lg'

                用栅格系统中的列(column)包裹输入框或其任何父元素，都可以很容易的为其设置宽度
                    <div class="row">
                    <div class="col-xs-2">
                        <input type="text" class="form-control" placeholder=".col-xs-2">
                    </div>
                    <div class="col-xs-3">
                        <input type="text" class="form-control" placeholder=".col-xs-3">
                    </div>
                    <div class="col-xs-4">
                        <input type="text" class="form-control" placeholder=".col-xs-4">
                    </div>
                    </div>

            输入框组

                .input-group 
                .input-group-addon 
                .input-group-lg
                .input-group-btn 

                输入框组嵌入多选框
                输入框组嵌入单选框
                输入框组嵌入按钮 .input-group-btn
        
        导航 

            .nav 
            .nav-tabs ：标签式导航
            .nav-pills ：胶囊式导航
            .nav-stacked ：垂直堆叠式导航
            .navbar 
            .navbar-default : 默认白色导航条
            .navbar-inverse : 默认反色导航条
            .navbar-header
            .navbar-brand
            .navbar-toggle collapsed data-toggle='collapsed' data-target='#mynavbar'
            .icon-bar 
                class="collapse navbar-collapse"
            .navbar-nav
            .navbar-right

        footer

            <footer class="footer">
                <div class="container">
                        <div class="row">
                                <div class="col-12">
                                        <p>2019 fraudig.com</p>
                                </div>
                        </div>
                </div>
            </footer>

        分页

            .pagination
            .pagination-lg
            .pager
            .previous :两端对齐 上下页
            .next

            <nav aria-label="Page navigation">
            <ul class="pagination">
                <li>
                <a href="#" aria-label="Previous">
                    <span aria-hidden="true">&laquo;</span>
                </a>
                </li>
                <li><a href="#">&laquo;</a></li>
                <li><a href="#">1</a></li>
                <li><a href="#">2</a></li>
                <li><a href="#">3</a></li>
                <li><a href="#">4</a></li>
                <li><a href="#">5</a></li>
                <li><a href="#">&raquo;</a></li>
                <li>
                <a href="#" aria-label="Next">
                    <span aria-hidden="true">&raquo;</span>
                </a>
                </li>
            </ul>
            </nav>

            向左箭头：&laquo
            向右箭头：&raquo 


        标签 
            .label 
            .label-default 

        徽章 
            .badge

        巨幕 
            
            .jumbotron
            .thumbnail 

        警告框 

            .alert
            .alert-color 
            .alert-dismissible 

                .close data-dismiss='alert'
            
            警告框中的链接 
                .alert-link 

        进度条 

            .progress-bar 
            .progress-bar-success
            .progress-bar-striped active 

            <div class="progress">
                <div class="progress-bar" style='width:90%'>90%</div>
            </div>

        面板 

            .panel 
            .panel-primary 
            .panel-heading 
            .panel-title 
            .panel-body 
            .panel-footer

        内嵌框架 

            .embed-responsive
            .embed-responsive-16by9
            .embed-responsive-4by3
            .embed-responsive-item 

        well 
            .well 
            .well-lg 
            .well-sm 

    Bootstrap下的jQuery插件 

        模态框：

            .modal-lg 
            

    css: justify-content: center; 可以让用来做分页的 btn-toolbar 居中