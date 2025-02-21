# 录像开发指导<a name="ZH-CN_TOPIC_0000001055234528"></a>

-   [使用场景](#zh-cn_topic_0000001051451869_section186634310418)
-   [接口说明](#zh-cn_topic_0000001051451869_section125479541744)
-   [约束与限制](#zh-cn_topic_0000001051451869_section1165911177314)
-   [开发步骤](#zh-cn_topic_0000001051451869_section1196016315516)

## 使用场景<a name="zh-cn_topic_0000001051451869_section186634310418"></a>

使用camera采集视频码流。

## 接口说明<a name="zh-cn_topic_0000001051451869_section125479541744"></a>

参考“拍照开发指导”的“接口说明”。

## 约束与限制<a name="zh-cn_topic_0000001051451869_section1165911177314"></a>

无。

## 开发步骤<a name="zh-cn_topic_0000001051451869_section1196016315516"></a>

1.  参考“拍照开发指导”中步骤1、步骤2、步骤3、步骤4。
2.  获取录像FrameConfig。

    ```
    /* 从recorder获取surface */
    Surface *surface = recorder_->GetSurface(0);
    surface->SetWidthAndHeight(1920, 1080);
    surface->SetQueueSize(3);
    surface->SetSize(1024 * 1024);
    /* 将surface配置到帧配置中 */
    FrameConfig *fc = new FrameConfig(FRAME_CONFIG_RECORD);
    fc->AddSurface(*surface);
    ```

3.  开启和停止录像。

    ```
    stateCallback->camera_->TriggerLoopingCapture(*fc); // 开始录像
    stateCallback->camera_->StopLoopingCapture(); // 结束录像
    ```


