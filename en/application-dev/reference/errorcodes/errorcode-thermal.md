# Thermal Manager Error Codes

> **NOTE**
>
> This topic describes only module-specific error codes. For details about universal error codes, see [Universal Error Codes](errorcode-universal.md).

## 4800101 Service Connection Failure

**Error Message**

Operation failed. Cannot connect to service.

**Description**

This error code is reported for a service connection failure.

**Possible Causes**

1. The system service stops running.

2. The internal communication of system services is abnormal.

**Solution**

Check whether the system services are running properly.

1. Run the following command on the console to view the current system service list:

    ```bash
    > hdc shell hidumper -ls
    ```

2. Check whether **ThermalService** is included in the system service list.
