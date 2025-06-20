# 分布式数据管理子系统Changelog

## cl.relationalStore.1 数据库插入长度为0的Uint8Array的数据，getRow、getValue 接口返回值发生变化

**访问级别**

公开接口

**变更原因**

当插入列类型是blob且数据为长度为0的Uint8Array时，数据库对应错误写入null值，导致使用getRow和getValue接口读取时，读取数值结果错误与插入数据不匹配。

**变更影响**

该变更为不兼容变更。

变更前：在blob类型的列里插入长度为0的Uint8Array，调用getRow/getValue接口，获取到的值是null。

变更后：在blob类型的列里插入长度为0的Uint8Array，调用getRow/getValue接口，获取到的值是长度为0的Uint8Array。

**起始 API Level**

| 接口名称 | 起始 API Level |
| -------- | -------------- |
| getRow   | API 11         |
| getValue | API 12         |

**变更发生版本**

从OpenHarmony SDK 5.0.0.46版本开始。

**变更的接口/组件**

@ohos.data.relationalStore.d.ts中getRow接口。
@ohos.data.relationalStore.d.ts中getValue接口。

**适配指导**

变更后，接口的调用方式没有发生变化。开发者需要关注，在blob类型的列里插入长度为0的Uint8Array后，调用getRow或getValue获取到的值发生了变化。
```ts
import { relationalStore } from '@kit.ArkData';
import { BusinessError } from '@kit.BasicServicesKit';
import { UIAbility } from '@kit.AbilityKit';
import { window } from '@kit.ArkUI';

const STORE_CONFIG: relationalStore.StoreConfig = {
  name: "RdbTest.db",
  securityLevel: relationalStore.SecurityLevel.S3
};
const CREATE_TABLE_TEST =
  "CREATE TABLE IF NOT EXISTS EMPLOYEE (id INTEGER PRIMARY KEY AUTOINCREMENT,name TEXT NOT NULL, age INTEGER, salary REAL, blobType BLOB)";

let store: relationalStore.RdbStore | undefined = undefined;
relationalStore.getRdbStore(this.context, STORE_CONFIG, (err: BusinessError, rdbStore: relationalStore.RdbStore) => {
  store = rdbStore;
  store.executeSql(CREATE_TABLE_TEST);
  if (err) {
    console.error(`Get RdbStore failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info('Get RdbStore successfully.');
})
//在ValuesBucket的blob类型插入长度为0的Uint8Array，并查询该数据。
let resultSet: relationalStore.ResultSet | undefined = undefined;
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
if (store != undefined) {
  (store as relationalStore.RdbStore).query(predicates).then((result: relationalStore.ResultSet) => {
    resultSet = result;
  });
}
if (resultSet != undefined) {
  //blobType是数据类型为blob的列名
  const codes = (resultSet as relationalStore.ResultSet).getValue((resultSet as relationalStore.ResultSet).getColumnIndex("blobType"));
}
//变更前 codes为null。
//变更后 codes为长度为0的Uint8Array。

if (resultSet != undefined) {
  const row = (resultSet as relationalStore.ResultSet).getRow();
}
//变更前 row.blobType为null。
//变更后 row.blobType为长度为0的Uint8Array。
```