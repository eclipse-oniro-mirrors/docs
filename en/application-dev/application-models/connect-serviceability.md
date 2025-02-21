

If a ServiceAbility wants to interact with a PageAbility or a ServiceAbility in another application, you must first create a connection by calling **connectAbility()**. The [connectAbility()](../reference/apis-ability-kit/js-apis-ability-featureAbility.md#featureabilityconnectability7) method of the PageAbility is defined in [featureAbility](../reference/apis-ability-kit/js-apis-ability-featureAbility.md), and the [connectAbility()](../reference/apis-ability-kit/js-apis-ability-particleAbility.md#particleabilityconnectability) method of the ServiceAbility is defined in [particleAbility](../reference/apis-ability-kit/js-apis-ability-particleAbility.md). For details about the connection rules, see [Component Startup Rules](component-startup-rules-fa.md). When using **connectAbility()** to process the callback, pass in the instances of [Want](../reference/apis-ability-kit/js-apis-app-ability-want.md) and [IAbilityConnection](../reference/apis-ability-kit/js-apis-inner-ability-connectOptions.md) of the target ServiceAbility. [IAbilityConnection](../reference/apis-ability-kit/js-apis-inner-ability-connectOptions.md) provides the following callbacks that you should implement.


**Table 1** IAbilityConnection APIs

| API| Description|
| -------- | -------- |
| onConnect() | Callback invoked when the ServiceAbility is connected.|
| onDisconnect() | Callback invoked when the ServiceAbility is disconnected.|
| onFailed() | Callback invoked when the connection to the ServiceAbility fails.|


The following sample code enables the PageAbility to create connection callback instances and connect to the local ServiceAbility:

```ts
import featureAbility from '@ohos.ability.featureAbility';
import common from '@ohos.app.ability.common';
import Want from '@ohos.app.ability.Want';
import promptAction from '@ohos.promptAction';
import rpc from '@ohos.rpc';
import hilog from '@ohos.hilog';
```
```ts
const LOG_TAG: string = '[Sample_FAModelAbilityDevelop]';
const LOG_DOMAIN: number = 0xFF00;
let option: common.ConnectOptions = {
  onConnect: (element, proxy) => {
    hilog.info(LOG_DOMAIN, LOG_TAG, 'onConnectLocalService onConnectDone element:' + JSON.stringify(element));
    if (proxy === null) {
      promptAction.showToast({
        message: 'connect service failed'
      });
      return;
    }
    let data = rpc.MessageParcel.create();
    let reply = rpc.MessageParcel.create();
    let option = new rpc.MessageOption();
    data.writeInterfaceToken('connect.test.token');
    proxy.sendRequest(0, data, reply, option);
    promptAction.showToast({
      message: 'connect service success'
    });
  },
  onDisconnect: (element) => {
    hilog.info(LOG_DOMAIN, LOG_TAG, `onConnectLocalService onDisconnectDone element:${element}`);
    promptAction.showToast({
      message: 'disconnect service success'
    });
  },
  onFailed: (code) => {
    hilog.info(LOG_DOMAIN, LOG_TAG, `onConnectLocalService onFailed errCode:${code}`);
    promptAction.showToast({
      message: 'connect service failed'
    });
  }
};

let request: Want = {
  bundleName: 'com.samples.famodelabilitydevelop',
  abilityName: 'com.samples.famodelabilitydevelop.ServiceAbility',
};
let connId = featureAbility.connectAbility(request, option);
hilog.info(LOG_DOMAIN, LOG_TAG, `connectAbility id:${connId}`);
```


When the ServiceAbility is connected, the **onConnect()** callback is invoked and returns an **IRemoteObject** defining the proxy used for communicating with the ServiceAbility. The system provides a default implementation of **IRemoteObject**. You can extend **rpc.RemoteObject** to implement your own class of **IRemoteObject**.


The following sample code shows how the ServiceAbility returns itself to the caller:

```ts
import type Want from '@ohos.app.ability.Want';
import rpc from '@ohos.rpc';
import hilog from '@ohos.hilog';

const TAG: string = '[Sample_FAModelAbilityDevelop]';
const domain: number = 0xFF00;

class FirstServiceAbilityStub extends rpc.RemoteObject {
  constructor(des: Object) {
    if (typeof des === 'string') {
      super(des);
    } else {
      return;
    }
  }

  onRemoteRequest(code: number, data: rpc.MessageParcel, reply: rpc.MessageParcel, option: rpc.MessageOption): boolean {
    hilog.info(domain, TAG, 'ServiceAbility onRemoteRequest called');
    if (code === 1) {
      let string = data.readString();
      hilog.info(domain, TAG, `ServiceAbility string=${string}`);
      let result = Array.from(string).sort().join('');
      hilog.info(domain, TAG, `ServiceAbility result=${result}`);
      reply.writeString(result);
    } else {
      hilog.info(domain, TAG, 'ServiceAbility unknown request code');
    }
    return true;
  }
}
//...
```
