# EmbeddedComponent

The **EmbeddedComponent** is a component used to embed into the current page the UI provided by another [EmbeddedUIExtensionAbility](../../apis-ability-kit/js-apis-app-ability-embeddedUIExtensionAbility.md) in the same application. The EmbeddedUIExtensionAbility runs in an independent process for UI layout and rendering.

It is usually used in modular development scenarios where process isolation is required.

> **NOTE**
>
> This component is supported since API version 12. Updates will be marked with a superscript to indicate their earliest API version.

## Constraints

The **EmbeddedComponent** is supported only on devices configured with multi-process permissions.

The **EmbeddedComponent** can be used only in the UIAbility, and the EmbeddedUIExtensionAbility to start must belong to the same application as the UIAbility.

## Child Components

Not supported

## APIs

EmbeddedComponent(loader: Want, type: EmbeddedType)

**Atomic service API**: This API can be used in atomic services since API version 12.

**Parameters**

| Name               | Type                                                  | Mandatory| Description                            |
| --------------------- | ---------------------------------------------------------- | ---- | ------------------------------------ |
| loader                | [Want](../../apis-ability-kit/js-apis-app-ability-want.md) | Yes  | EmbeddedUIExtensionAbility to load.|
| type                  | [EmbeddedType](ts-appendix-enums.md#embeddedtype12)                              | Yes  | Type of the provider.                      |

## Attributes

The [universal attributes](ts-universal-attributes-size.md) are supported.

> **NOTE**
>
> The default and minimum widths and heights of the **EmbeddedComponent** are all 10 vp. The following attributes related to the width and height are not supported: **constraintSize**, **aspectRatio**, **layoutWeight**, **flexBasis**, **flexGrow**, and **flexShrink**.

## Events

Event information related to screen coordinates is converted based on the position, width, and height of the **EmbeddedComponent**, before being transferred to the EmbeddedUIExtensionAbility for processing.

The [universal events](ts-universal-events-click.md) are not supported. Only the following events are supported.

### onTerminated

onTerminated(callback: Callback&lt;TerminationInfo&gt;)

Called when the started EmbeddedUIExtensionAbility is terminated by calling **terminateSelfWithResult** or **terminateSelf**.

**Atomic service API**: This API can be used in atomic services since API version 12.

**Parameters**

| Name  | Type  | Description                                                                                    |
| -------  | ------ | ---------------------------------------------------------------------------------------- |
| callback | [Callback](../../apis-basic-services-kit/js-apis-base.md#callback)\<[TerminationInfo](#terminationinfo)> | Callback used to return the result from the EmbeddedUIExtensionAbility.|

> **NOTE**
>
> - If the EmbeddedUIExtensionAbility is terminated by calling **terminateSelfWithResult**, the carried information is passed as arguments into the callback function.
> - If the EmbeddedUIExtensionAbility is terminated by calling **terminateSelf**, the input parameters **code** and **want** in the callback function are at their default values: **0** and **undefined**, respectively.

### onError

onError(callback: ErrorCallback)

Called when an error occurs during the running of the started EmbeddedUIExtensionAbility.

**Atomic service API**: This API can be used in atomic services since API version 12.

**Parameters**

| Name| Type                                                                        | Description     |
| ------ | ---------------------------------------------------------------------------- | --------- |
| callback    | [ErrorCallback](../../apis-basic-services-kit/js-apis-base.md#errorcallback) | Callback used to return the error information of the [BusinessError](../../apis-basic-services-kit/js-apis-base.md#businesserror) type. The error information can be obtained and processed based on the **code**, **name**, and **message** parameters.|

> **NOTE**
>
> This callback is called to notify the provider of the following:
> - The EmbeddedUIExtensionAbility fails to be started.
> - The EmbeddedUIExtensionAbility fails to be switched to the background.
> - The EmbeddedUIExtensionAbility fails to be destroyed.
> - The EmbeddedUIExtensionAbility exits abnormally.
> - An **EmbeddedComponent** is nested in the EmbeddedUIExtensionAbility.

## TerminationInfo

Provides the result returned by the started **EmbeddedUIExtensionAbility**.

**Atomic service API**: This API can be used in atomic services since API version 12.

| Name | Type  | Description                                                |
| ------- | ------ | ---------------------------------------------------  |
| code    | number | Result code returned when the EmbeddedUIExtensionAbility exits.|
| want    | [Want](../../apis-ability-kit/js-apis-app-ability-want.md)   | Data returned when the EmbeddedUIExtensionAbility exits.  |

## Example

This example shows the basic usage of the **EmbeddedComponent** and EmbeddedUIExtensionAbility. The bundle name of the sample application is **com.example.embeddeddemo**, and the started EmbeddedUIExtensionAbility is ExampleEmbeddedAbility.

- The EntryAbility (UIAbility) of the sample application loads the **pages/Index.ets** file, whose content is as follows:

  ```ts
  // The UIAbility loads pages/Index.ets when started.
  import { Want } from '@kit.AbilityKit';

  @Entry
  @Component
  struct Index {
    @State message: string = 'Message: '
    private want: Want = {
      bundleName: "com.example.embeddeddemo",
      abilityName: "ExampleEmbeddedAbility",
    }

    build() {
      Row() {
        Column() {
          Text(this.message).fontSize(30)
          EmbeddedComponent(this.want, EmbeddedType.EMBEDDED_UI_EXTENSION)
            .width('100%')
            .height('90%')
            .onTerminated((info)=>{
              this.message = 'Termination: code = ' + info.code + ', want = ' + JSON.stringify(info.want);
            })
            .onError((error)=>{
              this.message = 'Error: code = ' + error.code;
            })
        }
        .width('100%')
      }
      .height('100%')
    }
  }
  ```

- The EmbeddedUIExtensionAbility started by the **EmbeddedComponent** is implemented in the **ets/extensionAbility/ExampleEmbeddedAbility** file. The file content is as follows:

  ```ts
  import { EmbeddedUIExtensionAbility, UIExtensionContentSession, Want } from '@kit.AbilityKit';

  const TAG: string = '[ExampleEmbeddedAbility]'
  export default class ExampleEmbeddedAbility extends EmbeddedUIExtensionAbility {
    
    onCreate() {
      console.log(TAG, `onCreate`);
    }

    onForeground() {
      console.log(TAG, `onForeground`);
    }

    onBackground() {
      console.log(TAG, `onBackground`);
    }

    onDestroy() {
      console.log(TAG, `onDestroy`);
    }

    onSessionCreate(want: Want, session: UIExtensionContentSession) {
      console.log(TAG, `onSessionCreate, want: ${JSON.stringify(want)}`);
      let param: Record<string, UIExtensionContentSession> = {
        'session': session
      };
      let storage: LocalStorage = new LocalStorage(param);
      session.loadContent('pages/extension', storage);
    }

    onSessionDestroy(session: UIExtensionContentSession) {
      console.log(TAG, `onSessionDestroy`);
    }
  }
  ```

- The entry page file of the EmbeddedUIExtensionAbility is **pages/extension.ets**, whose content is as follows:

  ```ts
  import { UIExtensionContentSession } from '@kit.AbilityKit';

  let storage = LocalStorage.getShared()

  @Entry(storage)
  @Component
  struct Extension {
    @State message: string = 'EmbeddedUIExtensionAbility Index';
    private session: UIExtensionContentSession | undefined = storage.get<UIExtensionContentSession>('session');

    build() {
      Column() {
        Text(this.message)
          .fontSize(20)
          .fontWeight(FontWeight.Bold)
        Button("terminateSelfWithResult").fontSize(20).onClick(() => {
          this.session?.terminateSelfWithResult({
            resultCode: 1,
            want: {
              bundleName: "com.example.embeddeddemo",
              abilityName: "ExampleEmbeddedAbility",
            }});
        })
      }.width('100%').height('100%')
    }
  }
  ```

- Add an item to **extensionAbilities** in the **module.json5** file of the sample application. The details are as follows:
  ```json
  {
    "name": "ExampleEmbeddedAbility",
    "srcEntry": "./ets/extensionAbility/ExampleEmbeddedAbility.ets",
    "type": "embeddedUI"
  }
  ```
