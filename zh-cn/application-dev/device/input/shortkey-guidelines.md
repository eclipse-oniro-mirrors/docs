# 快捷键开发指导

## 场景介绍

快捷键可以设置快捷键拉起Ability的延迟时间，比如按下快捷键五秒后截屏等。

## 导入模块

```js
import shortKey from '@ohos.multimodalInput.shortKey';
```

## 接口说明

事件注入常用接口如下表所示，接口详细介绍请参考[ohos.multimodalInput.shortKey文档](../../reference/apis-input-kit/js-apis-shortKey-sys.md)。

| 接口名称  | 描述 |
| ------------------------------------------------------------ | -------------------------- |
| setKeyDownDuration(businessKey: string, delay: number, callback: AsyncCallback&lt;void&gt;): void |设置快捷键拉起Ability的延迟时间。 |

## 开发步骤

开发步骤以按下快捷键五秒后截屏为例。

```js
import shortKey from '@ohos.multimodalInput.shortKey';
try {
  shortKey.setKeyDownDuration("screenshot", 500, (error) => {//设置截屏应用screenshot延迟时间为5秒（500毫秒）
    if (error) {
      console.log(`Set key down duration failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set key down duration success`);
  });
} catch (error) {
  console.log(`Set key down duration failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```


