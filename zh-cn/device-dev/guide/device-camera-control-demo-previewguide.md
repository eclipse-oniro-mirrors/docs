# 预览开发指导<a name="ZH-CN_TOPIC_0000001055394496"></a>

-   [使用场景](#zh-cn_topic_0000001051930577_section186634310418)
-   [接口说明](#zh-cn_topic_0000001051930577_section125479541744)
-   [约束与限制](#zh-cn_topic_0000001051930577_section1165911177314)
-   [开发步骤](#zh-cn_topic_0000001051930577_section34171333656)

## 使用场景<a name="zh-cn_topic_0000001051930577_section186634310418"></a>

使用camera产生视频流并播放。

## 接口说明<a name="zh-cn_topic_0000001051930577_section125479541744"></a>

参考“拍照开发指导”的“接口说明”。

## 约束与限制<a name="zh-cn_topic_0000001051930577_section1165911177314"></a>

无。

## 开发步骤<a name="zh-cn_topic_0000001051930577_section34171333656"></a>

1.  参考“拍照开发指导”中步骤1、步骤2、步骤3、步骤4。
2.  设置预览显示的区域。

    ```
    Surface *surface = Surface::CreateSurface();
    /* 设置显示区域 */
    surface->SetUserData("region_position_x", "480"); // 矩形左上角横坐标
    surface->SetUserData("region_position_y", "270"); // 矩形左上角纵坐标
    surface->SetUserData("region_width", "960"); // 宽
    surface->SetUserData("region_height", "540"); // 高
    
    fc->AddSurface(*surface);
    ```

3.  开始和结束预览。

    ```
    stateCallback->camera_->TriggerLoopingCapture(*fc); // start previewing
    stateCallback->camera_->StopLoopingCapture(); // stop previewing
    ```


