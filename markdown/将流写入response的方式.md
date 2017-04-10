 ## 将流写入response的方式

#### 普通servlet

```java
fis = new FileInputStream(file );
IOUtils. copy(fis, response.getOutputStream());

response.getOutputStream().flush();
response.flushBuffer();

```

#### Apache CXF

```java
StreamingOutput stream = new StreamingOutput() {
  @Override
    public void write(OutputStream output) throws IOException, WebApplicationException {
      FileInputStream input = null;
      try {
        input = FileUtils.openInputStream(attr);
        IOUtils.copy(input, output);
      } finally {
        IOUtils.closeQuietly(input);
      }
    }
};
```

