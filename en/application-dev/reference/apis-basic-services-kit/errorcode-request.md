# Upload and Download Error Codes

> **NOTE**
>
> This topic describes only module-specific error codes. For details about universal error codes, see [Universal Error Codes](../errorcode-universal.md).

## 13400001 File Operation Error

**Error Message**

File operation error.

**Description**

This error code is reported when a file operation error occurs in invoking the **uploadFile** or **downloadFile** API.

**Possible Causes**

The file permission is insufficient.

**Solution**

Make sure you have the required permission on the target files.

## 13400002 File Path Error

**Error Message**

Bad file path.

**Description**

This error code is reported when a file path error occurs in invoking the **uploadFile** or **downloadFile** API.

**Possible Causes**

The file path is incorrect or the file already exists in the path.

**Solution**

Verify the file path.

## 13400003 Service Error

**Error Message**

Task service ability error.

**Description**

This error code is reported when a task manager service error occurs in invoking the **downloadFile** API.

**Possible Causes**

The task fails to be created.

**Solution**

Verify the task settings.

## 13499999 Other Error

**Error Message**

other error.

**Description**

This error code is reported when a special error occurs in invoking the **uploadFile** or **downloadFile** API.

**Possible Causes**

The task fails to be created.

**Solution**

Verify the task settings.


## 21900004 Application Task Queue Full

**Error Message**

application task queue full error.

**Description**

This error code is reported when the application task queue is full.

**Possible Causes**

The application fails to create a background task (resources are preempted by foreground tasks, where no task queue is involved).

**Solution**

1. Obtain all background tasks of the application through the query API.

2. Proactively remove tasks not needed to release the quota.

3. Create a background task again.

## 21900005 Task Mode Error

**Error Message**

task mode error.

**Description**

This error code is reported when a task mode error occurs.

**Possible Causes**

The application attempts to create a foreground task when it is not running in the foreground.

**Solution**

1. Register and deregister an event listener for a foreground application.

2. Follow the instructions in the API reference document.

## 21900006 Task Not Found

**Error Message**

task not found error.

**Description**

This error code is reported when the task is not found.

**Possible Causes**

The task to remove or query does not exist.

**Solution**

1. Query existing tasks through the query API.

2. Check whether the target task exists. (The system periodically deletes junk tasks.)

3. Verify the task ID and try again.

## 21900007 Operation Not Supported in Current State

**Error Message**

task state error.

**Description**

This error code is reported when the operation performed is not supported.

**Possible Causes**

1. The task to start has been deleted.

2. The task to start has not been initialized.

3. The task to pause is not being executed.

4. The task to resume is not paused.

5. The task to stop is not being executed.

**Solution**

1. Check the task status.

2. Perform the operation supported by the current task status.
