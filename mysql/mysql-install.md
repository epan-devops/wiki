# MySQL 安装

所有平台的MySQL下载地址为: [MySQL下载](https://dev.mysql.com/downloads/mysql/)。 挑选你需要的 MySQL Community Server 版本及对应的平台。

```
注意：安装过程我们需要通过开启管理员权限来安装，否则会由于权限不足导致无法安装。
```

# Linux/UNIX 上安装 MySQL  
Linux平台上推荐使用RPM包来安装Mysql,MySQL AB提供了以下RPM包的下载地址
- **MySQL** - MySQL服务器。你需要该选项，除非你只想连接运行在另一台机器上的MySQL服务器。  
- **MySQL-client** - MySQL 客户端程序，用于连接并操作Mysql服务器。  
- **MySQL-devel** - 库和包含文件，如果你想要编译其它MySQL客户端，例如Perl模块，则需要安装该RPM包。   
- **MySQL-shared** - 该软件包包含某些语言和应用程序需要动态装载的共享库(libmysqlclient.so*)，使用MySQL。  
- **MySQL-bench** - MySQL数据库服务器的基准和性能测试工具   

安装前，我们可以检测系统是否自带安装 MySQL:
```
rpm -qa | grep mysql
```

如果你系统有安装，那可以选择进行卸载:
```
rpm -e mysql　　// 普通删除模式
rpm -e --nodeps mysql　　// 强力删除模式，如果使用上面命令删除时，提示有依赖的其它文件，则用该命令可以对其进行强力删除
```

### 安装 MySQL：
接下来我们在 Centos7 系统下使用 yum 命令安装 MySQL，需要注意的是 CentOS 7 版本中 MySQL数据库已从默认的程序列表中移除，所以在安装前我们需要先去官网下载 Yum 资源包，下载地址为：https://dev.mysql.com/downloads/repo/yum/

```
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
rpm -ivh mysql-community-release-el7-5.noarch.rpm
yum update
yum install mysql-server
```

权限设置：
```
chown mysql:mysql -R /var/lib/mysql
```

初始化 MySQL：
```
mysqld --initialize
```
启动 MySQL：
```
systemctl start mysqld
```

查看 MySQL 运行状态：
```
systemctl status mysqld
```

```
注意：如果我们是第一次启动 mysql 服务，mysql 服务器首先会进行初始化的配置。
```

此外,你也可以使用 MariaDB 代替，MariaDB 数据库管理系统是 MySQL 的一个分支，主要由开源社区在维护，采用 GPL 授权许可。开发这个分支的原因之一是：甲骨文公司收购了 MySQL 后，有将 MySQL 闭源的潜在风险，因此社区采用分支的方式来避开这个风险。

MariaDB的目的是完全兼容MySQL，包括API和命令行，使之能轻松成为MySQL的代替品。

```
yum install mariadb-server mariadb 
systemctl start mariadb  #启动MariaDB
systemctl stop mariadb  #停止MariaDB
systemctl restart mariadb  #重启MariaDB
systemctl enable mariadb  #设置开机启动
```

### 验证 MySQL 安装

在成功安装 MySQL 后，一些基础表会表初始化，在服务器启动后，你可以通过简单的测试来验证 MySQL 是否工作正常。

使用 mysqladmin 工具来获取服务器状态：

使用 mysqladmin 命令俩检查服务器的版本, 在 linux 上该二进制文件位于 /usr/bin 目录，在 Windows 上该二进制文件位于C:\mysql\bin 。
```
[root@host]# mysqladmin --version
```

linux上该命令将输出以下结果，该结果基于你的系统信息：
```
mysqladmin  Ver 8.23 Distrib 5.0.9-0, for redhat-linux-gnu on i386
```

如果以上命令执行后未输入任何信息，说明你的Mysql未安装成功。

### Mysql安装后需要做的
Mysql安装成功后，默认的root用户密码为空，你可以使用以下命令来创建root用户的密码：
```
[root@host]# mysqladmin -u root password "new_password";
```
现在你可以通过以下命令来连接到Mysql服务器：
```
[root@host]# mysql -u root -p
Enter password:*******
```

注意：在输入密码时，密码是不会显示了，你正确输入即可。
