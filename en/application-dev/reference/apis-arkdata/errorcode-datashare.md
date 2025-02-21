# DataShare Error Codes

> **NOTE**
>
> This topic describes only module-specific error codes. For details about universal error codes, see [Universal Error Codes](../errorcode-universal.md).

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
    (1) Obtain the data provider bundle name in the path of the URI. For example, the bundle name in uri = "datashareproxy://com.acts.ohos.data.datasharetest/test" is **com.acts.ohos.data.datasharetest**.
    (2) Obtain the configuration based on the bundle name. For example, run **bm dump --bundle-name com.acts.ohos.data.datasharetest** to obtain the **DataShareExtension** configuration, and check whether the data consumer has **readPermission** or **writePermission**.

## 15700011 Failed to Add or Delete a Template

**Error Message**

The uri does not exist.

**Description**

This error code is returned when a template fails to be added or deleted.

**Possible Causes**

1. The input parameter **uri** of **addTemplate()** is incorrect.
2. The input parameter **uri** of **delTemplate()** is incorrect.

**Solution**

Obtain the correct URI.

## 15700012 Data Area Not Exist

**Error Message**

The data area does not exist.

**Description**

This error code is returned when a data update operaton fails.

**Possible Causes**

The input parameter **bundleName** of **publish()** is incorrect.

**Solution**

Obtain the correct **bundleName** value from the DataShare server provider.
