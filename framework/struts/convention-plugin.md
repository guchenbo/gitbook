# Struts2之convention plugin
**struts**的convention plugin，***约定大于配置***。

意思是指，我们如果遵守这个插件的约定，就可以做到零配置，而且我们也可以使用注解重载约定达到零配置。

这里的零配置也只是说大大减少配置。两种方式：

1. 约定
2. 注解


------

几个重要的配置：

> 搜索视图资源（jsp、freemarker等）路径：
>
> `<constant name="struts.convention.result.path" value="/app/"/>`
>
> 默认为/WEB-INF/content/，所有的视图资源都放在这个文件夹路径下




1、约定

> Action不存在

如果插件在包搜索路径下找不到与请求URL相匹配Action，则会到result的搜索路径下搜索与请求URL相匹配的视图资源，如果还搜索不到，则抛出no action mapped exception

*其中result.path 为 /app/*

示例：

| URL                            | 视图                   |
| ------------------------------ | -------------------- |
| /                              | /app/index.jsp       |
| /index                         | /app/index.jsp       |
| /hello-world                   | /app/hello-world.jsp |
| /test1/test2（namespace为/）      | /app/test2.jsp       |
| /test1/test2（namespace为/test1） | /app/test1/test2.jsp |

注：

[点击查看namespace的解析原理​]: 

> Action存在

执行Action的execute方法，返回视图资源为name-resultCode.jsp



2、注解

@Namespace

请求URL加入namespace，返回的视图资源也放在resultPath/namespace下

@Action

对应于action的name

