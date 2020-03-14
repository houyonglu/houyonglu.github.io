---
title: ffmpeg 将 GIF 转为 MP4
date: 2017-12-14 09:55:43
tags:
---

## GIF 转换为 MP4

``` bash
ffmpeg -f gif -i "FOO.gif" -pix_fmt yuv420p -c:v libx264 -movflags +faststart -filter:v crop='floor(in_w/2)*2:floor(in_h/2)*2' "BAR.mp4"
```

> 输出的 MP4 文件通过 H.264 编码，兼容 Windows, Mac OSX, Android, iOS。所有主流系统都支持 MP4 格式文件，没有必要生成额外的编码速度更慢的 webm 格式文件。`-movflags +faststart` 参数可让视频无需完成加载即可播放。压缩比通常为 10 : 1，但将小于 512KB 的 GIF 转换为 MP4 效益较低。

## 生成最多不超过 9 张关键帧缩略图

``` bash
ffmpeg -skip_frame nokey -i "BAR.mp4" -vsync 0 -vframes 9 -c:v mjpeg "thumb_%d.jpg"
```
<small>*注： 生成的缩略图数量可能小于指定数量。 *</small>
