# jsmpeg-ffmpeg
jsmpeg&amp;ffmpeg study

## 安装FFmpeg
### window环境
```
1.下载并解压安装包ffmpeg安装包
2.配置环境变量
  右键我的电脑-属性-高级系统设置-环境变量-编辑path,在变量原始值后面加入c:\ffmpeg\bin;（根据你的安装包解压目录）;
3.在命令行输入 ffmpeg --version查看FFMPEG版本信息，可以查看到，说明安装成功.
```
## 使用FFmpeg
```
1.将MP4视频文件考入解压目录
2.在该目录打开命令行
3.运行 ffmpeg -i in.mp4 -f mpegts \-codec:v mpeg1video -s 640x1236 -b:v 3000k -r 30 -bf 0 \-codec:a mp2 -ar 44100 -ac 1 -b:a 128k \out.ts
  in.mp4为视频源文件（可自定义）
  out.ts为导出后的文件名称（可自定义）
  640x1236为视频宽高
```
## 使用jsmpeg
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
    
</script>
```
更多参数请访问:[https://github.com/phoboslab/jsmpeg](https://github.com/phoboslab/jsmpeg)




## 视频转换格式
```
1.从视频提取音频
> ffmpeg -i video.mp4 -f mp3 -vn video.mp3

2.视频转 .ts
ffmpeg -i in.mp4 -f mpegts \-codec:v mpeg1video -s 640x1236 -b:v 3000k -r 30 -bf 0 \-codec:a mp2 -ar 44100 -ac 1 -b:a 128k \out.ts
```
