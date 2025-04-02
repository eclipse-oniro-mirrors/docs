# @ohos.arkui.StateManagement (State Management)

The state management module provides data storage, persistent data management, UIAbility data storage, and environment state and tools required by applications.

>**NOTE**
>
>The initial APIs of this module are supported since API version 12. Newly added APIs will be marked with a superscript to indicate their earliest API version.


The meanings of T and S in this topic are as follows:


| Type  | Description                                    |
| ---- | -------------------------------------- |
| T    | Class, number, boolean, string, and arrays of these types.|
| S    | number, boolean, string.                |


## Modules to Import

```ts
import { AppStorageV2,PersistenceV2,UIUtils} from '@kit.ArkUI';
```

## AppStorageV2

For details about how to use AppStorageV2, see [AppStorageV2: Storing Application-wide UI State](../../quick-start/arkts-new-appstoragev2.md).

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### connect

static connect\<T extends object\>( <br>
      type: TypeConstructorWithArgs\<T\>, <br>
      keyOrDefaultCreator?: string | StorageDefaultCreator\<T\>, <br>
      defaultCreator?: StorageDefaultCreator\<T\> <br>
): T | undefined;

Stores key-value pair data in the application memory. If the given key already exists in [AppStorageV2](../../quick-start/arkts-new-appstoragev2.md), it returns the corresponding value; otherwise, it constructs a default value using the constructor for obtaining the default value and returns it.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type  | Mandatory| Description              |
| -------- | ------ | ---- | ---------------------- |
| type | [TypeConstructorWithArgs\<T\>](#typeconstructorwithargst) | Yes  | Type. If no key is specified, the name of the type is used as the key.|
| keyOrDefaultCreator | string \| [StorageDefaultCreator\<T\>](#storagedefaultcreatort) | No  | Key, or the constructor for obtaining the default value.|
| defaultCreator | StorageDefaultCreator\<T\> | No  | Constructor for obtaining the default value.|

>**NOTE**
>
>1. The second parameter is used when no key is specified, and the third parameter is used otherwise.
>
>2. If the data has been stored in AppStorageV2, you can obtain the stored data without using the default constructor. If the data has not been stored, you must specify a default constructor; otherwise, an application exception will be thrown.
>
>3. Ensure that the data types match the key. Connecting different types of data to the same key will result in an application exception.
>
>4. You are advised to use meaningful values for the key, with a length not exceeding 255 characters. The behavior of using illegal characters or empty characters is undefined.

**Return value**

| Type                                  | Description                                                        |
| -------------------------------------- | ------------------------------------------------------------ |
| T | Returns data if the creation or data acquisition from AppStorageV2 is successful; returns **undefined** otherwise.|

**Example**

```ts
import { AppStorageV2 } from '@kit.ArkUI';

@ObservedV2
class SampleClass {
  @Trace p: number = 0;
}

// Store the key-value pair with the key SampleClass and the value as a new instance of SampleClass() in memory, and assign it to variable as1.
const as1: SampleClass | undefined = AppStorageV2.connect(SampleClass, () => new SampleClass());

// Store the key-value pair with the key key_as2 and the value as a new instance of SampleClass() in memory, and assign it to variable as2.
const as2: SampleClass = AppStorageV2.connect(SampleClass, 'key_as2', () => new SampleClass())!;

// As the key SampleClass already exists in AppStorageV2, the value associated with the key is returned to variable as3.
const as3: SampleClass = AppStorageV2.connect(SampleClass) as SampleClass;
```

### remove

static remove\<T\>(keyOrType: string | TypeConstructorWithArgs\<T\>): void;

Removes the specified key-value pair from [AppStorageV2](../../quick-start/arkts-new-appstoragev2.md). If the specified key does not exist in AppStorageV2, the removal will fail.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type  | Mandatory| Description              |
| -------- | ------ | ---- | ---------------------- |
| keyOrType | string \| TypeConstructorWithArgs\<T\> | Yes  | Key to be removed. If a type is specified, the key to be deleted is the name of that type.|

>**NOTE**
>
>Attempting to remove a key that does not exist in AppStorageV2 will result in a warning.


**Example**

<!--code_no_check-->
```ts
// Assuming that there is a key named key_as2 in AppStorageV2, the following will remove the corresponding key-value pair from AppStorageV2.
AppStorageV2.remove('key_as2');

// Assuming that there is a key named SampleClass in AppStorageV2, the following will remove the corresponding key-value pair from AppStorageV2.
AppStorageV2.remove(SampleClass);

// Assuming there is no key named key_as1 in AppStorageV2, the following will result in a warning.
AppStorageV2.remove('key_as1');
```

### keys

static keys(): Array\<string\>;

Obtains all keys in [AppStorageV2](../../quick-start/arkts-new-appstoragev2.md).

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type                                  | Description                                                        |
| -------------------------------------- | ------------------------------------------------------------ |
| Array\<string\> | All keys stored in AppStorageV2.|

>**NOTE**
>
>The order of the keys in the Array is not sequential and does not correspond to the order in which the keys were inserted into AppStorageV2.

**Example**

```ts
// Assuming there are two keys (key_as1 and key_as2) in AppStorageV2, the following will return an array containing these keys and assign it to keys.
const keys: Array<string> = AppStorageV2.keys();
```



## PersistenceV2

Inherits from [AppStorageV2](#appstoragev2). For details, see [PersistenceV2: Persisting Application State](../../quick-start/arkts-new-persistencev2.md).

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### save

static save\<T\>(keyOrType: string | TypeConstructorWithArgs\<T\>): void;

Persists the specified key-value pair data once.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type  | Mandatory| Description              |
| -------- | ------ | ---- | ---------------------- |
| keyOrType | string \| TypeConstructorWithArgs\<T\> | Yes  | Key to be persisted. If a type is specified, the key for persistence is the name of the type.|

>**NOTE**
>
>Since changes to non-[\@Trace](../../quick-start/arkts-new-observedV2-and-trace.md) decorated data do not automatically trigger persistence through [PersistenceV2](../../quick-start/arkts-new-persistencev2.md), you can call this API to manually persist the data for the corresponding key when needed.
>
>It is useless to manually persist the keys that are not in the **connect** state in the memory.

**Example**

<!--code_no_check-->

```ts
// Assuming there is a key named key_as2 in PersistenceV2, the following will persist the data for this key-value pair.
PersistenceV2.save('key_as2');

// Assuming there is a key named SampleClass in PersistenceV2, the following will persist the data for this key-value pair.
PersistenceV2.remove(SampleClass);

// Assuming there is no key named key_as1 in PersistenceV2, this operation is meaningless.
PersistenceV2.remove('key_as1');
```

### notifyOnError

static notifyOnError(callback: PersistenceErrorCallback | undefined): void;

Called when persistence fails.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type  | Mandatory| Description              |
| -------- | ------ | ---- | ---------------------- |
| callback | PersistenceErrorCallback \| undefined  | Yes  | Callback invoked when persistence fails.|

**Example**

```ts
// Called when persistence fails.
PersistenceV2.notifyOnError((key: string, reason: string, msg: string) => {
  console.error(`error key: ${key}, reason: ${reason}, message: ${msg}`);
});
```

## UIUtils

Provides APIs for handling data transformations related to state management.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### getTarget

static getTarget\<T extends object\>(source: T): T;

Obtains the original object from a proxy object wrapped by the state management framework. For details, see [getTarget API: Obtaining Original Objects](../../quick-start/arkts-new-getTarget.md).

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type| Mandatory| Description    |
| ------ | ---- | ---- | ------------ |
| source | T    | Yes  | Source object.|

**Return value**

| Type| Description                                            |
| ---- | ------------------------------------------------ |
| T    | Original object of the source after the proxy added by the state management framework is removed.|

**Example**

```ts
import { UIUtils } from '@kit.ArkUI';
class NonObservedClass {
  name: string = "Tom";
}
let nonObservedClass: NonObservedClass = new NonObservedClass();
@Entry
@Component
struct Index {
  @State someClass: NonObservedClass = nonObservedClass;
  build() {
    Column() {
      Text(`this.someClass === nonObservedClass: ${this.someClass === nonObservedClass}`) // false
      Text(`UIUtils.getTarget(this.someClass) === nonObservedClass: ${UIUtils.getTarget(this.someClass) ===
        nonObservedClass}`) // true
    }
  }
}
```
### makeObserved

static makeObserved\<T extends object\>(source: T): T;

Converts ordinary unobservable data into observable data. For details, see [makeObserved API: Changing Unobservable Data to Observable Data](../../quick-start/arkts-new-makeObserved.md).

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type| Mandatory| Description    |
| ------ | ---- | ---- | ------------ |
| source | T    | Yes  | Source object. It supports classes not decorated by @Observed or @ObserveV2, objects returned by **JSON.parse**, and classes decorated by @Sendable.<br>Array, Map, Set, and Date types are supported.<br>**collection.Array**, **collection.Set**, and **collection.Map** are supported.<br>For details, see [makeObserved API: Changing Unobservable Data to Observable Data](../../quick-start/arkts-new-makeObserved.md).|

**Return value**

| Type| Description                                            |
| ---- | ------------------------------------------------ |
| T    | Observable data.|

**Example**

```ts
import { UIUtils } from '@kit.ArkUI';
class NonObservedClass {
  name: string = 'Tom';
}

@Entry
@ComponentV2
struct Index {
  observedClass: NonObservedClass = UIUtils.makeObserved(new NonObservedClass());
  nonObservedClass: NonObservedClass = new NonObservedClass();
  build() {
    Column() {
      Text(`observedClass: ${this.observedClass.name}`)
        .onClick(() => {
          this.observedClass.name = 'Jane'; // This will trigger a UI update.
        })
      Text(`observedClass: ${this.nonObservedClass.name}`)
        .onClick(() => {
          this.nonObservedClass.name = 'Jane'; // This will not trigger a UI update.
        })
    }
  }
}
```

## StorageDefaultCreator\<T\>

type StorageDefaultCreator\<T\> = () => T;

Obtains the default constructor.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type| Description                                            |
| ---- | ------------------------------------------------ |
| () => T    | Default constructor.|

**Example**

```ts
import { PersistenceV2 } from '@kit.ArkUI';

@ObservedV2
class SampleClass {
  @Trace id: number = 0;
  count: number = 1;
}

@ObservedV2
class FatherSampleClass {
  @Trace sampleClass: SampleClass = new SampleClass();
}

// Persist the key-value pair with the key SampleClass and the value as an instance of SampleClass(), and assign it to variable source.
// StorageDefaultCreator refers to the function () => new FatherSampleClass().
const source: FatherSampleClass | undefined = PersistenceV2.connect(FatherSampleClass, () => new FatherSampleClass());

@Entry
@Component
struct SampleComp {
  data: FatherSampleClass | undefined = source;

  build() {
    Column() {
      Text(`${this.data?.sampleClass.id}`)
    }
  }
}
```

## TypeConstructorWithArgs\<T\>

Represents a class constructor that accepts arbitrary arguments.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### new

new(...args: any): T;

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type| Mandatory| Description    |
| ------ | ---- | ---- | ------------ |
| ...args | any    | Yes  | Function arguments.  |

**Return value**

| Type| Description                                            |
| ---- | ------------------------------------------------ |
| T    | Instance of the T type.|

**Example**

```ts
import { PersistenceV2 } from '@kit.ArkUI';

@ObservedV2
  // TypeConstructorWithArgs refers to the SampleClass constructor.
class SampleClass {
  @Trace id: number = 0;
  count: number = 1;
}

@ObservedV2
class FatherSampleClass {
  @Trace sampleClass: SampleClass = new SampleClass();
}

// Persist the key-value pair with the key SampleClass and the value as an instance of SampleClass(), and assign it to variable source.
const source: FatherSampleClass | undefined = PersistenceV2.connect(FatherSampleClass, () => new FatherSampleClass());

@Entry
@Component
struct SampleComp {
  data: FatherSampleClass | undefined = source;

  build() {
    Column() {
      Text(`${this.data?.sampleClass.id}`)
    }
  }
}
```

## PersistenceErrorCallback

type PersistenceErrorCallback = (key: string, reason: 'quota' | 'serialization' | 'unknown', message: string) => void;

Represents the callback invoked when persistence fails.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type| Mandatory| Description    |
| ------ | ---- | ---- | ------------ |
| key | string    | Yes  | Key associated with the error.  |
|reason| 'quota' \| 'serialization' \| 'unknown'    | Yes  | Type of the error.  |
| message | string    | Yes  | Additional information about the error.  |

**Example**

```ts
import { PersistenceV2, Type } from '@kit.ArkUI';

@ObservedV2
class SampleChild {
  @Trace id: number = 0;
  count: number = 10;
}

@ObservedV2
export class Sample {
  // For complex objects, use the @Type decorator to ensure successful serialization.
  @Type(SampleChild)
  @Trace sampleChild: SampleChild = new SampleChild();
}

// Callback used to receive persistence errors.
// PersistenceErrorCallback refers to (key: string, reason: string, msg: string) => {console.error(`error key: ${key}, reason: ${reason}, message: ${msg}`);}.
PersistenceV2.notifyOnError((key: string, reason: string, msg: string) => {
  console.error(`error key: ${key}, reason: ${reason}, message: ${msg}`);
});

@Entry
@ComponentV2
struct Index {
  // Create a key-value pair with the key Sample in PersistenceV2 (if the key exists, the data in PersistenceV2 is returned) and associate it with data.
  // Add @Local to decorate the data property that needs to change the connected object. (Changing the connected object is not recommended.)
  @Local data: Sample = PersistenceV2.connect(Sample, () => new Sample())!;
  pageStack: NavPathStack = new NavPathStack();

  build() {
    Text(`Index add 1 to data.id: ${this.data.sampleChild.id}`)
      .fontSize(30)
      .onClick(() => {
        this.data.sampleChild.id++;
      })
  }
}
```

## TypeConstructor\<T\>

Class constructor.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### new

new(): T;

**Return value**

| Type| Description                                            |
| ---- | ------------------------------------------------ |
| T    | Instance of the T type.|

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Example**

```ts
import { PersistenceV2, Type } from '@kit.ArkUI';

@ObservedV2
class SampleChild {
  @Trace id: number = 0;
  count: number = 10;
}

@ObservedV2
export class Sample {
  // For complex objects, use the @Type decorator to ensure successful serialization.
  // TypeConstructor refers to SampleChild.
  @Type(SampleChild)
  @Trace sampleChild: SampleChild = new SampleChild();
}

@Entry
@ComponentV2
struct Index {
  data: Sample = PersistenceV2.connect(Sample, () => new Sample())!;

  build() {
    Column() {
      Text(`Index add 1 to data.id: ${this.data.sampleChild.id}`)
        .fontSize(30)
        .onClick(() => {
          this.data.sampleChild.id++;
        })
    }
  }
}
```

## TypeDecorator

type TypeDecorator = \<T\>(type: TypeConstructor\<T\>) => PropertyDecorator;

Property decorator.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type| Mandatory| Description    |
| ------ | ---- | ---- | ------------ |
| type | [TypeConstructor\<T\>](#typeconstructort)    | Yes  | Type of the class property decorated.  |

**Return value**

| Type| Description                                            |
| ---- | ------------------------------------------------ |
| PropertyDecorator    | Property decorator.|

**Example**

```ts
import { PersistenceV2, Type } from '@kit.ArkUI';

@ObservedV2
class SampleChild {
  @Trace id: number = 0;
  count: number = 10;
}

@ObservedV2
export class Sample {
  // For complex objects, use the @Type decorator to ensure successful serialization.
  // TypeDecorator refers to @Type.
  @Type(SampleChild)
  @Trace sampleChild: SampleChild = new SampleChild();
}

@Entry
@ComponentV2
struct Index {
  data: Sample = PersistenceV2.connect(Sample, () => new Sample())!;

  build() {
    Column() {
      Text(`Index add 1 to data.id: ${this.data.sampleChild.id}`)
        .fontSize(30)
        .onClick(() => {
          this.data.sampleChild.id++;
        })
    }
  }
}
```
