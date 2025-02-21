# 应用及文件系统空间统计

在系统中，可能出现系统空间不够或者cacheDir等目录受系统配额限制等情况，需要应用开发者关注系统剩余空间，同时控制应用自身占用的空间大小。

## 接口说明

API的详细介绍请参见[ohos.file.statvfs](../reference/apis/js-apis-file-statvfs.md)、[ohos.file.storageStatistics](../reference/apis/js-apis-file-storage-statistics.md)。

**表1** 文件系统空间和应用空间统计

| 模块 | 接口名 | 功能 | 
| -------- | -------- | -------- |
| \@ohos.file.storageStatistics | getCurrentBundleStats | 获取当前应用的存储空间大小（单位为Byte）。 | 
| \@ohos.file.statvfs | getFreeSize | 获取指定文件系统的剩余空间大小（单位为Byte）。 | 
| \@ohos.file.statvfs | getTotalSize | 获取指定文件系统的总空间大小（单位为Byte）。 | 

**表2** 应用空间统计

| BundleStats属性 | 含义 | 统计路径 | 
| -------- | -------- | -------- |
| appSize | 应用安装文件大小（单位为Byte） | 应用安装文件保存在以下目录：<br/>/data/storage/el1/bundle | 
| cacheSize | 应用缓存文件大小（单位为Byte） | 应用的缓存文件保存在以下目录：<br/>/data/storage/el1/base/cache<br/>/data/storage/el1/base/haps/entry/cache<br/>/data/storage/el2/base/cache<br/>/data/storage/el2/base/haps/entry/cache | 
| dataSize | 应用文件存储大小（除应用安装文件和缓存文件）（单位为Byte） | 应用文件由本地文件、分布式文件以及数据库文件组成。<br/>本地文件保存在以下目录（注意缓存文件目录为以下目录的子目录）：<br/>/data/storage/el1/base<br/>/data/storage/el2/base<br/>分布式文件保存在以下目录：<br/>/data/storage/el2/distributedfiles<br/>数据库文件保存在以下目录：<br/>/data/storage/el1/database<br/>/data/storage/el2/database | 

## 开发示例

- 获取文件系统数据分区剩余空间大小。
    
  ```ts
  import statvfs from '@ohos.file.statvfs';
  
  let path = "/data";
  statvfs.getFreeSize(path, (err, number) => {
    if (err) {
      console.error(`Invoke getFreeSize failed, code is ${err.code}, message is ${err.message}`);
    } else {
      console.info(`Invoke getFreeSize succeeded, size is ${number}`);
    }
  });
  ```

- 获取当前应用的存储空间大小。
    
  ```ts
  import storageStatistics from "@ohos.file.storageStatistics";
  
  storageStatistics.getCurrentBundleStats((err, bundleStats) => {
    if (err) {
      console.error(`Invoke getCurrentBundleStats failed, code is ${err.code}, message is ${err.message}`);
    } else {
      console.info(`Invoke getCurrentBundleStats succeeded, appsize is ${bundleStats.appSize}`);
    }
  });
  ```
