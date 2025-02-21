# Worker简介

Worker主要作用是为应用程序提供一个多线程的运行环境，可满足应用程序在执行过程中与主线程分离，在后台线程中运行一个脚本操作耗时操作，极大避免类似于计算密集型或高延迟的任务阻塞主线程的运行。具体接口信息及使用方法详情请见[Worker](../reference/apis-arkts/js-apis-worker.md)。


## Worker运作机制

**图1** Worker运作机制示意图

![worker](figures/worker.png)

创建Worker的线程称为宿主线程（不一定是主线程，工作线程也支持创建Worker子线程），Worker自身的线程称为Worker子线程（或Actor线程、工作线程）。每个Worker子线程与宿主线程拥有独立的实例，包含基础设施、对象、代码段等。Worker子线程和宿主线程之间的通信是基于消息传递的，Worker通过序列化机制与宿主线程之间相互通信，完成命令及数据交互。


## Worker注意事项

- 创建Worker时，有手动和自动两种创建方式，手动创建Worker线程目录及文件时，还需同步进行相关配置，详情请参考[创建Worker的注意事项](#创建worker的注意事项)。
- 使用Worker能力时，构造函数中传入的Worker线程文件的路径在不同版本有不同的规则，详情请参见[文件路径注意事项](#文件路径注意事项)。
- Worker创建后需要手动管理生命周期，且最多同时运行的Worker子线程数量为8个，详情请参见[生命周期注意事项](#生命周期注意事项)。
- 由于不同线程中上下文对象是不同的，因此Worker线程只能使用线程安全的库，例如UI相关的非线程安全库不能使用，具体请见[多线程安全注意事项](multi-thread-safety.md)。
- 序列化传输的数据量大小限制为16MB。
- 使用Worker模块时，需要在主线程中注册onerror接口，否则当worker线程出现异常时会发生jscrash问题。
- 不支持跨HAP使用Worker线程文件。

### 创建Worker的注意事项

Worker线程文件需要放在"{moduleName}/src/main/ets/"目录层级之下，否则不会被打包到应用中。有手动和自动两种创建Worker线程目录及文件的方式。

- 手动创建：开发者手动创建相关目录及文件，此时需要配置build-profile.json5的相关字段信息，Worker线程文件才能确保被打包到应用中。

  Stage模型：

  ```json
  "buildOption": {
    "sourceOption": {
      "workers": [
        "./src/main/ets/workers/worker.ets"
      ]
    }
  }
  ```

  FA模型：

  ```json
  "buildOption": {
    "sourceOption": {
      "workers": [
        "./src/main/ets/MainAbility/workers/worker.ets"
      ]
    }
  }
  ```

- 自动创建：DevEco Studio支持一键生成Worker，在对应的{moduleName}目录下任意位置，**点击鼠标右键 > New > Worker**，即可自动生成Worker的模板文件及配置信息，无需再手动在build-profile.json5中进行相关配置。


### 文件路径注意事项

  当使用Worker模块具体功能时，均需先构造Worker实例对象，其构造函数与API版本相关，且构造函数需要传入Worker线程文件的路径（scriptURL）。

```ts
// 导入模块
import worker from '@ohos.worker';

// API 9及之后版本使用：
const worker1: worker.ThreadWorker = new worker.ThreadWorker('entry/ets/workers/MyWorker.ets');
// API 8及之前版本使用：
const worker2: worker.Worker = new worker.Worker('entry/ets/workers/MyWorker.ets');
```

#### Stage模型下的文件路径规则

构造函数中的scriptURL要求如下：

- scriptURL的组成包含 {moduleName}/ets 和相对路径 relativePath。
- relativePath是Worker线程文件和"{moduleName}/src/main/ets/"目录的相对路径。

**1） 加载Ability中Worker线程文件场景**

加载Ability中的worker线程文件，加载路径规则：{moduleName}/ets/{relativePath}。

```ts
import worker from '@ohos.worker';

// worker线程文件所在路径："entry/src/main/ets/workers/worker.ets"
const workerStage1: worker.ThreadWorker = new worker.ThreadWorker('entry/ets/workers/worker.ets');

// worker线程文件所在路径："phone/src/main/ets/ThreadFile/workers/worker.ets"
const workerStage2: worker.ThreadWorker = new worker.ThreadWorker('phone/ets/ThreadFile/workers/worker.ets');
```

2） 加载Library-[HSP](../quick-start/in-app-hsp.md)中Worker线程文件场景

加载HSP中worker线程文件，加载路径规则：{moduleName}/ets/{relativePath}。

```ts
import worker from '@ohos.worker';

// worker线程文件所在路径： "hsp/src/main/ets/workers/worker.ets"
const workerStage3: worker.ThreadWorker = new worker.ThreadWorker('hsp/ets/workers/worker.ets');
```

3） 加载Library-[HAR](../quick-start/har-package.md)中Worker线程文件场景

加载HAR中worker线程文件存在以下两种情况：

- @标识路径加载形式：所有种类的模块加载本地HAR中的Worker线程文件，加载路径规则：@{moduleName}/ets/{relativePath}。

- 相对路径加载形式：本地HAR加载该包内的Worker线程文件，加载路径规则：创建Worker对象所在文件与Worker线程文件的相对路径。

需要注意的是：如果HAR包会被打包成三方包使用，则HAR包中使用Worker仅支持通过相对路径加载形式创建。

```ts
import worker from '@ohos.worker';

// @标识路径加载形式：
// worker线程文件所在路径: "har/src/main/ets/workers/worker.ets"
const workerStage4: worker.ThreadWorker = new worker.ThreadWorker('@har/ets/workers/worker.ets');

// 相对路径加载形式：
// worker线程文件所在路径: "har/src/main/ets/workers/worker.ets"
// 创建Worker对象的文件所在路径："har/src/main/ets/components/mainpage/MainPage.ets"
const workerStage5: worker.ThreadWorker = new worker.ThreadWorker('../../workers/worker.ets');
```

#### FA模型下的文件路径规则

  构造函数中的scriptURL为：Worker线程文件与"{moduleName}/src/main/ets/MainAbility"的相对路径。

```ts
import worker from '@ohos.worker';

// 主要说明以下三种场景：

// 场景1： Worker线程文件所在路径："{moduleName}/src/main/ets/MainAbility/workers/worker.ets"
const workerFA1: worker.ThreadWorker = new worker.ThreadWorker("workers/worker.ets", {name:"first worker in FA model"});

// 场景2： Worker线程文件所在路径："{moduleName}/src/main/ets/workers/worker.ets"
const workerFA2: worker.ThreadWorker = new worker.ThreadWorker("../workers/worker.ets");

// 场景3： Worker线程文件所在路径："{moduleName}/src/main/ets/MainAbility/ThreadFile/workers/worker.ets"
const workerFA3: worker.ThreadWorker = new worker.ThreadWorker("ThreadFile/workers/worker.ets");
```



### 生命周期注意事项

- Worker的创建和销毁耗费性能，建议开发者合理管理已创建的Worker并重复使用。Worker空闲时也会一直运行，因此当不需要Worker时，可以调用[terminate()](../reference/apis-arkts/js-apis-worker.md#terminate9)接口或[parentPort.close()](../reference/apis-arkts/js-apis-worker.md#close9)方法主动销毁Worker。若Worker处于已销毁或正在销毁等非运行状态时，调用其功能接口，会抛出相应的错误。


- Worker存在数量限制，支持最多同时存在8个Worker。当Worker数量超出限制时，会抛出“Worker initialization failure, the number of workers exceeds the maximum.”错误。
