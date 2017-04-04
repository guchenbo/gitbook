# Maven之setting.xml
### 概述
maven的配置文件就一个setting.xml，本文详细分析setting.xml中每个元素的定义。

### 文件路径

* 全局配置：`${m2_home}/conf/setting.xml`，影响全部
* 用户配置：`${user.home}/.m2/setting.xml`，只影响当前用户


==注：用户配置优于全局配置==

### 元素列表
setting.xml中一级元素有哪些：

名称 | 说明
------- | -------
localRepository | 本地仓库路径
interactiveMode | 是否启用用户交互
usePluginRegistry | 是否管理plugin版本
offline | 离线模式
pluginGroups | plugin的groupId
servers | 配置服务端的信息
mirrors | 配置镜像
proxies | 配置代理
profiles | 配置环境参数
activeProfiles | 配置激活的profileId

### localRepository
默认为`${user.home}/.m2/repository`

### interactiveMode
默认为true

### usePluginRegistry
默认为false，设置为true表示使用文件`${user.home}/.m2/plugin-registry.xml`来管理plugin的版本

### offline
默认为false

### pluginGroups
plugin的groupId列表，子元素是`pluginGroup`。如果构建的时候没有指定plugin的groupId，就会从这个列表中查找groupId，默认增加了`org.apache.maven.plugins`和`org.codehaus.mojo`
额外增加自己的groupId：

```
<pluginGroups>
    <pluginGroup>com.your.plugins</pluginGroup>
</pluginGroups>
```

### servers
从repository下载依赖或者deploy依赖到repository上的时候，如何需要一些安全信息，就配置servers元素。配置连接repository服务器的一些安全信息，子元素是`server`，配置信息如下：

* id：用来匹配repository的id或者mirror的id
* username、password：用户和密码
* privateKey、passphrase：秘钥文件和通行口令，文件默认为`${user.home}/.ssh/id_dsa`，通行口令不是必填的，口令和上面的密码在现在的版本中为明文
* filePermissions、directoryPermissions：在deploy到repository时，创建文件和目录使用的权限，基于*nix的权限，不是必填的

==注：要么使用username/password，要么使用privateKey/passphrase，两者不能一起使用==

示例：

```
</servers>
	<server>
		<id>server001</id>
		<username>my_username</username>
		<password>my_password</password>
		<filePermissions>664</filePermissions>
		<directoryPermissions>775</directoryPermissions>
	</server>
	
	<server>
		<id>server002</id>
		<privateKey>${user.home}/.ssh/id_dsa</privateKey>
		<passphrase>my_passphrase</passphrase>
		<filePermissions>664</filePermissions>
		<directoryPermissions>775</directoryPermissions>
	</server>
</servers>
```

### mirrors
当repository的url不可访问，或者访问速度慢的情况下，我们可以设置镜像来替换指定的repository。maven会使用镜像的url去下载依赖。子元素是`mirror`，配置信息包括：

* id、name：id唯一，name不是必填的
* url：镜像的地址
* mirrorOf：用来替换的repository，
	* `repo`：一个
	* `repo1，repo2`：多个
	* `*`：全部
	* `*,!repo3`，除了repo3的全部

示例：

```
<mirrors>
	<mirror>
	 <id>mirrorId</id>
	 <mirrorOf>central</mirrorOf>
	 <name>Human Readable Name for this Mirror.</name>
	 <url>http://my.repository.com/repo/path</url>
	</mirror>
</mirrors>
```

### proxies
配置代理信息，子元素是`proxy`，配置信息包括：

* id：唯一，区别不同的proxy
* active：是否激活，当有一组代理，只需要使用其中一个的时候，这个就可以派上用处
* protocol、host、port：代理的`protocol://host:port`
* username、password：用户名和密码
* nonProxyHosts：配置不需要代理的域名

示例：

```
<proxies>
	<proxy>
      <id>optional</id>
      <active>true</active>
      <protocol>http</protocol>
      <username>proxyuser</username>
      <password>proxypass</password>
      <host>proxy.host.net</host>
      <port>80</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
</proxies>
```

### profiles
配置环境参数，是`pom.xml`里的profiles元素的简化版，激活的profile会覆盖`pom.xml`定义的profile，包括4个子元素：`activation、repositories、pluginRepositories、properties`

#### activation
环境可以通过activation来激活，当出现符合activation里配置的条件时，该profile会被激活，包括几个子元素：`jdk、os、property、file`

* jdk：当匹配的jdk被检测到时，profile会激活
* os：当匹配的os会检测到时，profile会激活
* property：当匹配的property会检测到时，profile会激活
* file：
	* exists：指定文件存在，profile会激活
	* missing：指定文件不存在，profile会激活

示例：

```
<activation>
 <jdk>1.4</jdk>
 <os>
	<name>Windows XP</name>
	<family>Windows</family>
	<arch>x86</arch>
	<version>5.1.2600</version>
 </os>
 <property>
	<name>mavenVersion</name>
	<value>2.0.3</value>
 </property>
 <file>
	<exists>${basedir}/file2.properties</exists>
	<missing>${basedir}/file1.properties</missing>
 </file>
</activation>
```

#### properties
激活的profile里定义属性可以在pom里使用。除此之外总共有五种类型的属性可以在pom里使用：

* env.X：环境变量里的属性，如`${env.PATH}`，就表示shell环境的$PATH
* project.x：`pom.xml`里的元素，如`<project><version>1.0</version></project>`，可以通过`${project.version}`表示
* settings.x：`settings.xml`里的元素，如`<settings><offline>false</offline></settings>`，可以通过`${settings.offline}`表示
* Java System Properties：`java.lang.System.getProperties()`可以访问到的属性都可以使用，如`${user.dir}`
* x：在`<properties/>`元素里定义的属性

示例：

```
<properties>
   <user.install>${user.home}/our-project</user.install>
 </properties>
```

#### repositories
远程仓库配置列表，配置信息包括：

* releases、snapshots：可以在同一个仓库，对release和snapshot两种类型采取不同的策略
* enabled：对指定类型，是否开启
* updatePolicy：更新策略，`always（一直）、daily（默认）、interval:X(每隔几分钟)、never（从不）`
* checksumPolicy：deploy时，checksum（校验文件）丢失的策略，`ignore、fail、warn`
* layout：远程仓库布局，Maven 2 用`default`，Maven 1用`legacy`

示例：

```
<repository>
 <id>codehausSnapshots</id>
 <name>Codehaus Snapshots</name>
 <releases>
   <enabled>false</enabled>
   <updatePolicy>always</updatePolicy>
   <checksumPolicy>warn</checksumPolicy>
 </releases>
 <snapshots>
   <enabled>true</enabled>
   <updatePolicy>never</updatePolicy>
   <checksumPolicy>fail</checksumPolicy>
 </snapshots>
 <url>http://snapshots.maven.codehaus.org/maven2</url>
 <layout>default</layout>
</repository>
```

#### pluginRepositories
仓库有两种类型的构件，一种是依赖dependence，还有一种是插件plugin，pluginRepositories配置和repositories一致

### activeProfiles
配置profileId的列表，配置在这个元素中的profileId都会被激活
==注：profile激活的条件，1、-P参数；2、`<profile><activation>`元素；3、`<activeProfiles>元素`==


