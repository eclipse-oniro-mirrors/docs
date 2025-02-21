# 拍照开发指导<a name="ZH-CN_TOPIC_0000001054915940"></a>

-   [使用场景](#zh-cn_topic_0000001052170554_section1963312376119)
-   [接口说明](#zh-cn_topic_0000001052170554_section56549532016)
-   [约束与限制](#zh-cn_topic_0000001052170554_section1165911177314)
-   [开发步骤](#zh-cn_topic_0000001052170554_section138543918214)

## 使用场景<a name="zh-cn_topic_0000001052170554_section1963312376119"></a>

使用Camera产生图片帧（拍照）。

## 接口说明<a name="zh-cn_topic_0000001052170554_section56549532016"></a>

**表 1**  API列表

<a name="zh-cn_topic_0000001052170554_table2069447114914"></a>
<table><thead align="left"><tr id="zh-cn_topic_0000001052170554_row4903852104914"><th class="cellrowborder" valign="top" width="14.93%" id="mcps1.2.4.1.1"><p id="zh-cn_topic_0000001052170554_p2903252174918"><a name="zh-cn_topic_0000001052170554_p2903252174918"></a><a name="zh-cn_topic_0000001052170554_p2903252174918"></a>类名</p>
</th>
<th class="cellrowborder" valign="top" width="61.660000000000004%" id="mcps1.2.4.1.2"><p id="zh-cn_topic_0000001052170554_p1595113912507"><a name="zh-cn_topic_0000001052170554_p1595113912507"></a><a name="zh-cn_topic_0000001052170554_p1595113912507"></a>接口名</p>
</th>
<th class="cellrowborder" valign="top" width="23.41%" id="mcps1.2.4.1.3"><p id="zh-cn_topic_0000001052170554_p15951597508"><a name="zh-cn_topic_0000001052170554_p15951597508"></a><a name="zh-cn_topic_0000001052170554_p15951597508"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0000001052170554_row492815717494"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p1592812716495"><a name="zh-cn_topic_0000001052170554_p1592812716495"></a><a name="zh-cn_topic_0000001052170554_p1592812716495"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p1492837144919"><a name="zh-cn_topic_0000001052170554_p1492837144919"></a><a name="zh-cn_topic_0000001052170554_p1492837144919"></a>int32_t GetCameraIds(std::list&lt;string&gt; cameraList)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p2092807134919"><a name="zh-cn_topic_0000001052170554_p2092807134919"></a><a name="zh-cn_topic_0000001052170554_p2092807134919"></a>获取cameraId列表</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row11928157114912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p139287774911"><a name="zh-cn_topic_0000001052170554_p139287774911"></a><a name="zh-cn_topic_0000001052170554_p139287774911"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p9928107174915"><a name="zh-cn_topic_0000001052170554_p9928107174915"></a><a name="zh-cn_topic_0000001052170554_p9928107174915"></a>CameraAbility&amp; GetCameraAbility(string cameraId)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p139281171494"><a name="zh-cn_topic_0000001052170554_p139281171494"></a><a name="zh-cn_topic_0000001052170554_p139281171494"></a>获取指定camera的能力</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row119282719496"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p159288734914"><a name="zh-cn_topic_0000001052170554_p159288734914"></a><a name="zh-cn_topic_0000001052170554_p159288734914"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p99280794913"><a name="zh-cn_topic_0000001052170554_p99280794913"></a><a name="zh-cn_topic_0000001052170554_p99280794913"></a>void RegisterCameraDeviceCallback(CameraDeviceCallback* callback, EventHandler* handler)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p8928197134910"><a name="zh-cn_topic_0000001052170554_p8928197134910"></a><a name="zh-cn_topic_0000001052170554_p8928197134910"></a>注册camera设备状态回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row4928673496"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p14928770497"><a name="zh-cn_topic_0000001052170554_p14928770497"></a><a name="zh-cn_topic_0000001052170554_p14928770497"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p14928197194915"><a name="zh-cn_topic_0000001052170554_p14928197194915"></a><a name="zh-cn_topic_0000001052170554_p14928197194915"></a>void UnregisterCameraDeviceCallback(CameraDeviceCallback* callback)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p17929197134913"><a name="zh-cn_topic_0000001052170554_p17929197134913"></a><a name="zh-cn_topic_0000001052170554_p17929197134913"></a>去注册camera设备状态回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row16929187104912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p6929157184911"><a name="zh-cn_topic_0000001052170554_p6929157184911"></a><a name="zh-cn_topic_0000001052170554_p6929157184911"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p1192910704914"><a name="zh-cn_topic_0000001052170554_p1192910704914"></a><a name="zh-cn_topic_0000001052170554_p1192910704914"></a>void CreateCamera(string cameraId, CameraStateCallback* callback, EventHandler* handler)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p12929167154912"><a name="zh-cn_topic_0000001052170554_p12929167154912"></a><a name="zh-cn_topic_0000001052170554_p12929167154912"></a>创建camera实例</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row592967184912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p9929127134915"><a name="zh-cn_topic_0000001052170554_p9929127134915"></a><a name="zh-cn_topic_0000001052170554_p9929127134915"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p0929107204913"><a name="zh-cn_topic_0000001052170554_p0929107204913"></a><a name="zh-cn_topic_0000001052170554_p0929107204913"></a>string GetCameraId()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p1592914710490"><a name="zh-cn_topic_0000001052170554_p1592914710490"></a><a name="zh-cn_topic_0000001052170554_p1592914710490"></a>获取cameraID</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row13929197104913"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p16929167134913"><a name="zh-cn_topic_0000001052170554_p16929167134913"></a><a name="zh-cn_topic_0000001052170554_p16929167134913"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p15929175491"><a name="zh-cn_topic_0000001052170554_p15929175491"></a><a name="zh-cn_topic_0000001052170554_p15929175491"></a>CameraConfig&amp; GetCameraConfig()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p19298714917"><a name="zh-cn_topic_0000001052170554_p19298714917"></a><a name="zh-cn_topic_0000001052170554_p19298714917"></a>获取camera配置信息</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row1892918764915"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p69291072495"><a name="zh-cn_topic_0000001052170554_p69291072495"></a><a name="zh-cn_topic_0000001052170554_p69291072495"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p5930172494"><a name="zh-cn_topic_0000001052170554_p5930172494"></a><a name="zh-cn_topic_0000001052170554_p5930172494"></a>FrameConfig&amp; GetFrameConfig(int32_t type)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p19301176495"><a name="zh-cn_topic_0000001052170554_p19301176495"></a><a name="zh-cn_topic_0000001052170554_p19301176495"></a>获取捕获帧类型</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row893019794915"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p893016714919"><a name="zh-cn_topic_0000001052170554_p893016714919"></a><a name="zh-cn_topic_0000001052170554_p893016714919"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p1093067134915"><a name="zh-cn_topic_0000001052170554_p1093067134915"></a><a name="zh-cn_topic_0000001052170554_p1093067134915"></a>void Configure(CameraConfig&amp; config)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p1493037114912"><a name="zh-cn_topic_0000001052170554_p1493037114912"></a><a name="zh-cn_topic_0000001052170554_p1493037114912"></a>配置camera</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row11930197174917"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p4930197184914"><a name="zh-cn_topic_0000001052170554_p4930197184914"></a><a name="zh-cn_topic_0000001052170554_p4930197184914"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p19304717492"><a name="zh-cn_topic_0000001052170554_p19304717492"></a><a name="zh-cn_topic_0000001052170554_p19304717492"></a>void Release()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p189301479494"><a name="zh-cn_topic_0000001052170554_p189301479494"></a><a name="zh-cn_topic_0000001052170554_p189301479494"></a>释放camera</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row109304717499"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p4930873496"><a name="zh-cn_topic_0000001052170554_p4930873496"></a><a name="zh-cn_topic_0000001052170554_p4930873496"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p1893017720490"><a name="zh-cn_topic_0000001052170554_p1893017720490"></a><a name="zh-cn_topic_0000001052170554_p1893017720490"></a>int TriggerLoopingCapture(FrameConfig&amp; frameConfig)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p149307754918"><a name="zh-cn_topic_0000001052170554_p149307754918"></a><a name="zh-cn_topic_0000001052170554_p149307754918"></a>开始循环帧捕获</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row19306794915"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p6930167194910"><a name="zh-cn_topic_0000001052170554_p6930167194910"></a><a name="zh-cn_topic_0000001052170554_p6930167194910"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p139311577499"><a name="zh-cn_topic_0000001052170554_p139311577499"></a><a name="zh-cn_topic_0000001052170554_p139311577499"></a>void StopLoopingCapture()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p693115764914"><a name="zh-cn_topic_0000001052170554_p693115764914"></a><a name="zh-cn_topic_0000001052170554_p693115764914"></a>停止循环帧捕获</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row593116713492"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p1193187174913"><a name="zh-cn_topic_0000001052170554_p1193187174913"></a><a name="zh-cn_topic_0000001052170554_p1193187174913"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p1493111713496"><a name="zh-cn_topic_0000001052170554_p1493111713496"></a><a name="zh-cn_topic_0000001052170554_p1493111713496"></a>int32_t TriggerSingleCapture(FrameConfig&amp; frameConfig)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p1193137104919"><a name="zh-cn_topic_0000001052170554_p1193137104919"></a><a name="zh-cn_topic_0000001052170554_p1193137104919"></a>抓图</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row1693112711491"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p89312716494"><a name="zh-cn_topic_0000001052170554_p89312716494"></a><a name="zh-cn_topic_0000001052170554_p89312716494"></a>CameraConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p199312784912"><a name="zh-cn_topic_0000001052170554_p199312784912"></a><a name="zh-cn_topic_0000001052170554_p199312784912"></a>void SetFrameStateCallback(FrameStateCallback* callback, EventHandler* handler);</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p49312714495"><a name="zh-cn_topic_0000001052170554_p49312714495"></a><a name="zh-cn_topic_0000001052170554_p49312714495"></a>设置帧状态回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row9931076492"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p59317784917"><a name="zh-cn_topic_0000001052170554_p59317784917"></a><a name="zh-cn_topic_0000001052170554_p59317784917"></a>CameraConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p17931197124912"><a name="zh-cn_topic_0000001052170554_p17931197124912"></a><a name="zh-cn_topic_0000001052170554_p17931197124912"></a>static CameraConfig* CreateCameraConfig()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p5931177164912"><a name="zh-cn_topic_0000001052170554_p5931177164912"></a><a name="zh-cn_topic_0000001052170554_p5931177164912"></a>创建camera配置信息实例</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row29321744917"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p1093219716492"><a name="zh-cn_topic_0000001052170554_p1093219716492"></a><a name="zh-cn_topic_0000001052170554_p1093219716492"></a>CameraAbility</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p12932979493"><a name="zh-cn_topic_0000001052170554_p12932979493"></a><a name="zh-cn_topic_0000001052170554_p12932979493"></a>std::list&lt;Size&gt; GetSupportedSizes(int format)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p1493210764918"><a name="zh-cn_topic_0000001052170554_p1493210764918"></a><a name="zh-cn_topic_0000001052170554_p1493210764918"></a>根据类型获取支持输出图像尺寸大小</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row1193267184910"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p1393214717492"><a name="zh-cn_topic_0000001052170554_p1393214717492"></a><a name="zh-cn_topic_0000001052170554_p1393214717492"></a>CameraAbility</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p119321477495"><a name="zh-cn_topic_0000001052170554_p119321477495"></a><a name="zh-cn_topic_0000001052170554_p119321477495"></a>std::list&lt;T&gt; GetParameterRange(uint32_t key)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p139331079491"><a name="zh-cn_topic_0000001052170554_p139331079491"></a><a name="zh-cn_topic_0000001052170554_p139331079491"></a>获取支持的参数范围</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row0933197134920"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p1493310764917"><a name="zh-cn_topic_0000001052170554_p1493310764917"></a><a name="zh-cn_topic_0000001052170554_p1493310764917"></a>CameraDevice</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p493313724915"><a name="zh-cn_topic_0000001052170554_p493313724915"></a><a name="zh-cn_topic_0000001052170554_p493313724915"></a>CameraDeviceCallback()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p993416724915"><a name="zh-cn_topic_0000001052170554_p993416724915"></a><a name="zh-cn_topic_0000001052170554_p993416724915"></a>camera设备回调类构造函数</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row093418712498"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p159341779492"><a name="zh-cn_topic_0000001052170554_p159341779492"></a><a name="zh-cn_topic_0000001052170554_p159341779492"></a>CameraDevice</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p1493411774912"><a name="zh-cn_topic_0000001052170554_p1493411774912"></a><a name="zh-cn_topic_0000001052170554_p1493411774912"></a>void OnCameraStatus​(std::string cameraId, int32_t status)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p1393419715491"><a name="zh-cn_topic_0000001052170554_p1393419715491"></a><a name="zh-cn_topic_0000001052170554_p1393419715491"></a>camera设备状态变化时的回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row109348711497"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p993419724914"><a name="zh-cn_topic_0000001052170554_p993419724914"></a><a name="zh-cn_topic_0000001052170554_p993419724914"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p993418720497"><a name="zh-cn_topic_0000001052170554_p993418720497"></a><a name="zh-cn_topic_0000001052170554_p993418720497"></a>CameraStateCallback​()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p693511794919"><a name="zh-cn_topic_0000001052170554_p693511794919"></a><a name="zh-cn_topic_0000001052170554_p693511794919"></a>camera状态回调类构造函数</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row159358717497"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p1992012253527"><a name="zh-cn_topic_0000001052170554_p1992012253527"></a><a name="zh-cn_topic_0000001052170554_p1992012253527"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p29351077497"><a name="zh-cn_topic_0000001052170554_p29351077497"></a><a name="zh-cn_topic_0000001052170554_p29351077497"></a>void OnConfigured​(Camera&amp; camera)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p093515774914"><a name="zh-cn_topic_0000001052170554_p093515774914"></a><a name="zh-cn_topic_0000001052170554_p093515774914"></a>camera配置成功回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row9935147184918"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p117291328135211"><a name="zh-cn_topic_0000001052170554_p117291328135211"></a><a name="zh-cn_topic_0000001052170554_p117291328135211"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p19935174496"><a name="zh-cn_topic_0000001052170554_p19935174496"></a><a name="zh-cn_topic_0000001052170554_p19935174496"></a>void OnConfigureFailed​(Camera&amp; camera,int32_t errorCode)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p159352077495"><a name="zh-cn_topic_0000001052170554_p159352077495"></a><a name="zh-cn_topic_0000001052170554_p159352077495"></a>camera配置失败回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row1935279498"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p1514619311525"><a name="zh-cn_topic_0000001052170554_p1514619311525"></a><a name="zh-cn_topic_0000001052170554_p1514619311525"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p493512744915"><a name="zh-cn_topic_0000001052170554_p493512744915"></a><a name="zh-cn_topic_0000001052170554_p493512744915"></a>void OnCreated​(Camera&amp; camera)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p1493511784914"><a name="zh-cn_topic_0000001052170554_p1493511784914"></a><a name="zh-cn_topic_0000001052170554_p1493511784914"></a>camera创建成功回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row189351877493"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p172071933175218"><a name="zh-cn_topic_0000001052170554_p172071933175218"></a><a name="zh-cn_topic_0000001052170554_p172071933175218"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p129361977498"><a name="zh-cn_topic_0000001052170554_p129361977498"></a><a name="zh-cn_topic_0000001052170554_p129361977498"></a>void OnCreateFailed​(std::string cameraId,int32_t errorCode)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p2936197114919"><a name="zh-cn_topic_0000001052170554_p2936197114919"></a><a name="zh-cn_topic_0000001052170554_p2936197114919"></a>camera创建失败回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row20936472491"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p61213391523"><a name="zh-cn_topic_0000001052170554_p61213391523"></a><a name="zh-cn_topic_0000001052170554_p61213391523"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p793697174919"><a name="zh-cn_topic_0000001052170554_p793697174919"></a><a name="zh-cn_topic_0000001052170554_p793697174919"></a>void OnReleased​(Camera&amp; camera)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p49361719495"><a name="zh-cn_topic_0000001052170554_p49361719495"></a><a name="zh-cn_topic_0000001052170554_p49361719495"></a>camera释放回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row159361179493"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p10936147194918"><a name="zh-cn_topic_0000001052170554_p10936147194918"></a><a name="zh-cn_topic_0000001052170554_p10936147194918"></a>FrameStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p9936279496"><a name="zh-cn_topic_0000001052170554_p9936279496"></a><a name="zh-cn_topic_0000001052170554_p9936279496"></a>FrameStateCallback​()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p49367718499"><a name="zh-cn_topic_0000001052170554_p49367718499"></a><a name="zh-cn_topic_0000001052170554_p49367718499"></a>帧状态回调类构造函数</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row1893617744916"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p136968511524"><a name="zh-cn_topic_0000001052170554_p136968511524"></a><a name="zh-cn_topic_0000001052170554_p136968511524"></a>FrameStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p209379744911"><a name="zh-cn_topic_0000001052170554_p209379744911"></a><a name="zh-cn_topic_0000001052170554_p209379744911"></a>void OnFrameFinished(Camera&amp; camera, FrameConfig&amp; frameConfig, FrameResult&amp; frameResult)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p19374724913"><a name="zh-cn_topic_0000001052170554_p19374724913"></a><a name="zh-cn_topic_0000001052170554_p19374724913"></a>拍照帧完成回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row093719718495"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p772975317527"><a name="zh-cn_topic_0000001052170554_p772975317527"></a><a name="zh-cn_topic_0000001052170554_p772975317527"></a>FrameStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p189371471498"><a name="zh-cn_topic_0000001052170554_p189371471498"></a><a name="zh-cn_topic_0000001052170554_p189371471498"></a>void OnFrameError​(Camera&amp; camera, FrameConfig&amp; frameConfig, int32_t errorCode, FrameResult&amp; frameResult)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p109371778497"><a name="zh-cn_topic_0000001052170554_p109371778497"></a><a name="zh-cn_topic_0000001052170554_p109371778497"></a>拍照帧异常回调</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row179381979499"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p169381975499"><a name="zh-cn_topic_0000001052170554_p169381975499"></a><a name="zh-cn_topic_0000001052170554_p169381975499"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p1793867124910"><a name="zh-cn_topic_0000001052170554_p1793867124910"></a><a name="zh-cn_topic_0000001052170554_p1793867124910"></a>int32_t GetFrameConfigType()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p1993817744915"><a name="zh-cn_topic_0000001052170554_p1993817744915"></a><a name="zh-cn_topic_0000001052170554_p1993817744915"></a>获取帧配置类型</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row793817784912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p69381724914"><a name="zh-cn_topic_0000001052170554_p69381724914"></a><a name="zh-cn_topic_0000001052170554_p69381724914"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p149382077496"><a name="zh-cn_topic_0000001052170554_p149382077496"></a><a name="zh-cn_topic_0000001052170554_p149382077496"></a>std::list&lt;OHOS::Surface&gt; GetSurfaces()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p893867114919"><a name="zh-cn_topic_0000001052170554_p893867114919"></a><a name="zh-cn_topic_0000001052170554_p893867114919"></a>获取帧配置的surface</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row109401570498"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p294019712492"><a name="zh-cn_topic_0000001052170554_p294019712492"></a><a name="zh-cn_topic_0000001052170554_p294019712492"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p19940170499"><a name="zh-cn_topic_0000001052170554_p19940170499"></a><a name="zh-cn_topic_0000001052170554_p19940170499"></a>void AddSurface(OHOS::AGP::UISurface&amp; surface);</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p11940197144915"><a name="zh-cn_topic_0000001052170554_p11940197144915"></a><a name="zh-cn_topic_0000001052170554_p11940197144915"></a>添加surface</p>
</td>
</tr>
<tr id="zh-cn_topic_0000001052170554_row994018711492"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0000001052170554_p1094016718493"><a name="zh-cn_topic_0000001052170554_p1094016718493"></a><a name="zh-cn_topic_0000001052170554_p1094016718493"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0000001052170554_p139411279498"><a name="zh-cn_topic_0000001052170554_p139411279498"></a><a name="zh-cn_topic_0000001052170554_p139411279498"></a>void RemoveSurface(OHOS::AGP::UISurface&amp; surface);</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="zh-cn_topic_0000001052170554_p39415717494"><a name="zh-cn_topic_0000001052170554_p39415717494"></a><a name="zh-cn_topic_0000001052170554_p39415717494"></a>删除surface</p>
</td>
</tr>
</tbody>
</table>

## 约束与限制<a name="zh-cn_topic_0000001052170554_section1165911177314"></a>

无。

## 开发步骤<a name="zh-cn_topic_0000001052170554_section138543918214"></a>

1.  <a name="zh-cn_topic_0000001052170554_li378084192111"></a>实现设备状态回调的派生类，用户在设备状态发生变更（如新插入相机设备/相机掉线）时，自定义操作。

    ```
    class SampleCameraDeviceCallback : public CameraDeviceCallback {
        void OnCameraStatus(std::string cameraId, int32_t status) override
        {
            //do something when camera is available/unavailable
        }
    };
    ```

2.  <a name="zh-cn_topic_0000001052170554_li8716104682913"></a>实现帧事件回调的派生类，这里在拿到帧数据以后将其转存为文件。

    ```
    static void SampleSaveCapture(const char *p, uint32_t size)
    {
        cout << "Start saving picture" << endl;
        struct timeval tv;
        gettimeofday(&tv, NULL);
        struct tm *ltm = localtime(&tv.tv_sec);
        if (ltm != nullptr) {
            ostringstream ss("Capture_");
            ss << "Capture" << ltm->tm_hour << "-" << ltm->tm_min << "-" << ltm->tm_sec << ".jpg";
    
            ofstream pic("/sdcard/" + ss.str(), ofstream::out | ofstream::trunc);
            cout << "write " << size << " bytes" << endl;
            pic.write(p, size);
            cout << "Saving picture end" << endl;
        }
    }
    
    class TestFrameStateCallback : public FrameStateCallback {
        void OnFrameFinished(Camera &camera, FrameConfig &fc, FrameResult &result) override
        {
            cout << "Receive frame complete inform." << endl;
            if (fc.GetFrameConfigType() == FRAME_CONFIG_CAPTURE) {
                cout << "Capture frame received." << endl;
                list<Surface *> surfaceList = fc.GetSurfaces();
                for (Surface *surface : surfaceList) {
                    SurfaceBuffer *buffer = surface->AcquireBuffer();
                    if (buffer != nullptr) {
                        char *virtAddr = static_cast<char *>(buffer->GetVirAddr());
                        if (virtAddr != nullptr) {
                            SampleSaveCapture(virtAddr, buffer->GetSize());
                        }
                        surface->ReleaseBuffer(buffer);
                    }
                    delete surface;
                }
                delete &fc;
            }
        }
    };
    ```

3.  <a name="zh-cn_topic_0000001052170554_li6671035102514"></a>实现相机状态回调的派生类，自定义相机状态发生变化（配置成功/失败，创建成功/失败\)时的操作。

    ```
    class SampleCameraStateMng : public CameraStateCallback {
    public:
        SampleCameraStateMng() = delete;
        SampleCameraStateMng(EventHandler &eventHdlr) : eventHdlr_(eventHdlr) {}
        ~SampleCameraStateMng()
        {
            if (recordFd_ != -1) {
                close(recordFd_);
            }
        }
        void OnCreated(Camera &c) override
        {
            cout << "Sample recv OnCreate camera." << endl;
            auto config = CameraConfig::CreateCameraConfig();
            config->SetFrameStateCallback(&fsCb_, &eventHdlr_);
            c.Configure(*config);
            cam_ = &c;
        }
        void OnCreateFailed(const std::string cameraId, int32_t errorCode) override {}
        void OnReleased(Camera &c) override {}
    };
    ```

4.  创建CameraKit，用于创建和获取camera信息。

    ```
    CameraKit *camKit = CameraKit::GetInstance();
    list<string> camList = camKit->GetCameraIds();
    string camId;
    for (auto &cam : camList) {
        cout << "camera name:" << cam << endl;
        const CameraAbility *ability = camKit->GetCameraAbility(cam);
        /* find camera which fits user's ability */
        list<CameraPicSize> sizeList = ability->GetSupportedSizes(0);
        if (find(sizeList.begin(), sizeList.end(), CAM_PIC_1080P) != sizeList.end()) {
            camId = cam;
            break;
        }
    }
    ```

5.  创建Camera实例。

    ```
    EventHandler eventHdlr; // Create a thread to handle callback events
    SampleCameraStateMng CamStateMng(eventHdlr);
    
    camKit->CreateCamera(camId, CamStateMng, eventHdlr);
    ```

6.  根据[步骤1](#zh-cn_topic_0000001052170554_li378084192111)、[步骤2](#zh-cn_topic_0000001052170554_li8716104682913)、[步骤3](#zh-cn_topic_0000001052170554_li6671035102514)中的回调设计，同步等待 OnCreated 回调拿到 cam\_ 之后，进行相关操作。

    ```
    void OnCreated(Camera &c) override
    {
        cout << "Sample recv OnCreate camera." << endl;
        auto config = CameraConfig::CreateCameraConfig();
        config->SetFrameStateCallback(&fsCb_, &eventHdlr_);
        c.Configure(*config);
        cam_ = &c;
    }
    
    void Capture()
    {
        if (cam_ == nullptr) {
            cout << "Camera is not ready." << endl;
            return;
        }
        FrameConfig *fc = new FrameConfig(FRAME_CONFIG_CAPTURE);
        Surface *surface = Surface::CreateSurface();
        if (surface == nullptr) {
            delete fc;
            return;
        }
        surface->SetWidthAndHeight(1920, 1080); /* 1920:width,1080:height */
        fc->AddSurface(*surface);
        cam_->TriggerSingleCapture(*fc);
    }
    ```


