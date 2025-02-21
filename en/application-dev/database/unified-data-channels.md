# Sharing Data via Unified Data Channels


## When to Use

In many-to-many data sharing across applications, a data channel needs to be provided to access data of different applications and share the data with other applications.

The Unified Data Management Framework (UDMF) provides unified data channels and standard data access interfaces for different service scenarios of many-to-many cross-application data sharing.

## Definition and Implementation of Unified Data Channels

The unified data channel provides cross-application data access for various service scenarios. It can temporarily store the unified data objects to be shared by an application, and manage the access permissions and lifecycle of the data according to certain policies.

The unified data channel is implemented by the system ability provided by the UDMF. When an application (data provider) needs to share data, it calls the **insert()** method provided by the UDMF to write the data to the UDMF data channel, and calls UDMF **update()** or **delete()** to update or delete the data. After passing the permission verification, the target application (data consumer) calls the UDMF **read()** to access the data. After the data is read, the UDMF performs lifecycle management of the data.

The unified data object (**UnifiedData**) is uniquely identified by a URI in the UDMF data channel. The URI is in the **udmf://*intention*/*bundleName*/*groupId*** format, where:

+ **udmf**: protocol used to provide the data channel.

+ *intention*: an enum of the data channel types supported by the UDMF.

+ *bundleName*: bundle name of the data source application.

+ *groupId*: group ID used for batch data management.

Currently, the UDMF provides the public data channel for cross-application data sharing.

The public data channel is a data channel shared by applications. All applications can write data to the channel. The data provider can update, delete, and query data based on the unique identifier generated when the data is written. The data consumer can read only the full data in the public data channel. The intention type of the public data channel is **DATA_HUB**.

## Available APIs

The following table lists the UDMF APIs. All of them are executed asynchronously in callback or promise mode. In the following table, callback-based APIs are used as an example. For details about more APIs and their usage, see [Unified Data Channel](../reference/apis-arkdata/js-apis-data-unifiedDataChannel.md) and [Standard Data Definition and Description](../reference/apis-arkdata/js-apis-data-uniformTypeDescriptor.md).

| API                                                                                   | Description                                         |
|-----------------------------------------------------------------------------------------|---------------------------------------------|
| insertData(options: Options, data: UnifiedData, callback: AsyncCallback\<string>): void | Inserts data to the UDMF public data channel. A unique data identifier is returned.|
| updateData(options: Options, data: UnifiedData, callback: AsyncCallback\<void>): void   | Updates the data in the UDMF public data channel.          |
| queryData(options: Options, callback: AsyncCallback\<Array\<UnifiedData>>): void        | Queries data in the UDMF public data channel.              |
| deleteData(options: Options, callback: AsyncCallback\<Array\<UnifiedData>>): void       | Deletes data from the UDMF public data channel. The deleted data set is returned.|


## How to Develop

The following example describes how to implement many-to-many data sharing. The data provider calls **insertData()** provided by the UMDF to write data to the public data channel. The return value (unique identifier of the data written) can be used to update or delete the data. The data consumer uses the query() APIs provided by the UDMF to obtain full data in the public data channel.

### Data Provider

1. Import the **@ohos.data.unifiedDataChannel** and **@ohos.data.uniformTypeDescriptor** modules.

   ```ts
   import unifiedDataChannel from '@ohos.data.unifiedDataChannel';
   import uniformTypeDescriptor from '@ohos.data.uniformTypeDescriptor';
   ```
2. Create a **UnifiedData** object and insert it into the UDMF public data channel.

   ```ts
   import { BusinessError } from '@ohos.base';
   let plainText = new unifiedDataChannel.PlainText();
   plainText.textContent = 'hello world!';
   let unifiedData = new unifiedDataChannel.UnifiedData(plainText);
   
   // Specify the type of the data channel to which the data is to be inserted.
   let options: unifiedDataChannel.Options = {
     intention: unifiedDataChannel.Intention.DATA_HUB
   }
   try {
     unifiedDataChannel.insertData(options, unifiedData, (err, key) => {
       if (err === undefined) {
         console.info(`Succeeded in inserting data. key = ${key}`);
       } else {
         console.error(`Failed to insert data. code is ${err.code},message is ${err.message} `);
       }
     });
   } catch (e) {
     let error: BusinessError = e as BusinessError;
     console.error(`Insert data throws an exception. code is ${error.code},message is ${error.message} `);
   }
   ```
3. Update the **UnifiedData** object inserted.

   ```ts
   import { BusinessError } from '@ohos.base';
   let plainText = new unifiedDataChannel.PlainText();
   plainText.textContent = 'How are you!';
   let unifiedData = new unifiedDataChannel.UnifiedData(plainText);
   
   // Specify the URI of the UnifiedData object to update.
   let options: unifiedDataChannel.Options = {
     // The key here is an example and cannot be directly used. Use the value in the callback of insertData().
     key: 'udmf://DataHub/com.ohos.test/0123456789'
   };
   
   try {
     unifiedDataChannel.updateData(options, unifiedData, (err) => {
       if (err === undefined) {
         console.info('Succeeded in updating data.');
       } else {
         console.error(`Failed to update data. code is ${err.code},message is ${err.message} `);
       }
     });
   } catch (e) {
     let error: BusinessError = e as BusinessError;
     console.error(`Update data throws an exception. code is ${error.code},message is ${error.message} `);
   }
   ```
4. Delete the **UnifiedData** object from the UDMF public data channel.

   ```ts
   import { BusinessError } from '@ohos.base';
   // Specify the type of the data channel whose data is to be deleted.
   let options: unifiedDataChannel.Options = {
     intention: unifiedDataChannel.Intention.DATA_HUB
   };

   try {
     unifiedDataChannel.deleteData(options, (err, data) => {
       if (err === undefined) {
         console.info(`Succeeded in deleting data. size = ${data.length}`);
         for (let i = 0; i < data.length; i++) {
           let records = data[i].getRecords();
           for (let j = 0; j < records.length; j++) {
             if (records[j].getType() === uniformTypeDescriptor.UniformDataType.PLAIN_TEXT) {
               let text = records[j] as unifiedDataChannel.PlainText;
               console.info(`${i + 1}.${text.textContent}`);
             }
           }
         }
       } else {
         console.error(`Failed to delete data. code is ${err.code},message is ${err.message} `);
       }
     });
   } catch (e) {
     let error: BusinessError = e as BusinessError;
     console.error(`Delete data throws an exception. code is ${error.code},message is ${error.message} `);
   }
   ```
   
### Data Consumer

1. Import the **@ohos.data.unifiedDataChannel** and **@ohos.data.uniformTypeDescriptor** modules.

   ```ts
   import unifiedDataChannel from '@ohos.data.unifiedDataChannel';
   import uniformTypeDescriptor from '@ohos.data.uniformTypeDescriptor';
   ```
2. Query the full data in the UDMF public data channel.

   ```ts
   import { BusinessError } from '@ohos.base';
   // Specify the type of the data channel whose data is to be queried.
   let options: unifiedDataChannel.Options = {
     intention: unifiedDataChannel.Intention.DATA_HUB
   };

   try {
     unifiedDataChannel.queryData(options, (err, data) => {
       if (err === undefined) {
         console.info(`Succeeded in querying data. size = ${data.length}`);
         for (let i = 0; i < data.length; i++) {
           let records = data[i].getRecords();
           for (let j = 0; j < records.length; j++) {
             if (records[j].getType() === uniformTypeDescriptor.UniformDataType.PLAIN_TEXT) {
               let text = records[j] as unifiedDataChannel.PlainText;
               console.info(`${i + 1}.${text.textContent}`);
             }
           }
         }
       } else {
         console.error(`Failed to query data. code is ${err.code},message is ${err.message} `);
       }
     });
   } catch(e) {
     let error: BusinessError = e as BusinessError;
     console.error(`Query data throws an exception. code is ${error.code},message is ${error.message} `);
   }
   ```
