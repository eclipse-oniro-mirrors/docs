| 操作 | 旧版本 | 新版本 | d.ts文件 |
| ---- | ------ | ------ | -------- |
|新增|NA|类名：call<br>方法or属性：function dialCall(phoneNumber: string, callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function dialCall(phoneNumber: string, options: DialCallOptions, callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function dialCall(phoneNumber: string, options?: DialCallOptions): Promise\<void>;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function answerCall(callId: number, callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function answerCall(callId?: number): Promise\<void>;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function answerCall(callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function hangUpCall(callId: number, callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function hangUpCall(callId?: number): Promise\<void>;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function hangUpCall(callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function rejectCall(callId: number, callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function rejectCall(callId: number, options: RejectMessageOptions, callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function rejectCall(callId?: number, options?: RejectMessageOptions): Promise\<void>;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function rejectCall(callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function rejectCall(options: RejectMessageOptions, callback: AsyncCallback\<void>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function on(type: 'mmiCodeResult', callback: Callback\<MmiCodeResults>): void;|@ohos.telephony.call.d.ts|
|新增|NA|类名：call<br>方法or属性：function off(type: 'mmiCodeResult', callback?: Callback\<MmiCodeResults>): void;|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: AudioDevice<br>方法 or 属性：DEVICE_EARPIECE|@ohos.telephony.call.d.ts|
|新增|NA|类名：AudioDevice<br>方法or属性：DEVICE_EARPIECE|@ohos.telephony.call.d.ts|
|新增|NA|类名：CallTransferInfo<br>方法or属性：startHour?: number;|@ohos.telephony.call.d.ts|
|新增|NA|类名：CallTransferInfo<br>方法or属性：startMinute?: number;|@ohos.telephony.call.d.ts|
|新增|NA|类名：CallTransferInfo<br>方法or属性：endHour?: number;|@ohos.telephony.call.d.ts|
|新增|NA|类名：CallTransferInfo<br>方法or属性：endMinute?: number;|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DialCallOptions|@ohos.telephony.call.d.ts|
|新增|NA|类名：DialCallOptions<br>方法or属性：|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DialCallOptions<br>方法 or 属性：accountId?: number;|@ohos.telephony.call.d.ts|
|新增|NA|类名：DialCallOptions<br>方法or属性：accountId?: number;|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DialCallOptions<br>方法 or 属性：videoState?: VideoStateType;|@ohos.telephony.call.d.ts|
|新增|NA|类名：DialCallOptions<br>方法or属性：videoState?: VideoStateType;|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DialCallOptions<br>方法 or 属性：dialScene?: DialScene;|@ohos.telephony.call.d.ts|
|新增|NA|类名：DialCallOptions<br>方法or属性：dialScene?: DialScene;|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DialCallOptions<br>方法 or 属性：dialType?: DialType;|@ohos.telephony.call.d.ts|
|新增|NA|类名：DialCallOptions<br>方法or属性：dialType?: DialType;|@ohos.telephony.call.d.ts|
|新增|NA|类名：CallTransferResult<br>方法or属性：startHour: number;|@ohos.telephony.call.d.ts|
|新增|NA|类名：CallTransferResult<br>方法or属性：startMinute: number;|@ohos.telephony.call.d.ts|
|新增|NA|类名：CallTransferResult<br>方法or属性：endHour: number;|@ohos.telephony.call.d.ts|
|新增|NA|类名：CallTransferResult<br>方法or属性：endMinute: number;|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: AudioDeviceOptions|@ohos.telephony.call.d.ts|
|新增|NA|类名：AudioDeviceOptions<br>方法or属性：|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: AudioDeviceOptions<br>方法 or 属性：bluetoothAddress?: string;|@ohos.telephony.call.d.ts|
|新增|NA|类名：AudioDeviceOptions<br>方法or属性：bluetoothAddress?: string;|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: MmiCodeResults|@ohos.telephony.call.d.ts|
|新增|NA|类名：MmiCodeResults<br>方法or属性：|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: MmiCodeResults<br>方法 or 属性：result: MmiCodeResult;|@ohos.telephony.call.d.ts|
|新增|NA|类名：MmiCodeResults<br>方法or属性：result: MmiCodeResult;|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: MmiCodeResults<br>方法 or 属性：message: string;|@ohos.telephony.call.d.ts|
|新增|NA|类名：MmiCodeResults<br>方法or属性：message: string;|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: MmiCodeResult|@ohos.telephony.call.d.ts|
|新增|NA|类名：MmiCodeResult<br>方法or属性：|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: MmiCodeResult<br>方法 or 属性：MMI_CODE_SUCCESS = 0|@ohos.telephony.call.d.ts|
|新增|NA|类名：MmiCodeResult<br>方法or属性：MMI_CODE_SUCCESS = 0|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: MmiCodeResult<br>方法 or 属性：MMI_CODE_FAILED = 1|@ohos.telephony.call.d.ts|
|新增|NA|类名：MmiCodeResult<br>方法or属性：MMI_CODE_FAILED = 1|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：UNASSIGNED_NUMBER = 1|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：UNASSIGNED_NUMBER = 1|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NO_ROUTE_TO_DESTINATION = 3|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NO_ROUTE_TO_DESTINATION = 3|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：CHANNEL_UNACCEPTABLE = 6|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：CHANNEL_UNACCEPTABLE = 6|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：OPERATOR_DETERMINED_BARRING = 8|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：OPERATOR_DETERMINED_BARRING = 8|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：CALL_COMPLETED_ELSEWHERE = 13|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：CALL_COMPLETED_ELSEWHERE = 13|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NORMAL_CALL_CLEARING = 16|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NORMAL_CALL_CLEARING = 16|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：USER_BUSY = 17|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：USER_BUSY = 17|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NO_USER_RESPONDING = 18|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NO_USER_RESPONDING = 18|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：USER_ALERTING_NO_ANSWER = 19|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：USER_ALERTING_NO_ANSWER = 19|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：CALL_REJECTED = 21|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：CALL_REJECTED = 21|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NUMBER_CHANGED = 22|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NUMBER_CHANGED = 22|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：CALL_REJECTED_DUE_TO_FEATURE_AT_THE_DESTINATION = 24|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：CALL_REJECTED_DUE_TO_FEATURE_AT_THE_DESTINATION = 24|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：FAILED_PRE_EMPTION = 25|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：FAILED_PRE_EMPTION = 25|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NON_SELECTED_USER_CLEARING = 26|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NON_SELECTED_USER_CLEARING = 26|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：DESTINATION_OUT_OF_ORDER = 27|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：DESTINATION_OUT_OF_ORDER = 27|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：INVALID_NUMBER_FORMAT = 28|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：INVALID_NUMBER_FORMAT = 28|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：FACILITY_REJECTED = 29|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：FACILITY_REJECTED = 29|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RESPONSE_TO_STATUS_ENQUIRY = 30|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RESPONSE_TO_STATUS_ENQUIRY = 30|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NORMAL_UNSPECIFIED = 31|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NORMAL_UNSPECIFIED = 31|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NO_CIRCUIT_CHANNEL_AVAILABLE = 34|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NO_CIRCUIT_CHANNEL_AVAILABLE = 34|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NETWORK_OUT_OF_ORDER = 38|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NETWORK_OUT_OF_ORDER = 38|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：TEMPORARY_FAILURE = 41|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：TEMPORARY_FAILURE = 41|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：SWITCHING_EQUIPMENT_CONGESTION = 42|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：SWITCHING_EQUIPMENT_CONGESTION = 42|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：ACCESS_INFORMATION_DISCARDED = 43|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：ACCESS_INFORMATION_DISCARDED = 43|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：REQUEST_CIRCUIT_CHANNEL_NOT_AVAILABLE = 44|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：REQUEST_CIRCUIT_CHANNEL_NOT_AVAILABLE = 44|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RESOURCES_UNAVAILABLE_UNSPECIFIED = 47|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RESOURCES_UNAVAILABLE_UNSPECIFIED = 47|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：QUALITY_OF_SERVICE_UNAVAILABLE = 49|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：QUALITY_OF_SERVICE_UNAVAILABLE = 49|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：REQUESTED_FACILITY_NOT_SUBSCRIBED = 50|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：REQUESTED_FACILITY_NOT_SUBSCRIBED = 50|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：INCOMING_CALLS_BARRED_WITHIN_THE_CUG = 55|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：INCOMING_CALLS_BARRED_WITHIN_THE_CUG = 55|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：BEARER_CAPABILITY_NOT_AUTHORIZED = 57|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：BEARER_CAPABILITY_NOT_AUTHORIZED = 57|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：BEARER_CAPABILITY_NOT_PRESENTLY_AVAILABLE = 58|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：BEARER_CAPABILITY_NOT_PRESENTLY_AVAILABLE = 58|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：SERVICE_OR_OPTION_NOT_AVAILABLE_UNSPECIFIED = 63|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：SERVICE_OR_OPTION_NOT_AVAILABLE_UNSPECIFIED = 63|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：BEARER_SERVICE_NOT_IMPLEMENTED = 65|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：BEARER_SERVICE_NOT_IMPLEMENTED = 65|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：ACM_EQUALTO_OR_GREATER_THAN_THE_MAXIMUM_VALUE = 68|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：ACM_EQUALTO_OR_GREATER_THAN_THE_MAXIMUM_VALUE = 68|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：REQUESTED_FACILITY_NOT_IMPLEMENTED = 69|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：REQUESTED_FACILITY_NOT_IMPLEMENTED = 69|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：ONLY_RESTRICTED_DIGITAL_INFO_BEARER_CAPABILITY_IS_AVAILABLE = 70|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：ONLY_RESTRICTED_DIGITAL_INFO_BEARER_CAPABILITY_IS_AVAILABLE = 70|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：SERVICE_OR_OPTION_NOT_IMPLEMENTED_UNSPECIFIED = 79|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：SERVICE_OR_OPTION_NOT_IMPLEMENTED_UNSPECIFIED = 79|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：INVALID_TRANSACTION_IDENTIFIER_VALUE = 81|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：INVALID_TRANSACTION_IDENTIFIER_VALUE = 81|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：USER_NOT_MEMBER_OF_CUG = 87|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：USER_NOT_MEMBER_OF_CUG = 87|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：INCOMPATIBLE_DESTINATION = 88|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：INCOMPATIBLE_DESTINATION = 88|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：INVALID_TRANSIT_NETWORK_SELECTION = 91|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：INVALID_TRANSIT_NETWORK_SELECTION = 91|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：SEMANTICALLY_INCORRECT_MESSAGE = 95|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：SEMANTICALLY_INCORRECT_MESSAGE = 95|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：INVALID_MANDATORY_INFORMATION = 96|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：INVALID_MANDATORY_INFORMATION = 96|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：MESSAGE_TYPE_NON_EXISTENT_OR_NOT_IMPLEMENTED = 97|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：MESSAGE_TYPE_NON_EXISTENT_OR_NOT_IMPLEMENTED = 97|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：MESSAGE_TYPE_NOT_COMPATIBLE_WITH_PROTOCOL_STATE = 98|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：MESSAGE_TYPE_NOT_COMPATIBLE_WITH_PROTOCOL_STATE = 98|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：INFORMATION_ELEMENT_NON_EXISTENT_OR_NOT_IMPLEMENTED = 99|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：INFORMATION_ELEMENT_NON_EXISTENT_OR_NOT_IMPLEMENTED = 99|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：CONDITIONAL_IE_ERROR = 100|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：CONDITIONAL_IE_ERROR = 100|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：MESSAGE_NOT_COMPATIBLE_WITH_PROTOCOL_STATE = 101|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：MESSAGE_NOT_COMPATIBLE_WITH_PROTOCOL_STATE = 101|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RECOVERY_ON_TIMER_EXPIRED = 102|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RECOVERY_ON_TIMER_EXPIRED = 102|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：PROTOCOL_ERROR_UNSPECIFIED = 111|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：PROTOCOL_ERROR_UNSPECIFIED = 111|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：INTERWORKING_UNSPECIFIED = 127|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：INTERWORKING_UNSPECIFIED = 127|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：CALL_BARRED = 240|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：CALL_BARRED = 240|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：FDN_BLOCKED = 241|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：FDN_BLOCKED = 241|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：IMSI_UNKNOWN_IN_VLR = 242|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：IMSI_UNKNOWN_IN_VLR = 242|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：IMEI_NOT_ACCEPTED = 243|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：IMEI_NOT_ACCEPTED = 243|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：DIAL_MODIFIED_TO_USSD = 244|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：DIAL_MODIFIED_TO_USSD = 244|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：DIAL_MODIFIED_TO_SS = 245|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：DIAL_MODIFIED_TO_SS = 245|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：DIAL_MODIFIED_TO_DIAL = 246|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：DIAL_MODIFIED_TO_DIAL = 246|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RADIO_OFF = 247|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RADIO_OFF = 247|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：OUT_OF_SERVICE = 248|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：OUT_OF_SERVICE = 248|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NO_VALID_SIM = 249|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NO_VALID_SIM = 249|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RADIO_INTERNAL_ERROR = 250|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RADIO_INTERNAL_ERROR = 250|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NETWORK_RESP_TIMEOUT = 251|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NETWORK_RESP_TIMEOUT = 251|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NETWORK_REJECT = 252|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NETWORK_REJECT = 252|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RADIO_ACCESS_FAILURE = 253|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RADIO_ACCESS_FAILURE = 253|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RADIO_LINK_FAILURE = 254|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RADIO_LINK_FAILURE = 254|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RADIO_LINK_LOST = 255|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RADIO_LINK_LOST = 255|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RADIO_UPLINK_FAILURE = 256|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RADIO_UPLINK_FAILURE = 256|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RADIO_SETUP_FAILURE = 257|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RADIO_SETUP_FAILURE = 257|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RADIO_RELEASE_NORMAL = 258|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RADIO_RELEASE_NORMAL = 258|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：RADIO_RELEASE_ABNORMAL = 259|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：RADIO_RELEASE_ABNORMAL = 259|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：ACCESS_CLASS_BLOCKED = 260|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：ACCESS_CLASS_BLOCKED = 260|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：NETWORK_DETACH = 261|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：NETWORK_DETACH = 261|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：INVALID_PARAMETER = 1025|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：INVALID_PARAMETER = 1025|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：SIM_NOT_EXIT = 1026|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：SIM_NOT_EXIT = 1026|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：SIM_PIN_NEED = 1027|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：SIM_PIN_NEED = 1027|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：CALL_NOT_ALLOW = 1029|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：CALL_NOT_ALLOW = 1029|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：SIM_INVALID = 1045|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：SIM_INVALID = 1045|@ohos.telephony.call.d.ts|
|新增|NA|模块名: ohos.telephony.call<br>类名: DisconnectedReason<br>方法 or 属性：UNKNOWN = 1279|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedReason<br>方法or属性：UNKNOWN = 1279|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedDetails<br>方法or属性：reason: DisconnectedReason;|@ohos.telephony.call.d.ts|
|新增|NA|类名：DisconnectedDetails<br>方法or属性：message: string;|@ohos.telephony.call.d.ts|
|新增|NA|类名：data<br>方法or属性：function getDefaultCellularDataSlotIdSync(): number;|@ohos.telephony.data.d.ts|
|新增|NA|类名：radio<br>方法or属性：function isNRSupported(): boolean;|@ohos.telephony.radio.d.ts|
|新增|NA|类名：radio<br>方法or属性：function isNRSupported(slotId: number): boolean;|@ohos.telephony.radio.d.ts|
|新增|NA|类名：radio<br>方法or属性：function getImsRegInfo(slotId: number, imsType: ImsServiceType, callback: AsyncCallback\<ImsRegInfo>): void;|@ohos.telephony.radio.d.ts|
|新增|NA|类名：radio<br>方法or属性：function getImsRegInfo(slotId: number, imsType: ImsServiceType): Promise\<ImsRegInfo>;|@ohos.telephony.radio.d.ts|
|新增|NA|类名：radio<br>方法or属性：function on(type: 'imsRegStateChange', slotId: number, imsType: ImsServiceType, callback: Callback\<ImsRegInfo>): void;|@ohos.telephony.radio.d.ts|
|新增|NA|类名：radio<br>方法or属性：function off(type: 'imsRegStateChange', slotId: number, imsType: ImsServiceType, callback?: Callback\<ImsRegInfo>): void;|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: SignalInformation<br>方法 or 属性：dBm: number;|@ohos.telephony.radio.d.ts|
|新增|NA|类名：SignalInformation<br>方法or属性：dBm: number;|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegState|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegState<br>方法or属性：|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegState<br>方法 or 属性：IMS_UNREGISTERED|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegState<br>方法or属性：IMS_UNREGISTERED|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegState<br>方法 or 属性：IMS_REGISTERED|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegState<br>方法or属性：IMS_REGISTERED|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegTech|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegTech<br>方法or属性：|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegTech<br>方法 or 属性：REGISTRATION_TECH_NONE|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegTech<br>方法or属性：REGISTRATION_TECH_NONE|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegTech<br>方法 or 属性：REGISTRATION_TECH_LTE|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegTech<br>方法or属性：REGISTRATION_TECH_LTE|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegTech<br>方法 or 属性：REGISTRATION_TECH_IWLAN|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegTech<br>方法or属性：REGISTRATION_TECH_IWLAN|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegTech<br>方法 or 属性：REGISTRATION_TECH_NR|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegTech<br>方法or属性：REGISTRATION_TECH_NR|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegInfo|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegInfo<br>方法or属性：|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegInfo<br>方法 or 属性：imsRegState: ImsRegState;|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegInfo<br>方法or属性：imsRegState: ImsRegState;|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsRegInfo<br>方法 or 属性：imsRegTech: ImsRegTech;|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsRegInfo<br>方法or属性：imsRegTech: ImsRegTech;|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsServiceType|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsServiceType<br>方法or属性：|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsServiceType<br>方法 or 属性：TYPE_VOICE|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsServiceType<br>方法or属性：TYPE_VOICE|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsServiceType<br>方法 or 属性：TYPE_VIDEO|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsServiceType<br>方法or属性：TYPE_VIDEO|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsServiceType<br>方法 or 属性：TYPE_UT|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsServiceType<br>方法or属性：TYPE_UT|@ohos.telephony.radio.d.ts|
|新增|NA|模块名: ohos.telephony.radio<br>类名: ImsServiceType<br>方法 or 属性：TYPE_SMS|@ohos.telephony.radio.d.ts|
|新增|NA|类名：ImsServiceType<br>方法or属性：TYPE_SMS|@ohos.telephony.radio.d.ts|
|新增|NA|类名：sim<br>方法or属性：function getOpKey(slotId: number, callback: AsyncCallback\<string>): void;|@ohos.telephony.sim.d.ts|
|新增|NA|类名：sim<br>方法or属性：function getOpKey(slotId: number): Promise\<string>;|@ohos.telephony.sim.d.ts|
|新增|NA|类名：sim<br>方法or属性：function getOpName(slotId: number, callback: AsyncCallback\<string>): void;|@ohos.telephony.sim.d.ts|
|新增|NA|类名：sim<br>方法or属性：function getOpName(slotId: number): Promise\<string>;|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_VOICE_MAIL_NUMBER_STRING = "voice_mail_number_string"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_VOICE_MAIL_NUMBER_STRING = "voice_mail_number_string"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_IMS_SWITCH_ON_BY_DEFAULT_BOOL = "ims_switch_on_by_default_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_IMS_SWITCH_ON_BY_DEFAULT_BOOL = "ims_switch_on_by_default_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_HIDE_IMS_SWITCH_BOOL = "hide_ims_switch_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_HIDE_IMS_SWITCH_BOOL = "hide_ims_switch_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_VOLTE_SUPPORTED_BOOL = "volte_supported_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_VOLTE_SUPPORTED_BOOL = "volte_supported_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_NR_MODE_SUPPORTED_LIST_INT_ARRAY = "nr_mode_supported_list_int_array"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_NR_MODE_SUPPORTED_LIST_INT_ARRAY = "nr_mode_supported_list_int_array"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_VOLTE_PROVISIONING_SUPPORTED_BOOL = "volte_provisioning_supported_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_VOLTE_PROVISIONING_SUPPORTED_BOOL = "volte_provisioning_supported_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_SS_OVER_UT_SUPPORTED_BOOL = "ss_over_ut_supported_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_SS_OVER_UT_SUPPORTED_BOOL = "ss_over_ut_supported_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_IMS_GBA_REQUIRED_BOOL = "ims_gba_required_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_IMS_GBA_REQUIRED_BOOL = "ims_gba_required_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_UT_PROVISIONING_SUPPORTED_BOOL = "ut_provisioning_supported_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_UT_PROVISIONING_SUPPORTED_BOOL = "ut_provisioning_supported_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_IMS_PREFER_FOR_EMERGENCY_BOOL = "ims_prefer_for_emergency_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_IMS_PREFER_FOR_EMERGENCY_BOOL = "ims_prefer_for_emergency_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_CALL_WAITING_SERVICE_CLASS_INT = "call_waiting_service_class_int"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_CALL_WAITING_SERVICE_CLASS_INT = "call_waiting_service_class_int"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_CALL_TRANSFER_VISIBILITY_BOOL = "call_transfer_visibility_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_CALL_TRANSFER_VISIBILITY_BOOL = "call_transfer_visibility_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_IMS_CALL_DISCONNECT_REASON_INFO_MAPPING_STRING_ARRAY = "ims_call_disconnect_reason_info_mapping_string_array"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_IMS_CALL_DISCONNECT_REASON_INFO_MAPPING_STRING_ARRAY = "ims_call_disconnect_reason_info_mapping_string_array"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_FORCE_VOLTE_SWITCH_ON_BOOL = "force_volte_switch_on_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_FORCE_VOLTE_SWITCH_ON_BOOL = "force_volte_switch_on_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_ENABLE_OPERATOR_NAME_CUST_BOOL = "enable_operator_name_cust_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_ENABLE_OPERATOR_NAME_CUST_BOOL = "enable_operator_name_cust_bool"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_OPERATOR_NAME_CUST_STRING = "operator_name_cust_string"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_OPERATOR_NAME_CUST_STRING = "operator_name_cust_string"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_SPN_DISPLAY_CONDITION_CUST_INT = "spn_display_condition_cust_int"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_SPN_DISPLAY_CONDITION_CUST_INT = "spn_display_condition_cust_int"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_PNN_CUST_STRING_ARRAY = "pnn_cust_string_array"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_PNN_CUST_STRING_ARRAY = "pnn_cust_string_array"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_OPL_CUST_STRING_ARRAY = "opl_cust_string_array"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_OPL_CUST_STRING_ARRAY = "opl_cust_string_array"|@ohos.telephony.sim.d.ts|
|新增|NA|模块名: ohos.telephony.sim<br>类名: OperatorConfigKey<br>方法 or 属性：KEY_EMERGENCY_CALL_STRING_ARRAY = "emergency_call_string_array"|@ohos.telephony.sim.d.ts|
|新增|NA|类名：OperatorConfigKey<br>方法or属性：KEY_EMERGENCY_CALL_STRING_ARRAY = "emergency_call_string_array"|@ohos.telephony.sim.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:call<br>方法 or 属性:function answer(callId: number, callback: AsyncCallback\<void>): void;|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:call<br>方法 or 属性:function answer(callId: number): Promise\<void>;|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:call<br>方法 or 属性:function hangup(callId: number, callback: AsyncCallback\<void>): void;|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:call<br>方法 or 属性:function hangup(callId: number): Promise\<void>;|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:call<br>方法 or 属性:function reject(callId: number, callback: AsyncCallback\<void>): void;|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:call<br>方法 or 属性:function reject(callId: number, options: RejectMessageOptions, callback: AsyncCallback\<void>): void;|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:call<br>方法 or 属性:function reject(callId: number, options?: RejectMessageOptions): Promise\<void>;|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:UNASSIGNED_NUMBER = 1|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:NO_ROUTE_TO_DESTINATION = 3|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:CHANNEL_UNACCEPTABLE = 6|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:OPERATOR_DETERMINED_BARRING = 8|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:NORMAL_CALL_CLEARING = 16|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:USER_BUSY = 17|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:NO_USER_RESPONDING = 18|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:USER_ALERTING_NO_ANSWER = 19|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:CALL_REJECTED = 21|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:NUMBER_CHANGED = 22|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:DESTINATION_OUT_OF_ORDER = 27|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:INVALID_NUMBER_FORMAT = 28|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:NETWORK_OUT_OF_ORDER = 38|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:TEMPORARY_FAILURE = 41|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:INVALID_PARAMETER = 1025|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:SIM_NOT_EXIT = 1026|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:SIM_PIN_NEED = 1027|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:CALL_NOT_ALLOW = 1029|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:SIM_INVALID = 1045|NA|@ohos.telephony.call.d.ts|
|删除|模块名：ohos.telephony.call<br>类名:DisconnectedDetails<br>方法 or 属性:UNKNOWN = 1279|NA|@ohos.telephony.call.d.ts|
|废弃版本有变化|类名：call<br>方法 or 属性：function dial(phoneNumber: string, callback: AsyncCallback\<boolean>): void;<br>废弃版本：N/A|类名：call<br>方法 or 属性：function dial(phoneNumber: string, callback: AsyncCallback\<boolean>): void;<br>废弃版本：9<br>代替接口：telephony.call|@ohos.telephony.call.d.ts|
|废弃版本有变化|类名：call<br>方法 or 属性：function dial(phoneNumber: string, options: DialOptions, callback: AsyncCallback\<boolean>): void;<br>废弃版本：N/A|类名：call<br>方法 or 属性：function dial(phoneNumber: string, options: DialOptions, callback: AsyncCallback\<boolean>): void;<br>废弃版本：9<br>代替接口：telephony.call|@ohos.telephony.call.d.ts|
|废弃版本有变化|类名：call<br>方法 or 属性：function dial(phoneNumber: string, options?: DialOptions): Promise\<boolean>;<br>废弃版本：N/A|类名：call<br>方法 or 属性：function dial(phoneNumber: string, options?: DialOptions): Promise\<boolean>;<br>废弃版本：9<br>代替接口：telephony.call|@ohos.telephony.call.d.ts|
|废弃版本有变化|类名：radio<br>方法 or 属性：function isNrSupported(): boolean;<br>废弃版本：N/A|类名：radio<br>方法 or 属性：function isNrSupported(): boolean;<br>废弃版本：9<br>代替接口：telephony.radio|@ohos.telephony.radio.d.ts|
|废弃版本有变化|类名：radio<br>方法 or 属性：function isNrSupported(slotId: number): boolean;<br>废弃版本：N/A|类名：radio<br>方法 or 属性：function isNrSupported(slotId: number): boolean;<br>废弃版本：9<br>代替接口：telephony.radio|@ohos.telephony.radio.d.ts|
|起始版本有变化|类名：CallTransferInfo<br>方法 or 属性：transferNum: string;<br>起始版本：N/A|类名：CallTransferInfo<br>方法 or 属性：transferNum: string;<br>起始版本：8|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：CallTransferInfo<br>方法 or 属性：type: CallTransferType;<br>起始版本：N/A|类名：CallTransferInfo<br>方法 or 属性：type: CallTransferType;<br>起始版本：8|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：CallTransferInfo<br>方法 or 属性：settingType: CallTransferSettingType;<br>起始版本：N/A|类名：CallTransferInfo<br>方法 or 属性：settingType: CallTransferSettingType;<br>起始版本：8|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：CallTransferResult<br>方法 or 属性：status: TransferStatus;<br>起始版本：N/A|类名：CallTransferResult<br>方法 or 属性：status: TransferStatus;<br>起始版本：8|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：CallTransferResult<br>方法 or 属性：number: string;<br>起始版本：N/A|类名：CallTransferResult<br>方法 or 属性：number: string;<br>起始版本：8|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：CallWaitingStatus<br>方法 or 属性：CALL_WAITING_DISABLE = 0<br>起始版本：N/A|类名：CallWaitingStatus<br>方法 or 属性：CALL_WAITING_DISABLE = 0<br>起始版本：7|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：CallWaitingStatus<br>方法 or 属性：CALL_WAITING_ENABLE = 1<br>起始版本：N/A|类名：CallWaitingStatus<br>方法 or 属性：CALL_WAITING_ENABLE = 1<br>起始版本：7|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：RestrictionStatus<br>方法 or 属性：RESTRICTION_DISABLE = 0<br>起始版本：N/A|类名：RestrictionStatus<br>方法 or 属性：RESTRICTION_DISABLE = 0<br>起始版本：8|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：RestrictionStatus<br>方法 or 属性：RESTRICTION_ENABLE = 1<br>起始版本：N/A|类名：RestrictionStatus<br>方法 or 属性：RESTRICTION_ENABLE = 1<br>起始版本：8|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：TransferStatus<br>方法 or 属性：TRANSFER_DISABLE = 0<br>起始版本：N/A|类名：TransferStatus<br>方法 or 属性：TRANSFER_DISABLE = 0<br>起始版本：8|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：TransferStatus<br>方法 or 属性：TRANSFER_ENABLE = 1<br>起始版本：N/A|类名：TransferStatus<br>方法 or 属性：TRANSFER_ENABLE = 1<br>起始版本：8|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：EmergencyNumberOptions<br>方法 or 属性：slotId?: number;<br>起始版本：N/A|类名：EmergencyNumberOptions<br>方法 or 属性：slotId?: number;<br>起始版本：7|@ohos.telephony.call.d.ts|
|起始版本有变化|类名：NumberFormatOptions<br>方法 or 属性：countryCode?: string;<br>起始版本：N/A|类名：NumberFormatOptions<br>方法 or 属性：countryCode?: string;<br>起始版本：7|@ohos.telephony.call.d.ts|
|权限有变化|类名：observer<br>方法 or 属性：function on(type: 'cellInfoChange', callback: Callback\<Array\<CellInformation>>): void;<br>权限:ohos.permission.LOCATION|类名：observer<br>方法 or 属性：function on(type: 'cellInfoChange', callback: Callback\<Array\<CellInformation>>): void;<br>权限:ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION|@ohos.telephony.observer.d.ts|
|权限有变化|类名：observer<br>方法 or 属性：function on(type: 'cellInfoChange', options: { slotId: number },<br>    callback: Callback\<Array\<CellInformation>>): void;<br>权限:ohos.permission.LOCATION|类名：observer<br>方法 or 属性：function on(type: 'cellInfoChange', options: { slotId: number },<br>    callback: Callback\<Array\<CellInformation>>): void;<br>权限:ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION|@ohos.telephony.observer.d.ts|
|权限有变化|类名：radio<br>方法 or 属性：function getCellInformation(callback: AsyncCallback\<Array\<CellInformation>>): void;<br>权限:ohos.permission.LOCATION|类名：radio<br>方法 or 属性：function getCellInformation(callback: AsyncCallback\<Array\<CellInformation>>): void;<br>权限:ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION|@ohos.telephony.radio.d.ts|
|权限有变化|类名：radio<br>方法 or 属性：function getCellInformation(slotId: number, callback: AsyncCallback\<Array\<CellInformation>>): void;<br>权限:ohos.permission.LOCATION|类名：radio<br>方法 or 属性：function getCellInformation(slotId: number, callback: AsyncCallback\<Array\<CellInformation>>): void;<br>权限:ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION|@ohos.telephony.radio.d.ts|
|权限有变化|类名：radio<br>方法 or 属性：function getCellInformation(slotId?: number): Promise\<Array\<CellInformation>>;<br>权限:ohos.permission.LOCATION|类名：radio<br>方法 or 属性：function getCellInformation(slotId?: number): Promise\<Array\<CellInformation>>;<br>权限:ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION|@ohos.telephony.radio.d.ts|
|删除(权限)|类名：data<br>方法 or 属性：function getDefaultCellularDataSlotId(callback: AsyncCallback\<number>): void;<br>权限:ohos.permission.GET_NETWORK_INFO|类名：data<br>方法 or 属性：function getDefaultCellularDataSlotId(callback: AsyncCallback\<number>): void;<br>权限:N/A|@ohos.telephony.data.d.ts|
|删除(权限)|类名：data<br>方法 or 属性：function getDefaultCellularDataSlotId(): Promise\<number>;<br>权限:ohos.permission.GET_NETWORK_INFO|类名：data<br>方法 or 属性：function getDefaultCellularDataSlotId(): Promise\<number>;<br>权限:N/A|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function muteRinger(callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function muteRinger(): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isEmergencyPhoneNumber(phoneNumber: string, callback: AsyncCallback\<boolean>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isEmergencyPhoneNumber(phoneNumber: string, options: EmergencyNumberOptions, callback: AsyncCallback\<boolean>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isEmergencyPhoneNumber(phoneNumber: string, options?: EmergencyNumberOptions): Promise\<boolean>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function formatPhoneNumber(phoneNumber: string, callback: AsyncCallback\<string>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function formatPhoneNumber(phoneNumber: string, options: NumberFormatOptions, callback: AsyncCallback\<string>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function formatPhoneNumber(phoneNumber: string, options?: NumberFormatOptions): Promise\<string>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function formatPhoneNumberToE164(phoneNumber: string, countryCode: string, callback: AsyncCallback\<string>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function formatPhoneNumberToE164(phoneNumber: string, countryCode: string): Promise\<string>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function holdCall(callId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function holdCall(callId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function unHoldCall(callId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function unHoldCall(callId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function switchCall(callId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function switchCall(callId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function combineConference(callId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function combineConference(callId: number): Promise\<void>;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getMainCallId(callId: number, callback: AsyncCallback\<number>): void;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getMainCallId(callId: number): Promise\<number>;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getSubCallIdList(callId: number, callback: AsyncCallback\<Array\<string>>): void;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getSubCallIdList(callId: number): Promise\<Array\<string>>;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getCallIdListForConference(callId: number, callback: AsyncCallback\<Array\<string>>): void;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getCallIdListForConference(callId: number): Promise\<Array\<string>>;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getCallWaitingStatus(slotId: number, callback: AsyncCallback\<CallWaitingStatus>): void;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getCallWaitingStatus(slotId: number): Promise\<CallWaitingStatus>;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function setCallWaiting(slotId: number, activate: boolean, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function setCallWaiting(slotId: number, activate: boolean): Promise\<void>;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function startDTMF(callId: number, character: string, callback: AsyncCallback\<void>): void;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function startDTMF(callId: number, character: string): Promise\<void>;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function stopDTMF(callId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function stopDTMF(callId: number): Promise\<void>;<br>错误码内容: 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isInEmergencyCall(callback: AsyncCallback\<boolean>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isInEmergencyCall(): Promise\<boolean>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function on(type: 'callDetailsChange', callback: Callback\<CallAttributeOptions>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function off(type: 'callDetailsChange', callback?: Callback\<CallAttributeOptions>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function on(type: 'callEventChange', callback: Callback\<CallEventOptions>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function off(type: 'callEventChange', callback?: Callback\<CallEventOptions>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function on(type: 'callDisconnectedCause', callback: Callback\<DisconnectedDetails>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function off(type: 'callDisconnectedCause', callback?: Callback\<DisconnectedDetails>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isNewCallAllowed(callback: AsyncCallback\<boolean>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isNewCallAllowed(): Promise\<boolean>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function separateConference(callId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function separateConference(callId: number): Promise\<void>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getCallRestrictionStatus(slotId: number, type: CallRestrictionType, callback: AsyncCallback\<RestrictionStatus>): void;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getCallRestrictionStatus(slotId: number, type: CallRestrictionType): Promise\<RestrictionStatus>;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function setCallRestriction(slotId: number, info: CallRestrictionInfo, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function setCallRestriction(slotId: number, info: CallRestrictionInfo): Promise\<void>;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getCallTransferInfo(slotId: number, type: CallTransferType, callback: AsyncCallback\<CallTransferResult>): void;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function getCallTransferInfo(slotId: number, type: CallTransferType): Promise\<CallTransferResult>;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function setCallTransfer(slotId: number, info: CallTransferInfo, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function setCallTransfer(slotId: number, info: CallTransferInfo): Promise\<void>;<br>错误码内容: 201, 401, 801, 8300001, 8300002, 8300003|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isRinging(callback: AsyncCallback\<boolean>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isRinging(): Promise\<boolean>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function setMuted(callback: AsyncCallback\<void>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function setMuted(): Promise\<void>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function cancelMuted(callback: AsyncCallback\<void>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function cancelMuted(): Promise\<void>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function setAudioDevice(device: AudioDevice, callback: AsyncCallback\<void>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function joinConference(mainCallId: number, callNumberList: Array\<string>, callback: AsyncCallback\<void>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function joinConference(mainCallId: number, callNumberList: Array\<string>): Promise\<void>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function updateImsCallMode(callId: number, mode: ImsCallMode, callback: AsyncCallback\<void>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function updateImsCallMode(callId: number, mode: ImsCallMode): Promise\<void>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function enableImsSwitch(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function enableImsSwitch(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function disableImsSwitch(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function disableImsSwitch(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isImsSwitchEnabled(slotId: number, callback: AsyncCallback\<boolean>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：call<br>方法 or 属性：function isImsSwitchEnabled(slotId: number): Promise\<boolean>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.call.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function setDefaultCellularDataSlotId(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301001|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function setDefaultCellularDataSlotId(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301001|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function isCellularDataEnabled(callback: AsyncCallback\<boolean>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function isCellularDataEnabled(): Promise\<boolean>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function enableCellularData(callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function enableCellularData(): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function disableCellularData(callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function disableCellularData(): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function isCellularDataRoamingEnabled(slotId: number, callback: AsyncCallback\<boolean>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function isCellularDataRoamingEnabled(slotId: number): Promise\<boolean>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function enableCellularDataRoaming(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function enableCellularDataRoaming(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function disableCellularDataRoaming(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：data<br>方法 or 属性：function disableCellularDataRoaming(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.data.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'networkStateChange', callback: Callback\<NetworkState>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'networkStateChange', options: { slotId: number }, callback: Callback\<NetworkState>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function off(type: 'networkStateChange', callback?: Callback\<NetworkState>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'signalInfoChange', callback: Callback\<Array\<SignalInformation>>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'signalInfoChange', options: { slotId: number },<br>    callback: Callback\<Array\<SignalInformation>>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function off(type: 'signalInfoChange', callback?: Callback\<Array\<SignalInformation>>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'cellInfoChange', callback: Callback\<Array\<CellInformation>>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'cellInfoChange', options: { slotId: number },<br>    callback: Callback\<Array\<CellInformation>>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function off(type: 'cellInfoChange', callback?: Callback\<Array\<CellInformation>>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'cellularDataConnectionStateChange',<br>    callback: Callback\<{ state: DataConnectState, network: RatType }>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'cellularDataConnectionStateChange', options: { slotId: number },<br>    callback: Callback\<{ state: DataConnectState, network: RatType }>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function off(type: 'cellularDataConnectionStateChange',<br>    callback?: Callback\<{ state: DataConnectState, network: RatType }>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'cellularDataFlowChange', callback: Callback\<DataFlowType>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'cellularDataFlowChange', options: { slotId: number },<br>    callback: Callback\<DataFlowType>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function off(type: 'cellularDataFlowChange', callback?: Callback\<DataFlowType>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'callStateChange', callback: Callback\<{ state: CallState, number: string }>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'callStateChange', options: { slotId: number },<br>    callback: Callback\<{ state: CallState, number: string }>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function off(type: 'callStateChange', callback?: Callback\<{ state: CallState, number: string }>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'simStateChange', callback: Callback\<SimStateData>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function on(type: 'simStateChange', options: { slotId: number }, callback: Callback\<SimStateData>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：observer<br>方法 or 属性：function off(type: 'simStateChange', callback?: Callback\<SimStateData>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.observer.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getRadioTech(slotId: number,<br>    callback: AsyncCallback\<{psRadioTech: RadioTechnology, csRadioTech: RadioTechnology}>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getRadioTech(slotId: number): Promise\<{psRadioTech: RadioTechnology, csRadioTech: RadioTechnology}>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNetworkState(callback: AsyncCallback\<NetworkState>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNetworkState(slotId: number, callback: AsyncCallback\<NetworkState>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNetworkState(slotId?: number): Promise\<NetworkState>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function sendUpdateCellLocationRequest(callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getCellInformation(callback: AsyncCallback\<Array\<CellInformation>>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getCellInformation(slotId: number, callback: AsyncCallback\<Array\<CellInformation>>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getCellInformation(slotId?: number): Promise\<Array\<CellInformation>>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNetworkSelectionMode(slotId: number, callback: AsyncCallback\<NetworkSelectionMode>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNetworkSelectionMode(slotId: number): Promise\<NetworkSelectionMode>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function setNetworkSelectionMode(options: NetworkSelectionModeOptions, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function setNetworkSelectionMode(options: NetworkSelectionModeOptions): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNetworkSearchInformation(slotId: number, callback: AsyncCallback\<NetworkSearchResult>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNetworkSearchInformation(slotId: number): Promise\<NetworkSearchResult>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getISOCountryCodeForNetwork(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getISOCountryCodeForNetwork(slotId: number): Promise\<string>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNrOptionMode(callback: AsyncCallback\<NrOptionMode>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNrOptionMode(slotId: number, callback: AsyncCallback\<NrOptionMode>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getNrOptionMode(slotId?: number): Promise\<NrOptionMode>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getIMEI(callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getIMEI(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getIMEI(slotId?: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getMEID(callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getMEID(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getMEID(slotId?: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getUniqueDeviceId(callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getUniqueDeviceId(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getUniqueDeviceId(slotId?: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getPrimarySlotId(callback: AsyncCallback\<number>): void;<br>错误码内容: 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getPrimarySlotId(): Promise\<number>;<br>错误码内容: 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function setPrimarySlotId(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function setPrimarySlotId(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getSignalInformation(slotId: number, callback: AsyncCallback\<Array\<SignalInformation>>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getSignalInformation(slotId: number): Promise\<Array\<SignalInformation>>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function isRadioOn(callback: AsyncCallback\<boolean>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function isRadioOn(slotId: number, callback: AsyncCallback\<boolean>): void<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function isRadioOn(slotId?: number): Promise\<boolean>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function turnOnRadio(callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function turnOnRadio(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function turnOnRadio(slotId?: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function turnOffRadio(callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function turnOffRadio(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function turnOffRadio(slotId?: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getOperatorName(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getOperatorName(slotId: number): Promise\<string>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function setPreferredNetwork(slotId: number, networkMode: PreferredNetworkMode, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function setPreferredNetwork(slotId: number, networkMode: PreferredNetworkMode): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getPreferredNetwork(slotId: number, callback: AsyncCallback\<PreferredNetworkMode>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：radio<br>方法 or 属性：function getPreferredNetwork(slotId: number): Promise\<PreferredNetworkMode>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.radio.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function hasOperatorPrivileges(slotId: number, callback: AsyncCallback\<boolean>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function hasOperatorPrivileges(slotId: number): Promise\<boolean>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getISOCountryCodeForSim(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getISOCountryCodeForSim(slotId: number): Promise\<string>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimOperatorNumeric(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimOperatorNumeric(slotId: number): Promise\<string>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimSpn(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimSpn(slotId: number): Promise\<string>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimState(slotId: number, callback: AsyncCallback\<SimState>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimState(slotId: number): Promise\<SimState>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getCardType(slotId: number, callback: AsyncCallback\<CardType>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getCardType(slotId: number): Promise\<CardType>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimIccId(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimIccId(slotId: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getVoiceMailIdentifier(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getVoiceMailIdentifier(slotId: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getVoiceMailNumber(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getVoiceMailNumber(slotId: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setVoiceMailInfo(slotId: number, mailName: string, mailNumber: string, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setVoiceMailInfo(slotId: number, mailName: string, mailNumber: string): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimTelephoneNumber(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimTelephoneNumber(slotId: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimGid1(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimGid1(slotId: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getIMSI(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getIMSI(slotId: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function hasSimCard(slotId: number, callback: AsyncCallback\<boolean>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function hasSimCard(slotId: number): Promise\<boolean>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimAccountInfo(slotId: number, callback: AsyncCallback\<IccAccountInfo>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getSimAccountInfo(slotId: number): Promise\<IccAccountInfo>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getActiveSimAccountInfoList(callback: AsyncCallback\<Array\<IccAccountInfo>>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getActiveSimAccountInfoList(): Promise\<Array\<IccAccountInfo>>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setDefaultVoiceSlotId(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301001|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setDefaultVoiceSlotId(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301001|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function activateSim(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function activateSim(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function deactivateSim(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function deactivateSim(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setShowName(slotId: number, name: string, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setShowName(slotId: number, name: string): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getShowName(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getShowName(slotId: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setShowNumber(slotId: number, number: string, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setShowNumber(slotId: number, number: string): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getShowNumber(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getShowNumber(slotId: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getOperatorConfigs(slotId: number, callback: AsyncCallback\<Array\<OperatorConfig>>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getOperatorConfigs(slotId: number): Promise\<Array\<OperatorConfig>>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockPin(slotId: number, pin: string, callback: AsyncCallback\<LockStatusResponse>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockPin(slotId: number, pin: string): Promise\<LockStatusResponse>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockPuk(slotId: number, newPin: string, puk: string, callback: AsyncCallback\<LockStatusResponse>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockPuk(slotId: number, newPin: string, puk: string): Promise\<LockStatusResponse>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function alterPin(slotId: number, newPin: string, oldPin: string, callback: AsyncCallback\<LockStatusResponse>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function alterPin(slotId: number, newPin: string, oldPin: string): Promise\<LockStatusResponse>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setLockState(slotId: number, options: LockInfo, callback: AsyncCallback\<LockStatusResponse>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function setLockState(slotId: number, options: LockInfo): Promise\<LockStatusResponse>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockPin2(slotId: number, pin2: string, callback: AsyncCallback\<LockStatusResponse>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockPin2(slotId: number, pin2: string): Promise\<LockStatusResponse>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockPuk2(slotId: number, newPin2: string, puk2: string, callback: AsyncCallback\<LockStatusResponse>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockPuk2(slotId: number, newPin2: string, puk2: string): Promise\<LockStatusResponse>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function alterPin2(slotId: number, newPin2: string, oldPin2: string, callback: AsyncCallback\<LockStatusResponse>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function alterPin2(slotId: number, newPin2: string, oldPin2: string): Promise\<LockStatusResponse>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function queryIccDiallingNumbers(slotId: number, type: ContactType, callback: AsyncCallback\<Array\<DiallingNumbersInfo>>): void<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function queryIccDiallingNumbers(slotId: number, type: ContactType): Promise\<Array\<DiallingNumbersInfo>>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function addIccDiallingNumbers(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function addIccDiallingNumbers(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function delIccDiallingNumbers(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function delIccDiallingNumbers(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function updateIccDiallingNumbers(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function updateIccDiallingNumbers(slotId: number, type: ContactType, diallingNumbers: DiallingNumbersInfo): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getLockState(slotId: number, lockType: LockType, callback: AsyncCallback\<LockState>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function getLockState(slotId: number, lockType: LockType): Promise\<LockState>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function sendEnvelopeCmd(slotId: number, cmd: string, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function sendEnvelopeCmd(slotId: number, cmd: string): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function sendTerminalResponseCmd(slotId: number, cmd: string, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function sendTerminalResponseCmd(slotId: number, cmd: string): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockSimLock(slotId: number, lockInfo: PersoLockInfo, callback: AsyncCallback\<LockStatusResponse>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sim<br>方法 or 属性：function unlockSimLock(slotId: number, lockInfo: PersoLockInfo): Promise\<LockStatusResponse>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999, 8301002|@ohos.telephony.sim.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function splitMessage(content: string, callback: AsyncCallback\<Array\<string>>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function splitMessage(content: string): Promise\<Array\<string>>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function createMessage(pdu: Array\<number>, specification: string, callback: AsyncCallback\<ShortMessage>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function createMessage(pdu: Array\<number>, specification: string): Promise\<ShortMessage>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function sendMessage(options: SendMessageOptions): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function setDefaultSmsSlotId(slotId: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function setDefaultSmsSlotId(slotId: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300004, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function setSmscAddr(slotId: number, smscAddr: string, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function setSmscAddr(slotId: number, smscAddr: string): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function getSmscAddr(slotId: number, callback: AsyncCallback\<string>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function getSmscAddr(slotId: number): Promise\<string>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function addSimMessage(options: SimMessageOptions, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function addSimMessage(options: SimMessageOptions): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function delSimMessage(slotId: number, msgIndex: number, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function delSimMessage(slotId: number, msgIndex: number): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function updateSimMessage(options: UpdateSimMessageOptions, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function updateSimMessage(options: UpdateSimMessageOptions): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function getAllSimMessages(slotId: number, callback: AsyncCallback\<Array\<SimShortMessage>>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function getAllSimMessages(slotId: number): Promise\<Array\<SimShortMessage>>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function setCBConfig(options: CBConfigOptions, callback: AsyncCallback\<void>): void;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function setCBConfig(options: CBConfigOptions): Promise\<void>;<br>错误码内容: 201, 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function getSmsSegmentsInfo(slotId: number, message: string, force7bit: boolean, callback: AsyncCallback\<SmsSegmentsInfo>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function getSmsSegmentsInfo(slotId: number, message: string, force7bit: boolean): Promise\<SmsSegmentsInfo>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function getImsShortMessageFormat(callback: AsyncCallback\<string>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function getImsShortMessageFormat(): Promise\<string>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function decodeMms(mmsFilePathName: string \| Array\<number>, callback: AsyncCallback\<MmsInformation>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function decodeMms(mmsFilePathName: string \| Array\<number>): Promise\<MmsInformation>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function encodeMms(mms: MmsInformation, callback: AsyncCallback\<Array\<number>>): void;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(错误码)|NA|类名：sms<br>方法 or 属性：function encodeMms(mms: MmsInformation): Promise\<Array\<number>>;<br>错误码内容: 401, 8300001, 8300002, 8300003, 8300999|@ohos.telephony.sms.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function holdCall(callId: number, callback: AsyncCallback\<void>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function holdCall(callId: number, callback: AsyncCallback\<void>): void;<br>权限:ohos.permission.ANSWER_CALL|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function holdCall(callId: number): Promise\<void>;<br>权限:N/A|类名：call<br>方法 or 属性：function holdCall(callId: number): Promise\<void>;<br>权限:ohos.permission.ANSWER_CALL|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function unHoldCall(callId: number, callback: AsyncCallback\<void>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function unHoldCall(callId: number, callback: AsyncCallback\<void>): void;<br>权限:ohos.permission.ANSWER_CALL|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function unHoldCall(callId: number): Promise\<void>;<br>权限:N/A|类名：call<br>方法 or 属性：function unHoldCall(callId: number): Promise\<void>;<br>权限:ohos.permission.ANSWER_CALL|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function switchCall(callId: number, callback: AsyncCallback\<void>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function switchCall(callId: number, callback: AsyncCallback\<void>): void;<br>权限:ohos.permission.ANSWER_CALL|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function switchCall(callId: number): Promise\<void>;<br>权限:N/A|类名：call<br>方法 or 属性：function switchCall(callId: number): Promise\<void>;<br>权限:ohos.permission.ANSWER_CALL|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function getCallWaitingStatus(slotId: number, callback: AsyncCallback\<CallWaitingStatus>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function getCallWaitingStatus(slotId: number, callback: AsyncCallback\<CallWaitingStatus>): void;<br>权限:ohos.permission.GET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function getCallWaitingStatus(slotId: number): Promise\<CallWaitingStatus>;<br>权限:N/A|类名：call<br>方法 or 属性：function getCallWaitingStatus(slotId: number): Promise\<CallWaitingStatus>;<br>权限:ohos.permission.GET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function setCallWaiting(slotId: number, activate: boolean, callback: AsyncCallback\<void>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function setCallWaiting(slotId: number, activate: boolean, callback: AsyncCallback\<void>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function setCallWaiting(slotId: number, activate: boolean): Promise\<void>;<br>权限:N/A|类名：call<br>方法 or 属性：function setCallWaiting(slotId: number, activate: boolean): Promise\<void>;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function on(type: 'callDetailsChange', callback: Callback\<CallAttributeOptions>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function on(type: 'callDetailsChange', callback: Callback\<CallAttributeOptions>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function off(type: 'callDetailsChange', callback?: Callback\<CallAttributeOptions>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function off(type: 'callDetailsChange', callback?: Callback\<CallAttributeOptions>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function on(type: 'callEventChange', callback: Callback\<CallEventOptions>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function on(type: 'callEventChange', callback: Callback\<CallEventOptions>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function off(type: 'callEventChange', callback?: Callback\<CallEventOptions>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function off(type: 'callEventChange', callback?: Callback\<CallEventOptions>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function on(type: 'callDisconnectedCause', callback: Callback\<DisconnectedDetails>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function on(type: 'callDisconnectedCause', callback: Callback\<DisconnectedDetails>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function off(type: 'callDisconnectedCause', callback?: Callback\<DisconnectedDetails>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function off(type: 'callDisconnectedCause', callback?: Callback\<DisconnectedDetails>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function getCallRestrictionStatus(slotId: number, type: CallRestrictionType, callback: AsyncCallback\<RestrictionStatus>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function getCallRestrictionStatus(slotId: number, type: CallRestrictionType, callback: AsyncCallback\<RestrictionStatus>): void;<br>权限:ohos.permission.GET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function getCallRestrictionStatus(slotId: number, type: CallRestrictionType): Promise\<RestrictionStatus>;<br>权限:N/A|类名：call<br>方法 or 属性：function getCallRestrictionStatus(slotId: number, type: CallRestrictionType): Promise\<RestrictionStatus>;<br>权限:ohos.permission.GET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function setCallRestriction(slotId: number, info: CallRestrictionInfo, callback: AsyncCallback\<void>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function setCallRestriction(slotId: number, info: CallRestrictionInfo, callback: AsyncCallback\<void>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function setCallRestriction(slotId: number, info: CallRestrictionInfo): Promise\<void>;<br>权限:N/A|类名：call<br>方法 or 属性：function setCallRestriction(slotId: number, info: CallRestrictionInfo): Promise\<void>;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function getCallTransferInfo(slotId: number, type: CallTransferType, callback: AsyncCallback\<CallTransferResult>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function getCallTransferInfo(slotId: number, type: CallTransferType, callback: AsyncCallback\<CallTransferResult>): void;<br>权限:ohos.permission.GET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function getCallTransferInfo(slotId: number, type: CallTransferType): Promise\<CallTransferResult>;<br>权限:N/A|类名：call<br>方法 or 属性：function getCallTransferInfo(slotId: number, type: CallTransferType): Promise\<CallTransferResult>;<br>权限:ohos.permission.GET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function setCallTransfer(slotId: number, info: CallTransferInfo, callback: AsyncCallback\<void>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function setCallTransfer(slotId: number, info: CallTransferInfo, callback: AsyncCallback\<void>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function setCallTransfer(slotId: number, info: CallTransferInfo): Promise\<void>;<br>权限:N/A|类名：call<br>方法 or 属性：function setCallTransfer(slotId: number, info: CallTransferInfo): Promise\<void>;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function enableImsSwitch(slotId: number, callback: AsyncCallback\<void>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function enableImsSwitch(slotId: number, callback: AsyncCallback\<void>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function enableImsSwitch(slotId: number): Promise\<void>;<br>权限:N/A|类名：call<br>方法 or 属性：function enableImsSwitch(slotId: number): Promise\<void>;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function disableImsSwitch(slotId: number, callback: AsyncCallback\<void>): void;<br>权限:N/A|类名：call<br>方法 or 属性：function disableImsSwitch(slotId: number, callback: AsyncCallback\<void>): void;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：call<br>方法 or 属性：function disableImsSwitch(slotId: number): Promise\<void>;<br>权限:N/A|类名：call<br>方法 or 属性：function disableImsSwitch(slotId: number): Promise\<void>;<br>权限:ohos.permission.SET_TELEPHONY_STATE|@ohos.telephony.call.d.ts|
|新增(权限)|类名：radio<br>方法 or 属性：function sendUpdateCellLocationRequest(callback: AsyncCallback\<void>): void;<br>权限:N/A|类名：radio<br>方法 or 属性：function sendUpdateCellLocationRequest(callback: AsyncCallback\<void>): void;<br>权限:ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION|@ohos.telephony.radio.d.ts|
|新增(权限)|类名：sim<br>方法 or 属性：function getLockState(slotId: number, lockType: LockType, callback: AsyncCallback\<LockState>): void;<br>权限:N/A|类名：sim<br>方法 or 属性：function getLockState(slotId: number, lockType: LockType, callback: AsyncCallback\<LockState>): void;<br>权限:ohos.permission.GET_TELEPHONY_STATE|@ohos.telephony.sim.d.ts|
|新增(权限)|类名：sim<br>方法 or 属性：function getLockState(slotId: number, lockType: LockType): Promise\<LockState>;<br>权限:N/A|类名：sim<br>方法 or 属性：function getLockState(slotId: number, lockType: LockType): Promise\<LockState>;<br>权限:ohos.permission.GET_TELEPHONY_STATE|@ohos.telephony.sim.d.ts|
|函数有变化|类名：call<br>方法 or 属性：function setAudioDevice(device: AudioDevice, callback: AsyncCallback\<void>): void;<br>|类名：call<br>方法 or 属性：function setAudioDevice(device: AudioDevice, callback: AsyncCallback\<void>): void;<br>|@ohos.telephony.call.d.ts|
|函数有变化|类名：call<br>方法 or 属性：function setAudioDevice(device: AudioDevice, callback: AsyncCallback\<void>): void;<br>|类名：call<br>方法 or 属性：function setAudioDevice(device: AudioDevice, options: AudioDeviceOptions, callback: AsyncCallback\<void>): void;<br>|@ohos.telephony.call.d.ts|
|函数有变化|类名：call<br>方法 or 属性：function setAudioDevice(device: AudioDevice): Promise\<void>;<br>|类名：call<br>方法 or 属性：function setAudioDevice(device: AudioDevice, options?: AudioDeviceOptions): Promise\<void>;<br>|@ohos.telephony.call.d.ts|
|函数有变化|类名：radio<br>方法 or 属性：function sendUpdateCellLocationRequest(callback: AsyncCallback\<void>): void;<br>|类名：radio<br>方法 or 属性：function sendUpdateCellLocationRequest(callback: AsyncCallback\<void>): void;<br>|@ohos.telephony.radio.d.ts|
|函数有变化|类名：radio<br>方法 or 属性：function sendUpdateCellLocationRequest(callback: AsyncCallback\<void>): void;<br>|类名：radio<br>方法 or 属性：function sendUpdateCellLocationRequest(slotId: number, callback: AsyncCallback\<void>): void;<br>|@ohos.telephony.radio.d.ts|
|函数有变化|类名：radio<br>方法 or 属性：function sendUpdateCellLocationRequest(): Promise\<void>;<br>|类名：radio<br>方法 or 属性：function sendUpdateCellLocationRequest(slotId?: number): Promise\<void>;<br>|@ohos.telephony.radio.d.ts|
|函数有变化|类名：sms<br>方法 or 属性：function isImsSmsSupported(callback: AsyncCallback\<boolean>): void;<br>|类名：sms<br>方法 or 属性：function isImsSmsSupported(slotId: number, callback: AsyncCallback\<boolean>): void;<br>|@ohos.telephony.sms.d.ts|
|函数有变化|类名：sms<br>方法 or 属性：function isImsSmsSupported(): Promise\<boolean>;<br>|类名：sms<br>方法 or 属性：function isImsSmsSupported(slotId: number): Promise\<boolean>;<br>|@ohos.telephony.sms.d.ts|
