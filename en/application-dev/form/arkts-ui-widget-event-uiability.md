# Updating Widget Content Through the router or call Event


On the widget page, the [postCardAction()](../reference/apis-arkui/js-apis-postCardAction.md#postcardaction) API can be used to trigger a router or call event to start a UIAbility, which then updates the widget content. The following is an example of this widget update mode.

> **NOTE**
>
> This topic describes development for dynamic widgets. For static widgets, see [FormLink](../reference/apis-arkui/arkui-ts/ts-container-formlink.md).

## Updating Widget Content Through the router Event

- On the widget page, register the **onClick** event callback of the button and call the [postCardAction()](../reference/apis-arkui/js-apis-postCardAction.md#postcardaction) API in the callback to trigger the router event to start the UIAbility.
  
  ```ts
  let storageUpdateRouter = new LocalStorage();
  
  @Entry(storageUpdateRouter)
  @Component
  struct WidgetUpdateRouterCard {
    @LocalStorageProp('routerDetail') routerDetail: ResourceStr = $r('app.string.init');
  
    build() {
      Column() {
        Column() {
          Text(this.routerDetail)
            .fontColor('#FFFFFF')
            .opacity(0.9)
            .fontSize(14)
            .margin({ top: '8%', left: '10%', right: '10%' })
            .textOverflow({ overflow: TextOverflow.Ellipsis })
            .maxLines(2)
        }.width('100%').height('50%')
        .alignItems(HorizontalAlign.Start)
  
        Row() {
          Button() {
            Text($r('app.string.JumpLabel'))
              .fontColor('#45A6F4')
              .fontSize(12)
          }
          .width(120)
          .height(32)
          .margin({ top: '30%', bottom: '10%' })
          .backgroundColor('#FFFFFF')
          .borderRadius(16)
          .onClick(() => {
            postCardAction(this, {
              action: 'router',
              abilityName: 'WidgetEventRouterEntryAbility', // Only the UIAbility of the current application is allowed.
              params: {
                routerDetail: 'RouterFromCard',
              }
            });
          })
        }.width('100%').height('40%')
        .justifyContent(FlexAlign.Center)
      }
      .width('100%')
      .height('100%')
      .alignItems(HorizontalAlign.Start)
      .backgroundImage($r('app.media.CardEvent'))
      .backgroundImageSize(ImageSize.Cover)
    }
  }
  ```
  
- In the **onCreate()** or **onNewWant()** lifecycle callback of the UIAbility, use the input parameter **want** to obtain the ID (**formID**) and other information of the widget, and then call the [updateForm](../reference/apis-form-kit/js-apis-app-form-formProvider.md#updateform) API to update the widget.
  
  ```ts
  import type AbilityConstant from '@ohos.app.ability.AbilityConstant';
  import type Base from '@ohos.base';
  import formBindingData from '@ohos.app.form.formBindingData';
  import formInfo from '@ohos.app.form.formInfo';
  import formProvider from '@ohos.app.form.formProvider';
  import hilog from '@ohos.hilog';
  import UIAbility from '@ohos.app.ability.UIAbility';
  import type Want from '@ohos.app.ability.Want';
  import type window from '@ohos.window';
  
  const TAG: string = 'WidgetEventRouterEntryAbility';
  const DOMAIN_NUMBER: number = 0xFF00;
  
  export default class WidgetEventRouterEntryAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
      this.handleFormRouterEvent(want);
    }
  
    handleFormRouterEvent(want: Want): void {
      hilog.info(DOMAIN_NUMBER, TAG, 'handleFormRouterEvent, Want:', JSON.stringify(want));
      if (want.parameters && want.parameters[formInfo.FormParam.IDENTITY_KEY] !== undefined) {
        let curFormId = JSON.stringify(want.parameters[formInfo.FormParam.IDENTITY_KEY]);
        let message: string = JSON.stringify(want.parameters.routerDetail);
        hilog.info(DOMAIN_NUMBER, TAG, `UpdateForm formId: ${curFormId}, message: ${message}`);
        let formData: Record<string, string> = {
          'routerDetail': message + 'UIAbility.', // It matches the widget layout.
        };
        let formMsg = formBindingData.createFormBindingData(formData);
        formProvider.updateForm(want.parameters[formInfo.FormParam.IDENTITY_KEY] + '', formMsg).then((data) => {
          hilog.info(DOMAIN_NUMBER, TAG, 'updateForm success.', JSON.stringify(data));
        }).catch((error: Base.BusinessError) => {
          hilog.info(DOMAIN_NUMBER, TAG, 'updateForm failed.', JSON.stringify(error));
        });
      }
    }
  
    // If the UIAbility is running in the background, onNewWant is triggered after the router event is received.
    onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
      hilog.info(DOMAIN_NUMBER, TAG, 'onNewWant Want:', JSON.stringify(want));
      if (want.parameters && want.parameters[formInfo.FormParam.IDENTITY_KEY] !== undefined) {
        let curFormId = JSON.stringify(want.parameters[formInfo.FormParam.IDENTITY_KEY]);
        let message: string = JSON.stringify(want.parameters.routerDetail);
        hilog.info(DOMAIN_NUMBER, TAG, `UpdateForm formId: ${curFormId}, message: ${message}`);
        let formData: Record<string, string> = {
          'routerDetail': message + 'onNewWant UIAbility.', // It matches the widget layout.
        };
        let formMsg = formBindingData.createFormBindingData(formData);
        formProvider.updateForm(want.parameters[formInfo.FormParam.IDENTITY_KEY] + '', formMsg).then((data) => {
          hilog.info(DOMAIN_NUMBER, TAG, 'updateForm success.', JSON.stringify(data));
        }).catch((error: Base.BusinessError) => {
          hilog.info(DOMAIN_NUMBER, TAG, 'updateForm failed.', JSON.stringify(error));
        });
      }
    }
  
    onWindowStageCreate(windowStage: window.WindowStage): void {
      // Main window is created, set main page for this ability
      hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', 'Ability onWindowStageCreate');
  
      windowStage.loadContent('pages/Index', (err, data) => {
        if (err.code) {
          hilog.error(DOMAIN_NUMBER, TAG, 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
          return;
        }
        hilog.info(DOMAIN_NUMBER, TAG, 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
      });
    }
    ...
  }
  ```



## Updating Widget Content Through the call Event

- When using the call event of the **postCardAction** API, the value of **formId** must be updated in the **onAddForm** callback of the FormExtensionAbility.

  ```ts
  import formBindingData from '@ohos.app.form.formBindingData';
  import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';
  import type Want from '@ohos.app.ability.Want';
  
  export default class WidgetCalleeFormAbility extends FormExtensionAbility {
    onAddForm(want: Want): formBindingData.FormBindingData {
      class DataObj1 {
        formId: string = '';
      }
  
      let dataObj1 = new DataObj1();
      if (want.parameters && want.parameters['ohos.extra.param.key.form_identity'] !== undefined) {
        let formId: string = want.parameters['ohos.extra.param.key.form_identity'].toString();
        dataObj1.formId = formId;
      }
      let obj1 = formBindingData.createFormBindingData(dataObj1);
      return obj1;
    }
    ...
  }
  ```

- On the widget page, register the **onClick** event callback of the button and call the **postCardAction** API in the callback to trigger the call event to start the UIAbility.
  
  ```ts
  let storageUpdateCall = new LocalStorage();
  
  @Entry(storageUpdateCall)
  @Component
  struct WidgetUpdateCallCard {
    @LocalStorageProp('formId') formId: string = '12400633174999288';
    @LocalStorageProp('calleeDetail') calleeDetail: ResourceStr = $r('app.string.init');
  
    build() {
      Column() {
        Column() {
            Text(this.calleeDetail)
            .fontColor('#FFFFFF')
            .opacity(0.9)
            .fontSize(14)
            .margin({ top: '8%', left: '10%' })
        }.width('100%').height('50%')
        .alignItems(HorizontalAlign.Start)
  
        Row() {
          Button() {
            Text($r('app.string.CalleeJumpLabel'))
              .fontColor('#45A6F4')
              .fontSize(12)
          }
          .width(120)
          .height(32)
          .margin({ top: '30%', bottom: '10%' })
          .backgroundColor('#FFFFFF')
          .borderRadius(16)
          .onClick(() => {
            postCardAction(this, {
              action: 'call',
              abilityName: 'WidgetCalleeEntryAbility', // Only the UIAbility of the current application is allowed.
              params: {
                method: 'funA',
                formId: this.formId,
                calleeDetail: 'CallFrom'
              }
            });
          })
        }.width('100%').height('40%')
        .justifyContent(FlexAlign.Center)
      }
      .width('100%')
      .height('100%')
      .alignItems(HorizontalAlign.Start)
      .backgroundImage($r('app.media.CardEvent'))
      .backgroundImageSize(ImageSize.Cover)
    }
  }
  ```
  
- Listen for the method required by the call event in the **onCreate** callback of the UIAbility, and then call the [updateForm](../reference/apis-form-kit/js-apis-app-form-formProvider.md#updateform) API in the corresponding method to update the widget.
  
  ```ts
  import type AbilityConstant from '@ohos.app.ability.AbilityConstant';
  import type Base from '@ohos.base';
  import formBindingData from '@ohos.app.form.formBindingData';
  import formProvider from '@ohos.app.form.formProvider';
  import hilog from '@ohos.hilog';
  import type rpc from '@ohos.rpc';
  import UIAbility from '@ohos.app.ability.UIAbility';
  import type Want from '@ohos.app.ability.Want';
  import type window from '@ohos.window';
  
  const TAG: string = 'WidgetCalleeEntryAbility';
  const DOMAIN_NUMBER: number = 0xFF00;
  const MSG_SEND_METHOD: string = 'funA';
  const CONST_NUMBER_1: number = 1;
  
  class MyParcelable implements rpc.Parcelable {
    num: number;
    str: string;
  
    constructor(num: number, str: string) {
      this.num = num;
      this.str = str;
    };
  
    marshalling(messageSequence: rpc.MessageSequence): boolean {
      messageSequence.writeInt(this.num);
      messageSequence.writeString(this.str);
      return true;
    };
  
    unmarshalling(messageSequence: rpc.MessageSequence): boolean {
      this.num = messageSequence.readInt();
      this.str = messageSequence.readString();
      return true;
    };
  }
  
  // After the call event is received, the method listened for by the callee is triggered.
  let funACall = (data: rpc.MessageSequence): MyParcelable => {
    // Obtain all parameters transferred in the call event.
    let params: Record<string, string> = JSON.parse(data.readString());
    if (params.formId !== undefined) {
      let curFormId: string = params.formId;
      let message: string = params.calleeDetail;
      hilog.info(DOMAIN_NUMBER, TAG, `UpdateForm formId: ${curFormId}, message: ${message}`);
      let formData: Record<string, string> = {
        'calleeDetail': message
      };
      let formMsg: formBindingData.FormBindingData = formBindingData.createFormBindingData(formData);
      formProvider.updateForm(curFormId, formMsg).then((data) => {
        hilog.info(DOMAIN_NUMBER, TAG, `updateForm success. ${JSON.stringify(data)}`);
      }).catch((error: Base.BusinessError) => {
        hilog.error(DOMAIN_NUMBER, TAG, `updateForm failed: ${JSON.stringify(error)}`);
      });
    }
    return new MyParcelable(CONST_NUMBER_1, 'aaa');
  };
  
  export default class WidgetCalleeEntryAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
      try {
        // Listen for the method required by the call event.
        this.callee.on(MSG_SEND_METHOD, funACall);
      } catch (error) {
        hilog.error(DOMAIN_NUMBER, TAG, `${MSG_SEND_METHOD} register failed with error ${JSON.stringify(error)}`);
      };
    }
  
    onWindowStageCreate(windowStage: window.WindowStage): void {
      // Main window is created, set main page for this ability
      hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', 'Ability onWindowStageCreate');
  
      windowStage.loadContent('pages/Index', (err, data) => {
        if (err.code) {
          hilog.error(DOMAIN_NUMBER, TAG, 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
          return;
        }
        hilog.info(DOMAIN_NUMBER, TAG, 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
      });
    }
  }
  ```
