# Maven之仓库详解
### 概述
maven管理的依赖包，都放在仓库中。构建maven项目时，仓库分为本地仓库和远程仓库。构建项目时，会从本地仓库中查找依赖，找不到在去远程仓库查找，即本地仓库是作为远程仓库的缓存。因此仓库分为：

* 本地仓库
* 远程仓库

==注：优先级：本地 > 远程==

### 本地仓库
默认路径`${user.home}/.m2/repository/`，也可以自定义，通过修改setting.xml：

```
<localRepository>$自定义路径</localRepository>
```
### 远程仓库
默认情况下，每个maven项目的POM都继承`super pom`，在`super pom`中有定义了一个远程仓库作为默认。

```
<repositories>
	<repository>
	 <id>central</id>
	 <name>Central Repository</name>
	 <url>http://repo.maven.apache.org/maven2</url>
	 <layout>default</layout>
	 <snapshots>
	   <enabled>false</enabled>
	 </snapshots>
	</repository>
</repositories>
```
自定义可以有几种配置方式：

* settings.xml的profile
* pom.xml的repository
* settings.xml的mirror

==注：优先级：repository > profile==
#### mirror
作为仓库的镜像，会替代需要镜像的仓库


