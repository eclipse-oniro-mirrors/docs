# I/O Intensive Task Development (TaskPool)


I/O intensive tasks are tasks that require frequent I/O operations such as disk read/write and network communication. While asynchronous concurrency can address the thread blocking issue for single I/O tasks, it falls short in the case of I/O intensive tasks. This is where multithread concurrency comes into play.


The performance focus of I/O intensive tasks is not the CPU processing capability, but the speed and efficiency of I/O operations, since such a task usually requires frequent operations such as disk read/write and network communication. The following uses frequent read/write operations on a system file to simulate concurrency processing of I/O intensive tasks.


1. Define a concurrency function that internally calls I/O capabilities intensively.
    ```ts
    // a.ts
    import fs from '@ohos.file.fs';

    // Define a concurrency function that internally calls I/O capabilities intensively.
    // Write data to the file.
    export async function write(data: string, filePath: string): Promise<void> {
      let file: fs.File = await fs.open(filePath, fs.OpenMode.READ_WRITE);
      await fs.write(file.fd, data);
      fs.close(file);
    }
    ```

	```ts
    import { write } from './a'
    import { BusinessError } from '@ohos.base';

    @Concurrent
    async function concurrentTest(fileList: string[]): Promise<boolean> {
      // Write data to the file cyclically.
      for (let i: number = 0; i < fileList.length; i++) {
        write('Hello World!', fileList[i]).then(() => {
          console.info(`Succeeded in writing the file. FileList: ${fileList[i]}`);
        }).catch((err: BusinessError) => {
          console.error(`Failed to write the file. Code is ${err.code}, message is ${err.message}`)
          return false;
        })
      }
      return true;
    }
	```

2. Use **TaskPool** to execute the concurrency function that contains the intensive I/O operations. Specifically, call [execute()](../reference/apis-arkts/js-apis-taskpool.md#taskpoolexecute) to execute the tasks and process the scheduling result in a callback. For details about how to obtain **filePath1** and **filePath2** in the example, see [Obtaining Application File Paths](../application-models/application-context-stage.md#obtaining-application-file-paths).

    ```ts
    import taskpool from '@ohos.taskpool';

    let filePath1: string = "path1"; // Application file path.
    let filePath2: string = "path2";

    // Use TaskPool to execute the concurrency function that contains the intensive I/O operations.
    // In the case of a large array, the distribution of I/O intensive tasks also preempts the main thread. Therefore, multiple threads are required.
    taskpool.execute(concurrentTest, [filePath1, filePath2]).then(() => {
      // Process the scheduling result.
    })
    ```
