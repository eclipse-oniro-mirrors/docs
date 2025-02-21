# @ohos.application.missionManager (missionManager)

The **missionManager** module provides APIs to lock, unlock, and clear missions, and switch a mission to the foreground.

> **NOTE**
> 
> The APIs of this module are supported since API version 8 and deprecated since API version 9. You are advised to use [@ohos.app.ability.missionManager](js-apis-app-ability-missionManager.md) instead. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import missionManager from '@ohos.application.missionManager';
```

## Required Permissions

ohos.permission.MANAGE_MISSIONS

## missionManager.registerMissionListener

registerMissionListener(listener: MissionListener): number;

Registers a listener to observe the mission status.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | listener | [MissionListener](js-apis-inner-application-missionListener.md) | Yes| Mission status listener to register.|

**Return value**

  | Type| Description|
  | -------- | -------- |
  | number | Index of the mission status listener, which is created by the system and allocated when the listener is registered.|

**Example**

```ts
let listener = {
    onMissionCreated: function (mission) {console.log('--------onMissionCreated-------');},
    onMissionDestroyed: function (mission) {console.log('--------onMissionDestroyed-------');},
    onMissionSnapshotChanged: function (mission) {console.log('--------onMissionSnapshotChanged-------');},
    onMissionMovedToFront: function (mission) {console.log('--------onMissionMovedToFront-------');},
    onMissionIconUpdated: function (mission, icon) {console.log('--------onMissionIconUpdated-------');},
    onMissionClosed: function (mission) {console.log('--------onMissionClosed-------');},
    onMissionLabelUpdated: function (mission) {console.log('--------onMissionLabelUpdated-------');}
};
console.log('registerMissionListener');
let listenerid = missionManager.registerMissionListener(listener);
```


## missionManager.unregisterMissionListener

unregisterMissionListener(listenerId: number, callback: AsyncCallback&lt;void&gt;): void;

Deregisters a mission status listener. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | listenerId | number | Yes| Index of the mission status listener to deregister. It is returned by **registerMissionListener()**.|
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

```ts
  let listener = {
      onMissionCreated: function (mission) {console.log('--------onMissionCreated-------');},
      onMissionDestroyed: function (mission) {console.log('--------onMissionDestroyed-------');},
      onMissionSnapshotChanged: function (mission) {console.log('--------onMissionSnapshotChanged-------');},
      onMissionMovedToFront: function (mission) {console.log('--------onMissionMovedToFront-------');},
      onMissionIconUpdated: function (mission, icon) {console.log('--------onMissionIconUpdated-------');},
      onMissionClosed: function (mission) {console.log('--------onMissionClosed-------');},
      onMissionLabelUpdated: function (mission) {console.log('--------onMissionLabelUpdated-------');}
  };
  console.log('registerMissionListener');
  let listenerid = missionManager.registerMissionListener(listener);

  missionManager.unregisterMissionListener(listenerid, (error) => {
      console.log('unregisterMissionListener');
  });
```


## missionManager.unregisterMissionListener

unregisterMissionListener(listenerId: number): Promise&lt;void&gt;;

Deregisters a mission status listener. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | listenerId | number | Yes| Index of the mission status listener to deregister. It is returned by **registerMissionListener()**.|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Example**

```ts
  let listener = {
      onMissionCreated: function (mission) {console.log('--------onMissionCreated-------');},
      onMissionDestroyed: function (mission) {console.log('--------onMissionDestroyed-------');},
      onMissionSnapshotChanged: function (mission) {console.log('--------onMissionSnapshotChanged-------');},
      onMissionMovedToFront: function (mission) {console.log('--------onMissionMovedToFront-------');},
      onMissionIconUpdated: function (mission, icon) {console.log('--------onMissionIconUpdated-------');},
      onMissionClosed: function (mission) {console.log('--------onMissionClosed-------');},
      onMissionLabelUpdated: function (mission) {console.log('--------onMissionLabelUpdated-------');}
  };
  console.log('registerMissionListener');
  let listenerid = missionManager.registerMissionListener(listener);

  missionManager.unregisterMissionListener(listenerid).catch(function (err) {
      console.log(err);
  });
```


## missionManager.getMissionInfo

getMissionInfo(deviceId: string, missionId: number, callback: AsyncCallback&lt;MissionInfo&gt;): void;

Obtains the information about a given mission. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | deviceId | string | Yes| Device ID. It is a null string by default for the local device.|
  | missionId | number | Yes| Mission ID.|
  | callback | AsyncCallback&lt;[MissionInfo](js-apis-inner-application-missionInfo.md)&gt; | Yes| Callback used to return the mission information obtained.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager'

  let allMissions=missionManager.getMissionInfos('',10).catch(function(err){console.log(err);});
      missionManager.getMissionInfo('', allMissions[0].missionId, (error, mission) => {
        console.log('getMissionInfo is called, error.code = ' + error.code)
        console.log('mission.missionId = ' + mission.missionId);
        console.log('mission.runningState = ' + mission.runningState);
        console.log('mission.lockedState = ' + mission.lockedState);
        console.log('mission.timestamp = ' + mission.timestamp);
        console.log('mission.label = ' + mission.label);
        console.log('mission.iconPath = ' + mission.iconPath);
      });
  ```


## missionManager.getMissionInfo

getMissionInfo(deviceId: string, missionId: number): Promise&lt;MissionInfo&gt;;

Obtains the information about a given mission. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | deviceId | string | Yes| Device ID. It is a null string by default for the local device.|
  | missionId | number | Yes| Mission ID.|

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[MissionInfo](js-apis-inner-application-missionInfo.md)&gt; | Promise used to return the mission information obtained.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  let mission = missionManager.getMissionInfo('', 10).catch(function (err){
      console.log(err);
  });
  ```


## missionManager.getMissionInfos

getMissionInfos(deviceId: string, numMax: number, callback: AsyncCallback&lt;Array&lt;MissionInfo&gt;&gt;): void;

Obtains information about all missions. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | deviceId | string | Yes| Device ID. It is a null string by default for the local device.|
  | numMax | number | Yes| Maximum number of missions whose information can be obtained.|
  | callback | AsyncCallback&lt;Array&lt;[MissionInfo](js-apis-inner-application-missionInfo.md)&gt;&gt; | Yes| Callback used to return the array of mission information obtained.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
      console.log('getMissionInfos is called, error.code = ' + error.code);
      console.log('size = ' + missions.length);
      console.log('missions = ' + JSON.stringify(missions));
  });
  ```


## missionManager.getMissionInfos

getMissionInfos(deviceId: string, numMax: number): Promise&lt;Array&lt;MissionInfo&gt;&gt;;

Obtains information about all missions. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | deviceId | string | Yes| Device ID. It is a null string by default for the local device.|
  | numMax | number | Yes| Maximum number of missions whose information can be obtained.|

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;Array&lt;[MissionInfo](js-apis-inner-application-missionInfo.md)&gt;&gt; | Promise used to return the array of mission information obtained.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  let allMissions = missionManager.getMissionInfos('', 10).catch(function (err){
      console.log(err);
  });
  ```


## missionManager.getMissionSnapShot

getMissionSnapShot(deviceId: string, missionId: number, callback: AsyncCallback&lt;MissionSnapshot&gt;): void;

Obtains the snapshot of a given mission. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | deviceId | string | Yes| Device ID. It is a null string by default for the local device.|
  | missionId | number | Yes| Mission ID.|
  | callback | AsyncCallback&lt;[MissionSnapshot](js-apis-inner-application-missionSnapshot.md)&gt; | Yes| Callback used to return the snapshot information obtained.|

**Example**

  ```ts
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


## missionManager.getMissionSnapShot

getMissionSnapShot(deviceId: string, missionId: number): Promise&lt;MissionSnapshot&gt;;

Obtains the snapshot of a given mission. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | deviceId | string | Yes| Device ID. It is a null string by default for the local device.|
  | missionId | number | Yes| Mission ID.|

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[MissionSnapshot](js-apis-inner-application-missionSnapshot.md)&gt; | Promise used to return the snapshot information obtained.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  let allMissions;
  missionManager.getMissionInfos('',10).then(function(res){
    allMissions=res;
    }).catch(function(err){console.log(err);});
    console.log('size = ' + allMissions.length);
    console.log('missions = ' + JSON.stringify(allMissions));
    let id = allMissions[0].missionId;

    let snapshot = missionManager.getMissionSnapShot('', id).catch(function (err){
        console.log(err);
    });
  ```

## missionManager.lockMission

lockMission(missionId: number, callback: AsyncCallback&lt;void&gt;): void;

Locks a given mission. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | missionId | number | Yes| Mission ID.|
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    console.log('getMissionInfos is called, error.code = ' + error.code);
    console.log('size = ' + missions.length);
    console.log('missions = ' + JSON.stringify(missions));
    let id = missions[0].missionId;

    missionManager.lockMission(id).then(() => {
  	console.log('lockMission is called ');
  });
  });
  ```


## missionManager.lockMission

lockMission(missionId: number): Promise&lt;void&gt;;

Locks a given mission. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | missionId | number | Yes| Mission ID.|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  let allMissions;
  missionManager.getMissionInfos('',10).then(function(res){
    allMissions=res;
  }).catch(function(err){console.log(err);});
  console.log('size = ' + allMissions.length);
  console.log('missions = ' + JSON.stringify(allMissions));
  let id = allMissions[0].missionId;

  missionManager.lockMission(id).catch(function (err){
      console.log(err);
  });
  ```


## missionManager.unlockMission

unlockMission(missionId: number, callback: AsyncCallback&lt;void&gt;): void;

Unlocks a given mission. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| missionId | number | Yes| Mission ID.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    console.log('getMissionInfos is called, error.code = ' + error.code);
    console.log('size = ' + missions.length);
    console.log('missions = ' + JSON.stringify(missions));
    let id = missions[0].missionId;

    missionManager.unlockMission(id).then(() => {
  	console.log('unlockMission is called ');
  });
  });
  ```


## missionManager.unlockMission

unlockMission(missionId: number): Promise&lt;void&gt;;

Unlocks a given mission. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | missionId | number | Yes| Mission ID.|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  let allMissions;
  missionManager.getMissionInfos('',10).then(function(res){
    allMissions=res;
  }).catch(function(err){console.log(err);});
  console.log('size = ' + allMissions.length);
  console.log('missions = ' + JSON.stringify(allMissions));
  let id = allMissions[0].missionId;

  missionManager.lockMission(id).catch(function (err){
      console.log(err);
  });
  missionManager.unlockMission(id).catch(function (err){
      console.log(err);
  });
  ```


## missionManager.clearMission

clearMission(missionId: number, callback: AsyncCallback&lt;void&gt;): void;

Clears a given mission, regardless of whether it is locked. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | missionId | number | Yes| Mission ID.|
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    console.log('getMissionInfos is called, error.code = ' + error.code);
    console.log('size = ' + missions.length);
    console.log('missions = ' + JSON.stringify(missions));
    let id = missions[0].missionId;

    missionManager.clearMission(id).then(() => {
  	console.log('clearMission is called ');
  });
  });
  ```


## missionManager.clearMission

clearMission(missionId: number): Promise&lt;void&gt;;

Clears a given mission, regardless of whether it is locked. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | missionId | number | Yes| Mission ID.|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  let allMissions;
  missionManager.getMissionInfos('',10).then(function(res){
    allMissions=res;
  }).catch(function(err){console.log(err);});
  console.log('size = ' + allMissions.length);
  console.log('missions = ' + JSON.stringify(allMissions));
  let id = allMissions[0].missionId;

  missionManager.clearMission(id).catch(function (err){
    console.log(err);
  });
  ```


## missionManager.clearAllMissions

clearAllMissions(callback: AsyncCallback&lt;void&gt;): void;

Clears all unlocked missions. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.clearAllMissions().then(() => {
    console.log('clearAllMissions is called ');
  });
  ```


## missionManager.clearAllMissions

clearAllMissions(): Promise&lt;void&gt;;

Clears all unlocked missions. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  missionManager.clearAllMissions().catch(function (err){
    console.log(err);
  });
  ```


## missionManager.moveMissionToFront

moveMissionToFront(missionId: number, callback: AsyncCallback&lt;void&gt;): void;

Switches a given mission to the foreground. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | missionId | number | Yes| Mission ID.|
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    console.log('getMissionInfos is called, error.code = ' + error.code);
    console.log('size = ' + missions.length);
    console.log('missions = ' + JSON.stringify(missions));
    let id = missions[0].missionId;

    missionManager.moveMissionToFront(id).then(() => {
  	console.log('moveMissionToFront is called ');
  });
  });
  ```


## missionManager.moveMissionToFront

moveMissionToFront(missionId: number, options: StartOptions, callback: AsyncCallback&lt;void&gt;): void;

Switches a given mission to the foreground, with the startup parameters for the switching specified. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | missionId | number | Yes| Mission ID.|
  | options | [StartOptions](js-apis-app-ability-startOptions.md) | Yes| Startup parameters, which are used to specify the window mode and device ID for switching the mission to the foreground.|
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    console.log('getMissionInfos is called, error.code = ' + error.code);
    console.log('size = ' + missions.length);
    console.log('missions = ' + JSON.stringify(missions));
    let id = missions[0].missionId;

    missionManager.moveMissionToFront(id,{windowMode : 101}).then(() => {
  	console.log('moveMissionToFront is called ');
    });
  });
  ```


## missionManager.moveMissionToFront

moveMissionToFront(missionId: number, options?: StartOptions): Promise&lt;void&gt;;

Switches a given mission to the foreground, with the startup parameters for the switching specified. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_MISSIONS

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | missionId | number | Yes| Mission ID.|
  | options | [StartOptions](js-apis-app-ability-startOptions.md) | No| Startup parameters, which are used to specify the window mode and device ID for switching the mission to the foreground.|

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.| 

**Example**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  let allMissions;
  missionManager.getMissionInfos('',10).then(function(res){
    allMissions=res;
  }).catch(function(err){console.log(err);});
  console.log('size = ' + allMissions.length);
  console.log('missions = ' + JSON.stringify(allMissions));
  let id = allMissions[0].missionId;

  missionManager.moveMissionToFront(id).catch(function (err){
    console.log(err);
  });
  ```
