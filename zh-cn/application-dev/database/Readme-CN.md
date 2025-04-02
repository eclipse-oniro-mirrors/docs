# ArkData（方舟数据管理）

- [ArkData简介](data-mgmt-overview.md)
- 标准化数据定义<!--uniform-data-definition-->
  - [标准化数据定义概述](unified-data-definition-overview.md)
  - [标准化数据类型](uniform-data-type-descriptors.md)
  - [标准化数据结构](uniform-data-structure.md)
  - [Uniform Type Descriptor(UTD)预置类型列表](uniform-data-type-list.md)
- 应用数据持久化<!--app-data-persistence-->
  - [应用数据持久化概述](app-data-persistence-overview.md)
  - [通过用户首选项实现数据持久化](data-persistence-by-preferences.md)
  - [通过键值型数据库实现数据持久化](data-persistence-by-kv-store.md)
  - [通过关系型数据库实现数据持久化](data-persistence-by-rdb-store.md)
- 同应用跨设备数据同步（分布式）<!--distributed-data-sync-->
  - [同应用跨设备数据同步概述](sync-app-data-across-devices-overview.md)
  - [键值型数据库跨设备数据同步](data-sync-of-kv-store.md)
  - [关系型数据库跨设备数据同步](data-sync-of-rdb-store.md)
  - [分布式数据对象跨设备数据同步](data-sync-of-distributed-data-object.md)
- 数据可靠性与安全性<!--data-reliability-security-->
  - [数据可靠性与安全性概述](data-reliability-security-overview.md)
  - [数据库备份与恢复](data-backup-and-restore.md)
  - [数据库加密](data-encryption.md)
  - [基于设备分类和数据分级的访问控制](access-control-by-device-and-data-level.md)
  - [E类加密数据库的使用](encrypted_estore_guidelines.md)
- 跨应用数据共享<!--cross-app-data-share-->
  - [跨应用数据共享概述](data-share-overview.md)
  <!--Del-->
  - 一对多跨应用数据共享（仅对系统应用开放）<!--one-to-many-data-share-->
    - [通过DataShareExtensionAbility实现数据共享](share-data-by-datashareextensionability.md)
    - [通过数据管理服务实现数据共享静默访问](share-data-by-silent-access.md)
  <!--DelEnd-->
  - 多对多跨应用数据共享 <!--many-to-many-data-share-->
    - [通过标准化数据通路实现数据共享](unified-data-channels.md)
- 智慧化数据构建与检索<!--intelligence-data-->
  - [智慧化数据构建与检索概述](aip-data-intelligence-overview.md)
  - [应用数据向量化](aip-data-intelligence-embedding.md)
- [RelationalStore开发指导 (C/C++)](native-relational-store-guidelines.md)
- [UDMF开发指导 (C/C++)](native-unified-data-management-framework-guidelines.md)
- [通过用户首选项实现数据持久化 (C/C++)](preferences-guidelines.md)