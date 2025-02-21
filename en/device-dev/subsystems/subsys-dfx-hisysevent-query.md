# HiSysEvent Query


## Overview

HiSysEvent allows you to query system events by specifying search criteria. For example, for a power consumption module, you can query required system events for analysis.


## How to Develop

### Available APIs

#### C++ Event Query API

HiSysEvent query is implemented using the API provided by the **HiSysEventManager** class. For details, see the [API Header Files](/base/hiviewdfx/hisysevent/interfaces/native/innerkits/hisysevent_manager/include/).

> **NOTE**
>
> For details about **HiSysEventRecord** in the **OnQuery()** API of **HiSysEventQueryCallback**, see Table 5 in [HiSysEvent Listening](subsys-dfx-hisysevent-listening.md).

  **Table 1** Description of the HiSysEvent query API

| API| Description|
| -------- | -------- |
| int32_t Query(struct&nbsp;QueryArg&amp;&nbsp;arg,<br>std::vector&lt;QueryRule&gt;&amp;&nbsp;rules,<br>std::shared_ptr&lt;HiSysEventQueryCallback&gt;&nbsp;callback) | Queries system events by search criteria such as the time segment, event domain, and event name.<br>Input arguments:<br>- **arg**: event query parameter.<br>- **rules**: rules for event filtering.<br>- **callback**: callback object for event query.<br>Return value:<br>- **0**: Query is successful.<br>- A negative value: Query has failed.|

  **Table 2** Description of QueryArg objects

| Attribute| Type| Description|
| -------- | -------- | -------- |
| beginTime | long long | Start time for query. The value is a Unix timestamp, in milliseconds.|
| endTime | long long | End time for query. The value is a Unix timestamp, in milliseconds.|
| maxEvents | int | Maximum number of returned events.|

  **Table 3** Description of QueryRule objects

| API| Description|
| -------- | -------- |
| QueryRule(const&nbsp;std::string&amp;&nbsp;domain,<br>const&nbsp;std::vector&lt;std::string&gt;&amp;&nbsp;eventList) | Constructor used to create a **QueryRule** object.<br>Input arguments:<br>- **domain**: domain to which the event of the **QueryRule** object belongs, in the string format. By default, an empty string indicates that the domain is successfully matched.<br>**eventList**: event name list, in the **std::vector&lt;std::string&gt;** format. By default, an empty string indicates that the event names on the list are successfully matched.|

  **Table 4** Description of HiSysEventQueryCallback objects

| API| Description|
| -------- | -------- |
| void&nbsp;HiSysEventQueryCallback::OnQuery(std::shared_ptr&lt;std::vector&lt;HiSysEventRecord&gt;&gt;&nbsp;sysEvents) | Callback object for event query.<br>Input arguments:<br>- **sysEvents**: event list.|
| void&nbsp;HiSysEventQueryCallback::OnComplete(int32_t&nbsp;reason,&nbsp;int32_t&nbsp;total) | Callback object for completion of event query.<br>Input arguments:<br>- **reason**: reason for completion of event query. The value **0** indicates that the query is normal, and any other value indicates that the query has failed.<br>- **total**: total number of events returned in this query.|

#### C Event Query API

HiSysEvent query is implemented using the API provided in the following table. For details, see the [API Header Files](/base/hiviewdfx/hisysevent/interfaces/native/innerkits/hisysevent_manager/include/).

 **Table 5** Description of the HiSysEvent query API

| API                                                    | Description                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| int OH_HiSysEvent_Query(const HiSysEventQueryArg& arg, HiSysEventQueryRule rules[], size_t ruleSize, HiSysEventQueryCallback& callback); | Queries system events by search criteria such as the time segment, event domain, event name, and event parameter.<br>Input arguments:<br>- **arg**: event query parameter.<br>- **rules**: rules for event filtering.<br>- **ruleSize**: number of event filtering rules.<br>- **callback**: callback object for event query.<br>Return value:<br>- **0**: Query is successful.<br>- A negative value: Query has failed.|

 **Table 6** Description of the HiSysEventQueryArg structure

| Attribute | Type| Description                                                |
| --------- | -------- | ---------------------------------------------------- |
| beginTime | int64_t  | Start time for query. The value is a Unix timestamp, in milliseconds.|
| endTime   | int64_t  | End time for query. The value is a Unix timestamp, in milliseconds.|
| maxEvents | int32_t  | Maximum number of returned events.                    |

**Table 7** Description of the HiSysEventQueryRule structure

| Attribute     | Type | Description                              |
| ------------- | --------- | ---------------------------------- |
| domain        | char[]    | Event domain.          |
| eventList     | char\[][] | Event name list.      |
| eventListSize | size_t    | Size of the event name list.  |
| condition     | char*     | Custom event parameter conditions for the query.|

The **condition** parameter must be in the specified JSON string format. For example:

```json
{
    "version":"V1",
    "condition":{
        "and":[
            {"param":"type_","op":">","value":0},
            {"param":"uid_","op":"=","value":1201}
        ],
        "or":[
            {"param":"NAME","op":"=","value":"SysEventService"},
            {"param":"NAME","op":"=","value":"SysEventSource"}
        ]
    }
}
```

- The **version** field is mandatory, indicating the supported version of the input condition. Currently, only **V1** is supported.
- The **condition** field is mandatory, indicating the input condition.
  - The **and** field is optional, indicating the AND relationship between conditions.
  - The **or** field is optional, indicating the OR relationship between conditions.
    - The **param** field is mandatory, indicating the parameter name for condition matching. The value must be a string.
    - The **op** field is mandatory, indicating the parameter comparison operator for condition matching. The value must be a string. Supported comparison operators include the following: =, >, <, >=, and <=.
    - The **value** field is mandatory, indicating the parameter value for condition matching. The value must be a string or an integer.

**Table 8** Description of the HiSysEventQueryCallback structure

| Attribute  | Type                                          | Description                                                        |
| ---------- | -------------------------------------------------- | ------------------------------------------------------------ |
| OnQuery    | void (*)(HiSysEventRecord records[], size_t size); | Callback object for event query.<br>Input arguments:<br>- **records**: event list.<br>- **size**: size of the event list.|
| OnComplete | void (*)(int32_t reason, int32_t total);           | Callback object for completion of event query.<br>Input arguments:<br>- **reason**: reason for completion of event query. The value **0** indicates that the query is normal, and any other value indicates that the query has failed.<br>- **total**: total number of events returned in this query.|

**Table 9** Description of the HiSysEventRecord event structure

| Attribute | Type           | Description                      |
| --------- | ------------------- | -------------------------- |
| domain    | char[]              | Event domain.          |
| eventName | char\[]             | Event name.              |
| type      | HiSysEventEventType | Event type.              |
| time      | uint64_t            | Event timestamp.            |
| tz        | char\[]             | Event time zone.              |
| pid       | int64_t             | Process ID of the event.            |
| tid       | int64_t             | Thread ID of the event.            |
| uid       | int64_t             | User ID of the event.            |
| traceId   | uint64_t            | Distributed call chain trace ID of the event.    |
| spandId   | uint64_t            | Span ID for the distributed call chain trace of the event.  |
| pspanId   | uint64_t            | Parent span ID for the distributed call chain trace of the event.|
| traceFlag | int                 | Distributed call chain trace flag of the event.  |
| level     | char*               | Event level.              |
| tag       | char*               | Event tag.              |
| jsonStr   | char*               | Event content.              |

**Table 10** Description of HiSysEventRecord APIs

| API                                                    |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| void OH_HiSysEvent_GetParamNames(const HiSysEventRecord& record, char*** params, size_t& len); | Obtains all parameter names of an event.<br>Input arguments:<br>- **record**: event structure.<br>- **params**: parameter name array.<br>- **len**: size of the parameter name array.|
| int OH_HiSysEvent_GetParamInt64Value(const HiSysEventRecord& record, const char* name, int64_t& value); | Parses the parameter value in the event to an int64_t value and assigns the value to **value**.<br>Input arguments:<br>- **record**: event structure.<br>- **name**: parameter name.<br>- **value**: parameter value of the int64_t type.|
| int OH_HiSysEvent_GetParamUint64Value(const HiSysEventRecord& record, const char* name, uint64_t& value); | Parses the parameter value in the event to an uint64_t value and assigns the value to **value**.<br>Input arguments:<br>- **record**: event structure.<br>- **name**: parameter name.<br>- **value**: parameter value of the uint64_t type.|
| int OH_HiSysEvent_GetParamDoubleValue(const HiSysEventRecord& record, const char* name, double& value); | Parses the parameter value in the event to a double value and assigns the value to **value**.<br>Input arguments:<br>- **record**: event structure.<br>- **name**: parameter name.<br>- **value**: parameter value of the double type.|
| int OH_HiSysEvent_GetParamStringValue(const HiSysEventRecord& record, const char* name, char** value); | Parses the parameter value in the event to a char array value and assigns the value to **value**. You need to release the memory manually after usage.<br>Input arguments:<br>- **record**: event structure.<br>- **name**: parameter name.<br>- **value**: char\* reference.|
| int OH_HiSysEvent_GetParamInt64Values(const HiSysEventRecord& record, const char* name, int64_t** value, size_t& len); | Parses the parameter value in the event to a int64_t array value and assigns the value to **value**. You need to release the memory manually after usage.<br>Input arguments:<br>- **record**: event structure.<br>- **name**: parameter name.<br>- **value**: int64_t\* reference.<br>- **len**: array size.|
| int OH_HiSysEvent_GetParamUint64Values(const HiSysEventRecord& record, const char* name, uint64_t** value, size_t& len); | Parses the parameter value in the event to a uint64_t array value and assigns the value to **value**. You need to release the memory manually after usage.<br>Input arguments:<br>- **record**: event structure.<br>- **name**: parameter name.<br>- **value**: uint64_t\* reference.<br>- **len**: array size.|
| int OH_HiSysEvent_GetParamDoubleValues(const HiSysEventRecord& record, const char* name, double** value, size_t& len); | Parses the parameter value in the event to a double array value and assigns the value to **value**. You need to release the memory manually after usage.<br>Input arguments:<br>- **record**: event structure.<br>- **name**: parameter name.<br>- **value**: double\* reference.<br>- **len**: array size.|
| int OH_HiSysEvent_GetParamStringValues(const HiSysEventRecord& record, const char* name, char*** value, size_t& len); | Parses the parameter value in the event to a char* array value and assigns the value to **value**. You need to release the memory manually after usage.<br>Input arguments:<br>- **record**: event structure.<br>- **name**: parameter name.<br>- **value**: char\*\* reference.<br>- **len**: array size.|

The return values of the HiSysEventRecord APIs are described as follows:

- **0**: The parsing is successful.
- -**1**: The event fails to be initialized.
- -**2**: The parameter name does not exist.
- -**3**: The type of the parameter value to be parsed does not match the type of the input parameter value.

### How to Develop

#### C++ HiSysEvent Query API

1. Import the corresponding header file:

   ```c++
   #include "hisysevent_manager.h"
   ```

2. Implement the callback API.

   ```c++
   class TestQueryCallback : public HiSysEventQueryCallback {
   public:
       void OnQuery(std::shared_ptr<std::vector<HiSysEventRecord>> sysEvents) override
       {
           if (sysEvents == nullptr) {
           	return;
           }
           for_each((*sysEvents).cbegin(), (*sysEvents).cend(), [](const HiSysEventRecord& event) {
               std::cout << event.AsJson() << std::endl;
           });
       }
   
       void OnComplete(int32_t reason, int32_t total) override
       {
           std::cout << "Query completed" << std::endl;
           return;
       }
   };
   ```

3. Call the query API while passing in the query parameter, rule, and callback object.

   ```c++
   // Create a query parameter object.
   long long startTime = 0;
   long long endTime = 1668245644000; //2022-11-12 09:34:04
   int queryCount = 10;
   QueryArg arg(startTime, endTime, queryCount);
   
   // Create a query rule object.
   QueryRule rule("HIVIEWDFX", { "PLUGIN_LOAD" });
   std::vector<QueryRule> queryRules = { rule };
   
   // Create a query callback object.
   auto queryCallback = std::make_shared<TestQueryCallback>();
   
   // Call the query API.
   HiSysEventManager::Query(arg, queryRules, queryCallback);
   ```

#### C HiSysEvent Query API

1. Import the corresponding header file:

   ```c++
   #include "hisysevent_manager_c.h"
   ```

2. Implement the callback API.

   ```c++
   void OnQueryTest(HiSysEventRecord records[], size_t size)
   {
       for (size_t i = 0; i < size; i++) {
           printf("OnQuery: event=%s", records[i].jsonStr);
       }
   }
   
   void OnCompleteTest(int32_t reason, int32_t total)
   {
       printf("OnCompleted, res=%d, total=%d\n", reason, total);
   }
   ```

3. Call the query API while passing in the query parameter, rule, and callback object.

   ```c++
   // Create a query parameter object.
   HiSysEventQueryArg arg;
   arg.beginTime = 0;
   arg.endTime = 1668245644000; //2022-11-12 09:34:04
   arg.maxEvents = 10;
   
   // Create a query rule object.
   constexpr char TEST_DOMAIN[] = "HIVIEWDFX";
   constexpr char TEST_NAME[] = "PLUGIN_LOAD";
   HiSysEventQueryRule rule;
   (void)strcpy_s(rule.domain, strlen(TEST_DOMAIN) + 1, TEST_DOMAIN);
   (void)strcpy_s(rule.eventList[0], strlen(TEST_NAME) + 1, TEST_NAME);
   rule.eventListSize = 1;
   rule.condition = nullptr;
   HiSysEventQueryRule rules[] = { rule };
   
   // Create a query callback object.
   HiSysEventQueryCallback callback;
   callback.OnQuery = OnQueryTest;
   callback.OnComplete = OnCompleteTest;
   
   // Call the query API.
   OH_HiSysEvent_Query(arg, rules, sizeof(rules) / sizeof(HiSysEventQueryRule), callback);
   ```

### Development Example

#### C++ HiSysEvent Query

Assume that you need to query all **PLUGIN_LOAD** events that are generated for the **HIVIEWDFX** domain until the current time on a service module. The development procedure is as follows:

1. Add the **libhisysevent** and **libhisyseventmanager** dependencies of the **hisysevent_native** component to **BUILD.gn** of the service module.

   ```c++
   external_deps = [
     "hisysevent_native:libhisysevent",
     "hisysevent_native:libhisyseventmanager",
   ]
   ```

2. Call the query API in the **TestQuery()** function of the service module.
   
   ```c++
   #include "hisysevent_manager.h"
   #include <iostream>
   #include <unistd.h>
   
   using namespace OHOS::HiviewDFX;
   
   class TestQueryCallback : public HiSysEventQueryCallback {
   public:
       void OnQuery(std::shared_ptr<std::vector<HiSysEventRecord>> sysEvents) override
       {
           if (sysEvents == nullptr) {
           	return;
           }
           for_each((*sysEvents).cbegin(), (*sysEvents).cend(), [](const HiSysEventRecord& event) {
               std::cout << event.AsJson() << std::endl;
           });
       }
   
       void OnComplete(int32_t reason, int32_t total) override
       {
           std::cout << "Query completed" << std::endl;
           return;
       }
   };
   
   int64_t GetMilliseconds()
   {
       auto now = std::chrono::system_clock::now();
       auto millisecs = std::chrono::duration_cast<std::chrono::milliseconds>(now.time_since_epoch());
       return millisecs.count();
   }
   
   void TestQuery()
   {
       // Create a query parameter object.
       long long startTime = 0;
       long long endTime = GetMilliseconds();
       int maxEvents = 100;
       QueryArg arg(startTime, endTime, maxEvents);
   
       // Create a query rule object.
       QueryRule rule("HIVIEWDFX", { "PLUGIN_LOAD" });
       std::vector<QueryRule> queryRules = { rule };
   
       // Create a query callback object.
       auto queryCallback = std::make_shared<TestQueryCallback>();
   
       // Call the query API.
       int ret = HiSysEventManager::Query(arg, queryRules, queryCallback);
   }
   ```

#### C HiSysEvent Query

Assume that you need to query all **PLUGIN_LOAD** events that are generated for the **HIVIEWDFX** domain until the current time on a service module. The development procedure is as follows:

1. Add the **libhisyseventmanager** dependency of the **hisysevent_native** component to the **BUILD.gn** file of the service module.

   ```c++
   external_deps = [ "hisysevent_native:libhisyseventmanager" ]
   
   // for strcpy_s
   deps = [ "//third_party/bounds_checking_function:libsec_shared" ]
   ```

2. Call the query API in the **TestQuery()** function of the service module.

   ```c++
   #include "hisysevent_manager_c.h"
   #include <securec.h>
   #include <time.h>
     
   void OnQueryTest(HiSysEventRecord records[], size_t size)
   {
       for (size_t i = 0; i < size; i++) {
           printf("OnQuery: event=%s", records[i].jsonStr);
       }
   }
   
   void OnCompleteTest(int32_t reason, int32_t total)
   {
       printf("OnCompleted, res=%d, total=%d\n", reason, total);
   }
   
   int64_t GetMilliseconds()
   {
       return time(NULL);
   }
   
   void TestQuery()
   {
       // Create a query parameter object.
       HiSysEventQueryArg arg;
       arg.beginTime = 0;
       arg.endTime = GetMilliseconds();
       arg.maxEvents = 100;
   
       // Create a query rule object.
       constexpr char TEST_DOMAIN[] = "HIVIEWDFX";
       constexpr char TEST_NAME[] = "PLUGIN_LOAD";
       HiSysEventQueryRule rule;
       (void)strcpy_s(rule.domain, strlen(TEST_DOMAIN) + 1, TEST_DOMAIN);
       (void)strcpy_s(rule.eventList[0], strlen(TEST_NAME) + 1, TEST_NAME);
       rule.eventListSize = 1;
       rule.condition = nullptr;
       HiSysEventQueryRule rules[] = { rule };
   
       // Create a query callback object.
       HiSysEventQueryCallback callback;
       callback.OnQuery = OnQueryTest;
       callback.OnComplete = OnCompleteTest;
   
       // Call the query API.
       int ret = OH_HiSysEvent_Query(arg, rules, sizeof(rules) / sizeof(HiSysEventQueryRule), callback);
   }
   ```
