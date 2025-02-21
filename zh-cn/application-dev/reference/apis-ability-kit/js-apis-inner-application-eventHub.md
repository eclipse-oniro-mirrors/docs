# EventHub

EventHub模块提供了事件中心，提供订阅、取消订阅、触发事件的能力。

> **说明：**
>
>  - 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。  
>  - 本模块接口仅可在Stage模型下使用。

## 导入模块

```ts
import common from '@ohos.app.ability.common';
```

## 使用说明

在使用eventHub的功能前，需要通过UIAbility实例的成员变量context获取。

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    eventFunc(){
        console.log('eventFunc is called');
    }

    onCreate() {
        this.context.eventHub.on('myEvent', this.eventFunc);
    }
}
```
EventHub不是全局的事件中心，不同的context对象拥有不同的EventHub对象，事件的订阅、取消订阅、触发都作用在某一个具体的EventHub对象上，因此不能用于虚拟机间或者进程间的事件传递。

## EventHub.on

on(event: string, callback: Function): void;

订阅指定事件。
> **说明：**
>
>  callback被emit触发时，调用方是EventHub对象，如果要修改callback中this的指向，可以使用箭头函数。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| event | string | 是 | 事件名称。 |
| callback | Function | 是 | 事件回调，事件触发后调用。 |

**示例1：**
callback被emit触发时，调用方是EventHub对象。EventHub对象没有value属性，因此结果是undefined。

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    value: number = 12;

    onCreate() {
        this.context.eventHub.on('myEvent', this.eventFunc);
    }

    onForeground() {
        // 结果：
        // eventFunc is called, value: undefined

        this.context.eventHub.emit('myEvent');
    }

    eventFunc() {
        console.log(`eventFunc is called, value: ${this.value}`);
    }
}
```

**示例2：**
callback使用箭头函数时，调用方是EntryAbility对象。EntryAbility对象里存在value属性，因此结果是12。

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    value: number = 12;

    onCreate() {
        // 支持使用匿名函数订阅事件
        this.context.eventHub.on('myEvent', () => {
            console.log(`anonymous eventFunc is called, value: ${this.value}`);
        });
    }

    onForeground() {
        // 结果：
        // anonymous eventFunc is called, value: 12
        this.context.eventHub.emit('myEvent');
    }

    eventFunc() {
        console.log(`eventFunc is called, value: ${this.value}`);
    }
}
```

## EventHub.off

off(event: string, callback?: Function): void;

取消订阅指定事件。
 - 传入callback：取消指定的callback对指定事件的订阅，当该事件触发后，将不会回调该callback。
 - 不传callback：取消所有callback对指定事件的订阅。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| event | string | 是 | 事件名称。 |
| callback | Function | 否 | 事件回调。如果不传callback，则取消订阅该事件下所有callback。 |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    onCreate() {
        this.context.eventHub.on('myEvent', this.eventFunc1);
        this.context.eventHub.off('myEvent', this.eventFunc1); // 取消eventFunc1对myEvent事件的订阅
        this.context.eventHub.on('myEvent', this.eventFunc1);
        this.context.eventHub.on('myEvent', this.eventFunc2);
        this.context.eventHub.off('myEvent');  // 取消eventFunc1和eventFunc2对myEvent事件的订阅
    }

    eventFunc1() {
        console.log('eventFunc1 is called');
    }

    eventFunc2() {
        console.log('eventFunc2 is called');
    }
}
```

## EventHub.emit

emit(event: string, ...args: Object[]): void;

触发指定事件。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| event | string | 是 | 事件名称。 |
| ...args | Object[] | 否 | 可变参数，事件触发时，传递给回调函数的参数。 |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    onCreate() {
        this.context.eventHub.on('myEvent', this.eventFunc);
    }

    onDestroy() {
        // 结果：
        // eventFunc is called,undefined,undefined
        this.context.eventHub.emit('myEvent');
        // 结果：
        // eventFunc is called,1,undefined
        this.context.eventHub.emit('myEvent', 1);
        // 结果：
        // eventFunc is called,1,2
        this.context.eventHub.emit('myEvent', 1, 2);
    }

    eventFunc(argOne: number, argTwo: number) {
        console.log(`eventFunc is called, ${argOne}, ${argTwo}`);
    }
}
```
