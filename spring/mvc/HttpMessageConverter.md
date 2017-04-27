# Sring MVC之HttpMessageConverter
Controller中带有@ResponseBody的方法，不会返回指定的View，而是直接将返回数据写入response的body中，我们可以使用@ResponseBody，完成json的返回。
如果参数带有@RequestBody，也会使用HttpMessageConverter解析参数

  


