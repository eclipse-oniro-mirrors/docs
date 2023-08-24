# UIExtensionComponent

**\<UIExtensionComponent>** is used to embed UIs provided by other applications in the local application UI. The embedded content runs in another process, and the local application does not participate in its layout and rendering.

This component is usually used in modular development scenarios where process isolation is required.

> **NOTE**
>
> This component is supported since API version 10. Updates will be marked with a superscript to indicate their earliest API version.
>
> The APIs provided by this component are system APIs.

## Restrictions

This component does not support preview.

The ability to be started must be a UIExtensionAbility, an extension ability with UI. For details about how to implement a UIExtensionAbility, see [Implementing UIExtensionAbility](../apis/js-apis-app-ability-uiExtensionAbility.md).

The width and height of the component must be set to non-zero valid values.

## Child Components

Not supported

## APIs

UIExtensionComponent(want: Want)

**Parameters**

| Name | Type                                    | Mandatory  | Description           |
| ---- | ---------------------------------------- | ---- | --------------- |
| want | [Want](../apis/js-apis-app-ability-want.md) | Yes   | Ability to start.|

## UIExtensionProxy

Implements a **UIExtensionProxy** instance to send data from the component host to the started UIExtensionAbility through the connection established between the two parties.

### send

send(data: { [key: string]: Object }): void

**Parameters**

| Name | Type                                    | Mandatory  | Description           |
| ---- | ---------------------------------------- | ---- | --------------- |
| data | { [key: string]: Object } | Yes   | Data to send to the started UIExtensionAbility.|

## Attributes

The [universal attributes](ts-universal-attributes-size.md) are supported.

## Events

The [universal events](ts-universal-events-click.md) are not supported.

The events are passed to the remote UIExtensionAbility for processing after coordinate conversion.

The following events are supported:

### onRemoteReady

onRemoteReady(callback: [Callback](../apis/js-apis-base.md#callback)\<UIExtensionProxy>)

Invoked when the connection to the remote UIExtensionAbility is set up, that is, the UIExtensionAbility is ready to receive data through the proxy.

**Parameters**

| Name                      | Type  | Description                                                        |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| proxy                        | UIExtensionProxy | Proxy used to send data to the remote UIExtensionAbility.                         |

### onReceive

onReceive(callback: [Callback](../apis/js-apis-base.md#callback)\<{ [key: string]: Object }>)

Invoked when the data sent by the started UIExtensionAbility is received.

**Parameters**

| Name                      | Type  | Description                                                        |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| data                        | { [key: string]: Object } | Data from the remote UIExtensionAbility.                |

### onResult

onResult(callback: [Callback](../apis/js-apis-base.md#callback)\<{code: number; want?: Want}>)

Invoked when the started UIExtensionAbility calls **terminateSelfWithResult**. After this callback is invoked, **OnRelease** is invoked.

The result data of the remote UIExtensionAbility can be processed in this callback. For details, see [AbilityResult](../apis/js-apis-inner-ability-abilityResult.md).

**Parameters**

| Name                      | Type  | Description                                                        |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| code                        | number | Result code from the remote UIExtensionAbility.                         |
| want                        | Want | [Want](../apis/js-apis-app-ability-want.md) of the result from the remote UIExtensionAbility.|

### onRelease

onRelease(callback: [Callback](../apis/js-apis-base.md#callback)\<number>)

Invoked when the started UIExtensionAbility is destroyed.

If the UIExtensionAbility is destroyed correctly by calling **terminateSelfWithResult** or **terminateSelf**, the value of **releaseCode** is **0**.

If the UIExtensionAbility is destroyed because it crashes or is forced stopped, the value of **releaseCode** is **1**.

**Parameters**

| Name                      | Type  | Description                                                        |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| releaseCode                        | number | Code that indicates how the remote UIExtensionAbility is destroyed. The value **0** means normal destruction, and **1** means abnormal destruction.                         |

### onError

onError(callback:[ErrorCallback](../apis/js-apis-base.md#errorcallback))

Invoked when an exception occurs during the running of the UIExtensionAbility. You can obtain the error information based on the **code**, **name**, and **message** parameters in the callback and rectify the exception accordingly.

**Parameters**

| Name                      | Type  | Description                                                        |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| err                        | [BusinessError](../apis/js-apis-base.md#businesserror) | Error information.   |

## Example

This example shows only the method used by the component and the UIExtensionAbility. For the code to run properly, you need to install the ability whose **bundleName** is **"com.example.uiextensionprovider"** and **abilityName** is **"UIExtensionProvider"** on the device.

```ts
// Component usage example:
@Entry
@Component
struct Index {
  @State message: string = 'Hello World'
  private myProxy: UIExtensionProxy
  build() {
    Row() {
      Column() {
        Text(this.message).fontColor(Color.Red)
        UIExtensionComponent(
          {
            bundleName: "com.example.uiextensionprovider",
            abilityName: "UIExtensionProvider",
            parameters: { "x": 12345, "y": "data" }
          }
        )
        .size({ width: "100%", height:"100%" })
        .onRemoteReady((proxy) => {
            this.message = "remote ready"
            this.myProxy = proxy
        })
        .onReceive((data) => {
            this.message = JSON.stringify(data)
        })
        .onRelease((releaseCode) => {
          this.message = "Release: " + releaseCode
        })
        .onResult((data) => {
          this.message = JSON.stringify(data)
        })
        .onError((error) => {
          this.message = "onError: " + error["code"] + ", name: " + error.name + ", message: " + error.message
        })
        Button("sendData").onClick(() => {
          this.myProxy.send({ "x": 5678910 })
        })
      }
      .width("100%")
    }
    .height('100%')
  }
}
```

```ts
// Extension entry point file UIExtensionProvider.ts
import UIExtensionAbility from '@ohos.app.ability.UIExtensionAbility'
const TAG: string = '[UIExtAbility]'
export default class UIExtAbility extends UIExtensionAbility {
  onCreate() {
    console.log(TAG, `UIExtAbility onCreate`)
  }

  onForeground() {
    console.log(TAG, `UIExtAbility onForeground`)
  }

  onBackground() {
    console.log(TAG, `UIExtAbility onBackground`)
  }

  onDestroy() {
    console.log(TAG, `UIExtAbility onDestroy`)
  }

  onSessionCreate(want, session) {
    console.log(TAG, `UIExtAbility onSessionCreate, want: ${JSON.stringify(want)}`)
    let storage: LocalStorage = new LocalStorage({
      'session': session
    });
    session.loadContent('pages/extension', storage);
  }

  onSessionDestroy(session) {
    console.log(TAG, `UIExtAbility onSessionDestroy`)
  }
}
```

```ts
// Extension Ability entry page file extension.ets
import UIExtensionContentSession from '@ohos.app.ability.UIExtensionContentSession'
let storage = LocalStorage.GetShared()
@Entry(storage)
@Component
struct Index {
  @State message: string = 'UIExtension'
  @State message2:string = 'message from comp'
  private session: UIExtensionContentSession = storage.get<UIExtensionContentSession>('session');
  controller: TextInputController = new TextInputController()
  onPageShow() {
    this.session.setReceiveDataCallback((data)=> {
      this.message2 = "data come from comp"
      this.message = JSON.stringify(data)
    })
  }
  build() {
    Row() {
      Column() {
        Text(this.message2)
        Text(this.message)
        Button("sendData")
          .onClick(()=>{
            this.session.sendData({"xxx": "data from extension"})
          })
        Button("terminateSelf")
          .onClick(()=>{
            this.session.terminateSelf();
            storage.clear();
          }).margin(5)
        Button("TerminateSelfWithResult")
          .onClick(()=>{
            this.session.terminateSelfWithResult({
              "resultCode": 0,
              "want": {
                "bundleName": "myName"
              }
            });
            storage.clear();
          }).margin(5)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```
<!--no_check-->