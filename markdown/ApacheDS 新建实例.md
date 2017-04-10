# ApacheDS 新建实例 #

1、安装apacheds-2.0.0_M20，成功之后会有默认的实例**default**

2、进入路径，/var/lib/apacheds-2.0.0_M20/

    # cd /var/lib/apacheds-2.0.0_M20/

3、拷贝default文件夹，改为新建的实例名<*instances*>，比如叫**test**

    # cp -rp default/ test

4、进入test，删除run/, partitions/, log/, syncrepl-data and cache/ 下的所有文件，保证conf/下只有三个文件，分别为：wrapper-instance.conf、log4j.properties、config.ldif，名字也要一致。

文档结构：
![](http://i.imgur.com/tisdNqZ.png)

5、修改config.ldif，只要修改ads-directoryServiceId，两个端口10389，10636

6、启动新的实例，`# ./apacheds start test`



