---
title: ffmpeg 命令行处理音视频
date: 2018-05-07 11:04:54
tags:
---

## 剪切视频

``` bash
# 通过 input seeking 和 copy 方式剪切 30 秒视频，速度很快
ffmpeg -ss 00:00:00 -to 00:00:30 -accurate_seek -i input.mkv -codec copy -avoid_negative_ts 1 output.mkv
```

## 视频截图

``` bash
# 以 copy 方式输出第 10 秒的截图
ffmpeg -ss 00:00:10 -i input.mkv -vframes 1 output.png
```

## 剪切视频并添加字幕并转换为 MP4

如果通过设置 `-acodec aac` 进行音频转换， `libfdk_aac` 库是必需的，否则需要设置 `-c:a aac -b:a 320k -ac 2` 以达到相同的效果。

``` bash
# 通过 combined seeking 方式先定位到 01:04:50 处，再逐帧定位到 01:05:00
# 从 01:05:00 剪切到 01:10:00
# -copyts 保留原始时间戳
# -vcodec h264 视频以 H.264 编码
# -acodec aac 音频以 AAC 编码
# subtitles=mySubtitles.ass 字幕文件，不需要重设字幕文件时间
# 该方法适合用于剪切大文件
ffmpeg -ss 01:04:50 -i input.mkv -ss 01:05:00 -to 01:10:00 -copyts -c:v libx264 -c:a aac -b:a 320k -ac 2 -vf subtitles=mySubtitles.ass output.mp4
```

## 压缩视频

``` bash
# 压缩为 720P
ffmpeg -i input.mp4 -s hd720 output.mp4

# 压缩为 480P
# -movflags +faststart 将 meta 信息移至头部，无需下载完成即可播放
ffmpeg -i input.mp4 -s hd480 -movflags +faststart output.mp4
```

## 视频转 GIF

``` bash
# 生成 palette
ffmpeg -i input.mp4 -vf fps=15,scale=320:-1:flags=lanczos,palettegen palette.png

# 利用 palette 生成 GIF 能更好地控制输出大小
ffmpeg -i input.mp4 -i palette.png -filter_complex "fps=15,scale=320:-1:flags=lanczos[x];[x][1:v]paletteuse" output.gif
```
