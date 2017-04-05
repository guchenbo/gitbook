# Java中的char
char类型长度两个字节，基于Unicode编码，采用UTF-16编码方法存储Unicode。
Unicode码点转成char方法为，UTF-16编码方式：

* U+0000～U+FFFF之间的，直接表示成一个char
* U+010000～U+10FFFF之间的，表示成两个char

### Unicode
Unicode有17个平面，第一个平面在U+0000～U+FFFF，叫做BMP（基本平面），其他16个平面叫做SMP（辅助平面）。
### UTF-16编码规则
BMP中U+D800～U+DFFF，是一个空段，不表示字符。利用这一特性，UTF-16这样规定

* U+0000～U+FFFF之间，直接表示
* U+010000～U+10FFFF之间，分别映射到U+D800～U+DFFF
	* 前10位（高位），映射到U+D800～U+DBFF
	* 后10为（低位），映射到U+DC00～U+DFFF

