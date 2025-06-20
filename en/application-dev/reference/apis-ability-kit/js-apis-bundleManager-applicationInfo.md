# ApplicationInfo

The ApplicationInfo module defines the application information. A third-party application can obtain its own application information through [bundleManager.getBundleInfoForSelf](js-apis-bundleManager.md#bundlemanagergetbundleinfoforself), with **GET_BUNDLE_INFO_WITH_APPLICATION** passed in to [bundleFlags](js-apis-bundleManager.md#bundleflag).

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## ApplicationInfo

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

| Name                      | Type                                                        | Read-Only| Optional| Description                                                        |
| -------------------------- | ------------------------------------------------------------ | ---- | ---- | ------------------------------------------------------------ |
| name                       | string                                                       | Yes  | No  | Application name.<br>**Atomic service API**: This API can be used in atomic services since API version 11.                                                |
| description                | string                                                       | Yes  | No  | Description of the application, for example, "description": $string: mainability_description". For details, see the description of the **descriptionResource** field below.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| descriptionId              | number                                                       | Yes  | No  | ID of the application description.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| enabled                    | boolean                                                      | Yes  | No  | Whether the application is enabled. The value **true** means that the application is enabled, and **false** means the opposite.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| label                      | string                                                       | Yes  | No  | Application name, for example, "label": "$string: mainability_description". For details, see the description of the **labelResource** field below.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| labelId                    | number                                                       | Yes  | No  | ID of the application label.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| icon                       | string                                                       | Yes  | No  | Application icon, for example, "icon": "$media:icon". For details, see the description of the **iconResource** field below.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| iconId                     | number                                                       | Yes  | No  | ID of the application icon.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| process                    | string                                                       | Yes  | No  | Process name.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| permissions                | Array\<string>                                               | Yes  | No  | Permissions required for accessing the application. The permissions can be obtained by passing in **GET_BUNDLE_INFO_WITH_APPLICATION** and **GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION** to the **bundleFlags** parameter of [getBundleInfoForSelf](js-apis-bundleManager.md#bundlemanagergetbundleinfoforself).<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| codePath                   | string                                                       | Yes  | No  | Installation directory of the application.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| metadata<sup>(deprecated)<sup>  | Map\<string, Array\<[Metadata](js-apis-bundleManager-metadata.md)>> | Yes  | No  | Metadata of the application. The information can be obtained by passing in **GET_BUNDLE_INFO_WITH_APPLICATION** and **GET_BUNDLE_INFO_WITH_METADATA** to the **bundleFlags** parameter of [getBundleInfoForSelf](js-apis-bundleManager.md#bundlemanagergetbundleinfoforself).<br>**NOTE**<br>The **metadata** field is deprecated since API version 10. You are advised to use **metadataArray** instead.|
| metadataArray<sup>10+</sup>              | Array\<[ModuleMetadata](#modulemetadata10)> | Yes  | No  | Metadata of the application. The information can be obtained by passing in **GET_BUNDLE_INFO_WITH_APPLICATION** and **GET_BUNDLE_INFO_WITH_METADATA** to the **bundleFlags** parameter of [getBundleInfoForSelf](js-apis-bundleManager.md#bundlemanagergetbundleinfoforself).<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| removable                  | boolean                                                      | Yes  | No  | Whether the application is removable. The value **true** means that the application is removable, and **false** means the opposite.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| accessTokenId             | number                                                       | Yes  | No  | Access token ID of the application.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| uid                       | number                                                       | Yes  | No  | UID of the application.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| iconResource              | [Resource](../apis-localization-kit/js-apis-resource-manager.md#resource9) | Yes| No| Resource information of the application icon. The resource information obtained contains the bundle name, module name, and ID of the resource. You can call [getMediaContent](../apis-localization-kit/js-apis-resource-manager.md#getmediacontent9) to obtain the resource details.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| labelResource             | [Resource](../apis-localization-kit/js-apis-resource-manager.md#resource9) | Yes| No| Resource information of the application label. The resource information obtained contains the bundle name, module name, and ID of the resource. You can call [getMediaContent](../apis-localization-kit/js-apis-resource-manager.md#getmediacontent9) to obtain the resource details.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| descriptionResource       | [Resource](../apis-localization-kit/js-apis-resource-manager.md#resource9) | Yes| No| Resource information of the application description. The resource information obtained contains the bundle name, module name, and ID of the resource. You can call [getMediaContent](../apis-localization-kit/js-apis-resource-manager.md#getmediacontent9) to obtain the resource details.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| appDistributionType       | string                                                       | Yes  | No  | Distribution type of the application signing certificate. The options are **app_gallery**, **enterprise**, **os_integration**, and **crowdtesting**.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| appProvisionType          | string                                                       | Yes  | No  | Type of the application signing certificate file. The options are **debug** and **release**.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| systemApp          | boolean                                                       | Yes  | No  | Whether the application is a system application. The value **true** means that the application is a system application, and **false** means the opposite.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| bundleType                |[bundleManager.BundleType](js-apis-bundleManager.md#bundletype)             | Yes  | No  | Bundle type, which can be **APP** (application) or **ATOMIC_SERVICE** (atomic service).<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| debug<sup>10+</sup>       | boolean                                | Yes  | No  | Whether the application is running in debug mode. The value **true** means that the application is running in debug mode, and **false** means the opposite.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| dataUnclearable<sup>11+</sup>       | boolean                      | Yes  | No  | Whether the application data is unclearable. The value **true** means that the application data is unclearable, and **false** means the opposite.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| nativeLibraryPath<sup>12+</sup> | string                                                                     | Yes  | No  | Local library file path of the application.                                                 |
| multiAppMode<sup>12+</sup> | [MultiAppMode](#multiappmode12) | Yes  | No  | Multi-app mode.|
| appIndex<sup>12+</sup>    | number    | Yes  | No  | Index of an application clone. It takes effect only for cloned applications.|
| installSource<sup>12+</sup>    | string    | Yes  | No  | Installation source of the application. The options are as follows:<br> - **pre-installed**: The application is a preset application installed at initial device startup.<br> - **ota**: The application is a preset application added during system upgrade.<br> - **recovery**: The preset application is uninstalled and then restored.<br> - Bundle name of an application: The application is installed from the specified bundle name.<br> - **unknown**: The installation source is unknown.<br>**Atomic service API**: This API can be used in atomic services since API version 12.|
| releaseType<sup>12+</sup>    | string    | Yes  | No  | Release type of the SDK used for application packing. Currently, the SDK release types include Canary, Beta, and Release. Each of the Canary and Beta releases can be distinguished by a sequential number, such as Canary1, Canary2, Beta1, and Beta2. You can compare the SDK release type on which application packaging depends and the OS release type (specified by [deviceInfo.distributionOSReleaseType](../apis-basic-services-kit/js-apis-device-info.md)) to determine the compatibility.<br>**Atomic service API**: This API can be used in atomic services since API version 12.|
| cloudFileSyncEnabled<sup>12+</sup>    | boolean    | Yes  | No  | Whether device-cloud file synchronization is enabled for the application. The value **true** means that device-cloud file synchronization is enabled, and **false** means the opposite.<br>**Atomic service API**: This API can be used in atomic services since API version 12.|

## MultiAppMode<sup>12+</sup>
Defines the multi-app mode.

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

**Parameters**

| Name     | Type          | Read-Only| Optional| Description                       |
| --------- | -------------- | ---- | ---- | --------------------------- |
| multiAppModeType<sup>12+</sup> | bundleManager.MultiAppModeType | Yes| No|  Type of the multi-app mode. |
| maxCount<sup>12+</sup> | number  | Yes| No|  Maximum number of accounts that can log in to the application at the same time. |

## ModuleMetadata<sup>10+</sup>

Describes the metadata of a module.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

| Name     | Type          | Read-Only| Optional| Description                       |
| --------- | -------------- | ---- | ---- | --------------------------- |
| moduleName<sup>10+</sup>| string         | Yes  | No  | Module name.  |
| metadata<sup>10+</sup>  | Array\<[Metadata](js-apis-bundleManager-metadata.md)>      | Yes  | No  | Metadata list of the module.|
