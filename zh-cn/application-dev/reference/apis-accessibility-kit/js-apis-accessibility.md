# @ohos.accessibility (辅助功能)

本模块提供辅助功能查询能力，包括获取辅助应用列表、辅助应用启用状态、无障碍字幕配置等。

> **说明：**
>
> - 本模块首批接口从 API version 7 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import accessibility from '@ohos.accessibility';
```

## AbilityState

辅助应用状态类型。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称      | 描述       |
| ------- | -------- |
| enable  | 辅助应用已启用。 |
| disable | 辅助应用已禁用。 |
| install | 辅助应用已安装。 |

## AbilityType

无障碍辅助应用类型。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称               | 描述        |
| ---------------- | --------- |
| audible          | 表示具有听觉反馈。 |
| generic          | 表示具有通用反馈。 |
| haptic           | 表示具有触觉反馈。 |
| spoken           | 表示具有语音反馈。 |
| visual           | 表示具有视觉反馈。 |
| all<sup>9+</sup> | 表示以上所有类别。 |

## AccessibilityAbilityInfo

辅助应用信息。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

### 属性

| 名称                             | 类型                                       | 可读   | 可写   | 说明               |
| ------------------------------ | ---------------------------------------- | ---- | ---- | ---------------- |
| id                             | string                                   | 是    | 否    | ability&nbsp;id。 |
| name                           | string                                   | 是    | 否    | ability 名。       |
| bundleName                     | string                                   | 是    | 否    | Bundle名称。        |
| targetBundleNames<sup>9+</sup> | Array&lt;string&gt;                      | 是    | 否    | 关注的目标Bundle名称。   |
| abilityTypes                   | Array&lt;[AbilityType](#abilitytype)&gt; | 是    | 否    | 辅助应用类型。          |
| capabilities                   | Array&lt;[Capability](#capability)&gt;   | 是    | 否    | 辅助应用能力列表。        |
| description                    | string                                   | 是    | 否    | 辅助应用描述。          |
| eventTypes                     | Array&lt;[EventType](#eventtype)&gt;     | 是    | 否    | 辅助应用关注的无障碍事件列表。  |

## Action

应用所支持的目标动作，需要配置参数的目标动作已在描述中标明。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称                      | 描述                 |
| ----------------------- |--------------------|
| click                   | 表示点击操作。            |
| longClick               | 表示长按操作。            |
| scrollForward           | 表示向前滚动操作。 |
| scrollBackward          | 表示向后滚动操作。 |
| focus                   | 表示获得焦点操作。 |
| clearFocus              | 表示清除焦点操作。 |
| clearSelection          | 表示清除选择操作。当前版本暂不支持。 |
| accessibilityFocus      | 表示获得无障碍焦点操作。       |
| clearAccessibilityFocus | 表示清除无障碍焦点操作。       |
| cut                     | 表示剪切操作。   |
| copy                    | 表示复制操作。   |
| paste                   | 表示粘贴操作。   |
| select                  | 表示选择操作。当前版本暂不支持。   |
| setText                 | 表示设置文本操作，需要配置参数setText。当前版本暂不支持。 |
| delete                  | 表示删除操作。当前版本暂不支持。   |
| setSelection            | 表示选择操作，需配置参数selectTextBegin、selectTextEnd。   |

## Capability

辅助应用能力类型。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称               | 描述                    |
| ---------------- |-----------------------|
| retrieve         | 具有检索窗口内容的能力。          |
| touchGuide       | 具有触摸探索模式的能力。          |
| keyEventObserver | 具有过滤按键事件的能力。          |
| zoom             | 具有控制显示放大的能力。当前版本暂不支持。 |
| gesture          | 具有执行手势动作的能力。          |

## CaptionsFontEdgeType<sup>8+</sup>

字幕字体边缘类型。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Hearing

| 名称         | 描述    |
| ---------- | ----- |
| none       | 无效果。  |
| raised     | 凸起效果。 |
| depressed  | 凹陷效果。 |
| uniform    | 轮廓效果。 |
| dropShadow | 阴影效果。 |

## CaptionsFontFamily<sup>8+</sup>

字幕字体。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Hearing

| 名称                  | 描述                |
| ------------------- | ----------------- |
| default             | 默认字体。             |
| monospacedSerif     | 等宽 Serif 字体。      |
| serif               | Serif 字体。         |
| monospacedSansSerif | 等宽 Sans Serif 字体。 |
| sansSerif           | Sans Serif 字体。    |
| casual              | 非正式字体。            |
| cursive             | 手写字体。             |
| smallCapitals       | 小型大写字母字体。         |

## CaptionsStyle<sup>8+</sup>

字幕风格。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Hearing

| 名称              | 类型                                       | 可读   | 可写   | 说明          |
| --------------- | ---------------------------------------- | ---- | ---- | ----------- |
| fontFamily      | [CaptionsFontFamily](#captionsfontfamily8) | 是    | 否    | 描述字幕字体。     |
| fontScale       | number                                   | 是    | 否    | 描述字幕字体缩放系数，单位%，参数范围1~200。 |
| fontColor       | number \| string                         | 是    | 否    | 描述字幕字体颜色，例如red对应#FF0000。   |
| fontEdgeType    | [CaptionsFontEdgeType](#captionsfontedgetype8) | 是    | 否    | 描述字幕字体边缘。   |
| backgroundColor | number \| string                         | 是    | 否    | 描述字幕背景颜色，例如red对应#FF0000。   |
| windowColor     | number \| string                         | 是    | 否    | 描述字幕窗口颜色，例如red对应#FF0000。   |

## CaptionsManager<sup>8+</sup>

字幕配置管理，在调用CaptionsManager的方法前，需要先通过 [accessibility.getCaptionsManager() ](#accessibilitygetcaptionsmanager8)获取 CaptionsManager实例。

**系统能力**：以下各项对应的系统能力均为SystemCapability.BarrierFree.Accessibility.Hearing

### 属性

| 名称      | 类型                               | 可读   | 可写   | 说明          |
| ------- | -------------------------------- | ---- | ---- | ----------- |
| enabled | boolean                          | 是    | 否    | 表示是否启用字幕配置。 |
| style   | [CaptionsStyle](#captionsstyle8) | 是    | 否    | 表示字幕风格。     |

boolean返回值的含义：True表示开启，False表示关闭。

### on('enableChange')

on(type: 'enableChange', callback: Callback&lt;boolean&gt;): void;

监听字幕配置启用状态变化事件，使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Hearing

**参数：**

| 参数名      | 类型                      | 必填   | 说明                                      |
| -------- | ----------------------- | ---- | --------------------------------------- |
| type     | string                  | 是    | 监听的事件名，固定为‘enableChange’，即字幕配置启用状态变化事件。 |
| callback | Callback&lt;boolean&gt; | 是    | 回调函数，在启用状态变化时将状态通过此函数进行通知。              |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

let captionsManager = accessibility.getCaptionsManager();
captionsManager.on('enableChange', (data: boolean) => {
  console.info(`subscribe caption manager enable state change, result: ${JSON.stringify(data)}`);
})
```

### on('styleChange')

on(type: 'styleChange', callback: Callback&lt;CaptionsStyle&gt;): void;

监听字幕风格变化事件，使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Hearing

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                 |
| -------- | ---------------------------------------- | ---- | ---------------------------------- |
| type     | string                                   | 是    | 监听的事件名，固定为‘styleChange’，即字幕风格变化事件。 |
| callback | Callback&lt;[CaptionsStyle](#captionsstyle8)&gt; | 是    | 回调函数，在字幕风格变化时通过此函数进行通知。            |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

let captionsManager = accessibility.getCaptionsManager();

captionsManager.on('styleChange', (data: accessibility.CaptionsStyle) => {
  console.info(`subscribe caption manager style state change, result: ${JSON.stringify(data)}`);
});
```

### off('enableChange')

off(type: 'enableChange', callback?: Callback&lt;boolean&gt;): void;

取消监听字幕配置启用状态变化事件，使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Hearing

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                         |
| -------- | ----------------------- | ---- | ------------------------------------------------------------ |
| type     | string                  | 是   | 取消监听的事件名，固定为‘enableChange’，即字幕配置启用状态变化事件。 |
| callback | Callback&lt;boolean&gt; | 否   | 回调函数，取消指定callback对象的事件响应。需与on('enableChange')的callback一致。缺省时，表示注销所有已注册事件。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

let captionsManager = accessibility.getCaptionsManager();

captionsManager.off('enableChange', (data: boolean) => {
  console.info(`Unsubscribe caption manager enable state change, result: ${JSON.stringify(data)}`);
});
```

### off('styleChange')

off(type: 'styleChange', callback?: Callback&lt;CaptionsStyle&gt;): void;

取消字幕风格变化监听事件，使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Hearing

**参数：**

| 参数名   | 类型                                             | 必填 | 说明                                                         |
| -------- | ------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                           | 是   | 取消监听的事件名，固定为‘styleChange’，即字幕风格变化事件。  |
| callback | Callback&lt;[CaptionsStyle](#captionsstyle8)&gt; | 否   | 回调函数，取消指定callback对象的事件响应。需与on('styleChange')的callback一致。缺省时，表示注销所有已注册事件。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

let captionsManager = accessibility.getCaptionsManager();

captionsManager.off('styleChange', (data: accessibility.CaptionsStyle) => {
  console.info(`Unsubscribe caption manager style state change, result: ${JSON.stringify(data)}`);
});
```

## EventInfo

界面变更事件。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

### 属性

| 名称               | 类型                                    | 必填  | 说明                    |
| ---------------- | ------------------------------------- |-----|-----------------------|
| type             | [EventType](#eventtype)               | 是   | 无障碍事件类型；不可缺省。         |
| windowUpdateType | [WindowUpdateType](#windowupdatetype) | 否   | 窗口变化类型。               |
| bundleName       | string                                | 是   | 目标应用名；不可缺省。           |
| componentType    | string                                | 否   | 事件源组件类型，如按钮、图表。       |
| pageId           | number                                | 否   | 事件源的页面 ID。            |
| description      | string                                | 否   | 事件描述。当前版本暂不支持。        |
| triggerAction    | [Action](#action)                     | 是   | 触发事件的 Action；不可缺省。    |
| textMoveUnit     | [TextMoveUnit](#textmoveunit)         | 否   | 文本移动粒度。当前版本暂不支持。      |
| contents         | Array&lt;string&gt;                   | 否   | 内容列表。                 |
| lastContent      | string                                | 否   | 最新内容。                 |
| beginIndex       | number                                | 否   | 画面显示条目的开始序号。当前版本暂不支持。 |
| currentIndex     | number                                | 否   | 当前条目序号。当前版本暂不支持。      |
| endIndex         | number                                | 否   | 画面显示条目的结束序号。当前版本暂不支持。 |
| itemCount        | number                                | 否   | 条目总数。当前版本暂不支持。        |

### constructor

constructor(jsonObject)

构造函数。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名        | 类型     | 必填   | 说明                   |
| ---------- | ------ | ---- | -------------------- |
| jsonObject | string | 是    | 创建对象所需要的 JSON 格式字符串。 |

**示例：**

  ```ts
  import accessibility from '@ohos.accessibility';

  let eventInfo: accessibility.EventInfo = ({
    type: 'click',
    bundleName: 'com.example.MyApplication',
    triggerAction: 'click',
  });
  ```

### constructor<sup>11+</sup>

constructor(type: EventType, bundleName: string, triggerAction: Action)

构造函数。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名  | 类型                | 必填 | 说明            |
|------|-------------------|---|---------------|
| type | [EventType](#eventtype)          | 是 | 无障碍事件类型。      |
| bundleName | string | 是 | 目标应用名。        |
| triggerAction | [Action](#action) | 是 | 触发事件的 Action。 |

**示例：**

  ```ts
  import accessibility from '@ohos.accessibility';

  let eventInfo = new accessibility.EventInfo('click', 'com.example.MyApplication', 'click');
  ```

## EventType

无障碍事件类型。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称                      | 描述                     |
| ----------------------- |------------------------|
| accessibilityFocus      | 描述获得无障碍焦点的事件。          |
| accessibilityFocusClear | 描述清除无障碍焦点的事件。          |
| click                   | 描述点击组件的事件。             |
| longClick               | 描述长按组件的事件。             |
| select                  | 描述选择组件的事件。    |
| hoverEnter              | 描述悬停进入组件的事件。当前版本暂不支持。  |
| hoverExit               | 描述悬停离开组件的事件。当前版本暂不支持。  |
| focus                   | 描述组件获得焦点的事件。当前版本暂不支持。  |
| textUpdate              | 描述组件文本已更改的事件。 |
| textSelectionUpdate     | 描述选定文本已更改的事件。当前版本暂不支持。 |
| scroll                  | 描述滚动视图的事件。    |


## TextMoveUnit

文本无障碍导航移动粒度。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称        | 描述              |
| --------- | --------------- |
| char      | 以字符为移动粒度遍历节点文本。 |
| word      | 以词为移动粒度遍历节点文本。  |
| line      | 以行为移动粒度遍历节点文本。  |
| page      | 以页为移动粒度遍历节点文本。  |
| paragraph | 以段落为移动粒度遍历节点文本。 |

## WindowUpdateType

窗口变化类型。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称     | 描述                 |
| ------ | ------------------ |
| add    | 添加窗口的窗口变化事件。       |
| remove | 一个窗口被删除的窗口变化事件。    |
| bounds | 窗口边界已更改的窗口变化事件。    |
| active | 窗口变为活动或不活动的窗口变化事件。 |
| focus  | 窗口焦点发生变化的窗口变化事件。   |

## accessibility.getAbilityLists<sup>(deprecated)</sup>

getAbilityLists(abilityType: AbilityType, stateType: AbilityState): Promise&lt;Array&lt;AccessibilityAbilityInfo&gt;&gt;

查询辅助应用列表，使用Promise异步回调。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃。
> 推荐使用[accessibility.getAccessibilityExtensionList()](#accessibilitygetaccessibilityextensionlist9)。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名         | 类型                            | 必填   | 说明       |
| ----------- | ----------------------------- | ---- | -------- |
| abilityType | [AbilityType](#abilitytype)   | 是    | 辅助应用的类型。 |
| stateType   | [AbilityState](#abilitystate) | 是    | 辅助应用的状态。 |

**返回值：**

| 类型                                       | 说明                    |
| ---------------------------------------- | --------------------- |
| Promise&lt;Array&lt;[AccessibilityAbilityInfo](#accessibilityabilityinfo)&gt;&gt; | Promise对象，返回辅助应用信息列表。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

let abilityType: accessibility.AbilityType = 'spoken';
let abilityState: accessibility.AbilityState = 'enable';

accessibility.getAbilityLists(abilityType, abilityState).then((data: accessibility.AccessibilityAbilityInfo[]) => {
  console.info(`Succeeded in get accessibility extension list, ${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.error(`failed to get accessibility extension list because ${JSON.stringify(err)}`);
});
```

## accessibility.getAbilityLists<sup>(deprecated)</sup>

getAbilityLists(abilityType: AbilityType, stateType: AbilityState,callback: AsyncCallback&lt;Array&lt;AccessibilityAbilityInfo&gt;&gt;): void

查询辅助应用列表，使用callback异步回调。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃。
> 推荐使用[accessibility.getAccessibilityExtensionList()](#accessibilitygetaccessibilityextensionlist9-1)。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名         | 类型                                       | 必填   | 说明               |
| ----------- | ---------------------------------------- | ---- | ---------------- |
| abilityType | [AbilityType](#abilitytype)              | 是    | 辅助应用的类型。         |
| stateType   | [AbilityState](#abilitystate)            | 是    | 辅助应用的状态。         |
| callback    | AsyncCallback&lt;Array&lt;[AccessibilityAbilityInfo](#accessibilityabilityinfo)&gt;&gt; | 是    | 回调函数，返回辅助应用信息列表。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

let abilityType: accessibility.AbilityType = 'spoken';
let abilityState: accessibility.AbilityState = 'enable';

accessibility.getAbilityLists(abilityType, abilityState, (err: BusinessError, data: accessibility.AccessibilityAbilityInfo[]) => {
  if (err) {
    console.error(`failed to get accessibility extension list because ${JSON.stringify(err)}`);
    return;
  }
  console.info(`Succeeded in get accessibility extension list, ${JSON.stringify(data)}`);
})
```

## accessibility.getAccessibilityExtensionList<sup>9+</sup>

getAccessibilityExtensionList(abilityType: AbilityType, stateType: AbilityState): Promise&lt;Array&lt;AccessibilityAbilityInfo&gt;&gt;

查询辅助应用列表，使用Promise异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名         | 类型                            | 必填   | 说明       |
| ----------- | ----------------------------- | ---- | -------- |
| abilityType | [AbilityType](#abilitytype)   | 是    | 辅助应用的类型。 |
| stateType   | [AbilityState](#abilitystate) | 是    | 辅助应用的状态。 |

**返回值：**

| 类型                                       | 说明                    |
| ---------------------------------------- | --------------------- |
| Promise&lt;Array&lt;[AccessibilityAbilityInfo](#accessibilityabilityinfo)&gt;&gt; | Promise对象，返回辅助应用信息列表。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

let abilityType: accessibility.AbilityType = 'spoken';
let abilityState: accessibility.AbilityState = 'enable';

accessibility.getAccessibilityExtensionList(abilityType, abilityState).then((data: accessibility.AccessibilityAbilityInfo[]) => {
  console.info(`Succeeded in get accessibility extension list, ${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.error(`failed to get accessibility extension list, Code is ${err.code}, message is ${err.message}`);
});
```

## accessibility.getAccessibilityExtensionList<sup>9+</sup>

getAccessibilityExtensionList(abilityType: AbilityType, stateType: AbilityState, callback: AsyncCallback&lt;Array&lt;AccessibilityAbilityInfo&gt;&gt;): void

查询辅助应用列表，使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名         | 类型                                       | 必填   | 说明               |
| ----------- | ---------------------------------------- | ---- | ---------------- |
| abilityType | [AbilityType](#abilitytype)              | 是    | 辅助应用的类型。         |
| stateType   | [AbilityState](#abilitystate)            | 是    | 辅助应用的状态。         |
| callback    | AsyncCallback&lt;Array&lt;[AccessibilityAbilityInfo](#accessibilityabilityinfo)&gt;&gt; | 是    | 回调函数，返回辅助应用信息列表。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

let abilityType: accessibility.AbilityType = 'spoken';
let abilityState: accessibility.AbilityState = 'enable';

accessibility.getAccessibilityExtensionList(abilityType, abilityState,(err: BusinessError, data: accessibility.AccessibilityAbilityInfo[]) => {
  if (err) {
    console.error(`failed to get accessibility extension list, Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.info(`Succeeded in get accessibility extension list, ${JSON.stringify(data)}`);
});
```

## accessibility.getCaptionsManager<sup>8+</sup>

getCaptionsManager(): CaptionsManager

获取无障碍字幕配置管理实例。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Hearing

**返回值：**

| 类型                                   | 说明         |
| ------------------------------------ | ---------- |
| [CaptionsManager](#captionsmanager8) | 无障碍字幕配置管理。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

let captionsManager = accessibility.getCaptionsManager();
```

## accessibility.on('accessibilityStateChange')

on(type: 'accessibilityStateChange', callback: Callback&lt;boolean&gt;): void

监听辅助应用启用状态变化事件，使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                         |
| -------- | ----------------------- | ---- | ------------------------------------------------------------ |
| type     | string                  | 是   | 监听的事件名，固定为‘accessibilityStateChange’，即辅助应用启用状态变化事件。 |
| callback | Callback&lt;boolean&gt; | 是   | 回调函数，在辅助应用启用状态变化时将状态通过此函数进行通知。此状态为全局辅助应用启用状态。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

accessibility.on('accessibilityStateChange', (data: boolean) => {
  console.info(`subscribe accessibility state change, result: ${JSON.stringify(data)}`);
});
```

## accessibility.on('touchGuideStateChange')

on(type: 'touchGuideStateChange', callback: Callback&lt;boolean&gt;): void

监听触摸浏览功能启用状态变化事件，使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Vision

**参数：**

| 参数名      | 类型                      | 必填   | 说明                                       |
| -------- | ----------------------- | ---- | ---------------------------------------- |
| type     | string                  | 是    | 监听的事件名，固定为‘touchGuideStateChange’，即触摸浏览启用状态变化事件。 |
| callback | Callback&lt;boolean&gt; | 是    | 回调函数，在触摸浏览启用状态变化时将状态通过此函数进行通知。           |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

accessibility.on('touchGuideStateChange', (data: boolean) => {
  console.info(`subscribe touch guide state change, result: ${JSON.stringify(data)}`);
});
```

## accessibility.off('accessibilityStateChange')

off(type: 'accessibilityStateChange', callback?: Callback&lt;boolean&gt;): void

取消监听辅助应用启用状态变化事件，使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                         |
| -------- | ----------------------- | ---- | ------------------------------------------------------------ |
| type     | string                  | 是   | 取消监听的事件名，固定为‘accessibilityStateChange’，即辅助应用启用状态变化事件。 |
| callback | Callback&lt;boolean&gt; | 否   | 回调函数，取消指定callback对象的事件响应。需与accessibility.on('accessibilityStateChange')的callback一致。缺省时，表示注销所有已注册事件。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

accessibility.off('accessibilityStateChange', (data: boolean) => {
  console.info(`Unsubscribe accessibility state change, result: ${JSON.stringify(data)}`);
});
```

## accessibility.off('touchGuideStateChange')

off(type: 'touchGuideStateChange', callback?: Callback&lt;boolean&gt;): void

取消监听触摸浏览启用状态变化事件，使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                         |
| -------- | ----------------------- | ---- | ------------------------------------------------------------ |
| type     | string                  | 是   | 取消监听的事件名，固定为‘touchGuideStateChange’，即触摸浏览启用状态变化事件。 |
| callback | Callback&lt;boolean&gt; | 否   | 回调函数，取消指定callback对象的事件响应。需与accessibility.on('touchGuideStateChange')的callback一致。缺省时，表示注销所有已注册事件。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

accessibility.off('touchGuideStateChange', (data: boolean) => {
  console.info(`Unsubscribe touch guide state change, result: ${JSON.stringify(data)}`);
});
```

## accessibility.isOpenAccessibility<sup>(deprecated)</sup>

isOpenAccessibility(): Promise&lt;boolean&gt;

判断是否启用了辅助功能, 使用Promise异步回调。

> **说明：**
>
> 从API version 10开始废弃。
>
> 推荐使用[accessibility.isOpenAccessibilitySync](#accessibilityisopenaccessibilitysync10)。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**返回值：**

| 类型                     | 说明                                       |
| ---------------------- | ---------------------------------------- |
| Promise&lt;boolean&gt; | Promise对象，如果辅助功能已启用，则返回 true；否则返回 false。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

accessibility.isOpenAccessibility().then((data: boolean) => {
  console.info(`success data:isOpenAccessibility : ${JSON.stringify(data)}`)
}).catch((err: BusinessError) => {
  console.error(`failed to  isOpenAccessibility, Code is ${err.code}, message is ${err.message}`);
});
```

## accessibility.isOpenAccessibility<sup>(deprecated)</sup>

isOpenAccessibility(callback: AsyncCallback&lt;boolean&gt;): void

判断是否启用了辅助功能，使用callback异步回调。

> **说明：**
>
> 从API version 10开始废弃。
>
> 推荐使用[accessibility.isOpenAccessibilitySync](#accessibilityisopenaccessibilitysync10)。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名      | 类型                           | 必填   | 说明                                  |
| -------- | ---------------------------- | ---- | ----------------------------------- |
| callback | AsyncCallback&lt;boolean&gt; | 是    | 回调函数，如果辅助功能已启用，则返回 true；否则返回 false。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

accessibility.isOpenAccessibility((err: BusinessError, data: boolean) => {
  if (err) {
    console.error(`failed to isOpenAccessibility, Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.info(`success data:isOpenAccessibility : ${JSON.stringify(data)}`);
});
```

## accessibility.isOpenAccessibilitySync<sup>10+</sup>

isOpenAccessibilitySync(): boolean

是否启用了辅助功能。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**返回值：**

| 类型        | 说明                                  |
| ----------- | ------------------------------------- |
| boolean | 启用辅助功能返回true，否则返回false。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

let status: boolean = accessibility.isOpenAccessibilitySync();
```

## accessibility.isOpenTouchGuide<sup>(deprecated)</sup>

isOpenTouchGuide(): Promise&lt;boolean&gt;

判断触摸浏览模式是否开启, 使用Promise异步回调。

> **说明：**
>
> 从API version 10开始废弃。
>
> 推荐使用[accessibility.isOpenTouchGuideSync](#accessibilityisopentouchguidesync10)。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Vision

**返回值：**

| 类型                     | 说明                                       |
| ---------------------- | ---------------------------------------- |
| Promise&lt;boolean&gt; | Promise对象，如果触摸浏览模式已开启，则返回 true；否则返回 false。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

accessibility.isOpenTouchGuide().then((data: boolean) => {
  console.info(`success data:isOpenTouchGuide : ${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.error(`failed to  isOpenTouchGuide, Code is ${err.code}, message is ${err.message}`);
});
```

## accessibility.isOpenTouchGuide<sup>(deprecated)</sup>

isOpenTouchGuide(callback: AsyncCallback&lt;boolean&gt;): void

判断触摸浏览模式是否开启, 使用callback异步回调。

> **说明：**
>
> 从API version 10开始废弃。
>
> 推荐使用[accessibility.isOpenTouchGuideSync](#accessibilityisopentouchguidesync10)。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Vision

**参数：**

| 参数名      | 类型                           | 必填   | 说明                                    |
| -------- | ---------------------------- | ---- | ------------------------------------- |
| callback | AsyncCallback&lt;boolean&gt; | 是    | 回调函数，如果触摸浏览模式已开启，则返回 true；否则返回 false。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

accessibility.isOpenTouchGuide((err: BusinessError, data: boolean) => {
  if (err) {
    console.error(`failed to isOpenTouchGuide, Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.info(`success data:isOpenTouchGuide : ${JSON.stringify(data)}`);
});
```

## accessibility.isOpenTouchGuideSync<sup>10+</sup>

isOpenTouchGuideSync(): boolean

是否开启了触摸浏览模式。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Vision

**返回值：**

| 类型    | 说明                                  |
| ------- | ------------------------------------- |
| boolean | 启用辅助功能返回true，否则返回false。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';

let status: boolean = accessibility.isOpenTouchGuideSync();
```

## accessibility.sendEvent<sup>(deprecated)</sup>

sendEvent(event: EventInfo): Promise&lt;void&gt;

发送无障碍事件, 使用Promise异步回调。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃。
> 推荐使用[accessibility.sendAccessibilityEvent()](#accessibilitysendaccessibilityevent9)。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名   | 类型                      | 必填   | 说明       |
| ----- | ----------------------- | ---- | -------- |
| event | [EventInfo](#eventinfo) | 是    | 无障碍事件对象。 |

**返回值：**

| 类型                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

let eventInfo: accessibility.EventInfo = ({
  type: 'click',
  bundleName: 'com.example.MyApplication',
  triggerAction: 'click',
});

accessibility.sendEvent(eventInfo).then(() => {
  console.info(`Succeeded in send event,eventInfo is ${eventInfo}`);
}).catch((err: BusinessError) => {
  console.error(`failed to sendEvent, Code is ${err.code}, message is ${err.message}`);
});
```

## accessibility.sendEvent<sup>(deprecated)</sup>

sendEvent(event: EventInfo, callback: AsyncCallback&lt;void&gt;): void

发送无障碍事件, 使用callback异步回调。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃。
> 推荐使用[accessibility.sendAccessibilityEvent()](#accessibilitysendaccessibilityevent9-1)。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明                                       |
| -------- | ------------------------- | ---- | ---------------------------------------- |
| event    | [EventInfo](#eventinfo)   | 是    | 辅助事件对象。                                  |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数，如果发送无障碍事件失败，则 AsyncCallback中err有数据返回。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

let eventInfo: accessibility.EventInfo = ({
  type: 'click',
  bundleName: 'com.example.MyApplication',
  triggerAction: 'click',
});

accessibility.sendEvent(eventInfo, (err: BusinessError) => {
  if (err) {
    console.error(`failed to sendEvent, Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.info(`Succeeded in sendEvent, eventInfo is ${eventInfo}`);
});
```

## accessibility.sendAccessibilityEvent<sup>9+</sup>

sendAccessibilityEvent(event: EventInfo): Promise&lt;void&gt;

发送无障碍事件, 使用Promise异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名   | 类型                      | 必填   | 说明       |
| ----- | ----------------------- | ---- | -------- |
| event | [EventInfo](#eventinfo) | 是    | 无障碍事件对象。 |

**返回值：**

| 类型                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

let eventInfo: accessibility.EventInfo = ({
  type: 'click',
  bundleName: 'com.example.MyApplication',
  triggerAction: 'click',
});

accessibility.sendAccessibilityEvent(eventInfo).then(() => {
  console.info(`Succeeded in send event,eventInfo is ${eventInfo}`);
}).catch((err: BusinessError) => {
  console.error(`failed to send event , Code is ${err.code}, message is ${err.message}`);
});
```

## accessibility.sendAccessibilityEvent<sup>9+</sup>

sendAccessibilityEvent(event: EventInfo, callback: AsyncCallback&lt;void&gt;): void

发送无障碍事件, 使用callback异步回调。

**系统能力**：SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明                                       |
| -------- | ------------------------- | ---- | ---------------------------------------- |
| event    | [EventInfo](#eventinfo)   | 是    | 辅助事件对象。                                  |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数，如果发送无障碍事件失败，则 AsyncCallback中err有数据返回。 |

**示例：**

```ts
import accessibility from '@ohos.accessibility';
import { BusinessError } from '@ohos.base';

let eventInfo: accessibility.EventInfo = ({
  type: 'click',
  bundleName: 'com.example.MyApplication',
  triggerAction: 'click',
});

accessibility.sendAccessibilityEvent(eventInfo, (err: BusinessError) => {
  if (err) {
    console.error(`failed to send event, Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.info(`Succeeded in send event, eventInfo is ${eventInfo}`);
});
```
