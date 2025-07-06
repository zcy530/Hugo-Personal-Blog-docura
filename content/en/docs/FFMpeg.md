
---
title: FFMpeg
slug: FFMpeg
lastmod: 2025-07-01T00:00:00+00:00
---
# FFMpeg

FFmpeg 是一个强大的多媒体处理工具，支持音视频格式转换、编辑、录制和流媒体处理

## Download

[https://ffmpeg.org/download.html](https://ffmpeg.org/download.html)，下载 **"Full"** 版本的 ZIP 文件

```cpp
cd C:/user/caiyizhang/Downloads/ffmpeg/bin/
ffmpeg -version
```

## Command

```cpp
ffmpeg [输入选项] -i [输入文件] [输出选项] [输出文件]
```

## Example

```cpp
// 将 MP4 转换为 AVI
ffmpeg -i input.mp4 output.avi

// 将 MKV 转换为 MP4
ffmpeg -i input.mkv output.mp4

// 改变帧率
ffmpeg -i input.mp4 -r 30 output.mp4

// 无损转换
// 如果不指定编解码器，FFmpeg 会默认重新编码，可能会损失质量
ffmpeg -i input.mkv -c copy output.mp4

// 压缩视频
// libx265 使用 H.265 编码，-crf 28 控制质量
ffmpeg -i input.mp4 -c:v libx265 -crf 28 output.mp4

// 调整分辨率到 1280x720
ffmpeg -i input.mp4 -vf scale=1280:720 output.mp4

// 裁剪 640x480 居中
ffmpeg -i input.mp4 -vf "crop=640:480:100:50" output.mp4

// 顺时针旋转 90 度
ffmpeg -i input.mp4 -vf "transpose=1" output.mp4

// 剪辑视频
// -ss 开始时间，-to 结束时间，-c copy 直接剪辑不重新编码
ffmpeg -i input.mp4 -ss 00:00:30 -to 00:01:00 -c copy output.mp4
```

## Parameter

FFmpeg 中的 output 参数非常多，但常用的主要涉及 编码器、比特率、分辨率、帧率、音视频流 等方面。以下是常见的 output 选项

| **类别** | **参数** | **用途** | **示例** |
| --- | --- | --- | --- |
| **帧率** | `-r 30` | 设置帧率为 30 FPS | `ffmpeg -i input.mp4 -r 30 output.mp4` |
|  | `-r 60` | 设置帧率为 60 FPS | `ffmpeg -i input.mp4 -r 60 output.mp4` |
| **比特率** | `-b:v 2M` | 视频比特率 2 Mbps | `ffmpeg -i input.mp4 -b:v 2M output.mp4` |
|  | `-b:a 192k` | 音频比特率 192 kbps | `ffmpeg -i input.mp4 -b:a 192k output.mp4` |
| **分辨率** | `-vf scale=1280:720` | 调整视频分辨率到 720p | `ffmpeg -i input.mp4 -vf scale=1280:720 output.mp4` |
|  | `-vf scale=-1:1080` | 宽度自适应，高度固定 1080p | `ffmpeg -i input.mp4 -vf scale=-1:1080 output.mp4` |
| **视频编码** | `-c:v libx264` | 使用 H.264 编码（常见） | `ffmpeg -i input.mp4 -c:v libx264 output.mp4` |
|  | `-c:v libx265` | 使用 H.265 编码（更高压缩比） | `ffmpeg -i input.mp4 -c:v libx265 output.mp4` |
|  | `-c:v vp9` | 使用 VP9 编码（适用于 WebM） | `ffmpeg -i input.mp4 -c:v vp9 output.webm` |
|  | `-c:v copy` | 不重新编码（最快、无损） | `ffmpeg -i input.mp4 -c:v copy output.mp4` |
| **硬件加速** | `-c:v h264_nvenc` | 使用 NVIDIA GPU 硬件加速（H.264） | `ffmpeg -i input.mp4 -c:v h264_nvenc output.mp4` |
|  | `-c:v h264_qsv` | 使用 Intel Quick Sync 硬件加速 | `ffmpeg -i input.mp4 -c:v h264_qsv output.mp4` |
|  | `-c:v h264_amf` | 使用 AMD GPU 硬件加速 | `ffmpeg -i input.mp4 -c:v h264_amf output.mp4` |
| **音频编码** | `-c:a aac` | 使用 AAC 音频编码（MP4 常见） | `ffmpeg -i input.mp4 -c:a aac output.mp4` |
|  | `-c:a mp3` | 使用 MP3 编码 | `ffmpeg -i input.mp4 -c:a mp3 output.mp3` |
|  | `-c:a copy` | 不重新编码（最快、无损） | `ffmpeg -i input.mp4 -c:a copy output.mp4` |
| **恒定质量因子** | `-crf 23` | 控制 H.264 质量（0-51，值越小质量越高） | `ffmpeg -i input.mp4 -c:v libx264 -crf 23 output.mp4` |
|  | `-crf 28` | 控制 H.265 质量（推荐 22-30） | `ffmpeg -i input.mp4 -c:v libx265 -crf 28 output.mp4` |
| **音视频流** | `-an` | 去掉音频，仅保留视频 | `ffmpeg -i input.mp4 -an output.mp4` |
|  | `-vn` | 去掉视频，仅保留音频 | `ffmpeg -i input.mp4 -vn output.mp3` |
| **剪辑** | `-ss 00:00:30 -to 00:01:00` | 截取 00:30-01:00 片段 | `ffmpeg -i input.mp4 -ss 00:00:30 -to 00:01:00 -c copy output.mp4` |
| **旋转** | `-vf "transpose=1"` | 顺时针旋转 90° | `ffmpeg -i input.mp4 -vf "transpose=1" output.mp4` |
|  | `-vf "transpose=2"` | 逆时针旋转 90° | `ffmpeg -i input.mp4 -vf "transpose=2" output.mp4` |
|  | `-vf "transpose=1,transpose=1"` | 旋转 180° | `ffmpeg -i input.mp4 -vf "transpose=1,transpose=1" output.mp4` |
| **裁剪** | `-vf "crop=640:480:100:50"` | 裁剪 640x480，起点 (100,50) | `ffmpeg -i input.mp4 -vf "crop=640:480:100:50" output.mp4` |
| **合并** | `-f concat -safe 0 -i file_list.txt -c copy` | 合并多个相同编码的视频 | `ffmpeg -f concat -safe 0 -i file_list.txt -c copy output.mp4` |