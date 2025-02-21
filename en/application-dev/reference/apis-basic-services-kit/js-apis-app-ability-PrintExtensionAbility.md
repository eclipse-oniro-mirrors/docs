# @ohos.app.ability.PrintExtensionAbility (Print Extension Ability)

The **PrintExtensionAbility** module provides operation APIs of the print extension ability.

> **NOTE** 
> The initial APIs of this module are supported since API version 14. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import PrintExtensionAbility from '@ohos.app.ability.PrintExtensionAbility';
```

## onCreate

onCreate(want: Want): void

Called to initialize the print extension when the system connects to the extension for the first time.

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type** | **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| want | Want | Yes| Parameters required for invoking the print page.|

**Example**

```ts
import PrintExtensionAbility from '@ohos.app.ability.PrintExtensionAbility';
import Want from '@ohos.app.ability.Want';

export default class HWPrintExtension extends PrintExtensionAbility {
    onCreate(want: Want): void {
        console.log('onCreate');
        // ...
    }
}
```

## onStartDiscoverPrinter

onStartDiscoverPrinter(): void

Called when an attempt to discover printers starts.

**System capability**: SystemCapability.Print.PrintFramework

**Example**

```ts
import PrintExtensionAbility from '@ohos.app.ability.PrintExtensionAbility';

export default class HWPrintExtension extends PrintExtensionAbility {
    onStartDiscoverPrinter(): void {
        console.log('onStartDiscoverPrinter enter');
        // ...
    }
}
```

## onStopDiscoverPrinter

onStopDiscoverPrinter(): void

Called when the attempt to discover printers stops.

**System capability**: SystemCapability.Print.PrintFramework

**Example**

```ts
import PrintExtensionAbility from '@ohos.app.ability.PrintExtensionAbility';

export default class HWPrintExtension extends PrintExtensionAbility {
    onStopDiscoverPrinter(): void {
        console.log('onStopDiscoverPrinter enter');
        // ...
    }
}
```

## onConnectPrinter

onConnectPrinter(printerId: number): void

Called when the device connects to the specified printer.

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type** | **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| printerId | number | Yes| Printer ID.|

**Example**

```ts
import PrintExtensionAbility from '@ohos.app.ability.PrintExtensionAbility';

export default class HWPrintExtension extends PrintExtensionAbility {
    onConnectPrinter(printerId: number): void {
        console.log('onConnectPrinter enter');
        // ...
    }
}
```

## onDisconnectPrinter

onDisconnectPrinter(printerId: number): void

Called when the device disconnects from the specified printer.

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type** | **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| printerId | number | Yes| Printer ID.|

**Example**

```ts
import PrintExtensionAbility from '@ohos.app.ability.PrintExtensionAbility';

export default class HWPrintExtension extends PrintExtensionAbility {
    onDisconnectPrinter(printerId: number): void {
        console.log('onDisconnectPrinter enter');
        // ...
    }
}
```

## onDestroy

onDestroy(): void

Called when the print extension ability is stopped.

**System capability**: SystemCapability.Print.PrintFramework

**Example**

```ts
import PrintExtensionAbility from '@ohos.app.ability.PrintExtensionAbility';

export default class HWPrintExtension extends PrintExtensionAbility {
    onDestroy(): void {
        console.log('onDestroy');
    }
}
```
