# @ohos.PiPWindow (画中画窗口)

该模块提供画中画基础功能，包括判断当前系统是否开启画中画功能，以及创建画中画控制器用于启动、停止画中画等。主要用于视频播放、视频通话或视频会议场景下，以小窗（画中画）模式呈现内容。

> **说明：**
>
> 本模块首批接口从API version 11开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 
> 需要在支持SystemCapability.Window.SessionManager能力的系统上使用该模块，参考[系统能力SystemCapability使用指南](../syscap.md)。

## 导入模块

```ts
import pipWindow from '@ohos.PiPWindow';
```

## pipWindow.isPiPEnabled

isPiPEnabled(): boolean

用于判断当前系统是否开启画中画功能。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型       | 说明                                  |
|----------|-------------------------------------|
| boolean  | 当前系统是否开启画中画功能。true表示开启，false则表示未开启。 |

**示例：**

```ts
let enable: boolean = pipWindow.isPiPEnabled();
console.info('isPipEnabled:' + enable);
```

## pipWindow.create

create(config: PiPConfiguration): Promise&lt;PiPController&gt;

创建画中画控制器，使用Promise异步回调。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名          | 类型                                       | 必填        | 说明             |
|--------------|------------------------------------------|-----------|----------------|
| config       | [PiPConfiguration](#pipconfiguration)    | 是         | 创建画中画控制器的参数。   |

**返回值：**

| 类型                                                         | 说明                       |
|------------------------------------------------------------|--------------------------|
| Promise&lt;[PiPController](#pipcontroller)&gt;  | Promise对象。返回当前创建的画中画控制器。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
let pipController: pipWindow.PiPController | undefined = undefined;
let mXComponentController: XComponentController = new XComponentController(); // 开发者应使用该mXComponentController初始化XComponent: XComponent( {id: 'video', type: 'surface', controller: mXComponentController} )，保证XComponent的内容可以被迁移到画中画窗口。
let navId: string = "page_1"; // 假设当前页面的导航id为page_1，详见PiPConfiguration定义，具体导航名称由开发者自行定义。
let contentWidth: number = 800; // 假设当前内容宽度800px。
let contentHeight: number = 600; // 假设当前内容高度600px。
let config: pipWindow.PiPConfiguration = {
  context: getContext(this),
  componentController: mXComponentController,
  navigationId: navId,
  templateType: pipWindow.PiPTemplateType.VIDEO_PLAY,
  contentWidth: contentWidth,
  contentHeight: contentHeight,
};

let promise : Promise<pipWindow.PiPController> = pipWindow.create(config);
promise.then((data : pipWindow.PiPController) => {
  pipController = data;
  console.info(`Succeeded in creating pip controller. Data:${data}`);
}).catch((err: BusinessError) => {
  console.error(`Failed to create pip controller. Cause:${err.code}, message:${err.message}`);
});
```

## PiPConfiguration

创建画中画控制器时的参数。

**系统能力：** SystemCapability.Window.SessionManager

| 名称                  | 类型                                                                    | 必填  | 说明                                                                                                                                                                                                                                                                                                                                           |
|---------------------|-----------------------------------------------------------------------|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| context             | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md)               | 是   | 表示上下文环境。                                                                                                                                                                                                                                                                                                                                     |
| componentController | [XComponentController](arkui-ts/ts-basic-components-xcomponent.md) | 是   | 表示原始[XComponent](../../ui/arkts-common-components-xcomponent.md)控制器。                                                                                                                                                                                                                                                                         |
| navigationId        | string                                                                | 否   | 当前page导航id。<br/>1、UIAbility使用[Navigation](arkui-ts/ts-basic-components-navigation.md)管理页面，需要设置Navigation控件的id属性，并将该id设置给画中画控制器，确保还原场景下能够从画中画窗口恢复到原页面。<br/>2、UIAbility使用[Router](js-apis-router.md)管理页面时（画中画场景不推荐该导航方式），无需设置navigationId。注意：该场景下启动画中画后，不要进行页面切换，否则还原场景可能出现异常。<br/>3、UIAbility只有单页面时，无需设置navigationId，还原场景下也能够从画中画窗口恢复到原页面。 |
| templateType        | [PiPTemplateType](#piptemplatetype)                                   | 否   | 模板类型，用以区分视频播放、视频通话或视频会议。                                                                                                                                                                                                                                                                                                                     |
| contentWidth        | number                                                                | 否   | 原始内容宽度，单位为px。用于确定画中画窗口比例。                                                                                                                                                                                                                                                                                                                    |
| contentHeight       | number                                                                | 否   | 原始内容高度，单位为px。用于确定画中画窗口比例。                                                                                                                                                                                                                                                                                                                    |

## PiPTemplateType

画中画媒体类型枚举。

**系统能力：** SystemCapability.Window.SessionManager

| 名称            | 值   | 说明                                   |
|---------------|-----|--------------------------------------|
| VIDEO_PLAY    | 0   | 表示将要切换为画中画播放的媒体类型是视频，系统依此加载视频播放模板。   |
| VIDEO_CALL    | 1   | 表示将要切换为画中画播放的媒体类型是视频通话，系统依此加载视频通话模板。 |
| VIDEO_MEETING | 2   | 表示将要切换为画中画播放的媒体类型是视频会议，系统依此加载视频会议模板。 |
| VIDEO_LIVE    | 3   | 表示将要切换为画中画播放的媒体类型是直播，系统依此加载直播模板。     |

## PiPState

画中画生命周期状态枚举。

**系统能力：** SystemCapability.Window.SessionManager

| 名称                   | 值   | 说明                    |
|----------------------|-----|-----------------------|
| ABOUT_TO_START       | 1   | 表示画中画将要启动。            |
| STARTED              | 2   | 表示画中画已经启动。            |
| ABOUT_TO_STOP        | 3   | 表示画中画将要停止。            |
| STOPPED              | 4   | 表示画中画已经停止。            |
| ABOUT_TO_RESTORE     | 5   | 表示画中画将从小窗播放恢复到原始播放界面。 |
| ERROR                | 6   | 表示画中画生命周期执行过程出现了异常。   |

## PiPActionEventType

画中画控制事件类型，支持以下四种。

**系统能力：** SystemCapability.Window.SessionManager

| 类型                                              | 说明          |
|-------------------------------------------------|-------------|
| [PiPVideoActionEvent](#pipvideoactionevent)     | 视频播放控制事件类型。 |
| [PiPCallActionEvent](#pipcallactionevent)       | 视频通话控制事件类型。 |
| [PiPMeetingActionEvent](#pipmeetingactionevent) | 视频会议控制事件类型。 |
| [PiPLiveActionEvent](#pipliveactionevent)       | 直播控制事件类型。   |

## PiPVideoActionEvent

视频播放控制事件类型。

**系统能力：** SystemCapability.Window.SessionManager

| 名称                     | 类型       | 说明                                                                                                  |
|------------------------|----------|-----------------------------------------------------------------------------------------------------|
| PiPVideoActionEvent    | string   | 有以下取值：<br/>-'playbackStateChanged'：播放状态发生了变化。<br>-'nextVideo'：播放下一个视频。<br>-'previousVideo'：播放上一个视频。 |

## PiPCallActionEvent

视频通话控制事件类型。

**系统能力：** SystemCapability.Window.SessionManager

| 名称                     | 类型     | 说明                                                                                             |
|------------------------|--------|------------------------------------------------------------------------------------------------|
| PiPCallActionEvent     | string | 有以下取值：<br/>-'hangUp'：挂断视频通话。<br>-'micStateChanged'：打开或关闭麦克风。<br>-'videoStateChanged'：打开或关闭摄像头。 |

## PiPMeetingActionEvent

视频会议控制事件类型。

**系统能力：** SystemCapability.Window.SessionManager

| 名称                         | 类型         | 说明                                                                                              |
|----------------------------|------------|-------------------------------------------------------------------------------------------------|
| PiPMeetingActionEvent      | string     | 有以下取值：<br/>-'hangUp'：挂断视频会议。<br>-'voiceStateChanged'：静音或解除静音。<br>-'videoStateChanged'：打开或关闭摄像头。 |

## PiPLiveActionEvent

直播控制事件类型。

**系统能力：** SystemCapability.Window.SessionManager

| 名称                       | 类型           | 说明                                |
|--------------------------|--------------|-----------------------------------|
| PiPLiveActionEvent       | string       | 值为'playbackStateChanged'：播放或暂停直播。 |

## PiPController

画中画控制器实例。用于启动、停止画中画以及更新回调注册等。

下列API示例中都需先使用[pipWindow.create()](#pipwindowcreate)方法获取到PiPController实例，再通过此实例调用对应方法。

**系统能力：** SystemCapability.Window.SessionManager

### startPiP

startPiP(): Promise&lt;void&gt;

启动画中画，使用Promise异步回调。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型                     | 说明                 |
|------------------------|--------------------|
| Promise&lt;void&gt;    | 无返回结果的Promise对象。   |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID      | 错误信息                                                   |
|------------|--------------------------------------------------------|
| 1300012    | If PiP window state is abnormal.                       |
| 1300013    | Create pip window failed.                              |
| 1300014    | Error when load PiP window content or show PiP window. |
| 1300015    | If window has created.                                 |

**示例：**

```ts
let promise : Promise<void> = pipController.startPiP();
promise.then(() => {
  console.info(`Succeeded in starting pip.`);
}).catch((err: BusinessError) => {
  console.error(`Failed to start pip. Cause:${err.code}, message:${err.message}`);
});
```

### stopPiP

stopPiP(): Promise&lt;void&gt;

停止画中画，使用Promise异步回调。

**系统能力：** SystemCapability.Window.SessionManager

**返回值：**

| 类型                   | 说明                  |
|----------------------|---------------------|
| Promise&lt;void&gt;  | 无返回结果的Promise对象。    |

**错误码：**

以下错误码的详细介绍请参见[窗口错误码](errorcode-window.md)。

| 错误码ID   | 错误信息                             |
|---------|----------------------------------|
| 1300011 | Stop PiP window failed.          |
| 1300012 | If PiP window state is abnormal. |
| 1300015 | If window is stopping.           |

**示例：**

```ts
let promise : Promise<void> = pipController.stopPiP();
promise.then(() => {
  console.info(`Succeeded in stopping pip.`);
}).catch((err: BusinessError) => {
  console.error(`Failed to stop pip. Cause:${err.code}, message:${err.message}`);
});
```

### setAutoStartEnabled

setAutoStartEnabled(enable: boolean): void

设置是否需要在返回桌面时自动启动画中画。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名      | 类型        | 必填    | 说明                              |
|----------|-----------|-------|---------------------------------|
| enable   | boolean   | 是     | true表示设置返回桌面时自动启动画中画，否则为false。  |

**示例：**

```ts
let enable: boolean = true;
pipController.setAutoStartEnabled(enable);
```

### updateContentSize

updateContentSize(width: number, height: number): void

当媒体源切换时，向画中画控制器更新媒体源尺寸信息。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名    | 类型     | 必填  | 说明                           |
|--------|--------|-----|------------------------------|
| width  | number | 是   | 表示媒体内容宽度，单位为px。用于更新画中画窗口比例。   |
| height | number | 是   | 表示媒体内容高度，单位为px。用于更新画中画窗口比例。   |

**示例：**

```ts
let width: number = 540; // 假设当前内容宽度变为540px。
let height: number = 960; // 假设当前内容高度变为960px。
pipController.updateContentSize(width, height);
```

### on('stateChange')

on(type: 'stateChange', callback: (state: PiPState, reason: string) => void): void

开启画中画生命周期状态的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名        | 类型        | 必填   | 说明                                                                                                |
|------------|-----------|------|---------------------------------------------------------------------------------------------------|
| type       | string    | 是    | 监听事件，固定为'stateChange'，即画中画生命周期状态变化事件。                                                             |
| callback   | function  | 是    | 回调生命周期状态变化事件以及原因：<br/>state：[PiPState](#pipstate)，表示当前画中画生命周期状态；<br/>reason：string，表示当前生命周期的切换原因。 |

**示例：**

```ts
pipController.on('stateChange', (state: pipWindow.PiPState, reason: string) => {
  let curState: string = '';
  switch (state) {
    case pipWindow.PiPState.ABOUT_TO_START:
      curState = 'ABOUT_TO_START';
      break;
    case pipWindow.PiPState.STARTED:
      curState = 'STARTED';
      break;
    case pipWindow.PiPState.ABOUT_TO_STOP:
      curState = 'ABOUT_TO_STOP';
      break;
    case pipWindow.PiPState.STOPPED:
      curState = 'STOPPED';
      break;
    case pipWindow.PiPState.ABOUT_TO_RESTORE:
      curState = 'ABOUT_TO_RESTORE';
      break;
    case pipWindow.PiPState.ERROR:
      curState = 'ERROR';
      break;
    default:
      break;
  }
  console.info('stateChange:' + curState + ' reason:' + reason);
});
```

### off('stateChange')

off(type: 'stateChange'): void

关闭画中画生命周期状态的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名       | 类型            | 必填    | 说明                                     |
|-----------|---------------|-------|----------------------------------------|
| type      | string        | 是     | 监听事件，固定为'stateChange'，即画中画生命周期状态变化事件。  |

**示例：**

```ts
pipController.off('stateChange');
```

### on('controlPanelActionEvent')

on(type: 'controlPanelActionEvent', callback: (event: PiPActionEventType) => void): void

开启画中画控制事件的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名      | 类型         | 必填    | 说明                                                                                                                             |
|----------|------------|-------|--------------------------------------------------------------------------------------------------------------------------------|
| type     | string     | 是     | 监听事件，固定为'controlPanelActionEvent'，即画中画控制事件。                                                                                    |
| callback | function   | 是     | 回调画中画控制事件:<br/>event: [PiPActionEventType](#pipactioneventtype)，表示控制事件类型。应用依据控制事件做相应处理，如触发'playbackStateChanged'事件时，需要开始或停止视频。 |

**示例：**

```ts
pipController.on('controlPanelActionEvent', (event: pipWindow.PiPActionEventType) => {
  switch (event) {
    case 'playbackStateChanged':
      // 开始或停止视频
      break;
    case 'nextVideo':
      // 切换到下一个视频
      break;
    case 'previousVideo':
      // 切换到上一个视频
      break;
    default:
      break;
  }
  console.info('registerActionEventCallback, event:' + event);
});
```

### off('controlPanelActionEvent')

off(type: 'controlPanelActionEvent'): void

关闭画中画控制事件的监听。

**系统能力：** SystemCapability.Window.SessionManager

**参数：**

| 参数名        | 类型                           | 必填   | 说明                                            |
|------------|------------------------------|------|-----------------------------------------------|
| type       | string                       | 是    | 监听事件，固定为'controlPanelActionEvent'，即画中画控制事件。   |

**示例：**

```ts
pipController.off('controlPanelActionEvent');
```