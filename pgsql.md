pgsql 安装初始化：

<https://webkul.com/blog/postgresql-windows-installation-problem-running-post-install-step-installation-may-not-complete-correctly/>

- Uninstall PostgreSQL
- Run command: **net user postgres /delete**
- Click: **Control Panel** -> **User Accounts** -> **Configure advanced user profile properties** -> delete all “**Unknown User**” instances that seem to be left from PostgreSQL installation.
- Run command: **net user postgres dbpass /add**
- Run: **compmgmt.msc** -> Click **Local Users and Groups** -> **Users** -> **postgres** ->**Member of** -> **Add…** -> **Administrators** -> **OK** 
- Restart Windows system
- Run: **runas /user:postgres cmd.exe** -> **cd \** -> **postgresql-8.4.9-1-windows.exe** -> installed successfully without errors. Checked data folder and confirmed files created successfully.
- Run: **compmgmt.msc** -> **Local Users and Groups** -> **User**s -> **postgres** -> **Member of** -> **Administrators** -> **Remove**
- Run: **compmgmt.msc** -> **Local Users and Groups** -> **Users** -> **postgres** -> **Member of** -> **Add…** -> **Power Users** -> **OK**

1，添加PGDATA环境变量

2，把对应的PGDATA目录制作成数据库集群目录，不然启动会报错：

​	pg_ctl: 目录 “d:\pgsql\”不是一个数据库集群目录

​	制作：先把上面的目录清空，然后运行：pg_ctl -D d:\pgsql\ initdb

​	命令运行完成后我们会看到 pgsql 目录下多了很多文件夹和文件，然后控制台会输出许多内容，	提示我们创建成功：

3，输入启动命令，其中那个-l 不是数字1，而是login的首字母 l :

​	pg_ctl start -D d:\pgsql\ -l LOGFILENAME

4，服务器启动完成。

常见错误：

 1. createdb: 无法联接到数据库 template1: 致命错误:  用户 "y5039" Password 认证失败：

    解决办法: psql DATABASENAME POSTGRESUSER

    

    

创建数据库：createdb -U postgres mydb

查看所有数据库：postgres=# \l

删除数据库：dropdb mydb

创建数据库用户：createuser -U postgres dbuser

查看所有数据库用户：postgres=# \du

更改数据库用户密码：postgres=# \password dbuser

删除数据库用户：dropuser -U postgres dbuser

