---
title: Video Knowledge
slug: Video-Knowledge
lastmod: 2025-07-01T00:00:00+00:00
---


# Video development

# Domin Knowledge

1. 语言基础  C, C++, Java, JNI
2. 视频图像基础  MP4 格式, YUV 格式, FLV 格式, IBP 帧，常见的性能指标
3. 音视频传输协议  WebRTC, RTP, RTCP, RTSP, RTMP, UDP
4. 视频编解码协议  H264, H265, AAC, AV1, VP9, Opus, HEVC
5. 开源多媒体处理框架  FFMpeg, x264 
6. 客户端多媒体相关sdk  Android camera 2, Media codec, iOS AV foundation, Media Capture, Media Foundation, Direct Show, OpenGL ES, GPU Image, Metal
7. 客户端开发  Android native, iOS native, Xamarin
8. 音视频质量优化  jitter buffer, SVC, GCC, FEC, simulcast
9. 找一个实战项目，包含以下功能
    - 功能 list
        - 播放/暂停
        - 变速播放
        - 调节音量
        - 上一/下一视频
        - 显示播放列表
        - 显示缓存时间
        - 实现直播低延迟播放
        - 硬件解码、软件解码切换
        - 多路视频同时播放，比如1080p播放25路
        - 4k/8k渲染的区别
        - 加密解密功能
        - 登录授权功能
        - 播放状态监测功能
        
    - 项目列表
        
        [https://www.udemy.com/course/mastering-webrtc-part-2-real-time-video-and-screen-share/](https://www.udemy.com/course/mastering-webrtc-part-2-real-time-video-and-screen-share/)
        
        [https://www.udemy.com/course/webrtc-2021-practical-course-create-meet-the-strangers-app/](https://www.udemy.com/course/webrtc-2021-practical-course-create-meet-the-strangers-app/)
        
        [https://www.udemy.com/course/the-complete-android-machine-learning-course/?couponCode=OF83024E](https://www.udemy.com/course/the-complete-android-machine-learning-course/?couponCode=OF83024E)
        

# Detail for interview

## **1. 语言基础**

## 2. 图像视频基础

- 图像的参数：像素, 分辨率, 位深, 跨距
    
    
    - **像素：**像素是图像的基本单元，一个个像素就组成了图像
    - **分辨率：**指图像由多少个像素组成，分辨率越高就越清晰。一张 1920x1080 的图像，指的是该图像的宽度方向上有 1920 个像素点，高度方向上有 1080 个像素点
        
        常见的分辨率有 QCIF（176x144）、CIF（352x288）、360P（640x360）、720P（1280x720）、1080P（1920x1080）、4K（3840x2160）
        
        ![Untitled](Untitled.png)
        
    - **位深：**存储每个像素需要的二进制位数，位深越大，颜色值越多，色彩越丰富
        
        常见图像由红绿蓝（RGB）三种颜色通道组成，每个通道用 8 位 (1 字节，表示 256 种颜色，即 2 的 8 次方) 表示，一个像素共占 24 位(3 字节，表示 1677 万种颜色，即 256 的 3 次方)。这类图像通常被称为 8bit 图像，其中的 8bit 指的就是每个通道的位深
        
        | **类型** | **每通道位数** | **总颜色种类** | **特点与用途** |
        | --- | --- | --- | --- |
        | **1 位图像** | 1 位 | 2 种颜色（黑/白） | 二值图（如扫描文档） |
        | **8 位彩色图像** | 每通道 8 位，共 24 位 | 1677 万色 | 最常见的图像格式 |
        | **10 位图像** | 每通道 10 位，共 30 位 | ~10 亿种颜色 | HDR 视频、电影制作 |
        | **12 位图像** | 每通道 12 位，共 36 位 | 更高色彩细节 | 专业摄影、医疗图像 |
        | **16 位图像** | 每通道 16 位，共 48 位 | 超过 280 万亿种颜色 | 天文、工业、科学级图像 |
        | **32 位图像** | 24 位 RGB + 8 位 Alpha | 带透明通道 | UI 图像、PNG 格式 |
        | **高动态范围图像 HDR** | 通常为 10/12/16 位浮点 | 光线更丰富的场景 | 视频 HDR10, Dolby Vision |
        
    - **跨距 Stride：**图像存储时，内存中每行像素所占用的对齐后的空间
        
        一张 1278×720 的 RGB 图像，每个像素占 3 字节，一行共需 1278 × 3 = 3834 字节。但 3834 不是 16 的倍数，不满足内存对齐要求。为了对齐，会在每行末尾补齐到 3840 字节（补 6 字节），这就叫做 **stride = 3840**。读取图像时，若不跳过这多出的字节，就会把它们误当成下一行的像素，导致图像显示异常，比如花屏、斜线等问题
        
        ![Untitled](Untitled%201.png)
        
- 视频的参数：帧率、丢帧率、码率、编码格式、封装格式、峰值信噪比
    
    
    - **帧率**：每秒播放多少帧图像，帧率越高，画面越流畅。24fps 普通、30fps 电影、60fps 游戏
    - **丢帧率：**视频播放中未能按时显示的帧数比例，丢帧率越高，视频会越卡顿
    - **码率**：表示每秒传输的数据量，单位 kbps/Mbps，码率越高，每一帧图像数据越大，越清晰越流畅，细节更丰富，但传输时占用带宽也更大，码率 = 分辨率 × fps × 每像素位数 × 压缩比
    - **编码格式**：把原始视频压缩存储的方式，常见格式有 H.264(AVC)、H.265(HEVC)、AV1，H.265 比 H.264 更高效，同样画质下占用更少带宽
    - **封装格式：**将视频、音频、字幕等打包在一起的文件格式，比如 MP4、MKV、MOV、FLV 等
    - **峰值信噪比 (PSNR)**: 计算压缩视频帧与原始图像间的误差大小，PSNR 越高误差越小，质量越好
    ****
- 图像颜色空间：YUV，RGB，HSV，full / limited range
    
    RGB 适合屏幕显示渲染，YUV 适合压缩和传输， HSV 适合调色和图像处理
    
    - **RGB**
        
        每一个像素由 Red, Green, Blue 三个值加权组成。适合用于显示设备，比如手机屏幕、显示器、摄像头预览。RGB 中每个颜色分量通常用 8 位表示，组合后能表示一千六百万种颜色
        
        注意 RGB 图像像素三个值并不一定是按 R、G、B 顺序排列的，也有可能是 B、G、R 顺序排列。比如 OpenCV 就经常使用 BGR 的排列方式来存储图像
        
    - **YUV**
        
        Y (Luma) 是亮度信息表示总体轮廓，U (Chroma Blue) V (Chroma Red) 描绘图像的色彩信息。YUV 最早主要是用于电视系统与模拟视频领域，现在的视频领域也基本是用 YUV 来表示图像。人眼对亮度更敏感，对色度不敏感，因此可以压缩色度数据而不明显降低画质，常用于视频压缩和传输，例如摄像头输出、视频编码和硬件加速。YUV 常见的排列格式有 YUV420、YUV422、NV12、I420 
        
    - **HSV**
        
        更接近人类感知方式的颜色空间，由色相 H、饱和度 S、明度 V 组成。它更方便做颜色筛选、图像处理和调色等操作，广泛用于图像编辑软件、颜色选取工具和滤镜开发中
        
    
    - **Color Range**
        
        表示颜色通道中像素值的取值范围，分为 full / limited range。full range 表示像素值从 0 ~ 255 全部可用，适用于图像编辑。limited range 只使用中间，比如 Y 范围是 16 ~ 235，UV 范围是 16 ~ 240，是为了兼容传统电视信号和视频标准，避免失真。视频编码常用 limited range，而图像处理常用 full range。如果编解码时 color range 不匹配，会导致图像发灰或对比度异常
        
    
    - **各种格式的使用场景**
        - 摄像头采集：结果一般是 YUV，更适合压缩，节省内存和带宽
        - 图像处理：通常用 RGB，算法大多基于 RGB 设计，需要将 YUV 转换为 RGB
        - 编码解码：H.264、H.265 通常要求输入 YUV 格式
        - 图像显示：显示设备一般只支持 RGB，所有 YUV 视频都需要转为 RGB
    - **RGB 和 YUV 之间的转换**
        
        RGB 和 YUV 互转的标准规范有 BT709 和 BT601，图像的 color range 可能有两种，所以在做 RGB 往 YUV 转换的时候需要知道是哪个标准+ 哪种 Range 
        
        | **标准** | **范围** | **RGB → YUV 公式** | **YUV → RGB 公式** |
        | --- | --- | --- | --- |
        | **BT.601** | **Full** | Y = 0.299R + 0.587G + 0.114B  
        U = -0.14713R - 0.28886G + 0.436B  
        V = 0.615R - 0.51499G - 0.10001B | R = Y + 1.13983V  
        G = Y - 0.39465U - 0.58060V  
        B = Y + 2.03211U |
        | **BT.601** | **Limited** | Y = 16 + (65.481R + 128.553G + 24.966B)/255  
        U = 128 + (-37.797R - 74.203G + 112.0B)/255
        V = 128 + (112.0R - 93.786G - 18.214B)/255 | R = 1.164(Y − 16) + 1.596(V − 128)  
        G = 1.164(Y − 16) − 0.392(V − 128) − 0.813(U − 128)  
        B = 1.164(Y − 16) + 2.017(U − 128) |
        | **BT.709** | **Full** | Y = 0.2126R + 0.7152G + 0.0722B  
        U = -0.1146R - 0.3854G + 0.5B  
        V = 0.5R - 0.4542G - 0.0458B | R = Y + 1.5748V  
        G = Y - 0.1873U - 0.4681V  
        B = Y + 1.8556U |
        | **BT.709** | **Limited** | Y = 16 + (45.75R + 152.0G + 15.75B)/255  
        U = 128 + (-25.5R - 129.0G + 154.5B)/255  
        V = 128 + (154.5R - 129.0G - 25.5B)/255 | R = 1.164(Y − 16) + 1.793(V − 128)  
        G = 1.164(Y − 16) − 0.534(V − 128) − 0.213(U − 128)  
        B = 1.164(Y − 16) + 2.115(U − 128) |
    
- 图像颜色空间：14 种 YUV 的类型和存储方式
    - **YUV 采样类型**：分为 444，422，420 三种类型，主要区别是 UV 分量像素点的个数和采集方式
        
        444：每个像素拥有 1 个 Y 分量和 1 个 U 分量、1 个 V 分量
        
        422：每个像素拥有 1 个 Y 分量和 0.5 个 U 分量、0.5 个 V 分量
        
        420：每个像素拥有 1 个 Y 分量和 0.25 个 U 分量、0.25 个 V 分量
        
        ![image.png](image.png)
        
    - **YUV 存储方式：**主要分为两大类 Planar 和 Packed
        
        ![image.png](image%201.png)
        
    - 总结一共有十四种排列方式
        
        
        | **采样类型** | **排列方式** | **格式名** | **内存结构描述** | **特点与用途** |
        | --- | --- | --- | --- | --- |
        | 4:4:4 | Planar | YUV444P(I444) | YYYYYYYY + UUUUUUUU + VVVVVVVV | 每像素都有完整 YUV，质量最好 |
        |  |  | YUV444P(YV24) | YYYYYYYY + VVVVVVVV + UUUUUUUU | 也是 YUV444P，只是U/V 顺序互换 |
        | 4:2:2 | Planar | YUV422P(I422) | YYYYYYYY + UUUU + VVVV | 水平减半采样，适中清晰度 |
        |  |  | YUV422P(YV16) | YYYYYYYY + VVVV + UUUU | 也是 YUV422P，只是U/V 顺序互换 |
        |  | Packed | NV16 | YYYYYYYY + UVUVUVUV | 水平减半，无垂直压缩 |
        |  |  | NV61 | YYYYYYYY + VUVUVUVU | 同 NV16 顺序不同 |
        |  |  | YUY2 | Y0 U0 Y1 V0，Y2 U1 Y3 V1，…. | USB 摄像头、Windows 平台常用 |
        |  |  | UYVY | U0 Y0 V0 Y1，U1 Y2 V1 Y3，… | 与 YUY2 顺序不同 |
        |  |  | YVYU | Y0 V0 Y1 U0，Y2 V1 Y3 U1，… | 不常见变体 |
        |  |  | VYUY | V0 Y0 U0 Y1，V1 Y2 U1 Y3 | 很少使用 |
        | 4:2:0 | Planar | YU12(I420) | YYYYYYYY + UUUU + VVVV | 垂直和水平均减半，主流压缩格式 |
        |  |  | YV12 | YYYYYYYY + VVVV + UUUU | I420 的变种，U/V 交换顺序 |
        |  | Packed | NV12 | YYYYYYYY + UVUVUVUV | Intel 平台和硬件编解码常用 |
        |  |  | NV21 | YYYYYYYY + VUVUVUVU | Android 默认格式 |
- 视频容器格式：MP4，FLV，MKV，MOV
    
    经过 H.264 / H.265 编码后的视频本身只是压缩后的码流（bitstream），还不能单独作为一个可播放的文件，它通常需要被封装进容器格式，才成为一个完整的视频文件，除非通过特定工具 FFmpeg 
    
    | **格式** | **类型** | **支持的编码** | **优点** | **缺点** | **适用场景** |
    | --- | --- | --- | --- | --- | --- |
    | MP4 | 通用容器 | H.264/H.265/AAC | 广泛兼容，压缩效率高 | 不支持复杂菜单或多音轨 | 网络视频、社交平台、移动设备 |
    | MKV | 开源容器 | 几乎所有编码格式 | 支持多视频流、多音轨、多字幕 | 某些设备支持度低 | 高清视频存储、多语言影片 |
    | MOV | Apple 容器 | H.264/ProRes/AAC | 与 Apple 设备兼容性好 | 文件大，跨平台兼容性差 | 苹果设备、视频编辑 |
    | FLV | Flash 容器 | H.263/VP6/H264 | 适合流媒体，文件小 | Flash 已淘汰，兼容性差 | 旧版网页视频 |
    
    - **MP4：**常见的数字多媒体容器格式，用于存储视频、音频、字幕和图片等内容，几乎所有设备和操作系统（Windows、macOS、Android、iOS）都能支持。压缩效率高，减小文件大小
    - **MKV**：支持多个视频流、音频流、字幕，适合高清电影和多语言视频文件的存储，几乎所有视频编码（如 H.264、VP9）和音频编码都兼容，通常用于存储高质量的影片，适合电影专业人员
    - **MOV**：由 Apple 公司推出的多媒体容器格式，广泛用于 QuickTime 播放器中，支持视频、音频和字幕等，Apple 设备（如 macOS、iOS）中视频播放的标准格式
    - **FLV**：由 Adobe 提出的 Flash 视频格式，主要用于在线视频流的传输和播放，通常需要 Flash Player 插件来播放，随着 HTML5 的普及，Flash 被逐步淘汰，FLV 格式也因此不再被广泛使用
- 帧类型：I 帧，P 帧，B 帧，IDR 帧，GOP 图像组，Slice
    
    ![Untitled](Untitled%202.png)
    
    - **I 帧：**帧内编码帧，I表示关键帧，这一帧画面的完整保留，解码时只需要本帧数据就可以完成
    - **P 帧：**前向预测编码帧，表示的是这一帧跟前一个 I 帧或 P 帧的差别。具体方法是，以参考帧找出某点的预测差值和运动矢量一起传送，解码时，根据运动矢量从参考帧找出 P 帧某点的预测值并与差值相加以得到 P 帧某点样值，从而可得到完整的 P 帧
    - **B 帧：**双向预测内插编码帧，记录本帧与前后帧的差别。以前面的 I 或 P 帧和后面的 P 帧为参考帧，找出 B 帧某点的预测值和两个运动矢量一起传送。解码时根据运动矢量在两个参考帧中算出预测值并与差值相加，得到 B 帧某点样值，从而可得到完整的 B 帧。压缩率高，但解码开销大
    - **IDR 帧：**首个 I 帧叫 IDR，IDR 即时解码刷新 (Instantaneous Decoding Refresh)，I 和 IDR 帧是一样的，只是为了将首个 I 帧和其他 I 帧区别开。IDR 作用是立刻刷新，使错误不会一直传播（由于 P/B 帧需要参考其它帧。如果编解码过程中有一个参考帧出现错误，那依赖它的 P/B 帧肯定也会出错，而这些有问题的 P 帧又会继续作为之后 P/B 帧的参考帧）
        
        H264 编码标准中规定，从 IDR 帧开始，重新算一个新的序列开始编码，DPB（参考帧列表）清空，在 IDR 帧之后的所有帧都不能引用任何 IDR 帧之前的帧的内容
        
        播放器永远可以从一个 IDR 帧播放，因为在它之后没有任何帧引用之前的帧。但是，不能在一个没有 IDR 帧的视频中从任意点开始播放，因为后面的帧总是会引用前面的帧
        
    - **GOP 图像组**：Group of Pictures，是视频编码中一组连续帧的结构单位，从一个 IDR 帧开始到下一个 IDR 帧的前一帧为止，这里面包含的 IDR 帧、普通 I 帧、P 帧和 B 帧
        
        GOP 大的好处：I 帧越少，而P 帧、B 帧的压缩率更高，因此整个视频的编码效率就会越高
        
        GOP 大的坏处：IDR 帧距离太大，点播场景的视频 seek 操作会不方便。而且 RTC 场景中，可能会因为网络原因丢包，导致接收端参考帧丢失而出现解码错误，从而引起长时间花屏和卡顿
        
        ![Untitled](Untitled%203.png)
        
    - **Slice**：一帧图像划分为数个 Slice，一个 Slice 又划分为数个宏块，宏块大小是 16 x 16。Slice 之间相互独立、互不依赖、独立编码，就可以多线程并行对多个 Slice 进行编码，从而提升速度。但因为一帧几个 Slice 是相互独立，所以如果帧内预测不能跨 Slice 进行，因此编码性能会差一些
        
        ![Untitled](Untitled%204.png)
        
    
- Video pipeline 的数据格式转换表
    
    
    | **阶段** | **数据格式** | 文件名 |
    | --- | --- | --- |
    | Capturer | YUV / Texture | .yuv |
    | Preview | RGB / Texture | .png、.bmp |
    | Encoder | H.264 / H.265 / VP9 | .h264、.h265、bitstream |
    | Transport | RTP / HLS / RTMP 包 | .pcap、.ts |
    | Decoder | YUV / Texture | .yuv |
    | Render | RGB / Texture | .png、.bmp |
- 码流的结构和传输 Bitstream
    - **码流的产生**：由编码器生成的，经过压缩后的二进制数据流，包含了编码后的视频帧的所有信息
    - 码流结构：指视频经过编码之后得到的二进制数据是怎么组织的，也就是说，怎么在在二进制码流数据中，分辨出哪一块数据是一帧图像，哪一块数据是另外一帧图像，H264 码流有两种格式：
        - **Annexb 格式：**使用起始码来表示一个编码数据的开始。起始码本身不是图像编码的内容，只是用来分隔用的。起始码有两种，一种是 4 字节的 00 00 00 01，一种是 3 字节的 00 00 01
        - **MP4 格式：**没有起始码，而是在图像编码数据的开始使用了 4 个字节作为长度标识，用来表示编码数据的长度，这样每次读取 4 个字节，计算出编码数据长度，然后取出编码数据
    - **码流的传输**：通常通过流媒体协议进行传输，例如直播视频流通过 RTP 或 RTSP 协议将压缩后的码流传输到接收端，传输通常考虑到带宽和延迟，可以采用自适应比特率传输（ABR）等技术
    - **码流的保存**：音视频码流会被封装在容器中，方便存储和播放。容器不仅包含编码后的音视频数据，还包含字幕、元数据、章节信息等。例如，MP4 容器包含 H.264 视频码流和 AAC 音频码流
    - **码流的解码**：接收端会使用相应的解码器来读取并解码码流，还原为原始的视频帧进行显示播放

## 3. Android 图像基础

- Frame buffer 采集的流程
    
    梳理了一下 capturer pipeline 的整个过程
    
    1. **Enuermation**: 通过 CameraManager 枚举摄像头，通过 CameraCharacteristics 来获取摄像头数据，方向，支持的分辨率，帧率等，保存摄像头信息供后续使用
    2. **Initialization**: RtcpalVideoSourceDL 调用 capturer.create() 创建 capturer 实例，对应着创建 camera manager，并且使用 openCamera() 来创建 CameraDevice 的过程
    3. **Capturing**: CameraDevice 通过 createCaptureSession() 来创建 CaptureSession，在 buffer mode 下会使用 ImageReader 的 Surface，在 texture mode 会使用 SurfaceTexture，来与 CaptureSession 关联起来。  CaptureSession 创建好后通过 setRepeatingRequest() 来请求 frame，Camera HAL 也就是硬件层会把获取到的 frame 传到前面这两种 surface 所绑定的 BufferQueue 里面
    4. **Frame delivering**: BufferQueue 收到帧之后，会触发回调函数也就是 ImageReader.onImageAvailable() 或者 SurfaceTexture. OnFrameAvailableListener。这两个回调函数内部，又会调用两个 JNI 回调函数也就是 onCpuFrameCaptured() 或者 onGpuFrameCaptured() 传入 video source
    5. **Frame buffer → Texture**: 如果使用的是 texture mode 则还有一步就是 Camera HAL 将 frame buffer 写入 SurfaceTexture 内部的 GraphicBuffer 之后，SurfaceTexture 会把收到的帧通过 updateTexImage() 映射成绑定的 OpenGL texture（GLuint）
- SurfaceTexture 使用 EGL OpenGL ES 渲染的流程
    1. Camera 输出一帧到 SurfaceTexture，响应 SurfaceTexture.OnFrameAvailableListener 回调，可以通过把 frame buffer 映射到到一个 OpenGL texture
    2. EGL 初始化，创建 EGLDisplay、EGLContext、EGLSurface，EGL 是管理 OpenGL 上下文和屏幕的桥梁
    3. OpenGL 渲染这一帧：更新 SurfaceTexture 内容 updateTexImage()，获取帧的纹理矩阵 getTransformMatrix(), 通过 顶点着色器（Vertex Shader）和片元着色器（Fragment Shader）
    绘制从 SurfaceTexture 拿到的纹理，eglSwapBuffers 显示到频幕上
    

## **3. 音视频传输协议**

- WebRTC 概念理解
    
    Web Real-Time Communication
    
    WebRTC 是浏览器内置的一个实时通信技术，能够让开发者在浏览器或者移动应用中，实现实时的音频、视频以及数据低延迟的传输，而无需额外插件(Flash)，以及在链接成功后不需要中转服务器
    
    他提供了一套接口，开发者可以轻松的在浏览器构建端对端的实时通信，涵盖从 capture，preview，encoder，transport，decoder，render 整个 pipeline 的全过程
    
    - 在**浏览器端**（Chrome, Firefox, Safari 等），你可以直接使用 JavaScript 的 WebRTC API
    - 在**移动端**，你可以使用 WebRTC 的 Android 或 iOS SDK 开发原生 app
    
- WebRTC 工作和连接的流程
    
    
    ![image.png](image%202.png)
    
    ![image.png](image%203.png)
    
    Client1 发 SDP offer
    
    1. Client1 getUserMedia，获取 localStream
        
        ```jsx
        localStream = await navigator.mediaDevices.getUserMedia({ audio: true, video: true });
        ```
        
        获取摄像头和麦克风权限
        
        拿到本地媒体流，可进行本地预览
        
    2. Client1 创建 PeerConnection 并添加到 localStream
        
        ```jsx
        const pc1 = new RTCPeerConnection(config);
        localStream.getTracks().forEach(track => pc1.addTrack(track, localStream));
        ```
        
    3. Client1 创建 SDP offer，发给 Signaling Server，Signaling Server 把 SDP offer 转发给 Client2
        
        ```jsx
        const offer = await pc1.createOffer();
        await pc1.setLocalDescription(offer);
        ```
        
    
    Client2 回 SDP answer
    
    1. Client2 收到 offer，getUserMedia，获取 local stream ****
        
        ```jsx
        localStream = await navigator.mediaDevices.getUserMedia({ audio: true, video: true });
        ```
        
    2. Client2 创建 PeerConnection 并添加到 localStream
        
        ```jsx
        const pc2 = new RTCPeerConnection(config);
        localStream.getTracks().forEach(track => pc2.addTrack(track, localStream));
        ```
        
    3. Client2 使用 SDP offer 设置远端描述，准备接收媒体 ****
        
        ```jsx
        
        const remoteDesc = new RTCSessionDescription(offer);
        await pc2.setRemoteDescription(remoteDesc);
        ```
        
    4. Client2 创建 SDP answer，并把 answer 发给 Signaling Server，Signaling Server 将 SDP answer 转发回 Client1
        
        ```jsx
        const answer = await pc2.createAnswer();
        await pc2.setLocalDescription(answer);
        ```
        
    
    8. Client1 收到 SDP answer，设置远端描述
    
    ```jsx
    const remoteDesc = new RTCSessionDescription(answer);
    await pc1.setRemoteDescription(remoteDesc);
    ```
    
    ICE Candidate 交换，建立连接，开始通信
    
    1. 双方交换 ICE 候选
        
        浏览器通过 ICE 框架获取可用的网络地址（NAT 穿透）
        
        每当一个候选可用，就通过信令服务器转发给对方
        
        ```jsx
        pc1.addIceCandidate(candidate);
        pc2.addIceCandidate(candidate);
        ```
        
    2. 连接建立，媒体流传输
        
        点对点媒体连接建立后，音频/视频通过 SRTP 在 Client1 和 Client2 间直接传输，Signaling Server 不再参与任何数据
        
    
- 理解 ICE candidate 和 NAT 内网穿透
    - **NAT（Network Address Translation）**
        
        是路由器用来让多个设备共享一个公网 IP 的机制，你的电脑在内网 IP 是 192.168.1.10，访问外网时，路由器会“转换”成公网 IP（比如 203.0.113.7）。这是为了 节省公网 IP 数量，提高安全性，因为外部访问不到你内网设备
        
    - **NAT Traversal 内网穿透**
        
        多数用户都在 NAT 后，比如家用 WiFi，公司局域网等，无法直接点对点通信。而内网穿透是一种绕过 NAT 限制，让两个都在 NAT 背后的设备建立连接的技术
        
    
    - **ICE（Interactive Connectivity Establishment）**
        
        ICE 是一套帮助 WebRTC 客户端“穿透 NAT，建立连接”的技术机制，过程依赖收集和测试多种ICE 候选地址，以实现内网穿透
        
        1. 每个客户端会收集三类 ICE 候选地址
        2. 通过 Signaling Server 互换 ICE 候选地址
        3. 双方尝试所有候选对，自动检测哪一对能连通
        4. 成功了，就选最优路径连接
        
    - **ICE Candidate**
        
        就是浏览器尝试建立连接时收集到的一种可用地址，WebRTC 为了确保连接成功，会尽可能多收集几种地址，双方都收集这些候选地址，然后逐个尝试组合（A 的地址 + B 的地址）进行连接
        
        | **类型** | **名字** | **来源** | **作用** |
        | --- | --- | --- | --- |
        | 本地地址 | host | 自己电脑的局域网 IP | 最快，适用于同一网络 |
        | 公网映射地址 | server reflexive | STUN 服务器获取 | 用于告诉对方“我在公网是这个 IP/端口” |
        | 中继地址 | relay | TURN 服务器分配 | 点对点失败时中继音视频数据 |
    
- 理解三种服务器：STUN/TURN/Signal server
    
    ```jsx
    +-----------+         +--------------------+         +-----------+
    |  Client A | <--->   |  Signaling Server  | <--->   |  Client B |
    +-----------+         +--------------------+         +-----------+
         |                       |                             |
         |    getUserMedia       |                             |
         |    createOffer        |                             |
         |-----> SDP offer ------>                             |
         |                       | -----> SDP offer ---------->|
         |                       | <----- SDP answer ----------|
         |<----- SDP answer <-----                             |
         |                       |                             |
         |<-> ICE Candidates <-> | <->   ICE Candidates <->    |
         |      |                |                |            |
         |      V                |                V            |
         |  +---------+      +---------+      +---------+      |
         |  |  STUN   |      |  TURN   |      |  STUN   |      |
         |  +---------+      +---------+      +---------+      |
         |      |                                 |            |
         |      |----------- P2P if possible -----|            |
         |                  Fallback to TURN                   |
         |---------------------------------------------------->|
    ```
    
    - **STUN Server：**告诉客户端自己在公网下的 IP/端口（为 NAT 穿透准备），便宜轻便
    - **TURN Server**：当 NAT 穿透失败时，使用 TURN server 中转音视频数据代替直连。比如企业内防火墙、对称 NAT，客户端和对端都无法直接连接，只能通过 TURN。比较贵因为服务器需要更大的贷款，通常只作为 falback 使用
    - **Signaling server**：帮助客户端交换 SDP 和 ICE 信息，建立连接用，只负责牵线搭桥，WebRTC 没规定你怎么实现 Signaling，只要能收发消息就行
    
- Webrtc demo link
    
    [https://github.com/zcy530/WebrtcDemo/tree/main](https://github.com/zcy530/WebrtcDemo/tree/main)
    
    server.js
    
    ```jsx
    const express = require('express');
    const app = express();
    const http = require('http').createServer(app);
    const io = require('socket.io')(http);
    
    app.use(express.static('public'));
    
    io.on('connection', socket => {
      console.log('User connected:', socket.id);
    
      socket.on('join', room => {
        socket.join(room);
        console.log(`${socket.id} joined room ${room}`);
        socket.to(room).emit('ready');
      });
    
      socket.on('offer', (offer, room) => {
        socket.to(room).emit('offer', offer);
      });
    
      socket.on('answer', (answer, room) => {
        socket.to(room).emit('answer', answer);
      });
    
      socket.on('ice-candidate', (candidate, room) => {
        socket.to(room).emit('ice-candidate', candidate);
      });
    });
    
    http.listen(3000, () => {
      console.log('Signaling server running on http://localhost:3000');
    });
    ```
    
    index.html
    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <title>WebRTC Demo</title>
    </head>
    <body>
      <h2>WebRTC Video Chat</h2>
      <video id="localVideo" autoplay muted playsinline></video>
      <video id="remoteVideo" autoplay playsinline></video>
    
      <script src="/socket.io/socket.io.js"></script>
      <script>
        const room = 'test-room';
        const socket = io();
        const localVideo = document.getElementById('localVideo');
        const remoteVideo = document.getElementById('remoteVideo');
    
        let localStream, peer;
    
        socket.emit('join', room);
    
        socket.on('ready', startCall);
    
        socket.on('offer', async (offer) => {
          await createPeer();
          await peer.setRemoteDescription(offer);
          const answer = await peer.createAnswer();
          await peer.setLocalDescription(answer);
          socket.emit('answer', answer, room);
        });
    
        socket.on('answer', async (answer) => {
          await peer.setRemoteDescription(answer);
        });
    
        socket.on('ice-candidate', async (candidate) => {
          try {
            await peer.addIceCandidate(candidate);
          } catch (e) {
            console.error('Error adding received ice candidate', e);
          }
        });
    
        async function startCall() {
          await createPeer();
          const offer = await peer.createOffer();
          await peer.setLocalDescription(offer);
          socket.emit('offer', offer, room);
        }
    
        async function createPeer() {
          localStream = await navigator.mediaDevices.getUserMedia({ video: true, audio: true });
          localVideo.srcObject = localStream;
    
          peer = new RTCPeerConnection();
    
          localStream.getTracks().forEach(track => peer.addTrack(track, localStream));
    
          peer.ontrack = event => {
            remoteVideo.srcObject = event.streams[0];
          };
    
          peer.onicecandidate = event => {
            if (event.candidate) {
              socket.emit('ice-candidate', event.candidate, room);
            }
          };
        }
      </script>
    </body>
    </html>
    ```
    
- HTTP / HTTPS
    
    HTTP 协议
    
    超文本传输协议（HyperText Transfer Protocol），它是基于 TCP 协议的应用层传输协议，简单来说就是客户端和服务器进行数据传输的一种规则，是一种发布和接收 HTML 页面的方法。客户端给服务端发送 request，服务端返回 response
    
    - HTTP 默认工作在 TCP 协议 80 端口，用户访问网站 http:**//** 打头的都是标准 HTTP 服务
    - HTTP 使用 TCP 三次握手建立连接，客户端和服务器需要交换3个包
    - HTTP是一种无状态协议, 不会对发送过的请求和相应的通信状态进行持久化处理，是为了保持 HTTP 协议的简单性，从而能够快速处理大量的事务，提高效率
    - HTTP 协议以明文方式发送内容，不提供任何方式的数据加密，如果攻击者截取了Web 浏览器和网站服务器之间的传输报文，就可以直接读懂其中的信息，因此，HTTP协议不适合传输一些敏感信息，比如：信用卡号、密码等支付信息
    
    HTTPS 协议
    
    超文本传输加密协议（Hypertext Transfer Protocol Secure），是由 HTTP+SSL 协议构建的可加密传输、身份认证的网络传输协议，数据传输过程是加密的，安全性较好，可以保护交换数据的隐私与完整性。HTTPS 经由 HTTP 进行通信，利用 SSL/TLS 来加密数据包
    
    - HTTPS  默认工作在 TCP 协议 443 端口
    - HTTPS 除了 TCP 三次握手建立连接的三个包，还要加上 SSL 握手的9个包，一共是12个包
    - 网页以加密的方式传输，用协商的对称加密算法和密钥加密，保证数据机密性。用协商的hash算法进行数据完整性保护，保证数据不被篡改
    
- TCP/UDP
    
    视频传输通常使用 UDP，但在某些特定场景下也会使用 TCP
    
    - 速度快延迟低：UDP是无连接协议，不需要三次握手和等待确认，适合实时性高的视频通话、直播
    - 容错性强：视频传输能容忍部分丢包。比如丢了 1 帧，下一帧照样能解码，肉眼不一定能察觉
    - 带宽效率高：UDP 不处理重传，不对乱序包排序，也不做流控，避免了大量 TCP 的开销
- RTP - Real-Time Transport Protocol
    
    RTP是一种网络协议，专门用于传输实时音视频数据。RTP协议确保数据的有序传输并提供时间戳和序列号，用于同步音视频和检测数据包丢失。RTP通常与RTCP配合使用，用于实时多媒体通信中的数据传输，如视频会议、VoIP等
    
- RTCP - RTP Control Protocol
    
    RTCP是RTP的控制协议，主要用于监控数据传输质量，并向发送方提供反馈信息。RTCP可以传输数据包丢失、延迟、抖动等信息，帮助发送方调整数据流的传输速率和质量。它在确保实时通信的可靠性和质量方面起着关键作用
    
- RTSP - Real-Time Streaming Protocol
    
    RTSP是一种网络控制协议，主要用于控制流媒体服务器，支持命令如播放、暂停和停止。RTSP本身并不传输数据，它主要用于控制RTP传输流。因此，RTSP常用于点播系统、监控系统中，支持客户端对音视频流的灵活控制
    
- RTMP - Real-Time Messaging Protocol
    
    RTMP是由Adobe开发的协议，广泛应用于直播流媒体传输，特别是在Flash播放器中。RTMP支持低延迟的视频传输，常用于直播平台。尽管Flash的使用已经减少，但RTMP仍在许多直播平台上得到支持，用于在服务器和客户端之间传输音视频数据
    

## 4. 视频编解码协议

- 压缩的必要性
    
    一个视频一秒钟不压缩的内存是 710 MB，相当于带宽需要 710 Mbps，编码之后的带宽是 2-10 Mbps，视频压缩的目的就是可以用尽量少的带宽，传送更高质量的图像
    
    YUV420: 表示有 YUV 三个分量，每个像素有一个亮度分量，有 1/4 个 U 分量和 1/4 个 V 分量
    
    ![image.png](image%204.png)
    
- 视频编码的步骤：分块，预测，转换，量化，熵编码
    1. **Devide 分块**
        
        把一个图像分为一些大小相等的块，比如说 H264 里面宏块的大小就是 16x16， H265 里是 64x64，就可以适用于更大的图像比如 4K 之类的
        
    2. **Prediction 预测**
        
        用来处理空域和时域信息，通过预测得到的残差块相比原本的编码块，去除了大部分空间冗余信息和时间冗余信息。GOP 里面有大量的 I/B/P 帧，I 帧使用帧内预测，BP 帧使用 帧间预测。因为Teams 是实时的，所以一般不用 B 帧，只用 P 帧，像 I P P P P 
        
        - **帧内预测**：去除了本帧的空间冗余，跟其他的帧没有关系，自己就能解。(1) 已编码完成的块中，找到将编码块的相邻的块，比如左边块、上边块、左上角块和右上角块，(2) 将相邻块与编码块相邻的像素，映射得到预测块，(3) 编码块减去预测块得到残差块，(4) 取所有算法计算出残差块中绝对值加起来最小的，为最后结果
            
            ![Untitled](Untitled%205.png)
            
        - **帧间预测**：将已编好的参考帧中每一个块作为对应预测块，用编码块与预测快做差值，得到残差块，取所有计算出的残差块中绝对值加起来最小的，为最后结果
    3. **DCT Transform 变换** 
        
        DCT 离散余弦变换，用来处理频域信息。人眼对于图像中高频信息(右下角，包含细节、纹理、噪声等) 的敏感度小于低频信息 (左上角，包含图像的亮度、颜色平滑变化等基本信息)。有的时候去除图像中的一些高频信息，人眼看起来差别不大
        
        ![image.png](image%205.png)
        
        $F(u) = \alpha(u) \sum_{x=0}^{N-1} f(x) \cdot \cos\left[ \frac{\pi (2x + 1) u}{2N} \right]$
        
    4. **Quantization 量化**
        
        按一定精度进行压缩，就是把大的数变成小的数，可以简单理解为除法，这样会出现更多的零，压缩效果更好，但也会带来失真。图像的失真主要来自量化这一步。QP（量化参数）越大，压缩越强，失真越明显，画质越差。QP 小，画质好但码率高。如果带宽低，就可以通过提高 QP 来控制输出的画质和码率
        
    5. **Entropy Coding 熵编码**
        
        根据不同数据出现的频率，使用更短的码给频率高的符号，长码给频率低的符号，从而减少整体数据量。比如有熵编码，霍夫曼编码，算术编码，在 264 里对于分辨率高一点的都用算术编码（arithmetic coding）来实现，因为复杂性比较高，压缩率比较高，用硬件实现的话收益就比较大。编码带来的压缩率就是 1/2 或者 1/4，也不会引入失真，因为这个过程是可逆的
        
    
- 视频解码的步骤：熵解码，反量化，反变换，预测重建，去块，滤波
    1. 熵解码：Decoder 这边是相反的，先解码，然后反量化反变换
    2. 滤波：因为他在量化或者预测的过程中可能会失真，引起一些块效应。所以再最后解码的部分他又加上了 deblocking 这个滤波，然后 H265 里面他又加上了 SAO 这种算法，为了这个图像主观看上去更好一些
    3. **去块滤波器，环路滤波器**
- 编码标准：H254, H265, H266, VP9, AV1, ProRes
    
    
    | **编码格式** | **全称** | **特点** | **应用场景** |
    | --- | --- | --- | --- |
    | **H.264** | AVC | 平衡压缩率和兼容性，广泛使用 | MP4 视频、流媒体、微信、抖音等 |
    | **H.265** | HEVC | 同画质下比 H.264 更小，适合 4K/8K，但计算复杂度高 | 4K/8K 视频、高清电视、Netflix |
    | **VP9** | Google | 类似 H.265，YouTube 专用较多 | YouTube、Chrome 浏览器 |
    | **AV1** | AudioVideo 1 | 开源免专利费，比 H.265 更高效 | YouTube、Netflix、新一代网络视频 |
    | **ProRes** | Apple ProRes | 保留高质量画质，压缩轻微，适合编辑 | Final Cut Pro |
    | **H.266** | VVC | 下一代，比 H.265 压缩率再高 50% | 未来 8K、XR 等超高清视频场景 |
- Video H.264 (AVC, Advanced Video Coding)
    
    H.264 是目前最广泛使用的视频编码标准之一，提供高压缩比和良好的视频质量
    
    基于以下主要技术框架
    
    - **帧间预测（Inter prediction）**：参考前后帧压缩冗余
    - **帧内预测（Intra prediction）**：利用当前图像块内的空间冗余压缩
    - **变换（Transform）**：通常是整数 DCT，压缩能量
    - **量化（Quantization）**：控制码率/画质平衡
    - **熵编码（Entropy coding）**：H.264 用 CAVLC/CABAC，H.265 只用 CABAC
    - **去块滤波器（Deblocking filter）**：去除宏块边界伪影
    - **环路滤波（Loop filters）**：如 SAO（H.265 特有），进一步增强主观质量
    
    主要的概念
    
    - **宏块（Macroblock, 16x16）**：最小处理单元
    - **预测单位（PU）** 和 **变换单位（TU）** 与宏块绑定
    - **熵编码**：CAVLC（baseline）或 CABAC（main/high）
    - **编码复杂度相对较低**，适用于实时编码（如视频会议）
- Video H.265 (HEVC, High Efficiency Video Coding)
    
    H.265 是 H.264 的继任者，提供了比 H.264 高 50% 的压缩比和更好的视频质量，在相同的图像质量下，可以比H.264减少约50%的带宽需求，适用于 4K 和 8K 视频传输
    
    **H.265 特别增强的实现结构**
    
    - **编码树单元（CTU, 最大 64x64）**：替代 H.264 的宏块，更灵活
    - **树状划分（Quad-Tree）**：CTU → Coding Unit（CU）→ Prediction Unit（PU）和 Transform Unit（TU）
    - **更多帧间预测模式**：提升编码效率
    - **环路滤波器新增 SAO（Sample Adaptive Offset）**
    - **并行友好设计（Tiles/WPP）**：适合多核处理器并发编码
    
- 基本单位：Macroblock / Slice /  GOP / NALU
    - **宏块 Macroblock**
        
        视频编码技术的基本单元。H264 中，宏块的大小通常是 16×16 像素，如果是 YUV420，则表示一个 16×16 的亮度块，两个 8×8 的色度块。H265 引入了更灵活的单元划分概念，编码树单元 CTU，支持大小从 16×16 到 64×64 像素的宏块
        
        视频帧被分成宏块后，可以分别对每个块执行编码操作，减少计算复杂度，提升压缩率
        
- SPS / PPS
- Audio AAC (Advanced Audio Coding)
    
    AAC是一种高效的音频编码格式，广泛应用于流媒体、数字广播和音乐压缩中。AAC提供了比MP3更高的音质和更好的压缩效率，尤其是在低码率下表现出色。因此，它被采用为许多流媒体平台和数字音频广播（DAB）的标准。
    
- AV1 (AOMedia Video 1)
    
    AV1是一种开源、免版税的视频编码格式，由AOMedia开发，旨在取代H.264和H.265。AV1在保持相同视频质量的情况下提供了更高的压缩效率，是流媒体平台未来的潜在标准，尤其在高分辨率和低带宽环境中优势明显。
    
- VP9 (Google)
    
    VP9是由Google开发的视频编码格式，主要用于YouTube等平台，作为H.265的开源替代方案。VP9提供了与H.265相当的压缩效率，但由于它是开源的，没有使用许可费用，因此在开源社区和非商业应用中受到青睐。
    
- 硬件加速
    
    ## **如何使用 `MediaCodec` 进行硬件加速？**
    
    `MediaCodec` 主要依赖设备的 **硬件编解码器** 来实现 **硬件加速**。相比于纯软件解码（如 `FFmpeg` 的 `libx264`），硬件解码可以更高效、低功耗，适用于 **视频播放器、视频通话、直播推流、视频录制** 等场景。
    
    ---
    
    ## **一、如何启用硬件加速？**
    
    ### **1. 选择支持的硬件编解码器**
    
    Android 提供的 `MediaCodecList` 可以列出所有可用的编解码器。通常，名称带有 `OMX` 的表示硬件加速。例如：
    
    - `OMX.qcom.video.decoder.avc`（高通硬件 H.264 解码器）
    - `OMX.google.h264.decoder`（Google 纯软件解码器，非硬件）
    
    ### **获取设备支持的硬件编解码器**
    
    ```java
    java
    CopyEdit
    MediaCodecList codecList = new MediaCodecList(MediaCodecList.ALL_CODECS);
    for (MediaCodecInfo codecInfo : codecList.getCodecInfos()) {
        if (!codecInfo.isEncoder()) { // 只获取解码器
            for (String type : codecInfo.getSupportedTypes()) {
                Log.d("Codec", "支持的编解码器: " + codecInfo.getName() + " -> " + type);
            }
        }
    }
    
    ```
    
    ---
    
    ### **2. 选择合适的 `MediaCodec`**
    
    默认情况下，`MediaCodec.createDecoderByType("video/avc")` 会自动选择可用的 H.264 硬件解码器。但可以手动指定 **硬件编解码器**：
    
    ```java
    java
    CopyEdit
    String codecName = "OMX.qcom.video.decoder.avc"; // 高通硬件解码器
    MediaCodec codec = MediaCodec.createByCodecName(codecName);
    
    ```
    
    如果设备不支持该硬件编解码器，可以回退到 `createDecoderByType()` 自动选择。
    
    ---
    
    ### **3. 使用 `Surface` 进行零拷贝解码**
    
    当 `MediaCodec` 直接输出到 `Surface` 时，视频帧不会拷贝到 CPU 内存，而是直接由 GPU 渲染，提高性能。
    
    ```java
    java
    CopyEdit
    Surface surface = new Surface(textureView.getSurfaceTexture()); // TextureView
    MediaCodec codec = MediaCodec.createDecoderByType("video/avc");
    MediaFormat format = MediaFormat.createVideoFormat("video/avc", width, height);
    codec.configure(format, surface, null, 0); // 绑定 Surface，启用硬件加速
    codec.start();
    
    ```
    
    ---
    
    ## **二、硬件解码：使用 `MediaCodec` 进行 H.264 硬件解码**
    
    **目标**：用 `MediaCodec` 通过硬件加速 **解码** H.264 视频流，并直接渲染到 `Surface` 上。
    
    ### **解码流程**
    
    1. **初始化 `MediaCodec`**，绑定 `Surface`
    2. **读取 H.264 码流**
    3. **将数据送入 `MediaCodec`**
    4. **从 `MediaCodec` 获取解码后的视频帧**
    5. **输出到 `Surface` 进行显示**
    
    ### **代码示例**
    
    ```java
    java
    CopyEdit
    // 1. 创建 MediaCodec 解码器
    MediaCodec codec = MediaCodec.createDecoderByType("video/avc");
    
    // 2. 配置解码器
    MediaFormat format = MediaFormat.createVideoFormat("video/avc", width, height);
    codec.configure(format, surface, null, 0); // 绑定 Surface 以启用硬件加速
    
    // 3. 开始解码
    codec.start();
    
    // 4. 读取 H.264 码流（来自文件或流媒体）
    byte[] h264Data = getH264Data();
    
    // 5. 获取输入缓冲区并写入数据
    int inputBufferIndex = codec.dequeueInputBuffer(10000);
    if (inputBufferIndex >= 0) {
        ByteBuffer inputBuffer = codec.getInputBuffer(inputBufferIndex);
        inputBuffer.clear();
        inputBuffer.put(h264Data);
        codec.queueInputBuffer(inputBufferIndex, 0, h264Data.length, 0, 0);
    }
    
    // 6. 获取解码后的视频帧
    MediaCodec.BufferInfo bufferInfo = new MediaCodec.BufferInfo();
    int outputBufferIndex = codec.dequeueOutputBuffer(bufferInfo, 10000);
    if (outputBufferIndex >= 0) {
        codec.releaseOutputBuffer(outputBufferIndex, true); // 直接渲染到 Surface
    }
    
    ```
    
    ✅ **关键点**：
    
    - **绑定 `Surface`**，可以直接渲染到 `TextureView`，减少 CPU 负担。
    - **使用 `queueInputBuffer()` 提交数据**。
    - **使用 `releaseOutputBuffer()` 渲染**，而不是手动取 `ByteBuffer`。
    
    ---
    
    ## **三、硬件编码：使用 `MediaCodec` 进行 H.264 硬件编码**
    
    **目标**：使用 `MediaCodec` 进行 **YUV → H.264 硬件编码**，适用于 **视频录制、直播推流**。
    
    ### **编码流程**
    
    1. **创建 `MediaCodec` 编码器**
    2. **配置 `MediaFormat`**
    3. **喂入 `YUV` 数据**
    4. **获取编码后的 `H.264` 数据**
    5. **存储或推流**
    
    ### **代码示例**
    
    ```java
    java
    CopyEdit
    // 1. 创建 H.264 编码器
    MediaCodec codec = MediaCodec.createEncoderByType("video/avc");
    
    // 2. 配置编码参数
    MediaFormat format = MediaFormat.createVideoFormat("video/avc", width, height);
    format.setInteger(MediaFormat.KEY_BIT_RATE, 1000000);  // 码率 1Mbps
    format.setInteger(MediaFormat.KEY_FRAME_RATE, 30);     // 帧率 30fps
    format.setInteger(MediaFormat.KEY_COLOR_FORMAT, MediaCodecInfo.CodecCapabilities.COLOR_FormatYUV420Flexible);
    format.setInteger(MediaFormat.KEY_I_FRAME_INTERVAL, 1); // 每秒 1 个 I 帧
    
    codec.configure(format, null, null, MediaCodec.CONFIGURE_FLAG_ENCODE);
    codec.start();
    
    // 3. 获取输入缓冲区并写入 YUV 数据
    int inputBufferIndex = codec.dequeueInputBuffer(10000);
    if (inputBufferIndex >= 0) {
        ByteBuffer inputBuffer = codec.getInputBuffer(inputBufferIndex);
        inputBuffer.clear();
        inputBuffer.put(yuvData);  // YUV420 数据
        codec.queueInputBuffer(inputBufferIndex, 0, yuvData.length, System.nanoTime() / 1000, 0);
    }
    
    // 4. 获取 H.264 输出数据
    MediaCodec.BufferInfo bufferInfo = new MediaCodec.BufferInfo();
    int outputBufferIndex = codec.dequeueOutputBuffer(bufferInfo, 10000);
    if (outputBufferIndex >= 0) {
        ByteBuffer outputBuffer = codec.getOutputBuffer(outputBufferIndex);
        byte[] h264Data = new byte[bufferInfo.size];
        outputBuffer.get(h264Data);
        codec.releaseOutputBuffer(outputBufferIndex, false);
    
        // 5. 发送到 RTMP 推流、存储为 MP4
        sendToRtmpServer(h264Data);
    }
    
    ```
    
    ✅ **关键点**：
    
    - `COLOR_FormatYUV420Flexible` 适用于硬件编码。
    - **设置 `KEY_I_FRAME_INTERVAL`** 以控制关键帧（影响流媒体延迟）。
    - `queueInputBuffer()` 送入 **YUV 数据**，`dequeueOutputBuffer()` 取出 **H.264 码流**。
    
    ---
    
    ## **四、如何确认 `MediaCodec` 在使用硬件加速？**
    
    1. **检查编解码器名称**
        
        ```java
        java
        CopyEdit
        MediaCodec codec = MediaCodec.createDecoderByType("video/avc");
        Log.d("Codec", "使用的编解码器: " + codec.getName());
        
        ```
        
        - `OMX.google.h264.decoder` → **软件解码**
        - `OMX.qcom.video.decoder.avc` → **硬件解码**
    2. **测量 CPU 占用率**
        - 硬件解码的 CPU 负载 **显著低于** 软件解码。
    
    ---
    
    ## **总结**
    
    - **`MediaCodec` 默认会使用硬件编解码器**，只需绑定 `Surface` 即可零拷贝渲染。
    - **`MediaCodecList` 可列出支持的硬件编解码器**，确保选择正确的 `OMX` 设备。
    - **硬件编码适用于视频录制、直播**，配合 `MediaMuxer` 生成 MP4 或推流。
    - **使用 `Surface` 进行零拷贝，提高渲染效率，降低功耗**

### **5. 开源多媒体处理框架**

- FFmpeg
    
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
    
- x264
    
    x264是一个开源的H.264视频编码器，以其高效的编码性能和灵活的参数设置著称。x264能够在高压缩比和高视频质量之间找到良好的平衡，广泛应用于视频流媒体、视频编辑和内容发布中。它也是FFmpeg中的一个重要组件，负责处理H.264编码任务。
    

### 6. 客户端多媒体相关sdk

- Android Camera 2 API
    
    Camera 2是Android系统提供的高级相机API，支持手动控制相机的各项参数，如曝光时间、感光度、焦距等。它允许开发者创建高质量的相机应用，特别适用于需要精细控制拍摄效果的场景，如摄影应用、增强现实（AR）应用的开发等。相比旧版Camera API，Camera 2提供了更丰富的功能和更高的性能，但同时也更为复杂，需要开发者具备较高的技术水平。
    
- Android Camera X API
    
    CameraX 是 Android Jetpack 提供的一套用于摄像头开发的现代 API，封装了复杂的底层逻辑，提供了更一致、更高效的摄像头访问方式，并与生命周期紧密集成，简化了传统 Camera2 API
    
    [https://developer.android.com/codelabs/camerax-getting-started?hl=zh-cn#3](https://developer.android.com/codelabs/camerax-getting-started?hl=zh-cn#3)
    
    **Camera 2**
    
    在 camera 2 你需要手动管理下面的流程，更强的灵活性，但代码非常冗长
    
    **用 Camera2 更适合：**需要对相机硬件高度控制的场景（比如 AI 相机，视频会议系统），多路输出、并行处理、低延迟预览、帧率自定义等高级功能，专业级 camera app 或定制设备
    
    - CameraManager 用于获取设备
        
        ```cpp
        CameraManager manager = getSystemService(CameraManager.class);
        ```
        
    - CameraDevice 用于打开相机
        
        ```cpp
        CameraDevice device = manager.openCamera(...);
        ```
        
    - CaptureRequest 用于设置参数
        
        ```cpp
        CaptureRequest.Builder builder = device.createCaptureRequest(...);
        ```
        
    - CameraCaptureSession 用于创建拍摄会话
        
        ```cpp
        CameraCaptureSession session = device.createCaptureSession(...);
        session.setRepeatingRequest(builder.build(), ...);
        ```
        
    - Surface 用于管理图像输出
    
    **CameraX**
    
    在 CameraX 对相机的操作又做了进一步的封装
    
    用 CameraX 更适合：快速开发相机功能，普通拍照/录像/扫码，希望减少工作量和开发时间
    
    - ProcessCameraProvider 作为 CameraX 的管理入口，负责绑定生命周期和 UseCase
        
        ```cpp
        val cameraProviderFuture = ProcessCameraProvider.getInstance(context)
        // 这是异步的，需要添加监听器
        cameraProviderFuture.addListener({
            val cameraProvider = cameraProviderFuture.get()
            // 后续步骤在此进行
        }, ContextCompat.getMainExecutor(context))
        
        ```
        
    - CameraSelector 指定前/后摄像头
        
        ```cpp
        val cameraSelector = CameraSelector.DEFAULT_BACK_CAMERA
        ```
        
    - Preview 创建一个用于相机预览的 UseCase
        
        ```cpp
        val preview = Preview.Builder().build()
        preview.setSurfaceProvider(previewView.surfaceProvider)
        
        // 将 use case 绑定到生命周期
        cameraProvider.bindToLifecycle(this, CameraSelector.DEFAULT_BACK_CAMERA, preview)
        ```
        
    - ImageCapture 用于拍照
        
        ```cpp
        val imageCapture = ImageCapture.Builder()
            .setCaptureMode(ImageCapture.CAPTURE_MODE_MINIMIZE_LATENCY)
            .build()
        ```
        
    - ImageAnalysis 实时图像分析
        
        ```cpp
        val imageAnalyzer = ImageAnalysis.Builder()
            .setBackpressureStrategy(ImageAnalysis.STRATEGY_KEEP_ONLY_LATEST)
            .build()
        imageAnalyzer.setAnalyzer(executor, YourAnalyzer())
        ```
        
    - PreviewView UI 组件，用于展示 Preview
        
        ```cpp
        <androidx.camera.view.PreviewView
            android:id="@+id/previewView"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />
        ```
        
    
    **对比**
    
    | Camera2 | CameraX  | 说明 |
    | --- | --- | --- |
    | Surface | PreviewView / SurfaceProvider | Preview 通常显示在 PreviewView 上 |
    | CameraManager | ProcessCameraProvider | 负责查找和绑定相机设备 |
    | CameraDevice | 内部封装，无需直接操作 | CameraX 内部管理打开的相机 |
    | CaptureRequest | UseCase (如 Preview, ImageCapture) | 每个 UseCase 相当于一个封装好的请求配置 |
    | CameraCaptureSession | 自动管理，CameraX 内部创建 | UseCase 自动管理会话和 Surface |
    | ImageReader | ImageAnalysis | 实时获取帧用于图像处理，比如人脸识别 |
    | CameraCharacteristics | CameraInfo | 查询相机方向、分辨率、支持特性等信息 |
    
- Media3 ExoPlayer
    
    ExoPlayer 是 Google 官方开源的 Android 媒体播放器库，支持多种格式流媒体
    
    [https://developer.android.com/media/media3/exoplayer?hl=zh-cn](https://developer.android.com/media/media3/exoplayer?hl=zh-cn)
    
    1. 引入依赖
    
    ```groovy
    implementation 'androidx.media3:media3-exoplayer:1.3.1'
    implementation 'androidx.media3:media3-ui:1.3.1'
    ```
    
    2. 布局文件
    
    ```xml
    <com.google.android.exoplayer2.ui.PlayerViewandroid:id="@+id/player_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
    ```
    
    3. 初始化和播放
    
    ```kotlin
    val player = ExoPlayer.Builder(context).build()
    val playerView = findViewById<PlayerView>(R.id.player_view)
    playerView.player = player
    
    val mediaItem = MediaItem.fromUri("https://your.video.url/xxx.mp4")
    player.setMediaItem(mediaItem)
    player.prepare()
    player.play()
    
    player.setPlaybackSpeed(1.5f) // 快速播放
    player.repeatMode = Player.REPEAT_MODE_ONE // 单个视频循环
    ```
    
    4. 获取系统支持的解码器，ExoPlayer 不实现编解码，而是通过 `MediaCodec` 使用系统硬件解码器
    
    ```jsx
    import androidx.media3.exoplayer.mediacodec.MediaCodecUtil
    
    val h264Decoders = MediaCodecUtil.getDecoderInfos("video/avc", false) // H264
    val h265Decoders = MediaCodecUtil.getDecoderInfos("video/hevc", false) // H265
    
    h264Decoders.forEach {
        Log.d("DecoderInfo", "H264 Decoder: ${it.name}")
    }
    h265Decoders.forEach {
        Log.d("DecoderInfo", "H265 Decoder: ${it.name}")
    }
    ```
    
    5. 监听播放状态
    
    ```jsx
    player.addListener(object : Player.Listener {
        override fun onPlaybackStateChanged(state: Int) {
            when (state) {
                Player.STATE_BUFFERING -> Log.d("ExoPlayer", "Buffering")
                Player.STATE_READY -> Log.d("ExoPlayer", "Ready to play")
                Player.STATE_ENDED -> Log.d("ExoPlayer", "Playback ended")
                Player.STATE_IDLE -> Log.d("ExoPlayer", "Idle")
            }
        }
    
        override fun onPlayerError(error: PlaybackException) {
            Log.e("ExoPlayer", "Playback error: ${error.message}")
        }
    })
    ```
    
    6. 释放资源
    
    ```kotlin
    override fun onStop() {
        super.onStop()
        player.release()
    }
    ```
    
- ijkplayer
    
    ijkplayer 是 Bilibili 开源的基于 FFmpeg 封装的播放器，适合自定义解码器和更底层控制的场景
    
    1. 引入依赖（使用 JitPack）
    
    ```groovy
    implementation 'tv.danmaku.ijk.media:ijkplayer-java:0.8.8'
    implementation 'tv.danmaku.ijk.media:ijkplayer-armv7a:0.8.8' // 需根据架构选对应的 so
    ```
    
    2. 布局文件
    
    ```xml
    <tv.danmaku.ijk.media.widget.IjkVideoViewandroid:id="@+id/video_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
    ```
    
    3. 初始化和播放
    
    ```kotlin
    val videoView = findViewById<IjkVideoView>(R.id.video_view)
    IjkMediaPlayer.loadLibrariesOnce(null)
    IjkMediaPlayer.native_profileBegin("libijkplayer.so")
    
    videoView.setVideoURI(Uri.parse("https://your.video.url/xxx.mp4"))
    videoView.start(
    ```
    
    4. 释放资源
    
    ```kotlin
    override fun onStop() {
        super.onStop()
        videoView.stopPlayback()
    }
    ```
    
- Media Codec
    
    MediaCodec是Android系统提供的硬件加速视频编码和解码API，支持多种视频格式的编码和解码操作。使用MediaCodec，开发者可以高效地处理视频数据，如录制、播放、实时流媒体传输等。MediaCodec通过调用底层硬件解码器，提供了比软件解码更快、更省电的性能，特别适合需要处理大量视频数据的应用。
    
- OpenGL ES
    
    OpenGL ES是为嵌入式系统（如移动设备）设计的跨平台图形API，支持2D和3D图形渲染。它在移动游戏、增强现实、实时图形处理等领域广泛应用。OpenGL ES提供了对GPU的直接控制，使开发者能够创建高效、流畅的图形渲染效果。它适用于需要高性能图形处理的应用，如3D游戏、图形编辑工具等。
    
- GPU Image
    
    GPU Image是一个开源的iOS图像处理库，基于GPU加速，支持实时图像处理效果。开发者可以使用GPU Image轻松实现各种图像滤镜、特效，如模糊、锐化、色彩调整等。由于其利用了GPU的并行计算能力，GPU Image在处理复杂图像操作时比传统的CPU处理快得多，适合用于相机应用、照片编辑等需要高效图像处理的场景。
    
- iOS AVFoundation
    
    AVFoundation是iOS系统中的核心多媒体框架，提供了丰富的API用于音视频捕获、编辑、播放和导出。通过AVFoundation，开发者可以轻松实现视频录制、音频处理、图像合成等多媒体功能。它支持的功能包括音视频剪辑、滤镜应用、实时预览、格式转换等，非常适合用于开发复杂的多媒体应用。
    
- Metal
    
    Metal是Apple开发的底层图形和计算API，提供了对GPU的直接访问，支持高性能图形渲染和数据并行计算。相比OpenGL ES，Metal提供了更低的开销和更高的效率，使其适合开发需要复杂图形处理和计算的应用，如高质量3D游戏、AR应用、视频特效等。Metal的出现标志着Apple在图形和计算性能上的进一步提升，是iOS和macOS应用开发中的重要工具。
    

### 7. 客户端开发

- 概述
    
    ![image.png](image%206.png)
    
- Android Native
    
    Android原生开发主要使用Java或Kotlin编程语言，利用Android SDK提供的API进行应用开发。原生开发可以访问设备的硬件和系统功能，如相机、传感器、蓝牙、文件系统等，因此能够实现高性能、低延迟的应用。原生开发的优点是对平台功能的全面支持和优化，但缺点是无法跨平台复用代码。
    
- iOS Native
    
    iOS原生开发主要使用Objective-C或Swift编程语言，利用Apple的iOS SDK进行开发。原生开发可以直接访问iOS设备的系统API和硬件功能，如Touch ID、Face ID、相机等，因此能够提供优质的用户体验和高性能。与Android原生开发类似，iOS原生开发也无法跨平台使用代码。
    
- Xamarin
    
    Xamarin是一种跨平台开发工具，使用C#编程语言开发Android和iOS应用。它允许开发者在共享代码库的基础上，编写一次代码并部署到多个平台，从而减少开发时间和维护成本。Xamarin提供了对平台原生API的访问能力，因此可以在保持跨平台的同时，利用平台特有的功能
    

### 8. 音视频质量优化

- Jitter Buffer
    
    抖动缓冲器（Jitter Buffer）是用于缓解网络抖动对音视频流的影响的技术。它通过在接收端引入少量延迟，缓冲一定数量的数据包，从而平滑传输中的不规则抖动，确保音视频流的连续性和播放质量。Jitter Buffer在实时通信、视频会议等需要稳定流媒体传输的场景中非常重要。
    
- 首屏时间（First Frame Time）优化方案
- 音视频同步怎么实现
- SVC (Scalable Video Coding)
    
    可伸缩视频编码（SVC）是一种支持多层次视频传输的技术，使得视频流可以根据网络状况动态调整质量。SVC通过编码多个分辨率、帧率和质量层次，使得在网络条件不佳时可以仅传输基本层，而在条件良好时则传输更高质量的增强层。SVC广泛应用于视频会议、流媒体服务中，以适应不同的网络条件和设备能力。
    
- GCC (Google Congestion Control)
    
    Google开发的拥塞控制算法（GCC）是WebRTC中的一个关键技术，用于管理音视频流的网络传输。GCC通过动态调整视频码率，适应网络带宽的变化，确保视频流在拥塞情况下仍能保持较高的质量和流畅性。它通过实时监测网络状态，做出迅速的响应，使得音视频通信更加可靠和高效。
    
- FEC (Forward Error Correction)
    
    前向纠错（FEC）是一种通过传输冗余数据来提高音视频流抗丢包能力的技术。在传输过程中，如果出现数据包丢失，接收端可以利用冗余数据进行重建，而不必重新请求丢失的数据包。FEC特别适用于网络条件较差、丢包率较高的环境中，如卫星通信、直播流媒体等。
    
- Simulcast
    
    **Simulcast（多码流传输）是一种在不同网络条件下同时传输多路视频流的技术，每路视频流具有不同的分辨率**和码率。接收端可以根据自身的网络条件选择合适的码流进行播放，从而在保障视频质量的同时降低带宽需求。Simulcast广泛应用于视频会议和直播中，确保不同用户都能获得最佳的视频体验。
    
- 弱网对抗、带宽预测、拥塞控制、丢包对抗
    
    在网络条件较差的情况下，音视频流媒体需要通过自适应技术进行优化。弱网对抗涉及调整传输码率和抖动缓冲，以减轻网络波动的影响。带宽预测通过分析历史数据和实时网络状态，预测未来的网络带宽变化，以调整视频流的传输策略。拥塞控制（如GCC）通过动态调整传输速率，避免网络过载，从而保持流畅的视频播放。丢包对抗通过FEC和自动重传请求（ARQ）等技术，减少丢包对视频质量的影响。
    
- 码控、压缩率、性能优化
    
    在视频编码过程中，码率控制（码控）直接影响到视频质量和压缩效率。优化码控策略可以在保证视频质量的同时，最大限度地减少带宽和存储消耗。压缩率优化涉及在不显著影响视频质量的前提下，进一步减少视频文件的大小。性能优化包括提高编码器和解码器的运行效率，降低处理延迟，从而在低性能设备上也能实现流畅的视频处理。
    
- 视频花屏和卡顿分析
    
    **花屏和卡顿是视频播放中常见的问题，通常由编码器和解码器的参数设置不当或硬件资源不足引起。通过分析花屏和卡顿**的产生原因，可以调整视频流的编码参数（如比特率、关键帧间隔等）和渲染器的性能设置，以减少这些现象的发生。优化解码器的性能，使其能够更高效地处理视频数据，也有助于降低卡顿的发生频率