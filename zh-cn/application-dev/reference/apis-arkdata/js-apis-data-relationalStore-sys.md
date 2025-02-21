# @ohos.data.relationalStore (关系型数据库)(系统接口)

关系型数据库（Relational Database，RDB）是一种基于关系模型来管理数据的数据库。关系型数据库基于SQLite组件提供了一套完整的对本地数据库进行管理的机制，对外提供了一系列的增、删、改、查等接口，也可以直接运行用户输入的SQL语句来满足复杂的场景需要。不支持Worker线程。
ArkTS侧支持的基本数据类型：number、string、二进制类型数据、boolean。为保证插入并读取数据成功，建议一条数据不要超过2M。超出该大小，插入成功，读取失败。

该模块提供以下关系型数据库相关的常用功能：

- [RdbPredicates](js-apis-data-relationalStore.md#rdbpredicates)： 数据库中用来代表数据实体的性质、特征或者数据实体之间关系的词项，主要用来定义数据库的操作条件。
- [RdbStore](#rdbstore)：提供管理关系数据库(RDB)方法的接口。
- [ResultSet](js-apis-data-relationalStore.md#resultset)：提供用户调用关系型数据库查询接口之后返回的结果集合。

> **说明：**
> 
> - 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> - 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.data.relationalStore (关系型数据库)](js-apis-data-relationalStore.md)。

## 导入模块

```ts
import relationalStore from '@ohos.data.relationalStore';
```

## StoreConfig

管理数据库配置。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称        | 类型          | 必填 | 说明                                                      |
| ------------- | ------------- | ---- | --------------------------------------------------------- |
| isSearchable<sup>11+</sup> | boolean | 否 | 指定数据库是否支持搜索，true表示支持搜索，false表示不支持搜索，默认不支持搜索。<br/>**系统接口：** 此接口为系统接口。<br/>从API version 11开始，支持此可选参数。|

## Reference<sup>11+</sup>

记录表之间通过表字段指定的关联关系。其中表a关联到表b，称a为b关联的子表，b为a关联的父表。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**系统接口：** 此接口为系统接口。

| 名称       | 类型   | 必填 | 说明                                     |
| ---------- | ------ | ---- | ---------------------------------------- |
| sourceTable | string | 是   | 关联的子表名称。   |
| targetTable | string | 是   | 关联的父表名称。   |
| refFields   | Record<string, string> | 是   | 表示关联表的关联字段。键值数据中键为子表字段，值为父表字段。       |

## DistributedConfig<sup>10+</sup>

记录表的分布式配置信息。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称     | 类型    | 必填 | 说明                                                         |
| -------- | ------- | ---- | ------------------------------------------------------------ |
| references<sup>11+</sup> | Array&lt;[Reference](#reference11)&gt; | 否   | 设置表之间的关联关系，可以设置多个字段的关联，子表和父表关联字段的值必须相同。默认数据库表之间无关联关系。<br/>**系统接口：** 此接口为系统接口。<br/>从API version 11开始，支持此可选参数。|

## RdbStore

提供管理关系型数据库（RDB）的接口。
在使用以下相关接口前，请使用[executeSql](js-apis-data-relationalStore.md#executesql)接口初始化数据库表结构和相关数据。

### update

update(table: string, values: ValuesBucket, predicates: dataSharePredicates.DataSharePredicates, callback: AsyncCallback&lt;number&gt;):void

根据DataSharePredicates的指定实例对象更新数据库中的数据，使用callback异步回调。由于共享内存大小限制为2Mb，因此单条数据的大小需小于2Mb，否则会查询失败。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                         |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| table      | string                                                       | 是   | 指定的目标表名。                                             |
| values     | [ValuesBucket](js-apis-data-relationalStore.md#valuesbucket)                                | 是   | values指示数据库中要更新的数据行。键值对与数据库表的列名相关联。 |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的更新条件。                |
| callback   | AsyncCallback&lt;number&gt;                                  | 是   | 指定的callback回调方法。返回受影响的行数。                   |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates'
import { ValuesBucket } from '@ohos.data.ValuesBucket';

let value1 = "Rose";
let value2 = 22;
let value3 = 200.5;
let value4 = new Uint8Array([1, 2, 3, 4, 5]);

// 以下三种方式可用
const valueBucket1: ValuesBucket = {
  'NAME': value1,
  'AGE': value2,
  'SALARY': value3,
  'CODES': value4,
};
const valueBucket2: ValuesBucket = {
  NAME: value1,
  AGE: value2,
  SALARY: value3,
  CODES: value4,
};
const valueBucket3: ValuesBucket = {
  "NAME": value1,
  "AGE": value2,
  "SALARY": value3,
  "CODES": value4,
};

let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Lisa");
if(store != undefined) {
  (store as relationalStore.RdbStore).update("EMPLOYEE", valueBucket1, predicates, (err, rows) => {
    if (err) {
      console.error(`Updated failed, code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info(`Updated row count: ${rows}`);
  })
}
```

### update

update(table: string, values: ValuesBucket, predicates: dataSharePredicates.DataSharePredicates):Promise&lt;number&gt;

根据DataSharePredicates的指定实例对象更新数据库中的数据，使用Promise异步回调。由于共享内存大小限制为2Mb，因此单条数据的大小需小于2Mb，否则会查询失败。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                         |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| table      | string                                                       | 是   | 指定的目标表名。                                             |
| values     | [ValuesBucket](js-apis-data-relationalStore.md#valuesbucket)                                | 是   | values指示数据库中要更新的数据行。键值对与数据库表的列名相关联。 |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的更新条件。                |

**返回值**：

| 类型                  | 说明                                      |
| --------------------- | ----------------------------------------- |
| Promise&lt;number&gt; | 指定的Promise回调方法。返回受影响的行数。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { ValuesBucket } from '@ohos.data.ValuesBucket';
import { BusinessError } from "@ohos.base";

let value1 = "Rose";
let value2 = 22;
let value3 = 200.5;
let value4 = new Uint8Array([1, 2, 3, 4, 5]);

// 以下三种方式可用
const valueBucket1: ValuesBucket = {
  'NAME': value1,
  'AGE': value2,
  'SALARY': value3,
  'CODES': value4,
};
const valueBucket2: ValuesBucket = {
  NAME: value1,
  AGE: value2,
  SALARY: value3,
  CODES: value4,
};
const valueBucket3: ValuesBucket = {
  "NAME": value1,
  "AGE": value2,
  "SALARY": value3,
  "CODES": value4,
};

let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Lisa");
if(store != undefined) {
  (store as relationalStore.RdbStore).update("EMPLOYEE", valueBucket1, predicates).then(async (rows: Number) => {
    console.info(`Updated row count: ${rows}`);
  }).catch((err: BusinessError) => {
    console.error(`Updated failed, code is ${err.code},message is ${err.message}`);
  })
}
```

### delete

delete(table: string, predicates: dataSharePredicates.DataSharePredicates, callback: AsyncCallback&lt;number&gt;):void

根据DataSharePredicates的指定实例对象从数据库中删除数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                          |
| ---------- | ------------------------------------------------------------ | ---- | --------------------------------------------- |
| table      | string                                                       | 是   | 指定的目标表名。                              |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的删除条件。 |
| callback   | AsyncCallback&lt;number&gt;                                  | 是   | 指定callback回调函数。返回受影响的行数。      |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Lisa");
if(store != undefined) {
  (store as relationalStore.RdbStore).delete("EMPLOYEE", predicates, (err, rows) => {
    if (err) {
      console.error(`Delete failed, code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info(`Delete rows: ${rows}`);
  })
}
```

### delete

delete(table: string, predicates: dataSharePredicates.DataSharePredicates):Promise&lt;number&gt;

根据DataSharePredicates的指定实例对象从数据库中删除数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                          |
| ---------- | ------------------------------------------------------------ | ---- | --------------------------------------------- |
| table      | string                                                       | 是   | 指定的目标表名。                              |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的删除条件。 |

**返回值**：

| 类型                  | 说明                            |
| --------------------- | ------------------------------- |
| Promise&lt;number&gt; | Promise对象。返回受影响的行数。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from "@ohos.base";

let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Lisa");
if(store != undefined) {
  (store as relationalStore.RdbStore).delete("EMPLOYEE", predicates).then((rows: Number) => {
    console.info(`Delete rows: ${rows}`);
  }).catch((err: BusinessError) => {
    console.error(`Delete failed, code is ${err.code},message is ${err.message}`);
  })
}
```

### query<sup>10+</sup>

query(table: string, predicates: dataSharePredicates.DataSharePredicates, callback: AsyncCallback&lt;ResultSet&gt;):void

根据指定条件查询数据库中的数据，使用callback异步回调。由于共享内存大小限制为2Mb，因此单条数据的大小需小于2Mb，否则会查询失败。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------------- |
| table      | string                                                       | 是   | 指定的目标表名。                                            |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的查询条件。               |
| callback   | AsyncCallback&lt;[ResultSet](#resultset)&gt; | 是   | 指定callback回调函数。如果操作成功，则返回ResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Rose");
if(store != undefined) {
  (store as relationalStore.RdbStore).query("EMPLOYEE", predicates, (err, resultSet) => {
    if (err) {
      console.error(`Query failed, code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
    // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
    while (resultSet.goToNextRow()) {
      const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
      const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
      const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
      const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
      console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
    }
    // 释放数据集的内存
    resultSet.close();
  })
}
```

### query

query(table: string, predicates: dataSharePredicates.DataSharePredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;ResultSet&gt;):void

根据指定条件查询数据库中的数据，使用callback异步回调。由于共享内存大小限制为2Mb，因此单条数据的大小需小于2Mb，否则会查询失败。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------------- |
| table      | string                                                       | 是   | 指定的目标表名。                                            |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的查询条件。               |
| columns    | Array&lt;string&gt;                                          | 是   | 表示要查询的列。如果值为空，则查询应用于所有列。            |
| callback   | AsyncCallback&lt;[ResultSet](#resultset)&gt; | 是   | 指定callback回调函数。如果操作成功，则返回ResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Rose");
if(store != undefined) {
  (store as relationalStore.RdbStore).query("EMPLOYEE", predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"], (err, resultSet) => {
    if (err) {
      console.error(`Query failed, code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
    // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
    while (resultSet.goToNextRow()) {
      const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
      const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
      const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
      const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
      console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
    }
    // 释放数据集的内存
    resultSet.close();
  })
}
```

### query

query(table: string, predicates: dataSharePredicates.DataSharePredicates, columns?: Array&lt;string&gt;):Promise&lt;ResultSet&gt;

根据指定条件查询数据库中的数据，使用Promise异步回调。由于共享内存大小限制为2Mb，因此单条数据的大小需小于2Mb，否则会查询失败。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                             |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------ |
| table      | string                                                       | 是   | 指定的目标表名。                                 |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的查询条件。    |
| columns    | Array&lt;string&gt;                                          | 否   | 表示要查询的列。如果值为空，则查询应用于所有列。 |

**返回值**：

| 类型                                                    | 说明                                               |
| ------------------------------------------------------- | -------------------------------------------------- |
| Promise&lt;[ResultSet](#resultset)&gt; | Promise对象。如果操作成功，则返回ResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from "@ohos.base";

let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Rose");
if(store != undefined) {
  (store as relationalStore.RdbStore).query("EMPLOYEE", predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]).then((resultSet: relationalStore.ResultSet) => {
    console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
    // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
    while (resultSet.goToNextRow()) {
      const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
      const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
      const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
      const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
      console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
    }
    // 释放数据集的内存
    resultSet.close();
  }).catch((err: BusinessError) => {
    console.error(`Query failed, code is ${err.code},message is ${err.message}`);
  })
}
```

### cloudSync<sup>11+</sup>

cloudSync(mode: SyncMode, predicates: RdbPredicates, progress: Callback&lt;ProgressDetails&gt;, callback: AsyncCallback&lt;void&gt;): void

手动执行按条件进行端云同步，使用callback异步回调。使用该接口需要实现云同步功能。

**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名         | 类型                             | 必填 | 说明                            |
|-------------|--------------------------------| ---- |-------------------------------|
| mode        | [SyncMode](js-apis-data-relationalStore.md#syncmode)          | 是   | 表示数据库的同步模式。                   |
| predicates  | [RdbPredicates](js-apis-data-relationalStore.md#rdbpredicates)                  | 是   | 表示同步数据的谓词条件。                  |
| progress    | Callback&lt;[ProgressDetails](js-apis-data-relationalStore.md#progressdetails10)&gt; | 是   | 用来处理数据库同步详细信息的回调函数。           |
| callback    | AsyncCallback&lt;void&gt;      | 是   | 指定的callback回调函数，用于向调用者发送同步结果。 |

**示例：**

```ts
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.in("id", ["id1", "id2"]);

if(store != undefined) {
  (store as relationalStore.RdbStore).cloudSync(relationalStore.SyncMode.SYNC_MODE_CLOUD_FIRST, predicates, (progressDetail: relationalStore.ProgressDetails) => {
    console.info(`progress: ${progressDetail}`);
   }, (err) => {
     if (err) {
       console.error(`cloudSync failed, code is ${err.code},message is ${err.message}}`);
       return;
     }
     console.info('Cloud sync succeeded');
  });
};
```

### cloudSync<sup>11+</sup>

cloudSync(mode: SyncMode, predicates: RdbPredicates, progress: Callback&lt;ProgressDetails&gt;): Promise&lt;void&gt;

手动执行按条件进行端云同步，使用Promise异步处理。使用该接口需要实现云同步功能。

**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名        | 类型                              | 必填 | 说明                  |
|------------|---------------------------------| ---- |---------------------|
| mode       | [SyncMode](js-apis-data-relationalStore.md#syncmode)           | 是   | 表示数据库的同步模式。         |
| predicates | [RdbPredicates](js-apis-data-relationalStore.md#rdbpredicates)                   | 是   | 表示同步数据的谓词条件。                |
| progress   | Callback&lt;[ProgressDetails](js-apis-data-relationalStore.md#progressdetails10)&gt; | 是   | 用来处理数据库同步详细信息的回调函数。 |

**返回值**：

| 类型                | 说明                                    |
| ------------------- | --------------------------------------- |
| Promise&lt;void&gt; | Promise对象，用于向调用者发送同步结果。 |

**示例：**

```ts
import {BusinessError} from "@ohos.base";

let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.in("id", ["id1", "id2"]);

if(store != undefined) {
  (store as relationalStore.RdbStore).cloudSync(relationalStore.SyncMode.SYNC_MODE_CLOUD_FIRST, predicates, (progressDetail: relationalStore.ProgressDetails) => {
    console.info(`progress: ${progressDetail}`);
  }).then(() => {
    console.info('Cloud sync succeeded');
  }).catch((err: BusinessError) => {
    console.error(`cloudSync failed, code is ${err.code},message is ${err.message}}`);
  });
};
```

### querySharingResource<sup>11+</sup>

querySharingResource(predicates: RdbPredicates, columns?: Array&lt;string&gt;): Promise&lt;ResultSet&gt;

根据谓词条件匹配的数据记录查找对应记录的共享资源标识，返回查找的结果集。 如果指定了列字段，则返回结果集中同时包含对应列的字段值，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                               |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------------------- |
| predicates | [RdbPredicates](js-apis-data-relationalStore.md#rdbpredicates) | 是   | 表示查询的谓词条件。    |
| columns    | Array&lt;string&gt;      | 否   | 表示要查找的列字段名。此参数不填时，返回的结果集中只包含共享资源标识字段。 |

**返回值：**

| 参数名    | 说明                                               |
| -------- | ------------------------------------------------- |
| Promise&lt;[ResultSet](#resultset)&gt; | Promise对象，返回查询的结果集。   |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 14800000     | Inner error.                           |

**示例：**

```ts
import { BusinessError } from "@ohos.base";

let sharingResource: string;
let predicates = new relationalStore.RdbPredicates('test_table');
predicates.equalTo('data', 'data_test');
if(store != undefined) {
  (store as relationalStore.RdbStore).querySharingResource(predicates, ['uuid', 'data']).then((resultSet) => {
    if (!resultSet.goToFirstRow()) {
      console.error(`resultSet error`);
      return;
    }
    const res = resultSet.getString(resultSet.getColumnIndex(relationalStore.Field.SHARING_RESOURCE_FIELD));
    console.info(`sharing resource: ${res}`);
    sharingResource = res;
  }).catch((err: BusinessError) => {
    console.error(`query sharing resource failed, code is ${err.code},message is ${err.message}`);
  })
}

```

### querySharingResource<sup>11+</sup>

querySharingResource(predicates: RdbPredicates, callback: AsyncCallback&lt;ResultSet&gt;): void

根据谓词条件匹配的数据记录查找对应记录的共享资源，返回查找的结果集，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                               |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------------------- |
| predicates | [RdbPredicates](js-apis-data-relationalStore.md#rdbpredicates)              | 是   | 表示查询的谓词条件。           |
| callback   | AsyncCallback&lt;[ResultSet](#resultset)&gt; | 是   | 回调函数。返回查询的结果集。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 14800000     | Inner error.                           |

**示例：**

```ts
let sharingResource: string;
let predicates = new relationalStore.RdbPredicates('test_table');
predicates.equalTo('data', 'data_test');
if(store != undefined) {
  (store as relationalStore.RdbStore).querySharingResource(predicates,(err, resultSet) => {
    if (err) {
      console.error(`sharing resource failed, code is ${err.code},message is ${err.message}`);
      return;
    }
    if (!resultSet.goToFirstRow()) {
      console.error(`resultSet error`);
      return;
    }
    const res = resultSet.getString(resultSet.getColumnIndex(relationalStore.Field.SHARING_RESOURCE_FIELD));
    console.info(`sharing resource: ${res}`);
    sharingResource = res;
  })
}

```

### querySharingResource<sup>11+</sup>

querySharingResource(predicates: RdbPredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;ResultSet&gt;): void

根据谓词条件匹配的数据记录查找对应记录的共享资源，返回查找到的共享资源的结果集，同时在结果集中返回谓词条件匹配的指定列名的字段值，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                               |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------------------- |
| predicates | [RdbPredicates](js-apis-data-relationalStore.md#rdbpredicates) | 是   | 表示查询的谓词条件。           |
| columns    | Array&lt;string&gt;              | 是   | 表示要查找的列字段名。           |
| callback   | AsyncCallback&lt;[ResultSet](#resultset)&gt;  | 是   | 回调函数。返回查询的结果集。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 14800000     | Inner error.                           |

**示例：**

```ts
let sharingResource: string;
let predicates = new relationalStore.RdbPredicates('test_table');
predicates.equalTo('data', 'data_test');
if(store != undefined) {
  (store as relationalStore.RdbStore).querySharingResource(predicates, ['uuid', 'data'], (err, resultSet) => {
    if (err) {
      console.error(`sharing resource failed, code is ${err.code},message is ${err.message}`);
      return;
    }
    if (!resultSet.goToFirstRow()) {
      console.error(`resultSet error`);
      return;
    }
    const res = resultSet.getString(resultSet.getColumnIndex(relationalStore.Field.SHARING_RESOURCE_FIELD));
    console.info(`sharing resource: ${res}`);
    sharingResource = res;
  })
}

```