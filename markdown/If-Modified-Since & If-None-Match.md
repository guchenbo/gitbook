# If-Modified-Since & If-None-Match

1、客户端首次访问页面A；

2、服务器响应头会加入Last-Modified和ETag，分别表示最新文件改动时间和文件最新状态；

3、客户端再次访问页面A，请求头加入If-Modified-Since和If-None-Match，他们的值分别为服务器响应头中的Last-Modified和ETag；

4、服务器验证If-Modified-Since和If-None-Match，判断文件是否有改动；

5、如果有改动，返回200，响应头加入新的Last-Modified和ETag；如果没有改动，返回304，和老的Etag；



If-Modified-Since和Last-Modified配对，If-None-Match和ETag配对；



说明：返回304，客户端就从本地缓存中加载页面，这种机制大大减少了网络上的传输，减轻服务器压力。



