# Linux 命令
### 增加用户和组

```
groupadd pen
useradd -s /bin/bash -d /home/pen -g pen -m pen
```
### 磁盘

```
du -ah --max-depth=1
```
### 快速截取某时间段的日志
```
# cat access.log | awk '$4 >="[21/Jul/2014:14:37:50" && $4 <="[21/Jul/2014:14:38:00"'
```
### 查看从某个日期开始的日志

```
sed '/2016-12-13/p' statistics.log |more
```
### 建立软连接

```
ln -s 目标文件夹 软连接文件夹
```
### 更改文件用户和组

```
chown $user $file
chgrp $group $file
```

### 从正式服务器拷贝日志

other --> 185

```
scp -P 10022 -r admin@192.168.1.161:/home/admin/logs/dashboard.log dashboard.log
```
185 --> 205

```
scp -P 10022 -r admin@106.36.41.185:/home/admin/dashboard.log dashboard.log
```
205 --> local

```
scp -P 10022 -r www@10.1.10.205:/home/www/dashboard.log dashboard.log 
```

### 查看cpu信息
 # 总核数 = 物理CPU个数 X 每颗物理CPU的核数 
	# 总逻辑CPU数 = 物理CPU个数 X 每颗物理CPU的核数 X 超线程数
	
	# 查看物理CPU个数
	cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l
	
	# 查看每个物理CPU中core的个数(即核数)
	cat /proc/cpuinfo| grep "cpu cores"| uniq
	
	# 查看逻辑CPU的个数
	cat /proc/cpuinfo| grep "processor"| wc -l

	# 查看CPU信息（型号）
	cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c
	
	# 查看内 存信息
	cat /proc/meminfo
	
### shell if 正则表达式判断
```
pth="^[1-9]\d*$"
if echo 3 | grep -q "$pth"; then

fi
```

