# TaskPool Introduction

TaskPool provides a multithreading environment for applications. It helps reduce resource consumption and improve system performance. It also frees you from caring about the lifecycle of thread instances. For details about the APIs and their usage, see [TaskPool](../reference/apis-arkts/js-apis-taskpool.md).


## TaskPool Operating Mechanism

**Figure 1** TaskPool operating mechanism

![TaskPool](figures/taskpool.png)

With TaskPool, you can encapsulate tasks in the main thread and throw the tasks to the task queue. The system selects proper worker threads to distribute and execute the tasks, and then returns the result to the main thread. TaskPool provides APIs to execute and cancel tasks, and set the task priority. It minimizes system resource usage through unified thread management, dynamic scheduling, and load balancing. By default, the system starts a worker thread and increases the thread quantity as the number of tasks increases. The maximum number of worker threads that can be created depends on the number of physical cores of the device. The actual number is managed internally to ensure optimal scheduling and execution efficiency. If no task is distributed for a long period of time, the system reduces the number of worker threads.


## Precautions for TaskPool

- A task function must be decorated with [\@Concurrent](arkts-concurrent.md) and can be used only in .ets files.

- Since API version 11, if a function that implements a task needs to use a class method, the class must be decorated with [\@Sendable](arkts-sendable.md) and used only in .ets files.

- A task function in the TaskPool worker thread must finish the execution within 3 minutes (excluding the time used for Promise or async/await asynchronous call, for example, the duration of I/O tasks such as network download and file read/write). Otherwise, it forcibly exits.

- Input parameter types in a task function must be those supported by serialization. For details, see [Serialization Types Supported by TaskPool and Worker](serialization-support-types.md).

- Parameters of the ArrayBuffer type are transferred in TaskPool by default. You can set the transfer list by calling [setTransferList()](../reference/apis-arkts/js-apis-taskpool.md#settransferlist10).

- Context objects vary in different threads. Therefore, the worker thread of TaskPool can use only a thread-safe library, but not a non-thread-safe library (for example, UI-related non-thread-safe library). For details, see [Precautions for Multithread Safe](multi-thread-safety.md).

- A maximum of 16 MB data can be serialized.
