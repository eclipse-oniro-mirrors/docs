# \@Sendable装饰器：声明并校验Sendable类

## 简介
在使用[TaskPool](../reference/apis-arkts/js-apis-taskpool.md)时，执行的并发函数若需要传输类对象且使用该类的内部方法，该类需要使用此装饰器修饰，否则无法使用此对象内的方法。Sendable class有以下两种行为：

- 支持Sendable class序列化。对象分配在各自的虚拟机内存空间，不存在竞争访问，不同线程可以同时读写。

- 支持Sendable class在跨线程传递时的引用传递（暂不支持）。


> **说明：**
>
> 从API version 11开始，支持使用@Sendable装饰器校验Sendable class。
>
> 当前该装饰器仅支持克隆拷贝，使用时需搭配[setCloneList](../reference/apis-arkts/js-apis-taskpool.md#setclonelist11)，否则会抛异常。

## 基本概念

 **Sendable class**：被@Sendable装饰器修饰的类为Sendable class。


## 装饰器说明
| \@Sendable类装饰器         | 说明                                                                   |
| ------------------------- | ---------------------------------------------------------------------- |
| 装饰器参数                 | 无。                                                                   |
| 使用场景限制               | 仅支持在Stage模型的工程中使用。仅支持在.ets文件中使用。                    |
| 装饰的类继承关系限制        | Sendable class只能继承Sendable class，普通Class可以继承Sendable class。  |
| 装饰的对象内的属性类型限制  | 支持string、number、boolean、Sendable class。禁止使用闭包变量。不支持#定义私有属性，需用private。不支持计算属性。           |
| 装饰的对象内的属性的其他限制 | 成员属性必须显式初始化。成员属性不能跟问号和感叹号。|
| 装饰的对象内的方法参数限制  | 允许使用local变量、入参和通过import引入的变量。禁止使用闭包变量。           |
| Sendable Class的限制      | 不支持增加属性、不支持删除属性、允许修改属性，修改前后属性的类型必须一致、不支持修改方法。必须声明或定义在文件顶层，不能定义在函数内。   |
| 其他限制                  | 导出Sendable class的文件，不能导出非Sendable class属性。只能标记class，不支持interface和enum。   |
| 适用场景                  | 在TaskPool使用类方法或传输对象的数据量较大的场景中推荐使用该装饰器。         |


## 装饰器使用示例

```ts
@Sendable
class TaskpoolTestClass {
  desc: string = "sendable: this is TaskpoolTestClass ";
  taskNum: number = 5;
  printName() {
    console.info("sendable: TaskpoolTestClass desc is: " + this.desc);
  }
  get getTaskNum(): number {
    return this.taskNum;
  }
}
```

