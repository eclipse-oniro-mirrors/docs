# module.json5 Configuration File

## Configuration File Example

This topic gives an overview of the **module.json5** configuration file. To start with, let's go through an example of what this file contains.

```json
{
  "module": {
    "name": "entry",
    "type": "entry",
    "description": "$string:module_desc",
    "mainElement": "EntryAbility",
    "deviceTypes": [
      "default",
      "tablet"
    ],
    "deliveryWithInstall": true,
    "installationFree": false,
    "pages": "$profile:main_pages",
    "virtualMachine": "ark",
    "metadata": [
      {
        "name": "string",
        "value": "string",
        "resource": "$profile:distributionFilter_config"
      }
    ],
    "abilities": [
      {
        "name": "EntryAbility",
        "srcEntry": "./ets/entryability/EntryAbility.ets",
        "description": "$string:EntryAbility_desc",
        "icon": "$media:icon",
        "label": "$string:EntryAbility_label",
        "startWindowIcon": "$media:icon",
        "startWindowBackground": "$color:start_window_background",
        "exported": true,
        "skills": [
          {
            "entities": [
              "entity.system.home"
            ],
            "actions": [
              "ohos.want.action.home"
            ]
          }
        ]
      }
    ],
    "definePermissions": [
      {
        "name": "ohos.abilitydemo.permission.PROVIDER",
        "grantMode": "system_grant",
        "availableLevel": "system_core",
        "provisionEnable": true,
        "distributedSceneEnable": false,
        "label": "$string:EntryAbility_label"
      }
    ],
    "requestPermissions": [
      {
        "name": "ohos.abilitydemo.permission.PROVIDER",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "FormAbility"
          ],
          "when": "inuse"
        }
      }
    ],
    "targetModuleName": "feature",
    "targetPriority": 50,
    "querySchemes": [
      "app1Scheme",
      "app2Scheme"
    ]
  }
}
```

## Tags in the Configuration File

As shown above, the **module.json5** file contains several tags.


  **Table 1** Tags in the module.json5 file

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the module. This name must be unique in the entire application. The value is a string with a maximum of 31 bytes.<br>This name can be changed during application updates. However, if it is changed, directories related to the module must be migrated. You can use the [file operation API](../reference/apis-core-file-kit/js-apis-file-fs.md#fscopydir10) for migration.| String| No|
| type | Type of the module. The options are as follows:<br>- **entry**: main module of the application.<br>- **feature**: feature module of the application.<br>- **har**: static shared module.<br>- **shared**: dynamic shared module.| String| No|
| srcEntry | Code path of the module. The value is a string with a maximum of 127 bytes.| String| Yes (initial value: left empty)|
| description | Description of the module. The value is a string with a maximum of 255 bytes. It can be a resource reference.| String| Yes (initial value: left empty)|
| process | Process name of the module. The value is a string with a maximum of 31 bytes. If **process** is configured under **HAP**, all UIAbilities, DataShareExtensionAbilities, and ServiceExtensionAbilities of the application will run in the specified process.<br>**NOTE**<br>This tag applies only to system applications and does not take effect for third-party applications.| String| Yes (initial value: value of **bundleName** under **app** in the **app.json5** file)|
| mainElement | Name of the entry UIAbility or ExtensionAbility of the module. The value is a string with a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| [deviceTypes](#devicetypes) | Types of the devices on which the module can run.| String array| No|
| deliveryWithInstall | Whether the HAP of the module is installed together with the application.<br>- **true**: The HAP of the module is installed together with the application.<br>- **false**: The HAP of the module is not installed together with the application.| Boolean| No|
| installationFree | Whether the module supports the installation-free feature.<br>- **true**: The module supports the installation-free feature and meets installation-free constraints.<br>- **false**: The module does not support the installation-free feature.<br>**NOTE**<br>If [bundleType](./app-configuration-file.md#tags-in-the-configuration-file) is set to **atomicService**, set this tag to **true**. Otherwise, set this tag to <b class="+ topic/ph hi-d/b " id="b1842016483597">false</b>.| Boolean| No|
| virtualMachine | Type of the target virtual machine (VM) where the module can run. It is used for cloud distribution, such as distribution by the application market and distribution center. If the target VM type is ArkTS engine, the value is **ark**+*version number*.| String| Yes (initial value: automatically inserted when DevEco Studio builds the HAP file)|
| [pages](#pages)| Profile that represents information about each page in the module. The value is a string with a maximum of 255 bytes.| String| No in the UIAbility scenario|
| [metadata](#metadata)| Custom metadata of the module. You can configure [distributionFilter](#distributionfilter) and [shortcuts](#shortcuts) by referencing resources. The setting is effective only for the current module, UIAbility, and ExtensionAbility.| Object array| Yes (initial value: left empty)|
| [abilities](#abilities) | UIAbility configuration of the module. The setting is effective only for the current UIAbility.| Object array| Yes (initial value: left empty)|
| [extensionAbilities](#extensionabilities) | ExtensionAbility configuration of the module. The setting is effective only for the current ExtensionAbility.| Object array| Yes (initial value: left empty)|
| [definePermissions](#definepermissions) | Permissions defined for the system resource HAP. Custom permissions are not supported.| Object array| Yes (initial value: left empty)|
| [requestPermissions](#requestpermissions) | A set of permissions that the application needs to request from the system for running correctly.| Object array| Yes (initial value: left empty)|
| [testRunner](#testrunner) | Test runner of the module.| Object| Yes (initial value: left empty)|
| [atomicService](#atomicservice)| Atomic service configuration.| Object| Yes (initial value: left empty) |
| [dependencies](#dependencies)| List of shared libraries on which the module depends during running.| Object array| Yes (initial value: left empty) |
| targetModuleName | Target module name of the bundle. This name must be unique in the entire application. The value is a string with a maximum of 31 bytes. The module that has this tag set provides the overlay feature. This tag is applicable only to HSPs.|String|Yes (initial value: left empty)|
| targetPriority | Priority of the module. The value ranges from 1 to 100. This tag is required only when **targetModuleName** is set. This tag is applicable only to HSPs.|Integer|Yes (initial value: **1**)|
| [proxyData](#proxydata) | List of data proxies provided by the module.| Object array| Yes (initial value: left empty)|
| isolationMode | Multi-process configuration of the module. The options are as follows:<br>- **nonisolationFirst**: The module preferentially runs in a non-independent process.<br>- **isolationFirst**: The module preferentially runs in an independent process.<br>- **isolationOnly**: The module runs only in an independent process.<br>- **nonisolationOnly**: The module runs only in a non-independent process.|String|Yes (initial value: **nonisolationFirst**)|
| generateBuildHash |Whether the hash value of the HAP or HSP is generated by the packing tool. The hash value (if any) is used to determine whether the application needs to be updated when the system is updated in OTA mode but the **versionCode** value of the application remains unchanged.<br>This tag is enabled only when the **generateBuildHash** tag in the [app.json5](./app-configuration-file.md) file is **false**.<br>**NOTE**<br>This tag applies only to system applications.|Boolean|Yes (initial value: **false**)|
| compressNativeLibs | Whether the **libs** libraries are packaged in the HAP file after being compressed.<br>- **true**: The **libs** libraries are packaged in the HAP file after being compressed.<br>- **false**: The **libs** libraries are stored without being compressed.| Boolean| Yes (initial value: **false**)|
| libIsolation | Whether to save the .so files of the current HAP to a separate folder. This is intended to avoid .so file conflicts between HAPs.<br>- **true**: The .so files of the current HAP are stored in a separate folder (named after the module) in the **libs** directory.<br>- **false**: The .so files of the current HAP are directly stored in the **libs** directory.| Boolean| Yes (initial value: **false**)|
| fileContextMenu | Context menu of the current HAP. The value is a string with a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| querySchemes | URL schemes that the current application can query for redirection. This tag is only available for entry modules. A maximum of 50 URL schemes can be configured, with each containing a maximum of 128 bytes.| String array| Yes (initial value: left empty)|

## deviceTypes

  **Table 2** deviceTypes

| Device Type| Value| Description|
| -------- | -------- | -------- |
| Tablet| tablet | - |
| Smart TV| tv | - |
| Smart watch| wearable | Watch that provides call features.|
| Head unit| car | - |
| Default device| default | Device that provides full access to system capabilities.|

Example of the **deviceTypes** structure:


```json
{
  "module": {
    "name": "myHapName",
    "type": "feature",
    "deviceTypes" : [
       "tablet"
    ]
  }
}
```


## pages

The **pages** tag is a profile that represents information about specified pages.


```json
{
  "module": {
    // ...
    "pages": "$profile:main_pages", // Configured through the resource file in the profile
  }
}
```

Define the **main_pages.json** file under **resources/base/profile** in the development view. The file name (**main_pages** in this example) can be customized, but must be consistent with the information specified by the **pages** tag. The file lists the page information of the current application, including the route information and the window-related configuration.

  **Table 3** pages

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| src | Route information about all pages in the module, including the page path and page name. The page path is relative to the **src/main/ets** directory of the current module. The value is a string array, each element of which represents a page.| String array| No|
| window | Window-related configuration.	 | Object| Yes (initial value: left empty)|


  **Table 4** window

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| designWidth | Baseline width for page design. The size of an element is scaled by the actual device width.| Number| Yes (initial value: **720px**)|
| autoDesignWidth | Whether to automatically calculate the baseline width for page design. If it is set to **true**, the **designWidth** attribute becomes invalid. The baseline width is calculated based on the device width and screen density.| Boolean| Yes (initial value: **false**)|

```json
{
  "src": [
    "pages/index/mainPage",
    "pages/second/payment",
    "pages/third/shopping_cart",
    "pages/four/owner"
  ],
  "window": {
    "designWidth": 720,
    "autoDesignWidth": false
  }
}
```


## metadata

The **metadata** tag represents the custom metadata of the HAP. The tag value is an array and contains three subtags: **name**, **value**, and **resource**.

**Table 5** metadata

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the data item. The value is a string with a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| value | Value of the data item. The value is a string with a maximum of 255 bytes.| String| Yes (initial value: left empty)|
| resource | Custom data format. The value is a resource index. It contains a maximum of 255 bytes.| String| Yes (initial value: left empty)|

The value of **resource** is in the format of $profile:file name, where **$profile** indicates that the resource is placed under **/resources/base/profile** in the project directory. For example, **$profile:shortcuts_config** indicates the **/resources/base/profile/shortcuts_config.json** file.

```json
{
  "module": {
    "metadata": [{
      "name": "module_metadata",
      "value": "a test demo for module metadata",
      "resource": "$profile:shortcuts_config"
    }],

    "abilities": [{
      "metadata": [{
        "name": "ability_metadata",
        "value": "a test demo for ability",
        "resource": "$profile:config_file"
      },
      {
        "name": "ability_metadata_2",
        "value": "a string test",
        "resource": "$profile:config_file"
      }],
    }],

    "extensionAbilities": [{
      "metadata": [{
        "name": "extensionAbility_metadata",
        "value": "a test for extensionAbility",
        "resource": "$profile:config_file"
      },
      {
        "name": "extensionAbility_metadata_2",
        "value": "a string test",
        "resource": "$profile:config_file"
      }],
    }]
  }
}
```


## abilities

The **abilities** tag represents the UIAbility configuration of the module, which is valid only for the current UIAbility component.

  **Table 6** abilities

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the UIAbility. This name must be unique in the entire application. The value is a string with a maximum of 127 bytes.| String| No|
| srcEntry | Code path of the entry UIAbility. The value is a string with a maximum of 127 bytes.| String| No|
| [launchType](../application-models/uiability-launch-type.md) | Launch type of the UIAbility. The options are as follows:<br>- **multiton**: A UIAbility instance is created each time the UIAbility is started.<br>- **singleton**: A UIAbility instance is created only when the UIAbility is started for the first time.<br>- **specified**: You can determine whether to create a UIAbility instance when the application is running.| String| Yes (initial value: **"singleton"**)|
| description | Description of the UIAbility. The value is a string with a maximum of 255 bytes. It must be a resource index to support multiple languages.| String| Yes (initial value: left empty)|
| icon | Icon of the UIAbility. The value is the index of the icon resource file.| String| Yes (initial value: left empty)<br>If **UIAbility** is set to **MainElement**, this attribute is mandatory.|
| label | Name of the UIAbility displayed to users. The value must be a resource index to support multiple languages. The value is a string with a maximum of 255 bytes.| String| Yes (initial value: left empty)<br>If **UIAbility** is set to **MainElement**, this attribute is mandatory.|
| permissions | Permissions required for another application to access the UIAbility.<br>The value is generally in the reverse domain name notation and contains a maximum of 255 bytes. It is an array of predefined permission names.| String array| Yes (initial value: left empty)|
| [metadata](#metadata)| Metadata information of the UIAbility component.| Object array| Yes (initial value: left empty)|
| exported | Whether the UIAbility can be called by other applications.<br>- **true**: The UIAbility can be called by other applications.<br>- **false**: The UIAbility cannot be called by other applications, not even by aa commands.| Boolean| Yes (initial value: **false**)|
| continuable | Whether the UIAbility can be continued on another device.<br>- **true**: The UIAbility can be continued on another device.<br>- **false**: The UIAbility cannot be continued on another device.| Boolean| Yes (initial value: **false**)|
| [skills](#skills) | A set of [wants](../application-models/want-overview.md) that can be received by the UIAbility or ExtensionAbility.<br>Configuration rules:<br>- For HAPs of the entry type, you can configure multiple **skills** attributes with the entry capability for an application. (A **skills** attribute with the entry capability is the one that has **ohos.want.action.home** and **entity.system.home** configured.)<br>- For HAPs of the feature type, you can configure the **skills** attribute with the entry capability for an application, but not for a service.| Object array| Yes (initial value: left empty)|
| backgroundModes | Continuous tasks of the UIAbility.<br>Continuous tasks are classified into the following types:<br>- **dataTransfer**: data transfer through the network or peer device, such as download, backup, and share<br>- **audioPlayback**: audio playback<br>- **audioRecording**: audio recording<br>- **location**: location and navigation<br>- **bluetoothInteraction**: Bluetooth scanning, connection, and transmission (wearables)<br>- **multiDeviceConnection**: multi-device connection<br>- **wifiInteraction**: Wi-Fi scanning, connection, and transmission (as used in multi-screen collaboration and device clone features)<br>- **voip**: voice and video calls over IP networks<br>- **taskKeeping**: computing| String array| Yes (initial value: left empty)|
| startWindowIcon | Index to the icon file of the UIAbility startup page. The value is a string with a maximum of 255 bytes.| String| No|
| startWindowBackground | Index to the background color resource file of the UIAbility startup page. The value is a string with a maximum of 255 bytes.<br>Example: **$color:red**.| String| No|
| removeMissionAfterTerminate | Whether to remove the relevant mission from the mission list after the UIAbility is destroyed.<br>- **true**: Remove the relevant mission from the mission list after the UIAbility is destroyed.<br>- **false**: Do not remove the relevant mission from the task mission list after the UIAbility is destroyed.| Boolean| Yes (initial value: **false**)|
| orientation | Orientation of the UIAbility when it is started. The options are as follows:<br>- **unspecified**: automatically determined by the system.<br>- **landscape**: landscape mode.<br>- **portrait**: portrait mode.<br>- **landscape_inverted**: inverted landscape mode.<br>- **portrait_inverted**: inverted portrait mode.<br>- **auto_rotation**: determined by the sensor.<br>- **auto_rotation_landscape**: determined by the sensor in the horizontal direction, including landscape and inverted landscape modes.<br>- **auto_rotation_portrait**: determined by the sensor in the vertical direction, including portrait and inverted portrait modes.<br>- **auto_rotation_restricted**: determined by the sensor when the sensor switch is enabled.<br>- **auto_rotation_landscape_restricted**: determined by the sensor in the horizontal direction, including landscape and inverted landscape modes, when the sensor switch is enabled.<br>- **auto_rotation_portrait_restricted**: determined by the sensor in the vertical direction, including portrait and inverted portrait modes, when the sensor switch is enabled.<br>- **locked**: auto rotation disabled.<br>- **auto_rotation_unspecified**: auto rotation controlled by the switch and determined by the system.<br>- **follow_desktop**: following the orientation of the home screen. | String| Yes (initial value: **"unspecified"**)|
| supportWindowMode | Window mode supported by the UIAbility. The options are as follows:<br>- **fullscreen**: full-screen mode.<br>- **split**: split-screen mode.<br>- **floating**: floating window mode.| String array| Yes (initial value:<br>["fullscreen", "split", "floating"])|
| priority | Priority of the UIAbility component. In the case of [implicit query](../application-models/explicit-implicit-want-mappings.md), UIAbility components with a higher priority are at the higher place of the returned list. The value ranges from 0 to 10. The greater the value, the higher the priority.<br>**NOTE**<br>This tag applies only to system applications and does not take effect for third-party applications.| Integer| Yes (initial value: **0**)|
| maxWindowRatio | Maximum aspect ratio supported by the UIAbility component. The minimum value is 0.| Number| Yes (initial value: maximum aspect ratio supported by the platform)|
| minWindowRatio | Minimum aspect ratio supported by the UIAbility component. The minimum value is 0.| Number| Yes (initial value: minimum aspect ratio supported by the platform)|
| maxWindowWidth | Maximum window width supported by the UIAbility, in vp.<br>The value cannot be less than the value of **minWindowWidth** or greater than the maximum window width allowed by the platform. For details about the window size, see [Constraints](../windowmanager/window-overview.md#constraints).| Number| Yes (initial value: maximum window width supported by the platform)|
| minWindowWidth | Minimum window width supported by the UIAbility, in vp.<br>The value cannot be less than the minimum window width allowed by the platform or greater than the value of **maxWindowWidth**. For details about the window size, see [Constraints](../windowmanager/window-overview.md#constraints).| Number| Yes (initial value: minimum window width supported by the platform)|
| maxWindowHeight | Maximum window height supported by the UIAbility, in vp.<br>The value cannot be less than the value of **minWindowHeight** or greater than the maximum window height allowed by the platform. For details about the window size, see [Constraints](../windowmanager/window-overview.md#constraints).| Number| Yes (initial value: maximum window height supported by the platform)|
| minWindowHeight | Minimum window height supported by the UIAbility, in vp.<br>The value cannot be less than the minimum window height allowed by the platform or greater than the value of **maxWindowHeight**. For details about the window size, see [Constraints](../windowmanager/window-overview.md#constraints).| Number| Yes (initial value: minimum window height supported by the platform)|
| excludeFromMissions | Whether the UIAbility component is displayed in Recents.<br>- **true**: displayed in Recents.<br>- **false**: not displayed in Recents.<br>**NOTE**<br>This attribute applies only to system applications and requires the **AllowAbilityExcludeFromMissions** privilege. For details, see [Application Privilege Configuration](../../device-dev/subsystems/subsys-app-privilege-config-guide.md).| Boolean| Yes (initial value: **false**)|
| recoverable | Whether the application can be recovered to its previous state in case of faults.<br>- **true**: The application can be recovered to its previous state in case of faults.<br>- **false**: The application cannot be recovered to its previous state in case of faults.| Boolean| Yes (initial value: **false**)|
| unclearableMission | Whether the UIAbility is unclearable in Recents.<br>- **true**: The UIAbility is unclearable in Recents.<br>- **false**: The UIAbility is clearable in Recents.<br>**NOTE**<br>This attribute works only after the [AllowMissionNotCleared](../../device-dev/subsystems/subsys-app-privilege-config-guide.md) privilege is obtained.| Boolean| Yes (initial value: **false**)|
| isolationProcess | Whether the component can run in an independent process.<br>- **true**: The component can run in an independent process.<br>- **false**: The component cannot run in an independent process.| Boolean| Yes (initial value: **false**)|

Example of the **abilities** structure:


```json
{
  "abilities": [{
    "name": "EntryAbility",
    "srcEntry": "./ets/entryability/EntryAbility.ets",
    "launchType":"singleton",
    "description": "$string:description_main_ability",
    "icon": "$media:icon",
    "label": "Login",
    "permissions": [],
    "metadata": [],
    "exported": true,
    "continuable": true,
    "skills": [{
      "actions": ["ohos.want.action.home"],
      "entities": ["entity.system.home"],
      "uris": []
    }],
    "backgroundModes": [
      "dataTransfer",
      "audioPlayback",
      "audioRecording",
      "location",
      "bluetoothInteraction",
      "multiDeviceConnection",
      "wifiInteraction",
      "voip",
      "taskKeeping"
    ],
    "startWindowIcon": "$media:icon",
    "startWindowBackground": "$color:red",
    "removeMissionAfterTerminate": true,
    "orientation": " ",
    "supportWindowMode": ["fullscreen", "split", "floating"],
    "maxWindowRatio": 3.5,
    "minWindowRatio": 0.5,
    "maxWindowWidth": 2560,
    "minWindowWidth": 1400,
    "maxWindowHeight": 300,
    "minWindowHeight": 200,
    "excludeFromMissions": false,
    "unclearableMission": false,
    "isolationProcess": false
  }]
}
```


## skills

The **skills** tag represents the feature set of [wants](../application-models/want-overview.md) that can be received by the UIAbility or ExtensionAbility component.

  **Table 7** skills

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| actions | Actions of wants that can be received, which can be predefined or customized.| String array| Yes (initial value: left empty)|
| entities | Entities of wants that can be received.| String array| Yes (initial value: left empty)|
| uris | URIs that match the wants.| Object array| Yes (initial value: left empty)|


  **Table 8** uris

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| scheme | Scheme of the URI, such as HTTP, HTTPS, file, and FTP.| String| Yes when only **type** is set in **uris** (initial value: left empty)|
| host | Host address of the URI. This field is valid only when **scheme** is set. Common methods:<br>- domain name, for example, **example.com**.<br>- IP address, for example, **10.10.10.1**.| String| Yes (initial value: left empty)|
| port | Port number of the URI. For example, the default HTTP port number is 80, the default HTTPS port number is 443, and the default FTP port number is 21. This field is valid only when both **scheme** and **host** are set.| String| Yes (initial value: left empty)|
| path \| pathStartWith \| pathRegex | Path of the URI. **path**, **pathStartWith**, and **pathRegex** represent different matching modes between the paths in the URI and the want. Set any one of them as needed. **path** indicates full matching, **pathStartWith** indicates prefix matching, and **pathRegex** indicates regular expression matching. This field is valid only when both **scheme** and **host** are set.| String| Yes (initial value: left empty)|
| type | Data type that matches the want. The value complies with the Multipurpose Internet Mail Extensions (MIME) type specification. This field can be configured together with **scheme** or be configured separately.| String| Yes (initial value: left empty)|
| utd | [Uniform data types](../reference/apis-arkdata/js-apis-data-uniformTypeDescriptor.md) that match the wants. This field is applicable to scenarios such as sharing.| String| Yes (initial value: left empty)|
| maxFileSupported | Maximum number of files of a specified type that can be received or opened at a time. This field is applicable to scenarios such as sharing and must be used together with **utd**.| Integer| Yes (initial value: **0**)|

Example of the **skills** structure:


```json
{
  "abilities": [
    {
      "skills": [
        {
          "actions": [
            "ohos.want.action.home"
          ],
          "entities": [
            "entity.system.home"
          ],
          "uris": [
            {
              "scheme":"http",
              "host":"example.com",
              "port":"80",
              "path":"path",
              "type": "text/*"
            }
          ]
        }
      ]
    }
  ]
}
```

## extensionAbilities

The **extensionAbilities** tag represents the configuration of ExtensionAbilities, which is valid only for the current ExtensionAbility.

  **Table 9** extensionAbilities

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the ExtensionAbility. This name must be unique in the entire application. The value is a string with a maximum of 127 bytes.| String| No|
| srcEntry | Code path of the ExtensionAbility. The value is a string with a maximum of 127 bytes.| String| No|
| description | Description of the ExtensionAbility. The value is a string with a maximum of 255 bytes. It can be a resource index to support multiple languages.| String| Yes (initial value: left empty)|
| icon | Icon of the ExtensionAbility. The value is the index of the icon resource file. If **ExtensionAbility** is set to **MainElement** of the current module, this field is mandatory.| String| Yes (initial value: left empty)|
| label | Name of the ExtensionAbility displayed to users. The value must be a resource index to support multiple languages. It contains a maximum of 255 bytes. If **ExtensionAbility** is set to **MainElement** of the current module, this field is mandatory and its value must be unique in the application.| String| Yes (initial value: left empty)|
| type | Type of the ExtensionAbility. The options are as follows:<br>- **form**: ExtensionAbility of a widget.<br>- **workScheduler**: ExtensionAbility of a deferred task.<br>- **inputMethod**: ExtensionAbility of an input method.<br>- **service**: service component running in the background.<br>- **accessibility**: ExtensionAbility of an accessibility feature.<br>- **fileAccess**: ExtensionAbility for public data access, allowing files and folders to be provided for file management applications to display.<br>- **dataShare**: ExtensionAbility for data sharing.<br>- **staticSubscriber**: ExtensionAbility for static broadcast.<br>- **wallpaper**: ExtensionAbility of the wallpaper.<br>- **backup**: ExtensionAbility for data backup.<br>- **window**: ExtensionAbility of a window. This type of ExtensionAbility creates a window during startup for which you can develop the GUI. The GUI you develop is combined with the windows of other applications through the **UIExtensionComponent**.<br>- **thumbnail**: ExtensionAbility for obtaining file thumbnails. You can provide thumbnails for files of customized file types.<br>- **preview**: ExtensionAbility for preview. This type of ExtensionAbility can parse the file and display it in a window. You can combine the window with other application windows.<br>- **print**: ExtensionAbility for the print framework.<br>- **push**: ExtensionAbility for the push service.<br>- **driver**: ExtensionAbility for the driver framework.<br>- **remoteNotification**: ExtensionAbility for remote notifications.<br>- **remoteLocation**: ExtensionAbility for remote location.<br>- **voip**: ExtensionAbility for VoIP calls.<br>- **action**: ExtensionAbility for custom service operations, which provides custom service operation templates based on UIExtension.<br>- **adsService**: ExtensionAbility for the ad service, which provides the ad service framework.<br>- **ads**: ExtensionAbility for the ad service, which is used with the AdComponent to display the ad page in other applications. This option is only available for device manufacturers.<br>- **appAccountAuthorization**: ExtensionAbility for application account authorization extension, which is used to process account authorization requests, for example, account login authorization.<br>- **autoFill/password**: ExtensionAbility for automatically filling in usernames and passwords.<br>- **hms/account**: ExtensionAbility for application account management.<br>- **sysDialog/atomicServicePanel**: ExtensionAbility that provides the basic capability of constructing the atomic service panel, which is implemented based on UIExtensionAbility.<br>- **sysDialog/userAuth**: ExtensionAbility for local user authentication.<br>- **sysDialog/common**: ExtensionAbility for common dialog boxes.<br>- **sysDialog/power**: ExtensionAbility for the shutdown and restart dialog boxes.<br>- **sysDialog/print**: ExtensionAbility for the print modals.<br>- **sysDialog/meetimeCall**: ExtensionAbility for MeeTime calls.<br>- **sysDialog/meetimeContact**: ExtensionAbility for MeeTime contacts.<br>- **sysPicker/meetimeMessage**: ExtensionAbility for MeeTime messages.<br>- **sysPicker/meetimeContact**: ExtensionAbility for the MeeTime contact list.<br>- **sysPicker/meetimeCallLog**: ExtensionAbility for the MeeTime call history.<br>- **sysPicker/share**: ExtensionAbility for sharing.<br>- **sysPicker/mediaControl**: ExtensionAbility for media control.<br>- **sys/commonUI**: non-common ExtensionAbility, which provides embedded display or dialog boxes closely related to service attributes.|
| permissions | Permissions required for another application to access the ExtensionAbility.<br>The value is generally in the reverse domain name notation and contains a maximum of 255 bytes. It is an array of [predefined permission names](../security/AccessToken/permissions-for-all.md).| String array| Yes (initial value: left empty)|
| readPermission | Permission required for reading data in the ExtensionAbility. The value is a string with a maximum of 255 bytes. This field is available only when the type of the ExtensionAbility is set to **dataShare**.| String| Yes (initial value: left empty)|
| writePermission | Permission required for writing data to the ExtensionAbility. The value is a string with a maximum of 255 bytes. This field is available only when the type of the ExtensionAbility is set to **dataShare**.| String| Yes (initial value: left empty)|
| uri | Data URI provided by the ExtensionAbility. The value is a string with a maximum of 255 bytes, in the reverse domain name notation.<br>**NOTE**<br>This field is mandatory when the type of the ExtensionAbility is set to **dataShare**.| String| Yes (initial value: left empty)|
|skills | A set of [wants](../application-models/want-overview.md) that can be received by the ExtensionAbility.<br>Configuration rule: In an entry package, you can configure multiple **skills** attributes with the entry capability. (A **skills** attribute with the entry capability is the one that has **ohos.want.action.home** and **entity.system.home** configured.) The label and icon of the first ExtensionAbility that has **skills** configured are used as the label and icon of the entire service/application.<br>**NOTE**<br>The **skills** attribute with the entry capability can be configured for the feature package of an application, but not for a service. | Array| Yes (initial value: left empty)|
| [metadata](#metadata)| Metadata of the ExtensionAbility component.| Object| Yes (initial value: left empty)|
| exported | Whether the ExtensionAbility can be called by other applications.<br>- **true**: The ExtensionAbility can be called by other applications.<br>- **false**: The ExtensionAbility cannot be called by other applications, not even by aa commands.| Boolean| Yes (initial value: **false**)|
| extensionProcessMode | Multi-process instance model of the ExtensionAbility. Currently, this field is effective only for UIExtensionAbilities and ExtensionAbilities extended from UIExtensionAbilities.<br>- **instance**: Each instance of the ExtensionAbility has a process.<br>- **type**: All instances of the ExtensionAbility run in the same process, separated from other ExtensionAbility instances.<br>- **bundle**: All instances of the ExtensionAbility run in the same process as instances of other ExtensionAbilities using the **bundle** model.| String| Yes (initial value: left empty)|

Example of the **extensionAbilities** structure:


```json
{
  "extensionAbilities": [
    {
      "name": "FormName",
      "srcEntry": "./form/MyForm.ts",
      "icon": "$media:icon",
      "label" : "$string:extension_name",
      "description": "$string:form_description",
      "type": "form",
      "permissions": ["ohos.abilitydemo.permission.PROVIDER"],
      "readPermission": "",
      "writePermission": "",
      "exported": true,
      "uri":"scheme://authority/path/query",
      "skills": [{
        "actions": [],
        "entities": [],
        "uris": []
      }],
      "metadata": [
        {
          "name": "ohos.extension.form",
          "resource": "$profile:form_config",
        }
      ],
      "extensionProcessMode": "instance"
    }
  ]
}
```


## requestPermissions

The **requestPermissions** tag represents a set of permissions that the application needs to request from the system for running correctly. For details about how to request permissions, see [Requesting Permissions for Applications](../security/AccessToken/determine-application-mode.md).

> **NOTE**
>
> - The permission settings configured in the **requestPermissions** tag apply to the entire application.
> - If your application needs to subscribe to an event published by itself and the permissions required for accessing the application are set in the **permissions** tag under **extensionAbilities**, then the application must register the related permissions in the **requestPermissions** tag to receive the event.
> - In ecosystem governance, **usedScene** is verified for restricted permissions. Yet, as it (together with **ability**) is not included in the HAR/HSP, it is not verified so that the HAR/HSP build can be successful.

**Table 10** requestPermissions

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the permission to request.| String| No|
| reason | Reason for requesting the permission. The value must be a resource reference to support multiple languages. | String| Yes (initial value: left empty)<br>**NOTE**<br>If the permission to request is **user_grant**, this field is required for the application to be released to the application market.|
| usedScene | Scene under which the permission is used. It consists of the **abilities** and **when** sub-attributes.<br>- **abilities**: array of UIAbility or ExtensionAbility names.<br>- **when**: when the permission is used. The options are **inuse** and **always**.| Object| Yes (initial value: left empty)<br>**NOTE**<br>If the permission to request is **user_grant**, the **abilities** sub-attribute is mandatory and **when** is optional.|

Example of the **requestPermissions** structure:


```json
{
  "module" : {
    "requestPermissions": [
      {
        "name": "ohos.abilitydemo.permission.PROVIDER",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "EntryFormAbility"
          ],
          "when": "inuse"
        }
      }
    ]
  }
}
```


## shortcuts

The **shortcuts** tag provides the shortcut information of an application. The value is an array and consists of four sub-attributes: **shortcutId**, **label**, **icon**, and **wants**.

The **shortcut** information is identified in **metadata**, where:

- **name** indicates the name of the shortcut, identified by **ohos.ability.shortcuts**.

- **resource** indicates where the resources of the shortcut are stored.

**Table 11** shortcuts

| Name| Description| Data Type | Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| shortcutId | ID of the shortcut. The value is a string with a maximum of 63 bytes.| String| No|
| label | Label of the shortcut, that is, the text description displayed for the shortcut. The value is a string with a maximum of 255 bytes. It can be descriptive content or a resource index.| String| Yes (initial value: left empty)|
| icon | Icon of the shortcut. The value is the index to the icon resource file.| String| Yes (initial value: left empty)|
| [wants](../application-models/want-overview.md) | Wants to which the shortcut points. Each want can contain one or more of the **bundleName**, **moduleName**, and **abilityName** sub-attributes.<br>- **bundleName**: target bundle name of the shortcut. The value is a string.<br>- **moduleName**: target module name of the shortcut. The value is a string.<br>- **abilityName**: target ability name of the shortcut. The value is a string.| Object| Yes (initial value: left empty)|


1. Configure the **shortcuts_config.json** file in **/resources/base/profile/**.

   ```json
   {
     "shortcuts": [
       {
         "shortcutId": "id_test1",
         "label": "$string:shortcut",
         "icon": "$media:aa_icon",
         "wants": [
           {
             "bundleName": "com.ohos.hello",
             "moduleName": "entry",
             "abilityName": "EntryAbility"
           }
         ]
       }
     ]
   }
   ```

2. In the **abilities** tag of the **module.json5** file, configure the **metadata** tag for the UIAbility component to which a shortcut needs to be added so that the shortcut configuration file takes effect for the UIAbility.

   ```json
   {
     "module": {
       // ...
       "abilities": [
         {
           "name": "EntryAbility",
           "srcEntry": "./ets/entryability/EntryAbility.ets",
           // ...
           "skills": [
             {
               "entities": [
                 "entity.system.home"
               ],
               "actions": [
                 "ohos.want.action.home"
               ]
             }
           ],
           "metadata": [
             {
               "name": "ohos.ability.shortcuts",
               "resource": "$profile:shortcuts_config"
             }
           ]
         }
       ]
     }
   }
   ```


## distributionFilter

The **distributionFilter** tag defines the rules for distributing HAP files based on different device specifications, so that precise matching can be performed when the application market distributes applications.

> **NOTE**
>
> This tag is supported since API version 10. In earlier versions, the **distroFilter** tag is used.

- **Application scenario**:
  
  If a project has multiple entry-type modules and the values of **deviceType** configured for these modules overlap, you need to use this tag to distinguish the modules. In the following example, both entry-type modules support the tablet type, and therefore the **distributionFilter** tag is required.
  
  ```json
  // Device types supported by entry1
  {
    "module": {
      "name": "entry1",
      "type": "entry",
      "deviceTypes" : [
        "tv",
        "tablet"
      ]
    }
  }
  ```
  ```json
  // Device types supported by entry2
  {
    "module": {
      "name": "entry2",
      "type": "entry",
      "deviceTypes" : [
        "car",
        "tablet"
      ]
    }
  }
  ```
  
- **Configuration rules**:

  This tag consists of four attributes: [screenShape](#screenshape), [screenWindow](#screenwindow), [screenDensity](#screendensity), and [countryCode](#countrycode).

  During distribution, a unique HAP is determined based on the mapping between **deviceTypes** and the preceding attributes.

  * When configuring this tag, include at least one of the attributes.
  * If any one or more attributes are set for one entry-type module, the same attributes must be set for all other entry-type modules.
  * The **screenShape** and **screenWindow** attributes are available only for lite wearables.

- **Configuration**:

  This tag must be configured in the **/resource/profile** directory and be referenced in the **resource** field of **metadata**.


**Table 12** distributionFilter

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| [screenShape](#screenshape) | Supported screen shapes.| Object array| Yes (initial value: left empty)|
| [screenWindow](#screenwindow) | Supported application window resolutions.| Object array| Yes (initial value: left empty)|
| [screenDensity](#screendensity)| Pixel density of the screen, in dots per inch (DPI).| Object array| Yes (initial value: left empty)|
| [countryCode](#countrycode)| Code of the country or region to which the application is to be distributed. The value is subject to the ISO-3166-1 standard. Enumerated definitions of multiple countries and regions are supported.| Object array| Yes (initial value: left empty)|

### screenShape

**Table 13** screenShape

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| policy | Rule for the sub-attribute value.<br>- **exclude**: Exclude the matches of the sub-attribute value.<br>- **include**: Include the matches of the sub-attribute value.| String| No|
| value | Screen shapes. The value can be **circle**, **rect**, or both. For example, different HAPs can be provided for a smart watch with a circular face and that with a rectangular face.| String array| No|

### screenWindow

**Table 14** screenWindow

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| policy | Rule for the sub-attribute value. Currently, the value can only be **include**.<br>- **include**: Include the matches of the sub-attribute value.| String| No|
| value | Screen width and height, in pixels. The value is an array of supported width and height pairs, each in the "width * height" format, for example, **"454 * 454"**.| String array| No|

### screenDensity

**Table 15** screenDensity

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| policy | Rule for the sub-attribute value.<br>- **exclude**: Exclude the matches of the sub-attribute value.<br>- **include**: Include the matches of the sub-attribute value.| String| No|
| value | Pixel density of the screen, in DPI. The options are as follows:<br>- **sdpi**: small-scale DPI. This value is applicable to devices with a DPI range of (0, 120].<br>- **mdpi**: medium-scale DPI. This value is applicable to devices with a DPI range of (120, 160].<br>- **ldpi**: large-scale DPI. This value is applicable to devices with a DPI range of (160, 240].<br>- **xldpi**: extra-large-scale DPI. This value is applicable to devices with a DPI range of (240, 320].<br>- **xxldpi**: extra-extra-large-scale DPI. This value is applicable to devices with a DPI range of (320, 480].<br>- **xxxldpi**: extra-extra-extra-large-scale DPI. This value is applicable to devices with a DPI range of (480, 640].| String array| No|

### countryCode

**Table 16** countryCode

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| policy | Rule for the sub-attribute value.<br>- **exclude**: Exclude the matches of the sub-attribute value.<br>- **include**: Include the matches of the sub-attribute value.| String| No|
| value | Code of the country or region to which the application is to be distributed.| String array| No|


Example:

1. Configure the **distributionFilter_config.json** file (this file name is customizable) in **resources/base/profile** under the development view.
   ```json
   {
     "distributionFilter": {
       "screenShape": {
         "policy": "include",
         "value": [
           "circle",
           "rect"
         ]
       },
       "screenWindow": {
         "policy": "include",
         "value": [
           "454*454",
           "466*466"
         ]
       },
       "screenDensity": {
         "policy": "exclude",
         "value": [
           "ldpi",
           "xldpi"
         ]
       },
       "countryCode": {// Distribution in China is supported.
         "policy": "include",
         "value": [
           "CN"
         ]
       }
     }
   }
   ```


2. Configure **metadata** in the **module** tag in the **module.json5** file.


    ```json
    {
      "module": {
        // ...
        "metadata": [
          {
            "name": "ohos.module.distribution",
            "resource": "$profile:distributionFilter_config",
          }
        ]
      }
    }
    ```


## testRunner

The **testRunner** tag represents the supported test runner.

**Table 17** testRunner

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of the test runner object. The value is a string with a maximum of 255 bytes.| String| No|
| srcPath | Code path of the test runner. The value is a string with a maximum of 255 bytes.	| String| No|

Example of the **testRunner** structure:


```json
{
  "module": {
    // ...
    "testRunner": {
      "name": "myTestRunnerName",
      "srcPath": "etc/test/TestRunner.ts"
    }
  }
}
```

## atomicService

The **atomicService** tag represents the atomic service configuration. It is available only when **bundleType** is set to **atomicService** in the **app.json** file.

**Table 18** atomicService

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| preloads | List of modules to preload in the atomic service.| Object array| Yes (initial value: left empty)|


**Table 19** preloads

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| moduleName | Name of the module to be preloaded when the current module is loaded in the atomic service. The value must match an existing module other than the current one. It contains a maximum of 31 bytes.| String| No|


Example of the **atomicService** structure:

```json
{
  "module": {
    "atomicService": {
      "preloads":[
        {
          "moduleName":"feature"
        }
      ]
    }
  }
}
```

## dependencies

The **dependencies** tag identifies the list of shared libraries that the module depends on when it is running.

**Table 20** dependencies

| Name   | Description                          | Data Type| Initial Value Allowed|
| ----------- | ------------------------------ | -------- | ---------- |
| bundleName  | Name of the shared bundle on which the current module depends. The value is a string of 7 to 128 bytes.| String  | Yes (initial value: left empty)|
| moduleName  | Module name of the shared bundle on which the current module depends. The value is a string with a maximum of 31 bytes.| String  | No|
| versionCode | Version number of the shared bundle. The value ranges from 0 to 2147483647.| Number    | Yes (initial value: left empty)|

Example of the **dependencies** structure:

```json
{
  "module": {
    "dependencies": [
      {
        "bundleName":"com.share.library",
        "moduleName": "library",
        "versionCode": 10001
      }
    ]
  }
}
```

## proxyData

The **proxyDatas** tag provides the list of data proxies provided by the module. It can be configured only for entry and feature modules.

**Table 21** proxyData
| Name   | Description                          | Data Type| Initial Value Allowed|
| ----------- | ------------------------------ | -------- | ---------- |
| uri | URI of the data proxy. The URIs configured for different data proxies must be unique and must be in the *datashareproxy://Current application bundle name/xxx* format. The value is a string with a maximum of 255 bytes.| String  | No|
| requiredReadPermission  | Permission required for reading data from the data proxy. If it is not specified, other applications will not be able to use the data proxy. For non-system applications, the level of the set permission must be **system_basic** or **system_core**. For system applications, the permission level is not limited. For details about the permission levels, see [Permissions for All Applications](../security/AccessToken/permissions-for-all.md). The value is a string with a maximum of 255 bytes.| String  | Yes (initial value: left empty)|
| requiredWritePermission | Permission required for writing data to the data proxy. If it is not specified, other applications will not be able to use the data proxy. For non-system applications, the level of the set permission must be **system_basic** or **system_core**. For system applications, the permission level is not limited. For details about the permission levels, see [Permissions for All Applications](../security/AccessToken/permissions-for-all.md). The value is a string with a maximum of 255 bytes.| String  | Yes (initial value: left empty)|
| [metadata](#metadata)| Metadata of the data proxy. Only the **name** and **resource** fields can be configured.| Object| Yes (initial value: left empty)|

Example of the **proxyData** structure:

```json
{
  "module": {
    "proxyData": [
      {
        "uri":"datashareproxy://com.ohos.datashare/event/Meeting",
        "requiredReadPermission": "ohos.permission.GET_BUNDLE_INFO",
        "requiredWritePermission": "ohos.permission.GET_BUNDLE_INFO",
        "metadata": {
          "name": "datashare_metadata",
          "resource": "$profile:datashare"
        }
      }
    ]
  }
}
```

## definePermissions

The **definePermissions** tag represents a set of permissions defined for the system resource HAP, which cannot be custom permissions. For details, see the definition of system resource permissions in the [config.json](https://gitee.com/openharmony/utils_system_resources/blob/master/systemres/main/config.json) file.

**Table 24** definePermissions

| Name| Description| Data Type| Initial Value Allowed|
| -------- | -------- | -------- | -------- |
| name | Name of a permission. The value can contain a maximum of 255 bytes.| String| No|
| grantMode | Permission grant mode. The options are as follows:<br>- **system_grant**: The permission is automatically granted by the system after the application is installed.<br>- **user_grant**: The permission is dynamically requested when needed and must be granted by the user.| String| Yes (initial value: **"system_grant"**)|
| availableLevel | Permission type. The options are as follows:<br>- **system_core**: system core permission.<br>- **system_basic**: basic system permission.<br>- **normal**: normal permission, which can be requested by all applications.| String| Yes (initial value: **"normal"**)|
| provisionEnable | Whether the permission can be requested in provision mode, including high-level permissions. The value **true** means that the permission can be requested in provision mode.| Boolean| Yes (initial value: **true**)|
| distributedSceneEnabled | Whether the permission can be used in distributed scenarios.| Boolean| Yes (initial value: **false**)|
| label | Brief description of the permission. The value is a resource index to the description.| String| Yes (initial value: left empty)|
| description | Detailed description of the permission. The value is a string or a resource index to the description.| String| Yes (initial value: left empty)|

Example of the **definePermissions** structure:

```json
{
  "module" : {
    "definePermissions": [
    {
      {
        "name": "ohos.abilitydemo.permission.PROVIDER",
        "grantMode": "system_grant",
        "availableLevel": "system_core",
        "provisionEnable": true,
        "distributedSceneEnable": false,
        "label": "$string:EntryAbility_label"
        }
      }
    ]
  }
}
```
