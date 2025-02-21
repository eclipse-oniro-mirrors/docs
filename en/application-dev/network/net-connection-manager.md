# Network Connection Management

## Introduction

The Network Connection Management module provides basic network management capabilities, including management of Wi-Fi/cellular/Ethernet connection priorities, network quality evaluation, subscription to network connection status changes, query of network connection information, and DNS resolution.

> **NOTE**
> To maximize the application running efficiency, most API calls are called asynchronously in callback or promise mode. The following code examples use the promise mode. For details about the APIs, see [API Reference](../reference/apis-network-kit/js-apis-net-connection.md).

## Basic Concepts

- Producer: a provider of data networks, such as Wi-Fi, cellular, and Ethernet.
- Consumer: a user of data networks, for example, an application or a system service.
- Network probe: a mechanism used to detect the network availability to prevent the switch from an available network to an unavailable network. The probe type can be binding network detection, DNS detection, HTTP detection, or HTTPS detection.
- Network selection: a mechanism used to select the optimal network when multiple networks coexist. It is triggered when the network status, network information, or network quality evaluation score changes.

## **Constraints**

- Programming language: JS
- The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## When to Use

Typical application scenarios of network connection management are as follows:

- Subscribing to status changes of the specified network
- Obtaining the list of all registered networks
- Querying network connection information based on the data network
- Resolving the domain name of a network to obtain all IP addresses

The following describes the development procedure specific to each application scenario.

## Available APIs

For the complete list of APIs and example code, see [Network Connection Management](../reference/apis-network-kit/js-apis-net-connection.md).

| API | Description |
| ---- | ---- |
| getDefaultNet(callback: AsyncCallback\<NetHandle>): void; |Creates a **NetHandle** object that contains the **netId** of the default network. This API uses an asynchronous callback to return the result. |
| getGlobalHttpProxy(callback: AsyncCallback\<HttpProxy>): void;| Obtains the global HTTP proxy for the network. This API uses an asynchronous callback to return the result. |
| setGlobalHttpProxy(httpProxy: HttpProxy, callback: AsyncCallback\<void>): void;| Sets the global HTTP proxy for the network. This API uses an asynchronous callback to return the result. |
| setAppHttpProxy(httpProxy: HttpProxy): void;| Sets the application-level HTTP proxy configuration of the network. |
| getAppNet(callback: AsyncCallback\<NetHandle>): void;| Obtains a **NetHandle** object that contains the **netId** of the network bound to the application. This API uses an asynchronous callback to return the result. |
| setAppNet(netHandle: NetHandle, callback: AsyncCallback\<void>): void;| Binds an application to the specified network. The application can access the external network only through this network. This API uses an asynchronous callback to return the result. |
| getDefaultNetSync(): NetHandle; |Obtains the default active data network in synchronous mode. You can use **getNetCapabilities** to obtain information such as the network type and capabilities.|
| hasDefaultNet(callback: AsyncCallback\<boolean>): void; |Checks whether the default data network is activated. This API uses an asynchronous callback to return the result. |
| getAllNets(callback: AsyncCallback\<Array\<NetHandle>>): void;| Obtains the list of **NetHandle** objects of the connected network. This API uses an asynchronous callback to return the result. |
| getConnectionProperties(netHandle: NetHandle, callback: AsyncCallback\<ConnectionProperties>): void; |Obtains network connection information of the network corresponding to the **netHandle**. This API uses an asynchronous callback to return the result. |
| getNetCapabilities(netHandle: NetHandle, callback: AsyncCallback\<NetCapabilities>): void; |Obtains capability information of the network corresponding to the **netHandle**. This API uses an asynchronous callback to return the result. |
| isDefaultNetMetered(callback: AsyncCallback\<boolean>): void; |Checks whether the data traffic usage on the current network is metered. This API uses an asynchronous callback to return the result. |
| reportNetConnected(netHandle: NetHandle, callback: AsyncCallback\<void>): void;| Reports a **netAavailable** event to NetManager. If this API is called, the application considers that its network status (ohos.net.connection.NetCap.NET_CAPABILITY_VAILDATED) is inconsistent with that of NetManager. This API uses an asynchronous callback to return the result. |
| reportNetDisconnected(netHandle: NetHandle, callback: AsyncCallback\<void>): void;| Reports a **netAavailable** event to NetManager. If this API is called, the application considers that its network status (ohos.net.connection.NetCap.NET_CAPABILITY_VAILDATED) is inconsistent with that of NetManager. This API uses an asynchronous callback to return the result. |
| getAddressesByName(host: string, callback: AsyncCallback\<Array\<NetAddress>>): void; |Obtains all IP addresses of the specified network by resolving the domain name. This API uses an asynchronous callback to return the result. |
| enableAirplaneMode(callback: AsyncCallback\<void>): void; | Enables the airplane mode. This API uses an asynchronous callback to return the result. |
| disableAirplaneMode(callback: AsyncCallback\<void>): void;| Disables the airplane mode. This API uses an asynchronous callback to return the result. |
| createNetConnection(netSpecifier?: NetSpecifier, timeout?: number): NetConnection; | Creates a **NetConnection** object. **netSpecifier** specifies the network, and **timeout** specifies the timeout interval in ms. **timeout** is configurable only when **netSpecifier** is specified. If neither of them is present, the default network is used. |
| bindSocket(socketParam: TCPSocket \| UDPSocket, callback: AsyncCallback\<void>): void; | Binds a **TCPSocket** or **UDPSocket** to the current network. This API uses an asynchronous callback to return the result. |
| getAddressesByName(host: string, callback: AsyncCallback\<Array\<NetAddress>>): void; |Obtains all IP addresses of the specified network by resolving the domain name. This API uses an asynchronous callback to return the result. |
| getAddressByName(host: string, callback: AsyncCallback\<NetAddress>): void; |Obtains an IP address of the specified network by resolving the domain name. This API uses an asynchronous callback to return the result. |
| on(type: 'netAvailable', callback: Callback\<NetHandle>): void;                   |Subscribes to **netAvailable** events. |
| on(type: 'netCapabilitiesChange', callback: Callback\<NetCapabilityInfo\>): void; |Subscribes to **netCapabilitiesChange** events. |
| on(type: 'netConnectionPropertiesChange', callback: Callback\<{ netHandle: NetHandle, connectionProperties: ConnectionProperties }>): void; |Subscribes to **netConnectionPropertiesChange** events. |
| on(type: 'netBlockStatusChange', callback: Callback<{ netHandle: NetHandle, blocked: boolean }>): void; |Subscribes to **netBlockStatusChange** events. |
| on(type: 'netLost', callback: Callback\<NetHandle>): void; |Subscribes to **netLost** events. |
| on(type: 'netUnavailable', callback: Callback\<void>): void; |Subscribes to **netUnavailable** events. |
| register(callback: AsyncCallback\<void>): void; |Subscribes to network status changes. |
| unregister(callback: AsyncCallback\<void>): void; |Unsubscribes from network status changes. |

## Subscribing to Status Changes of the Specified Network

1. Declare the required permission: **ohos.permission.GET_NETWORK_INFO**.
This permission is of the **normal** level. Before applying for the permission, ensure that the [basic principles for permission management](../security/AccessToken/app-permission-mgmt-overview.md#basic-principles-for-using-permissions) are met. Declare the permissions required by your application. For details, see [Declaring Permissions in the Configuration File](accesstoken-guidelines.md#declaring-permissions-in-the configuration-file).

1. Import the connection namespace from **@ohos.net.connection.d.ts**.

2. Call **createNetConnection()** to create a **NetConnection** object. You can specify the network type, capability, and timeout interval. If you do not specify parameters, the default values will be used. 

3. Call **conn.on()** to subscribe to the target event. You must pass in **type** and **callback**.

4. Call **conn.register()** to subscribe to network status changes of the specified network.

5. When the network is available, the callback will be invoked to return the **netAvailable** event. When the network is unavailable, the callback will be invoked to return the **netUnavailable** event.

6. Call **conn.unregister()** to unsubscribe from the network status changes if required.

```ts
// Import the connection namespace.
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

let netSpecifier: connection.NetSpecifier = {
  netCapabilities: {
    // Assume that the default network is Wi-Fi. If you need to create a cellular network connection, set the network type to CELLULAR.
    bearerTypes: [connection.NetBearType.BEARER_CELLULAR],
    // Set the network capability to INTERNET.
    networkCap: [connection.NetCap.NET_CAPABILITY_INTERNET]
  },
};

// Set the timeout value to 10s. The default value is 0.
let timeout = 10 * 1000;

// Create a NetConnection object.
let conn = connection.createNetConnection(netSpecifier, timeout);

// Register an observer for network status changes.
conn.register((err: BusinessError, data: void) => {
  console.log(JSON.stringify(err));
});

// Listen to network status change events. If the network is available, an on_netAvailable event is returned.
conn.on('netAvailable', ((data: connection.NetHandle) => {
  console.log("net is available, netId is " + data.netId);
}));

// Listen to network status change events. If the network is unavailable, an on_netUnavailable event is returned.
conn.on('netUnavailable', ((data: void) => {
  console.log("net is unavailable, data is " + JSON.stringify(data));
}));

// Unregister the observer for network status changes.
conn.unregister((err: BusinessError, data: void) => {
});
```

## Obtaining the List of All Registered Networks

### How to Develop

1. Declare the required permission: **ohos.permission.GET_NETWORK_INFO**.
This permission is of the **normal** level. Before applying for the permission, ensure that the [basic principles for permission management](../security/AccessToken/app-permission-mgmt-overview.md#basic-principles-for-using-permissions) are met. Declare the permissions required by your application. For details, see [Declaring Permissions in the Configuration File](accesstoken-guidelines.md#declaring-permissions-in-the configuration-file).

2. Import the connection namespace from **@ohos.net.connection.d.ts**.

3. Call **getAllNets** to obtain the list of all connected networks.

```ts
// Import the connection namespace.
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

// Construct a singleton object.
export class GlobalContext {
  public netList: connection.NetHandle[] = [];
  private constructor() {}
  private static instance: GlobalContext;
  private _objects = new Map<string, Object>();

  public static getContext(): GlobalContext {
    if (!GlobalContext.instance) {
      GlobalContext.instance = new GlobalContext();
    }
    return GlobalContext.instance;
  }

  getObject(value: string): Object | undefined {
    return this._objects.get(value);
  }

  setObject(key: string, objectClass: Object): void {
    this._objects.set(key, objectClass);
  }
}

// Obtain the list of all connected networks.
connection.getAllNets().then((data: connection.NetHandle[]) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
  if (data) {
    GlobalContext.getContext().netList = data;
  }
});
```

## Querying Network Capability Information and Connection Information of Specified Data Network

### How to Develop

1. Declare the required permission: **ohos.permission.GET_NETWORK_INFO**.
This permission is of the **normal** level. Before applying for the permission, ensure that the [basic principles for permission management](../security/AccessToken/app-permission-mgmt-overview.md#basic-principles-for-using-permissions) are met. Declare the permissions required by your application. For details, see [Declaring Permissions in the Configuration File](accesstoken-guidelines.md#declaring-permissions-in-the configuration-file).

2. Import the connection namespace from **@ohos.net.connection.d.ts**.

3. Call **getDefaultNet** to obtain the default data network via **NetHandle** or call **getAllNets** to obtain the list of all connected networks via **Array\<NetHandle>**.

4. Call **getNetCapabilities** to obtain the network capability information of the data network specified by **NetHandle**. The capability information includes information such as the network type (cellular, Wi-Fi, or Ethernet network) and the specific network capabilities.

5. Call **getConnectionProperties** to obtain the connection information of the data network specified by **NetHandle**.

```ts
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

// Construct a singleton object.
export class GlobalContext {
  public netList: connection.NetHandle[] = [];
  public netHandle: connection.NetHandle|null = null;
  private constructor() {}
  private static instance: GlobalContext;
  private _objects = new Map<string, Object>();

  public static getContext(): GlobalContext {
    if (!GlobalContext.instance) {
      GlobalContext.instance = new GlobalContext();
    }
    return GlobalContext.instance;
  }

  getObject(value: string): Object | undefined {
    return this._objects.get(value);
  }

  setObject(key: string, objectClass: Object): void {
    this._objects.set(key, objectClass);
  }
}

// Call getDefaultNet to obtain the default data network specified by **NetHandle**.
connection.getDefaultNet().then((data:connection.NetHandle) => {
  if (data) {
    console.info("getDefaultNet get data: " + JSON.stringify(data));
    GlobalContext.getContext().netHandle = data;
    // Obtain the network capability information of the data network specified by **NetHandle**. The capability information includes information such as the network type and specific network capabilities.
    connection.getNetCapabilities(GlobalContext.getContext().netHandle).then((data: connection.NetCapabilities) => {
      console.info("getNetCapabilities get data: " + JSON.stringify(data));

      // Obtain the network type via bearerTypes.
      let bearerTypes: Set<number> = new Set(data.bearerTypes);
      let bearerTypesNum = Array.from(bearerTypes.values());
      for (let item of bearerTypesNum) {
        if (item == 0) {
          // Cellular network
          console.log(JSON.stringify("BEARER_CELLULAR"));
        } else if (item == 1) {
          // Wi-Fi network
          console.log(JSON.stringify("BEARER_WIFI"));
        } else if (item == 3) {
          // Ethernet network
          console.log(JSON.stringify("BEARER_ETHERNET"));
        }
      }
      
      // Obtain the specific network capabilities via networkCap.
      let itemNumber : Set<number> = new Set(data.networkCap);
      let dataNumber = Array.from(itemNumber.values());
      for (let item of dataNumber) {
        if (item == 0) {
          // The network can connect to the carrier's Multimedia Messaging Service Center (MMSC) to send and receive multimedia messages.
          console.log(JSON.stringify("NET_CAPABILITY_MMS"));
        } else if (item == 11) {
          // The network traffic is not metered.
          console.log(JSON.stringify("NET_CAPABILITY_NOT_METERED"));
        } else if (item == 12) {
          // The network has the Internet access capability, which is set by the network provider.
          console.log(JSON.stringify("NET_CAPABILITY_INTERNET"));
        } else if (item == 15) {
          // The network does not use a Virtual Private Network (VPN).
          console.log(JSON.stringify("NET_CAPABILITY_NOT_VPN"));
        } else if (item == 16) {
          // The Internet access capability of the network is successfully verified by the connection management module.
          console.log(JSON.stringify("NET_CAPABILITY_VALIDATED"));
        }
      }
    })
  }
})

// Obtain the connection information of the data network specified by NetHandle. Connection information includes link and route information.
connection.getConnectionProperties(GlobalContext.getContext().netHandle).then((data: connection.ConnectionProperties) => {
  console.info("getConnectionProperties get data: " + JSON.stringify(data));
})

// Call getAllNets to obtain the list of all connected networks via Array<NetHandle>.
connection.getAllNets().then((data: connection.NetHandle[]) => {
  console.info("getAllNets get data: " + JSON.stringify(data));
  if (data) {
    GlobalContext.getContext().netList = data;

    let itemNumber : Set<connection.NetHandle> = new Set(GlobalContext.getContext().netList);
    let dataNumber = Array.from(itemNumber.values());
    for (let item of dataNumber) {
      // Obtain the network capability information of the network specified by each netHandle on the network list cyclically.
      connection.getNetCapabilities(item).then((data: connection.NetCapabilities) => {
        console.info("getNetCapabilities get data: " + JSON.stringify(data));
      })

      // Obtain the connection information of the network specified by each netHandle on the network list cyclically.
      connection.getConnectionProperties(item).then((data: connection.ConnectionProperties) => {
        console.info("getConnectionProperties get data: " + JSON.stringify(data));
      })
    }
  }
})
```

## Resolving the domain name of a network to obtain all IP addresses

### How to Develop

1. Declare the required permission: **ohos.permission.INTERNET**.
This permission is of the **normal** level. Before applying for the permission, ensure that the [basic principles for permission management](../security/AccessToken/app-permission-mgmt-overview.md#basic-principles-for-using-permissions) are met. Declare the permissions required by your application. For details, see [Declaring Permissions in the Configuration File](accesstoken-guidelines.md#declaring-permissions-in-the configuration-file).

2. Import the connection namespace from **@ohos.net.connection.d.ts**.

3. Call **getAddressesByName** to use the default network to resolve the host name to obtain the list of all IP addresses.

```ts
// Import the connection namespace.
import connection from '@ohos.net.connection';
import { BusinessError } from '@ohos.base';

// Use the default network to resolve the host name to obtain the list of all IP addresses.
connection.getAddressesByName("xxxx").then((data: connection.NetAddress[]) => {
  console.info("Succeeded to get data: " + JSON.stringify(data));
});
```
