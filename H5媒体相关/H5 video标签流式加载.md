# video标签

浏览器通常通过video标签的src属性来自动加载视频。

此方法的问题：

1. mp4文件不能流式加载
2. webm, flv, hls等格式兼容性问题
3. 播放器UI丑，功能少
4. 清晰度切换等操作需要重载视频，比较慢还会黑屏
5. 无法对视频加密

# 请求video流视频

- 可通过设置responseType为arraybuffer来获取二进制视频流
- 也可通过range字段来获取视频流片段

```js
const xhr = new window.XMLHttpRequest();
xhr.open('get', 'http://www.w3school.com.cn/i/movie.mp4');
xhr.responseType = 'arrayBuffer';
// xhr.setRequestHeader('Range', 'bytes=0-390625');
xhr.onload = function () {
  if (xhr.status === 200 || xhr.status === 206) {
    console.log(xhr.response);
  };
};

xhr.send();

```

或者通过fetch的arrayBuffer方法返回视频流：

```js
fetch('http://www.w3school.com.cn/i/movie.mp4').then(function (response) {
  return response.arrayBuffer();
})
```

# video播流

## MediaSource

简称mse，是H5的一个API，它允许通过js来生成媒体流，让浏览器播放。

### 使用

通过URL.createObjectURL来创建一个blob格式的视频文件，来给video标签播。

具体用法就是new MediaSource，然后根据这个MediaSource生成blob文件，然后向MediaSource中添加mime和视频流。

```html
<video id="video" controls preload="auto"></video>

<script>
(function(){
    const video = document.querySelector("#video");
    const mediaSource = new MediaSource();
    video.src = URL.createObjectURL(mediaSource);
    mediaSource.addEventListener('sourceopen', sourceOpen);

    function sourceOpen (e) {
      URL.revokeObjectURL(video.src);
      // 设置媒体编码类型
      const mime = 'video/webm; codecs="vorbis, vp8"';
      const mediaSource = e.target;
      const sourceBuffer = mediaSource.addSourceBuffer(mime);
      const videoURL = 'http://localhost:8080/media/video.webm';

      fetch(videoURL).then(function(response) {
        console.log(response)
        return response.arrayBuffer();
      })
      .then(function(arrayBuffer) {
        sourceBuffer.addEventListener('updateend', function(e) {
          if (!sourceBuffer.updating && mediaSource.readyState === 'open') {
            mediaSource.endOfStream();
            // 在数据请求完成后，我们需要调用endOfStream(),它会改变MediaSource.readyState为ended并且触发sourceended事件
            video.play().then(function () {}).catch(function(err) {
              console.log(err)
            });
          }
        });
        sourceBuffer.appendBuffer(arrayBuffer)
      });
    }
}())
</script>

```

### mime

video/webm是视频格式，codecs后面第一段是一些视频解码的一些重要信息，诸如编码方式、分辨率、帧率、码率、以及对编码器解码能力的要求。第二段是关于音频部分的信息。

生成这样的一个video标签。我们现在绕过了浏览器直接去请求src这一步，ajax请求视频流，然后我们可以对视频流进行处理，直接操作视频流实现我们需要的各种功能。
但是对于**mp4格式，是不支持流式加载的**，所以只能通过我们自己操作流来实现流式播放。