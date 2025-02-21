# FA模型的Context


FA模型下只有一个Context。Context中的所有功能都是通过方法来提供的，它提供了一些featureAbility中不存在的方法，相当于featureAbility的一个扩展和补全。


## 接口说明

FA模型下使用Context，需要通过featureAbility下的接口getContext来获取，而在此之前，需要先导入对应的包：


```ts
import featureAbility from "@ohos.ability.featureAbility";
```

然后使用如下方式获取对应的Context对象：


```ts
let context = featureAbility.getContext()
```

最终返回的对象为Context，其对应的接口说明请参见[接口文档](../reference/apis/js-apis-inner-app-context.md)。


## 开发步骤

1. 查询Bundle信息。
   
   ```ts
   import featureAbility from '@ohos.ability.featureAbility'
   export default {
     onCreate() {
       // 获取context并调用相关方法
       let context = featureAbility.getContext();
       context.getBundleName((data, bundleName)=>{
         console.info("ability bundleName:" + bundleName)
       });
       console.info('Application onCreate')
     },
     onDestroy() {
       console.info('Application onDestroy')
     },
   }
   ```

2. 设置当前featureAbility的显示方向。
   
   ```ts
   import featureAbility from '@ohos.ability.featureAbility'
   import bundle from '@ohos.bundle';
   
   export default {
     onCreate() {
       // 获取context并调用相关方法
       let context = featureAbility.getContext();
       context.setDisplayOrientation(bundle.DisplayOrientation.LANDSCAPE).then(() => {
           console.info("Set display orientation.")
       })
       console.info('Application onCreate')
     },
     onDestroy() {
       console.info('Application onDestroy')
     },
   }
   ```
