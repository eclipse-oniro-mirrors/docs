# Sensor Error Codes

> **NOTE**
>
> This topic describes only module-specific error codes. For details about universal error codes, see [Universal Error Codes](errorcode-universal.md).

## 14500101 Service Exception

**Error Message**

Service exception.

**Description**

This error code is reported if the HDI service is abnormal when the **on**, **once**, or **off** interface of the sensor module is called.

**Possible Causes**

The HDI service is abnormal.

**Solution**

1. Retry the operation at a specified interval (for example, 1s) or at an exponential increase interval.
2. If the operation fails for three consecutive times, stop the retry. You can also attempt to obtain the sensor list to check for device availability.
