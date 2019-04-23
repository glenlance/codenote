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

## 6.3.1 设置数据库

在启动并创建好数据库之后，我们还需要执行以下3个步骤：

1. 创建数据库用户；
2. 为用户创建数据库；
3. 运行安装脚本，创建执行相关操作所需的表。

首先，我们可以通过在命令行执行以下命令来创建数据库用户：

> createuser -P -d y5039

这一命令会创建出一个名为y5039的Postgres数据库用户，其中-P选项会让createuser程序在执行时弹出一个提示符，只需要在提示符出现之后输入相应的字符串，就可以将其设置为y5039用户的密码，而 -d 选项则会赋予y5039用户创建数据库所需的权限。

接着，我们需要为y5039用户创建数据库。通过在命令行执行以下命令，我们就可以创建一个名为y5039的数据库：

> createdb gwp

注意，这个数据库的名字跟我们刚刚创建的数据库用户的名字是一样的，都是y5039。虽然数据库用户也可以创建与自己名字不同的数据库，但这样做需要额外的权限设置，所以为了让事情尽可能简单，我们这里将使用默认的数据库命名方式，也就是为数据库用户创建一个与之同名的数据库。

在拥有了数据库之后我们还需要创建一个表，这个表也是接下来的内容中我们唯一使用的表。首先，我们需要创建一个名为setup.sql的文件，并将代码清单6-5所示的内容键入该文件中。

```sql
create table posts (
	id	serial primary key,
	content text,
	author varchar(255)
);
```

接着，我们还需要在命令行执行以下命令：

> psql -U y5039 -f setup.sql -d y5039

在创建并设置好数据库之后，现在是时候来连接这个数据库了。