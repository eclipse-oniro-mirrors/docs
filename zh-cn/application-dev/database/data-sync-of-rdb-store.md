# 关系型数据库跨设备数据同步


## 场景介绍

当应用程序本地存储的关系型数据存在跨设备同步的需求时，可以将需求同步的表数据迁移到新的支持跨设备的表中，当然也可以在刚完成表创建时设置其支持跨设备。


## 基本概念

关系型数据库跨设备数据同步，支持应用在多设备间同步存储的关系型数据。

- 分布式列表，应用在数据库中新创建表后，可以设置其为分布式表。在查询远程设备数据库时，根据本地表名可以获取指定远程设备的分布式表名。

- 设备之间同步数据，数据同步有两种方式，将数据从本地设备推送到远程设备或将数据从远程设备拉至本地设备。


## 运作机制

底层通信组件完成设备发现和认证，会通知上层应用程序设备上线。收到设备上线的消息后数据管理服务可以在两个设备之间建立加密的数据传输通道，利用该通道在两个设备之间进行数据同步。


### 数据跨设备同步机制

![relationalStore_sync](figures/relationalStore_sync.jpg)

业务将数据写入关系型数据库后，向数据管理服务发起同步请求。

数据管理服务从应用沙箱内读取待同步数据，根据对端设备的deviceId将数据发送到其他设备的数据管理服务。再由数据管理服务将数据写入同应用的数据库内。


### 数据变化通知机制

增、删、改数据库时，会给订阅者发送数据变化的通知。主要分为本地数据变化通知和分布式数据变化通知。

- **本地数据变化通知**：本地设备的应用内订阅数据变化通知，数据库增删改数据时，会收到通知。

- **分布式数据变化通知**：同一应用订阅组网内其他设备数据变化的通知，其他设备增删改数据时，本设备会收到通知。


## 约束限制

- 每个应用程序最多支持同时打开16个关系型分布式数据库。

- 单个数据库最多支持注册8个订阅数据变化的回调。

- 不支持非系统应用调用需要指定设备的分布式能力接口。


## 接口说明

以下是关系型设备协同分布式数据库跨设备数据同步功能的相关接口，大部分为异步接口。异步接口均有callback和Promise两种返回形式，下表均以callback形式为例，更多接口及使用方式请见[关系型数据库](../reference/apis/js-apis-data-relationalStore.md)。

| 接口名称 | 描述 | 
| -------- | -------- |
| setDistributedTables(tables: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void | 设置分布式同步表。 | 
| sync(mode: SyncMode, predicates: RdbPredicates, callback: AsyncCallback&lt;Array&lt;[string, number]&gt;&gt;): void | 分布式数据同步。 | 
| on(event: 'dataChange', type: SubscribeType, observer: Callback&lt;Array&lt;string&gt;&gt;): void | 订阅分布式数据变化。 | 
| off(event:'dataChange', type: SubscribeType, observer: Callback&lt;Array&lt;string&gt;&gt;): void | 取消订阅分布式数据变化。 | 
| obtainDistributedTableName(device: string, table: string, callback: AsyncCallback&lt;string&gt;): void; | 根据本地数据库表名获取指定设备上的表名。 | 
| remoteQuery(device: string, table: string, predicates: RdbPredicates, columns: Array&lt;string&gt; , callback: AsyncCallback&lt;ResultSet&gt;): void | 根据指定条件查询远程设备数据库中的数据。 | 


## 开发步骤

> **说明：**
>
> 数据只允许向数据安全标签不高于对端设备安全等级的设备同步数据，具体规则可见[跨设备同步访问控制机制](sync-app-data-across-devices-overview.md#跨设备同步访问控制机制)。

1. 导入模块。
     
   ```js
   import relationalStore from '@ohos.data.relationalStore';
   ```

2. 请求权限。

   1. 需要申请ohos.permission.DISTRIBUTED_DATASYNC权限，配置方式请参见[配置文件权限声明](../security/accesstoken-guidelines.md#配置文件权限声明)。
   2. 同时需要在应用首次启动时弹窗向用户申请授权，使用方式请参见[向用户申请授权](../security/accesstoken-guidelines.md#向用户申请授权)。

3. 创建关系型数据库，设置将需要进行分布式同步的表。
     
   ```js
   const STORE_CONFIG = {
     name: 'RdbTest.db', // 数据库文件名
     securityLevel: relationalStore.SecurityLevel.S1 // 数据库安全级别
   };
   relationalStore.getRdbStore(this.context, STORE_CONFIG, (err, store) => {
     store.executeSql('CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, AGE INTEGER, SALARY REAL, CODES BLOB)', null, (err) => {
       // 设置分布式同步表。
       store.setDistributedTables(['EMPLOYEE']);
       // 进行数据的相关操作
     })
   })
   ```

4. 分布式数据同步。使用SYNC_MODE_PUSH触发同步后，数据将从本设备向组网内的其它所有设备同步。
     
   ```js
   // 构造用于同步分布式表的谓词对象
   let predicates = new relationalStore.RdbPredicates('EMPLOYEE');
   // 调用同步数据的接口
   store.sync(relationalStore.SyncMode.SYNC_MODE_PUSH, predicates, (err, result) => {
     // 判断数据同步是否成功
     if (err) {
       console.error(`Failed to sync data. Code:${err.code},message:${err.message}`);
       return;
     }
     console.info('Succeeded in syncing data.');
     for (let i = 0; i < result.length; i++) {
       console.info(`device:${result[i][0]},status:${result[i][1]}`);
     }
   })
   ```

5. 分布式数据订阅。数据同步变化将触发订阅回调方法执行，回调方法的入参为发生变化的设备ID。
     
   ```js
   let observer = function storeObserver(devices) {
     for (let i = 0; i < devices.length; i++) {
       console.info(`The data of device:${devices[i]} has been changed.`);
     }
   }
   
   try {
     // 调用分布式数据订阅接口，注册数据库的观察者
     // 当分布式数据库中的数据发生更改时，将调用回调
     store.on('dataChange', relationalStore.SubscribeType.SUBSCRIBE_TYPE_REMOTE, observer);
   } catch (err) {
     console.error('Failed to register observer. Code:${err.code},message:${err.message}');
   }
   
   // 当前不需要订阅数据变化时，可以将其取消。
   try {
     store.off('dataChange', relationalStore.SubscribeType.SUBSCRIBE_TYPE_REMOTE, observer);
   } catch (err) {
     console.error('Failed to register observer. Code:${err.code},message:${err.message}');
   }
   ```

6. 跨设备查询。如果数据未完成同步，或未触发数据同步，应用可以使用此接口从指定的设备上查询数据。

   > **说明：**
   >
   > deviceIds通过调用[devManager.getTrustedDeviceListSync](../reference/apis/js-apis-device-manager.md#gettrusteddevicelistsync)方法得到，deviceManager模块的接口均为系统接口，仅系统应用可用。

     
   ```js
   // 获取deviceIds
   import deviceManager from '@ohos.distributedHardware.deviceManager';
   
   deviceManager.createDeviceManager("com.example.appdatamgrverify", (err, manager) => {
     if (err) {
       console.info(`Failed to create device manager. Code:${err.code},message:${err.message}`);
       return;
     }
     let devices = manager.getTrustedDeviceListSync();
     let deviceId = devices[0].deviceId;
   
     // 构造用于查询分布式表的谓词对象
     let predicates = new relationalStore.RdbPredicates('EMPLOYEE');
     // 调用跨设备查询接口，并返回查询结果
     store.remoteQuery(deviceId, 'EMPLOYEE', predicates, ['ID', 'NAME', 'AGE', 'SALARY', 'CODES'],
       function (err, resultSet) {
         if (err) {
           console.error(`Failed to remoteQuery data. Code:${err.code},message:${err.message}`);
           return;
         }
         console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
       }
     )
   })
   ```

## 相关实例

针对关系型数据库开发，有以下相关实例可供参考：

- [分布式组网认证（ArkTS）（Full SDK）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/OpenHarmony-3.2-Release/code/SuperFeature/DistributedAppDev/DistributedAuthentication)

- [分布式关系型数据库（ArkTS）（Full SDK）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/OpenHarmony-3.2-Release/code/SuperFeature/DistributedAppDev/DistributedRdb)