# \@Provide装饰器和\@Consume装饰器：与后代组件双向同步


\@Provide和\@Consume，应用于与后代组件的双向数据同步，应用于状态数据在多个层级之间传递的场景。不同于上文提到的父子组件之间通过命名参数机制传递，\@Provide和\@Consume摆脱参数传递机制的束缚，实现跨层级传递。


其中\@Provide装饰的变量是在祖先组件中，可以理解为被“提供”给后代的状态变量。\@Consume装饰的变量是在后代组件中，去“消费（绑定）”祖先组件提供的变量。


> **说明：**
>
> 从API version 9开始，这两个装饰器支持在ArkTS卡片中使用。


## 概述

\@Provide/\@Consume装饰的状态变量有以下特性：

- \@Provide装饰的状态变量自动对其所有后代组件可用，即该变量被“provide”给他的后代组件。由此可见，\@Provide的方便之处在于，开发者不需要多次在组件之间传递变量。

- 后代通过使用\@Consume去获取\@Provide提供的变量，建立在\@Provide和\@Consume之间的双向数据同步，与\@State/\@Link不同的是，前者可以在多层级的父子组件之间传递。

- \@Provide和\@Consume可以通过相同的变量名或者相同的变量别名绑定，建议类型相同，否则会发生类型隐式转换，从而导致应用行为异常。


```ts
// 通过相同的变量名绑定
@Provide a: number = 0;
@Consume a: number;

// 通过相同的变量别名绑定
@Provide('a') b: number = 0;
@Consume('a') c: number;
```


\@Provide和\@Consume通过相同的变量名或者相同的变量别名绑定时，\@Provide装饰的变量和\@Consume装饰的变量是一对多的关系。不允许在同一个自定义组件内，包括其子组件中声明多个同名或者同别名的\@Provide装饰的变量，@Provide的属性名或别名需要唯一且确定，如果声明多个同名或者同别名的@Provide装饰的变量，会发生运行时报错。


## 装饰器说明

\@State的规则同样适用于\@Provide，差异为\@Provide还作为多层后代的同步源。

| \@Provide变量装饰器 | 说明                                       |
| -------------- | ---------------------------------------- |
| 装饰器参数          | 别名：常量字符串，可选。<br/>如果指定了别名，则通过别名来绑定变量；如果未指定别名，则通过变量名绑定变量。 |
| 同步类型           | 双向同步。<br/>从\@Provide变量到所有\@Consume变量以及相反的方向的数据同步。双向同步的操作与\@State和\@Link的组合相同。 |
| 允许装饰的变量类型      | Object、class、string、number、boolean、enum类型，以及这些类型的数组。<br/>支持Date类型。<br/>API11及以上支持Map、Set类型。<br/>支持类型的场景请参考[观察变化](#观察变化)。<br/>API11及以上支持上述支持类型的联合类型，比如string \| number, string \| undefined 或者 ClassA \| null，示例见[@Provide_and_Consume支持联合类型实例](#provide_and_consume支持联合类型实例)。 <br/>**注意**<br/>当使用undefined和null的时候，建议显式指定类型，遵循TypeScript类型校验，比如：`@Provide a : string \| undefined = undefined`是推荐的，不推荐`@Provide a: string = undefined`。
<br/>支持ArkUI框架定义的联合类型Length、ResourceStr、ResourceColor类型。<br/>不支持any。| 必须指定类型。<br/>\@Provide变量的\@Consume变量的类型必须相同。|
| 被装饰变量的初始值      | 必须指定。                                    |
| 支持allowOverride参数          | 允许重写，只要声明了allowOverride，则别名和属性名都可以被Override。示例见\@Provide支持allowOverride参数。 |

| \@Consume变量装饰器 | 说明                                       |
| -------------- | ---------------------------------------- |
| 装饰器参数          | 别名：常量字符串，可选。<br/>如果提供了别名，则必须有\@Provide的变量和其有相同的别名才可以匹配成功；否则，则需要变量名相同才能匹配成功。 |
| 同步类型           | 双向：从\@Provide变量（具体请参见\@Provide）到所有\@Consume变量，以及相反的方向。双向同步操作与\@State和\@Link的组合相同。 |
| 允许装饰的变量类型      | Object、class、string、number、boolean、enum类型，以及这些类型的数组。<br/>支持Date类型。<br/>支持类型的场景请参考[观察变化](#观察变化)。<br/>API11及以上支持上述支持类型的联合类型，比如string \| number, string \| undefined 或者 ClassA \| null，示例见[@Provide_and_Consume支持联合类型实例](#provide_and_consume支持联合类型实例)。 <br/>**注意**<br/>当使用undefined和null的时候，建议显式指定类型，遵循TypeScript类型校验，比如：`@Consume a : string \| undefined`。
<br/>支持ArkUI框架定义的联合类型Length、ResourceStr、ResourceColor类型。<br/>不支持any。| 必须指定类型。<br/>\@Provide变量和\@Consume变量的类型必须相同。<br/>\@Consume装饰的变量，在其父组件或者祖先组件上，必须有对应的属性和别名的\@Provide装饰的变量。 |
| 被装饰变量的初始值      | 无，禁止本地初始化。                               |


## 变量的传递/访问规则说明


| \@Provide传递/访问 | 说明                                       |
| -------------- | ---------------------------------------- |
| 从父组件初始化和更新     | 可选，允许父组件中常规变量（常规变量对@Provide赋值，只是数值的初始化，常规变量的变化不会触发UI刷新，只有状态变量才能触发UI刷新）、\@State、\@Link、\@Prop、\@Provide、\@Consume、\@ObjectLink、\@StorageLink、\@StorageProp、\@LocalStorageLink和\@LocalStorageProp装饰的变量装饰变量初始化子组件\@Provide。 |
| 用于初始化子组件       | 允许，可用于初始化\@State、\@Link、\@Prop、\@Provide。 |
| 和父组件同步         | 否。                                       |
| 和后代组件同步        | 和\@Consume双向同步。                          |
| 是否支持组件外访问      | 私有，仅可以在所属组件内访问。                          |


  **图1** \@Provide初始化规则图示  


![zh-cn_image_0000001552614217](figures/zh-cn_image_0000001552614217.png)


| \@Consume传递/访问 | 说明                                       |
| -------------- | ---------------------------------------- |
| 从父组件初始化和更新     | 禁止。通过相同的变量名和alias（别名）从\@Provide初始化。      |
| 用于初始化子组件       | 允许，可用于初始化\@State、\@Link、\@Prop、\@Provide。 |
| 和祖先组件同步        | 和\@Provide双向同步。                          |
| 是否支持组件外访问      | 私有，仅可以在所属组件内访问                           |


  **图2** \@Consume初始化规则图示  


![zh-cn_image_0000001502094666](figures/zh-cn_image_0000001502094666.png)


## 观察变化和行为表现


### 观察变化

- 当装饰的数据类型为boolean、string、number类型时，可以观察到数值的变化。

- 当装饰的数据类型为class或者Object的时候，可以观察到赋值和属性赋值的变化（属性为Object.keys(observedObject)返回的所有属性）。

- 当装饰的对象是array的时候，可以观察到数组的添加、删除、更新数组单元。

- 当装饰的对象是Date时，可以观察到Date整体的赋值，同时可通过调用Date的接口`setFullYear`, `setMonth`, `setDate`, `setHours`, `setMinutes`, `setSeconds`, `setMilliseconds`, `setTime`, `setUTCFullYear`, `setUTCMonth`, `setUTCDate`, `setUTCHours`, `setUTCMinutes`, `setUTCSeconds`, `setUTCMilliseconds` 更新Date的属性。

```ts
@Component
struct CompD {
  @Consume selectedDate: Date;

  build() {
    Column() {
      Button(`child increase the day by 1`)
        .onClick(() => {
          this.selectedDate.setDate(this.selectedDate.getDate() + 1)
        })
      Button('child update the new date')
        .margin(10)
        .onClick(() => {
          this.selectedDate = new Date('2023-09-09')
        })
      DatePicker({
        start: new Date('1970-1-1'),
        end: new Date('2100-1-1'),
        selected: this.selectedDate
      })
    }
  }
}

@Entry
@Component
struct CompA {
  @Provide selectedDate: Date = new Date('2021-08-08')

  build() {
    Column() {
      Button('parent increase the day by 1')
        .margin(10)
        .onClick(() => {
          this.selectedDate.setDate(this.selectedDate.getDate() + 1)
        })
      Button('parent update the new date')
        .margin(10)
        .onClick(() => {
          this.selectedDate = new Date('2023-07-07')
        })
      DatePicker({
        start: new Date('1970-1-1'),
        end: new Date('2100-1-1'),
        selected: this.selectedDate
      })
      CompD()
    }
  }
}
```

- 当装饰的变量是Map时，可以观察到Map整体的赋值，同时可通过调用Map的接口`set`, `clear`, `delete` 更新Map的值。详见[装饰Map类型变量](#装饰map类型变量)。

- 当装饰的变量是Set时，可以观察到Set整体的赋值，同时可通过调用Set的接口`add`, `clear`, `delete` 更新Set的值。详见[装饰Set类型变量](#装饰set类型变量)。

### 框架行为

1. 初始渲染：
   1. \@Provide装饰的变量会以map的形式，传递给当前\@Provide所属组件的所有子组件；
   2. 子组件中如果使用\@Consume变量，则会在map中查找是否有该变量名/alias（别名）对应的\@Provide的变量，如果查找不到，框架会抛出JS ERROR；
   3. 在初始化\@Consume变量时，和\@State/\@Link的流程类似，\@Consume变量会在map中查找到对应的\@Provide变量进行保存，并把自己注册给\@Provide。

2. 当\@Provide装饰的数据变化时：
   1. 通过初始渲染的步骤可知，子组件\@Consume已把自己注册给父组件。父组件\@Provide变量变更后，会遍历更新所有依赖它的系统组件（elementid）和状态变量（\@Consume）；
   2. 通知\@Consume更新后，子组件所有依赖\@Consume的系统组件（elementId）都会被通知更新。以此实现\@Provide对\@Consume状态数据同步。

3. 当\@Consume装饰的数据变化时：

   通过初始渲染的步骤可知，子组件\@Consume持有\@Provide的实例。在\@Consume更新后调用\@Provide的更新方法，将更新的数值同步回\@Provide，以此实现\@Consume向\@Provide的同步更新。

![Provide_Consume_framework_behavior](figures/Provide_Consume_framework_behavior.png)


## 使用场景

在下面的示例是与后代组件双向同步状态\@Provide和\@Consume场景。当分别点击CompA和CompD组件内Button时，reviewVotes 的更改会双向同步在CompA和CompD中。



```ts
@Component
struct CompD {
  // @Consume装饰的变量通过相同的属性名绑定其祖先组件CompA内的@Provide装饰的变量
  @Consume reviewVotes: number;

  build() {
    Column() {
      Text(`reviewVotes(${this.reviewVotes})`)
      Button(`reviewVotes(${this.reviewVotes}), give +1`)
        .onClick(() => this.reviewVotes += 1)
    }
    .width('50%')
  }
}

@Component
struct CompC {
  build() {
    Row({ space: 5 }) {
      CompD()
      CompD()
    }
  }
}

@Component
struct CompB {
  build() {
    CompC()
  }
}

@Entry
@Component
struct CompA {
  // @Provide装饰的变量reviewVotes由入口组件CompA提供其后代组件
  @Provide reviewVotes: number = 0;

  build() {
    Column() {
      Button(`reviewVotes(${this.reviewVotes}), give +1`)
        .onClick(() => this.reviewVotes += 1)
      CompB()
    }
  }
}
```

### 装饰Map类型变量

> **说明：**
>
> 从API version 11开始，\@Provide，\@Consume支持Map类型。

在下面的示例中，message类型为Map<number, string>，点击Button改变message的值，视图会随之刷新。

```ts
@Component
struct Child {
  @Consume message: Map<number, string>

  build() {
    Column() {
      ForEach(Array.from(this.message.entries()), (item: [number, string]) => {
        Text(`${item[0]}`).fontSize(30)
        Text(`${item[1]}`).fontSize(30)
        Divider()
      })
      Button('Consume init map').onClick(() => {
        this.message = new Map([[0, "a"], [1, "b"], [3, "c"]])
      })
      Button('Consume set new one').onClick(() => {
        this.message.set(4, "d")
      })
      Button('Consume clear').onClick(() => {
        this.message.clear()
      })
      Button('Consume replace the first item').onClick(() => {
        this.message.set(0, "aa")
      })
      Button('Consume delete the first item').onClick(() => {
        this.message.delete(0)
      })
    }
  }
}


@Entry
@Component
struct MapSample {
  @Provide message: Map<number, string> = new Map([[0, "a"], [1, "b"], [3, "c"]])

  build() {
    Row() {
      Column() {
        Button('Provide init map').onClick(() => {
          this.message = new Map([[0, "a"], [1, "b"], [3, "c"], [4, "d"]])
        })
        Child()
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### 装饰Set类型变量

> **说明：**
>
> 从API version 11开始，\@Provide，\@Consume支持Set类型。

在下面的示例中，message类型为Set\<number\>，点击Button改变message的值，视图会随之刷新。

```ts
@Component
struct Child {
  @Consume message: Set<number>

  build() {
    Column() {
      ForEach(Array.from(this.message.entries()), (item: [number, string]) => {
        Text(`${item[0]}`).fontSize(30)
        Divider()
      })
      Button('Consume init set').onClick(() => {
        this.message = new Set([0, 1, 2, 3, 4])
      })
      Button('Consume set new one').onClick(() => {
        this.message.add(5)
      })
      Button('Consume clear').onClick(() => {
        this.message.clear()
      })
      Button('Consume delete the first one').onClick(() => {
        this.message.delete(0)
      })
    }
    .width('100%')
  }
}


@Entry
@Component
struct SetSample {
  @Provide message: Set<number> = new Set([0, 1, 2, 3, 4])

  build() {
    Row() {
      Column() {
        Button('Provide init set').onClick(() => {
          this.message = new Set([0, 1, 2, 3, 4, 5])
        })
        Child()
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### Provide_and_Consume支持联合类型实例

@Provide和@Consume支持联合类型和undefined和null，在下面的示例中，count类型为string | undefined，点击父组件Parent中的Button改变count的属性或者类型，Child中也会对应刷新。

```ts
@Component
struct Child {
  // @Consume装饰的变量通过相同的属性名绑定其祖先组件Ancestors内的@Provide装饰的变量
  @Consume count: string | undefined;

  build() {
    Column() {
      Text(`count(${this.count})`)
      Button(`count(${this.count}), Child`)
        .onClick(() => this.count = 'Ancestors')
    }
    .width('50%')
  }
}

@Component
struct Parent {
  build() {
    Row({ space: 5 }) {
      Child()
    }
  }
}

@Entry
@Component
struct Ancestors {
  // @Provide装饰的联合类型count由入口组件Ancestors提供其后代组件
  @Provide count: string | undefined = 'Child';

  build() {
    Column() {
      Button(`count(${this.count}), Child`)
        .onClick(() => this.count = undefined)
      Parent()
    }
  }
}
```

### \@Provide支持allowOverride参数

allowOverride：\@Provide重写选项。

> **说明：**
>
> 从API version 11开始使用。

| 名称   | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| allowOverride | string | 否 | 是否允许@Provide重写。允许在同一组件树下通过allowOverride重写同名的@Provide。如果开发者未写allowOverride，定义同名的@Provide，运行时会报错。 |

```ts
@Component
struct MyComponent {
  @Provide({allowOverride : "reviewVotes"}) reviewVotes: number = 10;
}
```

```ts
@Component
struct GrandSon {
  // @Consume装饰的变量通过相同的属性名绑定其祖先内的@Provide装饰的变量
  @Consume("reviewVotes") reviewVotes: number;

  build() {
    Column() {
      Text(`reviewVotes(${this.reviewVotes})`) // Text显示10
      Button(`reviewVotes(${this.reviewVotes}), give +1`)
        .onClick(() => this.reviewVotes += 1)
    }
    .width('50%')
  }
}

@Component
struct Child {
  @Provide({ allowOverride: "reviewVotes" }) reviewVotes: number = 10;

  build() {
    Row({ space: 5 }) {
      GrandSon()
    }
  }
}

@Component
struct Parent {
  @Provide({ allowOverride: "reviewVotes" }) reviewVotes: number = 20;

  build() {
    Child()
  }
}

@Entry
@Component
struct GrandParent {
  @Provide("reviewVotes") reviewVotes: number = 40;

  build() {
    Column() {
      Button(`reviewVotes(${this.reviewVotes}), give +1`)
        .onClick(() => this.reviewVotes += 1)
      Parent()
    }
  }
}
```

在上面的示例中：
- GrandParent声明了@Provide("reviewVotes") reviewVotes: number = 40
- Parent是GrandParent的子组件，声明@Provide为allowOverride，重写父组件GrandParent的@Provide("reviewVotes") reviewVotes: number = 40。如果不设置allowOverride，则会抛出运行时报错，提示@Provide重复定义。Child同理。
- GrandSon在初始化@Consume的时候，@Consume装饰的变量通过相同的属性名绑定其最近的祖先的@Provide装饰的变量。
- GrandSon查找到相同属性名的@Provide在祖先Child中，所以@Consume("reviewVotes") reviewVotes: number初始化数值为10。如果Child中没有定义与@Consume同名的@Provide，则继续向上寻找Parent中的同名@Provide值为20，以此类推。
- 如果查找到根节点还没有找到key对应的@Provide，则会报初始化@Consume找不到@Provide的报错。


## 常见问题

### \@BuilderParam尾随闭包情况下\@Provide未定义错误

在此场景下，CustomWidget执行this.builder()创建子组件CustomWidgetChild时，this指向的是HomePage。因此找不到CustomWidget的\@Provide变量，所以下面示例会报找不到\@Provide错误，和\@BuilderParam连用的时候要谨慎this的指向。

错误示例：

```ts
class Tmp {
  a: string = ''
}

@Entry
@Component
struct HomePage {
  @Builder
  builder2($$: Tmp) {
    Text(`${$$.a}测试`)
  }

  build() {
    Column() {
      CustomWidget() {
        CustomWidgetChild({ builder: this.builder2 })
      }
    }
  }
}

@Component
struct CustomWidget {
  @Provide('a') a: string = 'abc';
  @BuilderParam
  builder: () => void;

  build() {
    Column() {
      Button('你好').onClick(() => {
        if (this.a == 'ddd') {
          this.a = 'abc';
        }
        else {
          this.a = 'ddd';
        }

      })
      this.builder()
    }
  }
}

@Component
struct CustomWidgetChild {
  @Consume('a') a: string;
  @BuilderParam
  builder: ($$: Tmp) => void;

  build() {
    Column() {
      this.builder({ a: this.a })
    }
  }
}
```

正确示例：

```ts
class Tmp {
  name: string = ''
}

@Entry
@Component
struct HomePage {
  @Provide('name') name: string = 'abc';

  @Builder
  builder2($$: Tmp) {
    Text(`${$$.name}测试`)
  }

  build() {
    Column() {
      Button('你好').onClick(() => {
        if (this.name == 'ddd') {
          this.name = 'abc';
        } else {
          this.name = 'ddd';
        }
      })
      CustomWidget() {
        CustomWidgetChild({ builder: this.builder2 })
      }
    }
  }
}

@Component
struct CustomWidget {
  @BuilderParam
  builder: () => void;

  build() {
    this.builder()
  }
}

@Component
struct CustomWidgetChild {
  @Consume('name') name: string;
  @BuilderParam
  builder: ($$: Tmp) => void;

  build() {
    Column() {
      this.builder({ name: this.name })
    }
  }
}
```
