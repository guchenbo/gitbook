# Maven 按照本地依赖

命令：
```
mvn install:install-file -Dfile= -DgroupId= -DartifactId= -Dversion= -Dpackaging=
```
示例：
```
mvn install:install-file -Dfile=/Users/penglai/git/深入剖析Tomcat源码/lib/tomcat-util.jar -DgroupId=tomcat -DartifactId=catalina -Dversion=4.1.12 -Dpackaging=jar
```






