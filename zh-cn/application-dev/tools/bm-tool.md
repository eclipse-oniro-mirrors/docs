# bm工具

Bundle Manager（包管理工具，简称bm）是实现应用安装、卸载、更新、查询等功能的工具，bm为开发者提供基本的应用安装包的调试能力。

## 环境要求（hdc工具）

在使用本工具前，开发者需要先获取[hdc工具](../dfx/hdc.md#环境准备)，执行hdc shell。

## bm工具命令列表

| 命令 | 描述 |
| -------- | -------- |
| help | 帮助命令，用于查询bm支持的命令信息。 |
| install | 安装命令，用于安装应用。 |
| uninstall | 卸载命令，用于卸载应用。 |
| dump | 查询命令，用于查询应用的相关信息。 |
| clean | 清理命令，用于清理应用的缓存和数据。此命令在root版本下可用，在user版本下打开开发者模式可用。其它情况不可用。|
| <!--DelRow-->enable | 使能命令，用于使能应用，使能后应用可以继续使用。此命令在root版本下可用，在user版本下不可用。 |
| <!--DelRow-->disable | 禁用命令，用于禁用应用，禁用后应用无法使用。此命令在root版本下可用，在user版本下不可用。 |
| get | 获取udid命令，用于获取设备的udid。 |
| quickfix | 快速修复相关命令，用于执行补丁相关操作，如补丁安装、补丁查询。 |
| compile | 应用执行编译AOT命令。 |
| copy-ap | 把应用的ap文件拷贝到/data/local/pgo目录下，供shell用户读取文件。 |
| dump-dependencies | 查询应用依赖的模块信息。 |
| dump-shared | 查询应用间HSP应用信息。 |
| dump-overlay | 打印overlay应用的overlayModuleInfo。 |
| dump-target-overlay | 打印目标应用的所有关联overlay应用的overlayModuleInfo。 |


## 帮助命令（help）

```bash
# 显示帮助信息
bm help
```


## 安装命令（install）

```bash
bm install [-h] [-p filePath] [-r] [-w waitingTime] [-s hspDirPath]
```

  **安装命令参数列表**


| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -p | 必选参数，指定路径和多个HAP同时安装。 |
| -r | 可选参数，覆盖安装一个HAP。默认值为覆盖安装。 |
| -s | 根据场景判断，安装应用间HSP时为必选参数，其他场景为可选参数。安装应用间共享库， 每个路径目录下只能存在一个同包名的HSP。 |
| -w | 可选参数，安装HAP时指定bm工具等待时间，最小的等待时长为5s，最大的等待时长为600s,&nbsp;默认缺省为5s。 |


示例：
```bash
# 安装一个hap
bm install -p /data/app/ohos.app.hap
# 覆盖安装一个hap
bm install -p /data/app/ohos.app.hap -r
# 安装一个应用间共享库
bm install -s xxx.hsp
# 同时安装使用方应用和其依赖的应用间共享库
bm install -p aaa.hap -s xxx.hsp yyy.hsp
# 安装一个hap,等待时间为10s
bm install -p /data/app/ohos.app.hap -w 10
```

## 卸载命令（uninstall）

```bash
bm uninstall [-h] [-n bundleName] [-m moduleName] [-k] [-s] [-v versionCode]
```

  **卸载命令参数列表**

| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -n | 必选参数，指定Bundle名称卸载应用。|
| -m | 可选参数，指定卸载应用的一个模块。默认卸载所有模块。 |
| -k | 可选参数，卸载应用时保存应用数据。默认卸载应用时不保存应用数据。 |
| -s | 根据场景判断，安装应用间HSP时必选参数，其他场景为可选参数。卸载指定的共享库。|
| -v | 可选参数，指定共享包的版本号。默认卸载同包名的所有共享包。 |


示例：

```bash
# 卸载一个应用
bm uninstall -n com.ohos.app
# 卸载应用的一个模块
bm uninstall -n com.ohos.app -m com.ohos.app.EntryAbility
# 卸载一个shared bundle
bm uninstall -n com.ohos.example -s
# 卸载一个shared bundle的指定版本
bm uninstall -n com.ohos.example -s -v 100001
# 卸载一个应用，并保留用户数据
bm uninstall -n com.ohos.app -k
```


## 查询应用信息命令（dump）

```bash
bm dump [-h] [-a] [-n bundleName] [-s shortcutInfo] [-d deviceId]
```

  **查询命令参数列表**

| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -a | 可选参数，查询系统已经安装的所有应用。 |
| -n | 可选参数，查询指定Bundle名称的详细信息。 |
| -s | 可选参数，查询指定Bundle名称下的快捷方式信息。 |
| -d | 可选参数，查询指定设备中的包信息。默认查询当前设备。 |


示例：

```bash
# 显示所有已安装的Bundle名称
bm dump -a
# 查询该应用的详细信息
bm dump -n com.ohos.app
# 查询该应用的快捷方式信息
bm dump -s -n com.ohos.app
# 查询跨设备应用信息
bm dump -n com.ohos.app -d xxxxx
```

## 清理命令（clean）

```bash
bm clean [-h] [-c] [-n bundleName] [-d] [-i appIndex]
```
**清理命令参数列表**

| 参数 | 参数说明 |
| -------- | --------- |
| -h | 帮助信息。 |
| -c&nbsp;-n | -n为必选参数，-c为可选参数。清除指定Bundle名称的缓存数据。 |
| -d&nbsp;-n | -n为必选参数，-d为可选参数。清除指定Bundle名称的数据目录。 |
| -i | 可选参数，清除分身应用的数据目录。默认为0。|


示例：

```bash
# 清理该应用下的缓存数据
bm clean -c -n com.ohos.app
# 清理该应用下的用户数据
bm clean -d -n com.ohos.app
// 执行结果
clean bundle data files successfully.
```

<!--Del-->
## 使能命令（enable）

```bash
bm enable [-h] [-n bundleName] [-a abilityName]
```


  **使能命令参数列表**

| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -n | 必选参数，使能指定Bundle名称的应用。 |
| -a | 可选参数，使能指定Bundle名称下的元能力模块。 |


示例：

```bash
# 使能该应用
bm enable -n com.ohos.app -a com.ohos.app.EntryAbility
// 执行结果
enable bundle successfully.
```


## 禁用命令（disable）

```bash
bm disable [-h] [-n bundleName] [-a abilityName]
```


  **禁用命令参数列表**

| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -n | 必选参数，禁用指定Bundle名称的应用。 |
| -a | 可选参数，禁用指定Bundle名称下的元能力模块。 |


示例：

```bash
# 禁用该应用
bm disable -n com.ohos.app -a com.ohos.app.EntryAbility
// 执行结果
disable bundle successfully.
```
<!--DelEnd-->


## 获取udid命令（get）

```bash
bm get [-h] [-u]
```

  **获取udid命令参数列表**

| 参数 | 参数说明 |
| -------- | -------- |
| -h |帮助信息。 |
| -u | 必选参数，获取设备的udid。|


示例：

```bash
# 获取设备的udid
bm get -u
// 执行结果
udid of current device is :
23CADE0C
```


## 快速修复命令（quickfix）

```bash
bm quickfix [-h] [-a -f filePath [-t targetPath] [-d]] [-q -b bundleName] [-r -b bundleName]
```

注：hqf文件制作方式可参考[HQF打包指令](packing-tool.md#hqf打包指令)。

  **快速修复命令参数列表**
|   参数  | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -a&nbsp;-f | -a为可选参数，指定-a后，-f为必选参数。执行快速修复补丁安装命令，file-path对应hqf文件，支持传递1个或多个hqf文件，或传递hqf文件所在的目录。 |
| -q&nbsp;-b | -q为可选参数，指定-q后，-b为必选参数，未指定-q。根据包名查询补丁信息。 |
| -r&nbsp;-b | -r为可选参数，指定-r后，-b为必选参数。根据包名卸载未使能的补丁。|
| -t | 可选参数，快速修复应用到指定目标路径。|
| -d | 可选参数，应用快速修复调试模式。|



示例：

```bash
# 根据包名查询补丁包信息
bm quickfix -q -b com.ohos.app
// 执行结果
// Information as follows:
// ApplicationQuickFixInfo:
//  bundle name: com.ohos.app
//  bundle version code: xxx
//  bundle version name: xxx
//  patch version code: x
//  patch version name:
//  cpu abi:
//  native library path:
//  type:
# 快速修复补丁安装
bm quickfix -a -f /data/app/
// 执行结果
apply quickfix succeed.
# 快速修复补丁卸载
bm quickfix -r -b com.ohos.app
// 执行结果
delete quick fix successfully
```

## 共享库查询命令（dump-shared）

```bash
bm dump-shared [-h] [-a] [-n bundleName] [-m moduleName]
```

  **共享库查询命令参数列表**

| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -a | 可选参数，查询系统中已安装所有共享库。|
| -n | 可选参数，查询指定共享库包名的详细信息。|
| -m | 可选参数，查询指定共享库包名和模块名的详细信息。|


示例：

```bash
# 显示所有已安装共享库包名
bm dump-shared -a
# 显示该共享库的详细信息
bm dump-shared -n com.ohos.lib
# 显示指定应用指定模块依赖的共享库信息
bm dump-dependencies -n com.ohos.app -m entry
```

## 共享库依赖关系查询命令（dump-dependencies）

显示指定应用和指定模块依赖的共享库信息。
```bash
bm dump-dependencies [-h] [-n bundleName] [-m moduleName]
```

  **共享库依赖关系查询命令参数列表**
| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -n | 必选参数，查询指定共享库包名的详细信息。|
| -m | 可选参数，查询指定应用指定模块依赖的共享库信息。|

示例：
```Bash
# 显示指定应用指定模块依赖的共享库信息
bm dump-dependencies -n com.ohos.app -m entry
```


## 应用执行编译AOT命令（compile）

应用执行编译AOT命令。
```bash
bm compile [-h] [-m mode] [-r bundleName] [-a]
```
  **compile命令参数列表**

| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -a | 可选参数，编译所有应用。|
| -m | 可选参数，可选值为partial或者full。根据包名编译应用。|
| -r | 可选参数，移除应用的结果。|

示例：

```bash
# 根据包名编译应用
bm compile -m partial com.example.myapplication
```

## 拷贝ap文件命令（copy-ap）

拷贝ap文件到指定应用的/data/local/pgo路径。

```bash
bm copy-ap [-h] [-a] [-n bundleName]
```

**copy-ap命令参数列表**

| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -a | 可选参数，默认所有包相关ap文件。拷贝所有包相关ap文件。|
| -n | 可选参数，默认当前应用包名。根据包名拷贝对应包相关的ap文件。|

示例：

```bash
# 根据包名移动对应包相关的ap文件
bm copy-ap -n com.example.myapplication
```

## 查询overlay应用信息命令（dump-overlay）

打印overlay应用的overlayModuleInfo。
```bash
bm dump-overlay [-h] [-b bundleName] [-m moduleName] [-t targetModuleName]
```

**dump-overlay命令参数列表**
| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -b | 必选参数，获取指定应用的所有OverlayModuleInfo信息。|
| -m | 可选参数，默认当前应用主模块名。根据指定的包名和module名查询OverlayModuleInfo信息。|
| -t | 可选参数，根据指定的包名和目标module名查询OverlayModuleInfo信息。|

示例：

```bash
# 根据包名来获取overlay应用com.ohos.app中的所有OverlayModuleInfo信息
bm dump-overlay -b com.ohos.app

# 根据包名和module来获取overlay应用com.ohos.app中overlay module为entry的所有OverlayModuleInfo信息
bm dump-overlay -b com.ohos.app -m entry

# 根据包名和module来获取overlay应用com.ohos.app中目标module为feature的所有OverlayModuleInfo信息
bm dump-overlay -b com.ohos.app -m feature
```

## 查询应用的overlay相关信息命令（dump-target-overlay）

查询目标应用的所有关联overlay应用的overlayModuleInfo信息。

```bash
bm dump-target-overlay [-h] [-b bundleName] [-m moduleName]
```

**dump-target-overlay命令参数列表**
| 参数 | 参数说明 |
| -------- | -------- |
| -h | 帮助信息。 |
| -b | 必选参数，获取指定应用的所有OverlayBundleInfo信息。|
| -m | 可选参数，默认当前应用主模块名。根据指定的包名和module名查询OverlayBundleInfo信息。|

示例：

```bash
# 根据包名来获取目标应用com.ohos.app中的所有关联的OverlayBundleInfo信息
bm dump-target-overlay-b com.ohos.app

# 根据包名和module来获取目标应用com.ohos.app中目标module为entry的所有关联的OverlayModuleInfo信息
bm dump-target-overlay -b com.ohos.app -m entry
```

## bm工具错误码

### 301 系统账号不存在
**错误信息**

error: user not exist.

**错误描述**

系统账号不存在。

**可能原因**

安装应用时，系统账号ID不存在。

**处理步骤**

1. 重启手机后再次尝试安装应用。

2. 重复上述步骤3到5次后依旧安装失败，请导出日志文件提[在线工单](https://developer.huawei.com/consumer/cn/support/feedback/#/)获取帮助。

```
hdc file recv /data/log/hilog/
```

### 304 当前系统账号没有安装HAP包
**错误信息**

error: user does not install the hap.

**错误描述**

卸载操作时，当前系统账号没有安装HAP包。

**可能原因**

当前系统账号下未安装任何HAP包。

**处理步骤**

当前系统账号下未安装任何HAP包，请不要执行卸载应用操作。

### 9568319 签名文件异常
**错误信息**

error: cannot open signature file.

**错误描述**

安装应用过程中，出现签名文件打开异常，导致安装失败。

**可能原因**

HAP包签名文件存在异常。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

### 9568320 签名文件不存在
**错误信息**

error: no signature file.

**错误描述**

用户安装未签名的HAP包。

**可能原因**

HAP包没有签名。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

### 9568321 签名文件解析失败
**错误信息**

error: fail to parse signature file.

**错误描述**

用户安装时签名文件解析失败。

**可能原因**

HAP包签名文件存在异常。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

### 9568323 签名摘要验证未通过
**错误信息**

error: signature verification failed due to not bad digest.

**错误描述**

用户安装时签名验证失败。

**可能原因**

HAP包签名不正确。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

### 9568324 签名完整性校验未通过
**错误信息**

error: signature verification failed due to out of integrity.

**错误描述**

用户安装时签名验证失败。

**可能原因**

HAP包签名不正确。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

### 9568326 签名公钥存在异常
**错误信息**

error: signature verification failed due to bad public key.

**错误描述**

用户安装时签名验证失败，签名公钥存在异常。

**可能原因**

HAP包签名不正确。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

### 9568327 签名获取异常
**错误信息**

error: signature verification failed due to bad bundle signature.

**错误描述**

用户安装时签名验证失败，签名获取异常。

**可能原因**

HAP包签名不正确。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

### 9568328 未找到配置文件区块
**错误信息**

error: signature verification failed due to no profile block.

**错误描述**

用户安装时签名验证失败，未找到配置文件区块。

**可能原因**

HAP包签名不正确。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

### 9568330 初始化签名源失败
**错误信息**

error: signature verification failed due to init source failed.

**错误描述**

用户安装时签名验证失败，初始化签名源失败。

**可能原因**

HAP包签名不正确。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

### 9568257 签名文件Pkcs7校验失败

**错误信息**

error: fail to verify pkcs7 file.

**错误描述**

用户安装应用时签名Pkcs7校验失败。

**可能原因**

1. 证书链不完整或不受信任。
2. 签名算法不匹配。
3. 数据被篡改或签名文件损坏。
4. 签名格式不匹配。
5. 私钥不匹配。

**处理步骤**

1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
2. 使用手动签名，请参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。


### 9568347 解析本地so文件失败
**错误信息**

error: install parse native so failed.

**错误描述**

在启动调试或运行C++应用/服务时，安装HAP包出现错误，提示“error: install parse native so failed”错误信息。

**可能原因**

设备支持的Abi类型与C++工程中配置的Abi类型不匹配。

> **说明：**
>
> - 如果工程有依赖HSP或者HAR模块，请确保所有包含C++代码的模块配置的Abi类型包含设备支持的Abi类型。
> - 如果工程依赖的三方库包含so文件，请确保oh_modules/三方库/libs目录包含有设备支持的Abi目录，如libs/arm64-v8a、/libs/x86_64。
<!--RP1--><!--RP1End-->

**处理步骤**

1. 将设备与DevEco Studio进行连接。
2. 执行如下命令，查询设备支持的Abi列表，返回结果为default/armeabi-v7a/armeabi/arm64-v8a/x86/x86_64中的一个或多个Abi类型。
    ```
    hdc shell
    param get const.product.cpu.abilist
    ```
3. 根据查询返回结果，检查[模块级build-profile.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V13/ide-hvigor-compilation-options-customizing-sample-V13#section4322212200)文件中的[“abiFilters”参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ohos-abi#%E5%9C%A8%E7%BC%96%E8%AF%91%E6%9E%B6%E6%9E%84%E4%B8%AD%E6%8C%87%E5%AE%9Aabi)中的配置，规则如下：
    * 若返回结果为default，请执行如下命令，查询是否存在lib64文件夹。
      ```
      cd /system/
      ls
      ```
      ![示例图](figures/zh-cn_image_0000001609001262.png)
      * 存在lib64文件夹：则“abiFilters”参数中需要包含arm64-v8a类型。
      * 不存在lib64文件夹：则“abiFilters”参数中需要至少包含armeabi/armeabi-v7a中的一个类型。
    * 若返回结果为armeabi-v7a/armeabi/arm64-v8a/x86/x86_64中的一个或多个，需要在“abiFilters”参数中至少包含返回结果中的一个Abi类型。


### 9568344 解析配置文件失败
**错误信息**

error: install parse profile prop check error.

![示例图](figures/zh-cn_image_0000001585361412.png)

**错误描述**

在启动调试或运行应用/服务时，安装HAP出现错误，提示“error: install parse profile prop check error”错误信息。

**可能原因**

1. [app.json5配置文件](../quick-start/app-configuration-file.md#配置文件标签)中的bundleName、[module.json5配置文件](../quick-start/module-configuration-file.md#配置文件标签)中name不符合命名规则。

<!--Del-->
2. [extensionAbilities](../quick-start/module-configuration-file.md#extensionabilities标签)中type字段配置为service或dataShare。
<!--DelEnd-->


**处理步骤**
1. 根据命名规则调整app.json5配置文件中bundleName、module.json5文件中的name字段。
<!--Del-->
2. 若extensionAbilities中type字段配置为service或dataShare，应用需要配置[allowAppUsePrivilegeExtension特权](../../device-dev/subsystems/subsys-app-privilege-config-guide.md)，配置方式如下。

    1. 获取新的签名指纹。

        a. 在工程级build-profile.json5(工程根目录下)文件中，signingConfigs字段内的profile的值即为签名文件的存储路径。

        b. 打开该签名文件（后缀为.p7b），打开后在文件内搜索“development-certificate”，将“-----BEGIN CERTIFICATE-----”和“-----END CERTIFICATE-----”以及中间的信息拷贝到新的文本中，注意换行并去掉换行符，保存为一个新的.cer文件，如命名为xxx.cer。

        新的.cer文件格式如下图（仅作为格式示意，内容以实际为准）：

        ![示例图](figures/zh-cn_image_0000001585521364.png)

        c. 使用keytool工具（在DevEco Studio安装目录下的jbr/bin文件夹内），执行如下命令，通过.cer文件获取证书指纹的SHA256值。
          ```
          keytool -printcert -file xxx.cer
          ```
        d. 将证书指纹中SHA256的内容去掉冒号，即为最终要获得的签名指纹。

        如下图（仅作为格式示意，内容以实际为准）：
        ![示例图](figures/zh-cn_image_0000001635921233.png)

        去掉冒号后的签名指纹为：5753DDBC1A8EF88A62058A9FC4B6AFAFC1C5D8D1A1B86FB3532739B625F8F3DB。

    2. 获取设备的特权管控白名单文件install_list_capability.json。

        a. 连接设备，进入shell。
        ```
        hdc shell
        ```
        b. 执行如下命令查看设备的特权管控白名单文件install_list_capability.json。
        ```
        // 设备中查询白名单文件的位置
        find /system -name install_list_capability.json
        ```
        c. 执行如下命令拉取install_list_capability.json。
        ```
        hdc target mount
        hdc file recv /system/etc/app/install_list_capability.json
        ```

    3. 将步骤1获取到的签名指纹配置到install_list_capability.json文件的app_signature中，注意要配置到对应的bundleName下。
    ![示例图](figures/zh-cn_image_0000001635641893.png)
    4. 将修改后的install_list_capability.json文件重新推到设备上，并重启设备。

        ```
        hdc target mount
        hdc file send install_list_capability.json /system/etc/app/install_list_capability.json
        hdc shell chmod 644 /system/etc/app/install_list_capability.json
        hdc shell reboot
        ```
    5. 设备重启后，重新安装新的应用即可。<!--DelEnd-->


### 9568305 依赖的模块不存在
**错误信息**

error: dependent module does not exist.

![示例图](figures/zh-cn_image_0000001560338986.png)

**错误描述**

在启动调试或运行应用/服务时，安装HAP出现错误，提示“error: dependent module does not exist”错误信息。

**可能原因**

运行/调试的应用依赖的动态共享包（SharedLibrary）模块未安装导致安装报错。

**处理步骤**

1. 先安装依赖的动态共享包（SharedLibrary）模块，再在应用运行配置页勾选Keep Application Data，点击OK保存配置，再运行/调试。
![示例图](figures/zh-cn_image_0000001560201786.png)
2. 在运行配置页，选择Deploy Multi Hap标签页，勾选Deploy Multi Hap Packages，选择依赖的模块，点击OK保存配置，再进行运行/调试。
![示例图](figures/zh-cn_image_0000001610761941.png)
3. 单击Run > Edit Configurations，在General中，勾选Auto Dependencies。点击OK保存配置，再运行/调试。
![示例图](figures/zh-cn_image_9568305.png)

### 9568259 安装解析配置文件缺少字段
**错误信息**

error: install parse profile missing prop.

![示例图](figures/zh-cn_image_0000001559130596.png)

**错误描述**

在启动调试或运行应用/服务时，安装HAP出现错误，提示“error: install parse profile missing prop”错误信息。

**可能原因**

配置文件app.json5和module.json5中必填字段缺失。

**处理步骤**

* 方法1：请参考[app.json5配置文件](../quick-start/app-configuration-file.md)和[module.json5配置文件](../quick-start/module-configuration-file.md)查看并补充必填字段。
* 方法2：通过hilog日志判断缺失字段。

    开启落盘命令：
    ```
    hilog -w start
    ```

    落盘位置：/data/log/hilog。

    打开日志查看“profile prop %{public}s is mission”。如“profile prop icon is mission”表示“icon”字段缺失。


### 9568258 安装应用的releaseType与已安装应用的releaseType不相同
**错误信息**

error: install releaseType target not same.

![示例图](figures/zh-cn_image_0000001609976041.png)

**错误描述**

在启动调试或运行应用/服务时，安装HAP出现错误，提示“error: install releaseType target not same”错误信息。

**可能原因**

* 场景一：设备上已安装的旧HAP和现在要安装的新HAP所使用的SDK中的releaseType值不一样。
* 场景二：安装的应用为多HAP时，每个HAP所使用的SDK中的releaseType值不一致。

**处理步骤**

* 场景一：请先卸载设备上已安装的HAP，再安装新的HAP。
* 场景二：使用相同版本的SDK对HAP重新打包，保证多HAP的releaseType值一致。


### 9568322 由于应用来源不可信，签名验证失败
**错误信息**

error: signature verification failed due to not trusted app source.

![示例图](figures/zh-cn_image_0000001585042216.png)

**错误描述**

在启动调试或运行应用/服务时，安装HAP出现错误，提示“error: signature verification failed due to not trusted app source”错误信息。

**可能原因**

* 场景一：签名中未包含该调试设备的UDID。

* 场景二：签名时使用了[发布证书和发布profile文件](https://developer.huawei.com/consumer/cn/doc/app/agc-help-releaseharmony-0000001933963166)。发布证书签名的应用不能启动调试或运行。

**处理步骤**

* 场景一：
	1. 使用[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)。在连接设备后，重新为应用进行签名。
	2. 如果使用的是手动签名，对于OpenHarmony应用，请参考<!--RP2-->[OpenHarmony应用手动签名](../security/hapsigntool-guidelines.md)<!--RP2End-->，在UnsgnedDebugProfileTemplate.json文件中添加该调试设备的**UDID**。

        1. 获取当前设备的UDID。

        ```
          //UDID获取命令
          hdc shell bm get -u
        ```

        2. 打开IDE安装路径，在sdk目录下找到UnsgnedDebugProfileTemplate.json配置文件。

        ```
          IDE安装路径\sdk\版本号或者default\openharmony\toolchains\lib\

          例如：xxxx\Huawei\DevEco Studio\sdk\HarmonyOS-NEXT-DB1\openharmony\toolchains\lib\
          例如：xxxx\Huawei\DevEco Studio\sdk\default\openharmony\toolchains\lib\
        ```

        3. 在UnsgnedDebugProfileTemplate.json文件的device-ids字段中，添加当前设备的UDID。

* 场景二：使用[调试证书和调试profile文件](https://developer.huawei.com/consumer/cn/doc/app/agc-help-debug-app-0000001914423098)重新签名应用。

### 9568286 安装应用的签名证书profile文件中的类型与已安装应用的不相同
**错误信息**

error: install provision type not same.

**错误描述**

在启动调试或运行应用/服务时，由于安装应用的[签名证书profile文件](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-releaseprofile-0000001914714796)中的类型与已安装应用的不相同，导致安装HAP出现错误。

**可能原因**

设备上已安装应用的签名证书profile文件中的类型与待安装应用不一致。

**处理步骤**

1. 确保设备上已安装应用签名证书profile文件中的类型与待安装应用的类型一致，使用相同类型的profile文件签名，再安装新的HAP。
2. 卸载设备上已安装的应用，再安装新的HAP。


### 9568289 权限请求失败导致安装失败
**错误信息**

error: install failed due to grant request permissions failed.

![示例图](figures/zh-cn_image_0000001585201996.png)

**错误描述**

在启动调试或运行应用/服务时，安装HAP出现错误，提示“error: install failed due to grant request permissions failed”错误信息。

**可能原因**

默认应用等级为normal，只能使用normal等级的权限，如果使用了system_basic或system_core等级的权限，将导致报错。

**处理步骤**

1. 打开IDE安装路径，在sdk目录下找到UnsgnedDebugProfileTemplate.json配置文件。
```
IDE安装路径\sdk\版本号或者default\openharmony\toolchains\lib\

例如：xxxx\Huawei\DevEco Studio\sdk\HarmonyOS-NEXT-DB1\openharmony\toolchains\lib\
例如：xxxx\Huawei\DevEco Studio\sdk\default\openharmony\toolchains\lib\
```
2. 在UnsgnedDebugProfileTemplate.json文件中修改APL等级，修改APL等级为system_core等级，重新签名打包即可。

### 9568297 由于设备sdk版本较低导致安装失败
**错误信息**

error: install failed due to older sdk version in the device.

![示例图](figures/zh-cn_image_0000001635521909.png)

**错误描述**

在启动调试或运行应用/服务时，安装HAP出现错误，提示“error: install failed due to older sdk version in the device”错误信息。

**可能原因**

该问题是由于编译打包所使用的SDK版本与设备镜像版本不匹配。

**处理步骤**

* 场景一：设备上的镜像版本低于编译打包的SDK版本，请更新设备镜像版本。查询设备镜像版本命令：
  ```
  hdc shell param get const.ohos.apiversion
  ```
  如果镜像提供的api版本为10，且应用编译所使用的SDK版本也为10，仍出现该报错，可能是由于镜像版本较低，未兼容新版本SDK校验规则，请将镜像版本更新为最新版本。

* 场景二：对于需要运行在OpenHarmony设备上的应用，请确认runtimeOS已改为OpenHarmony。

### 9568332 签名不一致导致安装失败
**错误信息**

error: install sign info inconsistent.

![示例图](figures/zh-cn_image_0000001635761329.png)

**错误描述**

在启动调试或运行应用/服务时，安装HAP出现错误，提示“error: install sign info inconsistent”错误信息。

**可能原因**

1. 设备上已安装的应用与新安装的应用中签名不一致或者多个包（HAP和HSP）之间的签名存在差异。如果在“Edit Configurations”中勾选了“Keep Application Data”（即不卸载应用，直接覆盖安装），并且重新进行了签名，将导致该报错。
2. 如果某个应用被卸载但是保留了数据，那么后面安装相同包名的应用时，需要校验其身份信息的一致性。如果两者的签名信息皆不一致，则会导致该报错。


**处理步骤**

1. 请卸载设备上已安装的应用，或取消勾选“Keep Application Data”后，重新安装新的应用。
2. 如果是因不同团队提供的HSP导致签名不一致问题，可以采用[集成态HSP](../quick-start/integrated-hsp.md)的方式统一提供HSP；在多HAP包的情况下，必须确保所有HAP包的签名一致。
3. 如果某个应用被卸载但是保留了数据，后面安装相同包名但签名信息不一致的应用时，安装失败。如果出现这种情况，则需要把之前已卸载掉的应用重新安装之后，执行不保留数据地卸载，这样相同包名但签名信息不一致的应用才能安装成功。

### 9568329 签名信息验证失败
**错误信息**

error: verify signature failed.

![示例图](figures/zh-cn_image_155401.png)

**错误描述**

签名信息中的包名与应用的包名（bundleName）不一致。

**可能原因**

* 场景一：用户导入了三方提供的HSP模块，且该HSP既非[集成态HSP](../quick-start/integrated-hsp.md)，又非同包名的HSP，造成包名不一致。

* 场景二：用户使用了错误的签名文件（后缀为.p7b）进行签名，造成包名不一致。


**处理步骤**

* 场景一：HSP只能给同包名的应用使用，只有集成态HSP可以给不同包名的应用使用。需要用户与三方开发者确认，三方开发者应提供集成态HSP、或同包名的HSP给用户使用。

* 场景二：检查签名流程和签名证书，参考[应用/服务签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V13/ide-signing-V13)。


### 9568266 安装权限拒绝
**错误信息**

error: install permission denied.

![示例图](figures/zh-cn_image_9568266.png)

**错误描述**

使用hdc install安装HAP时出现错误，提示“code:9568266 error: install permission denied”错误信息。

**可能原因**

hdc install不能安装release签名的企业应用。

**处理步骤**

1. 请使用hdc install指令安装调试debug签名的企业应用。


### 9568337 安装解析失败
**错误信息**

error: install parse unexpected.

**错误描述**

应用推送到设备安装时，报错包管理打开hap文件失败。

**可能原因**

* 场景一：设备system分区存储空间已满，导致hdc file send文件后，因存储空间不足导致设备中文件损坏。

* 场景二：推送hap包到设备过程hap包损坏。

**处理步骤**

* 场景一：查看设备system分区存储空间，若已满，清理存储满足安装所需空间。
  ```bash
  hdc shell df -h /system
  ```

* 场景二：查看本地hap与推送到设备上hap的md5值，若不一致则表示推送过程hap损毁，请尝试重传。


### 9568316 数据代理中APL权限字段描述权限低
**错误信息**

error: apl of required permission in proxy data is too low.

**错误描述**

proxyData标签requiredReadPermission和requiredWritePermission属性验证失败。

**可能原因**

用户工程module.json中，proxyData标签requiredReadPermission和requiredWritePermission属性验证失败，这两个属性要求system_basic或system_core权限等级。

**处理步骤**

1. 检查应用定义的proxyData内容是否符合要求，参考[proxyData标签](../quick-start/module-configuration-file.md#proxydata标签)。


### 9568315 数据代理URI错误
**错误信息**

error: uri in proxy data is wrong.

**错误描述**

proxyData标签uri属性验证失败。

**可能原因**

用户工程module.json中，proxyData标签uri属性验证失败，不满足uri格式要求。

**处理步骤**

1. 检查应用定义的proxyData内容是否符合要求，参考[proxyData标签](../quick-start/module-configuration-file.md#proxydata标签)。


### 9568336 应用调试类型与已安装应用不一致
**错误信息**

error: install debug type not same.

**错误描述**

应用调试类型（app.json的debug字段）与已安装应用不一致。

**可能原因**

开发者使用DevEco Studio的debug按钮安装了应用，后面打包之后又通过hdc install方式安装。

**处理步骤**

1. 卸载已安装的应用，重新安装新应用。


### 9568296 包类型错误
**错误信息**

error: install failed due to error bundle type.

**错误描述**

bundleType错误导致应用安装失败。

**可能原因**

新安装应用的bundleType与已安装的有相同bundleName应用不一致。

**处理步骤**

* 方法一：卸载已安装的应用，重新安装新应用。

* 方法二：修改应用的bundleType，与已安装应用保持一致。


### 9568292 UserID为0的用户只能安装singleton应用
**错误信息**

error: install failed due to zero user can only install singleton app.

**错误描述**

UserID 0用户只允许安装singleton权限应用，singleton权限应用只允许被UserID 0用户安装。

**可能原因**

singleton权限应用安装未指定UserID 0。

**处理步骤**

1. 应用是singleton权限，安装时指定UserID 0。
	```
	//指定userId安装命令
	hdc install -p hap名.hap -u 0
	```


### 9568263 无法降级安装
**错误信息**

error: install version downgrade.

**错误描述**

正在安装应用的VersionCode小于系统中已安装应用的VersionCode，安装失败。

**可能原因**

正在安装应用的VersionCode小于系统中已安装应用的VersionCode。

**处理步骤**

1. 卸载已安装的应用，重新安装新应用。


### 9568304 应用不支持当前设备类型
**错误信息**

error: device type is not supported.

**错误描述**

正在安装的应用不支持当前设备类型，安装失败。

**可能原因**

正在安装的应用不支持当前设备类型。

**处理步骤**

1. 如需要适配当前设备，请在应用设备类型配置中增加当前设备类型。应用deviceTypes配置包含phone（手机）、tablet（平板）、2in1（2合1设备）、tv（智慧屏）、wearable（智能手表）和car（车机）。


### 9568317 应用的多进程配置与系统配置不匹配
**错误信息**

error: isolationMode does not match the system.

**错误描述**

安装应用时，设置的isolationMode与系统配置项允许的系统配置不匹配。

**可能原因**

* 场景一：设备支持隔离模式，即persist.bms.supportIsolationMode为true时，HAP配置的isolationMode为nonisolationOnly。

* 场景二：设备不支持隔离模式，即persist.bms.supportIsolationMode为false时，HAP配置的isolationMode为isolationOnly。

**处理步骤**

1. 按照设备的隔离模式配置HAP配置文件isolationMode属性。
	```
	//查询设备persist.bms.supportIsolationMode值，若返回errNum is:106说明没配置
	hdc shell
	param get persist.bms.supportIsolationMode
	//配置设备persist.bms.supportIsolationMode值
	hdc shell
	param set persist.bms.supportIsolationMode [true|false]
	```


### 9568315 数据代理的uri属性错误
**错误信息**

error: uri in proxy data is wrong.

**错误描述**

应用module.json文件中proxyData标签的uri属性验证失败。

**可能原因**

uri不满足格式规范。

**处理步骤**

1. 确认uri满足格式规范。
	```
	//uri格式规范
	不同数据代理的uri不可重复，且需要满足datashareproxy://当前应用包名/xxx的格式
	```


### 9568310 兼容策略不同
**错误信息**

error: compatible policy not same.

**错误描述**

新包与已安装包兼容策略不同。

**可能原因**

1. 应用已安装，再安装一个同包名的应用间共享库。
2. 应用间共享库已安装，再安装一个同包名的应用。

**处理步骤**

1. 卸载已安装的应用或应用间共享库，再安装新包。


### 9568391 包管理服务已停止
**错误信息**

error: bundle manager service is died.

**错误描述**

包管理服务已停止。

**可能原因**

系统出现未知的异常，导致包管理服务已停止或者异常退出。

**处理步骤**

1. 重启手机后再次尝试安装应用。

2. 重复上述步骤3到5次后依旧安装失败，请查询设备的/data/log/faultlog/faultlogger/目录下是否存在包含foundation字样的crash文件。
```
hdc shell
cd /data/log/faultlog/faultlogger/
ls -ls
```
3. 导出crash文件和日志文件提[在线工单](https://developer.huawei.com/consumer/cn/support/feedback/#/)获取帮助。
```
hdc file recv /data/log/faultlog/faultlogger/
hdc file recv /data/log/hilog/
```

### 9568393 验证代码签名失败
**错误信息**

error: verify code signature failed.

**错误描述**

验证代码签名失败。

**可能原因**

包没有代码签名信息。

**处理步骤**

1. 安装最新版本DevEco Studio，重新签名。

<!--RP3--><!--RP3End-->

### 9568399 拷贝文件失败

**错误信息**

error: copy file failed.

**错误描述**

安装应用过程中，拷贝文件失败。

**可能原因**

1. 拷贝源文件路径或目标路径为无效路径。
2. 源文件打开失败。
3. 获取源文件状态失败。
4. 源文件的大小无效。
6. 源文件拷贝失败。
7. 源文件没有访问权限。
8. 更改文件权限失败。

**处理步骤**

1. 重启手机后再次尝试安装应用。

2. 重复上述步骤3到5次后依旧安装失败，请导出日志文件提[在线工单](https://developer.huawei.com/consumer/cn/support/feedback/#/)获取帮助。

```
hdc file recv /data/log/hilog/
```

### 9568401 调试包仅支持运行在开发者模式设备
**错误信息**

error: debug bundle can only be installed in developer mode.

**错误描述**

调试包仅支持运行在开发者模式设备。

**可能原因**

终端设备未开启“开发者模式”。

**处理步骤**

1. 终端系统查看“设置 > 系统”中是否有“开发者选项”，如果不存在，可在“设置 > 关于本机”连续七次单击“版本号”，直到提示“开启开发者模式”，点击“确认开启”后输入PIN码（如果已设置），设备将自动重启。
2. USB数据线连接终端和PC，在“设置 > 系统 > 开发者选项”中，打开“USB调试”开关，弹出的“允许USB调试”的弹框，点击“允许”。
3. 启动调试或运行应用。

### 9568404 传递签名配置文件失败

**错误信息**

error: delivery sign profile failed.

**错误描述**

安装过程中，传递代码签名配置文件出现异常，导致安装失败。

**可能原因**

1. 文件路径不存在。
2. 创建文件路径失败。
3. 更改文件目录模式失败。
4. 写配置文件数据失败。
5. 更改配置文件模式失败。
6. 添加配置文件数据失败。

**处理步骤**

1. 重启手机后再次尝试安装应用。

2. 重复上述步骤3到5次后依旧安装失败，请导出日志文件提[在线工单](https://developer.huawei.com/consumer/cn/support/feedback/#/)获取帮助。

```
hdc file recv /data/log/hilog/
```

### 9568405 删除签名配置文件失败

**错误信息**

error: remove sign profile failed.

**错误描述**

应用卸载过程中，删除签名配置文件出现异常，导致卸载应用失败。

**可能原因**

1. 文件路径不存在。
2. 加载配置文件数据失败。
3. 文件权限不是可写的。

**处理步骤**

1. 重启手机后再次尝试卸载应用。

2. 重复上述步骤3到5次后依旧卸载失败，请导出日志文件提[在线工单](https://developer.huawei.com/consumer/cn/support/feedback/#/)获取帮助。

```
hdc file recv /data/log/hilog/
```

### 9568386 卸载的应用不存在
**错误信息**

error: uninstall missing installed bundle.

**错误描述**

卸载的应用不存在。

**可能原因**

要卸载的应用没有安装。

**处理步骤**

1. 确认要卸载的应用是否已经安装。

### 9568388 企业设备管理不允许卸载该应用
**错误信息**

error: Failed to uninstall the HAP because the uninstall is forbidden by enterprise device management.

**错误描述**

企业设备管理不允许卸载该应用。

**可能原因**

应用被设置为不允许被卸载。

**处理步骤**

1. 由设置方取消该应用的卸载管控。

### 9568284 安装版本不匹配
**错误信息**

error: install version not compatible.

**错误描述**

安装版本不匹配。

**可能原因**

当前安装HSP的版本信息与已安装HAP的版本信息不匹配。
安装HSP时会做如下校验：
1. bundleName和HAP的一致。
2. version和HAP的一致。
3. 签名和HAP的一致。

**处理步骤**

1. 卸载版本信息不匹配的HAP，再安装HSP。
2. 修改HSP版本信息与HAP一致，再安装HSP。

### 9568287 安装包entry模块数量不合规
**错误信息**

error: install invalid number of entry hap.

**错误描述**

安装包entry模块数量不合规。

**可能原因**

安装包中entry模块有多个。一个应用只能有一个entry模块，可以有多个feature模块。

**处理步骤**

1. 保留一个entry模块，其余entry模块修改为feature（修改module.json5中type字段）。


### 9568281 安装包vendor不一致
**错误信息**

error: install vendor not same.

**错误描述**

安装包vendor不一致。

**可能原因**

app.json5文件中app的vendor字段配置不一致。

**处理步骤**

1. 若只有一个HAP，要求与已安装应用vendor字段一致，卸载重装即可。
2. 若包含集成态HSP，要求集成态HSP与使用方HAP的vendor字段保持一致。


### 9568274 安装服务错误
**错误信息**

error: install installd service error.

**错误描述**

安装服务错误。

**可能原因**

安装服务异常。

**处理步骤**

1. 清除缓存，重启设备。


### 9568314 安装应用间共享库失败
**错误信息**

error: Failed to install the HSP because installing a shared bundle specified by hapFilePaths is not allowed.

**错误描述**

安装应用间共享库失败。

**可能原因**

安装应用间共享HSP时使用“hdc app install ***”指令。

**处理步骤**

1. 安装应用间HSP时使用“hdc install -s ***”指令。


### 9568359 安装设置selinux失败
**错误信息**

error: installd set selinux label failed.

**错误描述**

安装设置selinux失败。

**可能原因**

签名配置文件中APL字段错误。APL有“normal”、“system_basic”和“system_core”三种等级。

**处理步骤**

1. 确认签名文件p7b中apl字段是否有误。

    ![示例图](figures/zh-cn_image_9568359.png)

2. 若apl字段有误，修改UnsgnedReleasedProfileTemplate.json文件中apl字段，并重新签名。

    ![示例图](figures/zh-cn_image_9568359_2.png)


### 9568403 安装加密校验失败
**错误信息**

error: check encryption failed.

**错误描述**

安装加密校验失败。

**可能原因**

可能是镜像版本较老；或者HAP包lib目录内非so文件导致。

**处理步骤**

1. 安装新版本镜像。
2. 删除HAP工程中lib目录内非so文件，重新签名打包。

### 9568413 应用设备类型不支持当前设备

**错误信息**

error: check syscap filed and device type is not supported.

**错误描述**

应用配置的[设备类型](../quick-start/module-configuration-file.md#devicetypes标签)不支持安装。

**可能原因**

应用配置的[设备类型](../quick-start/module-configuration-file.md#devicetypes标签)和安装设备不一致。

**处理步骤**

调整正确的[设备类型](../quick-start/module-configuration-file.md#devicetypes标签)。

### 9568417 签名校验失败
**错误信息**

error: bundle cannot be installed because the appId is not same with preinstalled bundle.

**错误描述**

签名校验失败。

**可能原因**

安装的应用与已经预置的同包名应用签名不一致。

**处理步骤**

1. 如果安装的应用是预置应用，需要保证安装应用的签名与预置应用的一致。

### 9568278 安装包的版本号不一致
**错误信息**

error: install version code not same.

**可能原因**
1. 设备上安装的应用和安装报错的应用包版本号（versionCode）不一致。
2. 安装多个包中存在版本号（versionCode）不一致。

**处理步骤**
1. 调整安装包的版本和设备中已存在的应用包的版本号（versionCode）一致，或者卸载设备中的应用，再去安装新的应用包。
2. 调整安装的多个包的版本号（versionCode），所有的包都需要保持版本号（versionCode）一致。

### 9568380 卸载系统应用失败
**错误信息**

error: uninstall system app error.

**错误描述**

卸载系统应用失败。

**可能原因**

部分系统应用设置为不可卸载，不支持卸载此类应用。

**处理步骤**

不能卸载不可卸载的应用。

### 9568387 卸载未安装的模块，导致卸载失败
**错误信息**

error: uninstall missing installed module.

**错误描述**

卸载未安装的模块。

**可能原因**

卸载未安装的模块。

**处理步骤**

使用[bm dump -n](#查询应用信息命令dump)命令查看应用配置，确认要卸载的模块已经安装。