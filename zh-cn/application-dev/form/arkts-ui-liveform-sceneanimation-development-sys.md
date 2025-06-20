# 场景动效类型互动卡片开发指导（系统应用）

场景动效类型互动卡片基础开发指导，可以参考文档[场景动效类型互动卡片开发指导](arkts-ui-liveform-sceneanimation-development.md)。针对系统应用，场景动效类型互动卡片提供了**手势禁用配置**和**卡片长时激活**两个扩展能力。

## 接口说明

场景动效类型互动卡片开发关键接口如下表所示。

**表1** 主要接口

| 接口名                                                                                                                                                                       | 描述                                                                                                                  |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| [formProvider.activateSceneAnimation(formId: string): Promise&lt;void&gt;](../reference/apis-form-kit/js-apis-app-form-formProvider-sys.md#activatesceneanimation20)     | 互动卡片请求状态切换到激活态。 |
| [formProvider.deactivateSceneAnimation(formId: string): Promise&lt;void&gt;](../reference/apis-form-kit/js-apis-app-form-formProvider-sys.md#deactivatesceneanimation20) | 互动卡片请求切换到非激活态。 |


## 手势禁用配置
针对[场景动效类型互动卡片](arkts-ui-liveform-sceneanimation-overview.md)，若用户在桌面的长按、拖拽等操作会打断当前动效，卡片重新变成非激活态。系统应用可通过form_config.json中[disabledDesktopBehaviors](arkts-ui-widget-configuration.md#sceneanimationparams标签)字段进行配置取消该限制，确保用户在激活态卡片交互热区内操作时，不打断当前卡片动效。
不配置时，默认不拦截任何用户在桌面的有效手势操作。手势操作拦截后，对应手势事件由LiveFormExtensionAbility响应。

```ts
// entry/src/main/resources/base/profile/form_config.json
{
  "forms": [
    {
      // ...
      "sceneAnimationParams": {
        "abilityName": "MySystemLiveFormExtensionAbility",
        "disabledDesktopBehaviors": "LONG_CLICK|DRAG|SWIPE_DESKTOP|PULL_DOWN_SEARCH"
      }
    }
  ]
}
```

## 卡片长时激活

针对系统应用，支持卡片提供方通过接口控制卡片状态切换，不对激活态保持时间做强限制，即卡片可以长时间保持激活态。卡片进入/退出激活态操作由[formProvider.activateSceneAnimation](../reference/apis-form-kit/js-apis-app-form-formProvider-sys.md#activatesceneanimation20)和[formProvider.deactivateSceneAnimation](../reference/apis-form-kit/js-apis-app-form-formProvider-sys.md#deactivatesceneanimation20)接口控制。
此外，卡片通过formProvider.activateSceneAnimation进入激活态后，卡片动效渲染区域和卡片自身渲染区域等大，且不支持调用[formProvider.requestOverflow](../reference/apis-form-kit/js-apis-app-form-formProvider.md#formproviderrequestoverflow20)接口请求动效。

### 开发流程
1. 导入模块

```ts
import { formProvider } from '@kit.FormKit';
import { BusinessError } from '@kit.BasicServicesKit';
```

2. 触发卡片长时激活

```ts
let formId: string = '12400633174999288';

try {
  formProvider.activateSceneAnimation(formId).then(() => {
    console.info('activateSceneAnimation succeed.');
  }).catch((error: BusinessError) => {
    console.error(`promise error, code: ${error.code}, message: ${error.message})`);
  });
} catch (error) {
  console.error(`catch error, code: ${(error as BusinessError).code}, message: ${(error as BusinessError).message})`);
}
```

3. 卡片退出激活态

```ts
let formId: string = '12400633174999288';

try {
  formProvider.deactivateSceneAnimation(formId).then(() => {
    console.info('deactivateSceneAnimation succeed.');
  }).catch((error: BusinessError) => {
    console.error(`promise error, code: ${error.code}, message: ${error.message})`);
  });
} catch (error) {
  console.error(`catch error, code: ${(error as BusinessError).code}, message: ${(error as BusinessError).message})`);
}
```

4. LiveFormExtensionAbility适配

为卡片提供方更精准控制卡片状态切换，避免由于加载复杂界面UI时，耗时较长造成页面页面切换不流畅。卡片提供方需在切换至激活态时，通过session发送信息通知卡片使用方，卡片使用方收到信息后开始加载卡片激活态界面。

```ts
// entry/src/main/ets/mysystemliveformextensionability/MySystemLiveFormExtensionAbility.ets 
import { formInfo, LiveFormInfo, LiveFormExtensionAbility } from '@kit.FormKit';
import { UIExtensionContentSession } from '@kit.AbilityKit';

export default class MySystemLiveFormExtensionAbility extends LiveFormExtensionAbility {
  onLiveFormCreate(liveFormInfo: LiveFormInfo, session: UIExtensionContentSession) {
    let storage: LocalStorage = new LocalStorage();
    storage.setOrCreate('session', session);

    // 获取参卡片信息
    let formId: string = liveFormInfo.formId as string;
    storage.setOrCreate('formId', formId);
    let formRect: formInfo.Rect = liveFormInfo.rect;
    storage.setOrCreate('formRect', formRect);
    let borderRadius: number = liveFormInfo.borderRadius;
    storage.setOrCreate('borderRadius', borderRadius);
    console.log(`MySystemLiveFormExtensionAbility onSessionCreate formId: ${formId}, borderRadius: ${borderRadius}` +
      `, formRect: ${JSON.stringify(formRect)}`);

    // 加载提供方页面
    session.loadContent('mysystemliveformextensionability/pages/MySystemLiveFormPage', storage);

    // 卡片提供方需在激活态页面准备就绪时，通过 session 发送信息告知卡片使用方
    session.sendData({['isFormReady']: true});
  }

  onLiveFormDestroy(liveFormInfo: LiveFormInfo) {
    console.log(`MySystemLiveFormExtensionAbility onDestroy`);
  }
}
```