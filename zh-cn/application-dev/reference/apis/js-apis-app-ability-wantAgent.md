# @ohos.app.ability.wantAgent (WantAgent模块)

WantAgent模块提供了触发、取消、比较WantAgent实例和获取bundle名称的能力，包括创建WantAgent实例、获取实例的用户ID、获取want信息等。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。  

## 导入模块

```js
import WantAgent from '@ohos.app.ability.wantAgent';
```

## WantAgent.getWantAgent

getWantAgent(info: WantAgentInfo, callback: AsyncCallback\<WantAgent\>): void

创建WantAgent（callback形式）。 创建失败返回的WantAgent为空值。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名     | 类型                       | 必填 | 说明                    |
| -------- | -------------------------- | ---- | ----------------------- |
| info     | [WantAgentInfo](js-apis-inner-wantAgent-wantAgentInfo.md)              | 是   | WantAgent信息。           |
| callback | AsyncCallback\<WantAgent\> | 是   | 创建WantAgent的回调方法。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';

//getWantAgent回调
function getWantAgentCallback(err, data) {
	console.info('==========================>getWantAgentCallback=======================>');
}
//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo, getWantAgentCallback);
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.getWantAgent

getWantAgent(info: WantAgentInfo): Promise\<WantAgent\>

创建WantAgent（Promise形式）。 创建失败返回的WantAgent为空值。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型          | 必填 | 说明          |
| ---- | ------------- | ---- | ------------- |
| info | [WantAgentInfo](js-apis-inner-wantAgent-wantAgentInfo.md) | 是   | WantAgent信息。 |

**返回值：**

| 类型                                                        | 说明                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<WantAgent\> | 以Promise形式返回WantAgent。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```ts
let wantAgent;
//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo).then((data) => {
	    console.info('==========================>getWantAgentCallback=======================>');
    });
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.getBundleName

getBundleName(agent: WantAgent, callback: AsyncCallback\<string\>): void

获取WantAgent实例的包名（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名     | 类型                    | 必填 | 说明                              |
| -------- | ----------------------- | ---- | --------------------------------- |
| agent    | WantAgent               | 是   | WantAgent对象。                     |
| callback | AsyncCallback\<string\> | 是   | 获取WantAgent实例的包名的回调方法。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent;

//getWantAgent回调
function getWantAgentCallback(err, data) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.info('----getWantAgent failed!----');
    }
}
//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo, getWantAgentCallback);

    //getBundleName回调
    function getBundleNameCallback(err, data) {
	    console.info('==========================>getBundleNameCallback=======================>');
    }
    WantAgent.getBundleName(wantAgent, getBundleNameCallback);
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.getBundleName

getBundleName(agent: WantAgent): Promise\<string\>

获取WantAgent实例的包名（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名  | 类型      | 必填 | 说明          |
| ----- | --------- | ---- | ------------- |
| agent | WantAgent | 是   | WantAgent对象。 |

**返回值：**

| 类型                                                        | 说明                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<string\> | 以Promise形式返回获取WantAgent实例的包名。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent;

//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo).then((data) => {
	    console.info('==========================>getWantAgentCallback=======================>');
        wantAgent = data;
    });

    WantAgent.getBundleName(wantAgent).then((data) => {
	    console.info('==========================>getBundleNameCallback=======================>');
    });
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.getUid

getUid(agent: WantAgent, callback: AsyncCallback\<number\>): void

获取WantAgent实例的用户ID（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名     | 类型                    | 必填 | 说明                                |
| -------- | ----------------------- | ---- | ----------------------------------- |
| agent    | WantAgent               | 是   | WantAgent对象。                       |
| callback | AsyncCallback\<number\> | 是   | 获取WantAgent实例的用户ID的回调方法。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent;

//getWantAgent回调
function getWantAgentCallback(err, data) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.info('----getWantAgent failed!----');
    }
}
//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo, getWantAgentCallback);

    //getUid回调
    function getUidCallback(err, data) {
	    console.info('==========================>getUidCallback=======================>');
    }
    WantAgent.getUid(wantAgent, getUidCallback);
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.getUid

getUid(agent: WantAgent): Promise\<number\>

获取WantAgent实例的用户ID（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名  | 类型      | 必填 | 说明          |
| ----- | --------- | ---- | ------------- |
| agent | WantAgent | 是   | WantAgent对象。 |

**返回值：**

| 类型                                                        | 说明                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<number\> | 以Promise形式返回获取WantAgent实例的用户ID。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent;

//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo).then((data) => {
	    console.info('==========================>getWantAgentCallback=======================>');
        wantAgent = data;
    });

    WantAgent.getUid(wantAgent).then((data) => {
	    console.info('==========================>getUidCallback=======================>');
    });
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.getWant

getWant(agent: WantAgent, callback: AsyncCallback\<Want\>): void

获取WantAgent对象的want（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名     | 类型                  | 必填 | 说明                            |
| -------- | --------------------- | ---- | ------------------------------- |
| agent    | WantAgent             | 是   | WantAgent对象。                   |
| callback | AsyncCallback\<[Want](js-apis-app-ability-want.md)\> | 是   | 获取WantAgent对象want的回调方法。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000015   | Service timeout.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent;

//getWantAgent回调
function getWantAgentCallback(err, data) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.info('----getWantAgent failed!----');
    }
}
//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo, getWantAgentCallback);

    //getWant回调
    function getWantCallback(err, data) {
	    console.info('==========================>getWantCallback=======================>');
    }
    WantAgent.getWant(wantAgent, getWantCallback);
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.getWant

getWant(agent: WantAgent): Promise\<Want\>

获取WantAgent对象的want（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名  | 类型      | 必填 | 说明          |
| ----- | --------- | ---- | ------------- |
| agent | WantAgent | 是   | WantAgent对象。 |

**返回值：**

| 类型                                                        | 说明                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<[Want](js-apis-app-ability-want.md)\> | 以Promise形式返回获取WantAgent对象的want。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000015   | Service timeout.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent;

//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo).then((data) => {
	    console.info('==========================>getWantAgentCallback=======================>');
        wantAgent = data;
    });

    WantAgent.getWant(wantAgent).then((data) => {
	    console.info('==========================>getWantCallback=======================>');
    });
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.cancel

cancel(agent: WantAgent, callback: AsyncCallback\<void\>): void

取消WantAgent实例（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名     | 类型                  | 必填 | 说明                        |
| -------- | --------------------- | ---- | --------------------------- |
| agent    | WantAgent             | 是   | WantAgent对象。               |
| callback | AsyncCallback\<void\> | 是   | 取消WantAgent实例的回调方法。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent;

//getWantAgent回调
function getWantAgentCallback(err, data) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.info('----getWantAgent failed!----');
    }
}
//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo, getWantAgentCallback);

    //cancel回调
    function cancelCallback(err, data) {
	    console.info('==========================>cancelCallback=======================>');
    }
    WantAgent.cancel(wantAgent, cancelCallback);
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.cancel

cancel(agent: WantAgent): Promise\<void\>

取消WantAgent实例（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名  | 类型      | 必填 | 说明          |
| ----- | --------- | ---- | ------------- |
| agent | WantAgent | 是   | WantAgent对象。 |

**返回值：**

| 类型            | 说明                            |
| --------------- | ------------------------------- |
| Promise\<void\> | 以Promise形式获取异步返回结果。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent;

//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo).then((data) => {
	    console.info('==========================>getWantAgentCallback=======================>');
        wantAgent = data;
    });

    WantAgent.cancel(wantAgent).then((data) => {
	    console.info('==========================>cancelCallback=======================>');
    });
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.trigger

trigger(agent: WantAgent, triggerInfo: TriggerInfo, callback?: AsyncCallback\<CompleteData\>): void

主动激发WantAgent实例（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名        | 类型                          | 必填 | 说明                            |
| ----------- | ----------------------------- | ---- | ------------------------------- |
| agent       | WantAgent                     | 是   | WantAgent对象。                   |
| triggerInfo | [TriggerInfo](js-apis-inner-wantAgent-triggerInfo.md)                   | 是   | TriggerInfo对象。                 |
| callback    | AsyncCallback\<[CompleteData](#completedata)\> | 否   | 主动激发WantAgent实例的回调方法。 |

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent;

//getWantAgent回调
function getWantAgentCallback(err, data) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.info('----getWantAgent failed!----');
    }
}
//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo, getWantAgentCallback);

    //trigger回调
    function triggerCallback(data) {
	    console.info('==========================>triggerCallback=======================>');
    }


    let triggerInfo = {
        code:0
    };
    WantAgent.trigger(wantAgent, triggerInfo, triggerCallback);
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.equal

equal(agent: WantAgent, otherAgent: WantAgent, callback: AsyncCallback\<boolean\>): void

判断两个WantAgent实例是否相等（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名       | 类型                     | 必填 | 说明                                    |
| ---------- | ------------------------ | ---- | --------------------------------------- |
| agent      | WantAgent                | 是   | WantAgent对象。                           |
| otherAgent | WantAgent                | 是   | WantAgent对象。                           |
| callback   | AsyncCallback\<boolean\> | 是   | 判断两个WantAgent实例是否相等的回调方法。 |

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent1;
let wantAgent2;

//getWantAgent回调
function getWantAgentCallback(err, data) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent1 = data;
        wantAgent2 = data;
    } else {
        console.info('----getWantAgent failed!----');
    }
}
//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo, getWantAgentCallback);

    //equal回调
    function equalCallback(err, data) {
	    console.info('==========================>equalCallback=======================>');
    }
    WantAgent.equal(wantAgent1, wantAgent2, equalCallback);
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```



## WantAgent.equal

equal(agent: WantAgent, otherAgent: WantAgent): Promise\<boolean\>

判断两个WantAgent实例是否相等（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名       | 类型      | 必填 | 说明          |
| ---------- | --------- | ---- | ------------- |
| agent      | WantAgent | 是   | WantAgent对象。 |
| otherAgent | WantAgent | 是   | WantAgent对象。 |

**返回值：**

| 类型                                                        | 说明                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<boolean\> | 以Promise形式返回获取判断两个WantAgent实例是否相等的结果。 |

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';


//wantAgent对象
let wantAgent1;
let wantAgent2;

//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo).then((data) => {
	    console.info('==========================>getWantAgentCallback=======================>');
        wantAgent1 = data;
        wantAgent2 = data;
    });

    WantAgent.equal(wantAgent1, wantAgent2).then((data) => {
	    console.info('==========================>equalCallback=======================>');
    });
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```

## WantAgent.getOperationType

getOperationType(agent: WantAgent, callback: AsyncCallback\<number>): void;

获取一个WantAgent的OperationType信息（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名       | 类型                     | 必填 | 说明                                    |
| ---------- | ------------------------ | ---- | --------------------------------------- |
| agent      | WantAgent                | 是   | WantAgent对象。                           |
| callback   | AsyncCallback\<number> | 是   | 获取一个WantAgent的OperationType信息的回调方法。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000015   | Service timeout.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';

//wantAgent对象
let wantAgent;

//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

//getWantAgent回调
function getWantAgentCallback(err, data) {
    if (err === undefined) {
        wantAgent = data;
    } else {
        console.error('getWantAgent failed ${JSON.stringify(wantAgent)}');
    }
    //getOperationTypeCallback回调
    function getOperationTypeCallback(err, data) {
        if(err) {
            console.error('getOperationType failed! ${err.code} ${err.message}');
        } else {
            console.info('getOperationType ok! ${JSON.stringify(data)}');
        }
    }
    try {
        WantAgent.getOperationType(wantAgent, getOperationTypeCallback);
    } catch(err) {
        console.error('getOperationTypeCallback failed! ${err.code} ${err.message}');
    }
}
try {
    WantAgent.getWantAgent(wantAgentInfo).then((data) => {
	    console.info('==========================>getWantAgentCallback=======================>');
        wantAgent = data;
    });

    WantAgent.getOperationType(wantAgent, (OperationType) => {
        console.log('----------- getOperationType ----------, OperationType: ' + OperationType);
    })
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```

## WantAgent.getOperationType

getOperationType(agent: WantAgent): Promise\<number>;

获取一个WantAgent的OperationType信息（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名       | 类型      | 必填 | 说明          |
| ---------- | --------- | ---- | ------------- |
| agent      | WantAgent | 是   | WantAgent对象。 |

**返回值：**

| 类型                                                        | 说明                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<number> | 以Promise形式返回获取operationType的结果。 |

**错误码：**

| 错误码ID    | 错误信息            |
|-----------|--------------------|
| 16000007   | Service busyness. There are concurrent tasks, waiting for retry.|
| 16000015   | Service timeout.|
| 16000151   | Invalid wantagent object.|

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

```js
import WantAgent from '@ohos.app.ability.wantAgent';

//wantAgent对象
let wantAgent;

//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.MainAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

try {
    WantAgent.getWantAgent(wantAgentInfo).then((data) => {
	    console.info('==========================>getWantAgentCallback=======================>');
        wantAgent = data;
    });

    WantAgent.getOperationType(wantAgent).then((OperationType) => {
        console.log('getOperationType success, OperationType: ' + OperationType);
    }).catch((err) => {
        console.log('getOperationType fail, err: ' + err);
    })
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```

## WantAgentFlags

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称                | 值             | 说明                                                         |
| ------------------- | -------------- | ------------------------------------------------------------ |
| ONE_TIME_FLAG       | 0 | WantAgent仅能使用一次。                                      |
| NO_BUILD_FLAG       | 1 | 如果描述WantAgent对象不存在，则不创建它，直接返回null。      |
| CANCEL_PRESENT_FLAG | 2 | 在生成一个新的WantAgent对象前取消已存在的一个WantAgent对象。 |
| UPDATE_PRESENT_FLAG | 3 | 使用新的WantAgent的额外数据替换已存在的WantAgent中的额外数据。 |
| CONSTANT_FLAG       | 4 | WantAgent是不可变的。                                        |
| REPLACE_ELEMENT     | 5 | 当前Want中的element属性可被WantAgent.trigger()中Want的element属性取代 |
| REPLACE_ACTION      | 6 | 当前Want中的action属性可被WantAgent.trigger()中Want的action属性取代 |
| REPLACE_URI         | 7 | 当前Want中的uri属性可被WantAgent.trigger()中Want的uri属性取代 |
| REPLACE_ENTITIES    | 8 | 当前Want中的entities属性可被WantAgent.trigger()中Want的entities属性取代 |
| REPLACE_BUNDLE      | 9 | 当前Want中的bundleName属性可被WantAgent.trigger()中Want的bundleName属性取代 |



## OperationType

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称              | 值            | 说明                      |
| ----------------- | ------------- | ------------------------- |
| UNKNOWN_TYPE      | 0 | 不识别的类型。            |
| START_ABILITY     | 1 | 开启一个有页面的Ability。 |
| START_ABILITIES   | 2 | 开启多个有页面的Ability。 |
| START_SERVICE     | 3 | 开启一个无页面的ability。 |
| SEND_COMMON_EVENT | 4 | 发送一个公共事件。        |



## CompleteData 

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称           | 类型                           | 必填 | 说明                    |
| -------------- | ------------------------------ | ---- | ---------------------- |
| info           | WantAgent                       | 是   | 触发的wantAgent。       |
| want           | Want                            | 是   | 存在的被触发的want。     |
| finalCode      | number                          | 是   | 触发wantAgent的请求代码。|
| finalData      | string                          | 是   | 公共事件收集的最终数据。  |
| extraInfo      | {[key: string]: any}            | 否   | 额外数据。               |

