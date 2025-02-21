# UIExtensionComponent (系统接口)

UIExtensionComponent用于支持在本页面内嵌入其他应用提供的UI。展示的内容在另外一个进程中运行，本应用并不参与其中的布局和渲染。

通常用于有进程隔离诉求的模块化开发场景。

> **说明：**
>
> 该组件从API Version 10开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
>
> 本模块为系统接口。

## 使用约束

本组件不支持预览。

被拉起的Ability必须是带UI的Ability扩展，如何实现带UI的Ability扩展请参考[实现带UI的Ability扩展](../../apis-ability-kit/js-apis-app-ability-uiExtensionAbility.md)。

必须显示设置组件宽高为非0有效值。

## 子组件

无

## 接口

UIExtensionComponent(want: Want, options?: UIExtensionOptions)

**参数：**

| 参数名                | 参数类型                                                   | 必填 | 参数描述           |
| --------------------- | ---------------------------------------------------------- | ---- | ------------------ |
| want                  | [Want](../../apis-ability-kit/js-apis-app-ability-want.md) | 是   | 要加载的Ability。  |
| options<sup>11+</sup> | [UIExtensionOptions](#uiextensionoptions11)                | 否   | 需要传递的构造项。 |

## 属性

支持[通用属性](ts-universal-attributes-size.md)。

## 事件

不支持[通用事件](ts-universal-events-click.md)。

将事件经过坐标转换后传递给对端Ability处理。

支持以下事件：

### onRemoteReady

onRemoteReady(callback: [Callback](../../apis-basic-services-kit/js-apis-base.md#callback)\<UIExtensionProxy>)

UIExtensionAbility连接完成时的回调，之后可使用proxy向被拉起的Ability发送数据。

**参数：**

| 参数名                       | 类型   | 说明                                                         |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| proxy                        | UIExtensionProxy | 用于向对端Ability发送数据。                          |

### onReceive

onReceive(callback: [Callback](../../apis-basic-services-kit/js-apis-base.md#callback)\<{ [key: string]: Object }>)

收到被拉起的Ability发送的数据时触发的回调。

**参数：**

| 参数名                       | 类型   | 说明                                                         |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| data                        | { [key: string]: Object } | 收到来自对端Ability的数据。                 |

### onResult

onResult(callback: [Callback](../../apis-basic-services-kit/js-apis-base.md#callback)\<{code: number; want?: Want}>)

被拉起的Ability扩展调用terminateSelfWithResult时会先触发本回调函数，再触发OnRelease。

本回调内可处理对端Ability的结果数据，可参考[AbilityResult](../../apis-as/js-apis-inner-ability-abilityResult.md)。

**参数：**

| 参数名                       | 类型   | 说明                                                         |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| code                        | number | 收到来自对端Ability的处理結果code。                          |
| want                        | Want | 收到来自对端Ability的处理結果[Want](../../apis-ability-kit/js-apis-app-ability-want.md)。 |

### onRelease

onRelease(callback: [Callback](../../apis-basic-services-kit/js-apis-base.md#callback)\<number>)

用于处理被拉起的Ability销毁时的回调。

被拉起的Ability扩展调用terminateSelfWithResult或者terminateSelf时会触发本回调，此时releaseCode为0，即正常销毁。

被拉起的Ability扩展意外Crash或被kill时，触发本回调，此时releaseCode为1。

**参数：**

| 参数名                       | 类型   | 说明                                                         |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| releaseCode                        | number | 对端Ability销毁时的code，0为正常销毁，1为异常销毁。                          |

### onError

onError(callback:[ErrorCallback](../../apis-basic-services-kit/js-apis-base.md#errorcallback))

被拉起的Ability扩展在运行过程中发生异常时触发本回调。可通过回调参数中的code、name和message获取错误信息并做处理。

**参数：**

| 参数名                       | 类型   | 说明                                                         |
| ---------------------------- | ------ | ------------------------------------------------------------ |
| err                        | [BusinessError](../../apis-basic-services-kit/js-apis-base.md#businesserror) | 报错信息。    |

## UIExtensionOptions<sup>11+</sup>
用于在UIExtensionComponent进行构造的时传递可选的构造参数。

**参数：**

| 参数名               | 参数类型                                 | 必填 | 参数描述                                                                                                      |
| ----                 | ---------------------------------------- | ---- | ---------------                                                                                               |
| isTransferringCaller | boolean                                  | 否   | 在使用UIExtensionComponent嵌套时，设置当前UIExtensionComponent是否转发上一级的Caller信息。</br> 默认值：false。 |

## UIExtensionProxy

用于在双方建立连接成功后，组件使用方向被拉起的Ability发送数据、订阅和取消订阅注册。

### send

send(data: { [key: string]: Object }): void

用于在双方建立连接成功后，组件使用方向被拉起的Ability发送数据的场景，提供异步发送数据。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名  | 参数类型                                     | 必填   | 参数描述            |
| ---- | ---------------------------------------- | ---- | --------------- |
| data | { [key: string]: Object } | 是    | 异步发送给被拉起的扩展Ability的数据。 |

### sendSync<sup>11+</sup>

sendSync(data: { [key: string]: Object }): { [key: string]: Object }

用于在双方建立连接成功后，组件使用方向被拉起的Ability发送数据的场景，提供同步发送数据。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名  | 参数类型                                     | 必填   | 参数描述            |
| ---- | ---------------------------------------- | ---- | --------------- |
| data | { [key: string]: Object } | 是    | 同步发送给被拉起的扩展Ability的数据。 |

**返回值：**

| 类型 | 描述 |
| ---- | ----|
|{ [key: string]: Object } | 扩展Ability回复的数据。 |

**错误码：**

| 错误号 | 描述 |
| ---- | ----|
| 100011 | 扩展Ability未注册同步回调 |
| 100012 | 数据发送失败 |

### on('asyncReceiverRegister')<sup>11+</sup>

on(type: 'asyncReceiverRegister', callback: (proxy: UIExtensionProxy) => void): void

用于在双方建立连接成功后，组件使用方订阅被拉起的Ability发生异步注册的场景。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名  | 参数类型 |必填 | 参数描述 |
| ------ | -------- |---- | ------- |
| type   | string | 是 | 代表订阅扩展Ability发生异步注册回调。 |
| callback   | (proxy: UIExtensionProxy) => void | 是 | 订阅扩展Ability注册setReceiveDataCallback后触发的回调。 |

### on('syncReceiverRegister')<sup>11+</sup>

on(type: 'syncReceiverRegister', callback: (proxy: UIExtensionProxy) => void): void

用于在双方建立连接成功后，组件使用方订阅被拉起的Ability发生同步注册的场景。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名  | 参数类型 |必填 | 参数描述 |
| ------ | -------- |---- | ------- |
| type   | string | 是 | 订阅扩展Ability发生同步注册回调。 |
| callback   | (proxy: UIExtensionProxy) => void | 是 | 扩展Ability注册setReceiveDataForResultCallback后触发的回调。 |

### off('asyncReceiverRegister')<sup>11+</sup>

off(type: 'asyncReceiverRegister', callback?: (proxy: UIExtensionProxy) => void): void

用于在双方建立连接成功后，组件使用方取消订阅被拉起的Ability发生异步注册的场景。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名  | 参数类型 | 必填 | 参数描述 |
| ------ | -------- | ----- | ------- |
| type   | string | 是 | 取消订阅扩展Ability发生异步注册回调。 |
| callback | (proxy: UIExtensionProxy) => void | 否 | 为空代表取消订阅所有扩展Ability异步注册后触发回调。<br> 非空代表取消订阅异步对应回调。 |

### off('syncReceiverRegister')<sup>11+</sup>

off(type: 'syncReceiverRegister', callback?: (proxy: UIExtensionProxy) => void): void

用于在双方建立连接成功后，组件使用方取消订阅被拉起的Ability发生同步注册的场景。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名  | 参数类型 | 必填 | 参数描述 |
| ------ | -------- | ----- | ------- |
| type   | string | 是 | 取消订阅扩展Ability发生同步注册回调。 |
| callback | (proxy: UIExtensionProxy) => void | 否 | 为空代表取消订阅所有扩展Ability同步注册后触发回调<br> 非空代表取消订阅同步对应回调。 |

## 示例

本示例仅展示组件使用的方法和扩展的Ability，实际运行需在设备中安装bundleName为"com.example.uiextensionprovider"，abilityName为"UIExtensionProvider"的Ability扩展。

```ts
// 组件使用示例：
@Entry
@Component
struct Second {
  @State message1: string = 'Hello World 1'
  @State message2: string = 'Hello World 2'
  @State message3: string = 'Hello World 3'
  @State visible: Visibility = Visibility.Hidden
  @State wid: number = 300
  @State hei: number = 300
  private proxy: UIExtensionProxy | null = null;


  build() {
    Row() {
      Column() {
        Text(this.message1).fontSize(30)
        Text(this.message2).fontSize(30)
        Text(this.message3).fontSize(30)
        UIExtensionComponent({
          bundleName : "com.example.newdemo",
          abilityName: "UIExtensionProvider",
          parameters: {
            "ability.want.params.uiExtensionType": "dialog"
          }
        })
          .width(this.wid)
          .height(this.hei)
          .border({width: 5, color: Color.Blue})
          .onResult((data)=>{
            this.message1 = data['want'] ? JSON.stringify(data['want']['bundleName']) : "";
          })
          .onRelease((code)=>{
            this.message2 = "release code : " + code
          })
          .onReceive((data) => {
            console.info('Lee onReceive, for test')
            this.message3 = JSON.stringify(data['data'])
          })
          .onRemoteReady((proxy) => {
            console.info('onRemoteReady, for test')
            this.proxy = proxy

            this.proxy.on("syncReceiverRegister", syncRegisterCallback1);
            // this.proxy.on("syncReceiverRegister", syncRegisterCallback2);


            // this.proxy.off("syncReceiverRegister");

            // this.proxy.off("syncReceiverRegister", (proxy) => {
            //   console.info("off invoke for test, type is syncReceiverRegister");
            // });

            this.proxy.on("asyncReceiverRegister", (proxy1) => {
              console.info("on invoke for test, type is asyncReceiverRegister");
            });
            //
            // this.proxy.off("asyncReceiverRegister");
          })

        Button("点击向UIExtensionAbility发送数据").onClick(() => {
          if (this.proxy != undefined) {
            this.proxy.send({data: "你好1"})

            try {
              let re = this.proxy.sendSync({data: "你好2"})
              console.info("for test, re=" + JSON.stringify(re));
            } catch (err) {
              console.error(`sendSync failed for test. errCode=${err.code}, msg=${err.message}`);
            }
          }
        })
      }
      .width('100%')
    }
    .height('100%')
  }
}

function syncRegisterCallback1(proxy: UIExtensionProxy) {
  console.info("on invoke for test, syncRegisterCallback1, type is syncReceiverRegister");
}

function syncRegisterCallback2(proxy: UIExtensionProxy) {
  console.info("on invoke for test, syncRegisterCallback2, type is syncReceiverRegister");
}
```

```ts
// 扩展入口文件UIExtensionProvider.ts
import UIExtensionAbility from '@ohos.app.ability.UIExtensionAbility'
import UIExtensionContentSession from '@ohos.app.ability.UIExtensionContentSession'
import Want from '@ohos.app.ability.Want';
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

  onSessionCreate(want: Want, session: UIExtensionContentSession) {
    console.log(TAG, `UIExtAbility onSessionCreate, want: ${JSON.stringify(want)}`)
    let param: Record<string, UIExtensionContentSession> = {
      'session': session
    };
    let storage: LocalStorage = new LocalStorage(param);
    session.loadContent('pages/extension', storage);
  }

  onSessionDestroy(session: UIExtensionContentSession) {
    console.log(TAG, `UIExtAbility onSessionDestroy`)
  }
}
```

```ts
// 扩展Ability入口页面文件extension.ets
import UIExtensionContentSession from '@ohos.app.ability.UIExtensionContentSession';
import router from '@ohos.router';

let storage = LocalStorage.getShared()
AppStorage.setOrCreate('message', 'UIExtensionAbility')

@Entry(storage)
@Component
struct Extension {
  @StorageLink('message') storageLink: string = '';
  private session: UIExtensionContentSession | undefined = storage.get<UIExtensionContentSession>('session');

  onPageShow() {
    if (this.session != undefined) {
      this.session.setReceiveDataCallback((data)=> {
        this.storageLink = JSON.stringify(data)
        console.info("invoke for test, handle callback set by setReceiveDataCallback successfully");
      })

      this.session.setReceiveDataForResultCallback(func1)
    }
  }

  build() {
    Row() {
      Column() {
        Text(this.storageLink)
          .fontSize(20)
          .fontWeight(FontWeight.Bold)
        Button("点击向Component发送数据").onClick(()=>{
          if (this.session != undefined) {
            this.session.sendData({"data": 543321})
            console.info('send 543321, for test')
          }
        })
        Button("terminate").onClick(()=> {
          if (this.session != undefined) {
            this.session.terminateSelf();
          }
          storage.clear()
        })
        Button("terminate with result").onClick(()=>{
          if (this.session != undefined) {
            this.session.terminateSelfWithResult({
              resultCode: 0,
              want: {
                bundleName: "myBundleName",
                parameters: { "result": 123456 }
              }
            })
          }
          storage.clear()
        })

        Button("点击跳转").onClick(()=> {
          router.pushUrl({url: 'pages/hello'})
        })
      }
    }
    .height('100%')
  }
}
function func1(data: Record<string, Object>): Record<string, Object> {
  let linkToMsg: SubscribedAbstractProperty<string> = AppStorage.link('message');
  linkToMsg.set(JSON.stringify(data))
  console.info("invoke for test, handle callback set by setReceiveDataForResultCallback successfully");
  return data;
}

```
