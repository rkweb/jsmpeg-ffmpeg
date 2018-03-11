# jsmpeg-ffmpeg
jsmpeg&amp;ffmpeg study

```
## 视频转换格式
### 从视频提取音频
> ffmpeg -i video.mp4 -f mp3 -vn video.mp3

### 视频转 .ts
> ffmpeg -i in.mp4 -f mpegts \-codec:v mpeg1video -s 640x1236 -b:v 3000k -r 30 -bf 0 \-codec:a mp2 -ar 44100 -ac 1 -b:a 128k \out.ts
```
