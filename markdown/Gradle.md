# Gradle之初始
### 简介
Gradle和Maven一样也是一个自动构建工具，和Maven不同的是Maven基于pom.xml，xml语言，而Gradle基于Groovy语言。

### 概念
Gradle有两个重要的概念，`Project`和`Task`。一次构建build包含多个`Project`，一个`Project`包含多个`Task`。
### 构建脚本
`build.gradle`是Gradle的构建脚步文件，就类似于`pom.xml`之于`Maven`。它里面可以写脚步，使用`gradle task名字`执行命令。如：

```
task hello {
    doLast {
        println 'hello world'
    }
}
```

```
$> gradle hello   
:hello
hello world

BUILD SUCCESSFUL
```
更多的脚本命令，参考官网教程。
### 插件
一个脚本文件里包含了构建使用的任务，而插件的作用就是定义了一些构建需要的任务，供开发人员使用。使用插件写法：

```
apply plugin: 'java'
```

### 仓库
一个项目需要引用外部的依赖，需要知道仓库地址和依赖的写法，仓库可以添加Maven、Ivy
添加Maven仓库：

```
repositories {
    mavenCentral()
    maven {url "http://repo.maven.apache.org/maven2
"}
}
```
mavenCentral()，表示Maven的中央仓库的快捷写法

依赖写法：

```
dependencies {
    compile group: 'commons-collections', name: 'commons-collections', version: '3.2'
    testCompile group: 'junit', name: 'junit', version: '4.+'
}
```
便捷写法：

```
dependencies {
    compile 'commons-collections:commons-collections:3.2'
    testCompile 'junit:junit:4.0'
}
```


