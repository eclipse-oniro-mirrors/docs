| 操作 | 旧版本 | 新版本 | d.ts文件 |
| ---- | ------ | ------ | -------- |
|新增|NA|模块名: ohos.systemParameterEnhance<br>类名: systemParameterEnhance|@ohos.systemParameterEnhance.d.ts|
|新增|NA|模块名: ohos.systemParameterEnhance<br>类名: systemParameterEnhance<br>方法 or 属性: function getSync(key: string, def?: string): string;|@ohos.systemParameterEnhance.d.ts|
|新增|NA|模块名: ohos.systemParameterEnhance<br>类名: systemParameterEnhance<br>方法 or 属性: function get(key: string, callback: AsyncCallback\<string>): void;|@ohos.systemParameterEnhance.d.ts|
|新增|NA|模块名: ohos.systemParameterEnhance<br>类名: systemParameterEnhance<br>方法 or 属性: function get(key: string, def: string, callback: AsyncCallback\<string>): void;|@ohos.systemParameterEnhance.d.ts|
|新增|NA|模块名: ohos.systemParameterEnhance<br>类名: systemParameterEnhance<br>方法 or 属性: function get(key: string, def?: string): Promise\<string>;|@ohos.systemParameterEnhance.d.ts|
|新增|NA|模块名: ohos.systemParameterEnhance<br>类名: systemParameterEnhance<br>方法 or 属性: function setSync(key: string, value: string): void;|@ohos.systemParameterEnhance.d.ts|
|新增|NA|模块名: ohos.systemParameterEnhance<br>类名: systemParameterEnhance<br>方法 or 属性: function set(key: string, value: string, callback: AsyncCallback\<void>): void;|@ohos.systemParameterEnhance.d.ts|
|新增|NA|模块名: ohos.systemParameterEnhance<br>类名: systemParameterEnhance<br>方法 or 属性: function set(key: string, value: string): Promise\<void>;|@ohos.systemParameterEnhance.d.ts|
|废弃版本有变化|类名：deviceInfo<br>方法 or 属性：const hardwareProfile: string;<br>废弃版本：N/A|类名：deviceInfo<br>方法 or 属性：const hardwareProfile: string;<br>废弃版本：9<br>代替接口：N/A|@ohos.deviceInfo.d.ts|
|废弃版本有变化|类名：Device<br>方法 or 属性：static getInfo(options?: GetDeviceOptions): void;<br>废弃版本：N/A|类名：Device<br>方法 or 属性：static getInfo(options?: GetDeviceOptions): void;<br>废弃版本：6<br>代替接口：N/A|@system.device.d.ts|
|新增(权限)|类名：deviceInfo<br>方法 or 属性：const serial: string;<br>权限:N/A|类名：deviceInfo<br>方法 or 属性：const serial: string;<br>权限:ohos.permission.sec.ACCESS_UDID|@ohos.deviceInfo.d.ts|
|新增(权限)|类名：deviceInfo<br>方法 or 属性：const udid: string;<br>权限:N/A|类名：deviceInfo<br>方法 or 属性：const udid: string;<br>权限:ohos.permission.sec.ACCESS_UDID|@ohos.deviceInfo.d.ts|
