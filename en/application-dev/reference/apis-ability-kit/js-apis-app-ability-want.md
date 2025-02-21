# @ohos.app.ability.Want (Want)

Want is a carrier for information transfer between objects (application components). Want can be used as a parameter of **startAbility** to specify a startup target and information that needs to be carried during startup, for example, **bundleName** and **abilityName**, which respectively indicate the bundle name of the target ability and the ability name in the bundle. When UIAbilityA needs to start UIAbilityB and transfer some data to UIAbilityB, it can use Want a carrier to transfer the data.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import Want from '@ohos.app.ability.Want';
```

## Attributes

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityBase

| Name       | Type                | Mandatory | Description                                                        |
| ----------- | -------------------- | ---- | ------------------------------------------------------------ |
| deviceId    | string               | No  | ID of the device running the ability. If this field is unspecified, the local device is used.                               |
| bundleName   | string               | No  | Bundle name of the ability. |
| moduleName | string | No | Name of the module to which the ability belongs. |
| abilityName  | string               | No  | Name of the ability. If both **bundleName** and **abilityName** are specified in a **Want** object, the **Want** object can match a specific ability. The value of **abilityName** must be unique in an application. |
| action | string               | No  | Action to take, such as viewing and sharing application details. In implicit Want, you can define this field and use it together with **uri** or **parameters** to specify the operation to be performed on the data. For details about the definition and matching rules of implicit Want, see [Matching Rules of Explicit Want and Implicit Want](../../application-models/explicit-implicit-want-mappings.md).            |
| entities | Array\<string> | No | Additional category information (such as browser and video player) of the ability. It is a supplement to the **action** field for implicit Want. and is used to filter ability types. |
| uri | string | No | Data carried. This field is used together with **type** to specify the data type. If **uri** is specified in a Want, the Want will match the specified URI information, including **scheme**, **schemeSpecificPart**, **authority**, and **path**. |
| type | string | No | MIME type, that is, the type of the file to open, for example, **'text/xml'** and **'image/*'**. For details about the MIME type definition, see https://www.iana.org/assignments/media-types/media-types.xhtml?utm_source=ld246.com. |
| parameters   | Record\<string, Object> | No  | List of parameters in the **Want** object.<br>1. The values of the following keys are assigned by the system. Manual settings do not take effect, since the system automatically changes the values to the actual values during data transfer.<br>- **ohos.aafwk.param.callerPid**: PID of the caller. The value is a string.<br>- **ohos.aafwk.param.callerBundleName**: bundle name of the caller. The value is a string.<br>- **ohos.aafwk.param.callerToken**: token of the caller. The value is a string.<br>- **ohos.aafwk.param.callerUid**: UID in [BundleInfo](js-apis-bundleManager-bundleInfo.md#bundleinfo-1), that is, the application UID in the bundle information. The value is a number.<br>- **component.startup.newRules**: enabled status of the new control rule. The value is of the Boolean type.<br>- **moduleName**: module name of the caller. The value is a string.<br>- **ability.params.backToOtherMissionStack**: support for redirection back across mission stacks. The value is of the Boolean type.<br>- **ohos.ability.params.abilityRecoveryRestart**: support for ability restart upon fault recovery. The value is of the Boolean type.<br>- **ohos.extra.param.key.contentTitle**: title that can be shared by the atomic service. The value is a string.<br>- **ohos.extra.param.key.shareAbstract**: content that can be shared by the atomic service. The value is a string.<br>- **ohos.extra.param.key.shareUrl**: URL of the content that can be shared by the atomic service. The value is a string.<br>- **ohos.extra.param.key.supportContinuePageStack**: support for migration of page stack information during cross-device migration. The value is of the Boolean type. The default value is **true**, indicating that page stack information is automatically migrated.<br>- **ohos.extra.param.key.supportContinueSourceExit**: support for application exit on the source device during cross-device migration. The value is of the Boolean type. The default value is **true**, indicating that the application on the source device automatically exits.<br>- **ohos.dlp.params.sandbox**: available only for DLP files. This key is involved only in system applications.<br>- **ohos.dlp.params.bundleName**: bundle name of DLP. The value is a string. This key is involved only in system applications.<br>- **ohos.dlp.params.moduleName**: module name of DLP. The value is a string. This key is involved only in system applications.<br>- **ohos.dlp.params.abilityName**: ability name of DLP. The value is a string. This key is involved only in system applications.<br>- **ohos.dlp.params.index**: DLP index. The value is a number. This key is involved only in system applications.<br>2. Applications may further agree on the key-value pairs to transfer.<br>For details about the constants of **Params** in **want**, see [wantConstant](js-apis-app-ability-wantConstant.md).<br>Note that a maximum of 200 KB data that can be transferred by using **WantParams**. If the data volume exceeds 200 KB, transfer data in [WriteRawDataBuffer](../apis-ipc-kit/js-apis-rpc.md#writerawdatabuffer11) or [uri](../apis-arkts/js-apis-uri.md) mode.<br>The values of **parameters** must be of the following basic data types: String, Number, Boolean, Object, undefined, and null. |
| [flags](js-apis-ability-wantConstant.md#wantconstantflags) | number | No | How the **Want** object will be handled. By default, a number is passed in.<br>For example, **wantConstant.Flags.FLAG_ABILITY_CONTINUATION** specifies whether to start the ability in cross-device migration scenarios. |

**Example**

- Basic usage: called in a UIAbility object, as shown in the example below. For details about how to obtain the context, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

  ```ts
  import common from '@ohos.app.ability.common';
  import Want from '@ohos.app.ability.Want';
  import { BusinessError } from '@ohos.base';

  let context = getContext(this) as common.UIAbilityContext; // UIAbilityContext
  let want: Want = {
    deviceId: '', // An empty deviceId indicates the local device.
    bundleName: 'com.example.myapplication',
    abilityName: 'FuncAbility',
    moduleName: 'entry', // moduleName is optional.
  };

  context.startAbility(want, (err: BusinessError) => {
    if (err.code) {
      // Start an ability explicitly. The bundleName, abilityName, and moduleName parameters work together to uniquely identify an ability.
      console.error(`Failed to startAbility. Code: ${err.code}, message: ${err.message}`);
    }
  });
  ```

- Currently, the following data types are supported: string, number, Boolean, object, array, and file descriptor (FD).

    * String
        ```ts
        import common from '@ohos.app.ability.common';
        import Want from '@ohos.app.ability.Want';
        import { BusinessError } from '@ohos.base';

        let context = getContext(this) as common.UIAbilityContext; // UIAbilityContext
        let want: Want = {
          bundleName: 'com.example.myapplication',
          abilityName: 'FuncAbility',
          parameters: {
            keyForString: 'str',
          },
        };

        context.startAbility(want, (err: BusinessError) => {
          if (err.code) {
            console.error(`Failed to startAbility. Code: ${err.code}, message: ${err.message}`);
          }
        });
        ```
    * Number
        ```ts
        import common from '@ohos.app.ability.common';
        import Want from '@ohos.app.ability.Want';
        import { BusinessError } from '@ohos.base';

        let context = getContext(this) as common.UIAbilityContext; // UIAbilityContext
        let want: Want = {
          bundleName: 'com.example.myapplication',
          abilityName: 'FuncAbility',
          parameters: {
            keyForInt: 100,
            keyForDouble: 99.99,
          },
        };

        context.startAbility(want, (err) => {
          if (err.code) {
            console.error(`Failed to startAbility. Code: ${err.code}, message: ${err.message}`);
          }
        });
        ```
    * Boolean
        ```ts
        import common from '@ohos.app.ability.common';
        import Want from '@ohos.app.ability.Want';
        import { BusinessError } from '@ohos.base';

        let context = getContext(this) as common.UIAbilityContext; // UIAbilityContext
        let want: Want = {
          bundleName: 'com.example.myapplication',
          abilityName: 'FuncAbility',
          parameters: {
            keyForBool: true,
          },
        };

        context.startAbility(want, (err: BusinessError) => {
          if (err.code) {
            console.error(`Failed to startAbility. Code: ${err.code}, message: ${err.message}`);
          }
        });
        ```
    * Object
        ```ts
        import common from '@ohos.app.ability.common';
        import Want from '@ohos.app.ability.Want';
        import { BusinessError } from '@ohos.base';

        let context = getContext(this) as common.UIAbilityContext; // UIAbilityContext
        let want: Want = {
          bundleName: 'com.example.myapplication',
          abilityName: 'FuncAbility',
          parameters: {
            keyForObject: {
              keyForObjectString: 'str',
              keyForObjectInt: -200,
              keyForObjectDouble: 35.5,
              keyForObjectBool: false,
            },
          },
        };

        context.startAbility(want, (err: BusinessError) => {
          if (err.code) {
            console.error(`Failed to startAbility. Code: ${err.code}, message: ${err.message}`);
          }
        });
        ```
    * Array

        ```ts
        import common from '@ohos.app.ability.common';
        import Want from '@ohos.app.ability.Want';
        import { BusinessError } from '@ohos.base';

        let context = getContext(this) as common.UIAbilityContext; // UIAbilityContext
        let want: Want = {
          bundleName: 'com.example.myapplication',
          abilityName: 'FuncAbility',
          parameters: {
            keyForArrayString: ['str1', 'str2', 'str3'],
            keyForArrayInt: [100, 200, 300, 400],
            keyForArrayDouble: [0.1, 0.2],
            keyForArrayObject: [{ obj1: 'aaa' }, { obj2: 100 }],
          },
        };

        context.startAbility(want, (err: BusinessError) => {
          if (err.code) {
            console.error(`Failed to startAbility. Code: ${err.code}, message: ${err.message}`);
          }
        });
        ```
    * FD
      ```ts
        import fs from '@ohos.file.fs';
        import common from '@ohos.app.ability.common';
        import Want from '@ohos.app.ability.Want';
        import { BusinessError } from '@ohos.base';

        let context = getContext(this) as common.UIAbilityContext; // UIAbilityContext

        let fd: number = 0;
        try {
          fd = fs.openSync('/data/storage/el2/base/haps/pic.png').fd;
        } catch(err) {
          let code = (err as BusinessError).code;
          let message = (err as BusinessError).message;
          console.error(`Failed to openSync. Code: ${code}, message: ${message}`);
        }
        let want: Want = {
          deviceId: '', // An empty deviceId indicates the local device.
          bundleName: 'com.example.myapplication',
          abilityName: 'FuncAbility',
          moduleName: 'entry', // moduleName is optional.
          parameters: {
            'keyFd': { 'type': 'FD', 'value': fd } // {'type':'FD', 'value':fd} is a fixed usage, indicating that the data is a file descriptor.
          }
        };

        context.startAbility(want, (err: BusinessError) => {
          if (err.code) {
            console.error(`Failed to startAbility. Code: ${err.code}, message: ${err.message}`);
          }
        });
      ```

- **parameter** usage: **parameter** carries custom parameters. It is transferred by UIAbilityA to UIAbilityB and obtained from UIAbilityB.

    ```ts
      // (1) UIAbilityA calls startAbility to start UIAbilityB.
      import common from '@ohos.app.ability.common';
      import Want from '@ohos.app.ability.Want';
      import { BusinessError } from '@ohos.base';

      let context = getContext(this) as common.UIAbilityContext; // UIAbilityContext
      let want: Want = {
        bundleName: 'com.example.myapplication',
        abilityName: 'UIAbilityB',
        parameters: {
          developerParameters: 'parameters',
        },
      };
      context.startAbility(want, (err: BusinessError) => {
        if (err.code) {
          console.error(`Failed to startAbility. Code: ${err.code}, message: ${err.message}`);
        }
      });
    ```

    ```ts
      // (2) If the UIAbilityB instance is started for the first time, it enters the onCreate lifecycle.
      import UIAbility from '@ohos.app.ability.UIAbility';
      import AbilityConstant from '@ohos.app.ability.AbilityConstant';
      import Want from '@ohos.app.ability.Want';

      class UIAbilityB extends UIAbility {
        onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
          console.log(`onCreate, want parameters: ${want.parameters?.developerParameters}`);
        }
      }
    ```
- Usage of the keys of [wantConstant](js-apis-app-ability-wantConstant.md) in **parameter**.
    ```ts
      import common from '@ohos.app.ability.common';
      import Want from '@ohos.app.ability.Want';
      import wantConstant from '@ohos.app.ability.wantConstant';
      import { BusinessError } from '@ohos.base';

      let context = getContext(this) as common.UIAbilityContext; // UIAbilityContext
      let want: Want = {
        bundleName: 'com.example.myapplication',
        abilityName: 'FuncAbility',
        parameters: {
          [wantConstant.Params.CONTENT_TITLE_KEY]: 'contentTitle',
        },
      };

      context.startAbility(want, (err: BusinessError) => {
        if (err.code) {
          console.error(`Failed to startAbility. Code: ${err.code}, message: ${err.message}`);
        }
      });
    ```
