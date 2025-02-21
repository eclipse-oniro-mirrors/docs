# @ohos.net.connection (Network Connection Management)

The network connection management module provides basic network management capabilities. You can obtain the default active data network or the list of all active data networks, enable or disable the airplane mode, and obtain network capability information.

> **NOTE**
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import connection from '@ohos.net.connection';
```

## connection.createNetConnection

createNetConnection(netSpecifier?: NetSpecifier, timeout?: number): NetConnection

Creates a **NetConnection** object, where [netSpecifier](#netspecifier) specifies the network, and **timeout** specifies the timeout duration in ms. **timeout** is configurable only when **netSpecifier** is specified. If neither of them is present, the default network is used.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name      | Type                         | Mandatory| Description                                                        |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| netSpecifier | [NetSpecifier](#netspecifier) | No  | Network specifier, which specifies the characteristics of a network. If this parameter is not set or is set to **undefined**, the default network is used.                  |
| timeout      | number                        | No  | Timeout duration for obtaining the network specified by **netSpecifier**. This parameter is valid only when **netSpecifier** is specified. The default value is **0** if **netSpecifier** is **undefined**.|

**Return value**

| Type                           | Description                |
| ------------------------------- | -------------------- |
| [NetConnection](#netconnection) | Handle of the network specified by **netSpecifier**.|

**Example**

```ts
import connection from '@ohos.net.connection';

// For the default network, you do not need to pass in parameters.
let netConnection = connection.createNetConnection();

// For the cellular network, you need to pass in related network parameters. If the timeout parameter is not specified, the timeout value is 0 by default.
let netConnectionCellular = connection.createNetConnection({
  netCapabilities: {
    bearerTypes: [connection.NetBearType.BEARER_CELLULAR]
  }
});
```

## connection.getDefaultNet

getDefaultNet(callback: AsyncCallback\<NetHandle>): void

Obtains the default active data network. This API uses an asynchronous callback to return the result. You can use [getNetCapabilities](#connectiongetnetcapabilities) to obtain information such as the network type and capabilities.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                                   | Mandatory| Description                                                        |
| -------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<[NetHandle](#nethandle)> | Yes  | Callback used to return the result. If the default activated data network is obtained successfully, **error** is **undefined** and **data** is the default activated data network. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getDefaultNet((error: BusinessError, data: connection.NetHandle) => {
  if (error) {
    console.error(`Failed to get default net. Code:${error.code}, message:${error.message}`);
    return;
  }
  console.info("Succeeded to get data " + JSON.stringify(data));
});
```

## connection.getDefaultNet

getDefaultNet(): Promise\<NetHandle>

Obtains the default active data network. This API uses a promise to return the result. You can use [getNetCapabilities](#connectiongetnetcapabilities) to obtain information such as the network type and capabilities.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type                             | Description                                 |
| --------------------------------- | ------------------------------------- |
| Promise\<[NetHandle](#nethandle)> | Promise used to return the result.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
connection.getDefaultNet().then((data: connection.NetHandle) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
});
```

## connection.getDefaultNetSync<sup>9+</sup>

getDefaultNetSync(): NetHandle

Obtains the default active data network in synchronous mode. You can use [getNetCapabilities](#connectiongetnetcapabilities) to obtain information such as the network type and capabilities.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type     | Description                              |
| --------- | ---------------------------------- |
| [NetHandle](#nethandle) | Handle of the default active data network.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

let netHandle = connection.getDefaultNetSync();
```


## connection.setAppHttpProxy<sup>11+</sup>

setAppHttpProxy(httpProxy: HttpProxy): void;

Sets the application-level HTTP proxy configuration of the network.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name   | Type                                                        | Mandatory| Description            |
| --------- | ------------------------------------------------------------ | ---- | ---------------- |
| httpProxy | [HttpProxy](#httpproxy10)                                      | Yes  | Application-level HTTP proxy configuration.|

**Error codes**

| ID| Error Message                      |
| ------- | -----------------------------  |
| 401     | Parameter error.               |
| 2100001 | Invalid http proxy.            |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

let exclusionStr = "192.168,baidu.com";
let exclusionArray = exclusionStr.split(',');
connection.setAppHttpProxy({
  host: "192.168.xx.xxx",
  port: 8080,
  exclusionList: exclusionArray
} as connection.HttpProxy);
```

**Preset certificate PIN:**

A certificate PIN is the hash value calculated using the SHA256 algorithm for a certificate file.
For the **server.pem** certificate, you can use the following openssl command to calculate its PIN:

```shell
cat server.pem \
| sed -n '/-----BEGIN/,/-----END/p' \
| openssl x509 -noout -pubkey \
| openssl pkey -pubin -outform der \
| openssl dgst -sha256 -binary \
| openssl enc -base64
```

**Preset application-level certificate:**

The original certificate file is preset in the application. Currently, certificate files in the **.crt** and **.pem** formats are supported.

**Preset JSON configuration file:**

The mapping between preset certificates and network servers is configured in a JSON configuration file.
The configuration file is stored in the **src/main/resources/base/profile/network_config.json** directory of the application.

**JSON configuration file:**

The following is an example configuration of the certificate pin:
```json
{
  "network-security-config": {
    "domain-config": [
      {
        "domains": [
          {
            "include-subdomains": true,
            "name": "server.com"
          }
        ],
        "pin-set": {
          "expiration": "2024-11-08",
          "pin": [
            {
              "digest-algorithm": "sha256",
              "digest": "FEDCBA987654321"
            }
          ]
        }
      }
    ]
  }
}
```

The following is an example configuration of the application-level certificate:
```json
{
  "network-security-config": {
    "base-config": {
      "trust-anchors": [
        {
          "certificates": "/etc/security/certificates"
        }
      ]
    },
    "domain-config": [
      {
        "domains": [
          {
            "include-subdomains": true,
            "name": "example.com"
          }
        ],
        "trust-anchors": [
          {
            "certificates": "/data/storage/el1/bundle/entry/resources/resfile"
          }
        ]
      }
    ]
  }
}

```

**Description of fields**

**network-security-config (object: network security configuration)**

This field can contain zero or one **base-config**.

This field must contain one **domain-config**.

**base-config (object: application-wide security configuration)**

This field must contain one **trust-anchors**.

**domain-config (array: security configuration of each domain)**

This field can contain any number of items.

An item must contain one **domain**.

An item can contain zero or one **trust-anchors**.

An item can contain zero or one **pin-set**.

**trust-anchors (array: trusted CA)**

This field can contain any number of items.

An item must contain one **certificates** (string: CA certificate path).

**domain (array: domain)**

This field can contain any number of items.

An item must contain one **name** (string: domain name).

An item can contain zero or one **include-subdomains** (boolean: whether a rule is applicable to subdomains).

**pin-set (object: certificate PIN setting)**

This field must contain one **pin**.

This field can contain zero or one **expiration** (string: expiration time of the certificate PIN).

**pin (array: certificate PIN)**

This field can contain any number of items.

An item must contain one **digest-algorithm** (string: digest algorithm used to generate the PIN).

An item must contain one **digest** (string: public key PIN).

## connection.getDefaultHttpProxy<sup>10+</sup>

getDefaultHttpProxy(callback: AsyncCallback\<HttpProxy>): void

Obtains the default HTTP proxy configuration of the network.
If the global proxy is set, the global HTTP proxy configuration is returned. If [setAppNet](#connectionsetappnet9) is used to bind the application to the network specified by [NetHandle](#nethandle), the HTTP proxy configuration of this network is returned. In other cases, the HTTP proxy configuration of the default network is returned.
This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                                  | Mandatory| Description                                                        |
| -------- | -------------------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback<[HttpProxy](#httpproxy10)> | Yes  | Callback used to return the result. If the global HTTP proxy configuration of the network is obtained successfully, **error** is **undefined** and **data** is the global HTTP proxy configuration. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                                    |
| -------- | -------------------------------------------- |
| 2100002  | Operation failed. Cannot connect to service. |
| 2100003  | System internal error.                       |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getDefaultHttpProxy((error: BusinessError, data: connection.HttpProxy) => {
  if (error) {
    console.error(`Failed to get default http proxy. Code:${error.code}, message:${error.message}`);
    return;
  }
  console.log("Succeeded to get data" + JSON.stringify(data));
});
```

## connection.getDefaultHttpProxy<sup>10+</sup>

getDefaultHttpProxy(): Promise\<HttpProxy>;

Obtains the default HTTP proxy configuration of the network.
If the global proxy is set, the global HTTP proxy configuration is returned. If [setAppNet](#connectionsetappnet9) is used to bind the application to the network specified by [NetHandle](#nethandle), the HTTP proxy configuration of this network is returned. In other cases, the HTTP proxy configuration of the default network is returned.
This API uses a promise to return the result.

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type                            | Description                                     |
| -------------------------------- | ----------------------------------------- |
| Promise<[HttpProxy](#httpproxy10)> | Promise used to return the result.|

**Error codes**

| ID| Error Message                                    |
| -------- | -------------------------------------------- |
| 2100002  | Operation failed. Cannot connect to service. |
| 2100003  | System internal error.                       |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getDefaultHttpProxy().then((data: connection.HttpProxy) => {
  console.info(JSON.stringify(data));
}).catch((error: BusinessError) => {
  console.info(JSON.stringify(error));
});
```

## connection.getAppNet<sup>9+</sup>

getAppNet(callback: AsyncCallback\<NetHandle>): void

Obtains information about the network bound to an application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                                   | Mandatory| Description                                                        |
| -------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<[NetHandle](#nethandle)> | Yes  | Callback used to return the result. If information about the network bound to the application is successfully obtained, **error** is **undefined** and **data** is the obtained network information. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 401 | Parameter error.|
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getAppNet((error: BusinessError, data: connection.NetHandle) => {
  if (error) {
    console.error(`Failed to get app net. Code:${error.code}, message:${error.message}`);
    return;
  }
  console.info("Succeeded to get data: " + JSON.stringify(data));
})
```

## connection.getAppNet<sup>9+</sup>

getAppNet(): Promise\<NetHandle>;

Obtains information about the network bound to an application. This API uses a promise to return the result.

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type                             | Description                                 |
| --------------------------------- | ------------------------------------- |
| Promise\<[NetHandle](#nethandle)> | Promise used to return the result.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 401 | Parameter error.|
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getAppNet().then((data: connection.NetHandle) => {
  console.info(JSON.stringify(data));
}).catch((error: BusinessError) => {
  console.info(JSON.stringify(error));
});
```

## connection.getAppNetSync<sup>10+</sup>

getAppNetSync(): NetHandle

Obtains information about the network bound to an application. This API returns the result synchronously.

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type     | Description                              |
| --------- | ---------------------------------- |
| [NetHandle](#nethandle) | Handle of the data network bound to the application.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

let netHandle = connection.getAppNetSync();
```

## connection.setAppNet<sup>9+</sup>

setAppNet(netHandle: NetHandle, callback: AsyncCallback\<void>): void

Binds an application to the specified network, so that the application can access the external network only through this network. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name   | Type                   | Mandatory| Description                                                        |
| --------- | ----------------------- | ---- | ------------------------------------------------------------ |
| netHandle | [NetHandle](#nethandle) | Yes  | Handle of the data network.                                            |
| callback  | AsyncCallback\<void>    | Yes  | Callback used to return the result. If the application is successfully bound to the specified network, **error** is **undefined**. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getDefaultNet((error: BusinessError, netHandle: connection.NetHandle) => {
  connection.setAppNet(netHandle, (error: BusinessError, data: void) => {
    if (error) {
      console.error(`Failed to get default net. Code:${error.code}, message:${error.message}`);
      return;
    }
    console.info("Succeeded to get data: " + JSON.stringify(data));
  });
});
```

## connection.setAppNet<sup>9+</sup>

setAppNet(netHandle: NetHandle): Promise\<void>;

Binds an application to the specified network, so that the application can access the external network only through this network. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name   | Type                                                        | Mandatory| Description            |
| --------- | ------------------------------------------------------------ | ---- | ---------------- |
| netHandle | [NetHandle](#nethandle)                                      | Yes  | Handle of the data network.|

**Return value**

| Type                                       | Description                         |
| ------------------------------------------- | ----------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  connection.setAppNet(netHandle).then(() => {
    console.log("success");
  }).catch((error: BusinessError) => {
    console.log(JSON.stringify(error));
  })
});
```

## connection.getAllNets

getAllNets(callback: AsyncCallback&lt;Array&lt;NetHandle&gt;&gt;): void

Obtains the list of all connected networks. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;Array&lt;[NetHandle](#nethandle)&gt;&gt; | Yes| Callback used to return the result. If the list of all connected networks is obtained successfully, **error** is **undefined** and **data** is the list of activated data networks. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getAllNets((error: BusinessError, data: connection.NetHandle[]) => {
  if (error) {
    console.error(`Failed to get all nets. Code:${error.code}, message:${error.message}`);
    return;
  }
  console.info("Succeeded to get data: " + JSON.stringify(data));
}); 
```

## connection.getAllNets

getAllNets(): Promise&lt;Array&lt;NetHandle&gt;&gt;

Obtains the list of all connected networks. This API uses a promise to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;Array&lt;[NetHandle](#nethandle)&gt;&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

connection.getAllNets().then((data: connection.NetHandle[]) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
});
```

## connection.getAllNetsSync<sup>10+</sup>

getAllNetsSync(): Array&lt;NetHandle&gt;

Obtains the list of all connected networks. This API returns the result synchronously.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type     | Description                              |
| --------- | ---------------------------------- |
| Array&lt;[NetHandle](#nethandle)&gt; | List of all activated data networks.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

let netHandle = connection.getAllNetsSync();
```

## connection.getConnectionProperties

getConnectionProperties(netHandle: NetHandle, callback: AsyncCallback\<ConnectionProperties>): void

Obtains connection properties of the network corresponding to the **netHandle**. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name   | Type                                                        | Mandatory| Description                                                        |
| --------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| netHandle | [NetHandle](#nethandle)                                      | Yes  | Handle of the data network.                                            |
| callback  | AsyncCallback\<[ConnectionProperties](#connectionproperties)> | Yes  | Callback used to return the result. If the connection properties of the network corresponding to the **netHandle** is obtained successfully, **error** is **undefined** and **data** is the obtained network connection information. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  connection.getConnectionProperties(netHandle, (error: BusinessError, data: connection.ConnectionProperties) => {
    if (error) {
      console.error(`Failed to get connection properties. Code:${error.code}, message:${error.message}`);
      return;
    }
    console.info("Succeeded to get data: " + JSON.stringify(data));
  })
});
```

## connection.getConnectionProperties

getConnectionProperties(netHandle: NetHandle): Promise\<ConnectionProperties>

Obtains connection properties of the network corresponding to the **netHandle**. This API uses a promise to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name   | Type                   | Mandatory| Description            |
| --------- | ----------------------- | ---- | ---------------- |
| netHandle | [NetHandle](#nethandle) | Yes  | Handle of the data network.|

**Return value**

| Type                                                   | Description                             |
| ------------------------------------------------------- | --------------------------------- |
| Promise\<[ConnectionProperties](#connectionproperties)> | Promise used to return the result.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  connection.getConnectionProperties(netHandle).then((data: connection.ConnectionProperties) => {
    console.info("Succeeded to get data: " + JSON.stringify(data));
  })
});
```

## connection.getConnectionPropertiesSync<sup>10+</sup>

getConnectionPropertiesSync(netHandle: NetHandle): ConnectionProperties

Obtains network connection information based on the specified **netHandle**.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name   | Type                   | Mandatory| Description            |
| --------- | ----------------------- | ---- | ---------------- |
| netHandle | [NetHandle](#nethandle) | Yes  | Handle of the data network.|

**Return value**

| Type                                                   | Description                             |
| ------------------------------------------------------- | --------------------------------- |
| [ConnectionProperties](#connectionproperties) | Network connection information.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

let netHandle = connection.getDefaultNetSync();
let connectionproperties = connection.getConnectionPropertiesSync(netHandle);
```

## connection.getNetCapabilities

getNetCapabilities(netHandle: NetHandle, callback: AsyncCallback\<NetCapabilities>): void

Obtains capability information of the network corresponding to the **netHandle**. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name   | Type                                               | Mandatory| Description                                                        |
| --------- | --------------------------------------------------- | ---- | ------------------------------------------------------------ |
| netHandle | [NetHandle](#nethandle)                             | Yes  | Handle of the data network.                                            |
| callback  | AsyncCallback\<[NetCapabilities](#netcapabilities)> | Yes  | Callback used to return the result. If the capability information of the network corresponding to the **netHandle** is obtained successfully, **error** is **undefined** and **data** is the obtained network capability information. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  connection.getNetCapabilities(netHandle, (error: BusinessError, data: connection.NetCapabilities) => {
    if (error) {
      console.error(`Failed to get net capabilities. Code:${error.code}, message:${error.message}`);
      return;
    }
    console.info("Succeeded to get data: " + JSON.stringify(data));
  })
});
```

## connection.getNetCapabilities

getNetCapabilities(netHandle: NetHandle): Promise\<NetCapabilities>

Obtains capability information of the network corresponding to the **netHandle**. This API uses a promise to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name   | Type                   | Mandatory| Description            |
| --------- | ----------------------- | ---- | ---------------- |
| netHandle | [NetHandle](#nethandle) | Yes  | Handle of the data network.|

**Return value**

| Type                                         | Description                             |
| --------------------------------------------- | --------------------------------- |
| Promise\<[NetCapabilities](#netcapabilities)> | Promise used to return the result.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  connection.getNetCapabilities(netHandle).then((data: connection.NetCapabilities) => {
    console.info("Succeeded to get data: " + JSON.stringify(data));
  })
});
```

## connection.getNetCapabilitiesSync<sup>10+</sup>

getNetCapabilitiesSync(netHandle: NetHandle): NetCapabilities

Obtains capability information of the network corresponding to the **netHandle**. This API returns the result synchronously.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name   | Type                   | Mandatory| Description            |
| --------- | ----------------------- | ---- | ---------------- |
| netHandle | [NetHandle](#nethandle) | Yes  | Handle of the data network.|

**Return value**

| Type                                         | Description                             |
| --------------------------------------------- | --------------------------------- |
| [NetCapabilities](#netcapabilities) | Network capability information.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

let netHandle = connection.getDefaultNetSync();
let getNetCapabilitiesSync = connection.getNetCapabilitiesSync(netHandle);
```

## connection.isDefaultNetMetered<sup>9+</sup>

isDefaultNetMetered(callback: AsyncCallback\<boolean>): void

Checks whether the data traffic usage on the current network is metered. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                   | Mandatory| Description                                  |
| -------- | ----------------------- | ---- | -------------------------------------- |
| callback | AsyncCallback\<boolean> | Yes  | Callback used to return the result. The value **true** indicates the data traffic usage is metered.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.isDefaultNetMetered((error: BusinessError, data: boolean) => {
  console.log(JSON.stringify(error));
  console.log('data: ' + data);
});
```

## connection.isDefaultNetMetered<sup>9+</sup>

isDefaultNetMetered(): Promise\<boolean>

Checks whether the data traffic usage on the current network is metered. This API uses a promise to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type             | Description                                           |
| ----------------- | ----------------------------------------------- |
| Promise\<boolean> | Promise used to return the result. The value **true** indicates the data traffic usage is metered.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

connection.isDefaultNetMetered().then((data: boolean) => {
  console.log('data: ' + data);
});
```

## connection.isDefaultNetMeteredSync<sup>10+</sup>

isDefaultNetMeteredSync(): boolean

Checks whether the data traffic usage on the current network is metered. This API returns the result synchronously.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type             | Description                                           |
| ----------------- | ----------------------------------------------- |
| boolean | The value **true** indicates the data traffic usage is metered.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

let isMetered = connection.isDefaultNetMeteredSync();
```

## connection.hasDefaultNet

hasDefaultNet(callback: AsyncCallback\<boolean>): void

Checks whether the default data network is activated. This API uses an asynchronous callback to return the result. You can use [getDefaultNet](#connectiongetdefaultnet) to obtain the default data network, if any.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                   | Mandatory| Description                                  |
| -------- | ----------------------- | ---- | -------------------------------------- |
| callback | AsyncCallback\<boolean> | Yes  | Callback used to return the result. The value **true** indicates that the default data network is activated.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.hasDefaultNet((error: BusinessError, data: boolean) => {
  console.log(JSON.stringify(error));
  console.log('data: ' + data);
});
```

## connection.hasDefaultNet

hasDefaultNet(): Promise\<boolean>

Checks whether the default data network is activated. This API uses a promise to return the result. You can use [getDefaultNet](#connectiongetdefaultnet) to obtain the default data network, if any.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type             | Description                                           |
| ----------------- | ----------------------------------------------- |
| Promise\<boolean> | Promise used to return the result. The value **true** indicates that the default data network is activated.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
connection.hasDefaultNet().then((data: boolean) => {
  console.log('data: ' + data);
});
```

## connection.hasDefaultNetSync<sup>10+</sup>

hasDefaultNetSync(): boolean

Checks whether the default data network is activated. This API returns the result synchronously.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type             | Description                                           |
| ----------------- | ----------------------------------------------- |
| boolean | The value **true** indicates that the default data network is activated.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

let isDefaultNet = connection.hasDefaultNetSync();
```


## connection.reportNetConnected

reportNetConnected(netHandle: NetHandle, callback: AsyncCallback&lt;void&gt;): void

Reports connection of the data network to the network management module. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.GET_NETWORK_INFO and ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| netHandle | [NetHandle](#nethandle) | Yes| Handle of the data network. For details, see [NetHandle](#nethandle).|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the network status is reported successfully, **error** is **undefined**. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  connection.reportNetConnected(netHandle, (error: BusinessError) => {
    console.log(JSON.stringify(error));
  });
});
```

## connection.reportNetConnected

reportNetConnected(netHandle: NetHandle): Promise&lt;void&gt;

Reports connection of the data network to the network management module. This API uses a promise to return the result.

**Permission required**: ohos.permission.GET_NETWORK_INFO and ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| netHandle | [NetHandle](#nethandle) | Yes| Handle of the data network. For details, see [NetHandle](#nethandle).|

**Return value**
| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  connection.reportNetConnected(netHandle).then(() => {
    console.log(`report success`);
  });
});
```

## connection.reportNetDisconnected

reportNetDisconnected(netHandle: NetHandle, callback: AsyncCallback&lt;void&gt;): void

Reports disconnection of the data network to the network management module. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.GET_NETWORK_INFO and ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| netHandle | [NetHandle](#nethandle) | Yes| Handle of the data network. For details, see [NetHandle](#nethandle).|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the network status is reported successfully, **error** is **undefined**. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  connection.reportNetDisconnected(netHandle).then( () => {
    console.log(`report success`);
  });
});
```

## connection.reportNetDisconnected

reportNetDisconnected(netHandle: NetHandle): Promise&lt;void&gt;

Reports disconnection of the data network to the network management module. This API uses a promise to return the result.

**Permission required**: ohos.permission.GET_NETWORK_INFO and ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| netHandle | [NetHandle](#nethandle) | Yes| Handle of the data network. For details, see [NetHandle](#nethandle).|

**Return value**
| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  connection.reportNetDisconnected(netHandle).then( () => {
    console.log(`report success`);
  });
});
```

## connection.getAddressesByName

getAddressesByName(host: string, callback: AsyncCallback\<Array\<NetAddress>>): void

Resolves the host name by using the corresponding network to obtain all IP addresses. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                                             | Mandatory| Description                                                        |
| -------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| host     | string                                            | Yes  | Host name to resolve.                                          |
| callback | AsyncCallback\<Array\<[NetAddress](#netaddress)>> | Yes  | Callback used to return the result. If all IP addresses are successfully obtained, **error** is **undefined**, and **data** is the list of all obtained IP addresses. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";
connection.getAddressesByName("xxxx", (error: BusinessError, data: connection.NetAddress[]) => {
  if (error) {
    console.error(`Failed to get addresses. Code:${error.code}, message:${error.message}`);
    return;
  }
  console.info("Succeeded to get data: " + JSON.stringify(data));
});
```

## connection.getAddressesByName

getAddressesByName(host: string): Promise\<Array\<NetAddress>>

Resolves the host name by using the corresponding network to obtain all IP addresses. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| host   | string | Yes  | Host name to resolve.|

**Return value**

| Type                                       | Description                         |
| ------------------------------------------- | ----------------------------- |
| Promise\<Array\<[NetAddress](#netaddress)>> | Promise used to return the result.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
connection.getAddressesByName("xxxx").then((data: connection.NetAddress[]) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
});
```

## connection.addCustomDnsRule<sup>11+</sup>

addCustomDnsRule(host: string, ip: Array\<string\>, callback: AsyncCallback\<void\>): void

Adds the mapping between a custom host and the corresponding IP address for the current application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                | Mandatory| Description                                                        |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| host     | string               | Yes  | Name of the custom host.                                    |
| ip       | Array\<string>       | Yes  | List of IP addresses mapped to the host name.                                  |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result. If the mapping is added successfully, **error** is **undefined**. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';
connection.addCustomDnsRule("xxxx", ["xx.xx.xx.xx","xx.xx.xx.xx"], (error: BusinessError, data: void) => {
  if (error) {
    console.error(`Failed to get add custom dns rule. Code:${error.code}, message:${error.message}`);
    return;
  }
  console.info("Succeeded to get data: " + JSON.stringify(data));
})
```

## connection.addCustomDnsRule<sup>11+</sup>

addCustomDnsRule(host: string, ip: Array\<string\>): Promise\<void\>

Adds the mapping between a custom host and the corresponding IP address for the current application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type          | Mandatory| Description                      |
| ------ | -------------- | ---- | -------------------------- |
| host   | string         | Yes  | Name of the custom host.  |
| ip     | Array\<string> | Yes  | List of IP addresses mapped to the host name.|

**Return value**

| Type                  | Description                   |
| ---------------------- | ----------------------- |
| Promise\<Array\<void>> | Promise that returns no value.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';
connection.addCustomDnsRule("xxxx", ["xx.xx.xx.xx","xx.xx.xx.xx"]).then(() => {
    console.info("success");
}).catch((error: BusinessError) => {
    console.error(JSON.stringify(error));
})
```

## connection.removeCustomDnsRule<sup>11+</sup>

removeCustomDnsRule(host: string, callback: AsyncCallback\<void\>): void

Removes the custom DNS rules of the specified host from the current application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                | Mandatory| Description                                                        |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| host     | string               | Yes  | Name of the host for which DNS rules are to be deleted.                             |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result. If the DNS rules are removed successfully, **error** is **undefined**. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';
connection.removeCustomDnsRule("xxxx", (error: BusinessError, data: void) => {
  if (error) {
    console.error(`Failed to remove custom dns rule. Code:${error.code}, message:${error.message}`);
    return;
  }
  console.info("Succeeded to get data: " + JSON.stringify(data));
})
```

## connection.removeCustomDnsRule<sup>11+</sup>

removeCustomDnsRule(host: string): Promise\<void\>

Removes the custom DNS rules of the specified host from the current application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type  | Mandatory| Description                           |
| ------ | ------ | ---- | ------------------------------- |
| host   | string | Yes  | Name of the host for which DNS rules are to be deleted.|

**Return value**

| Type                  | Description                   |
| ---------------------- | ----------------------- |
| Promise\<Array\<void>> | Promise that returns no value.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';
connection.removeCustomDnsRule("xxxx").then(() => {
    console.log("success");
}).catch((error: BusinessError) => {
    console.log(JSON.stringify(error));
})
```

## connection.clearCustomDnsRules<sup>11+</sup>

clearCustomDnsRules(callback: AsyncCallback\<void\>): void

Removes all custom DNS rules from the current application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                | Mandatory| Description                                                        |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result. If all the DNS rules are removed successfully, **error** is **undefined**. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';
connection.clearCustomDnsRules((error: BusinessError, data: void) => {
  if (error) {
    console.error(`Failed to clear custom dns rules. Code:${error.code}, message:${error.message}`);
    return;
  }
  console.info("Succeeded to get data: " + JSON.stringify(data));
})
```

## connection.clearCustomDnsRules<sup>11+</sup>

clearCustomDnsRules(): Promise\<void\>

Removes all custom DNS rules from the current application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Return value**

| Type                  | Description                   |
| ---------------------- | ----------------------- |
| Promise\<void\>        | Promise that returns no value. |

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';
connection.clearCustomDnsRules().then(() => {
    console.log("success");
}).catch((error: BusinessError) => {
    console.log(JSON.stringify(error));
})
```


## NetConnection

Represents the network connection handle.

> **NOTE**
> When a device changes to the network connected state, the **netAvailable**, **netCapabilitiesChange**, and **netConnectionPropertiesChange** events will be triggered.
> When a device changes to the network disconnected state, the **netLost** event will be triggered.
> When a device switches from a Wi-Fi network to a cellular network, the **netLost** event will be first triggered to indicate that the Wi-Fi network is lost and then the **netAvaliable** event will be triggered to indicate that the cellular network is available.

### register

register(callback: AsyncCallback\<void>): void

Registers a listener for network status changes.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                | Mandatory| Description                                                        |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result. If a listener for network status changes is registered successfully, **error** is **undefined**. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |
| 2101008 | The same callback exists.     |
| 2101022 | The number of requests exceeded the maximum. |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";
let netCon: connection.NetConnection = connection.createNetConnection();
netCon.register((error: BusinessError) => {
  console.log(JSON.stringify(error));
});
```

### unregister

unregister(callback: AsyncCallback\<void>): void

Unregisters the listener for network status changes.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                | Mandatory| Description                                                        |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result. If a listener for network status changes is unregistered successfully, **error** is **undefined**. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201 | Permission denied.|
| 401 | Parameter error.         |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |
| 2101007 | The callback is not exists.      |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";
let netCon: connection.NetConnection = connection.createNetConnection();
netCon.unregister((error: BusinessError) => {
  console.log(JSON.stringify(error));
});
```

### on('netAvailable')

on(type: 'netAvailable', callback: Callback\<NetHandle>): void

Registers a listener for **netAvailable** events.

**Model restriction**: Before you call this API, make sure that you have called **register** to add a listener and called **unregister** API to unsubscribe from status changes of the default network.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                              | Mandatory| Description                                                        |
| -------- | ---------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                             | Yes  | Event type. This field has a fixed value of **netAvailable**.<br>**netAvailable**: event indicating that the data network is available.|
| callback | Callback\<[NetHandle](#nethandle)> | Yes  | Callback used to return the network handle.|

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";

// Create a NetConnection object.
let netCon: connection.NetConnection = connection.createNetConnection();

// Call register to register a listener.
netCon.register((error: BusinessError) => {
  console.log(JSON.stringify(error));
});

// Subscribe to netAvailable events. Event notifications can be received only after register is called.
netCon.on('netAvailable', (data: connection.NetHandle) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
});

// Call unregister to unregister the listener.
netCon.unregister((error: BusinessError) => {
  console.log(JSON.stringify(error));
});
```

### on('netBlockStatusChange')

on(type: 'netBlockStatusChange', callback: Callback\<NetBlockStatusInfo>): void

Registers a listener for **netBlockStatusChange** events. This API uses an asynchronous callback to return the result.

**Model restriction**: Before you call this API, make sure that you have called **register** to add a listener and called **unregister** API to unsubscribe from status changes of the default network.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                                        |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | Yes  | Event type. This field has a fixed value of **netBlockStatusChange**.<br>**netBlockStatusChange**: event indicating a change in the network blocking status.|
| callback | Callback<[NetBlockStatusInfo](#netblockstatusinfo11)> | Yes  | Callback used to return the result.  |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";

// Create a NetConnection object.
let netCon: connection.NetConnection = connection.createNetConnection();

// Call register to register a listener.
netCon.register((error: BusinessError) => {
  console.log(JSON.stringify(error));
});

// Subscribe to netBlockStatusChange events. Event notifications can be received only after register is called.
netCon.on('netBlockStatusChange', (data: connection.NetBlockStatusInfo) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
});

// Call unregister to unregister the listener.
netCon.unregister((error: BusinessError) => {
  console.log(JSON.stringify(error));
});
```

### on('netCapabilitiesChange')

on(type: 'netCapabilitiesChange', callback: Callback\<NetCapabilityInfo\>): void

Registers a listener for **netCapabilitiesChange** events.

**Model restriction**: Before you call this API, make sure that you have called **register** to add a listener and called **unregister** API to unsubscribe from status changes of the default network.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                                        |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | Yes  | Event type. This field has a fixed value of **netCapabilitiesChange**.<br>**netCapabilitiesChange**: event indicating that the network capabilities have changed.|
| callback | Callback<[NetCapabilityInfo](#netcapabilityinfo10)> | Yes  | Callback used to return the network handle (**netHandle**) and capability information (**netCap**).|

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";

// Create a NetConnection object.
let netCon: connection.NetConnection = connection.createNetConnection();

// Call register to register a listener.
netCon.register((error: BusinessError) => {
  console.log(JSON.stringify(error));
});

// Subscribe to netCapabilitiesChange events. Event notifications can be received only after register is called.
netCon.on('netCapabilitiesChange', (data: connection.NetCapabilityInfo) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
});

// Call unregister to unregister the listener.
netCon.unregister((error: BusinessError) => {
  console.log(JSON.stringify(error));
});
```

### on('netConnectionPropertiesChange')

on(type: 'netConnectionPropertiesChange', callback: Callback\<NetConnectionPropertyInfo\>): void

Registers a listener for **netConnectionPropertiesChange** events.

**Model restriction**: Before you call this API, make sure that you have called **register** to add a listener and called **unregister** API to unsubscribe from status changes of the default network.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                                        |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | Yes  | Event type. This field has a fixed value of **netConnectionPropertiesChange**.<br>**netConnectionPropertiesChange**: event indicating that network connection properties have changed.|
| callback | Callback<[NetConnectionPropertyInfo](#netconnectionpropertyinfo11)> | Yes  | Callback used to return the result.  |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";

// Create a NetConnection object.
let netCon: connection.NetConnection = connection.createNetConnection();

// Call register to register a listener.
netCon.register((error: BusinessError) => {
  console.log(JSON.stringify(error));
});

// Subscribe to netConnectionPropertiesChange events. Event notifications can be received only after register is called.
netCon.on('netConnectionPropertiesChange', (data: connection.NetConnectionPropertyInfo) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
});

// Call unregister to unregister the listener.
netCon.unregister((error: BusinessError) => {
  console.log(JSON.stringify(error));
});
```

### on('netLost')

on(type: 'netLost', callback: Callback\<NetHandle>): void

Registers a listener for **netLost** events.

**Model restriction**: Before you call this API, make sure that you have called **register** to add a listener and called **unregister** API to unsubscribe from status changes of the default network.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                              | Mandatory| Description                                                        |
| -------- | ---------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                             | Yes  | Event type. This field has a fixed value of **netLost**.<br>netLost: event indicating that the network is interrupted or normally disconnected.|
| callback | Callback\<[NetHandle](#nethandle)> | Yes  | Callback used to return **netHandle**.|

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";

// Create a NetConnection object.
let netCon: connection.NetConnection = connection.createNetConnection();

// Call register to register a listener.
netCon.register((error: BusinessError) => {
  console.log(JSON.stringify(error));
});

// Subscribe to netLost events. Event notifications can be received only after register is called.
netCon.on('netLost', (data: connection.NetHandle) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
});

// Call unregister to unregister the listener.
netCon.unregister((error: BusinessError) => {
  console.log(JSON.stringify(error));
});
```

### on('netUnavailable')

on(type: 'netUnavailable', callback: Callback\<void>): void

Registers a listener for **netUnavailable** events.

**Model restriction**: Before you call this API, make sure that you have called **register** to add a listener and called **unregister** API to unsubscribe from status changes of the default network.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type           | Mandatory| Description                                                        |
| -------- | --------------- | ---- | ------------------------------------------------------------ |
| type     | string          | Yes  | Event type. This field has a fixed value of **netUnavailable**.<br>**netUnavailable**: event indicating that the network is unavailable.|
| callback | Callback\<void> | Yes  | Callback used to return the result, which is empty.|

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";

// Create a NetConnection object.
let netCon: connection.NetConnection = connection.createNetConnection();

// Call register to register a listener.
netCon.register((error: BusinessError) => {
  console.log(JSON.stringify(error));
});

// Subscribe to netUnavailable events. Event notifications can be received only after register is called.
netCon.on('netUnavailable', () => {
  console.info("Succeeded to get unavailable net event");
});

// Call unregister to unregister the listener.
netCon.unregister((error: BusinessError) => {
  console.log(JSON.stringify(error));
});
```

## NetHandle

Defines the handle of the data network.

Before invoking **NetHandle** APIs, call **getNetHandle** to obtain a **NetHandle** object.

**System capability**: SystemCapability.Communication.NetManager.Core

### Attributes

| Name   | Type  | Mandatory| Description                     |
| ------ | ------ | --- |------------------------- |
| netId  | number | Yes |  Network ID. The value **0** indicates no default network. Any other value must be greater than or equal to 100.|

### bindSocket<sup>9+</sup>

bindSocket(socketParam: TCPSocket \| UDPSocket, callback: AsyncCallback\<void>): void

Binds a **TCPSocket** or **UDPSocket** object to the data network. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name     | Type                    | Mandatory| Description                           |
| ----------- | ------------------------ | ---- | -------------------------------|
| socketParam | [TCPSocket](js-apis-socket.md#tcpsocket) \| [UDPSocket](js-apis-socket.md#udpsocket) | Yes| **TCPSocket** or **UDPSocket** object.|
| callback    | AsyncCallback\<void>      | Yes  | Callback used to return the result. If the **TCPSocket** or **UDPSocket** object is successfully bound to the current network, **error** is **undefined**. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import socket from "@ohos.net.socket";
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

interface Data {
  message: ArrayBuffer,
  remoteInfo: socket.SocketRemoteInfo
}

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  let tcp = socket.constructTCPSocketInstance();
  let udp = socket.constructUDPSocketInstance();
  let socketType = "TCPSocket";
  if (socketType == "TCPSocket") {
    tcp.bind({address:"192.168.xxx.xxx",
              port:8080,
              family:1} as socket.NetAddress, (error: Error) => {
      if (error) {
        console.log('bind fail');
        return;
      }
      netHandle.bindSocket(tcp, (error: BusinessError, data: void) => {
        if (error) {
          console.error(`Failed to bind socket. Code:${error.code}, message:${error.message}`);
        } else {
          console.info(JSON.stringify(data));
        }
      });
    });
  } else {
    let callback: (value: Data) => void = (value: Data) => {
      console.log("on message, message:" + value.message + ", remoteInfo:" + value.remoteInfo);
    };
    udp.bind({address:"192.168.xxx.xxx",
              port:8080,
              family:1} as socket.NetAddress, (error: BusinessError) => {
      if (error) {
        console.error(`Failed to bind. Code:${error.code}, message:${error.message}`);
        return;
      }
      udp.on('message', (data: Data) => {
        console.info("Succeeded to get data: " + JSON.stringify(data));
      });
      netHandle.bindSocket(udp, (error: BusinessError, data: void) => {
        if (error) {
          console.error(`Failed to bind socket. Code:${error.code}, message:${error.message}`);
        } else {
          console.info(JSON.stringify(data));
        }
      });
    });
  }
});
```

### bindSocket<sup>9+</sup>

bindSocket(socketParam: TCPSocket \| UDPSocket): Promise\<void>;

Binds a **TCPSocket** or **UDPSocket** object to the data network. This API uses a promise to return the result.

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name         | Type                 | Mandatory | Description                          |
| --------------- | --------------------- | ---- | ------------------------------ |
| socketParam     | [TCPSocket](js-apis-socket.md#tcpsocket) \| [UDPSocket](js-apis-socket.md#udpsocket) | Yes  | **TCPSocket** or **UDPSocket** object.|

**Return value**

| Type          | Description                  |
| -------------- | ---------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import socket from "@ohos.net.socket";
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';
interface Data {
  message: ArrayBuffer,
  remoteInfo: socket.SocketRemoteInfo
}

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  let tcp = socket.constructTCPSocketInstance();
  let udp = socket.constructUDPSocketInstance();
  let socketType = "TCPSocket";
  if (socketType == "TCPSocket") {
    tcp.bind({address:"192.168.xxx.xxx",
              port:8080,
              family:1} as socket.NetAddress, (error: Error) => {
      if (error) {
        console.log('bind fail');
        return;
      }
      netHandle.bindSocket(tcp).then(() => {
        console.info("bind socket success");
      }).catch((error: BusinessError) => {
        console.error(`Failed to bind socket. Code:${error.code}, message:${error.message}`);
      });
    });
  } else {
    let callback: (value: Data) => void = (value: Data) => {
      console.log("on message, message:" + value.message + ", remoteInfo:" + value.remoteInfo);
    }
    udp.bind({address:"192.168.xxx.xxx",
              port:8080,
              family:1} as socket.NetAddress, (error: BusinessError) => {
    if (error) {
      console.error(`Failed to bind. Code:${error.code}, message:${error.message}`);
      return;
    }
    udp.on('message', (data: Data) => {
      console.info("Succeeded to get data: " + JSON.stringify(data));
    });
    netHandle.bindSocket(udp).then(() => {
      console.info("bind socket success");
    }).catch((error: BusinessError) => {
      console.error(`Failed to bind socket. Code:${error.code}, message:${error.message}`);
    });
  });
}
});
```

### getAddressesByName

getAddressesByName(host: string, callback: AsyncCallback\<Array\<NetAddress>>): void

Resolves the host name by using the corresponding network to obtain all IP addresses. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                                             | Mandatory| Description                                                        |
| -------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| host     | string                                            | Yes  | Host name to resolve.                                          |
| callback | AsyncCallback\<Array\<[NetAddress](#netaddress)>> | Yes  | Callback used to return the result. If all IP addresses are successfully obtained, **error** is **undefined**, and **data** is the list of all obtained IP addresses. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  let host = "xxxx";
  netHandle.getAddressesByName(host, (error: BusinessError, data: connection.NetAddress[]) => {
    if (error) {
      console.error(`Failed to get addresses. Code:${error.code}, message:${error.message}`);
      return;
    }
    console.info("Succeeded to get data: " + JSON.stringify(data));
  });
});
```

### getAddressesByName

getAddressesByName(host: string): Promise\<Array\<NetAddress>>

Resolves the host name by using the corresponding network to obtain all IP addresses. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| host   | string | Yes  | Host name to resolve.|

**Return value**

| Type                                       | Description                         |
| ------------------------------------------- | ----------------------------- |
| Promise\<Array\<[NetAddress](#netaddress)>> | Promise used to return the result.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  let host = "xxxx";
  netHandle.getAddressesByName(host).then((data: connection.NetAddress[]) => {
    console.info("Succeeded to get data: " + JSON.stringify(data));
  });
});
```

### getAddressByName

getAddressByName(host: string, callback: AsyncCallback\<NetAddress>): void

Resolves the host name by using the corresponding network to obtain the first IP address. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name  | Type                                     | Mandatory| Description                                                        |
| -------- | ----------------------------------------- | ---- | ------------------------------------------------------------ |
| host     | string                                    | Yes  | Host name to resolve.                                          |
| callback | AsyncCallback\<[NetAddress](#netaddress)> | Yes  | Callback used to return the result. If the first IP address is obtained successfully, **error** is **undefined**, and **data** is the first obtained IP address. Otherwise, **error** is an error object.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from "@ohos.base";

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  let host = "xxxx";
  netHandle.getAddressByName(host, (error: BusinessError, data: connection.NetAddress) => {
    if (error) {
      console.error(`Failed to get address. Code:${error.code}, message:${error.message}`);
      return;
    }
    console.info("Succeeded to get data: " + JSON.stringify(data));
  });
});
```

### getAddressByName

getAddressByName(host: string): Promise\<NetAddress>

Resolves the host name by using the corresponding network to obtain the first IP address. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Communication.NetManager.Core

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| host   | string | Yes  | Host name to resolve.|

**Return value**

| Type                               | Description                           |
| ----------------------------------- | ------------------------------- |
| Promise\<[NetAddress](#netaddress)> | Promise used to return the result.|

**Error codes**

| ID| Error Message                       |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 401     | Parameter error.               |
| 2100001 | Invalid parameter value.                |
| 2100002 | Operation failed. Cannot connect to service.|
| 2100003 | System internal error.         |

**Example**

```ts
import connection from '@ohos.net.connection';

connection.getDefaultNet().then((netHandle: connection.NetHandle) => {
  let host = "xxxx";
  netHandle.getAddressByName(host).then((data: connection.NetAddress) => {
    console.info("Succeeded to get data: " + JSON.stringify(data));
  });
});
```

## NetCap

Defines the network capability.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name                 | Value  | Description                  |
| ------------------------ | ---- | ---------------------- |
| NET_CAPABILITY_MMS | 0 | The network can connect to the carrier's Multimedia Messaging Service Center (MMSC) to send and receive multimedia messages.|
| NET_CAPABILITY_NOT_METERED | 11 | The network traffic is not metered.|
| NET_CAPABILITY_INTERNET  | 12   | The network has the Internet access capability, which is set by the network provider.|
| NET_CAPABILITY_NOT_VPN | 15 | The network does not use a virtual private network (VPN).|
| NET_CAPABILITY_VALIDATED | 16   | The Internet access capability of the network is successfully verified by the connection management module.|

## NetBearType

Enumerates network types.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name        | Value  | Description       |
| --------------- | ---- | ----------- |
| BEARER_CELLULAR | 0    | Cellular network. |
| BEARER_WIFI     | 1    | Wi-Fi network.|
| BEARER_ETHERNET | 3 | Ethernet network.|

## HttpProxy<sup>10+</sup>

Represents the HTTP proxy configuration.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name   | Type  | Mandatory| Description                     |
| ------ | ------ | --- |------------------------- |
| host  | string | Yes |  Host name of the proxy server.|
| port  | number | Yes |  Host port.|
| exclusionList  | Array<string> | Yes | List of the names of hosts that do not use a proxy. Host names can be domain names, IP addresses, or wildcards. The detailed matching rules are as follows:<br>- Domain name matching:<br>  - Exact match: The host name of the proxy server exactly matches any host name in the list.<br>  - Partial match: The host name of the proxy server contains any host name in the list.<br>For example, if **ample.com** is set in the host name list, **ample.com**, **www.ample.com**, and **ample.com:80** are matched, and **www.example.com** and **ample.com.org** are not matched.<br>- IP address matching: The host name of the proxy server exactly matches any IP address in the list.<br>- Both the domain name and IP address are added to the list for matching.<br>- A single asterisk (*) is the only valid wildcard. If the list contains only wildcards, the wildcards match all host names; that is, the HTTP proxy is disabled. A wildcard can only be added independently. It cannot be added to the list together with other domain names or IP addresses. Otherwise, the wildcard does not take effect.<br>- Host names are case insensitive.<br>- Protocol prefixes such as **http** and **https** are ignored during matching.|


## NetSpecifier

Provides an instance that bears data network capabilities.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name                    | Type                               | Mandatory | Description                                                        |
| ----------------------- | ----------------------------------- | ---- | ------------------------------------------------------------ |
| netCapabilities         | [NetCapabilities](#netcapabilities) |  Yes | Network transmission capabilities and bearer types of the data network.                               |
| bearerPrivateIdentifier | string                              |  No |  Network identifier. The identifier of a Wi-Fi network is **wifi**, and that of a cellular network is **slot0** (corresponding to SIM card 1).|

## NetCapabilityInfo<sup>10+</sup>

Provides an instance that bears data network capabilities.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name                    | Type                               | Mandatory | Description                                                        |
| ----------------------- | ----------------------------------- | ---- | ------------------------------------------------------------ |
| netHandle         | [NetHandle](#nethandle) |  Yes | Handle of the data network.                               |
| netCap |  [NetCapabilities](#netcapabilities)       |  No |  Network transmission capabilities and bearer types of the data network.|

## NetCapabilities

Defines the network capability set.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name                 | Type                               | Mandatory| Description                    |
| --------------------- | ---------------------------------- | --- | ------------------------ |
| linkUpBandwidthKbps   | number                             |  No|  Uplink (device-to-network) bandwidth, in kbit/s. The value **0** indicates that the network bandwidth cannot be evaluated.|
| linkDownBandwidthKbps | number                             |  No|  Downlink (network-to-device) bandwidth, in kbit/s. The value **0** indicates that the network bandwidth cannot be evaluated.|
| networkCap            | Array\<[NetCap](#netcap)>           |  No|  Network capability.          |
| bearerTypes           | Array\<[NetBearType](#netbeartype)> |  Yes|  Network type. The array contains only one specific network type.     |

## NetConnectionPropertyInfo<sup>11+</sup>

Defines the network connection properties.

**System capability**: SystemCapability.Communication.NetManager.Core

### Attributes

| Name                | Type                                  | Mandatory|  Description           |
| -------------------- | ------------------------------------- | ---- |---------------- |
| netHandle            | [NetHandle](#nethandle)                             | Yes  |Data network handle.      |
| connectionProperties | [ConnectionProperties](#connectionproperties)                  | Yes  |Network connection properties.|

## NetBlockStatusInfo<sup>11+</sup>

Obtains the network block status information.

**System capability**: SystemCapability.Communication.NetManager.Core

### Attributes

| Name                | Type                                  | Mandatory|  Description           |
| -------------------- | ------------------------------------- | ---- |---------------- |
| netHandle            | [NetHandle](#nethandle)                             | Yes  |Data network handle.  |
| blocked | boolean                  | Yes  |Whether the current network is blocked.|

## ConnectionProperties

Defines the network connection properties.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name          | Type                              | Mandatory|  Description            |
| ------------- | ---------------------------------- | ----|---------------- |
| interfaceName | string                             | Yes|Network interface card (NIC) name.      |
| domains       | string                             | Yes|Domain. The default value is **""**.|
| linkAddresses | Array\<[LinkAddress](#linkaddress)> | Yes|Link information.      |
| routes        | Array\<[RouteInfo](#routeinfo)>     | Yes|Route information.      |
| dnses     | Array\<[NetAddress](#netaddress)> | Yes|Network address. For details, see [NetAddress](#netaddress).|
| mtu           | number                             | Yes|Maximum transmission unit (MTU).  |

## RouteInfo

Defines network route information.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name          | Type                       | Mandatory|Description            |
| -------------- | --------------------------- | --- |---------------- |
| interface      | string                      | Yes|NIC name.      |
| destination    | [LinkAddress](#linkaddress) | Yes|Destination address.      |
| gateway        | [NetAddress](#netaddress)   | Yes|Gateway address.      |
| hasGateway     | boolean                     | Yes|Whether a gateway is present.    |
| isDefaultRoute | boolean                     | Yes|Whether the route is the default route.|

## LinkAddress

Defines network link information.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name       | Type                     | Mandatory|Description                |
| ------------ | ----------------------- |---- |-------------------- |
| address      | [NetAddress](#netaddress) | Yes| Link address.          |
| prefixLength | number                    | Yes|Length of the link address prefix.|

## NetAddress

Defines a network address.

**System capability**: SystemCapability.Communication.NetManager.Core

| Name| Type| Mandatory| Description|
| ------- | ------ | -- |------------------------------ |
| address | string | Yes|Network address.|
| family  | number | No|Address family identifier. The value is **1** for IPv4 and **2** for IPv6. The default value is **1**.|
| port    | number | No|Port number. The value ranges from **0** to **65535**.|
