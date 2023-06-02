---
title: 博客内嵌入Bilibili视频
tags:
  - 博客
  - Bilibili
categories:
  - 建站博客
copyright: false
abbrlink: f0c817ec
cover: '/assets/img/post/bilibili.webp'
date: 2021-09-11 10:22:33
---

## 一、原理

使用iframe标签，更改其中src对应bilibili视频的aid和cid，组装新的HTML源码，即可在文章内嵌入bilibili视频。

## 二、获取aid和cid

aid为视频的av号，但是每个av号下不一定只有1p，所以B站用cid来管理视频的真正id，那么也可以说如果视频只有1p，那么cid就无用了，我测试直接填1也是可以的。

我们在转发视频的时候直接可以看到嵌入代码

![](/assets/img/post/f0c817ec/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202021-09-11%20103434.png)

这是官方准备的嵌入代码，可以直接拿来用，但是显示效果不是很理想，样式不是我们希望的，需要调整一下。

```html
<iframe src="//player.bilibili.com/player.html?aid=80241883&bvid=BV15J411s7SZ&cid=169757174&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

从嵌入代码中我们直接得到了aid和cid

我们重新设置一下功能、大小、样式，得到可用的HTML代码

```html
<iframe src="//player.bilibili.com/player.html?aid=80241883&bvid=BV15J411s7SZ&cid=169757174&page=1" scrolling="no" frameborder="no" width="95%" height="600"></iframe></p>
```

以后插入需要的bilibili视频只需要改变上面的aid和cid就可以了！

## 三、移动端适配

```html
<div style="position: relative; padding: 30% 45%;">
<iframe style="position: absolute; width: 100%; height: 100%; left: 0; top: 0;" src="https://player.bilibili.com/player.html?cid=169757174&aid=80241883&page=1&as_wide=1&high_quality=1&danmaku=0" frameborder="no" scrolling="no"></iframe>
</div>
```

可以用这个代码作为样板，以后只需要改变src的id好就可以了！

## 四、参数说明

本来这篇博客是我的游戏之作，但没想到捧场的朋友这么多，我看到评论区有朋友讲清晰度的问题，我这里再说一下几个参数。

```text
https://player.bilibili.com/player.html?cid=169757174&aid=80241883&page=1&as_wide=1&high_quality=1&danmaku=0
```

| key          | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| aid          | 视频ID 就是B站的 avxxxx 后面的数字                           |
| cid          | 应该是客户端id, clientId 的缩写(推测的, 不一定准确) 经过测试, 这个字段不填也没关系 |
| page         | 第几个视频, 起始下标为 1 (默认值也是为1) 就是B站视频, 选集里的, 第几个视频 |
| as_wide      | 是否宽屏 1: 宽屏, 0: 小屏                                    |
| high_quality | 是否高清 1: 高清, 0: 最低视频质量(默认) 如视频有 360p 720p 1080p 三种, 默认或者 high_quality=0 是最低 360p high_quality=1 是最高1080p |
| danmaku      | 是否开启弹幕 1: 开启(默认), 0: 关闭                          |

所以只要设置**high_quality=1**就能开启最高画质了。

B站官方并没有给出文档说明.....但我发现论坛上有一些相关的讨论

[**相关链接**](http://link.acg.tv/forum.php?mod=viewthread&tid=22308&highlight=播放器参数的官方文档在哪里呢)

经测试high_quality参数可以正常使用，此参数控制外链播放器的默认清晰度：
=1时默认清晰度是最高非大会员清晰度，例如：
（1）原视频清晰度有360P、480P、720P，外链播放器默认为最高的720P，
（2）原视频清晰度有360P、480P、720P、1080P，外链播放器默认为最高的1080P，
（3）原视频清晰度有360P、480P、720P、1080P、1080P+，外链播放器默认为1080P，
选择其他清晰度会打开原视频页面，

=其他数值或没有此参数时默认清晰度是360P，选择其他清晰度会打开原视频页面。

## 五、示例

```html
<div style="position: relative; padding: 30% 45%;">
<iframe style="position: absolute; width: 100%; height: 100%; left: 0; top: 0;" src="https://player.bilibili.com/player.html?cid=169757174&aid=80241883&page=1&as_wide=1&high_quality=1&danmaku=0" frameborder="no" scrolling="no"></iframe>
</div>
```

<div style="position: relative; padding: 30% 45%;">
<iframe style="position: absolute; width: 100%; height: 100%; left: 0; top: 0;" src="https://player.bilibili.com/player.html?cid=169757174&aid=80241883&page=1&as_wide=1&high_quality=1&danmaku=0" frameborder="no" scrolling="no"></iframe>
</div>
