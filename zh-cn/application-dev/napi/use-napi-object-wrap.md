# Native与ArkTS对象绑定

## 场景介绍

通过`napi_wrap`将ArkTS对象与Native的C++对象绑定，后续操作时再通过`napi_unwrap`将ArkTS对象绑定的C++对象取出，并对其进行操作。

## 使用示例

1. 接口声明、编译配置以及模块注册

   **接口声明**

   ```ts
   // index.d.ts
   export class MyObject {
      constructor(arg: number);
      plusOne: () => number;
   
      public get value();
      public set value(newVal: number);
   }
   ```

   **编译配置**

   ```
   // CMakeLists.txt
   # the minimum version of CMake.
   cmake_minimum_required(VERSION 3.4.1)
   project(object_wrap)
   
   set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})
   
   include_directories(${NATIVERENDER_ROOT_PATH}
                       ${NATIVERENDER_ROOT_PATH}/include)
   
   add_definitions("-DLOG_DOMAIN=0x0000")
   add_definitions("-DLOG_TAG=\"testTag\"")
   
   add_library(object_wrap SHARED object_wrap.cpp)
   target_link_libraries(object_wrap PUBLIC libace_napi.z.so libhilog_ndk.z.so)
   ```

   **模块注册**

   ```cpp
   // object_wrap.cpp
   class MyObject {
    public:
     static napi_value Init(napi_env env, napi_value exports);
     static void Destructor(napi_env env, void* nativeObject, void* finalize_hint);
   
    private:
     explicit MyObject(double value_ = 0);
     ~MyObject();
   
     static napi_value New(napi_env env, napi_callback_info info);
     static napi_value GetValue(napi_env env, napi_callback_info info);
     static napi_value SetValue(napi_env env, napi_callback_info info);
     static napi_value PlusOne(napi_env env, napi_callback_info info);
   
     double value_;
     napi_env env_;
     napi_ref wrapper_;
   };
   
   static thread_local napi_ref g_ref = nullptr;
   
   MyObject::MyObject(double value)
       : value_(value), env_(nullptr), wrapper_(nullptr) {}
   
   MyObject::~MyObject()
   {
     napi_delete_reference(env_, wrapper_);
   }
   
   void MyObject::Destructor(napi_env env,
                             void* nativeObject,
                             [[maybe_unused]] void* finalize_hint)
   {
     OH_LOG_INFO(LOG_APP, "MyObject::Destructor called");
     reinterpret_cast<MyObject*>(nativeObject)->~MyObject();
   }
   
   napi_value MyObject::Init(napi_env env, napi_value exports)
   {
     napi_property_descriptor properties[] = {
         {"value", 0, 0, GetValue, SetValue, 0, napi_default, 0},
         { "plusOne", nullptr, PlusOne, nullptr, nullptr, nullptr, napi_default, nullptr }
     };
   
     napi_value cons;
     assert(napi_define_class(env, "MyObject", NAPI_AUTO_LENGTH, New, nullptr, 2,
                              properties, &cons) == napi_ok);
   
     assert(napi_create_reference(env, cons, 1, &g_ref) == napi_ok);
     assert(napi_set_named_property(env, exports, "MyObject", cons) == napi_ok);
     return exports;
   }
   
   EXTERN_C_START
   static napi_value Init(napi_env env, napi_value exports)
   {
       MyObject::Init(env, exports);
       return exports;
   }
   EXTERN_C_END
   
   static napi_module nativeModule = {
       .nm_version = 1,
       .nm_flags = 0,
       .nm_filename = nullptr,
       .nm_register_func = Init,
       .nm_modname = "object_wrap",
       .nm_priv = nullptr,
       .reserved = { 0 },
   };
   
   extern "C" __attribute__((constructor)) void RegisterObjectWrapModule()
   {
       napi_module_register(&nativeModule);
   }
   ```

2. 在构造函数中绑定ArkTS与C++对象

   ```cpp
   napi_value MyObject::New(napi_env env, napi_callback_info info)
   {
     OH_LOG_INFO(LOG_APP, "MyObject::New called");
   
     napi_value newTarget;
     assert(napi_get_new_target(env, info, &newTarget) == napi_ok);
     if (newTarget != nullptr) {
       // 使用`new MyObject(...)`调用方式
       size_t argc = 1;
       napi_value args[1];
       napi_value jsThis;
       assert(napi_get_cb_info(env, info, &argc, args, &jsThis, nullptr) == napi_ok);
   
       double value = 0.0;
       napi_valuetype valuetype;
       assert(napi_typeof(env, args[0], &valuetype) == napi_ok);
       if (valuetype != napi_undefined) {
         assert(napi_get_value_double(env, args[0], &value) == napi_ok);
       }
   
       MyObject* obj = new MyObject(value);
   
       obj->env_ = env;
       // 通过napi_wrap将ArkTS对象jsThis与C++对象obj绑定
       assert(napi_wrap(env,
                        jsThis,
                        reinterpret_cast<void*>(obj),
                        MyObject::Destructor,
                        nullptr,  // finalize_hint
                        &obj->wrapper_) == napi_ok);
   
       return jsThis;
     } else {
       // 使用`MyObject(...)`调用方式
       size_t argc = 1;
       napi_value args[1];
       assert(napi_get_cb_info(env, info, &argc, args, nullptr, nullptr) == napi_ok && argc == 1);
   
       napi_value cons;
       assert(napi_get_reference_value(env, g_ref, &cons) == napi_ok);
       napi_value instance;
       assert(napi_new_instance(env, cons, argc, args, &instance) == napi_ok);
   
       return instance;
     }
   }
   ```

3. 将ArkTS对象之前绑定的C++对象取出，并对其进行操作

   ```cpp
   napi_value MyObject::GetValue(napi_env env, napi_callback_info info)
   {
     OH_LOG_INFO(LOG_APP, "MyObject::GetValue called");
   
     napi_value jsThis;
     assert(napi_get_cb_info(env, info, nullptr, nullptr, &jsThis, nullptr) == napi_ok);
   
     MyObject* obj;
     // 通过napi_unwrap将jsThis之前绑定的C++对象取出，并对其进行操作
     assert(napi_unwrap(env, jsThis, reinterpret_cast<void**>(&obj)) == napi_ok);
     napi_value num;
     assert(napi_create_double(env, obj->value_, &num) == napi_ok);
   
     return num;
   }
   
   napi_value MyObject::SetValue(napi_env env, napi_callback_info info)
   {
     OH_LOG_INFO(LOG_APP, "MyObject::SetValue called");
   
     size_t argc = 1;
     napi_value value;
     napi_value jsThis;
   
     assert(napi_get_cb_info(env, info, &argc, &value, &jsThis, nullptr) == napi_ok);
   
     MyObject* obj;
     // 通过napi_unwrap将jsThis之前绑定的C++对象取出，并对其进行操作
     assert(napi_unwrap(env, jsThis, reinterpret_cast<void**>(&obj)) == napi_ok);
     assert(napi_get_value_double(env, value, &obj->value_) == napi_ok);
   
     return nullptr;
   }
   
   napi_value MyObject::PlusOne(napi_env env, napi_callback_info info)
   {
     OH_LOG_INFO(LOG_APP, "MyObject::PlusOne called");
   
     napi_value jsThis;
     assert(napi_get_cb_info(env, info, nullptr, nullptr, &jsThis, nullptr) == napi_ok);
   
     MyObject* obj;
     // 通过napi_unwrap将jsThis之前绑定的C++对象取出，并对其进行操作
     assert(napi_unwrap(env, jsThis, reinterpret_cast<void**>(&obj)) == napi_ok);
     obj->value_ += 1;
     napi_value num;
     assert(napi_create_double(env, obj->value_, &num) == napi_ok);
   
     return num;
   }
   ```

4. ArkTS侧示例代码 

   ```ts
   import hilog from '@ohos.hilog';
   import { MyObject } from 'libobject_wrap.so'
   
   let object : MyObject = new MyObject(0);
   object.value = 1023;
   hilog.info(0x0000, 'testTag', 'MyObject value after set: %{public}d', object.value);
   hilog.info(0x0000, 'testTag', 'MyObject plusOne: %{public}d', object.plusOne());
   ```