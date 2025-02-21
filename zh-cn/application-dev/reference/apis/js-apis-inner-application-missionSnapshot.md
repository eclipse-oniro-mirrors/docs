# MissionSnapshot

一个任务的任务快照对象，可以通过[missionManager.getMissionSnapShot](js-apis-app-ability-missionManager.md#missionmanagergetmissionsnapshot)获取。

> **说明：**
> 
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 本模块接口均为系统接口，三方应用不支持调用。

## 导入模块

```ts
import missionManager from '@ohos.app.ability.missionManager';
```

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Mission

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| ability | ElementName | 是 | 是 | 表示该任务的组件信息。 |
| snapshot | [PixelMap](js-apis-image.md#pixelmap7) | 是 | 是 | 表示任务快照。 |

## 使用说明

通过missionManager中的getMissionSnapShot来获取。

**示例：**
```ts
import ElementName from '@ohos.bundle';
import image from '@ohos.multimedia.image';
import missionManager from '@ohos.application.missionManager';

missionManager.getMissionInfos('', 10, (error, missions) => {
  console.log('getMissionInfos is called, error.code = ' + error.code);
  console.log('size = ' + missions.length);
  console.log('missions = ' + JSON.stringify(missions));
  let id = missions[0].missionId;

  missionManager.getMissionSnapShot('', id, (error, snapshot) => {
    console.log('getMissionSnapShot is called, error.code = ' + error.code);
    console.log('bundleName = ' + snapshot.ability.bundleName);
  });
});
```