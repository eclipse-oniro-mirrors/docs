# MissionListener

定义系统任务状态监听，可以通过[registerMissionListener](js-apis-application-missionManager.md#missionmanagerregistermissionlistener)注册。

> **说明：**
> 
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。 

## 导入模块

```ts
import missionManager from '@ohos.app.ability.missionManager';
```

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Mission

| 名称        | 类型                 | 必填 | 说明                                                         |
| ----------- | -------- | ---- | ------------------------------------------------------------ |
| onMissionCreated    | function               | 否   | 表示当系统创建任务时回调执行。                                |
| onMissionDestroyed   | function               | 否   | 表示当系统销毁任务时回调执行。 |
| onMissionSnapshotChanged   | function               | 否   | 表示当系统更新任务缩略图时回调执行。 |
| onMissionMovedToFront   | function               | 否   | 表示当系统将任务移动到前台时回调执行。 |
| onMissionLabelUpdated<sup>9+</sup>   | function               | 否   | 表示当系统更新任务标签时回调执行。 |
| onMissionIconUpdated<sup>9+</sup>   | function               | 否   | 表示当系统更新任务图标时回调执行。 |
| onMissionClosed<sup>9+</sup>   | function               | 否   | 表示当系统关闭任务时回调执行。 |

**示例：**
```ts
import missionManager from '@ohos.application.missionManager';

let listener = {
    onMissionCreated: function (mission) {
        console.log('onMissionCreated mission: ' + JSON.stringify(mission));
    },
    onMissionDestroyed: function (mission) {
        console.log('onMissionDestroyed mission: ' + JSON.stringify(mission));
    },
    onMissionSnapshotChanged: function (mission) {
        console.log('onMissionSnapshotChanged mission: ' + JSON.stringify(mission));
    },
    onMissionMovedToFront: function (mission) {
        console.log('onMissionMovedToFront mission: ' + JSON.stringify(mission));
    },
    onMissionLabelUpdated: function (mission) {
        console.log('onMissionLabelUpdated mission: ' + JSON.stringify(mission));
    },
    onMissionIconUpdated: function (mission, icon) {
        console.log('onMissionIconUpdated mission: ' + JSON.stringify(mission));
        console.log('onMissionIconUpdated icon: ' + JSON.stringify(icon));
    },
    onMissionClosed: function (mission) {
        console.log('onMissionClosed mission: ' + JSON.stringify(mission));
    }
};
let listenerid = missionManager.registerMissionListener(listener);
```