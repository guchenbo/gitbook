# file.encoding属性 #
`String.getBytes()`如果不指定Charset的话，默认是使用`Charset.defaultCharset`，这个Charset是指系统属性`System.getProperty("file.encoding")`，这个属性只跟main方法所在类有关，是main方法所在类的文件保存编码，只设置一次