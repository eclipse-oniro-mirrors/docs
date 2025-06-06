# relational_store.h


## Overview

Provides APIs for managing data in a relational database (RDB) store. The APIs not marked as supporting vector stores are available only to RDB stores.

**File to include**: <database/rdb/relational_store.h>

**Library**: libnative_rdb_ndk.z.so

**Since**: 10

**Related module**: [RDB](_r_d_b.md)


## Summary


### Structs

| Name| Description|
| -------- | -------- |
| [OH_Rdb_Config](_o_h___rdb___config.md) | Represents the RDB store configuration.|
| [OH_Rdb_Store](_o_h___rdb___store.md) | Represents the RDB store type.|
| [Rdb_DistributedConfig](_rdb___distributed_config.md) | Represents the distributed configuration of a table.|
| [Rdb_KeyInfo](_rdb___key_info.md) | Represents the primary key or row number of the row that changes.|
| [Rdb_KeyInfo::Rdb_KeyData](union_rdb___key_info_1_1_rdb___key_data.md) | Represents the changed data.|
| [Rdb_ChangeInfo](_rdb___change_info.md) | Represents the details about the device-cloud sync.|
| [Rdb_SubscribeCallback](union_rdb___subscribe_callback.md) | Represents a callback used to listen for data changes.|
| [Rdb_DataObserver](_rdb___data_observer.md) | Represents the data observer.|
| [Rdb_Statistic](_rdb___statistic.md) | Represents the device-cloud sync statistics of a table.|
| [Rdb_TableDetails](_rdb___table_details.md) | Represents the statistics of device-cloud upload and download tasks of a table.|
| [Rdb_ProgressDetails](_rdb___progress_details.md) | Represents the statistics of the overall device-cloud upload and download tasks of a database.|
| [Rdb_ProgressObserver](_rdb___progress_observer.md) | Represents the observer of the device-cloud sync progress.|


### Macros

| Name| Description|
| -------- | -------- |
| [DISTRIBUTED_CONFIG_VERSION](_r_d_b.md#distributed_config_version)&nbsp;&nbsp;&nbsp;1 | Version of [Rdb_DistributedConfig](_rdb___distributed_config.md).|
| [DISTRIBUTED_CHANGE_INFO_VERSION](_r_d_b.md#distributed_change_info_version)&nbsp;&nbsp;&nbsp;1 | Version of [Rdb_ChangeInfo](_rdb___change_info.md).|
| [DISTRIBUTED_PROGRESS_DETAIL_VERSION](_r_d_b.md#distributed_progress_detail_version)&nbsp;&nbsp;&nbsp;1 | Version of [Rdb_ProgressDetails](_rdb___progress_details.md).|


### Types

| Name| Description|
| -------- | -------- |
| [OH_Rdb_SecurityLevel](_r_d_b.md#oh_rdb_securitylevel) | Defines an enum for RDB store security levels.|
| [Rdb_SecurityArea](_r_d_b.md#rdb_securityarea) | Defines an enum for database directory encryption levels.|
| typedef struct [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) | Defines a struct for the RDB store configuration. Different from [OH_Rdb_Config](_o_h___rdb___config.md), this struct does not expose its member variables externally. Methods are used to configure the properties of this struct. It supports vector stores.|
| typedef enum [Rdb_DBType](_r_d_b.md#rdb_dbtype) [Rdb_DBType](_r_d_b.md#rdb_dbtype) | Defines an enum for the database kernel types.|
| [Rdb_DistributedType](_r_d_b.md#rdb_distributedtype) | Defines an enum for distributed types.|
| [Rdb_DistributedConfig](_r_d_b.md#rdb_distributedconfig) | Defines a struct for the distributed configuration of a table.|
| [Rdb_ChangeType](_r_d_b.md#rdb_changetype) | Defines an enum for data change types.|
| [Rdb_KeyInfo](_r_d_b.md#rdb_keyinfo) | Defines a struct for the primary key or row number of the row that changes.|
| [Rdb_ChangeInfo](_r_d_b.md#rdb_changeinfo) | Defines a struct for details about the device-cloud sync process.|
| [Rdb_SubscribeType](_r_d_b.md#rdb_subscribetype) | Defines an enum for subscription types.|
| [Rdb_BriefObserver](_r_d_b.md#rdb_briefobserver) | Defines a callback used to return the device-cloud data change event.|
| [Rdb_DetailsObserver](_r_d_b.md#rdb_detailsobserver) | Defines a callback used to return the details about the device-cloud data change.|
| [Rdb_SubscribeCallback](union_rdb___subscribe_callback.md) |  Defines a callback used to return the subscribed event.|
| [Rdb_DataObserver](_rdb___data_observer.md) | Defines a struct for the data observer.|
| [Rdb_SyncMode](_r_d_b.md#rdb_syncmode) | Defines an enum for RDB store sync modes.|
| [Rdb_Statistic](_r_d_b.md#rdb_statistic) | Defines a struct for device-cloud sync statistics of a database table.|
| [Rdb_TableDetails](_r_d_b.md#rdb_tabledetails) | Defines a struct for statistics of device-cloud upload and download tasks of a database table.|
| [Rdb_Progress](_r_d_b.md#rdb_progress) | Defines an enum for device-cloud sync progresses.|
| [Rdb_ProgressCode](_r_d_b.md#rdb_progresscode) | Defines an enum for states in the device-cloud sync process.|
| [Rdb_ProgressDetails](_r_d_b.md#rdb_progressdetails) | Defines a struct for statistics of the overall device-cloud upload and download tasks of an RDB store.|
| [Rdb_ProgressCallback](_r_d_b.md#rdb_progresscallback) | Defines a callback used to return the device-cloud sync progress.|
| [Rdb_SyncCallback](_r_d_b.md#rdb_synccallback) | Defines a callback to be invoked in device-cloud sync.|
| [Rdb_ProgressObserver](_r_d_b.md#rdb_progressobserver) | Defines a struct for the observer of the device-cloud sync progress.|


### Enums

| Name| Description|
| -------- | -------- |
| [OH_Rdb_SecurityLevel](_r_d_b.md#oh_rdb_securitylevel-1) { S1 = 1, S2, S3, S4} | Enumerates the RDB store security levels.|
| [Rdb_SecurityArea](_r_d_b.md#rdb_securityarea-1) { RDB_SECURITY_AREA_EL1 = 1, RDB_SECURITY_AREA_EL2, RDB_SECURITY_AREA_EL3, RDB_SECURITY_AREA_EL4 } | Enumerates the database directory encryption levels.|
| [Rdb_DBType](_r_d_b.md#rdb_dbtype-1) { RDB_SQLITE = 1, RDB_CAYLEY = 2, DBTYPE_BUTT = 64 } | Enumerates the database kernel types.|
| [Rdb_DistributedType](_r_d_b.md#rdb_distributedtype-1) { RDB_DISTRIBUTED_CLOUD } | Enumerates the distributed types.|
| [Rdb_ChangeType](_r_d_b.md#rdb_changetype-1) { RDB_DATA_CHANGE, RDB_ASSET_CHANGE } | Enumerates the data change types.|
| [Rdb_SubscribeType](_r_d_b.md#rdb_subscribetype-1) { RDB_SUBSCRIBE_TYPE_CLOUD, RDB_SUBSCRIBE_TYPE_CLOUD_DETAILS, RDB_SUBSCRIBE_TYPE_LOCAL_DETAILS } | Enumerates the subscription types.|
| [Rdb_SyncMode](_r_d_b.md#rdb_syncmode-1) { RDB_SYNC_MODE_TIME_FIRST, RDB_SYNC_MODE_NATIVE_FIRST, RDB_SYNC_MODE_CLOUD_FIRST } | Enumerates the RDB store sync modes.|
| [Rdb_Progress](_r_d_b.md#rdb_progress-1) { RDB_SYNC_BEGIN, RDB_SYNC_IN_PROGRESS, RDB_SYNC_FINISH } | Enumerates the device-cloud sync progresses.|
| [Rdb_ProgressCode](_r_d_b.md#rdb_progresscode-1) {<br>RDB_SUCCESS, RDB_UNKNOWN_ERROR, RDB_NETWORK_ERROR, RDB_CLOUD_DISABLED,<br>RDB_LOCKED_BY_OTHERS, RDB_RECORD_LIMIT_EXCEEDED, RDB_NO_SPACE_FOR_ASSET<br>} | Enumerates the states in the device-cloud sync process.|


### Functions

| Name| Description|
| -------- | -------- |
| int [OH_Rdb_SetPersistent](_r_d_b.md#oh_rdb_setpersistent) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, bool isPersistent) | Sets whether to persist an RDB store. | 
| int [OH_Rdb_BatchInsert](_r_d_b.md#oh_rdb_batchinsert) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*table, const [OH_Data_VBuckets](_r_d_b.md#oh_data_vbuckets) \*rows, [Rdb_ConflictResolution](_r_d_b.md#rdb_conflictresolution) resolution, int64_t \*changes) | Inserts a batch of data into a table. | 
| int [OH_Rdb_CreateTransaction](_r_d_b.md#oh_rdb_createtransaction) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const [OH_RDB_TransOptions](_r_d_b.md#oh_rdb_transoptions) \*options, [OH_Rdb_Transaction](_r_d_b.md#oh_rdb_transaction) \*\*trans) | Creates a transaction object.|
| int [OH_Rdb_ExecuteV2](_r_d_b.md#oh_rdb_executev2) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*sql, const [OH_Data_Values](_r_d_b.md#oh_data_values) \*args, [OH_Data_Value](_r_d_b.md#oh_data_value) \*\*result) | Executes an SQL statement with a return value. This API supports vector stores.|
| [OH_Cursor](_o_h___cursor.md) \* [OH_Rdb_ExecuteQueryV2](_r_d_b.md#oh_rdb_executequeryv2) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*sql, const [OH_Data_Values](_r_d_b.md#oh_data_values) \*args) | Queries data in the database using the specified SQL statement. This API supports vector stores.|
| int [OH_Rdb_IsTokenizerSupported](_r_d_b.md#oh_rdb_istokenizersupported) ([Rdb_Tokenizer](_r_d_b.md#rdb_tokenizer) tokenizer, bool \*isSupported) | Checks whether the specified tokenizer is supported.|
| int [OH_Rdb_SetTokenizer](_r_d_b.md#oh_rdb_settokenizer) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, [Rdb_Tokenizer](_r_d_b.md#rdb_tokenizer) tokenizer) | Sets a tokenizer for a database file.|
| [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \* [OH_Rdb_CreateConfig](_r_d_b.md#oh_rdb_createconfig) () | Creates an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| int [OH_Rdb_DestroyConfig](_r_d_b.md#oh_rdb_destroyconfig) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config) | Destroys an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| int [OH_Rdb_SetDatabaseDir](_r_d_b.md#oh_rdb_setdatabasedir) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, const char \*databaseDir) | Sets the database file path for an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| int [OH_Rdb_SetStoreName](_r_d_b.md#oh_rdb_setstorename) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, const char \*storeName) | Sets the database name for an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| int [OH_Rdb_SetBundleName](_r_d_b.md#oh_rdb_setbundlename) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, const char \*bundleName) | Sets the application bundle name for an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| int [OH_Rdb_SetModuleName](_r_d_b.md#oh_rdb_setmodulename) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, const char \*moduleName) | Sets the module name for an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| int [OH_Rdb_SetEncrypted](_r_d_b.md#oh_rdb_setencrypted) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, bool isEncrypted) | Sets whether to encrypt the database for an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| int [OH_Rdb_SetSecurityLevel](_r_d_b.md#oh_rdb_setsecuritylevel) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, int securityLevel) | Sets the database security level ([OH_Rdb_SecurityLevel](_r_d_b.md#oh_rdb_securitylevel)) for an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| int [OH_Rdb_SetArea](_r_d_b.md#oh_rdb_setarea) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, int area) | Sets the security area level ([Rdb_SecurityArea](_r_d_b.md#rdb_securityarea)) for an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| int [OH_Rdb_SetDbType](_r_d_b.md#oh_rdb_setdbtype) ([OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, int dbType) | Sets the database type ([Rdb_DBType](_r_d_b.md#rdb_dbtype)) for an [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) instance.|
| const int \* [OH_Rdb_GetSupportedDbType](_r_d_b.md#oh_rdb_getsupporteddbtype) (int \*typeCount) | Obtains the supported database type [Rdb_DBType](_r_d_b.md#rdb_dbtype).|
| [OH_Rdb_Store](_o_h___rdb___store.md) \* [OH_Rdb_CreateOrOpen](_r_d_b.md#oh_rdb_createoropen) (const [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config, int \*errCode) | Creates or opens an [OH_Rdb_Store](_o_h___rdb___store.md) instance based on the given [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2).|
| int [OH_Rdb_ExecuteByTrxId](_r_d_b.md#oh_rdb_executebytrxid) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, int64_t trxId, const char \*sql) | Executes an SQL statement that returns no value based on the specified transaction ID. This API supports vector stores.|
| int [OH_Rdb_BeginTransWithTrxId](_r_d_b.md#oh_rdb_begintranswithtrxid) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, int64_t \*trxId) | Begins a transaction. This API returns a transaction ID. This API supports vector stores.|
| int [OH_Rdb_RollBackByTrxId](_r_d_b.md#oh_rdb_rollbackbytrxid) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, int64_t trxId) | Rolls back the executed SQL statements based on the specified transaction ID. This API supports vector stores.|
| int [OH_Rdb_CommitByTrxId](_r_d_b.md#oh_rdb_commitbytrxid) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, int64_t trxId) | Commits the executed SQL statements based on the specified transaction ID. This API supports vector stores.|
| [OH_Rdb_CreateValueObject](_r_d_b.md#oh_rdb_createvalueobject) (void) | Creates an [OH_VObject](_o_h___v_object.md) instance.|
| [OH_Rdb_CreateValuesBucket](_r_d_b.md#oh_rdb_createvaluesbucket) (void) | Creates an [OH_VBucket](_o_h___v_bucket.md) instance.|
| [OH_Rdb_CreatePredicates](_r_d_b.md#oh_rdb_createpredicates) (const char \*table) | Creates an [OH_Predicates](_o_h___predicates.md) instance.|
| [OH_Rdb_GetOrOpen](_r_d_b.md#oh_rdb_getoropen) (const [OH_Rdb_Config](_o_h___rdb___config.md) \*config, int \*errCode) | Obtains an [OH_Rdb_Store](_o_h___rdb___store.md) instance for RDB store operations.|
| [OH_Rdb_CloseStore](_r_d_b.md#oh_rdb_closestore) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store) | Destroys an [OH_Rdb_Store](_o_h___rdb___store.md) object and reclaims the memory occupied by the object.|
| [OH_Rdb_DeleteStore](_r_d_b.md#oh_rdb_deletestore) (const [OH_Rdb_Config](_o_h___rdb___config.md) \*config) | Deletes an RDB store with the specified database file configuration.|
| int [OH_Rdb_DeleteStoreV2](_r_d_b.md#oh_rdb_deletestorev2) (const [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2) \*config) | Deletes an RDB store based on the given [OH_Rdb_ConfigV2](_r_d_b.md#oh_rdb_configv2). If a vector store is used, ensure that the vector store has been correctly closed before calling the API.|
| [OH_Rdb_Insert](_r_d_b.md#oh_rdb_insert) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*table, [OH_VBucket](_o_h___v_bucket.md) \*valuesBucket) | Inserts a row of data into a table.|
| [OH_Rdb_Update](_r_d_b.md#oh_rdb_update) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, [OH_VBucket](_o_h___v_bucket.md) \*valuesBucket, [OH_Predicates](_o_h___predicates.md) \*predicates) | Updates data in an RDB store based on specified conditions.|
| [OH_Rdb_Delete](_r_d_b.md#oh_rdb_delete) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, [OH_Predicates](_o_h___predicates.md) \*predicates) | Deletes data from an RDB store based on specified conditions.|
| [OH_Rdb_Query](_r_d_b.md#oh_rdb_query) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, [OH_Predicates](_o_h___predicates.md) \*predicates, const char \*const \*columnNames, int length) | Queries data in an RDB store.|
| [OH_Rdb_Execute](_r_d_b.md#oh_rdb_execute) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*sql) | Executes the SQL statement that returns no value.|
| [OH_Rdb_ExecuteQuery](_r_d_b.md#oh_rdb_executequery) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*sql) | Queries data in the database using the specified SQL statement. This API supports vector stores.|
| [OH_Rdb_BeginTransaction](_r_d_b.md#oh_rdb_begintransaction) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store) | Begins the transaction before executing the SQL statements.|
| [OH_Rdb_RollBack](_r_d_b.md#oh_rdb_rollback) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store) | Rolls back the SQL statements that have been executed.|
| [OH_Rdb_Commit](_r_d_b.md#oh_rdb_commit) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store) | Commits the executed SQL statements.|
| [OH_Rdb_Backup](_r_d_b.md#oh_rdb_backup) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*databasePath) | Backs up an RDB store using the backup file of the specified path. This API supports vector stores.|
| [OH_Rdb_Restore](_r_d_b.md#oh_rdb_restore) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*databasePath) | Restores a database from a specified database backup file. This API supports vector stores.|
| [OH_Rdb_GetVersion](_r_d_b.md#oh_rdb_getversion) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, int \*version) | Obtains the RDB store version.|
| [OH_Rdb_SetVersion](_r_d_b.md#oh_rdb_setversion) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, int version) | Sets the RDB store version.|
| [OH_Rdb_SetDistributedTables](_r_d_b.md#oh_rdb_setdistributedtables) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*tables[], uint32_t count, [Rdb_DistributedType](_r_d_b.md#rdb_distributedtype) type, const [Rdb_DistributedConfig](_rdb___distributed_config.md) \*config) | Sets distributed database tables.|
| [OH_Rdb_FindModifyTime](_r_d_b.md#oh_rdb_findmodifytime) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const char \*tableName, const char \*columnName, [OH_VObject](_o_h___v_object.md) \*values) | Obtains the last modification time of a table in an RDB store.|
| [OH_Rdb_Subscribe](_r_d_b.md#oh_rdb_subscribe) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, [Rdb_SubscribeType](_r_d_b.md#rdb_subscribetype) type, const [Rdb_DataObserver](_rdb___data_observer.md) \*observer) | Registers an observer for an RDB store. When data in the RDB store changes, a callback will be invoked to return the data changes.|
| [OH_Rdb_Unsubscribe](_r_d_b.md#oh_rdb_unsubscribe) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, [Rdb_SubscribeType](_r_d_b.md#rdb_subscribetype) type, const [Rdb_DataObserver](_rdb___data_observer.md) \*observer) | Unregisters the observer of the specified type.|
| [OH_Rdb_GetTableDetails](_r_d_b.md#oh_rdb_gettabledetails) ([Rdb_ProgressDetails](_rdb___progress_details.md) \*progress, int32_t version) | Obtains the device-cloud sync statistics of a table.|
| [OH_Rdb_CloudSync](_r_d_b.md#oh_rdb_cloudsync) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, [Rdb_SyncMode](_r_d_b.md#rdb_syncmode) mode, const char \*tables, int count, const [Rdb_ProgressObserver](_rdb___progress_observer.md) \*observer) | Performs device-cloud sync.|
| [OH_Rdb_SubscribeAutoSyncProgress](_r_d_b.md#oh_rdb_subscribeautosyncprogress) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const [Rdb_ProgressObserver](_rdb___progress_observer.md) \*observer) | Subscribes to the automatic sync progress of an RDB store. The registered callback will be invoked to return the automatic sync progress.|
| [OH_Rdb_UnsubscribeAutoSyncProgress](_r_d_b.md#oh_rdb_unsubscribeautosyncprogress) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, const [Rdb_ProgressObserver](_rdb___progress_observer.md) \*observer) | Unsubscribes from the automatic sync process of an RDB store.|
| int [OH_Rdb_LockRow](_r_d_b.md#oh_rdb_lockrow) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, [OH_Predicates](_o_h___predicates.md) \*predicates) | Locks data in an RDB store based on specified conditions. The locked data will be blocked from the device-cloud sync.|
| int [OH_Rdb_UnlockRow](_r_d_b.md#oh_rdb_unlockrow) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, [OH_Predicates](_o_h___predicates.md) \*predicates) | Unlocks data in an RDB store based on the specified conditions.|
| [OH_Cursor](_o_h___cursor.md) \* [OH_Rdb_QueryLockedRow](_r_d_b.md#oh_rdb_querylockedrow) ([OH_Rdb_Store](_o_h___rdb___store.md) \*store, [OH_Predicates](_o_h___predicates.md) \*predicates, const char \*const \*columnNames, int length) | Queries the locked data in an RDB store.|
