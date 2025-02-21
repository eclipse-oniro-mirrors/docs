# @system.mediaquery (Media Query)

The **mediaquery** module provides different styles for different media types.


> **NOTE**
>
> - The APIs of this module are no longer maintained since API version 7. You are advised to use [`@ohos.mediaquery`](js-apis-mediaquery.md) instead.
> - The initial APIs of this module are supported since API version 3. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import


```ts
import mediaquery from '@system.mediaquery';
```


## mediaquery.matchMedia

matchMedia(condition: string): MediaQueryList

Creates a **MediaQueryList** object based on the query condition.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name      | Type    | Mandatory  | Description      |
| --------- | ------ | ---- | -------- |
| condition | string | Yes   | Query condition.|

**Return value**

| Type          | Description                                      |
| -------------- | ---------------------------------------- |
| MediaQueryList | Attributes of the **MediaQueryList** object created. For details, see **MediaQueryList** attributes.|

**Example**

```ts
let mMediaQueryList = mediaquery.matchMedia('(max-width: 466)');    
```

## MediaQueryEvent

Defines a media query event.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name     | Type   | Mandatory  | Description   |
| ------- | ------- | ---- | ----- |
| matches | boolean | Yes   | Matching result.|

## MediaQueryList

Defines a media query list.

### Attributes

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name     | Type   | Mandatory  | Description               |
| ------- | ------- | ---- | ----------------- |
| media   | string  | No   | Serialized media query condition. This parameter is read-only.|
| matches | boolean | Yes   | Matching result.            |

### onchange

onchange?: (matches: boolean) => void

Called when the **matches** value changes.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name    | Type     | Mandatory  | Description            |
| ------- | ------- | ---- | -------------- |
| matches | boolean | Yes   | New **matches** value.|


### MediaQueryList.addListener

addListener(callback: (event: MediaQueryEvent) => void): void

Adds a listener for this **MediaQueryList** object. The listener must be added before **onShow** is called, that is, it must be added in the **onInit** or **onReady** API.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name     | Type                              | Mandatory  | Description            |
| -------- | -------------------------------- | ---- | -------------- |
| callback | (event: MediaQueryEvent) => void | Yes   | Callback invoked when the query condition changes.|

**Example**

```ts
function maxWidthMatch(e){
  if(e.matches){
    // do something
  }
}
mMediaQueryList.addListener(maxWidthMatch);
```


### MediaQueryList.removeListener

removeListener(callback: (event: MediaQueryEvent) => void): void

Removes the listener for this **MediaQueryList** object.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name     | Type                               | Mandatory  | Description            |
| -------- | --------------------------------- | ---- | -------------- |
| callback | (event: MediaQueryEvent) => void) | Yes   | Callback invoked when the query condition changes.|

**Example**

```ts
function maxWidthMatch(e){
  if(e.matches){
    // do something
  }
}
mMediaQueryList.removeListener(maxWidthMatch);
```
