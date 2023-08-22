| 操作 | 旧版本 | 新版本 | d.ts文件 |
| ---- | ------ | ------ | -------- |
|新增|NA|类名：settings;<br>方法or属性：function getValue(context: Context, name: string, callback: AsyncCallback\<string>): void;|@ohos.settings.d.ts|
|新增|NA|类名：settings;<br>方法or属性：function getValue(context: Context, name: string): Promise\<string>;|@ohos.settings.d.ts|
|新增|NA|类名：settings;<br>方法or属性：function setValue(context: Context, name: string, value: string, callback: AsyncCallback\<boolean>): void;|@ohos.settings.d.ts|
|新增|NA|类名：settings;<br>方法or属性：function setValue(context: Context, name: string, value: string): Promise\<boolean>;|@ohos.settings.d.ts|
|新增|NA|类名：settings;<br>方法or属性：function getValueSync(context: Context, name: string, defValue: string): string;|@ohos.settings.d.ts|
|新增|NA|类名：settings;<br>方法or属性：function setValueSync(context: Context, name: string, value: string): boolean;|@ohos.settings.d.ts|
|废弃版本有变化|类名：settings;<br>方法or属性：function getURI(name: string): Promise\<object>;<br>旧版本信息：|类名：settings;<br>方法or属性：function getURI(name: string): Promise\<object>;<br>新版本信息：9<br>代替接口：|@ohos.settings.d.ts|
|废弃版本有变化|类名：settings;<br>方法or属性：function getValue(dataAbilityHelper: DataAbilityHelper, name: string): Promise\<object>;<br>旧版本信息：|类名：settings;<br>方法or属性：function getValue(dataAbilityHelper: DataAbilityHelper, name: string): Promise\<object>;<br>新版本信息：9<br>代替接口： ohos.settings#getValue|@ohos.settings.d.ts|
|废弃版本有变化|类名：settings;<br>方法or属性：function setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object): Promise\<boolean>;<br>旧版本信息：|类名：settings;<br>方法or属性：function setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object): Promise\<boolean>;<br>新版本信息：9<br>代替接口： ohos.settings#setValue|@ohos.settings.d.ts|
|新增(错误码)|类名：call;<br>方法or属性：function makeCall(phoneNumber: string): Promise\<void>;<br>旧版本信息：|类名：call;<br>方法or属性：function makeCall(phoneNumber: string): Promise\<void>;<br>新版本信息：401,8300001,8300002,8300003,8300999|@ohos.telephony.call.d.ts|
|访问级别有变化|类名：settings;<br>方法or属性：function setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object): Promise\<boolean>;<br>旧版本信息：|类名：settings;<br>方法or属性：function setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object): Promise\<boolean>;<br>新版本信息：systemapi|@ohos.settings.d.ts|
|model有变化|类名：settings;<br>方法or属性：function getValue(dataAbilityHelper: DataAbilityHelper, name: string, callback: AsyncCallback\<object>): void;<br>旧版本信息：FAModelOnly|类名：settings;<br>方法or属性：function getValue(dataAbilityHelper: DataAbilityHelper, name: string, callback: AsyncCallback\<object>): void;<br>新版本信息：famodelonly|@ohos.settings.d.ts|
|model有变化|类名：settings;<br>方法or属性：function getValue(dataAbilityHelper: DataAbilityHelper, name: string): Promise\<object>;<br>旧版本信息：|类名：settings;<br>方法or属性：function getValue(dataAbilityHelper: DataAbilityHelper, name: string): Promise\<object>;<br>新版本信息：famodelonly|@ohos.settings.d.ts|
|model有变化|类名：settings;<br>方法or属性：function setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object, callback: AsyncCallback\<boolean>): void;<br>旧版本信息：FAModelOnly|类名：settings;<br>方法or属性：function setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object, callback: AsyncCallback\<boolean>): void;<br>新版本信息：famodelonly|@ohos.settings.d.ts|
|model有变化|类名：settings;<br>方法or属性：function setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object): Promise\<boolean>;<br>旧版本信息：|类名：settings;<br>方法or属性：function setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object): Promise\<boolean>;<br>新版本信息：famodelonly|@ohos.settings.d.ts|
|model有变化|类名：settings;<br>方法or属性：function getValueSync(dataAbilityHelper: DataAbilityHelper, name: string, defValue: string): string;<br>旧版本信息：FAModelOnly|类名：settings;<br>方法or属性：function getValueSync(dataAbilityHelper: DataAbilityHelper, name: string, defValue: string): string;<br>新版本信息：famodelonly|@ohos.settings.d.ts|
|model有变化|类名：settings;<br>方法or属性：function setValueSync(dataAbilityHelper: DataAbilityHelper, name: string, value: string): boolean;<br>旧版本信息：FAModelOnly|类名：settings;<br>方法or属性：function setValueSync(dataAbilityHelper: DataAbilityHelper, name: string, value: string): boolean;<br>新版本信息：famodelonly|@ohos.settings.d.ts|