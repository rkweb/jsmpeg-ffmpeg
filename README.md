# jsmpeg-ffmpeg
jsmpeg&amp;ffmpeg study

## 1. 安装FFmpeg
### window环境
```
1.下载并解压安装包ffmpeg安装包（可以直接在上面下载）
2.配置环境变量
  右键我的电脑-属性-高级系统设置-环境变量-编辑path,在变量原始值后面加入c:\ffmpeg\bin;（根据你的安装包解压目录）;
3.在命令行输入 ffmpeg --version查看FFMPEG版本信息，可以查看到，说明安装成功.
```
图文教程（看不明白上面，可以看）:[https://zh.wikihow.com/%E5%9C%A8Windows%E4%B8%8A%E5%AE%89%E8%A3%85FFmpeg%E7%A8%8B%E5%BA%8F)

### mac环境下待更新...


## 2. 使用FFmpeg
```
1.将MP4视频文件考入解压目录
2.在该目录打开命令行
3.运行 ffmpeg -i in.mp4 -f mpegts \-codec:v mpeg1video -s 640x1236 -b:v 3000k -r 30 -bf 0 \-codec:a mp2 -ar 44100 -ac 1 -b:a 128k \out.ts
  in.mp4为视频源文件（可自定义）
  out.ts为导出后的文件名称（可自定义）
  640x1236为视频宽高
```


## 3. 使用jsmpeg
### html
```
<canvas id="canvas"></canvas>
```
### js
```
<script src="http://go.163.com/2015/public/common/js/zepto.min.js"></script>
<script src="jsmpeg.min.js"></script>
<script src="webaudio.js"></script>
<script>
    $(document).on('touchmove', function (evt) {
        evt.preventDefault();
    });
    //设置视频宽高
    $('#canvas').css({
        width: $(window).width(),
        height: $(window).height()
    });
    //
    var canvas = document.querySelector('#canvas');
    var player = new JSMpeg.Player('out3.ts', { canvas: canvas, loop: true, autoplay: false, audio: true });
    //微信下解锁声音
    $(document).on('WeixinJSBridgeReady', function () {
        player.audioOut.unlock(onUnlocked);
        player.play();
    });
    player.audioOut.unlock(onUnlocked);
    player.play();

    function onUnlocked() {
        //设置音量
        player.volume = 1;

    }
    
    //如需查看详细demo，看自行查看上面的index.html
    
    
    //
    player.play() 播放视频
           .pause() 暂停播放
           .stop()停止播放并回到视频开始
           .destroy()停止播放，清楚WebGL和WebAudio
           .volume 获取或者设置音量（0 - 1 ）
           .currentTime 获取或者设置播放位置
</script>
```

## demo
查看demo:[http://test.go.163.com/web/sale_go/20180312_videoAutoPlay/](http://test.go.163.com/web/sale_go/20180312_videoAutoPlay/)

## 扩展
更多参数请访问:[https://github.com/phoboslab/jsmpeg](https://github.com/phoboslab/jsmpeg)

更多视频转换配置请访问:[http://www.ffmpeg.org/](http://www.ffmpeg.org/)




## 更多转换命令
```
1.从视频提取音频
> ffmpeg -i video.mp4 -f mp3 -vn video.mp3

2.视频转 .ts
ffmpeg -i in.mp4 -f mpegts \-codec:v mpeg1video -s 640x1236 -b:v 3000k -r 30 -bf 0 \-codec:a mp2 -ar 44100 -ac 1 -b:a 128k \out.ts
```
