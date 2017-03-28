# Tomcat启动指定PID文件
在tomcat/bin/setclasspath.sh里，设置变量CATALINA_PID，指定tomcat-pid的文件
如：`CATALINA_PID="/Users/penglai/pid/tomcat-pid"`
#### 启动tomcat
会把tomcat的pid（进程号），写入tomcat-pid文件中
#### 关闭tomcat
会删除tomcat-pid文件


