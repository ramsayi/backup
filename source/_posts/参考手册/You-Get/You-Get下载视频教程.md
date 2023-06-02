---
title: You-Get下载视频教程
tags:
  - 视频
  - 下载
  - You-Get
categories:
  - 参考手册
  - You-Get
copyright: false
abbrlink: 295f256c
date: 2020-03-01 18:29:54
---

[You-Get](https://you-get.org/) 乃一小小哒命令行程序，提供便利的方式来下载网络上的媒体信息。

利用`you-get`下载[这个网页](http://www.fsf.org/blogs/rms/20140407-geneva-tedx-talk-free-software-free-society)的视频:

```
$ you-get http://www.fsf.org/blogs/rms/20140407-geneva-tedx-talk-free-software-free-society
Site:       fsf.org
Title:      TEDxGE2014_Stallman05_LQ
Type:       WebM video (video/webm)
Size:       27.12 MiB (28435804 Bytes)

Downloading TEDxGE2014_Stallman05_LQ.webm ...
100.0% ( 27.1/27.1 MB) ├████████████████████████████████████████┤[1/1]   12 MB/s
```

为什么你要好好的用You-get：

- 你欢喜于互联网上的富媒体内容，并为个人寻欢而储存
- 你喜悦观看的视频，然而不得保存；对个人设备无从控制，此乃违背开放互联网之行为
- 你寻求解脱于闭源软件或JavaScript代码，并禁止Flash运行
- 你为黑客精神与自由软件而欣喜

`you-get`之功用:

- 下载流行网站之音视频，例如YouTube, Youku, Niconico,以及更多. (查看[完整支持列表](https://github.com/soimort/you-get/wiki/中文说明#supported-sites))
- 于您心仪的媒体播放器中观看在线视频，脱离浏览器与广告
- 下载您喜欢的网页上的图片
- 下载任何非HTML内容，例如二进制文件

心动? [现在安装](https://github.com/soimort/you-get/wiki/中文说明#installation) 并 [查看使用范例](https://github.com/soimort/you-get/wiki/中文说明#getting-started).

使用Python编程？敬请查看 [源代码](https://github.com/soimort/you-get) 并fork!

![img](https://camo.githubusercontent.com/6799729106cb60a1fc57e33288e50483a896096a/68747470733a2f2f692e696d6775722e636f6d2f48687a324978452e706e67)

## 安装

### 绪论

以下乃必要依赖，需要单独安装，除非于Windows下使用预包装包:

- **[Python 3](https://www.python.org/downloads/)**
- **[FFmpeg](https://www.ffmpeg.org/)** (强烈推荐) or [Libav](https://libav.org/)
- (可选) [RTMPDump](https://rtmpdump.mplayerhq.hu/)

### 选项 1: 通过pip安装

`you-get`之官方版本通过[PyPI](https://pypi.python.org/pypi/you-get)分发, 可从PyPI镜像中通过[pip](https://en.wikipedia.org/wiki/Pip_(package_manager)) 包管理器安装. 须知您务必使用版本3的 `pip`:

```
$ pip3 install you-get
```

### 选项 2: 使用预装包(仅供Windows)

`exe` (单独文件) 或 `7z` (包括所有依赖) 可从https://github.com/soimort/you-get/releases/latest 下载.

### 选项 3: 于GitHub下载

您可选择[稳定版](https://github.com/soimort/you-get/archive/master.zip) (与PyPI最新版等同) 或 [开发版](https://github.com/soimort/you-get/archive/develop.zip) (更多的热补丁与不稳定功能)的`you-get`. 解压并将含有`you-get`的目录加入`PATH`.

或者, 运行

```
$ make install
```

以安装`you-get` 于永久路径.

### 选项 4: Git clone

即使您不常使用Python，作为开发者，也请使用此方法。

```
$ git clone git://github.com/soimort/you-get.git
```

将目录加入 `PATH`, 或运行 `make install` 以安装`you-get` 于永久路径.

## 升级

考虑到 `you-get` 安装方法之差异, 请使用:

```
$ pip3 install --upgrade you-get
```

或下载最新更新:

```
$ you-get https://github.com/soimort/you-get/archive/master.zip
```

## 开始

### 下载视频

当观赏感兴趣之视频，您可以使用 `--info`/`-i` 以查看所有可用画质与格式、s:

```
$ you-get -i 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
site:                YouTube
title:               Me at the zoo
streams:             # Available quality and codecs
    [ DEFAULT ] _________________________________
    - itag:          43
      container:     webm
      quality:       medium
      size:          0.5 MiB (564215 bytes)
    # download-with: you-get --itag=43 [URL]

    - itag:          18
      container:     mp4
      quality:       medium
    # download-with: you-get --itag=18 [URL]

    - itag:          5
      container:     flv
      quality:       small
    # download-with: you-get --itag=5 [URL]

    - itag:          36
      container:     3gp
      quality:       small
    # download-with: you-get --itag=36 [URL]

    - itag:          17
      container:     3gp
      quality:       small
    # download-with: you-get --itag=17 [URL]
```

标有`DEFAULT` 为默认画质。如认同，可下载:

```
$ you-get 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
site:                YouTube
title:               Me at the zoo
stream:
    - itag:          43
      container:     webm
      quality:       medium
      size:          0.5 MiB (564215 bytes)
    # download-with: you-get --itag=43 [URL]

Downloading zoo.webm ...
100.0% (  0.5/0.5  MB) ├████████████████████████████████████████┤[1/1]    7 MB/s

Saving Me at the zoo.en.srt ...Done.
```

(如YouTube视频带有字幕，将被一同下载，以SubRip格式保存.)

或，如您希望其他格式(mp4)，请使用其他提示选项:

```
$ you-get --itag=18 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

**注意:**

- 目前，格式选择没有大规模铺开；默认选项为最高画质.
- `ffmpeg`为必要依赖，以下载流式视频以及合并分块视频(例如，类似Youku), 以及YouTube的1080p或更高分辨率.
- 如不希望`you-get`合并视频，使用`--no-merge`/`-n`.

### 下载其他内容

如你有URL，可以直接使用:

```
$ you-get https://stallman.org/rms.jpg
Site:       stallman.org
Title:      rms
Type:       JPEG Image (image/jpeg)
Size:       0.06 MiB (66482 Bytes)

Downloading rms.jpg ...
100.0% (  0.1/0.1  MB) ├████████████████████████████████████████┤[1/1]  127 kB/s
```

或者, `you-get`将自动检查网页，下载一切有可能感兴趣的内容:

```
$ you-get http://kopasas.tumblr.com/post/69361932517
Site:       Tumblr.com
Title:      kopasas
Type:       Unknown type (None)
Size:       0.51 MiB (536583 Bytes)

Site:       Tumblr.com
Title:      tumblr_mxhg13jx4n1sftq6do1_1280
Type:       Portable Network Graphics (image/png)
Size:       0.51 MiB (536583 Bytes)

Downloading tumblr_mxhg13jx4n1sftq6do1_1280.png ...
100.0% (  0.5/0.5  MB) ├████████████████████████████████████████┤[1/1]   22 MB/s
```

**注意:**

- 此功能为测试性，远未完成。对于类似Tumblr和Blogger的大图有效，但是没有办法为所有网站建立通用格式.

### 在Google Videos搜索并下载

`you-get`可以吃任何东西. 如果不是合法的URL, `you-get`将在Google查找并下载最相关视频. (可能不是最心仪的，但是很有可能)

```
$ you-get "Richard Stallman eats"
```

### 暂停与恢复下载

可以使用Ctrl+C 暂停下载.

临时的`.download`文件将保存于输出目录。下次使用`you-get`传入相同参数时，下载将从上次继续开始. 如果下载已经完成 (临时的`.download` 扩展名消失), `you-get`将忽略下载.

用`--force`/`-f`强行重下载. (**注意:** 将覆盖同名文件或临时文件!)

### 设置输出文件名或路径

使用`--output-dir`/`-o` 设定路径, `--output-filename`/`-O` 设定输出文件名:

```
$ you-get -o ~/Videos -O zoo.webm 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

**提示:**

- 如果原视频标题含有与系统不兼容字符，十分有效.
- 也可以帮助使用脚本批量下载于指定目录和文件名.

### 代理设置

使用 `--http-proxy`/`-x`为`you-get`设置HTTP代理:

```
$ you-get -x 127.0.0.1:8087 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

然而系统代理 (即系统变量`http_proxy`) 自动使用. 使用`--no-proxy`强行关闭.

**提示:**

- 如果经常使用代理 (网络封锁了部分网站), 考虑将`you-get`和 [proxychains](https://github.com/rofl0r/proxychains-ng) 一同使用，并设置`alias you-get="proxychains -q you-get"` (于命令行).
- 对于某些网站(例如Youku), 如果你需要下载仅供中国大陆观看的视频, 可以使用 `--extractor-proxy`/`-y`单独为解析器设置代理. 可以使用 `-y proxy.uku.im:8888` (鸣谢： [Unblock Youku](https://github.com/zhuzhuor/Unblock-Youku) 项目).

### 观看视频

使用 `--player`/`-p` 将视频喂进播放器, 例如 `mplayer` 或者 `vlc`,而不是下载:

```
$ you-get -p vlc 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

或者你想在浏览器中观看而不希望看广告或评论区:

```
$ you-get -p chromium 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

**提示:**

- 可以使用 `-p` 开启下载工具,例如 `you-get -p uget-gtk 'https://www.youtube.com/watch?v=jNQXAC9IVRw'`, 虽然有可能不灵.

### 加载cookie

并非所有视频可供任何人观看。如果需要登录以观看 (例如, 私密视频), 可能必须将浏览器cookie通过`--cookies`/`-c` 加载入 `you-get`.

**注意:**

- 目前我们支持两种cookie格式：Mozilla `cookies.sqlite` 和 Netscape `cookies.txt`.

### 复用解析数据

使用 `--url`/`-u` 获得页面所有可下载URL列表. 使用 `--json`以获得JSON格式.

**警告:**

- 目前此功能**未定型**,JSON格式未来有可能变化.

## 支持网站

| 网站                        | URL                                               | 视频? | 图像? | 音频? |
| --------------------------- | ------------------------------------------------- | ----- | ----- | ----- |
| **YouTube**                 | https://www.youtube.com/                          | ✓     |       |       |
| **Twitter**                 | https://twitter.com/                              | ✓     | ✓     |       |
| VK                          | http://vk.com/                                    | ✓     |       |       |
| Vine                        | https://vine.co/                                  | ✓     |       |       |
| Vimeo                       | https://vimeo.com/                                | ✓     |       |       |
| Vidto                       | http://vidto.me/                                  | ✓     |       |       |
| Veoh                        | http://www.veoh.com/                              | ✓     |       |       |
| **Tumblr**                  | https://www.tumblr.com/                           | ✓     | ✓     | ✓     |
| TED                         | http://www.ted.com/                               | ✓     |       |       |
| SoundCloud                  | https://soundcloud.com/                           |       |       | ✓     |
| Pinterest                   | https://www.pinterest.com/                        |       | ✓     |       |
| MusicPlayOn                 | http://en.musicplayon.com/                        | ✓     |       |       |
| MTV81                       | http://www.mtv81.com/                             | ✓     |       |       |
| Mixcloud                    | https://www.mixcloud.com/                         |       |       | ✓     |
| Metacafe                    | http://www.metacafe.com/                          | ✓     |       |       |
| Magisto                     | http://www.magisto.com/                           | ✓     |       |       |
| Khan Academy                | https://www.khanacademy.org/                      | ✓     |       |       |
| JPopsuki TV                 | http://www.jpopsuki.tv/                           | ✓     |       |       |
| Internet Archive            | https://archive.org/                              | ✓     |       |       |
| **Instagram**               | https://instagram.com/                            | ✓     | ✓     |       |
| Heavy Music Archive         | http://www.heavy-music.ru/                        |       |       | ✓     |
| **Google+**                 | https://plus.google.com/                          | ✓     | ✓     |       |
| Freesound                   | http://www.freesound.org/                         |       |       | ✓     |
| Flickr                      | https://www.flickr.com/                           | ✓     | ✓     |       |
| Facebook                    | https://www.facebook.com/                         | ✓     |       |       |
| eHow                        | http://www.ehow.com/                              | ✓     |       |       |
| Dailymotion                 | http://www.dailymotion.com/                       | ✓     |       |       |
| CBS                         | http://www.cbs.com/                               | ✓     |       |       |
| Bandcamp                    | http://bandcamp.com/                              |       |       | ✓     |
| AliveThai                   | http://alive.in.th/                               | ✓     |       |       |
| interest.me                 | http://ch.interest.me/tvn                         | ✓     |       |       |
| **755 ナナゴーゴー**        | http://7gogo.jp/                                  | ✓     | ✓     |       |
| **niconico ニコニコ動画**   | http://www.nicovideo.jp/                          | ✓     |       |       |
| **163 网易视频 网易云音乐** | http://v.163.com/ http://music.163.com/           | ✓     |       | ✓     |
| 56网                        | http://www.56.com/                                | ✓     |       |       |
| **AcFun**                   | http://www.acfun.tv/                              | ✓     |       |       |
| **Baidu 百度贴吧**          | http://tieba.baidu.com/                           | ✓     | ✓     |       |
| 爆米花网                    | http://www.baomihua.com/                          | ✓     |       |       |
| **bilibili 哔哩哔哩**       | http://www.bilibili.com/                          | ✓     |       |       |
| Dilidili                    | http://www.dilidili.com/                          | ✓     |       |       |
| 豆瓣                        | http://www.douban.com/                            |       |       | ✓     |
| 斗鱼                        | http://www.douyutv.com/                           | ✓     |       |       |
| 凤凰视频                    | http://v.ifeng.com/                               | ✓     |       |       |
| 风行网                      | http://www.fun.tv/                                | ✓     |       |       |
| iQIYI 爱奇艺                | http://www.iqiyi.com/                             | ✓     |       |       |
| 激动网                      | http://www.joy.cn/                                | ✓     |       |       |
| 酷6网                       | http://www.ku6.com/                               | ✓     |       |       |
| 酷狗音乐                    | http://www.kugou.com/                             |       |       | ✓     |
| 酷我音乐                    | http://www.kuwo.cn/                               |       |       | ✓     |
| 乐视网                      | http://www.letv.com/                              | ✓     |       |       |
| 荔枝FM                      | http://www.lizhi.fm/                              |       |       | ✓     |
| 秒拍                        | http://www.miaopai.com/                           | ✓     |       |       |
| MioMio弹幕网                | http://www.miomio.tv/                             | ✓     |       |       |
| 痞客邦                      | https://www.pixnet.net/                           | ✓     |       |       |
| PPTV聚力                    | http://www.pptv.com/                              | ✓     |       |       |
| 齐鲁网                      | http://v.iqilu.com/                               | ✓     |       |       |
| QQ 腾讯视频                 | http://v.qq.com/                                  | ✓     |       |       |
| 阡陌视频                    | http://qianmo.com/                                | ✓     |       |       |
| Sina 新浪视频 微博秒拍视频  | http://video.sina.com.cn/ http://video.weibo.com/ | ✓     |       |       |
| Sohu 搜狐视频               | http://tv.sohu.com/                               | ✓     |       |       |
| 天天动听                    | http://www.dongting.com/                          |       |       | ✓     |
| **Tudou 土豆**              | http://www.tudou.com/                             | ✓     |       |       |
| 虾米                        | http://www.xiami.com/                             |       |       | ✓     |
| 阳光卫视                    | http://www.isuntv.com/                            | ✓     |       |       |
| **音悦Tai**                 | http://www.yinyuetai.com/                         | ✓     |       |       |
| **Youku 优酷**              | http://www.youku.com/                             | ✓     |       |       |
| 战旗TV                      | http://www.zhanqi.tv/lives                        | ✓     |       |       |
| 央视网                      | http://www.cntv.cn/                               | ✓     |       |       |

对于不在列表的网站，通用解析器将寻找并下载感兴趣之内容.

### 已知问题

如果 `you-get` 出现问题，不要惊慌. (是的，问题一直存在！)

看看是不是在 https://github.com/soimort/you-get/wiki/Known-Bugs里面, 搜索 [开放Issue](https://github.com/soimort/you-get/issues). 如果没人报告，开个新issue, 加上详细的命令行输出.

## 参与我们

使用Gitter [#soimort/you-get](https://gitter.im/soimort/you-get) (如何为Gitter [设置IRC客户端](http://irc.gitter.im/) ). 如果是个关于 `you-get` 的小问题, 在这里问.

我们欢迎各种pull requestse. 然而请注意:

- 你要向 [`develop`](https://github.com/soimort/you-get/tree/develop) 分支发PR.
- 记得rebase.
- 写出详细文档，如果可以，给出一些测试URL.
- commit message格式优美，清晰可读. 如果不知道，看看以往的.
- 我们不会强制你签署 CLA, 但是你必须确保你的代码可以被合法分发(使用 MIT 协议).

## 法律问题

本软件使用 [MIT 协议](https://raw.github.com/soimort/you-get/master/LICENSE.txt).

请特别注意:

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

(一个中文翻译可在http://lucien.cc/?p=15 查询。)

人话:

*如果你使用本软件进行盗版行为，或者非法行径，作者不为你负责.*

我们仅提供代码, 如何使用请自行考虑.

## 作者

[@soimort](https://github.com/soimort), 在此查看 [贡献者名单](https://github.com/soimort/you-get/graphs/contributors).