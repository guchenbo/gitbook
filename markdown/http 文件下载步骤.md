# http 文件下载步骤

1、为了防止中文乱码，对文件名进行编码

`URLEncoder.encode(filename, "UTF-8");`

`new String(filename.getBytes(), "ISO-8859-1");`



2、设置response的Content-Type（mime-type）和头信息

	> 1、Content-Type，根据后缀名不同而不同（这样比较准确）
	>
	> 2、Content-Dispostion头，固定为`attachment; filename=${filename}`
	>
	> 3、Content-Length头，文件长度

[Content-Type对应表​]: http://tool.oschina.net/commons

3、将文件流写入response

------

示例代码：

```java
String contentType = gainContentType(ext);
response.setContentType(contentType);
response.setHeader("Content-Disposition", "attachment; filename="
                              + filename);


String gainContentType(String ext) {
  String[] doc = { "doc", "docx" };
  String[] excel = { "xls", "xlsx" };
  String[] jpg = { "jpg", "jpeg" };
  String[] txt = { "txt" };

  if (ArrayUtils.contains(doc, ext)) {
    return "application/msword";
  } else if (ArrayUtils.contains(excel, ext)) {
    return "application/vnd.ms-excel";

  } else if (ArrayUtils.contains(jpg, ext)) {
    return "image/jpeg";
  } else if (ArrayUtils.contains(txt, ext)) {
    return "text/plain";
  }

  return "application/octet-stream";
}
```