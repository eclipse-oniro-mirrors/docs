# app.json5 Configuration File

## Configuration File Example


This topic gives an overview of the **app.json5** configuration file. To start with, let's go through an example of what this file contains.

```json
{
  "app": {
    "bundleName": "com.application.myapplication",
    "vendor": "example",
    "versionCode": 1000000,
    "versionName": "1.0.0",
    "icon": "$media:layered-image",
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
    "targetPriority": 50,
    "appEnvironments": [
      {
        "name":"name1",
        "value": "value1"
      }
    ],
    "maxChildProcess": 5,
    "multiAppMode": {
      "multiAppModeType": "multiInstance",
      "maxCount": 5
    },
    "cloudFileSyncEnabled": false,
    "configuration": "$profile:configuration"
  },
}
```
## Tags in the Configuration File

As shown above, the **app.json5** file contains several tags.


**Table 1** Tags in the app.json5 file

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| bundleName | Bundle name, which uniquely identifies an application. The value must comply with the following rules:<br>- Starts with a letter and consists of letters, digits, underscores (_), and periods (.).<br>- Contains 7 to 128 bytes.<br>You are advised to use the reverse domain name notation, for example, *com.example.demo*, where the first part is the domain suffix **com**, the second part is the vendor/individual name, and the third part is the application name, which can be of multiple levels.<br>If an application is built with the system source code, you are advised to name it in *com.ohos.demo* notation, where **ohos** signifies that the application is a system application.| String| No|
| bundleType| Bundle type, which is used to distinguish applications and atomic services. The options are as follows:<br>- **app**: The bundle is an application.<br>- **atomicService**: The bundle is an atomic service.<br>- **shared**: The bundle is a shared library. This option is reserved.<br>- **appService**: The bundle is a system-level shared library and can be used only by system applications.| String| Yes (initial value: **app**)|
| debug | Whether the application can be debugged.<br>-&nbsp;**true**: Can be debugged. Used in the development phase.<br>-&nbsp;**false**: Cannot be debugged. Used in the release phase.| Boolean| Yes (initial value: **false**; it is generated during compilation and building in DevEco Studio.)  |
| [icon](#icon)| [Icon of the application](../application-models/application-component-configuration-stage.md). The value is the index to an icon resource file.| String| No|
| label | [Name of the application](../application-models/application-component-configuration-stage.md). The value is the index to a string resource. It is a string with a maximum of 63 bytes.| String| No|
| description | Description of the application. The value is the index to a description. It is a string with a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| vendor | Vendor of the application. The value is a string with a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| versionCode | Version code of the application. The value is a positive integer less than 2 to the power of 31. It is used only to determine whether a version is later than another version. A larger value indicates a later version.<br>Ensure that a new version of the application uses a value greater than any of its predecessors.| Number| No|
| versionName | Version number of the application displayed to users.<br>The value contains a maximum of 127 bytes and consists of only digits and dots. The four-part format *A.B.C.D* is recommended, wherein:<br>Part 1 (*A*): major version number, which ranges from 0 to 99. A major version consists of major new features or large changes.<br>Part 2 (*B*): minor version number, which ranges from 0 to 99. A minor version consists of some new features or large bug fixes.<br>Part 3 (*C*): feature version number, which ranges from 0 to 99. A feature version consists of scheduled new features.<br>Part 4 (*D*): maintenance release number or patch number, which ranges from 0 to 999. A maintenance release or patch consists of resolution to security flaws or minor bugs.| String| No|
| minCompatibleVersionCode | Minimum compatible version of the application. It is used to check whether the application is compatible with a version on other devices in the cross-device scenario. The value ranges from 0 to 2147483647.| Number| Yes (initial value: value of **versionCode**)|
| minAPIVersion | Minimum API version required for running the application. The value ranges from 0 to 2147483647.| Number| Yes (initial value: value of **compatibleSdkVersion** in **build-profile.json5**)|
| targetAPIVersion | Target API version required for running the application. The value ranges from 0 to 2147483647.| Number| Yes (initial value: value of **compileSdkVersion** in **build-profile.json5**)|
| apiReleaseType | Type of the target API version required for running the application. The value can be **"CanaryN"**, **"BetaN"**, or **"Release"**, where **N** represents a positive integer.<br>- **Canary**: indicates a restricted release.<br>- **Beta**: indicates a publicly released beta version.<br>- **Release**: indicates a publicly released official version.| String| Yes (the value is automatically set by DevEco Studio based on the stage of the SDK in use; a manually set value will be overwritten during compilation and building)|
| accessible | Whether the installation directory of the application is accessible. This tag is effective only for system applications and pre-installed applications in the stage model.| Boolean| Yes (initial value: **false**)|
| multiProjects | Whether the application supports joint development of multiple projects.<br>- **true**: The application supports joint development of multiple projects. For details about multi-project development, see <!--RP1-->[Implementing Multi-Project Builds](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-hvigor-multi-projects-V5)<!--RP1End-->.<br>- **false**: The application does not support joint development of multiple projects.| Boolean| Yes (initial value: **false**)|
| asanEnabled | Whether to enable AddressSanitizer (ASan) to detect memory corruption issues such as buffer overflows.<br>- **true**: ASan is enabled.<br>- **false**: ASan is disabled.| Boolean| Yes (initial value: **false**)|
| tablet | Tablet-specific configuration, which includes the **minAPIVersion** attribute.<br>When running on tablets, the application applies the attribute settings under this tag and ignores the general settings in the **app.json5** file.| Object| Yes (initial value: general settings in the **app.json5** file)|
| tv | TV-specific configuration, which includes the **minAPIVersion** attribute.<br>When running on TVs, the application applies the attribute settings under this tag and ignores the general settings in the **app.json5** file.| Object| Yes (initial value: general settings in the **app.json5** file)|
| wearable | Wearable-specific configuration, which includes the **minAPIVersion** attribute.<br>When running on wearables, the application applies the attribute settings under this tag and ignores the general settings in the **app.json5** file.| Object| Yes (initial value: general settings in the **app.json5** file)|
| car | Telematics–specific configuration, which includes the **minAPIVersion** attribute. <br>When running on telematics devices, the application applies the attribute settings under this tag and ignores the general settings in the **app.json5** file.| Object| Yes (initial value: general settings in the **app.json5** file)|
| default | Default device–specific configuration, which includes the **minAPIVersion** attribute.<br>When running on default devices, the application applies the attribute settings under this tag and ignores the general settings in the **app.json5** file.| Object| Yes (initial value: general settings in the **app.json5** file)|
|targetBundleName|Target bundle name. The value rule and range are the same as those of **bundleName**. When a value is specified, the target application becomes one with the overlay feature.|String|Yes (initial value: left empty)|
|targetPriority|Priority of the application. The value ranges from 1 to 100. This tag can be configured only when **targetBundleName** is configured.|Number|Yes (initial value: **1**)|
|generateBuildHash |Whether to generate hash values for all HAP and HSP files of the application by using the packaging tool.<br>If this tag is set to **true**, the packaging tool generates hash values for all HAP and HSP files of the application. The hash values (if any) are used to determine whether the application needs to be updated when the system is updated in OTA mode but the **versionCode** value of the application remains unchanged.<br>**NOTE**<br>This tag applies only to system applications.|Boolean|Yes (initial value: **false**)|
| GWPAsanEnabled | Whether to enable GWP-ASan to detect memory safety errors, such as use-after-free and out-of-bounds memory read/write.<br>- **true**: GWP-ASan is enabled.<br>- **false**: GWP-ASan is disabled.| Boolean| Yes (initial value: **false**)|
| [appEnvironments](#appenvironments) | Application environment variables configured for the current module.| Object array| Yes (initial value: left empty)|
| maxChildProcess | Maximum number of child processes that can be created by the current application. The value ranges from 0 to 512. The value **0** indicates that the number is not limited. If the application has multiple modules, use the configuration of the **entry** module.| Number| Yes (initial value: preconfigured value)|
| [multiAppMode](#multiappmode)| Multi-app mode of the application. This tag takes effect only for the entry or feature module of the application whose **bundleType** is **app**. If there are multiple modules, use the configuration of the **entry** module.| Object| Yes (initial value: left empty)|
| cloudFileSyncEnabled | Whether device-cloud file synchronization is enabled for the application.<br>-&nbsp;**true**: The device-cloud file synchronization is enabled.<br>-&nbsp;**false**: The device-cloud file synchronization is disabled.| Boolean| Yes (initial value: **false**) |
| [configuration](#configuration)| Whether the font size of the current application follows the system.<br>This tag is a **profile** file resource that used to specify the configuration file that describes the application font size changes with the system.| String| Yes (initial value: by default)|

## icon

The **icon** tag represents the [application icons](../application-models/application-component-configuration-stage.md) and the index to the layered icon configuration files.

Layered icons can be configured as follows:

1. Place the foreground and background resources of the icon in the **AppScope/resources/base/media** directory.

2. Create a JSON file (for example, **layered-image.json**) in the **media** directory and reference the foreground and background resources in the file. For details, see [Icon Resource Specifications](https://developer.huawei.com/consumer/en/doc/design-guides/application-icon-0000001953444009#section634668113212).

Example of the layered icon resource file:

```json
{
  "layered-image":
    {
      "background":"$media:background," // Background resource
      "foreground":"$media:foreground" // Foreground resource
    }    
}
```

Example of the **icon** structure:

```json
{
  "app":{
    "icon":"$media:layered-image"
  }
}
```

## appEnvironments

The **appEnvironments** tag represents the application environment variables.

**Table 2** appEnvironments

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name          | Name of the environment variable. The value is a string with a maximum of 4096 bytes.| String | Yes (initial value: left empty)|
| value         | Value of the environment variable. The value is a string with a maximum of 4096 bytes.      | String | Yes (initial value: left empty)|

Example of the **appEnvironments** structure:

```json
{
  "app": {
    "appEnvironments": [
      {
        "name":"name1",
        "value": "value1"
      }
    ]
  }
}
```

## multiAppMode

The **multiAppMode** tag represents the multi-app mode of the application.

**Table 3** multiAppMode

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| multiAppModeType          | Multi-open mode. The options are as follows:<br>- **multiInstance**: multi-instance mode. Only 2-in-1 devices are supported.<br>- **appClone**: app clone mode.| String | No|
| maxCount         | Maximum number of applications that can be opened. The options are as follows:<br>- In **multiInstance** mode, the value ranges from 1 to 10.<br>- In **appClone** mode, the value ranges from 1 to 5.     | Number | No|

Example of the **multiAppMode** structure:

```json
{
  "app": {
    "multiAppMode": {
      "multiAppModeType": "appClone",
      "maxCount": 5
    }
  }
}
```

## configuration

This tag is a **profile** file resource that used to specify the configuration file that describes the application font size changes with the system.

Example of the **configuration** structure:

```json
{
  "app": {
    "configuration": "$profile:configuration"  
  }
}
```

Define the **configuration.json** file under **resources/base/profile** in the development view. The file name (**configuration** in this example) can be customized, but must be consistent with the information specified by the **configuration** tag. The file lists the attributes that enable the application font size to change with the system.

**Table 4** configuration

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| fontSizeScale | Settings of the application font size. The options are as follows:<br>- followSystem: The font size follows the system.<br>- FollowSystem: The font size does not follow the system.| String| Yes (initial value: **followSystem**)|
| fontSizeMaxScale | Maximum ratio of the application font size after the font size is set to follow the system. The options are as follows: 1, 1.15, 1.3, 1.45, 1.75, 2, and 3.2.	 <br> If **fontSizeScale** is set to **nonFollowSystem**, this attribute does not take effect.| String| Yes (initial value: **3.2**)|

resources/base/profile/configuration.json

```json
{
  "configuration": {
    "fontSizeScale": "followSystem",
    "fontSizeMaxScale": "3.2"
  }
}
```
