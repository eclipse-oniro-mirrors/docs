# 使用picker管理联系人

## 接口说明

| 接口名                  | 描述                                       |
| --------------------- | ------------------------------------------ |
| addContactViaUI(context: Context, contact: Contact): Promise&lt;number&gt; | 调用新建联系人接口，打开新建联系人UI界面，新建完成。使用Promise异步回调。 |
| saveToExistingContactViaUI(context: Context, contact: Contact): Promise&lt;number&gt; | 调用保存至已有联系人接口，选择联系人UI界面并完成编辑。使用Promise异步回调。 |


## 使用picker新建联系人

调用新建联系人接口，打开新建联系人UI界面，用户可在UI界面中填写并新建联系人。

```js
import { common } from '@kit.AbilityKit';
import { contact } from '@kit.ContactsKit';


@Entry
@Component
struct Index {
  @State message: string = 'Hello World';
    
  build() {
    Column() {
      Text(this.message)
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
        .onClick(() => {
          let contactInfo: contact.Contact = {
            name: {
              fullName: 'xxx'
            },
            phoneNumbers: [{
              phoneNumber: '138xxxxxx'
            }]
          }
          let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
          let promise = contact.addContactViaUI(context, contactInfo);
        })
    }
  }
}
```

## 使用picker更新联系人信息

可以通过拉起picker，将选中的联系人信息更新到现有联系人中。

```js
import { common } from '@kit.AbilityKit';
import { contact } from '@kit.ContactsKit';


@Entry
@Component
struct Index {
  @State message: string = 'Hello World';
    
  build() {
    Column() {
      Text(this.message)
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
        .onClick(() => {
          let contactInfo: contact.Contact = {
            id: 1,
            name: {
              fullName: 'xxx'
            },
            phoneNumbers: [{
              phoneNumber: '138xxxxxx'
            }]
          }
          let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
          let promise = contact.saveToExistingContactViaUI(context, contactInfo);
        })
    }
  }
}
``` 