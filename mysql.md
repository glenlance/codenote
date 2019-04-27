数据库设计

    用户表(user)：
    
    id              用户id
    nickname            用户名
    password        密码
    creat_time      注册时间
    email           邮箱

​    举报信息(report)表：
​    
​    id              report_id
​    named           被举报人姓名
​    workplace       工作单位
​    wechat          微信
​    phone_num       手机号码
​    tieba_id        贴吧id，如果有的话
​    taobao2_id      闲鱼id
​    weibo_id        微博id
​    native_placed   被举报人籍贯/或者现今生活所在地          
​    other_social_info    其他社交信息
​    net_address     事件发生网址
​    address         事件发生地理位置
​    relate_people   事件相关人
​    relate_people_workplace 事件相关人工作单位
​    argu_time       事件发生时间
​    report_time     事件举报时间
​    user_id         举报人的用户id

process 事件发生过程







    评论(comment)表：
    
    id              评论id
    user_id         主评人用户id
    follow_user_id  跟评人用户id
    main_comment    主评论
    follow_comment  跟评论
    report_id       主评论所在report的id


​    

数据库操作种类：

User

- 增：创建用户
- 删
- 改
- 查

Report

- 增：创建Report
- 删：删除Report
- 改：修改Report
- 查：查看Report



Comment

- 增：增加评论
- 删
- 改
- 查：查看评论


