# LifecycleService接口切换


  | FA模型接口 | Stage模型接口对应d.ts文件 | Stage模型对应接口 | 
| -------- | -------- | -------- |
| onStart?():&nbsp;void; | \@ohos.app.ability.ServiceExtensionAbility.d.ts | [onCreate(want:&nbsp;Want):&nbsp;void;](../reference/apis/js-apis-app-ability-serviceExtensionAbility.md#serviceextensionabilityoncreate) |
| onCommand?(want:&nbsp;Want,&nbsp;startId:&nbsp;number):&nbsp;void; | \@ohos.app.ability.ServiceExtensionAbility.d.ts | [onRequest(want:&nbsp;Want,&nbsp;startId:&nbsp;number):&nbsp;void;](../reference/apis/js-apis-app-ability-serviceExtensionAbility.md#serviceextensionabilityonrequest) |  |
| onStop?():&nbsp;void; | \@ohos.app.ability.ServiceExtensionAbility.d.ts | [onDestroy():&nbsp;void;](../reference/apis/js-apis-app-ability-serviceExtensionAbility.md#serviceextensionabilityondestroy) |  |
| onConnect?(want:&nbsp;Want):&nbsp;rpc.RemoteObject; | \@ohos.app.ability.ServiceExtensionAbility.d.ts | [onConnect(want:&nbsp;Want):&nbsp;rpc.RemoteObject;](../reference/apis/js-apis-app-ability-serviceExtensionAbility.md#serviceextensionabilityonconnect) |  |
| onDisconnect?(want:&nbsp;Want):&nbsp;void; | \@ohos.app.ability.ServiceExtensionAbility.d.ts | [onDisconnect(want:&nbsp;Want):&nbsp;void;](../reference/apis/js-apis-app-ability-serviceExtensionAbility.md#serviceextensionabilityondisconnect) |  |
| onReconnect?(want:&nbsp;Want):&nbsp;void; | \@ohos.app.ability.ServiceExtensionAbility.d.ts | [onReconnect(want:&nbsp;Want):&nbsp;void;](../reference/apis/js-apis-app-ability-serviceExtensionAbility.md#serviceextensionabilityonreconnect) |  |
