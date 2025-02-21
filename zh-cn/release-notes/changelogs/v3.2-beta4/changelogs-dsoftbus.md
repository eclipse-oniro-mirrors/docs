# 软总线子系统Changelog

## IPC&RPC API支持异常处理方式和支持传入布尔值与数值选择同步或异步方式发送信息变更
1. 软总线IPC&RPC部分接口使用业务逻辑返回值表示错误信息，不符合OpenHarmony接口错误规范；
2. 支持传入布尔值选择同步或异步方式发送信息。
#### 变更影响

此版本兼容之前的应用开发，不需要适配，后续可调用新增接口支持以下两个变更：
1. 支持异常处理并返回错误码；
2. 提供通过布尔值或通过0与非0数字选择同步或异步发消息。

#### 关键接口/组件变更

为适配统一的API异常处理方式，对IPC&RPC相关接口进行废弃，并新增对应接口和方法。新增接口支持统一的错误码异常处理规范，功能上与原接口保持一致。
|  类名 | 废弃接口  | 新增替换类名  | 新增替代接口  |
| ------------ | ------------ | ------------ | ------------ |
| MessageParcel | static create(): MessageParcel | MessageSequence  | static create(): MessageSequence |
| MessageParcel | reclaim(): void | MessageSequence | reclaim(): void |
| MessageParcel | writeRemoteObject(object: IRemoteObject): boolean| MessageSequence |writeRemoteObject(object: IRemoteObject): void|
| MessageParcel | readRemoteObject(): IRemoteObject | MessageSequence | readRemoteObject(): IRemoteObject |
|  MessageParcel | writeInterfaceToken(token: string): boolean | MessageSequence | writeInterfaceToken(token: string): void |
|  MessageParcel | readInterfaceToken(): string | MessageSequence | readInterfaceToken(): string |
|  MessageParcel | getSize(): number | MessageSequence | getSize(): number |
|  MessageParcel | getCapacity(): number | MessageSequence | getCapacity(): number|
|  MessageParcel | setSize(size: number): boolean | MessageSequence | setCapacity(size: number): void |
|  MessageParcel | getReadableBytes(): number | MessageSequence | getReadableBytes(): number |
|  MessageParcel | getReadPosition(): number | MessageSequence | getReadPosition(): number |
|  MessageParcel | getWritePosition(): number | MessageSequence | getWritePosition(): number |
|  MessageParcel | rewindRead(pos: number): boolean | MessageSequence | rewindRead(pos: number): void |
|  MessageParcel | rewindWrite(pos: number): boolean | MessageSequence  | rewindWrite(pos: number): void |
|  MessageParcel | writeNoException(): void | MessageSequence | writeNoException(): void |
|  MessageParcel | readException(): void | MessageSequence  | readException(): void |
|  MessageParcel | writeByte(val: number): boolean | MessageSequence  | writeByte(val: number): void |
|  MessageParcel | writeShort(val: number): boolean | MessageSequence | writeShort(val: number): void |
|  MessageParcel | writeInt(val: number): boolean | MessageSequence | writeInt(val: number): void |
|  MessageParcel | writeLong(val: number): boolean | MessageSequence | writeLong(val: number): void |
|  MessageParcel | writeFloat(val: number): boolean | MessageSequence | writeFloat(val: number): void |
|  MessageParcel | writeDouble(val: number): boolean | MessageSequence | writeDouble(val: number): void |
|  MessageParcel | writeBoolean(val: boolean): boolean | MessageSequence | writeBoolean(val: boolean): void |
|  MessageParcel | writeChar(val: number): boolean | MessageSequence | writeChar(val: number): void |
|  MessageParcel | writeString(val: string): boolean | MessageSequence | writeString(val: string): void |
|  MessageParcel | writeSequenceable(val: Sequenceable): boolean | MessageSequence | writeParcelable(val: Parcelable): void |
|  MessageParcel | writeByteArray(byteArray: number[]): boolean | MessageSequence | writeByteArray(byteArray: number[]): void |
|  MessageParcel | writeShortArray(shortArray: number[]): boolean | MessageSequence | writeShortArray(shortArray: number[]): void |
|  MessageParcel | writeIntArray(intArray: number[]): boolean | MessageSequence | writeIntArray(intArray: number[]): void |
|  MessageParcel | writeLongArray(longArray: number[]): boolean | MessageSequence | writeLongArray(longArray: number[]): void |
|  MessageParcel | writeFloatArray(floatArray: number[]): boolean | MessageSequence | writeFloatArray(floatArray: number[]): void |
|  MessageParcel | writeDoubleArray(doubleArray: number[]): boolean | MessageSequence | writeDoubleArray(doubleArray: number[]): void |
|  MessageParcel | writeBooleanArray(booleanArray: boolean[]): boolean | MessageSequence | writeBooleanArray(booleanArray: boolean[]): void |
|  MessageParcel | writeCharArray(charArray: number[]): boolean | MessageSequence | writeCharArray(charArray: number[]): void |
|  MessageParcel | writeStringArray(stringArray: string[]): boolean | MessageSequence  | writeStringArray(stringArray: string[]): void |
|  MessageParcel | writeSequenceableArray(sequenceableArray: Sequenceable[]): boolean | MessageSequence  | writeParcelableArray(sequenceableArray: Parcelable[]): void |
|  MessageParcel | writeRemoteObjectArray(objectArray: IRemoteObject[]): boolean | MessageSequence  | writeRemoteObjectArray(objectArray: IRemoteObject[]): void |
|  MessageParcel | readByte(): number | MessageSequence | readByte(): number |
|  MessageParcel | readShort(): number | MessageSequence | readShort(): number |
|  MessageParcel | readLong(): number | MessageSequence | readLong(): number |
|  MessageParcel | readFloat(): number | MessageSequence | readFloat(): number |
|  MessageParcel | readDouble(): number | MessageSequence | readDouble(): number |
|  MessageParcel | readBoolean(): boolean | MessageSequence | readBoolean(): boolean |
|  MessageParcel | readChar(): number | MessageSequence | readChar(): number |
|  MessageParcel | readString(): string | MessageSequence | readString(): string |
|  MessageParcel | readSequenceable(dataIn: Sequenceable) : boolean | MessageSequence | readSequenceable(dataIn: Parcelable) : void |
|  MessageParcel | readByteArray(dataIn: number[]) : void | MessageSequence | readByteArray(dataIn: number[]) : void |
|  MessageParcel | readByteArray(): number[] | MessageSequence | readByteArray(): number[] |
|  MessageParcel | readShortArray(dataIn: number[]) : void | MessageSequence | readShortArray(dataIn: number[]) : void |
|  MessageParcel | readShortArray(): number[] | MessageSequence | readShortArray(): number[] |
|  MessageParcel | readIntArray(dataIn: number[]) : void | MessageSequence | readIntArray(dataIn: number[]) : void |
|  MessageParcel | readIntArray() : number[] | MessageSequence | readIntArray() : number[] |
|  MessageParcel | readLongArray(dataIn: number[]) : void | MessageSequence | readLongArray(dataIn: number[]) : void |
|  MessageParcel | readLongArray(): number[] | MessageSequence | readLongArray(): number[] |
|  MessageParcel | readFloatArray(dataIn: number[]) : void | MessageSequence | readFloatArray(dataIn: number[]) : void |
|  MessageParcel | readFloatArray(): number[] | MessageSequence | readFloatArray(): number[] |
|  MessageParcel | readDoubleArray(dataIn: number[]) : void | MessageSequence | readDoubleArray(dataIn: number[]) : void |
|  MessageParcel | readDoubleArray(): number[] | MessageSequence | readDoubleArray(): number[] |
|  MessageParcel | readBooleanArray(dataIn: boolean[]) : void | MessageSequence | readBooleanArray(dataIn: boolean[]) : void |
|  MessageParcel | readBooleanArray(): boolean[] | MessageSequence | readBooleanArray(): boolean[] |
|  MessageParcel | readCharArray(dataIn: number[]) : void | MessageSequence | readCharArray(dataIn: number[]) : void |
|  MessageParcel | readCharArray(): number[] | MessageSequence | readCharArray(): number[] |
|  MessageParcel | readStringArray(dataIn: string[]) : void | MessageSequence | readStringArray(dataIn: string[]) : void |
|  MessageParcel | readStringArray(): string[] | MessageSequence | readStringArray(): string[] |
| MessageParcel | readSequenceableArray(sequenceableArray: Sequenceable[]): void | MessageSequence | readSequenceableArray(sequenceableArray: Parcelable[]): void |
| MessageParcel | readRemoteObjectArray(objects: IRemoteObject[]): void | MessageSequence | readRemoteObjectArray(objects: IRemoteObject[]): void |
| MessageParcel | readRemoteObjectArray(): IRemoteObject[] | MessageSequence | readRemoteObjectArray(): IRemoteObject[] |
| MessageParcel | static closeFileDescriptor(fd: number): void | MessageSequence | static closeFileDescriptor(fd: number): void |
| MessageParcel | static dupFileDescriptor(fd: number) :number | MessageSequence | static dupFileDescriptor(fd: number) :number |
| MessageParcel | containFileDescriptors(): boolean | MessageSequence | containFileDescriptors(): boolean |
| MessageParcel | writeFileDescriptor(fd: number): boolean | MessageSequence | writeFileDescriptor(fd: number): void |
| MessageParcel | readFileDescriptor(): number | MessageSequence | readFileDescriptor(): number |
| MessageParcel | writeAshmem(ashmem: Ashmem): boolean | MessageSequence | writeAshmem(ashmem: Ashmem): void |
| MessageParcel | readAshmem(): Ashmem | MessageSequence | readAshmem(): Ashmem |
| MessageParcel | writeRawData(rawData: number[], size: number): boolean | MessageSequence | writeRawData(rawData: number[], size: number): void |
| MessageParcel | readRawData(size: number): number[] | MessageSequence | readRawData(size: number): number[] |
| Sequenceable | marshalling(dataOut: MessageParcel): boolean | Parcelable | marshalling(dataOut: MessageSequence): boolean |
| Sequenceable | unmarshalling(dataIn: MessageParcel) : boolean | Parcelable | unmarshalling(dataIn: MessageSequence) : boolean |
| SendRequestResult | errCode: number | RequestResult | errCode: number |
| SendRequestResult | code: number | RequestResult | code: number |
| SendRequestResult | data: MessageParcel | RequestResult | data: MessageSequence |
| SendRequestResult | reply: MessageParcel | RequestResult | reply: MessageSequence |
| IRemoteObject | queryLocalInterface(descriptor: string): IRemoteBroker | NA | getLocalInterface(descriptor: string): IRemoteBroker |
| IRemoteObject | getInterfaceDescriptor(): string | NA | getDescriptor(): string |
| IRemoteObject | addDeathRecipient(recipient: DeathRecipient, flags: number): boolean | NA | registerDeathRecipient(recipient: DeathRecipient, flags: number): void |
| IRemoteObject | removeDeathRecipient(recipient: DeathRecipient, flags: number): boolean | NA | unregisterDeathRecipient(recipient: DeathRecipient, flags: number): void |
| IRemoteObject | NA | NA | sendMessageRequest(code: number, data: MessageSequence, reply: MessageSequence, options: MessageOption): Promise<RequestResult> |
| IRemoteObject | sendRequest(code: number, data: MessageParcel, reply: MessageParcel, options: MessageOption, callback: AsyncCallback<SendRequestResult>): void | NA | sendMessageRequest(code: number, data: MessageSequence, reply: MessageSequence, options: MessageOption,callback: AsyncCallback<RequestResult>): void |
| MessageOption | NA | NA | isAsync(): boolean |
| MessageOption | NA | NA | setAsync(async: boolean): void |
| MessageOption | NA | NA | constructor(async?: boolean) |
| RemoteObject | queryLocalInterface(descriptor: string): IRemoteBroker | NA | getLocalInterface(descriptor: string): IRemoteBroker |
| RemoteObject | attachLocalInterface(localInterface: IRemoteBroker, descriptor: string): void  | NA | modifyLocalInterface(localInterface: IRemoteBroker, descriptor: string): void |
| RemoteObject | getInterfaceDescriptor(): string | NA | getDescriptor(): string |
| RemoteObject | onRemoteRequestEx(code : number, data : MessageParcel, reply: MessageParcel, options : MessageOption): boolean&nbsp;\|&nbsp;Promise<boolean> | NA | onRemoteMessageRequest(code: number, data: MessageSequence, reply: MessageSequence, options: MessageOption): boolean&nbsp;\|&nbsp;Promise<boolean> |
| RemoteObject | sendRequest(code: number, data: MessageParcel, reply: MessageParcel, options: MessageOption): Promise<SendRequestResult> | NA | sendMessageRequest(code: number, data: MessageSequence, reply: MessageSequence, options: MessageOption): Promise<RequestResult> |
| RemoteObject | sendRequest(code: number, data: MessageParcel, reply: MessageParcel, options: MessageOption, callback: AsyncCallback<SendRequestResult>): void | NA | sendMessageRequest(code: number, data: MessageSequence, reply: MessageSequence, options: MessageOption, callback: AsyncCallback<RequestResult>): void |
| RemoteProxy | queryLocalInterface(interface: string): IRemoteBroker | NA | getLocalInterface(descriptor: string): IRemoteBroker |
| RemoteProxy | getInterfaceDescriptor(): string | NA | getDescriptor(): string |
| RemoteProxy | addDeathRecipient(recipient: DeathRecipient, flags: number): boolean | NA | registerDeathRecipient(recipient: DeathRecipient, flags: number): void |
| RemoteProxy | removeDeathRecipient(recipient: DeathRecipient, flags: number): boolean | NA | unregisterDeathRecipient(recipient: DeathRecipient, flags: number): void |
| RemoteProxy | NA | NA | sendMessageRequest(code: number, data: MessageSequence, reply: MessageSequence, options: MessageOption): Promise<RequestResult> |
| RemoteProxy | sendRequest(code: number, data: MessageParcel, reply: MessageParcel, options: MessageOption, callback: AsyncCallback<SendRequestResult>): void | NA | sendMessageRequest(code: number, data: MessageSequence, reply: MessageSequence, options: MessageOption, callback: AsyncCallback<RequestResult>): void |
| IPCSkeleton | static flushCommands(object: IRemoteObject): number | NA | static flushCmdBuffer(object: IRemoteObject): void |
| IPCSkeleton | static setCallingIdentity(identity: string): boolean | NA | static restoreCallingIdentity(identity: string): void |
| Ashmem | static createAshmem(name: string, size: number): Ashmem | NA | static create(name: string, size: number): Ashmem |
| Ashmem  | static createAshmemFromExisting(ashmem: Ashmem): Ashmem | NA | static create(ashmem: Ashmem): Ashmem |
| Ashmem  | mapAshmem(mapType: number): boolean | NA | mapTypedAshmem(mapType: number): void |
| Ashmem  | mapReadAndWriteAshmem(): boolean | NA | mapReadWriteAshmem(): void |
| Ashmem  | mapReadOnlyAshmem(): boolean | NA | mapReadonlyAshmem(): void |
| Ashmem  | setProtection(protectionType: number): boolean | NA | setProtectionType(protectionType: number): void |
| Ashmem  | writeToAshmem(buf: number[], size: number, offset: number): boolean | NA | writeAshmem(buf: number[], size: number, offset: number): void |
| Ashmem  | readFromAshmem(size: number, offset: number): number[] | NA | readAshmem(size: number, offset: number): number[] |

#### 适配指导

新增的接口以抛异常的方式返回错误码及对应的错误信息，以MessageParcel中的create接口为例，使用示例代码如下：
```js
import rpc from '@ohos.rpc'

try {
    var data = rpc.MessageParcel.create();
    data.reclaim();
} catch (error) {
    console.info("create meassageParcel failed, errorCode = " + error.errCode);
    console.info("create meassageParcel failed, errorMessage = " + error.errorMessage);
}
```
更多接口的示例代码可参考[RPC通信API文档](../../../application-dev/reference/apis/js-apis-rpc.md)。