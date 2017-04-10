# GitBook Mac 安装

需要有Node.js环境，安装：

```
npm install gitbook-cli -g
```
gitbook-cli，是用来管理gitbook的版本的。
检测是否安装成功

```
gitbook -V
```
之后会安装最新版gitbook，提示Install gitbook 3.2.2，会很慢很慢，直到安装完成。

### 使用
初始化一本书，

```
gitbook init test
```
进入目录，发布书籍

```
cd test
gitbook server
```
会打印

```
Live reload server started on port: 35729
Press CTRL+C to quit ...

info: 7 plugins are installed 
info: loading plugin "livereload"... OK 
info: loading plugin "highlight"... OK 
info: loading plugin "search"... OK 
info: loading plugin "lunr"... OK 
info: loading plugin "sharing"... OK 
info: loading plugin "fontsettings"... OK 
info: loading plugin "theme-default"... OK 
info: found 1 pages 
info: found 0 asset files 
info: >> generation finished with success in 0.6s ! 

Starting server ...
Serving book on http://localhost:4000
```

使用浏览器打开，http://localhost:4000， 就好看到效果


