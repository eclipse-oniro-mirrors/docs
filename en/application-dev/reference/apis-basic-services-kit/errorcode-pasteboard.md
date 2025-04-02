# Pasteboard Error Codes

> **NOTE**
>
> This topic describes only module-specific error codes. For details about universal error codes, see [Universal Error Codes](../errorcode-universal.md).

## 12900001 Index Out of Range

**Error Message**

The index is out of range.

**Description**

This error code is reported when the index passed in to the called API, such as **getRecord**, is out of range.

**Possible Causes**

The index passed in the API is beyond the record index range of the **PasteData** object. For example, the index passed in to **getRecord** exceeds the number of records.

**Solution**

Check the index range and call the API again with a valid index.

## 12900002 Maximum Number of Records Reached

**Error Message**

The number of records exceeds the upper limit.

**Description**

This error code is reported when no new **PasteData** record can be added.

**Possible Causes**

The number of **PasteData** records has reached the maximum.

**Solution**

1. Check whether the number of **PasteData** records has reached the maximum.
2. If the number of **PasteData** records has reached the maximum, delete some records before adding new ones.

## 12900003 Another Copy or Paste Operation in Progress

**Error Message**

Another copy or paste operation is in progress.

**Description**

This error code is reported when a new copy or paste attempt is made before the previous one is completed.

**Possible Causes**

The copy and paste APIs are both asynchronous APIs. If the data to be copied or pasted is in large amount, the time required may be long. New copy or paste operations can be performed only after the previous operations have been completed.

**Solution**

1. Before you copy or paste data, check the status of the last copy or paste operation.
2. Wait until the last copy or paste operation has finished, and then copy or paste data again.

## 12900004 Copy Prohibited

**Error Message**

Replication is prohibited.

**Description**

This error code is reported when an attempt is made to copy data that cannot be copied.

**Possible Causes**

The data is read-only and cannot be copied.

**Solution**

1. Make sure the target data allows the copy action.
2. Make sure you only copy data that allows for copy.

## 12900005 Request Timeout

**Error Message**

Request timed out.

**Description**

This error code is reported when the time spent in internal data processing exceeds the timeout.

**Possible Causes**

The data to be processed is large and consumes too much time.

**Solution**

If the data to be processed is too large, consider using an asynchronous API.

## 12900006 Settings Already Exists

**Error Message**

Settings already exist.

**Description**

This error code is reported when the global pasteable range of the application to be set already exists.

**Possible Causes**

The global pasteable scope of the application already exists.

**Solution**

Delete the existing settings and then set the new one.

## 12900007 File Copying Failure

**Error Message**

Copy file failed.

**Description**

This error code is reported when a file fails to be copied.

**Possible Causes**

The file fails to be downloaded and copied.

**Solution**

1. Before copying related data, check whether the destination path is valid.
2. If the destination path is invalid, confirm the correct path.

## 12900008 Progress Startup Failure

**Error Message**

Failed to start progress.

**Description**

This error code is reported when the progress fails to be created using the default progress indicator.

**Possible Causes**

The system thread is abnormal.

**Solution**

Check whether the pasting is successful. If yes, ignore this error; otherwise, contact technical support.

## 12900009 Progress Reporting Exception

**Error Message**

Progress exits abnormally.

**Description**

 This error code is reported when the progress reporting on default progress indicator is abnormal.

**Possible Causes**

The progress is displayed abnormally.

**Solution**

Check whether the pasting is successful. If yes, ignore this error; otherwise, contact technical support.

## 12900010 Data Obtaining Failure

**Error Message**

Get Data failed.

**Description**

This error code is reported when the copied data fails to be obtained.

**Possible Causes**

The copied data fails to be obtained.

**Solution**

Contact technical support.
