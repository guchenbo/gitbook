# centos7 rpm 安装mysql #

1、安装服务端

	rpm -ivh MySQL-server-5.6.21-1.rhel5.x86_64.rpm
    
包冲突报错，卸载冲突的软件

    rpm -e --nodeps

    yum remove -y 

重新安装，perl Module缺少

    FATAL ERROR: please install the following Perl modules before executing ./scripts/mysql_install_db:
    Data::Dumper

安装perl Module

    yum list|grep -i perl-modul*

    yum install -y perl-Module-Install.noarch 

重新安装，成功

2、启动服务

    service mysql start

3、安装客户端

    rpm -ivh MySQL-client-5.6.21-1.rhel5.x86_64.rpm

4、访问，注意mysql server **会随机生成密码在/root/.mysql_secret文件里，有时不生成，直接登录，很奇怪**

5、运行客户端命令，`# mysql -u root -p密码`

6、更改mysql的密码，在mysql客户端里执行命令，`SET PASSWORD=PASSWORD('mysql'); `