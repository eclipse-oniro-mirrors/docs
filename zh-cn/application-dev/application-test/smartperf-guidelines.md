# SmartPerf Device性能工具使用指导

## 工具简介

SmartPerf Device是一款基于系统开发的性能功耗测试工具，操作简单易用。该工具可以监测性能、功耗相关指标，包括FPS、CPU、GPU、RAM、Temp等，通过量化的指标项了解应用、整机性能状况。

<!--Del-->在开发过程中，会使用到有屏或无屏设备，对此SmartPerf Device提供了两种方式：分别是Device-hap端和Device-daemon端。Device-hap端适用于有屏设备，支持可视化操作。测试时是通过悬浮窗的开始和暂停来实时展示性能指标数据，保存后可生成数据报告，在报告中可分析各指标数据详情。<!--DelEnd-->Device-daemon端支持shell命令行方式，同时适用于有屏和无屏设备。

### 指标说明

- CPU：每秒读取一次设备节点下CPU大中小核的频点和各核使用率，衡量应用占用CPU资源的情况，占用过多的CPU资源会导致芯片发烫。
- GPU：每秒读取一次设备节点下GPU的频点和负载信息，衡量应用占用GPU资源的情况，当GPU占用过多时，会导致性能下降，应用程序的运行速度变慢。
- FPS：应用界面每秒刷新次数，衡量应用画面的流畅度，FPS越高通常表示图像流畅度越好，用户体验也越好。
- TEMP：每秒读取一次设备节点下GPU温度、系统芯片温度信息。
- RAM：每秒读取一次应用进程的实际物理内存，衡量应用的内存占比情况。
- snapshot：每2秒截取一张应用界面截图。

## 实现原理

下图展示了SmartPerf Device工具的主要功能组成。Device-hap端设置好采集项和采集参数后，启动应用，FPS、RAM、Trace等指标通过消息发送给Device-daemon端，Device-daemon端进行数据采集、持久化和数据分析<!--Del-->，将生成的报告回传给Device-hap端，Device-hap端进行可视化显示<!--DelEnd-->。

![图片说明](figures/SmartPerfStru.png)

## 约束与限制

1. Device-daemon端<!--Del-->、Device-hap端<!--DelEnd-->在API 9版本开始预置使用。

2. Device-daemon端执行需连接硬件设备<!--Del-->，Device-hap端需在有屏幕设备使用<!--DelEnd-->。

3. Device-daemon端执行前需完成[hdc环境配置](https://gitee.com/openharmony/developtools_hdc)。

<!--Del-->

## SmartPerf Device-hap端

下面的操作步骤和界面内容以RK3568设备为例。

### 获取应用列表

点击设备上"SmartPerf Device-hap端"应用图标，进入"首页"，点击"请选择一个应用"，在应用列表页选择需要测试的应用。

![图片说明](figures/SmartPerfConfig1.png)
![图片说明](figures/SmartPerfConfig2.png)
![图片说明](figures/SmartPerfConfig3.png)

### 设置采集参数

应用选择完成后回到开始测试页面，根据实际业务需要，配置"测试指标"。同时，可修改测试名称（测试名称包含测试的应用名称和测试时间，会呈现在报告列表中），是否抓取trace，选择是否开启截图。配置完成后，点击底部"开始测试"按钮。

### 悬浮窗控制采集

点击悬浮窗"start"开始采集，点击悬浮窗"计时器"（如下图中00:07）暂停采集。再次点击"计时器"，继续开始采集。双击"计时器"，实时展示采集数据。长按"计时器"，结束采集。<br>整个过程中，可拖动悬浮框调整悬浮框位置。

![图片说明](figures/SmartPerfControl1.png)
![图片说明](figures/SmartPerfControl2.png)

### 查看报告

点击"报告"，查看测试报告列表。点击项目，进入报告详情页，查看测试指标项详情。

![图片说明](figures/SmartPerfReport1.png)
![图片说明](figures/SmartPerfReport2.png)
<!--DelEnd-->

<!--RP1-->
## SmartPerf Device-daemon端
<!--RP1End-->

### 采集前提

#### 进入shell

  ```
  C:\Users\issusser>hdc shell
  #
  ```

#### 拉起和查看daemon进程

  ```
  C:\Users\issusser>hdc shell
  // 拉起daemon进程
  # SP_daemon 
  // 查看daemon进程是否存在
  # ps -ef | grep SP_daemon
  root          1584     1 0 21:50:05 ?     00:00:00 SP_daemon
  root          1595  1574 3 21:51:02 pts/0 00:00:00 grep SP_daemon
  #
  ```

#### 执行和查看帮助命令

<!--RP3-->

  ```
  # SP_daemon --help
  OpenHarmony performance testing tool SmartPerf command-line version
   Usage: SP_daemon [options] [arguments]
    
   options:
    -N              set the collection times(default value is 0) range[1,2147483647], for example: -N 10
    -PKG            set package name, must add, for example: -PKG ohos.samples.ecg
    -c              get device CPU frequency and CPU usage, process CPU usage and CPU load ..
    -g              get device GPU frequency and GPU load
    -f              get app refresh fps(frames per second) and fps jitters and refreshrate
    -profilerfps    get refresh fps and timestamp
    -sections       set collection time period(using with profilerfps)
    -t              get remaining battery power and temperature..
    -p              get battery power consumption and voltage(Not supported by some devices)
    -r              get process memory and total memory
    -snapshot       get screen capture
    -net            get uplink and downlink traffic
    -start          collection start command
    -stop           collection stop command
    -VIEW           set layler, for example: -VIEW DisplayNode
    -OUT            set csv output path.
    -d              get device DDR information
    -screen         get screen resolution
    -deviceinfo     get device information
    -server         start a process to listen to the socket message of the start and stop commands
    -clear          clear the process ID
    -ohtestfps      used by the validator to obtain the fps, the collection times can be set
    -editorServer   start a process to listen to the socket message of the editor
    -recordcapacity get the battery level difference
    --version       get version
    --help          get help
    -editor         scenario-based collection identifier, parameter configuration items can be added later
    responseTime   get the page response delay after an application is operated
    completeTime   get the page completion delay after an application is operated
    fpsohtest      used by the validator to obtain the fps
    example1:
    SP_daemon -N 20 -c -g -t -p -r -net -snapshot -d
    SP_daemon -N 20 -PKG ohos.samples.ecg -c -g -t -p -f -r -net -snapshot -d
    SP_daemon -start -c
    SP_daemon -stop
    example2: These parameters need to be used separately
    SP_daemon -screen
    SP_daemon -deviceinfo
    SP_daemon -server
    SP_daemon -clear
    SP_daemon -ohtestfps 10
    SP_daemon -editorServer
    SP_daemon -recordcapacity
    example3: These parameters need to be used separately
    SP_daemon -editor responseTime ohos.samples.ecg app name
    SP_daemon -editor completeTime ohos.samples.ecg app name
    SP_daemon -editor fpsohtest
    
    
    
    command exec finished!
   #
  ```
<!--RP3End-->

### 基础采集

#### 通过-N开启采集

| 命令参数   |必选| 说明                   |
| :-----| :-----| :--------------------- |
| -N    |是| 设置采集次数，一秒采集一次。    |
| -PKG  |否| 设置包名。                |
| -c    |否| 采集cpu的频点和使用率。<br>设置应用包名时，采集整机和应用CPU信息。 <br>不设置应用包名时，采集整机CPU信息。     |
| -g    |否| 采集gpu的频点和负载信息。   |
| -f    |否| 采集指定应用的fps以及屏幕刷新率，必须设置应用包名。        |
| -t    |否| 采集GPU温度、系统芯片温度。           |
| -r    |否| 采集内存。<br>设置应用包名时，采集整机和应用内存信息。 <br>不设置应用包名时，采集整机内存信息。             |
| -snapshot |否| 屏幕截图。             |
| -net |否| 采集网络速率。              |
| -VIEW |否| 设置图层，需要先获取应用图层名。                |
| -d    |否| 采集DDR。                 |
| -sections|否| 设置分段采集。          |
<!--RP2--><!--RP2End-->

##### 使用示例

- 采集2次整机CPU大中小核频率、各核使用率

  ```
    # SP_daemon -N 2 -c

    order:0 timestamp=1501839064260
    order:1 TotalcpuUsage=0.502513
    order:2 TotalcpuidleUsage=99.497487
    order:3 TotalcpuioWaitUsage=0.000000
    order:4 TotalcpuirqUsage=0.000000
    order:5 TotalcpuniceUsage=0.000000
    order:6 TotalcpusoftIrqUsage=0.000000
    order:7 TotalcpusystemUsage=0.251256
    order:8 TotalcpuuserUsage=0.251256
    order:9 cpu0Frequency=1992000
    order:10 cpu0Usage=1.000000
    order:11 cpu0idleUsage=99.000000
    order:12 cpu0ioWaitUsage=0.000000
    order:13 cpu0irqUsage=0.000000
    order:14 cpu0niceUsage=0.000000
    order:15 cpu0softIrqUsage=0.000000
    order:16 cpu0systemUsage=0.000000
    order:17 cpu0userUsage=1.000000
    order:18 cpu1Frequency=1992000
    order:19 cpu1Usage=0.000000
    order:20 cpu1idleUsage=100.000000
    order:21 cpu1ioWaitUsage=0.000000
    order:22 cpu1irqUsage=0.000000
    order:23 cpu1niceUsage=0.000000
    order:24 cpu1softIrqUsage=0.000000
    order:25 cpu1systemUsage=0.000000
    order:26 cpu1userUsage=0.000000
    order:27 cpu2Frequency=1992000
    order:28 cpu2Usage=1.000000
    order:29 cpu2idleUsage=99.000000
    order:30 cpu2ioWaitUsage=0.000000
    order:31 cpu2irqUsage=0.000000
    order:32 cpu2niceUsage=0.000000
    order:33 cpu2softIrqUsage=0.000000
    order:34 cpu2systemUsage=1.000000
    order:35 cpu2userUsage=0.000000
    order:36 cpu3Frequency=1992000
    order:37 cpu3Usage=0.000000
    order:38 cpu3idleUsage=100.000000
    order:39 cpu3ioWaitUsage=0.000000
    order:40 cpu3irqUsage=0.000000
    order:41 cpu3niceUsage=0.000000
    order:42 cpu3softIrqUsage=0.000000
    order:43 cpu3systemUsage=0.000000
    order:44 cpu3userUsage=0.000000

    ...

    command exec finished!
    #
  ```

- 采集2次整机CPU大中小核频率、各核使用率以及进程CPU使用率、负载

  ```
    # SP_daemon -N 2 -PKG ohos.samples.ecg -c



    order:0 timestamp=1501839151499
    order:1 ProcAppName=ohos.samples.ecg
    order:2 ProcCpuLoad=0.000000
    order:3 ProcCpuUsage=36.177645
    order:4 ProcId=2111
    order:5 ProcSCpuUsage=8.982036
    order:6 ProcUCpuUsage=27.195609
    order:7 TotalcpuUsage=62.500000
    order:8 TotalcpuidleUsage=37.500000
    order:9 TotalcpuioWaitUsage=0.000000
    order:10 TotalcpuirqUsage=0.000000
    order:11 TotalcpuniceUsage=0.000000
    order:12 TotalcpusoftIrqUsage=0.000000
    order:13 TotalcpusystemUsage=21.614583
    order:14 TotalcpuuserUsage=40.885417
    order:15 cpu0Frequency=1992000
    order:16 cpu0Usage=77.083333
    order:17 cpu0idleUsage=22.916667
    order:18 cpu0ioWaitUsage=0.000000
    order:19 cpu0irqUsage=0.000000
    order:20 cpu0niceUsage=0.000000
    order:21 cpu0softIrqUsage=0.000000
    order:22 cpu0systemUsage=21.875000
    order:23 cpu0userUsage=55.208333
    order:24 cpu1Frequency=1992000
    order:25 cpu1Usage=57.731959
    order:26 cpu1idleUsage=42.268041
    order:27 cpu1ioWaitUsage=0.000000
    order:28 cpu1irqUsage=0.000000
    order:29 cpu1niceUsage=0.000000
    order:30 cpu1softIrqUsage=0.000000
    order:31 cpu1systemUsage=21.649485
    order:32 cpu1userUsage=36.082474
    order:33 cpu2Frequency=1992000
    order:34 cpu2Usage=59.793814
    order:35 cpu2idleUsage=40.206186
    order:36 cpu2ioWaitUsage=0.000000
    order:37 cpu2irqUsage=0.000000
    order:38 cpu2niceUsage=0.000000
    order:39 cpu2softIrqUsage=0.000000
    order:40 cpu2systemUsage=19.587629
    order:41 cpu2userUsage=40.206186
    order:42 cpu3Frequency=1992000
    order:43 cpu3Usage=55.789474
    order:44 cpu3idleUsage=44.210526
    order:45 cpu3ioWaitUsage=0.000000
    order:46 cpu3irqUsage=0.000000
    order:47 cpu3niceUsage=0.000000
    order:48 cpu3softIrqUsage=0.000000
    order:49 cpu3systemUsage=23.157895
    order:50 cpu3userUsage=32.631579

    ...

    command exec finished!
    #
  ```

  >**说明**
  >
  >- 使用该命令采集时需进入被测应用内。

- 采集1次整机GPU频率和负载
 
  ```
    # SP_daemon -N 1 -g
    
    
    
    order:0 timestamp=1503078740268
    order:1 gpuFrequency=200000000
    order:2 gpuLoad=38.000000
    
    command exec finished!
    #
  ```

- 采集2次整机温度

  ```
    # SP_daemon -N 2 -t

    order:0 timestamp=1502720711191
    order:1 gpu-thermal=42500.000000
    order:2 soc-thermal=43.125000
    
    
    order:0 timestamp=1502720712191
    order:1 gpu-thermal=41875.000000
    order:2 soc-thermal=42.500000

    command exec finished!
    #
  ```

- 采集2次整机内存

  ```
    # SP_daemon -N 2 -r
    order:0 timestamp=1705041562521
    order:1 memAvailable=7339224
    order:2 memFree=7164708
    order:3 memTotal=11641840

    order:0 timestamp=1705041563527
    order:1 memAvailable=7339136
    order:2 memFree=7164684
    order:3 memTotal=11641840

    command exec finished!
    #
  ```

- 采集1次整机和指定应用进程内存

  ```
    # SP_daemon -N 1 -PKG ohos.samples.ecg -r

    order:0 timestamp=1720427095197
    order:1 arktsHeapPss=17555
    order:2 gpuPss=7021
    order:3 graphicPss=163320
    order:4 heapAlloc=120344
    order:5 heapFree=14362
    order:6 heapSize=133436
    order:7 memAvailable=2757504
    order:8 memFree=190852
    order:9 memTotal=11742716
    order:10 nativeHeapPss=49102
    order:11 privateClean=1100020
    order:12 privateDirty=175169
    order:13 pss=422172
    order:14 sharedClean=89348
    order:15 sharedDirty=19084
    order:16 stackPss=1588
    order:17 swap=122076
    order:18 swapPss=122076


    command exec finished!
    #
  ```
  >**说明**
  >
  >- 使用该命令采集时需进入被测应用内。
  >- 该命令集成了历史版本-m的数据（arktsHeapPss、gpuPss、graphicPss...）。

- 采集2次截图

  ```
    # SP_daemon -N 2 -snapshot

    order:0 timestamp=1501837609657
    order:1 capture=data/local/tmp/capture/screenCap_1501837609657.png
    
    
    order:0 timestamp=1501837610657
    order:1 capture=NA

    command exec finished!
    #
  ```
  >**说明**
  >
  >- 截图采集是2秒截取一次。
  >
  >- 截图报告存放路径为：data/local/tmp/capture。
  >
  >- 采集结束后：进入 data/local/tmp/capture 查看生成的截图。
  >
  >- 导出截图到D盘：重启一个命令行工具执行命令： hdc file recv data/local/tmp/capture/screenCap_1700725192774.png D:\。

- 采集2次网络速率

  ```
    # SP_daemon -N 2 -net

    order:0 timestamp=1705041904832
    order:1 networkDown=0
    order:2 networkUp=0

    order:0 timestamp=1705041905870
    order:1 networkDown=22931
    order:2 networkUp=2004

    command exec finished!
    #
  ```

- 采集5次指定应用帧率

  ```
    # SP_daemon -N 5 -PKG ohos.samples.ecg -f

    order:0 timestamp=1705306472232
    order:1 fps=43
    order:2 fpsJitters=602261688;;8352083;;8267708;;8305209;;8298437;;8308854;;8313542;;8569271;;8061458;;8300521;;8308333;;8309896;;8429167;;8241667;;8258333;;8318229;;8312500;;8304167;;41760937;;16418750;;8298959;;8319270;;8308334;;8313541;;8302605;;8320312;;8298958;;8326042;;8321354;;8301042;;8310417;;8309895;;8308855;;8331250;;8286458;;8343229;;8278125;;8311458;;8306250;;8312500;;8320834;;8346875;;8283333
    order:3 refreshrate=69

    order:0 timestamp=1705306473234
    order:1 fps=40
    order:2 fpsJitters=674427313;;8191145;;8310417;;8319271;;8301562;;8318750;;8302084;;8314062;;8333334;;8283854;;8307812;;8311979;;8310417;;8307813;;8309375;;8323958;;8306250;;8308333;;8317709;;8296875;;8721875;;7895833;;8320833;;8340625;;8276563;;8409896;;8216145;;8310938;;8301042;;8362500;;8252604;;8317708;;8376042;;8256250;;8292187;;8303125;;8313542;;8310417;;8520312
    order:3 refreshrate=69
    ...

    command exec finished!
    #
  ```
  >**说明**
  >
  >- 使用该命令采集时需进入被测应用内，滑动或切换页面。
  >- 在智能刷新率情况下，刷新率是实时变化的（一秒内可能存在多次变化），refreshrate取值是采集时刻（timestamp）的刷新率。

 
- 采集10次指定图层帧率

  ```
    # SP_daemon -N 10 -VIEW DisplayNode -f
    order:0 timestamp=1705306822850
    order:1 fps=15
    order:2 fpsJitters=876291843;;8314062;;8308334;;8314583;;8310417;;8308333;;8326042;;8314583;;8292708;;8492709;;8143750;;8340104;;8294271;;8302604;;8297396
    order:3 refreshrate=69
 
    order:0 timestamp=1705306823852
    order:1 fps=12
    order:2 fpsJitters=906667363;;8279167;;8311458;;8315625;;8291146;;8313021;;8323438;;8293750;;8303125;;8313541;;8301563;;8317708
    order:3 refreshrate=69
    ...

    command exec finished!
    #
  ```
  >**说明**
  >
  >- DisplayNode 是指定的图层名。
  >
  >- 使用该命令采集时，需在传入的图层上操作页面。
  >
  >- 该命令不能与指定应用帧率一起采集（SP_daemon -N 20 -PKG ohos.samples.ecg -f 或 SP_daemon -N 20 -VIEW DisplayNode -f）。

- 采集1次DDR信息

  ```
    # SP_daemon -N 1 -d
    
    order:0 timestamp=1710916175201
    order:1 ddrFrequency=1531000000
    
    command exec finished!
    #
  ```
<!--RP4--><!--RP4End-->

- 全量采集示例1，采集整机信息，包括cpu、gpu、温度、内存信息、DDR信息、网络速率、屏幕截图
 
  ```
    # SP_daemon -N 10 -c -g -t -r -d -net -snapshot

    order:0 timestamp=1501837838664
    order:1 TotalcpuUsage=0.751880
    order:2 TotalcpuidleUsage=99.248120
    order:3 TotalcpuioWaitUsage=0.000000
    order:4 TotalcpuirqUsage=0.000000
    order:5 TotalcpuniceUsage=0.000000
    order:6 TotalcpusoftIrqUsage=0.000000
    order:7 TotalcpusystemUsage=0.501253
    order:8 TotalcpuuserUsage=0.250627
    order:9 cpu0Frequency=1992000
    order:10 cpu0Usage=0.000000
    order:11 cpu0idleUsage=100.000000
    order:12 cpu0ioWaitUsage=0.000000
    order:13 cpu0irqUsage=0.000000
    order:14 cpu0niceUsage=0.000000
    order:15 cpu0softIrqUsage=0.000000
    order:16 cpu0systemUsage=0.000000
    order:17 cpu0userUsage=0.000000
    order:18 cpu1Frequency=1992000
    order:19 cpu1Usage=0.000000
    order:20 cpu1idleUsage=100.000000
    order:21 cpu1ioWaitUsage=0.000000
    order:22 cpu1irqUsage=0.000000
    order:23 cpu1niceUsage=0.000000
    order:24 cpu1softIrqUsage=0.000000
    order:25 cpu1systemUsage=0.000000
    order:26 cpu1userUsage=0.000000
    order:27 cpu2Frequency=1992000
    order:28 cpu2Usage=1.000000
    order:29 cpu2idleUsage=99.000000
    order:30 cpu2ioWaitUsage=0.000000
    order:31 cpu2irqUsage=0.000000
    order:32 cpu2niceUsage=0.000000
    order:33 cpu2softIrqUsage=0.000000
    order:34 cpu2systemUsage=1.000000
    order:35 cpu2userUsage=0.000000
    order:36 cpu3Frequency=1992000
    order:37 cpu3Usage=0.000000
    order:38 cpu3idleUsage=100.000000
    order:39 cpu3ioWaitUsage=0.000000
    order:40 cpu3irqUsage=0.000000
    order:41 cpu3niceUsage=0.000000
    order:42 cpu3softIrqUsage=0.000000
    order:43 cpu3systemUsage=0.000000
    order:44 cpu3userUsage=0.000000
    order:45 gpuFrequency=200000000
    order:46 gpuLoad=0.000000
    order:47 gpu-thermal=40000.000000
    order:48 soc-thermal=40.625000
    order:49 memAvailable=1142820
    order:50 memFree=687988
    order:51 memTotal=1935948
    order:52 ddrFrequency=800000000
    order:53 networkDown=0
    order:54 networkUp=0
    order:55 capture=data/local/tmp/capture/screenCap_1501837838669.png

    ...

    command exec finished!
    #
  ```

- 全量采集示例2，采集指定应用信息，包括cpu、gpu、温度、fps、内存信息、DDR信息、网络速率、屏幕截图
 
  <!--RP5-->
  ```
    # SP_daemon -N 10 -PKG ohos.samples.ecg -c -g -t -f -r -d -net -snapshot

    order:0 timestamp=1501837949706
    order:1 ProcAppName=ohos.samples.ecg
    order:2 ProcCpuLoad=0.000000
    order:3 ProcCpuUsage=38.775000
    order:4 ProcId=1960
    order:5 ProcSCpuUsage=8.875000
    order:6 ProcUCpuUsage=29.900000
    order:7 TotalcpuUsage=85.416667
    order:8 TotalcpuidleUsage=14.583333
    order:9 TotalcpuioWaitUsage=0.000000
    order:10 TotalcpuirqUsage=0.000000
    order:11 TotalcpuniceUsage=0.000000
    order:12 TotalcpusoftIrqUsage=0.000000
    order:13 TotalcpusystemUsage=33.072917
    order:14 TotalcpuuserUsage=52.343750
    order:15 cpu0Frequency=1992000
    order:16 cpu0Usage=92.929293
    order:17 cpu0idleUsage=7.070707
    order:18 cpu0ioWaitUsage=0.000000
    order:19 cpu0irqUsage=0.000000
    order:20 cpu0niceUsage=0.000000
    order:21 cpu0softIrqUsage=0.000000
    order:22 cpu0systemUsage=40.404040
    order:23 cpu0userUsage=52.525253
    order:24 cpu1Frequency=1992000
    order:25 cpu1Usage=82.291667
    order:26 cpu1idleUsage=17.708333
    order:27 cpu1ioWaitUsage=0.000000
    order:28 cpu1irqUsage=0.000000
    order:29 cpu1niceUsage=0.000000
    order:30 cpu1softIrqUsage=0.000000
    order:31 cpu1systemUsage=29.166667
    order:32 cpu1userUsage=53.125000
    order:33 cpu2Frequency=1992000
    order:34 cpu2Usage=81.111111
    order:35 cpu2idleUsage=18.888889
    order:36 cpu2ioWaitUsage=0.000000
    order:37 cpu2irqUsage=0.000000
    order:38 cpu2niceUsage=0.000000
    order:39 cpu2softIrqUsage=0.000000
    order:40 cpu2systemUsage=31.111111
    order:41 cpu2userUsage=50.000000
    order:42 cpu3Frequency=1992000
    order:43 cpu3Usage=85.858586
    order:44 cpu3idleUsage=14.141414
    order:45 cpu3ioWaitUsage=0.000000
    order:46 cpu3irqUsage=0.000000
    order:47 cpu3niceUsage=0.000000
    order:48 cpu3softIrqUsage=0.000000
    order:49 cpu3systemUsage=32.323232
    order:50 cpu3userUsage=53.535354
    order:51 gpuFrequency=200000000
    order:52 gpuLoad=29.000000
    order:53 gpu-thermal=41875.000000
    order:54 soc-thermal=45.000000
    order:55 fps=40
    order:56 fpsJitters=14482127;;28966003;;28971836;;14484751;;28952878;;28970962;;14480959;;28968337;;14476001;;28967461;;28968045;;14477751;;28966878;;28975337;;14475126;;28962795;;28967461;;14496710;;28953169;;28966003;;14483002;;28963961;;28965711;;28964836;;28966295;;14550085;;28898628;;28964544;;28975628;;14497293;;28938878;;43454546;;28966003;;28973295;;28959878;;28964252;;14476585;;28965128;;28970670;;14478626
    order:57 refreshrate=69
    order:58 arktsHeapPss=10970
    order:59 gpuPss=0
    order:60 graphicPss=10800
    order:61 heapAlloc=0
    order:62 heapFree=0
    order:63 heapSize=0
    order:64 memAvailable=1137784
    order:65 memFree=682592
    order:66 memTotal=1935948
    order:67 nativeHeapPss=21398
    order:68 privateClean=24816
    order:69 privateDirty=44932
    order:70 pss=91587
    order:71 sharedClean=100512
    order:72 sharedDirty=36832
    order:73 stackPss=1444
    order:74 swap=0
    order:75 swapPss=0
    order:76 ddrFrequency=800000000
    order:77 networkDown=0
    order:78 networkUp=0
    order:79 capture=data/local/tmp/capture/screenCap_1501837950216.png

    ...

    command exec finished!
    #
  ```
  <!--RP5End-->

  >**说明**
  >
  >- 使用该命令采集时需进入被测应用内。


#### 通过-start开启采集

先执行start开始采集命令，然后操作设备或应用，最后执行stop结束采集命令。

| 命令参数   |必选| 说明                   |
| :-----|:-----| :--------------------- |
| -start |是| 开始采集，该命令参数后可添加基础采集命令，一秒采集一次。            |
| -stop |是| 结束采集，执行后会生成采集报告。              |

##### 使用示例
  
   ```
   开始采集
   # SP_daemon -start -c
   SP_daemon Collection begins
    
    
   command exec finished!
   #
      
   结束采集
   # SP_daemon -stop
   SP_daemon Collection ended
   Output Path: data/local/tmp/smartperf/1/t_index_info.csv
    
    
   command exec finished!
   #
   ```
   >**说明**
   >
   >- 开始采集示例1（采整机）：SP_daemon -start -c -g -t -r -d -net -snapshot。
   >
   >- 开始采集示例2（采整机和进程）：SP_daemon -start -PKG ohos.samples.ecg -c -g -t -f -r -d -net -snapshot。
   >
   >- 启停服务文件输出路径为：data/local/tmp/smartperf/1/t_index_info.csv，可通过hdc file recv的方式导出查看报告。具体请参考[查看csv采集结果](#查看csv采集结果)。

#### 查看csv采集结果

若采集结果保存在csv文件中，可以按照如下操作导出和查看结果内容。

  - 采集结果默认输出路径：/data/local/tmp/data.csv

  - 查看文件位置

    ```
    C:\Users\issusser>hdc shell
    # cd data/local/tmp
    # ls
    data.csv
    #
    ```

  - 导出文件
    ```
    C:\Users\issusser>hdc file recv data/local/tmp/data.csv D:\
    [I][2023-11-08 16:16:41] HdcFile::TransferSummary success
    FileTransfer finish, Size:429, File count = 1, time:6ms rate:71.50kB/s

    C:\Users\issusser>
    ```

  - 打开data.csv查看采集数据

    在自定义导出路径里找到data.csv文件打开查看采集数据表，data.csv数据名描述如下：

    | 数据项    | 说明             |备注|
    | :-----| :--------------------- |:-----|
    | cpuFrequency      | CPU大中小核频率。        |单位：Hz|
    | cpuUasge          | CPU各核使用率。          |%|
    | cpuidleUsage      | CPU空闲态使用率。        |%| 
    | cpuioWaitUsage    | 等待I/O的使用率。        |%|
    | cpuirqUsage       | 硬中断的使用率。         |%|  
    | cpuniceUsage      | 低优先级用户态使用率。    |%|
    | cpusoftIrqUsage   | 软中断的使用率。         |%| 
    | cpusystemUsage    | 系统/内核态使用率。      |%|
    | cpuuserUsage      | 用户态使用率。           |%| 
    | ProcId            | 进程id。                |-|
    | ProcAppName       | app包名。                |-| 
    | ProcCpuLoad       | 进程CPU负载占比。        |%|
    | ProcCpuUsage      | 进程CPU使用率。          |%| 
    | ProcUCpuUsage     | 进程用户态CPU使用率。     |%|
    | ProcSCpuUsage     | 进程内核态CPU使用率。     |%| 
    | gpuFrequ          | 整机GPU的频率。          |%|
    | gpuLoad           | 整机GPU的负载占比。      |%|
    | currentNow        | 当前读到的电流值。       |单位：mA| 
    | voltageNow        | 当前读到的电压值。       |单位：μV| 
    | fps               | 每秒帧数。              |单位：fps|
    | fpsJitters        | 每一帧绘制间隔。        |单位：ns|
    | refreshrate       | 屏幕刷新率。            |单位：Hz|
    | networkDown       | 下行速率。              |单位：byte/s|
    | networkUp         | 上行速率。              |单位：byte/s|
    | ddrFrequency      | DDR频率。               |单位：Hz|
    | gpu-thermal       | GPU温度。              |单位：°C|
    | soc-thermal       | 系统芯片温度。          |单位：°C|
    | memAvailable      | 整机可用内存。         |单位：KB|
    | memFree           | 整机空闲内存。         |单位：KB|
    | memTotal          | 整机总内存。           |单位：KB|
    | pss               | 进程实际使用内存。      |单位：KB|
    | sharedClean       | 共享的未改写页面。      |单位：KB|
    | sharedDirty       | 共享的已改写页面。      |单位：KB|
    | priviateClean     | 私有的未改写页面。      |单位：KB|
    | privateDirty      | 私有的已改写页面。      |单位：KB|
    | swapTotal         | 总的交换内存。          |单位：KB|
    | swapPss           | 交换的pss内存。        |单位：KB|
    | HeapSize          | 堆内存大小。           |单位：KB|
    | HeapAlloc         | 可分配的堆内存大小。    |单位：KB|
    | HeapFree          | 剩余的堆内存大小。      |单位：KB|
    | gpuPss            | 使用的gpu内存大小。     |单位：KB|
    | graphicPss        | 使用的图形内存大小。     |单位：KB|
    | arktsHeapPss      | 使用的arkts内存大小。    |单位：KB|
    | nativeHeapPss     | 使用的native内存大小。   |单位：KB|
    | stackPss          | 使用的栈内存大小。       |单位：KB|
    | timeStamp         | 当前时间戳。            |对应采集时间| 
    <!--RP6--><!--RP6End-->

### 场景化采集

<!--RP7-->

除基本采集外，还支持采集响应和完成时延等内容。场景化采集结果不写入data.csv，采集结果直接在命令框显示。

| 命令参数   |必选| 说明                   |
| :-----|:-----| :--------------------- |
| -editor|是|    场景化采集标识，后可添加参数配置项。         |
| -responseTime|否|    响应时延。         |
| -completeTime|否|    完成时延。         |
| -fpsohtest|否|    validator用于获取fps，1秒采集一次，默认采集10次。       |

#### 使用示例

- 应用响应时延（命令仅支持RK）

  ```
   # SP_daemon -editor responseTime ohos.samples.ecg ohtest
   time:544ms

   command exec finished!
  ```
  >**说明**
  >
  >- 采集前先进入应用内，在命令框回车后切换至应用内页面，等待打印采集结果。

- 应用完成时延（命令仅支持RK）

  ```
   # SP_daemon -editor completeTime ohos.samples.ecg ohtest
   time:677ms

   command exec finished!
  ```
  >**说明**
  >
  >- 采集前先进入应用内，在命令框回车后切换至应用内页面，等待打印采集结果。

- validator获取应用页面帧率

  ```
   # SP_daemon -editor fpsohtest
   set num:10 successfps:0|1726909713442fps:97|1726909714442fps:113|1726909715442fps:116|1726909716442fps:116|1726909717442fps:118|1726909718442fps:114|1726909719442fps:114|1726909720442fps:115|1726909721442fps:118|1726909722442SP_daemon exec finished!
  ```
  >**说明**
  >
  >- 执行命令后需滑动或切换当前页面，等待10s后打印采集结果。

<!--RP7End-->

### 其他采集

当前设备电量采集结果可写入csv文件，其它命令需单独采集，采集结果不写入data.csv，仅在命令框显示。

| 命令参数   |必选| 说明                   |
| :-----|:-----| :--------------------- |
| -screen |否| 采集屏幕分辨率和刷新率。               |
| -deviceinfo|否| 获取设备信息。              |
| -server|否|    启停采集用来拉起daemon进程。           |
| -clear|否|    清除所有SP_daemon进程。           |
| -ohtestfps|否|    validator用于获取fps，可设置采集次数(1秒采集一次)。          |
| -editorServer|否|    editor工具用来拉起daemon进程。         |
| -recordcapacity|否|    获取当前设备电量。         |
| -profilerfps |否| 采集当前界面fps。          |

#### 使用示例

- 获取屏幕分辨率

  ```
   # SP_daemon -screen
   activeMode: 720x1280, refreshrate=69
    
    
   command exec finished!
   #
  ```
  >**说明**
  >
  >- activeMode表示当前屏幕分辨率，refreshrate表示屏幕刷新率。

- 获取设备信息

  ```
   # SP_daemon -deviceinfo
   abilist: default
   activeMode: 720x1280
   board: hw
   brand: default
   cpu_c1_cluster: 0 1 2 3
   cpu_c1_max: 1992000
   cpu_c1_min: 408000
   cpu_cluster_name: policy0
   daemonPerfVersion: 1.0.5
   deviceTypeName: rk3568
   fullname: OpenHarmony-5.1.0.46
   gpu_max_freq: 800000000
   gpu_min_freq: 200000000
   model: ohos
   name: OpenHarmony 3.2
   sn: 150100424a5444345209d941bec6b900
   version: OpenHarmony 5.1.0.46
    
   command exec finished!
   #
  ```

- 启动一个进程来监听start和stop命令的socket消息。

  ```
   # SP_daemon -server
   #
   # pidof SP_daemon
   7024
   #
  ```
  >**说明**
  >
  >- 可执行pidof SP_daemon查看进程id。

- 清除SP_daemon进程ID

  ```
   # pidof SP_daemon
   2725   
   # SP_daemon -clear
    
    
   command exec finished!
   #
   # pidof SP_daemon
   #
  ```
  >**说明**
  >
  >- 可执行pidof SP_daemon查看进程id。

- validator用于获取当前页面帧率

  ```
   # SP_daemon -ohtestfps 10
   set num:10 success
   fps:1|1501926684532
   fps:18|1501926685532
   fps:37|1501926686532
   fps:41|1501926687532
   fps:42|1501926688532
   fps:16|1501926689532
   fps:40|1501926690532
   fps:40|1501926691532
   fps:42|1501926692532
   fps:41|1501926693532
   SP_daemon exec finished!
   #
  ```
  >**说明**
  >
  >- 该条命令里的10表示采集的次数（一秒采集一次），可以设置为其他正整数。


- 启动一个进程来监听editor工具的socket消息

  ```
   # SP_daemon -editorServer
    
    
   command exec finished!
  ```


- 获取电池电量

  ```
   # SP_daemon -recordcapacity
   recordTime: 1726903063
   recordPower: 5502
  ```
  >**说明**
  >
  >- recordTime表示时间戳，recordPower表示当前时刻的电量。
  >
  >- 该命令需单独采集，采集结果写入/data/local/tmp/powerLeftRecord.csv，可以使用hdc file recv导出到本地。具体请参考[查看csv采集结果](#查看csv采集结果)。

- 采集当前界面fps

  ```
    # SP_daemon -profilerfps 10
    set num:10 success
    fps:0|1711692357278
    fps:0|1711692358278
    fps:1|1711692359278
    fps:0|1711692360278
    fps:0|1711692361278
    fps:0|1711692362278
    fps:0|1711692363278
    fps:0|1711692364278
    fps:26|1711692365278
    fps:53|1711692366278
    SP_daemon exec finished!
    #
  ```
  >**说明**
  >
  >- 该条命令里的100表示采集的次数（一秒采集一次），可以设置为其他正整数。

- fps分段采集

  ```
    # SP_daemon -profilerfps 100 -sections 10
    set num:100 success
    fps:0|1711692393278
    fps:0|1711692394278
    fps:0|1711692395278
    fps:44|1711692396278
    sectionsFps:0|1711692396278
    sectionsFps:0|1711692396378
    sectionsFps:40|1711692396478
    sectionsFps:60|1711692396578
    sectionsFps:60|1711692396678
    sectionsFps:60|1711692396778
    sectionsFps:60|1711692396878
    sectionsFps:40|1711692396978
    sectionsFps:60|1711692397078
    sectionsFps:60|1711692397178
    fps:51|1711692397278

    ...

    SP_daemon exec finished!
    #
  ```
  >**说明**
  >
  >- 该条命令里的100表示采集的次数（一秒采集一次），可以设置为其他正整数，10表示分段：目前支持设置 1-10（正整数）段采集。