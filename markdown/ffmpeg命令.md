# ffmpeg 几点
#### 截取音频

```
ffmpeg -i gaobai.m4r -ss 5 -to 10  -acodec libmp3lame -ab 96k -y output3.mp3
```
-i 输入文件
-ss 起始时间
-to 结束时间
-acodec 音频转码
-ab 音频码率


http://www.ffmpeg.org/ffmpeg-utils.html#time-duration-syntax


