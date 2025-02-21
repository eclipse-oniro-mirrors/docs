# EventHub

The **EventHub** module provides APIs to subscribe to, unsubscribe from, and trigger events.

> **NOTE**
>
>  - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version. 
>  - The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import common from '@ohos.app.ability.common';
```

## Usage

Before using any APIs in the **EventHub**, you must obtain an **EventHub** instance through the member variable **context** of the **UIAbility** instance.

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
EventHub is not a global event center. Different context objects have different EventHub objects. Event subscription, unsubscription, and triggering are performed on a specific EventHub object. Therefore, EventHub cannot be used for event transmission between VMs or processes.

## EventHub.on

on(event: string, callback: Function): void;

Subscribes to an event.
> **NOTE**
>
>  When the callback is triggered by **emit**, the invoker is the **EventHub** object. To change the direction of **this** in **callback**, use an arrow function.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| event | string | Yes| Event name.|
| callback | Function | Yes| Callback invoked when the event is triggered.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    value: number = 12;

    onCreate() {
        this.context.eventHub.on('myEvent', this.eventFunc);
        // Anonymous functions can be used to subscribe to events.
        this.context.eventHub.on('myEvent', () => {
            console.log(`anonymous eventFunc is called, value: ${this.value}`);
        });
    }

    onForeground() {
        // Result
        // eventFunc is called, value: undefined
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

Unsubscribes from an event.
 - If **callback** is specified, this API unsubscribes from the given event with the specified callback.
 - If **callback** is not specified, this API unsubscribes from the given event with all callbacks.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| event | string | Yes| Event name.|
| callback | Function | No| Callback for the event. If **callback** is unspecified, the given event with all callbacks is unsubscribed.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    onCreate() {
        this.context.eventHub.on('myEvent', this.eventFunc1);
        this.context.eventHub.off('myEvent', this.eventFunc1); // Unsubscribe from the myEvent event with the callback eventFunc1.
        this.context.eventHub.on('myEvent', this.eventFunc1);
        this.context.eventHub.on('myEvent', this.eventFunc2);
        this.context.eventHub.off('myEvent');  // Unsubscribe from the myEvent event with all the callbacks (eventFunc1 and eventFunc2).
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

Triggers an event.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| event | string | Yes| Event name.|
| ...args | Object[] | No| Variable parameters, which are passed to the callback when the event is triggered.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    onCreate() {
        this.context.eventHub.on('myEvent', this.eventFunc);
    }

    onDestroy() {
        // Result
        // eventFunc is called,undefined,undefined
        this.context.eventHub.emit('myEvent');
        // Result
        // eventFunc is called,1,undefined
        this.context.eventHub.emit('myEvent', 1);
        // Result
        // eventFunc is called,1,2
        this.context.eventHub.emit('myEvent', 1, 2);
    }

    eventFunc(argOne: number, argTwo: number) {
        console.log(`eventFunc is called, ${argOne}, ${argTwo}`);
    }
}
```
