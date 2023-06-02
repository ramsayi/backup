---
title: 视频处理工具 FFmpeg 常用实例详解
tags:
  - FFmpeg
  - 终端
categories:
  - 参考手册
  - FFmpeg
copyright: false
abbrlink: d33dd9c1
date: 2020-05-01 17:43:33
---

[FFmpeg](https://www.ffmpeg.org/) 是一个专业的多媒体框架，能够解码、编码、转码、复用、解复用、流式传输、过滤和播放几乎所有格式的媒体文件。

其核心就是 FFmpeg 程序本身，是一个基于**命令行**的视频和音频处理工具，多用于**视频转码**、**基础编辑**（修剪和合并）、**视频缩放**、**后期效果制作**等场景。

这里通过一些示例简单地介绍下 ffmpeg 命令的基本使用。

#### 一、获取详细信息

`ffmpeg -i <inputfile> -hide_banner`
其中 `-hide_banner` 选项用于在输出文件的详细信息时省略 ffmpeg 的版本信息和编译选项等。

```
$ ffmpeg -i bbb.mp4 -hide_banner
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'bbb.mp4':
  Metadata:
    major_brand     : isom
    minor_version   : 1
    compatible_brands: isomavc1
    creation_time   : 2013-12-17T16:40:26.000000Z
    title           : Big Buck Bunny, Sunflower version
    artist          : Blender Foundation 2008, Janus Bager Kristensen 2013
    comment         : Creative Commons Attribution 3.0 - http://bbb3d.renderfarming.net
    genre           : Animation
    composer        : Sacha Goedegebure
  Duration: 00:10:34.53, start: 0.000000, bitrate: 8487 kb/s
    Stream #0:0(und): Video: h264 (High) (avc1 / 0x31637661), yuv420p, 3840x2160 [SAR 1:1 DAR 16:9], 8002 kb/s, 60 fps, 60 tbr, 60k tbn, 120 tbc (default)
    Metadata:
      creation_time   : 2013-12-17T16:40:26.000000Z
      handler_name    : GPAC ISO Video Handler
    Stream #0:1(und): Audio: mp3 (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 160 kb/s (default)
    Metadata:
      creation_time   : 2013-12-17T16:40:28.000000Z
      handler_name    : GPAC ISO Audio Handler
    Stream #0:2(und): Audio: ac3 (ac-3 / 0x332D6361), 48000 Hz, 5.1(side), fltp, 320 kb/s (default)
    Metadata:
      creation_time   : 2013-12-17T16:40:28.000000Z
      handler_name    : GPAC ISO Audio Handler
    Side data:
      audio service type: main
At least one output file must be specified
```



#### 二、格式转换

```
ffmpeg -i <inputfile> <outputfile>
```

FFmpeg 是一个强大的音频和视频格式转换器，几乎支持当前所有常用的格式，如：
`$ ffmpeg -i input.avi output.mp4`

或者经常需要用到的，将视频文件转为 **GIF 动图**：
`$ ffmpeg -i input.mp4 output.gif`

如果在格式转换时需要保留源视频的质量，可以添加上 `-qscale 0` 选项（-qscale 的值越低，输出视频的质量越高）：
`$ ffmpeg -i input.webm -qscale 0 output.mp4`

可以使用 `-formats` 选项列出 ffmpeg 命令支持的所有格式（很长很长的一个列表。。。）：

```
$ ffmpeg -formats -hide_banner
File formats:
 D. = Demuxing supported
 .E = Muxing supported
 --
 D  3dostr          3DO STR
  E 3g2             3GP2 (3GPP2 file format)
  E 3gp             3GP (3GPP file format)
 D  4xm             4X Technologies
  E a64             a64 - video for Commodore 64
 D  aa              Audible AA format files
 D  aac             raw ADTS AAC (Advanced Audio Coding)
 DE ac3             raw AC-3
 D  acm             Interplay ACM
 D  act             ACT Voice file format
 D  adf             Artworx Data Format
 D  adp             ADP
 D  ads             Sony PS2 ADS
  E adts            ADTS AAC (Advanced Audio Coding)
 DE adx             CRI ADX
 D  aea             MD STUDIO audio
 D  afc             AFC
 DE aiff            Audio IFF
 D  aix             CRI AIX
 DE alaw            PCM A-law
 D  alias_pix       Alias/Wavefront PIX image
 DE amr             3GPP AMR
 D  amrnb           raw AMR-NB
 D  amrwb           raw AMR-WB
 D  anm             Deluxe Paint Animation
 D  apc             CRYO APC
 D  ape             Monkey's Audio
...
```



#### 三、指定编码

可以通过 `-c` 选项手动指定输出文件的编码，如：
`$ ffmpeg -i input.mp4 -c:v vp9 -c:a libvorbis output.mkv`
其中 `-c:v` 用于指定视频编码，`-c:a` 指定音频编码

**PS**：视频文件的后缀如 `mp4`、`mkv`、`avi` 等只是表示用来装载媒体流的**“容器”**类型，而编码时使用的编码方式则另需指定。
当然很多时候 `ffmpeg` 会根据输出文件的后缀自行选择默认的编码方式，无需手动指定。

##### 只改变视频或者音频流的编码

可以在指定编码时，只改变视频或者音频编码中的一项，另一项则保持原来的格式：
`$ ffmpeg -i input.webm -c:v copy -c:a flac output.mkv`
`-c:v copy` 表示复制输入文件中的视频流到输出文件，不重新进行编码

##### 只改变文件后缀

即输入文件中的视频流和音频流同时复制到输出文件，只改变文件后缀：
`$ ffmpeg -i input.webm -c:av copy output.mkv`

##### 编码列表

查看 FFmpeg 支持的所有音视频编码格式（又一个很长的列表。。。）：

```
$ ffmpeg -codecs -hide_banner
Codecs:
 D..... = Decoding supported
 .E.... = Encoding supported
 ..V... = Video codec
 ..A... = Audio codec
 ..S... = Subtitle codec
 ...I.. = Intra frame-only codec
 ....L. = Lossy compression
 .....S = Lossless compression
 -------
 ...
 DEV.L. flv1                 FLV / Sorenson Spark / Sorenson H.263 (Flash Video) (decoders: flv ) (encoders: flv )
 D.V..S fmvc                 FM Screen Capture Codec
 D.VI.S fraps                Fraps
 D.VI.S frwu                 Forward Uncompressed
 D.V.L. g2m                  Go2Meeting
 D.V.L. gdv                  Gremlin Digital Video
 DEV..S gif                  GIF (Graphics Interchange Format)
 DEV.L. h261                 H.261
 DEV.L. h263                 H.263 / H.263-1996, H.263+ / H.263-1998 / H.263 version 2
 D.V.L. h263i                Intel H.263
 DEV.L. h263p                H.263+ / H.263-1998 / H.263 version 2
 DEV.LS h264                 H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10 (decoders: h264 h264_qsv h264_cuvid ) (encoders: libx264 libx264rgb h264_amf h264_nvenc h264_qsv nvenc nvenc_h264 )
 DEVIL. hap                  Vidvox Hap
 DEV.L. hevc                 H.265 / HEVC (High Efficiency Video Coding) (decoders: hevc hevc_qsv hevc_cuvid ) (encoders: libx265 nvenc_hevc hevc_amf hevc_nvenc hevc_qsv )
...
```



#### 四、视频压缩

##### 编码与比特率

有些时候，基于磁盘空间和网络传输的考虑，需要对视频文件进行压缩处理。其中一种方法就是改变视频的**比特率**。
在某些情况下，比特率的适当缩减对视频的观看效果并不会产生太大的影响（人眼察觉的范围内）。
当然**编码的选择**也会对输出文件的大小产生一定的影响，示例如下：

`$ ffmpeg -i input.webm -c:a copy -c:v vp9 -b:v 1M output.mkv`
`-b:v` 用于指定视频的比特率。

##### 帧率

另一种方式就是改变视频文件的**帧率**，也就是人们常常提到的**FPS**。

`$ ffmpeg -i input.webm -c:a copy -c:v vp9 -r 30 output.mkv`
`-r 30` 选项用于指定输出视频的帧率为 30 FPS。

##### 分辨率

视频的分辨率也会影响文件的大小，可以使用 `-s` 选项指定输出文件的分辨率。当然，视频的画幅大小也会产生相应的变化：

```
$ ffmpeg -i input.mkv -c:a copy -s hd720 output.mkv`
或
`$ ffmpeg -i input.mkv -c:a copy -s 1280x720 output.mkv
```

#### 五、提取音频

通过格式转换，FFmpeg 可以直接将视频文件转为音频文件，只需要指定输出文件的格式为 `.mp3` 或 `.ogg` 等。如：
`$ ffmpeg -i input.mp4 output.mp3`

同时，也可以在转换时指定音频的格式选项：
`$ ffmpeg -i input.mp4 -vn -ar 44100 -ac 2 -ab 320 -f mp3 output.mp3`

其中：
`-vn` ：指定输出文件中禁用视频
`-ar` ：指定输出文件中音频的采样率
`-ac`：指定音频的通道数
`-ab`：指定音频的比特率
`-f`：指定输出文件的格式

#### 六、常用实用命令集锦

##### 调整分辨率

将某视频文件的分辨率改为 1280x720：
`$ ffmpeg -i input.mp4 -filter:v scale=1280:720 output.mp4`
或者：
`$ ffmpeg -i input.mp4 -s 1280x720 output.mp4`

##### 压缩视频文件

```
$ ffmpeg -i input.mp4 -vf scale=1280:-1 -c:v libx264 -preset veryslow -crf 24 output.mp4
```

也可以添加如下选项同时对音频流进行压缩：
`-c:a aac -strict -2 -b:a 128k`

##### 移除音频

`$ ffmpeg -i input.mp4 -an output.mp4`
`-an` 选项表示在输出文件中禁用音频

##### 提取图片

```
$ ffmpeg -i input.mp4 -r 1 -f image2 image-%2d.png
```

其中各选项的含义：
`-r` ：设置帧率，即每秒有多少帧画面被提取到图片中。默认为 25
`-f` ：指定输出的格式。本例中为图片（`image2`）
`-image-%2d.png` ：指定提取出的图片的命名方式。本例中最终的命名为 image-01.png、image-02.png 等。如使用 `image-%3d.png` ，则最终的命名为 image-001.png、imag-002.png 等

##### 裁剪视频

即截取指定范围内的**视频画面**，裁切掉多余的部分：
`$ ffmpeg -i input.mp4 -vf "crop=w:h:x:y" output.mp4`

其中 `crop=w:h:x:y` 用于指定“裁剪框”的大小和位置。
`w` 表示裁剪部分的宽度（默认为源视频的宽度 iw）；
`h` 表示裁剪部分的高度（默认为源视频的高度 ih；
`x` 表示 x 轴上裁剪的起始位置（最左边为 0，默认为源视频的中间位置）；
`y` 表示 y 轴上裁剪的起始位置（最顶部为 0，默认为源视频的中间位置）。

##### 改变视频比例

视频比例即视频画幅的长宽比，也就是通常所说的 `4:3` 和 `16:9` 等。
`$ ffmpeg -i input.mp4 -aspect 16:9 output.mp4`

##### 设置音频封面

即创建以一张静止的图片为画面的视频。

`$ ffmpeg -loop 1 -i inputimage.jpg -i inputaudio.wav -c:v libx264 -tune stillimage -c:a aac -b:a 192k -shortest output.mp4`
其中的选项和参数可以根据需求自行修改和省略。

##### 截取视频片段

`$ ffmpeg -i input.mp4 -ss 00:00:50 -codec copy -t 60 output.mp4`
截取视频中从第 50 秒开始，持续时间为一分钟的视频片段。

其中 `-ss` 用于指定视频片段的开始时间；
`-t` 指定视频片段的持续时间，单位都为秒。

也可以使用如下方式：
`$ ffmpeg -i audio.mp3 -ss 00:01:54 -to 00:06:53 -c copy output.mp3`

以上命令也适用于音频文件。

##### 视频分割

`$ ffmpeg -i input.mp4 -t 00:00:30 -c copy part1.mp4 -ss 00:00:30 -codec copy part2.mp4`
将输入的视频文件分割为两段，第一段为从最开始到第 30 秒；第二段为第 30 秒到视频结束。
其中 `-t 00:00:30` 前面省略了 `-ss 00:00:00`；
`-ss 00:00:30` 后面省略了 `-t 剩余时间`。

有点类似于截取多个连续的视频片段。

##### 视频合并

首先创建包含各媒体文件路径列表的文本文件 `join.txt` ：

```
file '~/myvideos/part1.mp4'
file '~/myvideos/part2.mp4'
file '~/myvideos/part3.mp4'
```



使用 `-f concat` 选项对多个视频进行合并：
`$ ffmpeg -f concat -i join.txt -c copy output.mp4`

##### 添加字幕文件

```
$ ffmpeg -i input.mp4 -i subtitle.srt -map 0 -map 1 -c copy -c:v libx264 -crf 23 -preset veryfast output.mp4
```

##### 改变视频播放速度（音频不受影响）

```
$ ffmpeg -i input.mp4 -vf "setpts=0.5*PTS" output.mp4
```

上述命令会加快视频画面的播放速度，音频播放速度不变。

如果想放慢视频画面的切换速度，可以相应地将 `setpts=0.5*PTS` 中的 0.5 改为大于 1 的数值。

##### Padding

即宽银幕视频中上下的两道“黑边”，可以使用 FFmpeg 命令添加类似的效果：

```
$ ffmpeg -i input.mp4 -vf "scale=1920:1080:force_original_aspect_ratio=decrease,pad=1920:1080:(ow-iw)/2:(oh-ih)/2:black" output.mp4
```



该效果由 `-vf` 选项的 `pad` 参数指定，可以根据情况自行修改。

##### 从图片创建视频

`$ ffmpeg -framerate 1 -i img%02d.jpg -c:v libx264 -r 30 -pix_fmt yuv420p output.mp4`
把当前目录下的多张图片（名字为 `img01.jpg`、`img02.jpg` 的形式）组合为一个视频文件，效果类似于自动播放的 PPT。
**每秒切换一张图片**。

`$ ffmpeg -framerate 30 -i img%02d.jpg -c:v libx264 -pix_fmt yuv420p output.mp4`
也是将当前目录下的多张图片组合成一个完整的视频，该视频帧率为 30 FPS。
**每帧切换一张图片**。

#### 参考资料

[20 FFmpeg Commands For Beginners](https://www.ostechnix.com/20-ffmpeg-commands-beginners/)
[How to create a video from images with FFmpeg?](https://stackoverflow.com/questions/24961127/how-to-create-a-video-from-images-with-ffmpeg)

> [视频处理工具 FFmpeg 常用实例详解](https://www.starky.ltd/2019/03/10/ffmpeg-user-manual-and-practical-examples/)