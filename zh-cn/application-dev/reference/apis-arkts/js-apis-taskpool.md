# @ohos.taskpool（启动任务池）

任务池（taskpool）作用是为应用程序提供一个多线程的运行环境，降低整体资源的消耗、提高系统的整体性能，且您无需关心线程实例的生命周期。您可以使用任务池API创建后台任务（Task），并对所创建的任务进行如任务执行、任务取消的操作。理论上您可以使用任务池API创建数量不受限制的任务，但是出于内存因素不建议您这样做。此外，不建议您在任务中执行阻塞操作，特别是无限期阻塞操作，长时间的阻塞操作占据工作线程，可能会阻塞其他任务调度，影响您的应用性能。

您所创建的同一优先级任务的执行顺序可以由您决定，任务真实执行的顺序与您调用任务池API提供的任务执行接口顺序一致。任务默认优先级是MEDIUM。

当同一时间待执行的任务数量大于任务池工作线程数量，任务池会根据负载均衡机制进行扩容，增加工作线程数量，减少整体等待时长。同样，当执行的任务数量减少，工作线程数量大于执行任务数量，部分工作线程处于空闲状态，任务池会根据负载均衡机制进行缩容，减少工作线程数量。

任务池API以数字形式返回错误码。有关各个错误码的更多信息，请参阅文档[语言基础类库错误码](errorcode-utils.md)。

taskpool使用过程中的相关注意点请查[TaskPool注意事项](../../arkts-utils/taskpool-introduction.md#taskpool注意事项)。

> **说明：**<br/>
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import taskpool from '@ohos.taskpool';
```
## taskpool.execute

execute(func: Function, ...args: Object[]): Promise\<Object>

将待执行的函数放入taskpool内部任务队列等待，等待分发到工作线程执行。当前执行模式不可取消任务。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型      | 必填 | 说明                                                                   |
| ------ | --------- | ---- | ---------------------------------------------------------------------- |
| func   | Function  | 是   | 执行的逻辑需要传入函数，必须使用[@Concurrent装饰器](../../arkts-utils/arkts-concurrent.md)装饰，支持的函数返回值类型请查[序列化支持类型](#序列化支持类型)。     |
| args   | Object[] | 否   | 执行逻辑的函数所需要的入参，支持的参数类型请查[序列化支持类型](#序列化支持类型)。默认值为undefined。 |

**返回值：**

| 类型              | 说明                                 |
| ----------------- | ------------------------------------ |
| Promise\<Object>  | Promise对象，返回任务函数的执行结果。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                      |
| -------- | -------------------------------------------- |
| 10200003 | Worker initialization failure.               |
| 10200006 | An exception occurred during serialization.  |
| 10200014 | The function is not mark as concurrent.      |

**示例：**

```ts
@Concurrent
function printArgs(args: number): number {
    console.info("printArgs: " + args);
    return args;
}

taskpool.execute(printArgs, 100).then((value: Object) => { // 100: test number
  console.info("taskpool result: " + value);
});
```

## taskpool.execute

execute(task: Task, priority?: Priority): Promise\<Object>

将创建好的任务放入taskpool内部任务队列等待，等待分发到工作线程执行。当前执行模式可以设置任务优先级和尝试调用cancel进行任务取消。该任务不可以是任务组任务和串行队列任务。该任务可以多次调用execute执行。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型                  | 必填 | 说明                                       |
| -------- | --------------------- | ---- | ---------------------------------------- |
| task     | [Task](#task)         | 是   | 需要在任务池中执行的任务。                  |
| priority | [Priority](#priority) | 否   | 等待执行的任务的优先级，该参数默认值为taskpool.Priority.MEDIUM。 |

**返回值：**

| 类型              | 说明              |
| ----------------  | ---------------- |
| Promise\<Object> | Promise对象，返回任务函数的执行结果。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                     |
| -------- | ------------------------------------------- |
| 10200003 | Worker initialization failure.              |
| 10200006 | An exception occurred during serialization. |
| 10200014 | The function is not mark as concurrent.     |

**示例：**

```ts
@Concurrent
function printArgs(args: number): number {
    console.info("printArgs: " + args);
    return args;
}

let task1: taskpool.Task = new taskpool.Task(printArgs, 100); // 100: test number
let task2: taskpool.Task = new taskpool.Task(printArgs, 200); // 200: test number
let task3: taskpool.Task = new taskpool.Task(printArgs, 300); // 300: test number
taskpool.execute(task1, taskpool.Priority.LOW).then((value: Object) => {
  console.info("taskpool result1: " + value);
});
taskpool.execute(task2, taskpool.Priority.MEDIUM).then((value: Object) => {
  console.info("taskpool result2: " + value);
});
taskpool.execute(task3, taskpool.Priority.HIGH).then((value: Object) => {
  console.info("taskpool result3: " + value);
});
```

## taskpool.execute<sup>10+</sup>

execute(group: TaskGroup, priority?: Priority): Promise<Object[]>

将创建好的任务组放入taskpool内部任务队列等待，等待分发到工作线程执行。任务组中任务全部执行完成后，结果数组统一返回。当前执行模式适用于执行一组有关联的任务。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名     | 类型                        | 必填 | 说明                                                           |
| --------- | --------------------------- | ---- | -------------------------------------------------------------- |
| group     | [TaskGroup](#taskgroup10)     | 是   | 需要在任务池中执行的任务组。                                      |
| priority  | [Priority](#priority)       | 否   | 等待执行的任务组的优先级，该参数默认值为taskpool.Priority.MEDIUM。 |

**返回值：**

| 类型                 | 说明                               |
| ----------------    | ---------------------------------- |
| Promise\<Object[]>  | Promise对象数组，返回任务函数的执行结果。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                     |
| -------- | ------------------------------------------- |
| 10200006 | An exception occurred during serialization. |

**示例：**

```ts
@Concurrent
function printArgs(args: number): number {
    console.info("printArgs: " + args);
    return args;
}

let taskGroup1: taskpool.TaskGroup = new taskpool.TaskGroup();
taskGroup1.addTask(printArgs, 10); // 10: test number
taskGroup1.addTask(printArgs, 20); // 20: test number
taskGroup1.addTask(printArgs, 30); // 30: test number

let taskGroup2: taskpool.TaskGroup = new taskpool.TaskGroup();
let task1: taskpool.Task = new taskpool.Task(printArgs, 100); // 100: test number
let task2: taskpool.Task = new taskpool.Task(printArgs, 200); // 200: test number
let task3: taskpool.Task = new taskpool.Task(printArgs, 300); // 300: test number
taskGroup2.addTask(task1);
taskGroup2.addTask(task2);
taskGroup2.addTask(task3);
taskpool.execute(taskGroup1).then((res: Array<Object>) => {
  console.info("taskpool execute res is:" + res);
});
taskpool.execute(taskGroup2).then((res: Array<Object>) => {
  console.info("taskpool execute res is:" + res);
});
```

## taskpool.executeDelayed<sup>11+</sup>

executeDelayed(delayTime: number, task: Task, priority?: Priority): Promise\<Object>

延时执行任务。当前执行模式可以设置任务优先级和尝试调用cancel进行任务取消。该任务不可以是任务组任务和串行队列任务。该任务可以多次调用executeDelayed执行。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名       | 类型          | 必填 | 说明                 |
| ----------- | ------------- | ---- | -------------------- |
| delayTime   | number        | 是   | 延时时间。单位为ms。  |
| task        | [Task](#task) | 是   | 需要延时执行的任务。 |
| priority    | [Priority](#priority)       | 否   | 延时执行的任务的优先级，该参数默认值为taskpool.Priority.MEDIUM。 |

**返回值：**

| 类型                 | 说明                               |
| ----------------    | ---------------------------------- |
| Promise\<Object>  | Promise对象，返回任务函数的执行结果。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID   | 错误信息                         |
| --------- | -------------------------------- |
| 10200028 | The delayTime is less than zero. |

**示例：**

```ts
// import BusinessError
import { BusinessError } from '@ohos.base'

@Concurrent
function printArgs(args: number): void {
    console.info("printArgs: " + args);
}

let t: number = Date.now();
console.info("taskpool start time is: " + t);
let task: taskpool.Task = new taskpool.Task(printArgs, 100); // 100: test number
taskpool.executeDelayed(1000, task).then(() => { // 1000:delayTime is 1000ms
  console.info("taskpool execute success");
}).catch((e: BusinessError) => {
  console.error(`taskpool execute: Code: ${e.code}, message: ${e.message}`);
})
```


## taskpool.cancel

cancel(task: Task): void

取消任务池中的任务。当任务在taskpool等待队列中，取消该任务后该任务将不再执行，并返回undefined作为结果；当任务已经在taskpool工作线程执行，取消该任务并不影响任务继续执行，执行结果在catch分支返回，搭配isCanceled使用可以对任务取消行为作出响应。taskpool.cancel对其之前的taskpool.execute/taskpool.executeDelayed生效。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型          | 必填 | 说明                 |
| ------ | ------------- | ---- | -------------------- |
| task   | [Task](#task) | 是   | 需要取消执行的任务。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                      |
| -------- | -------------------------------------------- |
| 10200015 | The task does not exist when it is canceled. |
| 10200016 | The task is executing when it is canceled.   |

从API version10开始，此接口调用时不再涉及上报错误码10200016。

**正在执行的任务取消示例：**

```ts
@Concurrent
function inspectStatus(arg: number): number {
  // 第一次检查任务是否已经取消并作出响应
  if (taskpool.Task.isCanceled()) {
    console.info("task has been canceled before 2s sleep.");
    return arg + 2;
  }
  // 2s sleep
  let t: number = Date.now();
  while (Date.now() - t < 2000) {
    continue;
  }
  // 第二次检查任务是否已经取消并作出响应
  if (taskpool.Task.isCanceled()) {
    console.info("task has been canceled after 2s sleep.");
    return arg + 3;
  }
  return arg + 1;
}

function concurrntFunc() {
  let task1: taskpool.Task = new taskpool.Task(inspectStatus, 100); // 100: test number
  let task2: taskpool.Task = new taskpool.Task(inspectStatus, 200); // 200: test number
  let task3: taskpool.Task = new taskpool.Task(inspectStatus, 300); // 300: test number
  let task4: taskpool.Task = new taskpool.Task(inspectStatus, 400); // 400: test number
  let task5: taskpool.Task = new taskpool.Task(inspectStatus, 500); // 500: test number
  let task6: taskpool.Task = new taskpool.Task(inspectStatus, 600); // 600: test number
  taskpool.execute(task1).then((res: Object)=>{
    console.info("taskpool test result: " + res);
  });
  taskpool.execute(task2);
  taskpool.execute(task3);
  taskpool.execute(task4);
  taskpool.execute(task5);
  taskpool.execute(task6);
  // 1s后取消task
  setTimeout(()=>{
    try {
      taskpool.cancel(task1);
    } catch (e) {
      console.error(`taskpool: cancel error code: ${e.code}, info: ${e.message}`);
    }
  }, 1000);
}

concurrntFunc();
```

## taskpool.cancel<sup>10+</sup>

cancel(group: TaskGroup): void

取消任务池中的任务组。当一个任务组的任务未全部执行结束时取消任务组，返回undefined作为任务组结果。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型                    | 必填 | 说明                 |
| ------- | ----------------------- | ---- | -------------------- |
| group   | [TaskGroup](#taskgroup10) | 是   | 需要取消执行的任务组。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                                 |
| -------- | ------------------------------------------------------- |
| 10200018 | The task group does not exist when it is canceled.      |

**示例：**

```ts
@Concurrent
function printArgs(args: number): number {
  let t: number = Date.now();
  while (Date.now() - t < 2000) {
    continue;
  }
  console.info("printArgs: " + args);
  return args;
}

function concurrntFunc() {
  let taskGroup1: taskpool.TaskGroup = new taskpool.TaskGroup();
  taskGroup1.addTask(printArgs, 10); // 10: test number
  let taskGroup2: taskpool.TaskGroup = new taskpool.TaskGroup();
  taskGroup2.addTask(printArgs, 100); // 100: test number
  taskpool.execute(taskGroup1).then((res: Array<Object>)=>{
    console.info("taskGroup1 res is:" + res);
  });
  taskpool.execute(taskGroup2).then((res: Array<Object>)=>{
    console.info("taskGroup2 res is:" + res);
  });
  setTimeout(()=>{
    try {
      taskpool.cancel(taskGroup2);
    } catch (e) {
      console.error(`taskpool: cancel error code: ${e.code}, info: ${e.message}`);
    }
  }, 1000);
}

concurrntFunc();
```


## taskpool.getTaskPoolInfo<sup>10+</sup>

getTaskPoolInfo(): TaskPoolInfo

获取任务池内部信息，包含线程信息和任务信息。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型                                | 说明                |
| ----------------------------------- | ------------------ |
| [TaskPoolInfo](#taskpoolinfo10)   | 任务池的内部信息。   |

**示例：**

```ts
let taskpoolInfo: taskpool.TaskPoolInfo = taskpool.getTaskPoolInfo();
```

## Priority

表示所创建任务（Task）执行时的优先级。

**系统能力：**  SystemCapability.Utils.Lang

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| HIGH   | 0    | 任务为高优先级。 |
| MEDIUM | 1 | 任务为中优先级。 |
| LOW | 2 | 任务为低优先级。 |

**示例：**

```ts
@Concurrent
function printArgs(args: number): number {
  let t: number = Date.now();
  while (Date.now() - t < 1000) { // 1000: delay 1s
    continue;
  }
  console.info("printArgs: " + args);
  return args;
}

let allCount = 100; // 100: test number
let taskArray: Array<taskpool.Task> = [];
// 创建300个任务并添加至taskArray
for (let i: number = 1; i < allCount; i++) {
  let task1: taskpool.Task = new taskpool.Task(printArgs, i);
  taskArray.push(task1);
  let task2: taskpool.Task = new taskpool.Task(printArgs, i * 10); // 10: test number
  taskArray.push(task2);
  let task3: taskpool.Task = new taskpool.Task(printArgs, i * 100); // 100: test number
  taskArray.push(task3);
}

// 从taskArray中获取不同的任务并给定不同优先级执行
for (let i: number = 0; i < allCount; i+=3) { // 3: 每次执行3个任务，循环取任务时需后移3项，确保执行的是不同的任务
  taskpool.execute(taskArray[i], taskpool.Priority.HIGH);
  taskpool.execute(taskArray[i + 1], taskpool.Priority.LOW);
  taskpool.execute(taskArray[i + 2], taskpool.Priority.MEDIUM);
}
```

## Task

表示任务。使用[constructor](#constructor)方法构造Task。任务可以多次执行或放入任务组执行或放入串行队列执行或添加依赖关系执行。

### constructor

constructor(func: Function, ...args: Object[])

Task的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型      | 必填 | 说明                                                                  |
| ------ | --------- | ---- | -------------------------------------------------------------------- |
| func   | Function  | 是   | 执行的逻辑需要传入函数，必须使用[@Concurrent装饰器](../../arkts-utils/arkts-concurrent.md)装饰，支持的函数返回值类型请查[序列化支持类型](#序列化支持类型)。     |
| args   | Object[] | 否   | 任务执行传入函数的入参，支持的参数类型请查[序列化支持类型](#序列化支持类型)。默认值为undefined。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                 |
| -------- | --------------------------------------- |
| 10200014 | The function is not mark as concurrent. |

**示例：**

```ts
@Concurrent
function printArgs(args: number): number {
  console.info("printArgs: " + args);
  return args;
}

let task: taskpool.Task = new taskpool.Task(printArgs, "this is my first Task");
```

### constructor<sup>11+</sup>

constructor(name: string, func: Function, ...args: Object[])

Task的构造函数，可以指定任务名称。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型     | 必填 | 说明                                                         |
| ------ | -------- | ---- | ------------------------------------------------------------ |
| name   | string   | 是   | 任务名称。                                                   |
| func   | Function  | 是   | 执行的逻辑需要传入函数，必须使用[@Concurrent装饰器](../../arkts-utils/arkts-concurrent.md)装饰，支持的函数返回值类型请查[序列化支持类型](#序列化支持类型)。     |
| args   | Object[] | 否   | 任务执行传入函数的入参，支持的参数类型请查[序列化支持类型](#序列化支持类型)。默认值为undefined。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                |
| -------- | --------------------------------------- |
| 10200014 | The function is not mark as concurrent. |

**示例：**

```ts
@Concurrent
function printArgs(args: string): string {
  console.info("printArgs: " + args);
  return args;
}

let taskName: string = "taskName";
let task: taskpool.Task = new taskpool.Task(taskName, printArgs, "this is my first Task");
let name: string = task.name;
```

### isCanceled<sup>10+</sup>

static isCanceled(): boolean

检查当前正在运行的任务是否已取消。使用该方法前需要先构造Task。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型    | 说明                                 |
| ------- | ------------------------------------ |
| boolean | 如果当前正在运行的任务被取消返回true，未被取消返回false。|

**示例：**

```ts
@Concurrent
function inspectStatus(arg: number): number {
    // do something
    if (taskpool.Task.isCanceled()) {
      console.info("task has been canceled.");
      // do something
      return arg + 1;
    }
    // do something
    return arg;
}
```

> **说明：**<br/>
> isCanceled方法需要和taskpool.cancel方法搭配使用，如果不调用cancel方法，isCanceled方法默认返回false。

**示例：**

```ts
@Concurrent
function inspectStatus(arg: number): number {
  // 第一次检查任务是否已经取消并作出响应
  if (taskpool.Task.isCanceled()) {
    console.info("task has been canceled before 2s sleep.");
    return arg + 2;
  }
  // 延时2s
  let t: number = Date.now();
  while (Date.now() - t < 2000) {
    continue;
  }
  // 第二次检查任务是否已经取消并作出响应
  if (taskpool.Task.isCanceled()) {
    console.info("task has been canceled after 2s sleep.");
    return arg + 3;
  }
  return arg + 1;
}

let task: taskpool.Task = new taskpool.Task(inspectStatus, 100); // 100: test number
taskpool.execute(task).then((res: Object)=>{
  console.info("taskpool test result: " + res);
}).catch((err: string) => {
  console.error("taskpool test occur error: " + err);
});
// 不调用cancel，isCanceled()默认返回false，task执行的结果为101
```

### setTransferList<sup>10+</sup>

setTransferList(transfer?: ArrayBuffer[]): void

设置任务的传输列表。使用该方法前需要先构造Task。不调用该接口，则传给任务的数据中的ArrayBuffer默认transfer转移。

> **说明：**<br/>
> 此接口可以设置任务池中ArrayBuffer的transfer列表，transfer列表中的ArrayBuffer对象在传输时不会复制buffer内容到工作线程而是转移buffer控制权至工作线程，传输后当前的ArrayBuffer失效。若ArrayBuffer为空，则不会transfer转移。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型           | 必填 | 说明                                          |
| -------- | ------------- | ---- | --------------------------------------------- |
| transfer | ArrayBuffer[] | 否   | 可传输对象是ArrayBuffer的实例对象，默认为空数组。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                                        |
| -------- | -------------------------------------------------------------- |
| 10200029 | Can not set an arraybuffer to both transferList and cloneList. |

**示例：**

```ts
@Concurrent
function testTransfer(arg1: ArrayBuffer, arg2: ArrayBuffer): number {
  console.info("testTransfer arg1 byteLength: " + arg1.byteLength);
  console.info("testTransfer arg2 byteLength: " + arg2.byteLength);
  return 100;
}

let buffer: ArrayBuffer = new ArrayBuffer(8);
let view: Uint8Array = new Uint8Array(buffer);
let buffer1: ArrayBuffer = new ArrayBuffer(16);
let view1: Uint8Array = new Uint8Array(buffer1);

console.info("testTransfer view byteLength: " + view.byteLength);
console.info("testTransfer view1 byteLength: " + view1.byteLength);
// 执行结果为：
// testTransfer view byteLength: 8
// testTransfer view1 byteLength: 16

let task: taskpool.Task = new taskpool.Task(testTransfer, view, view1);
task.setTransferList([view.buffer, view1.buffer]);
taskpool.execute(task).then((res: Object)=>{
  console.info("test result: " + res);
}).catch((e: string)=>{
  console.error("test catch: " + e);
})
console.info("testTransfer view2 byteLength: " + view.byteLength);
console.info("testTransfer view3 byteLength: " + view1.byteLength);
// 经过transfer转移之后值为0，执行结果为：
// testTransfer view2 byteLength: 0
// testTransfer view3 byteLength: 0
```


### setCloneList<sup>11+</sup>

setCloneList(cloneList: Object[] | ArrayBuffer[]): void

设置任务的拷贝列表。使用该方法前需要先构造Task。

> **说明：**<br/>
> 当前仅支持拷贝，[@Sendable装饰器](../../arkts-utils/arkts-sendable.md)需搭配该接口使用，否则会抛异常。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名    | 类型                      | 必填 | 说明                                          |
| --------- | ------------------------ | ---- | --------------------------------------------- |
| cloneList | Object[] \| ArrayBuffer[]  | 是 | - 传入数组的类型必须为[SendableClass](../../arkts-utils/arkts-sendable.md#基本概念)或ArrayBuffer。<br/>- 所有传入cloneList的对象持有的SendableClass实例或ArrayBuffer类型对象，在线程间传输的行为都会变成拷贝，即修改传输后的对象不会对原有对象产生任何影响。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                                        |
| -------- | -------------------------------------------------------------- |
| 10200029 | Can not set an arraybuffer to both transferList and cloneList. |

**示例：**

```ts
// sendable.ets
// 定义两个Sendable class：BaseClass及其子类DeriveClass
@Sendable
export class BaseClass {
  private str: string = "sendable: BaseClass";
  static num :number = 10;
  str1: string = "sendable: this is BaseClass's string";
  num1: number = 5;
  isDone1: boolean = false;

  private fibonacciRecursive(n: number): number {
    if (n <= 1) {
      return n;
    } else {
      return this.fibonacciRecursive(n - 1) + this.fibonacciRecursive(n - 2);
    }
  }

  private privateFunc(num: number): number{
    let res: number = this.fibonacciRecursive(num);
    console.info("sendable: BaseClass privateFunc res is: " + res);
    return res;
  }

  publicFunc(num: number): number {
    return this.privateFunc(num);
  }

  get GetNum(): number {
    return this.num1;
  }
  set SetNum(num: number) {
    this.num1 = num;
  }

  constructor(){
    console.info(this.str);
    this.isDone1 = true;
  }
}

@Sendable
export class DeriveClass extends BaseClass {
  name: string = "sendable: this is DeriveClass";
  printName() {
    console.info(this.name);
  }
  constructor() {
    super();
  }
}
```


```ts
// index.ets
// 主线程调用taskpool，在taskpool线程中调用BaseClass和DeriveClass的方法、访问对应属性
import taskpool from '@ohos.taskpool'
import { BusinessError } from '@ohos.base'
import { BaseClass, DeriveClass } from './sendable'

@Concurrent
function testFunc(arr: Array<BaseClass>, num: number): number {
  let baseInstance1 = arr[0];
  console.info("sendable: str1 is: " + baseInstance1.str1);
  baseInstance1.SetNum = 100;
  console.info("sendable: num1 is: " + baseInstance1.GetNum);
  console.info("sendable: isDone1 is: " + baseInstance1.isDone1);
  // 获取斐波那契数列第num项的结果
  let res: number = baseInstance1.publicFunc(num);
  return res;
}

@Concurrent
function printLog(arr: Array<DeriveClass>): void {
  let deriveInstance = arr[0];
  deriveInstance.printName();
}

@Entry
@Component
struct Index {
  @State message: string = 'Hello World'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
        Button() {
          Text("TaskPool Test")
        }.onClick(() => {
          // task1访问调用BaseClass.str1/BaseClass.SetNum/BaseClass.GetNum/BaseClass.isDone1/BaseClass.publicFunc
          let baseInstance1: BaseClass = new BaseClass();
          let array1 = new Array<BaseClass>();
          array1.push(baseInstance1);
          let task1 = new taskpool.Task(testFunc, array1, 10);
          task1.setCloneList(array1);
          taskpool.execute(task1).then((res: Object) => {
            console.info("sendable: task1 res is: " + res);
          }).catch((e:BusinessError) => {
            console.error(`sendable: task1 execute Code is ${e.code}, message is ${e.message}`);
          })

          // task2调用DeriveClass.printName
          let deriveInstance: DeriveClass = new DeriveClass();
          let array2 = new Array<DeriveClass>();
          array2.push(deriveInstance);
          let task2 = new taskpool.Task(printLog, array2);
          task2.setCloneList(array2);
          taskpool.execute(task2).then(() => {
            console.info("sendable: task2 execute success");
          }).catch((e:BusinessError) => {
            console.error(`sendable: task2 execute Code is ${e.code}, message is ${e.message}`);
          })
        })
        .height('15%')
        .width('30%')
      }
      .width('100%')
    }
    .height('100%')
  }
}
```


### sendData<sup>11+</sup>

static sendData(...args: Object[]): void

在任务执行过程中向宿主线程发送消息并触发回调。使用该方法前需要先构造Task。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型          | 必填 | 说明                                              |
| -------- | ------------- | ---- | ------------------------------------------------- |
| args     | Object[]      | 是   | 可传输对象默认转移，作为回调函数的参数，支持的参数类型请查[序列化支持类型](#序列化支持类型)。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                 |
| -------- | --------------------------------------- |
| 10200006  | An exception occurred during serialization. |
| 10200022  | The function is not called in the taskpool thread. |
| 10200023  | The function is not called in the concurrent function. |
| 10200024  | The callback is not registered on the host side. |

**示例：**

```ts
@Concurrent
function ConcurrentFunc(num: number): number {
  let res: number = num * 10;
  taskpool.Task.sendData(res);
  return num;
}
```

### onReceiveData<sup>11+</sup>

onReceiveData(callback?: Function): void

为任务注册回调函数，以接收和处理来自任务池工作线程的数据。使用该方法前需要先构造Task。

> **说明：**<br/>
> 不支持给同一个任务定义多种回调函数，如果重复赋值只有最后一个会生效。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| callback | Function | 否   | 处理数据的回调函数，发送到宿主线程的数据将会作为入参传入该回调函数。不传参可以取消注册的回调函数。 |

**示例：**

```ts
@Concurrent
function ConcurrentFunc(num: number): number {
  let res: number = num * 10;
  taskpool.Task.sendData(res);
  return num;
}

function pringLog(data: number): void {
  console.info("taskpool: data is: " + data);
}

async function testFunc(): Promise<void> {
  try {
    let task: taskpool.Task = new taskpool.Task(ConcurrentFunc, 1);
    task.onReceiveData(pringLog);
    await taskpool.execute(task);
  } catch (e) {
    console.error(`taskpool: error code: ${e.code}, info: ${e.message}`);
  }
}

testFunc();
```

### addDependency<sup>11+</sup>

addDependency(...tasks: Task[]): void

为当前任务添加对其他任务的依赖。使用该方法前需要先构造Task。该任务和被依赖的任务不可以是任务组任务、串行队列任务和已执行的任务。存在依赖关系的任务（依赖其他任务的任务或被依赖的任务）执行后不可以再次执行。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| tasks  | [Task](#task)[] | 是   | 被依赖的任务数组。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                        |
| -------- | ------------------------------- |
| 10200026 | There is a circular dependency. |

**示例：**

```ts
@Concurrent
function delay(args: number): number {
  let t: number = Date.now();
  while ((Date.now() - t) < 1000) {
	continue;
  }
  return args;
}

let task1:taskpool.Task = new taskpool.Task(delay, 100);
let task2:taskpool.Task = new taskpool.Task(delay, 200);
let task3:taskpool.Task = new taskpool.Task(delay, 200);

console.info("dependency: add dependency start");
task1.addDependency(task2);
task2.addDependency(task3);
console.info("dependency: add dependency end");

console.info("dependency: start execute second")
taskpool.execute(task1).then(() => {
  console.info("dependency: second task1 success");
})
taskpool.execute(task2).then(() => {
  console.info("dependency: second task2 success");
})
taskpool.execute(task3).then(() => {
  console.info("dependency: second task3 success");
})
```

### removeDependency<sup>11+</sup>

removeDependency(...tasks: Task[]): void

删除当前任务对其他任务的依赖。使用该方法前需要先构造Task。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| tasks  | [Task](#task)[] | 是   | 被依赖的任务数组。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 10200027 | The dependency does not exist. |

**示例：**

```ts
@Concurrent
function delay(args: number): number {
  let t: number = Date.now();
  while ((Date.now() - t) < 1000) {
	continue;
  }
  return args;
}

let task1:taskpool.Task = new taskpool.Task(delay, 100);
let task2:taskpool.Task = new taskpool.Task(delay, 200);
let task3:taskpool.Task = new taskpool.Task(delay, 200);

console.info("dependency: add dependency start");
task1.addDependency(task2);
task2.addDependency(task3);
console.info("dependency: add dependency end");
console.info("dependency: remove dependency start");
task1.removeDependency(task2);
task2.removeDependency(task3);
console.info("dependency: remove dependency end");

console.info("dependency: start execute")
taskpool.execute(task1).then(() => {
  console.info("dependency: task1 success");
})
taskpool.execute(task2).then(() => {
  console.info("dependency: task2 success");
})
taskpool.execute(task3).then(() => {
  console.info("dependency: task3 success");
})
```

### 属性

**系统能力：** SystemCapability.Utils.Lang

| 名称                 | 类型       | 可读 | 可写 | 说明                                                         |
| -------------------- | --------- | ---- | ---- | ------------------------------------------------------------ |
| function             | Function  | 是   | 是   | 创建任务时需要传入的函数，支持的函数返回值类型请查[序列化支持类型](#序列化支持类型)。 |
| arguments            | Object[]  | 是   | 是   | 创建任务传入函数所需的参数，支持的参数类型请查[序列化支持类型](#序列化支持类型)。 |
| name<sup>11+</sup>   | string    | 是   | 是   | 创建任务时指定的任务名称。                                    |
| totalDuration<sup>11+</sup>  | number    | 是   | 否   | 执行任务总耗时。                                    |
| ioDuration<sup>11+</sup>     | number    | 是   | 否   | 执行任务异步IO耗时。                                    |
| cpuDuration<sup>11+</sup>    | number    | 是   | 否   | 执行任务CPU耗时。                                    |

## TaskGroup<sup>10+</sup>

表示任务组，一次执行一组任务，适用于执行一组有关联的任务。如果所有任务正常执行，异步执行完毕后返回所有任务结果的数组，数组中元素的顺序与[addTask](#addtask10-1)的顺序相同；如果任意任务失败，则会抛出对应异常。任务组可以多次执行，但执行后不能新增任务。使用[constructor](#constructor10)方法构造TaskGroup。

### constructor<sup>10+</sup>

constructor()

TaskGroup的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

```ts
let taskGroup = new taskpool.TaskGroup();
```

### constructor<sup>11+</sup>

constructor(name: string)

TaskGroup的构造函数，可以指定任务组名称。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型   | 必填 | 说明         |
| ------ | ------ | ---- | ------------ |
| name   | string | 是   | 任务组名称。 |

**示例：**

```ts
let taskGroupName: string = "groupName";
let taskGroup: taskpool.TaskGroup = new taskpool.TaskGroup(taskGroupName);
let name: string = taskGroup.name;
```

### addTask<sup>10+</sup>

addTask(func: Function, ...args: Object[]): void

将待执行的函数添加到任务组中。使用该方法前需要先构造TaskGroup。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型      | 必填 | 说明                                                                   |
| ------ | --------- | ---- | ---------------------------------------------------------------------- |
| func   | Function  | 是   | 执行的逻辑需要传入函数，必须使用[@Concurrent装饰器](../../arkts-utils/arkts-concurrent.md)装饰，支持的函数返回值类型请查[序列化支持类型](#序列化支持类型)。     |
| args   | Object[] | 否   | 任务执行函数所需要的入参，支持的参数类型请查[序列化支持类型](#序列化支持类型)。默认值为undefined。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                 |
| -------- | --------------------------------------- |
| 10200014 | The function is not mark as concurrent. |

**示例：**

```ts
@Concurrent
function printArgs(args: number): number {
  console.info("printArgs: " + args);
  return args;
}

let taskGroup: taskpool.TaskGroup = new taskpool.TaskGroup();
taskGroup.addTask(printArgs, 100); // 100: test number
```

### addTask<sup>10+</sup>

addTask(task: Task): void

将创建好的任务添加到任务组中。使用该方法前需要先构造TaskGroup。任务组不可以添加其他任务组任务、串行队列任务、有依赖关系的任务和已执行的任务。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型                  | 必填 | 说明                                       |
| -------- | --------------------- | ---- | ---------------------------------------- |
| task     | [Task](#task)         | 是   | 需要添加到任务组中的任务。                  |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                 |
| -------- | --------------------------------------- |
| 10200014 | The function is not mark as concurrent. |

**示例：**

```ts
@Concurrent
function printArgs(args: number): number {
  console.info("printArgs: " + args);
  return args;
}

let taskGroup: taskpool.TaskGroup = new taskpool.TaskGroup();
let task: taskpool.Task = new taskpool.Task(printArgs, 200); // 200: test number
taskGroup.addTask(task);
```

### 属性

**系统能力：** SystemCapability.Utils.Lang

| 名称 | 类型   | 可读 | 可写 | 说明                         |
| ---- | ------ | ---- | ---- | ---------------------------- |
| name<sup>11+</sup> | string | 是   | 是   | 创建任务组时指定的任务组名称。 |

## SequenceRunner <sup>11+</sup>

表示串行队列的任务，用于执行一组需要串行执行的任务。使用[constructor](#constructor11-3)方法构造SequenceRunner。

### constructor<sup>11+</sup>

constructor(priority?: Priority)

SequenceRunner的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型                  | 必填 | 说明                                                       |
| -------- | --------------------- | ---- | ---------------------------------------------------------- |
| priority | [Priority](#priority) | 否   | 指定任务的优先级，该参数默认值为taskpool.Priority.MEDIUM。 |

**示例：**

```ts
let runner: taskpool.SequenceRunner = new taskpool.SequenceRunner();
```

### execute<sup>11+</sup>

execute(task: Task): Promise\<Object>

执行串行任务。使用该方法前需要先构造SequenceRunner。串行队列不可以执行任务组任务、其他串行队列任务、有依赖关系的任务和已执行的任务。

> **说明：**
>
> - 不支持加入存在依赖的任务。
> - 前面的任务执行失败或取消不影响后续任务执行。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型          | 必填 | 说明                             |
| ------ | ------------- | ---- | -------------------------------- |
| task   | [Task](#task) | 是   | 需要添加到串行任务队列中的任务。 |

**返回值：**

| 类型             | 说明                              |
| ---------------- | --------------------------------- |
| Promise\<Object> | Promise对象，返回任务执行的结果。 |

**错误码：**

以下错误码的详细介绍请参见[语言基础类库错误码](errorcode-utils.md)。

| 错误码ID | 错误信息                                    |
| -------- | ------------------------------------------- |
| 10200003 | Worker initialization failure.              |
| 10200006 | An exception occurred during serialization. |
| 10200025 | Add dependent task to SequenceRunner.       |

**示例：**

```ts
@Concurrent
function additionDelay(delay:number): void {
  let start: number = new Date().getTime();
  while (new Date().getTime() - start < delay) {
    continue;
  }
}
@Concurrent
function waitForRunner(finalString: string): string {
  return finalString;
}
async function seqRunner()
{
  let finalString:string = "";
  let task1:taskpool.Task = new taskpool.Task(additionDelay, 3000);
  let task2:taskpool.Task = new taskpool.Task(additionDelay, 2000);
  let task3:taskpool.Task = new taskpool.Task(additionDelay, 1000);
  let task4:taskpool.Task = new taskpool.Task(waitForRunner, finalString);

  let runner:taskpool.SequenceRunner = new taskpool.SequenceRunner();
  runner.execute(task1).then(() => {
    finalString += 'a';
    console.info("seqrunner: task1 done.");
  });
  runner.execute(task2).then(() => {
    finalString += 'b';
    console.info("seqrunner: task2 done");
  });
  runner.execute(task3).then(() => {
    finalString += 'c';
    console.info("seqrunner: task3 done");
  });
  await runner.execute(task4);
  console.info("seqrunner: task4 done, finalString is " + finalString);
}
```

## State<sup>10+</sup>

表示任务（Task）状态的枚举。当任务创建成功后，调用execute，任务进入taskpool等待队列，状态设置为WAITING；任务从等待队列出来进入taskpool工作线程中，任务状态更新为RUNNING；当任务执行完成，返回结果后任务状态重置为WAITING；当主动cancel任务时，将任务状态更新为CANCELED。

**系统能力：**  SystemCapability.Utils.Lang

| 名称      | 值        | 说明          |
| --------- | -------- | ------------- |
| WAITING   | 1        | 任务正在等待。 |
| RUNNING   | 2        | 任务正在执行。 |
| CANCELED  | 3        | 任务已被取消。 |


## TaskInfo<sup>10+</sup>

任务的内部信息。

**系统能力：** SystemCapability.Utils.Lang

### 属性

**系统能力：** SystemCapability.Utils.Lang

| 名称     | 类型                | 可读 | 可写 | 说明                                                           |
| -------- | ------------------ | ---- | ---- | ------------------------------------------------------------- |
| taskId   | number             | 是   | 否   | 任务的ID。                                                     |
| state    | [State](#state10)  | 是   | 否   | 任务的状态。                                                    |
| duration | number             | 是   | 否   | 任务执行至当前所用的时间，单位为ms。当返回为0时，表示任务未执行；返回为空时，表示没有任务执行。  |

## ThreadInfo<sup>10+</sup>

工作线程的内部信息。

**系统能力：** SystemCapability.Utils.Lang

### 属性

**系统能力：** SystemCapability.Utils.Lang

| 名称     | 类型                    | 可读 | 可写 | 说明                                                      |
| -------- | ---------------------- | ---- | ---- | -------------------------------------------------------- |
| tid      | number                 | 是   | 否   | 工作线程的标识符。返回为空时，代表没有任务执行。              |
| taskIds  | number[]               | 是   | 否   | 在当前线程上运行的任务id列表。返回为空时，代表没有任务执行。   |
| priority | [Priority](#priority)  | 是   | 否   | 当前线程的优先级。返回为空时，代表没有任务执行。              |

## TaskPoolInfo<sup>10+</sup>

任务池的内部信息。

**系统能力：** SystemCapability.Utils.Lang

### 属性

**系统能力：** SystemCapability.Utils.Lang

| 名称          | 类型                              | 可读 | 可写 | 说明                  |
| ------------- | -------------------------------- | ---- | ---- | -------------------- |
| threadInfos   | [ThreadInfo[]](#threadinfo10)    | 是   | 否   | 工作线程的内部信息。   |
| taskInfos     | [TaskInfo[]](#taskinfo10)        | 是   | 否   | 任务的内部信息。       |


## 其他说明

### 序列化支持类型
序列化支持类型包括：All Primitive Type(不包括symbol)、Date、String、RegExp、Array、Map、Set、Object、ArrayBuffer、TypedArray。详情可见[TaskPool和Worker支持的序列化类型](../../arkts-utils/serialization-support-types.md)。

### 简单使用

**示例一**

```ts
// 支持普通函数、引用入参传递
@Concurrent
function printArgs(args: string): string {
  console.info("func: " + args);
  return args;
}
async function taskpoolExecute(): Promise<void> {
  // taskpool.execute(task)
  let task: taskpool.Task = new taskpool.Task(printArgs, "create task, then execute");
  console.info("taskpool.execute(task) result: " + await taskpool.execute(task));
  // taskpool.execute(function)
  console.info("taskpool.execute(function) result: " + await taskpool.execute(printArgs, "execute task by func"));
}
taskpoolExecute();
```

**示例二**

```ts
// b.ets
export let c: string = "hello";
```
```ts
// 引用import变量
// a.ets(与b.ets位于同一目录中)
import { c } from "./b";

@Concurrent
function printArgs(a: string): string {
    console.info(a);
    console.info(c);
    return a;
}

async function taskpoolExecute(): Promise<void> {
  // taskpool.execute(task)
  let task: taskpool.Task = new taskpool.Task(printArgs, "create task, then execute");
  console.info("taskpool.execute(task) result: " + await taskpool.execute(task));

  // taskpool.execute(function)
  console.info("taskpool.execute(function) result: " + await taskpool.execute(printArgs, "execute task by func"));
}

taskpoolExecute();
```

**示例三**

```ts
// 支持async函数
@Concurrent
async function delayExcute(): Promise<Object> {
  let ret = await Promise.all<Object>([
    new Promise<Object>(resolve => setTimeout(resolve, 1000, "resolved"))
  ]);
  return ret;
}

async function taskpoolExecute(): Promise<void> {
  taskpool.execute(delayExcute).then((result: Object) => {
    console.info("taskPoolTest task result: " + result);
  }).catch((err: string) => {
    console.error("taskpool test occur error: " + err);
  });
}

taskpoolExecute();
```

**示例四**

```ts
// c.ets
import taskpool from '@ohos.taskpool';

@Concurrent
function strSort(inPutArr: Array<string>): Array<string> {
  let newArr = inPutArr.sort();
  return newArr;
}
export async function func1(): Promise<void> {
  console.info("taskpoolTest start");
  let strArray: Array<string> = ['c test string', 'b test string', 'a test string'];
  let task: taskpool.Task = new taskpool.Task(strSort, strArray);
  console.info("func1 result:" + await taskpool.execute(task));
}

export async function func2(): Promise<void> {
  console.info("taskpoolTest2 start");
  let strArray: Array<string> = ['c test string', 'b test string', 'a test string'];
  taskpool.execute(strSort, strArray).then((result: Object) => {
    console.info("func2 result: " + result);
  }).catch((err: string) => {
    console.error("taskpool test occur error: " + err);
  });
}
```

```ts
// index.ets
import { func1, func2 } from "./c";

func1();
func2();
```

**示例五**

```ts
// 任务取消成功
@Concurrent
function inspectStatus(arg: number): number {
  // 第一次检查任务是否已经取消并作出响应
  if (taskpool.Task.isCanceled()) {
    console.info("task has been canceled before 2s sleep.");
    return arg + 2;
  }
  // 2s sleep
  let t: number = Date.now();
  while (Date.now() - t < 2000) {
    continue;
  }
  // 第二次检查任务是否已经取消并作出响应
  if (taskpool.Task.isCanceled()) {
    console.info("task has been canceled after 2s sleep.");
    return arg + 3;
  }
  return arg + 1;
}

async function taskpoolCancel(): Promise<void> {
  let task: taskpool.Task = new taskpool.Task(inspectStatus, 100); // 100: test number
  taskpool.execute(task).then((res: Object)=>{
    console.info("taskpool test result: " + res);
  }).catch((err: string) => {
    console.error("taskpool test occur error: " + err);
  });
  // 1s后取消task
  setTimeout(()=>{
    try {
      taskpool.cancel(task);
    } catch (e) {
      console.error(`taskpool: cancel error code: ${e.code}, info: ${e.message}`);
    }
  }, 1000);
}

taskpoolCancel();
```

**示例六**

```ts
// 已执行的任务取消失败
@Concurrent
function inspectStatus(arg: number): number {
  // 第一次检查任务是否已经取消并作出响应
  if (taskpool.Task.isCanceled()) {
    return arg + 2;
  }
  // 延时2s
  let t: number = Date.now();
  while (Date.now() - t < 500) {
    continue;
  }
  // 第二次检查任务是否已经取消并作出响应
  if (taskpool.Task.isCanceled()) {
    return arg + 3;
  }
  return arg + 1;
}

async function taskpoolCancel(): Promise<void> {
  let task: taskpool.Task = new taskpool.Task(inspectStatus, 100); // 100: test number
  taskpool.execute(task).then((res: Object)=>{
    console.info("taskpool test result: " + res);
  }).catch((err: string) => {
    console.error("taskpool test occur error: " + err);
  });

  setTimeout(()=>{
    try {
      taskpool.cancel(task); // 任务已执行,取消失败
    } catch (e) {
      console.error(`taskpool: cancel error code: ${e.code}, info: ${e.message}`);
    }
  }, 3000); // 延时3s，确保任务已执行
}

taskpoolCancel();
```

**示例七**

```ts
// 待执行的任务组取消成功
@Concurrent
function printArgs(args: number): number {
  let t: number = Date.now();
  while (Date.now() - t < 1000) {
    continue;
  }
  console.info("printArgs: " + args);
  return args;
}

async function taskpoolGroupCancelTest(): Promise<void> {
  let taskGroup1: taskpool.TaskGroup = new taskpool.TaskGroup();
  taskGroup1.addTask(printArgs, 10); // 10: test number
  taskGroup1.addTask(printArgs, 20); // 20: test number
  taskGroup1.addTask(printArgs, 30); // 30: test number
  let taskGroup2: taskpool.TaskGroup = new taskpool.TaskGroup();
  let task1: taskpool.Task = new taskpool.Task(printArgs, 100); // 100: test number
  let task2: taskpool.Task = new taskpool.Task(printArgs, 200); // 200: test number
  let task3: taskpool.Task = new taskpool.Task(printArgs, 300); // 300: test number
  taskGroup2.addTask(task1);
  taskGroup2.addTask(task2);
  taskGroup2.addTask(task3);
  taskpool.execute(taskGroup1).then((res: Array<Object>) => {
    console.info("taskpool execute res is:" + res);
  }).catch((e: string) => {
    console.error("taskpool execute error is:" + e);
  });
  taskpool.execute(taskGroup2).then((res: Array<Object>) => {
    console.info("taskpool execute res is:" + res);
  }).catch((e: string) => {
    console.error("taskpool execute error is:" + e);
  });

  try {
    taskpool.cancel(taskGroup2);
  } catch (e) {
    console.error(`taskpool: cancel error code: ${e.code}, info: ${e.message}`);
  }
}

taskpoolGroupCancelTest()
```

**示例八**

```ts
// 分别创建执行100个高、中、低优先级的任务，查看其各项信息
@Concurrent
function delay(): void {
  let start: number = new Date().getTime();
  while (new Date().getTime() - start < 500) {
    continue;
  }
}

let highCount: number = 0;
let mediumCount: number = 0;
let lowCount: number = 0;
let allCount: number = 100;
for (let i = 0; i < allCount; i++) {
  let task1: taskpool.Task = new taskpool.Task(delay);
  let task2: taskpool.Task = new taskpool.Task(delay);
  let task3: taskpool.Task = new taskpool.Task(delay);
  taskpool.execute(task1, taskpool.Priority.LOW).then(() => {
    lowCount++;
  }).catch((e: string) => {
    console.error("low task error: " + e);
  })
  taskpool.execute(task2, taskpool.Priority.MEDIUM).then(() => {
    mediumCount++;
  }).catch((e: string) => {
    console.error("medium task error: " + e);
  })
  taskpool.execute(task3, taskpool.Priority.HIGH).then(() => {
    highCount++;
  }).catch((e: string) => {
    console.error("high task error: " + e);
  })
}
let start: number = new Date().getTime();
while (new Date().getTime() - start < 1000) {
  continue;
}
let taskpoolInfo: taskpool.TaskPoolInfo = taskpool.getTaskPoolInfo();
let tid: number = 0;
let taskIds: Array<number> = [];
let priority: number = 0;
let taskId: number = 0;
let state: number = 0;
let duration: number = 0;
let threadIS = Array.from(taskpoolInfo.threadInfos)
for(let threadInfo of threadIS) {
  tid = threadInfo.tid;
  if (threadInfo.taskIds != undefined && threadInfo.priority != undefined )
  {
    taskIds.length = threadInfo.taskIds.length;
    priority = threadInfo.priority;
  }
  console.info("taskpool---tid is:" + tid + ", taskIds is:" + taskIds + ", priority is:" + priority);
}
let taskIS = Array.from(taskpoolInfo.taskInfos)
for(let taskInfo of taskIS) {
  taskId = taskInfo.taskId;
  state = taskInfo.state;
  if (taskInfo.duration != undefined )
  {
    duration = taskInfo.duration;
  }
  console.info("taskpool---taskId is:" + taskId + ", state is:" + state + ", duration is:" + duration);
}
```