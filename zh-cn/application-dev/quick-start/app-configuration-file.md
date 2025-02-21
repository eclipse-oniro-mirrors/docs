# app.json5配置文件

## 配置文件示例


先通过一个示例，整体认识一下app.json5配置文件。

```json
{
  "app": {
    "bundleName": "com.application.myapplication",
    "vendor": "example",
    "versionCode": 1000000,
    "versionName": "1.0.0",
    "icon": "$media:app_icon",
    "label": "$string:app_name",
    "description": "$string:description_application",
    "minAPIVersion": 9,
    "targetAPIVersion": 9,
    "apiReleaseType": "Release",
    "debug": false,
    "car": {
      "minAPIVersion": 8
    },
    "targetBundleName": "com.application.test",
    "targetPriority": 50
  },
}
```
## 配置文件标签

app.json5配置文件包含以下标签。


  **表1** app.json5配置文件标签说明

| 属性名称 | 含义 | 数据类型 | 是否可缺省 |
| -------- | -------- | -------- | -------- |
| bundleName | 标识应用的Bundle名称，用于标识应用的唯一性。命名规则如下&nbsp;：<br/>-&nbsp;由字母、数字、下划线和符号“.”组成，且必须以字母开头。<br/>-&nbsp;字符串最小长度为7字节，最大长度128字节。<br/>-&nbsp;推荐采用反域名形式命名（如“com.example.demo”，建议第一级为域名后缀com，第二级为厂商/个人名，第三级为应用名，也可以多级）。<br/>对于随系统源码编译的应用，建议命名为“com.ohos.demo”形式，其中的ohos标识系统应用。 | 字符串 | 该标签不可缺省。 |
| bundleType| 标识应用的Bundle类型，用于区分应用或者元服务。支持的取值如下：<br/>-&nbsp;app：当前Bundle为应用。<br/>-&nbsp;atomicService：当前Bundle为元服务。<br/>-&nbsp;shared：当前Bundle为共享库应用，预留字段。<br/>-&nbsp;appService：当前Bundle为系统级共享库应用，仅供系统应用使用。 | 字符串| 该标签可缺省，缺省值为app。 |
| debug | 标识应用是否可调试。<br/>-&nbsp;true：可调试。<br/>-&nbsp;false：不可调试。 | 布尔值 | 由IDE编译构建时生成。该标签可缺省，缺省值为false。 |
| icon | 标识[应用的图标](../application-models/application-component-configuration-stage.md)，取值为图标资源文件的索引。 | 字符串 | 该标签不可缺省。 |
| label | 标识[应用的名称](../application-models/application-component-configuration-stage.md)，取值为字符串资源的索引，字符串长度不超过63字节。 | 字符串 | 该标签不可缺省。 |
| description | 标识应用的描述信息。取值为长度不超过255字节的字符串，内容为描述信息的字符串资源索引。 | 字符串 | 该标签可缺省，缺省值为空。 |
| vendor | 标识对应用开发厂商的描述，取值为长度不超过255字节的字符串。 | 字符串 | 该标签可缺省，缺省值为空。 |
| versionCode | 标识应用的版本号，取值为小于2^31次方的正整数。此数字仅用于确定某个版本是否比另一个版本更新，数值越大表示版本越高。<br/>开发者可以将该值设置为任何正整数，但是必须确保应用的新版本都使用比旧版本更大的值。 | 数值 | 该标签不可缺省。 |
| versionName | 标识向用户展示的应用版本号。<br/>取值为长度不超过127字节的字符串，仅由数字和点构成，推荐采用“A.B.C.D”四段式的形式。四段式推荐的含义如下所示。<br/>第一段：主版本号/Major，范围0\~99，重大修改的版本，如实现新的大功能或重大变化。<br/>第二段：次版本号/Minor，范围0\~99，表示实现较突出的特点，如新功能添加或大问题修复。<br/>第三段：特性版本号/Feature，范围0\~99，标识规划的新版本特性。<br/>第四段：修订版本号/Patch，范围0\~999，表示维护版本，如修复bug。 | 字符串 | 该标签不可缺省。 |
| minCompatibleVersionCode | 标识应用能够兼容的最低历史版本号，用于应用跨设备兼容性判断。取值范围为0~2147483647。 | 数值 | 该标签可缺省，缺省值等于versionCode标签值。 |
| minAPIVersion | 标识应用运行需要的SDK的API最小版本。取值范围为0~2147483647。 | 数值 | 应用编译构建时由build-profile.json5中的compatibleSdkVersion自动生成。 |
| targetAPIVersion | 标识应用运行需要的API目标版本。取值范围为0~2147483647。 | 数值 | 应用编译构建时由build-profile.json5中的compileSdkVersion自动生成。 |
| apiReleaseType | 标识应用运行需要的API目标版本的类型，采用字符串类型表示。取值为“CanaryN”、“BetaN”或者“Release”，其中，N代表大于零的整数。<br/>-&nbsp;Canary：受限发布的版本。<br/>-&nbsp;Beta：公开发布的Beta版本。<br/>-&nbsp;Release：公开发布的正式版本。 | 字符串 | 应用编译构建时根据当前使用的SDK的Stage自动生成。即便手动配置了取值，编译构建时也会被覆盖。 |
| accessible | 标识应用是否能访问应用的安装目录，仅针对Stage模型的系统应用和预置应用生效。 | 布尔值 | 该标签可缺省，缺省值为false。 |
| multiProjects | 标识当前工程是否支持多个工程的联合开发。<br/>-&nbsp;true：当前工程支持多个工程的联合开发。多工程开发可参考[多工程构建](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/build_overview-0000001055075201-V3#section73401914284)。<br/>-&nbsp;false：当前工程不支持多个工程的联合开发。 | 布尔值 | 该标签可缺省，缺省值为false。 |
| asanEnabled | 标识应用程序是否开启asan检测，用于辅助定位buffer越界造成的crash问题。<br/>-&nbsp;true：当前工程开启asan检测。<br/>-&nbsp;false：当前工程不开启asan检测。Release版本不支持开启asan检测。 | 布尔值 | 该标签可缺省，缺省值为false。 |
| tablet | 标识对tablet设备做的特殊配置，可以配置的属性字段有上文提到的：minAPIVersion。<br/>如果使用该属性对tablet设备做了特殊配置，则应用在tablet设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。 | 对象 | 该标签可缺省，缺省时tablet设备使用app.json5公共区域配置的属性值。 |
| tv | 标识对tv设备做的特殊配置，可以配置的属性字段有上文提到的：minAPIVersion。<br/>如果使用该属性对tv设备做了特殊配置，则应用在tv设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。 | 对象 | 该标签可缺省，缺省时tv设备使用app.json5公共区域配置的属性值。 |
| wearable | 标识对wearable设备做的特殊配置，可以配置的属性字段有上文提到的：minAPIVersion。<br/>如果使用该属性对wearable设备做了特殊配置，则应用在wearable设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。 | 对象 | 该标签可缺省，缺省时wearable设备使用app.json5公共区域配置的属性值。 |
| car | 标识对car设备做的特殊配置，可以配置的属性字段有上文提到的：minAPIVersion。<br/>如果使用该属性对car设备做了特殊配置，则应用在car设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。 | 对象 | 该标签可缺省，缺省时car设备使用app.json5公共区域配置的属性值。 |
| default | 标识对default设备做的特殊配置，可以配置的属性字段有上文提到的：minAPIVersion。<br/>如果使用该属性对default设备做了特殊配置，则应用在default设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。 | 对象 | 该标签可缺省，缺省时default设备使用app.json5公共区域配置的属性值。 |
|targetBundleName|标识当前包所指定的目标应用, 标签值的取值规则和范围与bundleName标签一致。配置该字段的应用为具有overlay特征的应用。|字符串|该标签可缺省，缺省值为空。|
|targetPriority|标识当前应用的优先级，取值范围为1~100。配置targetBundleName字段之后，才支持配置该字段。|数值|该标签可缺省, 缺省值为1。|
|generateBuildHash |标识当前应用的所有HAP和HSP是否由打包工具生成哈希值。<br/>该字段配置为true时，该应用下的所有HAP和HSP都会由打包工具生成对应的哈希值。系统OTA升级时，若应用的versionCode保持不变，可根据哈希值判断应用是否需要升级。<br/>**说明：** <br/>该字段仅对预置应用生效。|布尔值|该标签可缺省, 缺省值为false。|
| GWPAsanEnabled | 标识应用程序是否开启GWP-asan堆内存检测工具，用于对内存越界、内存释放后使用等内存破坏问题进行分析。<br/>-&nbsp;true：当前工程开启GWP-asan检测。<br/>-&nbsp;false：当前工程不开启GWP-asan检测。 | 布尔值 | 该标签可缺省, 缺省值为false。 |

