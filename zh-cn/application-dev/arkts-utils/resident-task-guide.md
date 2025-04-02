# 常驻任务开发指导（Worker）

此处提供使用Worker进行常驻任务的开发指导，Worker会持续执行任务直到宿主线程发出终止指令。

开发过程和示例如下所示：

1. DevEco Studio支持一键生成Worker，在对应的{moduleName}目录下任意位置，点击鼠标右键 &gt; New &gt; Worker，即可自动生成Worker的模板文件及配置信息。本文以创建“Worker”为例。

   此外，还支持手动创建Worker文件，具体方式和相关注意事项请见[创建Worker的注意事项](worker-introduction.md#创建worker的注意事项)。

2. 导入Worker模块。

   ```ts
   // Index.ets
   import { worker } from '@kit.ArkTS';
   ```

3. 在宿主线程中通过调用ThreadWorker的[constructor()](../reference/apis-arkts/js-apis-worker.md#constructor9)方法创建Worker对象，当前线程为宿主线程。

   ```ts
   // Index.ets
   const workerInstance: worker.ThreadWorker = new worker.ThreadWorker('entry/ets/workers/Worker.ets');
   ```

4. 此处宿主线程为UI主线程，宿主线程发送'start'，开始执行某个长期运行的任务并接收子线程返回的相关消息。在不需要执行该任务时发送'stop'，停止该任务执行，该示例中10s后结束该任务。

   ```ts
   // Index.ets
   
   @Entry
   @Component
   struct Index {
     build() {
       Column() {
         Text("Listener task")
           .id('HelloWorld')
           .fontSize(50)
           .fontWeight(FontWeight.Bold)
           .onClick(() => {
             workerInstance.postMessage({type: 'start'})
             workerInstance.onmessage = (event) => {
               console.info('UI主线程收到消息:', event.data);
             }
             // 10秒后停止worker
             setTimeout(() => {
               workerInstance.postMessage({ type: 'stop' });
             }, 10000);
           })
       }
       .height('100%')
       .width('100%')
     }
   }
   ```

5. 在Worker线程中当接受到宿主线程发送的消息为'start'时，开始执行某个长时间不定期运行的任务并实时返回消息给宿主线程。当接收到的消息为'stop'时结束该任务执行并返回相应消息给宿主线程。

   ```ts
   // Worker.ets
   import { ErrorEvent, MessageEvents, ThreadWorkerGlobalScope, worker } from '@kit.ArkTS';
   const workerPort: ThreadWorkerGlobalScope = worker.workerPort;
   let isRunning = false;
   workerPort.onmessage = (e: MessageEvents) => {
     const type = e.data.type as string;
     if (type === 'start') {
       if (!isRunning) {
         isRunning = true;
         // 开始常驻任务
         performTask();
       }
     } else if (type === 'stop') {
       isRunning = false;
       workerPort.close();  // 关闭Worker
     }
   }
   // 模拟常驻任务
   function performTask() {
     if (isRunning) {
       // 模拟某个长期运行的任务
       workerPort.postMessage('Worker is performing a task');
       // 1秒后再次执行任务
       setTimeout(performTask, 1000);
     }
     workerPort.postMessage('Worker is stop performing a task');
   }
   ```
