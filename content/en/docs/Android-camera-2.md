
---
title: Android Camera 2
slug: Android-Camera-2
lastmod: 2025-07-01T00:00:00+00:00
---

# Android Camera 2

### Source code

[Camera.java - Android Code Search](https://cs.android.com/android/platform/superproject/main/+/main:frameworks/base/core/java/android/hardware/Camera.java;l=508?q=%22Fail%20to%20connect%20to%20camera%20service%22)

### Intro

- Introduce
    
    从 Android 5.0 开始，Google 引入了一套全新的相机框架 Camera2（android.hardware.camera2）并且废弃了旧的相机框架 Camera1（android.hardware.Camera）。基本原因是，camera1 接口过于简单，没法满足更加复杂的相机应用场景。为了给应用层提供更多的相机控制权限，从而构建出更高质量的相机应用程序，Google 才推出了 Camera2 接口
    
    看下和 Camera1 比较，Camera2 有哪些高级特性：
    
    - 在开启相机之前检查相机信息
    - 在不开启预览的情况下拍照
    - 一次拍摄多张不同格式和尺寸的图片
    - 控制曝光时间，灵活的 3A 控制
    - 以更快的间隔拍摄图像
    - 显示来自多个摄像机的预览
    - 直接应用效果和滤镜
    - 改进了新硬件的性能。Supported Hardware Level 的概念，不同厂商对 Camera2 的支持程度不同，从低到高有 LEGACY、LIMITED、FULL 和 LEVEL_3 四个级别
- Camera2 API class
    
    看下 Camera2 API 涉及到哪些类：
    
    ![Untitled](Untitled.png)
    
    ![Untitled](Untitled%201.png)
    
- Camera2 structure
    
    Android Camera 整体框架主要包括三个进程：app 进程、camera server 进程、HAL 进程（provider进程），进程之间的通信都是通过 binder 实现，其中 app 和 camera server 通信使用 AIDL (Android Interface Definition Language) ，camera server 和 hal（provider进程）通信使用 HIDL (HAL interface definition language) 。Android 上面的框架分级，基本都是类似的
    
    ![Untitled](Untitled%202.png)
    
- Pipeline
    
    Camera2 的 API 模型被设计成一个 Pipeline（管道），它按顺序处理每一帧的请求并返回请求结果给客户端。下面这张来自官方的图展示了 Pipeline 的工作流程
    
    ![Untitled](Untitled%203.png)
    
    Request的整体处理流程
    
    ![Untitled](Untitled%204.png)
    
    一个例子解释上面的第一张图的示意图，假设我们想要同时拍摄两张不同尺寸的图片，并且在拍摄的过程中闪光灯必须亮起来。整个拍摄流程如下：
    
    1. 创建一个用于从 Pipeline 获取图片的 CaptureRequest
    2. 修改 CaptureRequest 的闪光灯配置，让闪光灯在拍照过程中亮起来
    3. 创建两个不同尺寸的 Surface 用于接收图片数据，并且将它们添加到 CaptureRequest 中
    4. 发送配置好的 CaptureRequest 到 Pipeline 中等待它返回拍照结果
    5. 一个新的 CaptureRequest 会被放入一个被称作 Pending Request Queue 的队列中等待被执行，当 In-Flight Capture Queue 队列空闲的时候就会从 Pending Request Queue 获取若干个待处理的 CaptureRequest，并且根据每一个 CaptureRequest 的配置进行 Capture 操作
    6. 最后我们从不同尺寸的 Surface 中获取图片数据并且还会得到一个包含了很多与本次拍照相关的信息的 CaptureResult，流程结束
    
    Camera2开发流程：
    
    ![Untitled](Untitled%205.png)
    
- Supported Hardware Level
    
    相机功能的强大与否和硬件息息相关，不同厂商对 Camera2 的支持程度也不同，所以 Camera2 定义了一个叫做 Supported Hardware Level 的重要概念，其作用是将不同设备上的 Camera2 根据功能的支持情况划分成多个不同级别以便开发者能够大概了解当前设备上 Camera2 的支持情况：
    
    - **LEGACY**：向后兼容的级别，处于该级别的设备意味着它只支持 Camera1 的功能，不具备任何 Camera2 高级特性
    - **LIMITED**：除了支持 Camera1 的基础功能之外，还支持部分 Camera2 高级特性的级别
    - **FULL**：支持所有 Camera2 的高级特性
    - **LEVEL_3**：新增更多 Camera2 高级特性，例如 YUV 数据的后处理等

### API

- Capture
    
    Camera 的所有操作和参数配置最终都是服务于 capture，例如对焦是为了让某一个区域的图像更加清晰，调节曝光补偿是为了调节图像的亮度。因此，在 Camera2 里面所有的相机操作和参数配置都被抽象成 Capture，所以不要简单的把 Capture 直接理解成是拍照，因为 Capture 操作可能仅仅是为了让预览画面更清晰而进行对焦而已。如果你熟悉 Camera1，那你可能会问 setFlashMode在哪，setFocusMode()，takePicture() ，告诉你它们都是通过 Capture 来实现的
    
    Capture 从执行方式上又被细分为单次模式、多次模式和重复模式三种：
    
    - 单次模式（One-shot）：指的是只执行一次的 Capture 操作，例如设置闪光灯模式、对焦模式和拍一张照片等。多个一次性模式的 Capture 会进入队列按顺序执行
    - 多次模式（Burst）：指的是连续多次执行指定的 Capture 操作，该模式和多次执行单次模式的最大区别是连续多次 Capture 期间不允许插入其他任何 Capture 操作，例如连续拍摄 100 张照片，在拍摄这 100 张照片期间任何新的 Capture 请求都会排队等待，直到拍完 100 张照片。多组多次模式的 Capture 会进入队列按顺序执行
    - 重复模式（Repeating）：指的是不断重复执行指定的 Capture 操作，当有其他模式的 Capture 提交时会暂停该模式，转而执行其他被模式的 Capture，当其他模式的 Capture 执行完毕后又会自动恢复继续执行该模式的 Capture，例如显示预览画面就是不断 Capture 获取每一帧画面。该模式的 Capture 是全局唯一的，也就是新提交的重复模式 Capture 会覆盖旧的重复模式，Capture
- Surface
    
    Surface 是一块用于填充图像数据的内存空间，例如你可以使用 SurfaceView 的 Surface 接收每一帧预览数据用于显示预览画面，也可以使用 ImageReader 的 Surface 接收 JPEG 或 YUV 数据。每一个 Surface 都可以有自己的尺寸和数据格式，你可以从 CameraCharacteristics 获取某一个数据格式支持的尺寸列表
    
- CameraManager
    
    CameraManager 是一个用于检测相机，打开相机，以及获取相机设备特性的系统服务
    
    CameraManager 的关键功能
    
    1. 获取当前连接的相机设备列表和 camera id
        
        String[] getCameraIdList()
        
    2. 根据 camera id 获取对应相机设备的特征。返回一个 CameraCharacteristics，类比于旧 API 中的 Camera.Parameter 类，里面封装了相机设备固有的所有属性功能
        
        CameraCharacteristics getCameraCharacteristics(String cameraId)
        
    3. 根据 camera id 打开指定的相机设备，
        
        void openCamera(id, callback, handler)
        
    
    CameraManager 中包含两个公有的内部类
    
    1. **CameraManager.AvailabilityCallback**
        
        当一个相机设备的可用状态发生变化时，就会回调这个类 
        
        onCameraAvailable(String cameraId)
        
        onCameraUnavailable(String cameraId) 
        
    2. **CameraManager.TorchCallback**
        
        当一个相机设备的闪光灯的 Torch 模式可用状态发生变化时，就会回调这个类
        
        onTorchModeChanged(String cameraId, boolean enabled
        
        onTorchModeUnavailable(String cameraId) 
        
        setTorchMode(String cameraId, boolean enabled) 
        
    
    **举例：打开相机设备**
    
    ```java
    CameraManager cameraManager = (CameraManager) context.getSystemService(Context.CAMERA_SERVICE);
    String[] cameraIds = cameraManager.getCameraIdList();
    
    cameraManager.openCamera(cameraIds[0], new CameraDevice.StateCallback() {
        @Override
        public void onOpened(@NonNull CameraDevice camera) {
            // 当相机成功打开时回调该方法，接下来可以执行创建预览的操作
            mCameraOpenCloseLock.release();
            mCameraDevice = camera;
            createCameraPreviewSession();
        }
    
        @Override
        public void onDisconnected(@NonNull CameraDevice camera) {
            // 当相机断开连接时回调该方法，应该在此执行释放相机的操作
            mCameraOpenCloseLock.release();
            camera.close();
            mCameraDevice = null;
        }
    
        @Override
        public void onError(@NonNull CameraDevice camera, int error) {
            // 当相机打开失败时，应该在此执行释放相机的操作
            mCameraOpenCloseLock.release();
            camera.close();
            mCameraDevice = null;
        }
    
        @Override
        public void onClosed(@NonNull CameraDevice camera) {
            super.onClosed(camera);
        }
    }, null);
    ```
    
    CameraManager.openCamera 的三个参数：
    
    - cameraId：摄像头的唯一标识
    - callback：设备连接状态变化的回调，类型是 CameraDevice.StateCallback
    - handler：指定回调执行的线程，传 null 时默认使用当前线程的 Looper，我们通常创建一个后台线程来处理
    
    CameraDevice.StateCallback 的四个回调函数
    
    - onOpened：成功打开时的回调，此时 camera 准备就绪，得到一个 CameraDevice
    - onDisconnected：当相机断开连接时回调该方法，需要进行释放相机的操作
    - onError：当相机打开失败时，error 为具体错误原因，需要进行释放相机的操作
    - onClosed：调用 Camera.close()后的回调方法
    
- CameraDevice
    
    **介绍**：CameraDevice 代表当前连接的相机设备，用于创建 CameraCaptureSession。你可以看作为相机设备在 java 代码中的表现。熟悉 Camera1 的人可能会说 CameraDevice 就是 Camera1 的 Camera 类，实则不是，Camera 类几乎负责了所有相机的操作，而 CameraDevice 的功能则十分的单一，就是只负责建立相机连接的事务，而更加细化的相机操作则交给了 CameraCaptureSession
    
    **获取实例：**他是通过 CameraManager → openCamera 打开相机，在 CameraDevice.State Callback.onOpened(CameraDevice camera) 方法中获得 CameraDevice 的实例
    
    **内部类：**CameraDevice.StateCallback
    
    当相机状态发生变化时，会调用该类相应的回调方法
    
    - onOpened：成功打开时的回调，此时 camera 准备就绪，得到一个 CameraDevice
    - onDisconnected：当相机断开连接时回调该方法，需要进行释放相机的操作
    - onError：当相机打开失败时，error 为具体错误原因，需要进行释放相机的操作
        
        
        | Error Code | Description |
        | --- | --- |
        | CameraDevice.StateCallback.ERROR_CAMERA_IN_USE | 当前相机设备已经在一个更高优先级的地方打开了 |
        | CameraDevice.StateCallback.ERROR_MAX_CAMERAS_IN_USE | 已打开相机数量到上限了，无法再打开新的相机了 |
        | CameraDevice.StateCallback.ERROR_CAMERA_DISABLED | 由于相关设备策略该相机设备无法打开 |
        | CameraDevice.StateCallback.ERROR_CAMERA_DEVICE | 相机设备发生了一个致命错误 |
        | CameraDevice.StateCallback.ERROR_CAMERA_SERVICE | 相机设备发生了一个致命错误 |
    - onClosed：调用 Camera.close()后的回调方法
    
    **主要职责**：
    
    1. 关闭相机设备 
        
        void close()
        
    2. 获得当前相机设备的 camera id
        
        String getId()
        
    3. 使用内部类监听相机设备的状态，例如开启成功、开启失败、断开连接等
        
        CameraDevice.StateCallback
        
    4. 创建 CaptureRequest，根据指定的模板，并且 addTarget
        
        CaptureRequest.Builder createCaptureRequest(int templateType)
        
        addTarget(Surface)
        
    5. 创建 CameraCaptureSession，根据指定的 Surface output 列表
        
        void createCaptureSession(outputs, callback, handler)
        
    
    **CameraDevice.createCaptureRequest**
    
    使用指定模板创建一个 CaptureRequest.Builder 用于新的捕获请求构建。
    
    | templateType | 描述 | 适用性 |
    | --- | --- | --- |
    | **TEMPLATE_PREVIEW** | 用于创建一个相机预览请求。相机会优先保证高帧率而不是高画质 | 所有相机设备 |
    | TEMPLATE_STILL_CAPTURE | 用于创建一个拍照请求。相机会优先保证高画质而不是高帧率 | 所有相机设备 |
    | TEMPLATE_RECORD | 用于创建一个录像请求。相机会使用标准帧率，并设置录像级别的画质 | 所有相机设备 |
    | TEMPLATE_VIDEO_SNAPSHOT | 用于创建一个录像时拍照的请求。相机会尽可能的保证照片质量的同时不破坏正在录制的视频质量 | 硬件支持级别高于 LEGACY 的相机设备 |
    | TEMPLATE_ZERO_SHUTTER_LAG | 用于创建一个零延迟拍照的请求。相机会尽可能的保证照片质量的同时不损失预览图像的帧率，3A（自动曝光、自动聚焦、自动白平衡）都为 auto 模式 | 支持 PRIVATE_REPROCESSING 和 YUV_REPROCESSING 的相机设备 |
    | TEMPLATE_MANUAL | 用于创建一个手动控制相机参数的请求。相机所有自动控制将被禁用，后期处理参数为预览质量，手动控制参数被设置为合适的默认值，需要用户自己根据需求来调整各参数 | 支持 MANUAL_SENSOR 的相机设备 |
    
    **CameraDevice.createCaptureSession**
    
    先使用 CameraDevice.createCaptureRequest() 创建  Capture Request 对象，然后使用 CameraDevice.createCaptureSession() 创建 Capture Session，这个函数接受三个参数
    
    - outputs：用于接受图像数据的 surface 集合，每个 CaptureRequest 的输出 Surface 都应该是 outputs 的一个子元素
    - callback：创建 session 的回调函数，用于监听 Session 状态，类型是 CameraCaptureSession.StateCallback 对象
    - handler：指定回调执行的线程，用于执行 CameraCaptureSession. StateCallback 的 Handler 对象，传入 null 则使用当前的主线程 Handler，默认使用当前线程的 Looper
    
    **举例：使用 cameraDevice 创建 CaptureRequest 和 CaptureSession**  
    
    ```java
    private void startPreview() {
        **// prepare surface as target**
        SurfaceTexture texture = mTextureView.getSurfaceTexture();
        texture.setDefaultBufferSize(mPreviewSize.getWidth(), mPreviewSize.getHeight());
        Surface surface = new Surface(texture);
    
        try {
            **// create CaptureRequest**
            mPreviewRequestBuilder = mCameraDevice.createCaptureRequest(CameraDevice.TEMPLATE_PREVIEW);
            mPreviewRequestBuilder.addTarget(surface);
    
            **// create CameraCaptureSession for camera preview**
            mCameraDevice.createCaptureSession(
                Arrays.asList(surface, mImageReader.getSurface()),
                new CameraCaptureSession.StateCallback() {
                    @Override
                    public void onConfigured(@NonNull CameraCaptureSession cameraCaptureSession) {
                        mCaptureSession = cameraCaptureSession;
                    }
    
                    @Override
                    public void onConfigureFailed(CameraCaptureSession cameraCaptureSession);
                }, 
                null
             );
        } catch (CameraAccessException e) {
            e.printStackTrace();
        }
    }
    ```
    
- CameraCaptureSession
    
    **介绍：**是连接摄像头硬件和应用程序的桥梁，用于发送 capture 请求并接收相应的图像数据。绝大部分的相机操作都是通过向 CameraCaptureSession 提交一个 Capture 请求实现的，例如拍照、连拍、设置闪光灯模式、触摸对焦、显示预览画面等等
    
    CameraCaptureSession 实际上就是配置了目标 Surface 的相机实例，我们在使用相机功能之前必须先创建 CameraCaptureSession 实例。一个 CameraDevice 一次只能开启一个 CameraCaptureSession
    
    **获取实例**：通过 CameraDevice.createCaptureSession() 方法创建，并在回调的 onConfigured(CameraCaptureSession session) 方法中获取实例
    
    **内部类：**CameraCaptureSession.StateCallback
    
    当相机捕捉事务 CameraCaptureSession 他自己本身的状态发生变化时，会回调这个类中的相应方法。其中 onConfigured 和 onConfigureFailed 两个方法是抽象的（必须重写），其余均有空实现
    
    | 方法名 | 描述 |
    | --- | --- |
    | onConfigureFailed | 该会话无法按照相应的配置发起请求时回调 |
    | onConfigured | 相机设备完成配置，并开始处理捕捉请求时回调 |
    | onActive | 在 onConfigured 后执行，即开始真的处理捕捉请求了 |
    | onReady | 每当没有捕捉请求处理时都会回调该方法，即该方法会回调多次 |
    | onCaptureQueueEmpty | 当相机设备的输入捕捉队列为空时回调 |
    | onClosed | 当事务关闭时回调 |
    
    **内部类：**CameraCaptureSession.CaptureCallback
    
    当一个 capture 请求发送给相机设备时，可以使用这个类来跟踪各进度
    
    所有方法均有默认的空实现，根据需求重写相应的方法即可
    
    | 方法名 | 描述 |
    | --- | --- |
    | onCaptureStarted | 当相机设备开始为请求捕捉输出图时 |
    | onCaptureProgressed | 当图像捕获部分进行时就会回调该方法，此时一些(但不是全部)结果是可用的 |
    | onCaptureCompleted | 当图像捕捉完全完成时，并且结果已经可用时回调该方法 |
    | onCaptureFailed | 对应 onCaptureCompleted 方法，当相机设备产生 TotalCaptureResult 失败时就回调该方法 |
    | onCaptureSequenceCompleted | 当一个捕捉段完成时并且所有 CaptureResult 或者 captureFailure 都通过该监听器返回时被回调，这个方法独立于 CaptureCallback 的其他方法 |
    | onCaptureSequenceAborted | 当 CaptureResult 或者 captureFailure 没有通过该监听器被返回而被中断时被回调，这个方法同样独立于 CaptureCallback 的其他方法 |
    | onCaptureBufferLost | 当捕捉的缓冲没有被送到目标 surface 时被回调 |
    
    **主要职责**：
    
    1. 获取该 CameraCaptureSession 创建对应的 CameraDevice 对象
        
        CameraDevice getDevice()
        
    2. 请求 capture 单张图片，常用于拍照场景
        
        int capture(captureRequest, captureCallback, handler)
        
    3. 不断重复请求 capture 画面，常用于预览或者连拍场景
        
        int setRepeatingRequest(captureRequest, captureCallback, handler)
        
    4. 停止正常进行的所有的重复请求
        
        void stopRepeating()
        
    5. 取消当前队列中或正在处理中的所有请求
        
        void abortCaptures()
        
    6. 关闭 capture session，在相机释放的步骤中也要对 capture session 关闭操作
        
        void close() 异步
        
    
    使用举例：
    
    ```java
    /**
     * Creates a new {@link CameraCaptureSession} for camera preview.
     */
    private void createCameraPreviewSession() {
        try {
            SurfaceTexture texture = mTextureView.getSurfaceTexture();
            Surface surface = new Surface(texture);
            
            // create CaptureRequest
            mPreviewRequestBuilder = mCameraDevice.createCaptureRequest(CameraDevice.TEMPLATE_PREVIEW);
            mPreviewRequestBuilder.addTarget(surface);
            
            // createCameraCaptureSession for camera preview
            mCameraDevice.createCaptureSession(
                  Arrays.asList(surface, mImageReader.getSurface()),
                  new CameraCaptureSession.StateCallback() {
    
                      @Override
                      public void onConfigured(@NonNull CameraCaptureSession cameraCaptureSession) {
                          mCaptureSession = cameraCaptureSession;
                          mPreviewRequest = mPreviewRequestBuilder.build();
                          
                          // send capture request
                          mCaptureSession.setRepeatingRequest(
                                         mPreviewRequest,
                                         mCaptureCallback, 
                                         mBackgroundHandler);
                      }
                      @Override
                      public void onConfigureFailed(@NonNull CameraCaptureSession cameraCaptureSession);
                  }, 
                  null
            );
        } catch (CameraAccessException e) {
            e.printStackTrace();
        }
    }
    
    ```
    
- CameraCharacteristics
    
    CameraCharacteristics 是一个只读的相机信息提供者，其内部携带大量的相机信息，如果你对 Camera1 比较熟悉，那么 CameraCharacteristics 有点像 Camera1 的 Camera.CameraInfo 或者 Camera.Parameters，比如
    
    1. 代表相机朝向的 LENS_FACIN
    2. 判断闪光灯是否可用的 FLASH_INFO_AVAILABLE
    3. 获取所有可用 AE 模式的 CONTROL_AE_AVAILABLE_MODES 等等
- CaptureRequest
    
    CaptureRequest 是向 CameraCaptureSession 提交 Capture 请求时的信息载体，其内部包括了本次 Capture 的参数配置和接收图像数据的 Surface。CaptureRequest 可以配置的信息非常多，包括图像格式、图像分辨率、传感器控制、闪光灯控制、3A 控制等等，可以说绝大部分的相机参数都是通过 CaptureRequest 配置的
    
    值得注意的是每一个 CaptureRequest 表示一帧画面的操作，这意味着你可以精确控制每一帧的 Capture 操作
    
    **举例：创建 CaptureRequest**
    
    详细的创建代码在 CameraDevice 的使用说明里面，在 CameraDevice.StateCallback 的 onOpened 回调中执行
    
    ```java
    mPreviewRequestBuilder = mCameraDevice.createCaptureRequest(CameraDevice.TEMPLATE_PREVIEW);
    mPreviewRequestBuilder.addTarget(surface);
    ```
    
    onprev
    
    通过 CameraDevice.createCaptureRequest() 创建 CaptureRequest.Builder 对象，传入一个 templateType 参数，templateType 用于指定使用何种模板创建CaptureRequest.Builder 对象
    
    - Template_preview
    - TEMPLATE_PREVIEW：预览模式
    - TEMPLATE_STILL_CAPTURE：拍照模式
    - TEMPLATE_RECORD：视频录制模式
    - TEMPLATE_VIDEO_SNAPSHOT：视频截图模式
    - TEMPLATE_MANUAL：手动配置参数模式
    
    除了模式的配置，CaptureRequest还可以配置很多其他信息，例如图像格式、图像分辨率、传感器控制、闪光灯控制、3A(自动对焦-AF、自动曝光-AE和自动白平衡-AWB)控制等。在createCaptureSession 的回调中可以进行设置
    
    ```java
    // Auto focus should be continuous for camera preview.
    mPreviewRequestBuilder.set(CaptureRequest.CONTROL_AF_MODE,
            CaptureRequest.CONTROL_AF_MODE_CONTINUOUS_PICTURE);
    // Flash is automatically enabled when necessary.
    setAutoFlash(mPreviewRequestBuilder);
    
    // Finally, we start displaying the camera preview.
    mPreviewRequest = mPreviewRequestBuilder.build();
    
    // 代码中设置了AF为设置未图片模式下的连续对焦，并设置自动闪光灯
    // 最后通过build()方法生成CaptureRequest对象。
    ```
    
- CaptureResult
    
    CaptureResult 是每一次 Capture 操作的结果，里面包括了很多状态信息，包括闪光灯状态、对焦状态、时间戳等等。例如你可以在拍照完成的时候，通过 CaptureResult 获取本次拍照时的对焦状态和时间戳
    
    需要注意的是，CaptureResult 并不包含任何图像数据，前面我们在介绍 Surface 的时候说了，图像数据都是从 Surface 获取的
    

### Used in MSRTC

- android.content.Context
- android.graphics.Matrix
- android.graphics.Rect
- android.graphics.SurfaceTexture
- android.hardware.camera2.CameraAccessException
- android.hardware.camera2.CameraCaptureSession
- android.hardware.camera2.CameraDevice
- android.hardware.camera2.CaptureRequest
- android.hardware.camera2.CaptureResult
- android.hardware.camera2.TotalCaptureResult
- android.hardware.camera2.params.Face
- android.media.Image
- android.media.ImageReader
- android.os.Handler
- android.os.Looper
- android.util.Range
- android.view.Surface