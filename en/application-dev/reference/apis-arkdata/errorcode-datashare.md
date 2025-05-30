# DataShare Error Codes

> **NOTE**
>
> This topic describes only module-specific error codes. For details about universal error codes, see [Universal Error Codes](../errorcode-universal.md).

##  15700000 Internal Error

**Error Message**

Inner error.

**Description**

Internal error.

**Possible Causes**

View the error log to determine the cause of the error. Possible causes include the following:
1. Abnormal internal state.
2. Incorrect use of APIs.
3. Incorrect permission configuration.
4. System errors, such as null pointers, insufficient memory, unexpected restart of data services, I/O errors, IPC exceptions, and JS engine exceptions.

**Solution**

1. Check whether a closed object is reused.
2. Check whether the APIs are called correctly. If not, apply necessary corrections.
3. Check whether the permission configuration is correct.
4. If the problem persists, ask the user to restart or update the application or upgrade the device version.

## 15700010 Failed to Create a DataShareHelper

**Error Message**

The DataShareHelper is not initialized successfully.

**Description**

The **DataShareHelper** class fails to be created.

**Possible Causes**

1. The **uri** specified in **createDataHelper** is incorrect.
2. The **context** specified in **createDataHelper** is incorrect. **DataShare** supports only the stage model.
3. The client application does not have the permission to start **DataShareExtension** from the background when the client attempts to start **DataShareExtension** from the background to create **DataShareHelper**.

**Solution**

1. Obtain the correct URI.
2. Check that the context of the stage model is used.
3. Check whether the client has the read or write permission on data. Perform the following steps:
    (1) Obtain the data provider bundle name from the URI. For example, the bundle name in uri "datashareproxy://com.acts.ohos.data.datasharetest/test" is **com.acts.ohos.data.datasharetest**.
    (2) Obtain the configuration based on the bundle name. For example, run **bm dump --bundle-name com.acts.ohos.data.datasharetest** to obtain the **DataShareExtension** configuration, and check whether the data consumer has **readPermission** or **writePermission**.

## 15700011 URI Not Exist

**Error Message**

The URI does not exist.

**Description**

This error code is generated when a template fails to be added or deleted, or an incorrect URI or path is passed in when silent access is enabled or disabled.

**Possible Causes**

1. The input URI is incorrect.
2. The input URI is in incorrect format.

**Solution**

Obtain the correct URI.

## 15700012 Data Area Not Exist

**Error Message**

The data area does not exist.

**Description**

This error code is returned when a data update fails.

**Possible Causes**

The input parameter **bundleName** of **publish()** is incorrect.

**Solution**

Obtain the correct **bundleName** value from the DataShare server provider.

## 15700013 DataShareHelper Instance Closed

**Error Message**

The DataShareHelper instance is already closed.

**Description**

This error code is generated when a closed **DataShareHelper** instance is used.

**Possible Causes**

The closed **DataShareHelper** instance cannot be used.

**Solution**

Create a new **DataShareHelper** instance for use.
