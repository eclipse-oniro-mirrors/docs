# 从TypeScript到ArkTS的迁移指导

本文通过提供简洁的约束指导如何将标准的TypeScript代码重构为ArkTS代码。尽管ArkTS是基于TypeScript设计的，但出于性能考虑，一些TypeScript的特性被限制了。因此，在ArkTS中，所有的TypeScript特性被分成三类。 

1. **完全支持的特性**：原始代码无需任何修改。根据测试，对于已遵循最佳TypeScript实践的项目，代码库中90%到97%的内容可以保持原封不动。
2. **部分支持的特性**：需小规模的代码重构。例如，必须使用关键字`let`代替`var` 来声明变量。注意，根据本文提供的约束进行代码重构后，您的代码仍为有效的TypeScript代码。
3. **不支持的特性**：需大规模的代码重构。例如，不支持`any`类型，所有使用`any`的代码都需要引入显式类型。

本文将逐一介绍所有部分支持和所有不支持的特性，并提供代码重构的建议。对于没有提到的特性，则说明ArkTS完全支持。

**示例**

包含关键字`var`的原始TypeScript代码：

```typescript
function addTen(x: number): number {
    var ten = 10
    return x + ten
}
```

重构后的代码：

```typescript
// 重要！重构后仍然是有效的TypeScript代码。
function addTen(x: number): number {
    let ten = 10
    return x + ten
}
```

**不支持的特性**

目前，不支持的特性主要包括：

- 与降低运行时性能的动态类型相关的特性。
- 需要编译器额外支持从而导致项目构建时间增加的特性。

根据开发者的反馈以及更多实际场景的数据，我们将来可能进一步**缩小**不支持特性的范围。

## 概述

本节罗列了ArkTS不支持或部分支持的TypeScript特性。完整的列表以及详细的代码示例和重构建议，请参考[约束说明](#约束说明)。

### 强制使用静态类型

ArkTS在设计之初，就确定了如下目标：

- ArkTS代码需非常容易阅读和理解，因为代码的阅读频率高于编写频率。
- 以最小功耗快速执行代码，这点对于移动设备（ArkTS的目标设备）来说至关重要。

静态类型是ArkTS最重要的特性之一。使用静态类型有助于实现上述两个目标。如果程序采用静态类型，即所有类型在编译时都是已知的，那么开发者就能够容易理解代码中使用了哪些数据结构。同时，由于所有类型在程序实际运行前都是已知的，编译器可以提前验证代码的正确性，从而可以减少运行时类型检查项，有助于性能提升。

基于上述考虑，ArkTS中禁止使用`any`类型。

**示例**

```typescript
//
// 不支持：
//

let res : any = some_api_function("hello", "world")

// `res`是什么？错误代码的数字？字符串？对象？
// 该如何处理它？

//
// 支持：
//

class CallResult {
    public succeeded() : boolean { ... }
    public errorMessage() : string { ... }
}

let res : CallResult = some_api_function("hello", "world")
if (!res.succeeded()) {
    console.log("Call failed: " + res.errorMessage())
}
```

`any`类型在TypeScript中并不常见，只有大约1%的TypeScript代码库使用。一些代码检查工具（例如ESLint）也制定一系列规则来禁止使用`any`。因此，虽然禁止`any` 将导致代码重构，但重构量很小，有助于整体性能提升，因此这个约束是非常有价值的。

### 禁止在运行时变更对象布局

为实现最佳性能，ArkTS要求在程序执行期间不能更改对象的布局。换句话说，ArkTS禁止以下行为：

- 向对象中添加新的属性或方法
- 从对象中删除已有的属性或方法
- 将任意类型的值赋值给对象属性

TypeScript编译器已经禁止了许多此类操作。然而，有些操作还是有可能绕过编译器的，例如，使用ArkTS不支持的`as any`进行转换。（详见下面的示例。）

**示例**

```typescript
class Point {
    public x : number = 0
    public y : number = 0

    constructor(x : number, y : number) {
        this.x = x
        this.y = y
    }
}

// 无法从对象中删除某个属性，从而确保所有Point对象都具有属性x：
let p1 = new Point(1.0, 1.0)
delete p1.x           // 无论使用TypeScript还是ArkTS，都会产生编译时错误
delete (p1 as any).x  // 使用TypeScript时，不会报错；使用ArkTS时，会产生编译时错误

// Point类没有定义命名为`z`的属性，在程序运行时也无法添加该属性：
let p2 = new Point(2.0, 2.0)
p2.z = "Label";         // 无论使用TypeScript还是ArkTS，都会产生编译时错误
(p2 as any).z = "Label" // 使用TypeScript时，不会报错；使用ArkTS时，会产生编译时错误

// 确保所有Point对象只有属性x和y，并且无法产生一些任意标识符并将其用作新属性：
let p3 = new Point(3.0, 3.0)
let prop = Symbol();     // 使用TypeScript时，不会报错；使用ArkTS时，会产生编译时错误
(p3 as any)[prop] = p3.x // 使用TypeScript时，不会报错；使用ArkTS时，会产生编译时错误
p3[prop] = p3.x          // 无论使用TypeScript还是ArkTS，都会产生编译时错误

// 确保所有Point对象都具有number类型的属性x和y。因此，无法赋予其他类型的值给该属性：
let p4 = new Point(4.0, 4.0)
p4.x = "Hello!";         // 无论使用TypeScript还是ArkTS，都会产生编译时错误
(p4 as any).x = "Hello!" // 使用TypeScript时，不会报错；使用ArkTS时，会产生编译时错误

// 使用符合类定义的Point对象：
function distance(p1 : Point, p2 : Point) : number {
    return Math.sqrt(
      (p2.x - p1.x) * (p2.x - p1.x) + (p2.y - p1.y) * (p2.y - p1.y)
    )
}
let p5 = new Point(5.0, 5.0)
let p6 = new Point(6.0, 6.0)
console.log("Distance between p5 and p6: " + distance(p5, p6))
```

不可预测的对象布局修改会影响代码的可读性以及运行时性能。从开发者的角度来说，在某处定义类，然后又在其他地方修改实际的对象布局，很容易引起困惑乃至引入错误。此外，这点还需要额外的运行时支持，增加了执行开销。这一点与静态类型的约束也冲突：既然已决定使用显式类型，为什么还需要添加或删除属性呢？

当前，只有少数项目允许在运行时变更对象布局，一些常用的代码检查工具也增加了相应的限制规则。这个约束只会导致少量代码重构，但对性能提升会有积极的影响。

### 限制运算符的语义

为获得更好的性能并鼓励开发者编写更清晰的代码，ArkTS限制了一些运算符的语义。详细的语义限制，请参考[约束说明](#约束说明)。

**示例**

```typescript
// 运算符`+`可以用于数字和字符串，但不能用于其他类型：
class C {
    // ...
}
let c1 : C = new C()
let c2 : C = new C()
console.log(c1 + c2) // 编译时报错
```

使用额外的语义重载语言运算符会增加语言规范的复杂度，而且，开发者还被迫牢记所有可能的例外情况及对应的处理规则。在某些情况下，产生一些不必要的运行时开销。

当前只有不到1%的代码库使用该特性。因此，尽管限制运算符的语义需要重构代码，但重构量很小且非常容易操作，并且，通过重构能使代码更清晰、具备更高性能。

### （暂时）不支持 structural typing

假设两个不相关的类`T`和`U`拥有相同的公共API：

```typescript
class T {
    public name : string = ""

    public greet() : void {
        console.log("Hello, " + this.name)
    }
}

class U {
    public name : string = ""

    public greet() : void {
        console.log("Greetings, " + this.name)
    }
}
```

我们能把类型为`T`的值赋给类型为`U`的变量吗？

```typescript
let u : U = new T() // 是否允许？
```

我们能把类型为`T`的值传递给接受类型为`U`的参数的函数吗？

```typescript
function greeter(u : U) {
    console.log("To " + u.name)
    u.greet()
}

let t : T = new T()
greeter(t) // 是否允许？
```

换句话说，我们将采取下面哪种方法呢：

- `T`和`U`没有继承关系或没有任何公共接口，但由于它们具有相同的公共API，它们“在某种程度上是相等的”，所以上述两个问题的答案都是“是”；
- `T`和`U`没有继承关系或没有任何公共接口，应当始终被视为完全不同的类型，因此上述两个问题的答案都是“否”。

采用第一种方法的语言支持structural typing，而采用第二种方法的语言则不支持structural typing。目前TypeScript支持structural typing，而ArkTS不支持。

structural typing是否有助于生成清晰、易理解的代码，关于这一点并没有定论。但至少有一点很明确，structural typing不会降低程序的性能（至少在某些时候）。那为什么ArkTS不支持structural typing呢？

因为对structural typing的支持是一个重大的特性，需要在语言规范、编译器和运行时进行大量的考虑和仔细的实现。另外，安全高效的实现还要考虑到其他方面（静态类型、更改对象布局的限制）。鉴于此，当前我们还不支持该特性。根据实际场景的需求和反馈，我们后续会重新加以考虑。更多案例和建议请参考[约束说明](#约束说明)。

## 约束说明

### 仅支持属性名称为标识符的对象

**规则：**`arkts-identifiers-as-prop-names`

**级别：错误**

ArkTS不支持属性名称为数字或字符串的对象。通过属性名访问类的属性，通过数值索引访问数组元素。

**TypeScript**

```typescript
var x = {"name": 1, 2: 3}

console.log(x["name"])
console.log(x[2])
```

**ArkTS**

```typescript
class X {
    public name: number
}
let x = {name: 1}
console.log(x.name)

let y = [1, 2, 3]
console.log(y[2])

// 在需要通过非标识符（即不同类型的key）获取数据的场景中，使用Map<Object, some_type>:
let z = new Map<Object, number>()
z.set("name", 1)
z.set(2, 2)
console.log(z.get("name"))
console.log(z.get(2))
```

**相关约束**

* 不支持Symbol() API
* 访问未定义的属性将导致编译时错误
* 不支持delete运算符
* 仅允许在表达式中使用typeof运算符
* 不支持in运算符
* 禁止运行时检查对象属性
* 不支持声明动态属性
* 限制使用标准库


### 不支持`Symbol()`API

**规则：**`arkts-no-symbol`

**级别：错误**

TypeScript中的`Symbol()` API用于在运行时生成唯一的属性名称。由于该API的常见使用场景在静态类型语言中没有意义，因此，ArkTS不支持`Symbol()` API。在ArkTS中，对象布局在编译时就确定了，且不能在运行时被更改。

**TypeScript**

```typescript
const sym = Symbol()
let o = {
   [sym]: "value"
}
```

**ArkTS**

```typescript
class SomeClass {
    public someProperty : string
}
let o = new SomeClass()
```

**相关约束**

* 仅支持属性名为标识符的对象
* 访问未定义的属性将导致编译时错误
* 不支持delete运算符
* 仅允许在表达式中使用typeof运算符
* 不支持in运算符
* 禁止运行时检查对象属性
* 不支持声明动态属性
* 限制使用标准库

### 不支持带“#”符号的私有修饰符

**规则：**`arkts-no-private-identifiers`

**级别：错误**

ArkTS不支持以`#`符号开头的私有修饰符。改用 `private`关键字。

**TypeScript**

```typescript
class C {
    #foo: number = 42
}
```

**ArkTS**

```typescript
class C {
    private foo: number = 42
}
```

### 类型、命名空间等的命名必须唯一

**规则：**`arkts-unique-names`

**级别：错误**

类型、命名空间等的命名必须唯一，且能够与变量名等其他名称区分开来。

**TypeScript**

```typescript
let X: string
type X = number[] // 类型的别名与变量同名
```

**ArkTS**

```typescript
let X: string
type T = number[] // 为避免名称冲突，此处不允许使用X
```

### 使用`let`而非`var`

**规则：**`arkts-no-var`

**级别：错误**

ArkTS不支持 `var`，请始终使用`let`代替。

**TypeScript**

```typescript
function f(shouldInitialize: boolean) {
    if (shouldInitialize) {
       var x = 10
    }
    return x
}

console.log(f(true))  // 10
console.log(f(false)) // undefined

let upper_let = 0
{
    var scoped_var = 0
    let scoped_let = 0
    upper_let = 5
}
scoped_var = 5 // 可见
scoped_let = 5 // 编译时错误
```

**ArkTS**

```typescript
function f(shouldInitialize: boolean): Object {
    let x: Object = new Object()
    if (shouldInitialize) {
        x = 10
    }
    return x
}

console.log(f(true))  // 10
console.log(f(false)) // {}

let upper_let = 0
let scoped_var = 0
{
    let scoped_let = 0
    upper_let = 5
}
scoped_var = 5
scoped_let = 5 //编译时错误
```

### 使用具体的类型而非`any`、`undefined`或`unknown`

**规则：**`arkts-no-any-undefined-unknown`

**级别：错误**

ArkTS不支持`any`、`undefined`和`unknown`类型。显式指定具体类型。

**TypeScript**

```typescript
var x
console.log(x) // undefined

var y: any
console.log(y) // undefined
```

**ArkTS**

```typescript
// 所有变量都应显式指定其具体类型：
let x: Object = {}
console.log(x) // {}
```

**相关约束**

* 使用Object[]而非tuple

### `bigint`不是内置类型，不支持带后缀`n`的数字字面量

**规则：**`arkts-no-n-suffix`

**级别：错误**

在ArkTS中，`bigint`是标准库的一部分，而非一种内置类型。不支持带后缀`n`的数字字面量。使用`BigInt`工厂函数生成`bigint`类型的值。

**TypeScript**

```typescript
let a: bigint = 1n
```

**ArkTS**

```typescript
let a = BigInt(1)
let b: bigint = BigInt(2)
```

### 使用`Object[]`而非tuple

**规则：**`arkts-no-tuples`

**级别：错误**

当前ArkTS不支持tuple。可以使用`Object[]`来代替tuple。

**TypeScript**

```typescript
var t: [number, string] = [3, "three"]
var n = t[0]
var s = t[1]
```

**ArkTS**

```typescript
let t: Object[] = [3, "three"]
let n = t[0]
let s = t[1]
```

### 使用`class` 而非具有call signature的类型

**规则：**`arkts-no-call-signatures`

**级别：错误**

ArkTS不支持对象类型中包含call signature。改用类。

**TypeScript**

```typescript
type DescribableFunction = {
    description: string
    (someArg: number): string // call signature
}

function doSomething(fn: DescribableFunction): void {
    console.log(fn.description + " returned " + fn(6))
}
```

**ArkTS**

```typescript
class DescribableFunction {
    description: string
    public invoke(someArg: number): string {
        return someArg.toString()
    }
    constructor() {
        this.description = "desc"
    }
}

function doSomething(fn: DescribableFunction): void {
    console.log(fn.description + " returned " + fn.invoke(6))
}

doSomething(new DescribableFunction())
```

**相关约束**

* 使用class而非具有构造函数签名的类型

### 使用`class`而非具有构造函数签名的类型

**规则：**`arkts-no-ctor-signatures-type`

**级别：错误**

ArkTS不支持对象类型中的构造函数签名。改用类。

**TypeScript**

```typescript
class SomeObject {}

type SomeConstructor = {
    new (s: string): SomeObject
}

function fn(ctor: SomeConstructor) {
    return new ctor("hello")
}
```

**ArkTS**

```typescript
class SomeObject {
    public f: string
    constructor (s: string) {
        this.f = s
    }
}

function fn(s: string): SomeObject {
    return new SomeObject(s)
}
```

**相关约束**

* 使用class而非具有call signature的类型

### 仅支持一个静态块

**规则：**`arkts-no-multiple-static-blocks`

**级别：错误**

ArkTS不允许类中有多个静态块。如果存在多个静态块语句，请合并到一个静态块中。

**TypeScript**

```typescript
class C {
    static s: string

    static {
        C.s = "aa"
    }
    static {
        C.s = C.s + "bb"
    }
}
```

**ArkTS**

```typescript
class C {
    static s: string

    static {
        C.s = "aa"
        C.s = C.s + "bb"
    }
}
```

### 不支持index signature

**规则：**`arkts-no-indexed-signatures`

**级别：错误**

ArkTS不允许index signature。改用数组。

**TypeScript**

```typescript
// 带index signature的接口：
interface StringArray {
    [index: number]: string
}

function getStringArray() : StringArray {
    return ["a", "b", "c"]
}

const myArray: StringArray = getStringArray()
const secondItem = myArray[1]
```

**ArkTS**

```typescript
class X {
    public f: string[]
}

let myArray: X = new X()
const secondItem = myArray.f[1]
```

### 使用继承而非intersection type

**规则：**`arkts-no-intersection-types`

**级别：错误**

目前ArkTS不支持intersection type。可以使用继承作为替代方案。

**TypeScript**

```typescript
interface Identity {
    id: number
    name: string
}

interface Contact {
    email: string
    phone: string
}

type Employee = Identity & Contact
```

**ArkTS**

```typescript
interface Identity {
    id: number
    name: string
}

interface Contact {
    email: string
    phone: string
}

interface Employee extends Identity,  Contact {}
```

### 不支持返回`this`类型

**规则：**`arkts-no-this-as-return-type`

**级别：错误**

ArkTS不支持返回`this`类型。改用显式具体类型。

**TypeScript**

```typescript
interface ListItem {
    getHead(): this
}
```

**ArkTS**

```typescript
interface ListItem {
    getHead(): ListItem
}
```

### 不支持条件类型

**规则：**`arkts-no-conditional-types`

**级别：错误**

ArkTS不支持条件类型别名。引入带显式约束的新类型，或使用`Object`重写逻辑。不支持`infer`关键字。

**TypeScript**

```typescript
type X<T> = T extends number ? T : never

type Y<T> = T extends Array<infer Item> ? Item : never
```

**ArkTS**

```typescript
// 在类型别名中提供显式约束
type X1<T extends number> = T

// 用Object重写，这种情况下，类型控制较少，需要更多的类型检查以确保安全
type X2<T> = Object

// Item必须作为泛型参数使用，并能正确实例化
type YI<Item, T extends Array<Item>> = Item
```

### 可选参数不能使用primitive type

**规则：**`arkts-no-opt-params`

**级别：错误**

ArkTS中，可选参数的类型不能为primitive type。可以使用默认参数或引用类型。对于引用类型，可选参数缺省值为`null`。

**TypeScript**

```typescript
// x为可选参数：
function f(x?: number) {
    console.log(x) // 打印undefined或某个数字
}

// x为带默认值的必选参数：
function g(x: number = 1) {
    console.log(x)
}
```

**ArkTS**

```typescript
// 使用引用类型（缺省值为null）：
function f(x?: Number) {
    console.log(x) // 打印null或某个数字
}

// 使用带默认值的必选参数：
function g(x: number = 1) {
    console.log(x)
}
```

### 不支持在`constructor`中声明字段

**规则：**`arkts-no-ctor-prop-decls`

**级别：错误**

ArkTS不支持在`constructor`中声明类字段。在`class`中声明这些字段。

**TypeScript**

```typescript
class Person {
    constructor(
        protected ssn: string,
        private firstName: string,
        private lastName: string
    ) {
        this.ssn = ssn
        this.firstName = firstName
        this.lastName = lastName
    }

    getFullName(): string {
        return this.firstName + " " + this.lastName
    }
}
```

**ArkTS**

```typescript
class Person {
    protected ssn: string
    private firstName: string
    private lastName: string

    constructor(ssn: string, firstName: string, lastName: string) {
        this.ssn = ssn
        this.firstName = firstName
        this.lastName = lastName
    }

    getFullName(): string {
        return this.firstName + " " + this.lastName
    }
}
```

### 接口中不支持构造函数签名

**规则：**`arkts-no-ctor-signatures-iface`

**级别：错误**

ArkTS不支持接口中的构造函数签名。改用方法。

**TypeScript**

```typescript
interface I {
    new (s: string): I
}

function fn(i: I) {
    return new i("hello")
}
```

**ArkTS**

```typescript
interface I {
    create(s: string): I
}

function fn(i: I) {
    return i.create("hello")
}
```

**相关约束**

* 使用class而非具有构造函数签名的类型

### 不支持索引访问类型

**规则：**`arkts-no-aliases-by-index`

**级别：错误**

ArkTS不支持索引访问类型。改用类型别名。

**TypeScript**

```typescript
type Point = {x: number, y: number}
type N = Point["x"] // 等同于number
```

**ArkTS**

```typescript
class Point {x: number = 0; y: number = 0}
type N = number
```

### 不支持索引访问字段

**规则：**`arkts-no-props-by-index`

**级别：错误**

ArkTS不支持针对类字段的索引访问。改用点操作符。

**TypeScript**

```typescript
class Point {x: number = 0; y: number = 0}
let p: Point = {x: 1, y: 2}
let x = p["x"]
```

**ArkTS**

```typescript
class Point {x: number = 0; y: number = 0}
let p: Point = {x: 1, y: 2}
let x = p.x
```

### 不支持structural identity

**规则：**`arkts-no-structural-identity`

**级别：错误**

目前ArkTS不支持structural identity，即编译器无法比较两种类型的公共API并决定它们是否相同。可改用其他机制，例如继承、接口或类型别名。

对于下面的示例，类型`X`和`Y`在TypeScript中是等价的（可互换），而在ArkTS中，他们是不等价的。

**TypeScript**

```typescript
interface X {
    f(): string
}

interface Y { // Y等于X
    f(): string
}
```

**ArkTS**

```typescript
interface X {
    f(): string
}

type Y = X // Y等于X
```

**相关约束**

* 子类型/父类型不支持structural typing
* 赋值检查不支持structural typing
* 类型推断不支持structural typing

### 子类型/父类型不支持structural typing

**规则：**`arkts-no-structural-subtyping`

**级别：错误**

当前ArkTS在类型推导时不会检查structural是否相同，即编译器无法比较两种类型的公共API并决定它们是否相同。改用其他机制，例如继承或接口。

**TypeScript**

```typescript
class X {
    public foo: number

    constructor() {
        this.foo = 0
    }
}

class Y {
    public foo: number

    constructor() {
        this.foo = 0
    }
}

let x = new X()
let y = new Y()

console.log("Assign X to Y")
y = x

console.log("Assign Y to X")
x = y
```

**ArkTS**

```typescript
class X {
    public foo: number

    constructor() {
        this.foo = 0
    }
}

// Y从X派生，显式定义继承关系
class Y extends X {
    constructor() {
        super()
    }
}

let x = new X()
let y = new Y()

console.log("Assign Y to X")
x = y // ok, X是Y的父类

// 不能将X赋值给Y
// y = x -编译时错误
```

**相关约束**

* 不支持structural identity
* 赋值检查不支持structural typing
* 类型推断不支持structural typing

### 赋值检查不支持structural typing

**规则：**`arkts-no-structural-assignability`

**级别：错误**

当前ArkTS在检查变量是否可相互赋值时不检查结构等价性，即编译器无法比较两种类型的公共API并决定它们是否相同。改用其他机制，例如继承或接口。

**TypeScript**

```typescript
class X {
    public foo: number

    constructor() {
       this.foo = 0
    }
}

class Y {
    public foo: number
    constructor() {
        this.foo = 0
    }
}

let x = new X()
let y = new Y()

console.log("Assign X to Y")
y = x

console.log("Assign Y to X")
x = y
```

**ArkTS**

```typescript
interface Z {
   foo: number
}

// X实现了接口Z，显示化定义了X和Y之间的关系。
class X implements Z {
    public foo: number

    constructor() {
       this.foo = 0
    }
}

// Y实现了接口Z，显示化定义了X和Y之间的关系。
class Y implements Z {
    public foo: number

    constructor() {
       this.foo = 0
    }
}

let x: Z = new X()
let y: Z = new Y()

console.log("Assign X to Y")
y = x // ok，两者类型相同

console.log("Assign Y to X")
x = y // ok，两者类型相同
```

**相关约束**

* 不支持structural identity
* 子类型/父类型不支持structural typing
* 类型推断不支持structural typing

### 可选属性的的类型不能为primitive type

**规则：**`arkts-no-opt-props`

**级别：错误**

ArkTS中，可选属性的类型不能为primitive type。使用默认值或引用类型。对于引用类型，可选属性缺省值为`null`。该规则同样适用于类和接口。

**TypeScript**

```typescript
class CompilerOptions {
    strict?: boolean
    sourcePath?: string
    targetPath?: string
}

let options: CompilerOptions = {
    strict: true,
    sourcePath: "./src"
}

if (options.targetPath == undefined) {
    // 一些代码
}
```

**ArkTS**

```typescript
class CompilerOptions {
    strict: boolean = false
    sourcePath: string = ""
    targetPath?: string
}

let options: CompilerOptions = {
    strict: true,
    sourcePath: "./src"
    // targetPath的值为null
}

if (options.targetPath == null) {
    // 一些代码
}
```

### 显式标注泛型函数类型实参，除非可以推断出类型实参

**规则：**`arkts-no-inferred-generic-params`

**级别：错误**

如果可以从传递给泛型函数的参数中推断出具体类型，ArkTS允许省略泛型类型实参。否则，会发生编译时错误。禁止仅基于函数返回类型推断泛型类型参数。

**TypeScript**

```typescript
function choose<T>(x: T, y: T): T {
    return Math.random() < 0.5 ? x : y
}

let x = choose(10, 20)   // OK，推断choose<number>(...)
let y = choose("10", 20) // 编译时错误

function greet<T>(): T {
    return "Hello" as T
}
let z = greet() // x的类型被推断为“unknown”
```

**ArkTS**

```typescript
function choose<T>(x: T, y: T): T {
    return Math.random() < 0.5 ? x : y
}

let x = choose(10, 20)   // OK，推断choose<number>(...)
let y = choose("10", 20) // 编译时错误

function greet<T>(): T {
    return "Hello" as T
}
let z = greet<string>()
```

### 类型推断不支持structural typing

**规则：**`arkts-no-structural-inference`

**级别：错误**

当前ArkTS不支持structural typing，即编译器无法比较两种类型的公共API并决定它们是否相同。使用继承和接口显式指定类型之间的关系。

**TypeScript**

```typescript
class X  {
    public foo: number
    private s: string

    constructor (f: number) {
        this.foo = f
        this.s = ""
    }

    public say(): void {
       console.log("X = ", this.foo)
    }
}

class Y {
    public foo: number

    constructor (f: number) {
        this.foo = f
    }
    public say(): void {
        console.log("Y = ", this.foo)
    }
}

function bar(z: X): void {
    z.say()
}

// X和Y具有相同的公共API，因此它们是等价的。
// 允许第二次调用
bar(new X(1))
bar(new Y(2) as X)
```

**ArkTS**

```typescript
interface Z {
   say(): void
}

class X implements Z {
    public foo: number
    private s: string

    constructor (f: number) {
        this.foo = f
        this.s = ""
    }
    public say(): void {
        console.log("X = ", this.foo)
    }
}

class Y implements Z {
    public foo: number

    constructor (f: number) {
        this.foo = f
    }
    public say(): void {
        console.log("Y = ", this.foo)
    }
}

function bar(z: Z): void {
    z.say()
}

// X和Y实现了相同的接口Z，因此两个调用均允许：
bar(new X(1))
bar(new Y(2))
```

**相关约束**

* 不支持structural identity
* 子类型/父类型不支持structural typing
* 赋值检查不支持structural typing

### 不支持使用正则字面量

**规则：**`arkts-no-regexp-literals`

**级别：错误**

当前ArkTS不支持正则字面量。改用通过`RegExp()`创建。

**TypeScript**

```typescript
let regex: RegExp = /bc*d/
```

**ArkTS**

```typescript
let regex: RegExp = new RegExp("/bc*d/")
```

### 对象字面量必须对应显式声明的类或接口

**规则：**`arkts-no-untyped-obj-literals`

**级别：错误**

如果编译器可以推断对象字面量对应于哪些类或接口，则可以使用对象字面量。否则，将发生编译时错误。具体来说，在以下上下文中不支持使用字面量初始化类和接口：

* 初始化具有`any`、`Object`或`object`类型的任何对象
* 初始化带有方法的类或接口
* 初始化有自定义且有参数的构造函数的类
* 初始化带`readonly`字段的类

**TypeScript**

```typescript
let o1 = {n: 42, s: "foo"}
let o2: Object = {n: 42, s: "foo"}
let o3: object = {n: 42, s: "foo"}

let oo: Object[] = [{n: 1, s: "1"}, {n: 2, s: "2"}]

class C2 {
    s: string
    constructor(s: string) {
        this.s = "s =" + s
    }
}
let o4: C2 = {s: "foo"}

class C3 {
    readonly n: number = 0
    readonly s: string = ""
}
let o5: C3 = {n: 42, s: "foo"}

abstract class A {}
let o6: A = {}

class C4 {
    n: number = 0
    s: string = ""
    f() {
        console.log("Hello")
    }
}
let o7: C4 = {n: 42, s: "foo", f : () => {}}

class Point {
    x: number = 0
    y: number = 0
}

function id_x_y(o: Point): Point {
    return o
}

// structural typing用于推断p为Point
let p = {x: 5, y: 10}
id_x_y(p)

// 可通过上下文推断出对象字面量的类型为Point
id_x_y({x: 5, y: 10})
```

**ArkTS**

```typescript
class C1 {
    n: number = 0
    s: string = ""
}

let o1: C1 = {n: 42, s: "foo"}
let o2: C1 = {n: 42, s: "foo"}
let o3: C1 = {n: 42, s: "foo"}

let oo: C1[] = [{n: 1, s: "1"}, {n: 2, s: "2"}]

class C2 {
    s: string
    constructor(s: string) {
        this.s = "s =" + s
    }
}
let o4 = new C2("foo")

class C3 {
    n: number = 0
    s: string = ""
}
let o5: C3 = {n: 42, s: "foo"}

abstract class A {}
class C extends A {}
let o6: C = {} // 或 let o6: C = new C()

class C4 {
    n: number = 0
    s: string = ""
    f() {
        console.log("Hello")
    }
}
let o7 = new C4()
o7.n = 42
o7.s = "foo"

class Point {
    x: number = 0
    y: number = 0

    // 在字面量初始化之前，使用constructor()创建一个有效对象。
    // 由于Point没有其它构造函数，编译器将自动添加一个默认构造函数。
}

function id_x_y(o: Point): Point {
    return o
}

// 字面量初始化需要显式定义类型
let p: Point = {x: 5, y: 10}
id_x_y(p)

// id_x_y预计接受Point类型，字面量初始化生成一个Point的新实例
id_x_y({x: 5, y: 10})
```

**相关约束**

* 对象字面量不能用于类型声明
* 数组字面量必须仅包含可推断类型的元素

### 对象字面量不能用于类型声明

**规则：**`arkts-no-obj-literals-as-types`

**级别：错误**

ArkTS不支持使用对象字面量声明类型。需显式声明类和接口。

**TypeScript**

```typescript
let o: {x: number, y: number} = {
    x: 2,
    y: 3
}

type S = Set<{x: number, y: number}>
```

**ArkTS**

```typescript
class O {
    x: number
    y: number
}

let o: O = {x: 2, y: 3}

type S = Set<O>
```

**相关约束**

* 对象字面量必须对应某些显式声明的类或接口
* 数组字面量必须仅包含可推断类型的元素

### 数组字面量必须仅包含可推断类型的元素

**规则：**`arkts-no-noninferrable-arr-literals`

**级别：错误**

本质上，ArkTS将数组字面量的类型推断为数组内容的联合类型。如果其中任何一个元素的类型无法根据上下文推导出来（例如，未类型化的对象字面量），则会发生编译时错误。

**TypeScript**

```typescript
let a = [{n: 1, s: "1"}, {n: 2, s : "2"}]
```

**ArkTS**

```typescript
class C {
    n: number = 0
    s: string = ""
}

let a1 = [{n: 1, s: "1"} as C, {n: 2, s : "2"} as C] // a1的类型为“C[]”
let a2: C[] = [{n: 1, s: "1"}, {n: 2, s : "2"}]      // a2的类型为“C[]”
```

**相关约束**

* 对象字面量必须对应某些显式声明的类或接口
* 对象字面量不能用于类型声明

### Lambda函数的参数类型必须显式化

**规则：**`arkts-explicit-param-types-in-lambdas`

**级别：错误**

当前ArkTS要求显式标注lambda函数的参数的类型。

**TypeScript**

```typescript
let f = (s) => { // 隐式定义类型为any
    console.log(s)
}
```

**ArkTS**

```typescript
// lambda函数的参数类型必须显式化
let f = (s: string) => {
    console.log(s)
}
```

### 使用箭头函数而非函数表达式

**规则：**`arkts-no-func-expressions`

**级别：错误**

ArkTS不支持函数表达式。使用箭头函数。

**TypeScript**

```typescript
let f = function (s: string) {
    console.log(s)
}
```

**ArkTS**

```typescript
let f = (s: string) => {
    console.log(s)
}
```

### 使用泛型函数而非泛型箭头函数

**规则：**`arkts-no-generic-lambdas`

**级别：错误**

ArkTS不支持泛型箭头函数。

**TypeScript**

```typescript
let generic_arrow_func = <T extends String> (x: T) => { return x }

generic_arrow_func("string")
```

**ArkTS**

```typescript
function generic_func<T extends String>(x: T): T {
    return x
}

generic_func<String>("string")
```

### 不支持使用类表达式

**规则：**`arkts-no-class-literals`

**级别：错误**

ArkTS不支持使用类表达式。必须显式声明一个类。

**TypeScript**

```typescript
const Rectangle = class {
    constructor(height: number, width: number) {
        this.heigth = height
        this.width = width
    }

    heigth
    width
}

const rectangle = new Rectangle(0.0, 0.0)
```

**ArkTS**

```typescript
class Rectangle {
    constructor(height: number, width: number) {
        this.heigth = height
        this.width = width
    }

    heigth: number
    width: number
}

const rectangle = new Rectangle(0.0, 0.0)
```

### 类不允许被`implements`

**规则：**`arkts-implements-only-iface`

**级别：错误**

ArkTS不允许类被`implements`，只有接口可以被`implements`。

**TypeScript**

```typescript
class C {
  foo() {}
}

class C1 implements C {
  foo() {}
}
```

**ArkTS**

```typescript
interface C {
  foo()
}

class C1 implements C {
  foo() {}
}
```

### 访问未定义的属性将导致编译时错误

**规则：**`arkts-no-undefined-prop-access`

**级别：错误**

ArkTS仅支持访问那些在类中已声明或通过继承可访问的属性。禁止访问任何其他属性，否则会导致编译时错误。使用恰当的类型可以帮助编译期进行类型检查，确定属性是否存在。

**TypeScript**

```typescript
let person = {name: "Bob", isEmployee: true}

let n = person["name"]
let e = person["isEmployee"]
let s = person["office"] // undefined
```

**ArkTS**

```typescript
class Person {
    constructor(name: string, isEmployee: boolean) {
        this.name = name
        this.isEmployee = isEmployee
    }

    name: string
    isEmployee: boolean
}

let person = new Person("Bob", true)
let n = person.name
let e = person.isEmployee
let s = person.office // 编译时错误
```

**相关约束**

* 仅支持属性名称为标识符的对象
* 不支持Symbol() API
* 不支持delete运算符
* 仅允许在表达式中使用typeof运算符
* 不支持in运算符
* 禁止运行时检查对象属性
* 不支持声明动态属性
* 限制使用标准库

### 类型转换仅支持`as T`语法

**规则：**`arkts-as-casts`

**级别：错误**

在ArkTS中，`as`关键字是类型转换的唯一语法。错误的类型转换会导致编译时错误或者运行时抛出`ClassCastException`异常。不支持使用`<type>`语法进行类型转换。

**TypeScript**

```typescript
class Shape {}
class Circle extends Shape {x: number = 5}
class Square extends Shape {y: string = "a"}

function createShape(): Shape {
    return new Circle()
}

let c1 = <Circle> createShape()

let c2 = createShape() as Circle

// 如果转换错误，不会产生编译时或运行时报错
let c3 = createShape() as Square
console.log(c3.y) // undefined
```

**ArkTS**

```typescript
class Shape {}
class Circle extends Shape {x: number = 5}
class Square extends Shape {y: string = "a"}

function createShape(): Shape {
    return new Circle()
}

let c2 = createShape() as Circle

// 运行时抛出ClassCastException异常：
let c3 = createShape() as Square
```

### 不支持JSX表达式

**规则：**`arkts-no-jsx`

**级别：错误**

不支持使用JSX。

### 一元运算符`+`、`-`和`~`仅适用于数值类型

**规则：**`arkts-no-polymorphic-unops`

**级别：错误**

ArkTS仅允许一元运算符用于数值类型，否则会发生编译时错误。与TypeScript不同，ArkTS不支持隐式将字符串转换成数值，必须进行显示转换。

**TypeScript**

```typescript
let a = +5   // 5为number
let b = +"5" // 5为number
let c = -5   // -5为number
let d = -"5" // -5为number
let e = ~5   // -6为number
let f = ~"5" // -6为number
let g = +"string" // NaN为number
```

**ArkTS**

```typescript
let a = +5   // 5为number
let b = +"5" // 编译时错误
let c = -5   // -5为number
let d = -"5" // 编译时错误
let e = ~5   // -6为number
let f = ~"5" // 编译时错误
let g = +"string" // 编译时错误
```

**相关约束**

* 二元运算符\*、/、%、-、<<、>>、>>>、&、^ 和|仅适用于数值类型
* 二元运算符+仅支持数字和字符串的隐式转换

### 一元运算符`+`不能将任何类型转换为数值类型

**规则：**`arkts-no-unary-plus-cast`

**级别：错误**

ArkTS不支持使用一元运算符`+`将任何类型转换为数值类型，该运算符只能用于数值类型。

**TypeScript**

```typescript
function returnTen(): string {
    return "-10"
}

function returnString(): string {
    return "string"
}

let a = +returnTen()    // -10为数值
let b = +returnString() // NaN
```

**ArkTS**

```typescript
function returnTen(): string {
    return "-10"
}

function returnString(): string {
    return "string"
}

let a = +returnTen()    // 编译时错误
let b = +returnString() // 编译时错误
```

**相关约束**

* 一元运算符+、-和~仅适用于数值类型
* 二元运算符\*、/、%、-、<<、>>、>>>、&、^ 和|仅适用于数值类型
* 二元运算符+仅支持数字和字符串的隐式转换

### 不支持`delete`运算符

**规则：**`arkts-no-delete`

**级别：错误**

ArkTS中，对象布局在编译时就确定了，且不能在运行时被更改。因此，删除属性的操作没有意义。

**TypeScript**

```typescript
class Point {
    x?: number = 0.0
    y?: number = 0.0
}

let p = new Point()
delete p.y
```

**ArkTS**

```typescript
// 可以声明一个可空类型并使用null作为缺省值
class Point {
    x: number | null
    y: number | null
}

let p = new Point()
p.y = null
```

**相关约束**

* 仅支持属性名称为标识符的对象
* 不支持Symbol() API
* 访问未定义的属性将导致编译时错误
* 仅允许在表达式中使用typeof运算符
* 不支持in运算符
* 禁止运行时检查对象属性
* 不支持声明动态属性

### 仅允许在表达式中使用`typeof`运算符

**规则：**`arkts-no-type-query`

**级别：错误**

ArkTS仅支持在表达式中使用`typeof`运算符。不允许使用`typeof`作为类型。

**TypeScript**

```typescript
let n1 = 42
let s1 = "foo"
console.log(typeof n1) // "number"
console.log(typeof s1) // "string"
let n2: typeof n1
let s2: typeof s1
```

**ArkTS**

```typescript
let n1 = 42
let s1 = "foo"
console.log(typeof n1) // "number"
console.log(typeof s1) // "string"
let n2: number
let s2: string
```

**相关约束**

* 仅支持属性名称为标识符的对象
* 不支持Symbol() API
* 访问未定义的属性将导致编译时错误
* 不支持delete运算符
* 不支持in运算符
* 禁止运行时检查对象属性
* 不支持声明动态属性
* 限制使用标准库

### 二元运算符`*`、`/`、`%`、`-`、`<<`、`>>`、`>>>`、`&`、`^`和`|`仅适用于数值类型

**规则：**`arkts-no-polymorphic-binops`

**级别：错误**

在ArkTS中，二元运算符`*`、`/`、`%`、`-`，`<<`、`>>`、`>>>`、`&`、`^`和`|`仅可用于数值类型。不支持将其他类型隐式转换为数值类型，否则会导致编译时错误。

**TypeScript**

```typescript
let a = (5 & 5)     // 5
let b = (5.5 & 5.5) // 5，非5.5
let c = (5 | 5)     // 5
let d = (5.5 | 5.5) // 5，非5.5

enum Direction {
    Up = -1,
    Down
}
let e = Direction.Up >> 1 // -1
let f = Direction.Up >>> 1 // 2147483647

let g = ("10" as any) << 1  // 20
let h = ("str" as any) << 1 // 0

let i = 10 * 5
let j = 10 / 5
let k = 10 % 5
let l = 10 - 5
```

**ArkTS**

```typescript
let a = (5 & 5)     // 5
let b = (5.5 & 5.5) // 编译时错误
let c = (5 | 5)     // 5
let d = (5.5 | 5.5) // 编译时错误

enum Direction {
    Up,
    Down
}

let e = Direction.Up >> 1  // 0
let f = Direction.Up >>> 1 // 0

let i = 10 * 5
let j = 10 / 5
let k = 10 % 5
let l = 10 - 5
```

**相关约束**

* 一元运算符+、-和~仅适用于数值类型
* 一元运算符`+`不能将任何类型转换为数值类型
* 二元运算符+仅支持数字和字符串的隐式转换

### 二元运算符+仅支持数字和字符串的隐式转换

**规则：**`arkts-no-polymorphic-plus`

**级别：错误**

ArkTS支持使用`+`对字符串和数字进行隐式转换。其他情形下，都需要显式转换为字符串。

**TypeScript**

```typescript
enum E { E1, E2 }

let a = 10 + 32   // 42
let b = E.E1 + 10 // 10
let c = 10 + "5"  // "105"

let d = "5" + E.E2 // "51"
let e = "Hello, " + "world!" // "Hello, world!"
let f = "string" + true // "stringtrue"

let g = (new Object()) + "string" // "[object Object]string"
```

**ArkTS**

```typescript
enum E { E1, E2 }

let a = 10 + 32   // 42
let b = E.E1 + 10 // 10
let c = 10 + "5"  // "105"

let d = "5" + E.E2 // "51"
let e = "Hello, " + "world!" // "Hello, world!"
let f = "string" + true // "stringtrue"

let g = (new Object()).toString() + "string"
```

**相关约束**

* 一元运算符+、-和~仅适用于数值类型
* 一元运算符`+`不能将任何类型转换为数值类型
* 二元运算符\*、/、%、-、<<、>>、>>>、&、^ 和|仅适用于数值类型

### 部分支持`instanceof`运算符

**规则：**`arkts-instanceof-ref-types`

**级别：错误**

在TypeScript中，`instanceof`运算符的左操作数的类型必须为`any`类型、对象类型，或者它是类型参数，否则结果为`false`。在ArkTS中，`instanceof`运算符的左操作数的类型必须为引用类型，否则会发生编译时错误。此外，在ArkTS中，`instanceof`运算符的左操作数不能是类型。

**TypeScript**

```typescript
class X {}

let a = (new X()) instanceof Object // true
let b = (new X()) instanceof X // true
// 左操作数是类型
let c = X instanceof Object // true
let d = X instanceof X // false

// 左操作数的类型不是any类型
let e = (5.0 as Number) instanceof Number // false
```

**ArkTS**

```typescript
class X {}

let a = (new X()) instanceof Object // true
let b = (new X()) instanceof X // true
// 左操作数是类型
let c = X instanceof Object // 编译时错误
let d = X instanceof X // 编译时错误

// 左操作数可以为任何引用类型，如Number
let e = (5.0 as Number) instanceof Number // true
```

### 不支持`in`运算符

**规则：**`arkts-no-in`

**级别：错误**

由于在ArkTS中，对象布局在编译时是已知的并且在运行时无法修改，因此，不支持`in`运算符。如果仍需检查某些类成员是否存在，使用`instanceof`代替。

**TypeScript**

```typescript
class Person {
    name: string = ""
}
let p = new Person()

let b = "name" in p // true
```

**ArkTS**

```typescript
class Person {
    name: string = ""
}
let p = new Person()

let b = p instanceof Person // true，且属性name一定存在
```

**相关约束**

* 仅支持属性名称为标识符的对象
* 不支持Symbol() API
* 访问未定义的属性将导致编译时错误
* 不支持delete运算符
* 仅允许在表达式中使用typeof运算符
* 禁止运行时检查对象属性
* 不支持声明动态属性
* 限制使用标准库

### 不支持解构赋值

**规则：**`arkts-no-destruct-assignment`

**级别：错误**

ArkTS不支持解构赋值。可使用其他替代方法，例如，使用临时变量。

**TypeScript**

```typescript
let [one, two] = [1, 2]; // 此处需要分号
[one, two] = [two, one]

let head, tail
[head, ...tail] = [1, 2, 3, 4]
```

**ArkTS**

```typescript
let arr: number[] = [1, 2]
let one = arr[0]
let two = arr[1]

let tmp = one
one = two
two = tmp

let data: Number[] = [1,2,3,4]
let head = data[0]
let tail = new Array(data.length - 1)
for (let i = 1; i < data.length; ++i) {
    tail[i - 1] = data[i]
}
```

### 逗号运算符`,`仅用在`for`循环语句中

**规则：**`arkts-no-comma-outside-loops`

**级别：错误**

为了方便理解执行顺序，在ArkTS中，逗号运算符`,`仅适用于`for`循环语句中。

**TypeScript**

```typescript
for (let i = 0, j = 0; i < 10; ++i, j += 2) {
    console.log(i)
    console.log(j)
}

let x = 0
x = (++x, x++) // 1
```

**ArkTS**

```typescript
for (let i = 0, j = 0; i < 10; ++i, j += 2) {
    console.log(i)
    console.log(j)
}

// 通过语句表示执行顺序，而非逗号运算符
let x = 0
++x
x = x++
```

### 不支持解构变量声明

**规则：**`arkts-no-destruct-decls`

**级别：错误**

ArkTS不支持解构变量声明。它是一个依赖于结构兼容性的动态特性并且解构声明中的名称必须和被解构对象中的属性名称一致。

**TypeScript**

```typescript
class Point {
    x: number = 0.0
    y: number = 0.0
}

function returnZeroPoint(): Point {
    return new Point()
}

let {x, y} = returnZeroPoint()
```

**ArkTS**

```typescript
class Point {
    x: number = 0.0
    y: number = 0.0
}

function returnZeroPoint(): Point {
    return new Point()
}

// 创建一个局部变量来处理每个字段：
let zp = returnZeroPoint()
let x = zp.x
let y = zp.y
```

### 不支持隐含类型的推断

**规则：**`arkts-no-implied-inference`

**级别：错误**

目前ArkTS不支持隐含类型的推断，改用显式的类型标注。如果容器中有不同类型的数据，请使用`Object[]`。

**TypeScript**

```typescript
let [a, b, c] = [1, "hello", true]
```

**ArkTS**

```typescript
let a = 1
let b = "hello"
let c = true

let arr: Object[] = [1, "hello", true]
let a1 = arr[0]
let b1 = arr[1]
let c1 = arr[2]
```

### 不支持在catch语句标注类型

**规则：**`arkts-no-types-in-catch`

**级别：错误**

在TypeScript的catch语句中，只能标注类型为`any`或`unknown`。由于ArkTS不支持这些类型，应省略类型注释。

**TypeScript**

```typescript
try {
    // 一些代码
}
catch (a: unknown) {}
```

**ArkTS**

```typescript
try {
    // 一些代码
}
catch (a) {}
```

**相关约束**

* 限制throw语句中表达式的类型

### 不支持`for .. in`

**规则：**`arkts-no-for-in`

**级别：错误**

由于在ArkTS中，对象布局在编译时是确定的、并且不能在运行时被改变，所以不支持使用`for .. in`迭代一个对象的属性。对于数组来说，可以使用常规的`for`循环。

**TypeScript**

```typescript
let a: number[] = [1.0, 2.0, 3.0]
for (let i in a) {
    console.log(a[i])
}
```

**ArkTS**

```typescript
let a: number[] = [1.0, 2.0, 3.0]
for (let i = 0; i < a.length; ++i) {
    console.log(a[i])
}
```

**相关约束**

* 不支持可迭代接口
* for-of仅适用于数组和字符串

### 不支持可迭代接口

**规则：**`arkts-noiterable`

**级别：错误**

ArkTS不支持`Symbol` API、`Symbol.iterator`和最终可迭代的接口。请使用数组和标准库中的容器。

**相关约束**

* 不支持Symbol() API
* 不支持for .. in
* for-of仅支持数组和字符串

### `for-of`仅适用于数组和字符串

**规则：**`arkts-for-of-str-arr`

**级别：错误**

ArkTS支持通过`for .. of`迭代数组和字符串，但不支持迭代对象。

**TypeScript**

```typescript
let a: Set<number> = new Set([1, 2, 3])
for (let s of a) {
    console.log(s)
}
```

**ArkTS**

```typescript
let a: Set<number> = new Set([1, 2, 3])
let numbers = a.values()
for (let n of numbers) {
    console.log(n)
}
```

**相关约束**

* 不支持for .. in
* 不支持可迭代接口

### 不支持映射类型

**规则：**`arkts-no-mapped-types`

**级别：错误**

ArkTS不支持映射类型。使用其他语法来表示相同的语义。

**TypeScript**

```typescript
type OptionsFlags<Type> = {
    [Property in keyof Type]: boolean
}
```

**ArkTS**

```typescript
class C {
    n: number = 0
    s: string = ""
}

class CFlags {
    n: boolean = false
    s: boolean = false
}
```

**相关约束**

* 不支持keyof运算符

### 不支持`with`语句

**规则：**`arkts-no-with`

**级别：错误**

ArkTS不支持`with`语句。使用其他语法来表示相同的语义。

### `case`语句仅支持编译期值

**规则：**`arkts-no-computed-case`

**级别：错误**

在ArkTS中，`case`语句仅支持编译期值。若值无法在编译期确定，请使用`if`语句。

**TypeScript**

```typescript
let x = 2
let y = 3
switch (x) {
    case 1:
        console.log(1)
        break
    case 2:
        console.log(2)
        break
    case y:
        console.log(y)
        break
    default:
        console.log("other")
}
```

**ArkTS**

```typescript
let x = 2
switch (x) {
    case 1:
        console.log(1)
        break
    case 2:
        console.log(2)
        break
    case 3:
        console.log(3)
        break
    default:
        console.log("other")
}
```

### 限制`switch`语句中表达式的类型

**规则：**`arkts-limited-switch`

**级别：错误**

ArkTS支持`switch`语句中使用`number`, `Number`, `string`, `String` 或者`enum`类型的值。其他情况下请使用`if`语句。

**TypeScript**

```typescript
class Point {
    x: number = 0
    y: number = 0
}

let a = new Point()

switch (a) {
    case null: break
    default: console.log("not null")
}
```

**ArkTS**

```typescript
class Point {
    x: number = 0
    y: number = 0
}

let a = new Point()

if (a != null) {
    console.log("not null")
}
```

### 限制`throw`语句中表达式的类型

**规则：**`arkts-limited-throw`

**级别：错误**

ArkTS只支持抛出`Error`类或其派生类的实例。禁止抛出其他类型（例如`number`或`string`）的数据。

**TypeScript**

```typescript
throw 4
throw ""
throw new Error()
```

**ArkTS**

```typescript
throw new Error()
```

### 限制省略函数返回类型标注

**规则：**`arkts-no-implicit-return-types`

**级别：错误**

ArkTS在部分场景中支持对函数返回类型进行推断。当`return`语句中的表达式是对某个函数或方法进行调用，且该函数或方法的返回类型没有被显著标注时，会出现编译时错误。在这种情况下，请标注函数返回类型。

**TypeScript**

```typescript
function f(x: number) {
    if (x <= 0) {
        return x
    }
    return g(x)
}

function g(x: number) {
    return f(x - 1)
}

function doOperation(x: number, y: number) {
    return x + y
}

console.log(f(10))
console.log(doOperation(2, 3))
```

**ArkTS**

```typescript
// 需标注返回类型：
function f(x: number) : number {
    if (x <= 0) {
        return x
    }
    return g(x)
}

// 需标注返回类型：
function g(x: number) : number {
    return f(x - 1)
}

// 可以省略返回类型
function doOperation(x: number, y: number) {
    return x + y
}

console.log(f(10))
console.log(doOperation(2, 3))
```

### 不支持参数解构的函数声明

**规则：**`arkts-no-destruct-params`

**级别：错误**

ArkTS要求实参必须直接传递给函数，且必须指定到形参。

**TypeScript**

```typescript
function drawText({ text = "", location: [x, y] = [0, 0], bold = false }) {
    console.log(text)
    console.log(x)
    console.log(y)
    console.log(bold)
}

drawText({ text: "Hello, world!", location: [100, 50], bold: true })
```

**ArkTS**

```typescript
function drawText(text: String, location: number[], bold: boolean) {
    let x = location[0]
    let y = location[1]
    console.log(text)
    console.log(x)
    console.log(y)
    console.log(bold)
}

function main() {
    drawText("Hello, world!", [100, 50], true)
}
```

### 不支持在函数内声明函数

**规则：**`arkts-no-nested-funcs`

**级别：错误**

ArkTS不支持在函数内声明函数。改用lambda函数。

**TypeScript**

```typescript
function addNum(a: number, b: number): void {

    // 函数内声明函数：
    function logToConsole(message: String): void {
        console.log(message)
    }

    let result = a + b

    // 调用函数：
    logToConsole("result is " + result)
}
```

**ArkTS**

```typescript
function addNum(a: number, b: number): void {
    // 使用lambda函数代替声明函数：
    let logToConsole: (message: string) => void = (message: string): void => {
        console.log(message)
    }

    let result = a + b

    logToConsole("result is " + result)
}
```

### 不支持在函数中使用`this`

**规则：**`arkts-no-standalone-this`

**级别：错误**

ArkTS不支持在函数中使用`this`。只能在方法中使用`this`。

**TypeScript**

```typescript
function foo(i: number) {
    this.count = i
}

class A {
    count: number = 1
    m = foo
}

let a = new A()
console.log(a.count) // 打印“1”
a.m(2)
console.log(a.count) // 打印“2”
```

**ArkTS**

```typescript
class A {
    count: number = 1
    m(i: number): void {
        this.count = i
    }
}

function main(): void {
    let a = new A()
    console.log(a.count)  // 打印"1"
    a.m(2)
    console.log(a.count)  // 打印"2"
}
```

**相关约束**

* 不支持Function.apply、Function.bind以及Function.call

### 不支持生成器函数

**规则：**`arkts-no-generators`

**级别：错误**

目前ArkTS不支持生成器函数。使用`async`或`await`机制进行并行任务处理。

**TypeScript**

```typescript
function* counter(start: number, end: number) {
    for (let i = start; i <= end; i++) {
        yield i
    }
}

for (let num of counter(1, 5)) {
    console.log(num)
}
```

**ArkTS**

```typescript
async function complexNumberProcessing(n : number) : Promise<number> {
    //一些代码逻辑
    return n
}

async function foo() {
    for (let i = 1; i <= 5; i++) {
        console.log(await complexNumberProcessing(i))
    }
}

foo()
```

### 使用`instanceof`和`as`进行类型保护

**规则：**`arkts-no-is`

**级别：错误**

ArkTS不支持`is`运算符，必须用`instanceof`运算符替代。在使用之前，必须使用`as`运算符将对象转换为需要的类型。

**TypeScript**

```typescript
class Foo {
    foo: number = 0
    common: string = ""
}

class Bar {
    bar: number = 0
    common: string = ""
}

function isFoo(arg: any): arg is Foo {
    return arg.foo !== undefined
}

function doStuff(arg: Foo | Bar) {
    if (isFoo(arg)) {
        console.log(arg.foo)    // OK
        console.log(arg.bar)    // 编译时错误
    } else {
        console.log(arg.foo)    // 编译时错误
        console.log(arg.bar)    // OK
    }
}

doStuff({ foo: 123, common: '123' })
doStuff({ bar: 123, common: '123' })
```

**ArkTS**

```typescript
class Foo {
    foo: number = 0
    common: string = ""
}

class Bar {
    bar: number = 0
    common: string = ""
}

function isFoo(arg: Object): boolean {
    return arg instanceof Foo
}

function doStuff(arg: Object): void {
    if (isFoo(arg)) {
        let fooArg = arg as Foo
        console.log(fooArg.foo)     // OK
        console.log(arg.bar)        // 编译时错误
    } else {
        let barArg = arg as Bar
        console.log(arg.foo)        // 编译时错误
        console.log(barArg.bar)     // OK
    }
}

function main(): void {
    doStuff(new Foo())
    doStuff(new Bar())
}
```

### 不支持`keyof`运算符

**规则：**`arkts-no-keyof`

**级别：错误**

在ArkTS中，由于对象布局在编译时就确定了，且不能在运行时被更改，因此，不支持使用`keyof`运算符。直接访问对象的属性。

**TypeScript**

```typescript
class Point {
    x: number = 1
    y: number = 2
}

type PointKeys = keyof Point  // PointKeys表示Point属性名称组成的联合类型

function getPropertyValue(obj: Point, key: PointKeys) {
    return obj[key]
}

let obj = new Point()
console.log(getPropertyValue(obj, "x"))  // 打印"1"
console.log(getPropertyValue(obj, "y"))  // 打印"2"
```

**ArkTS**

```typescript
class Point {
    x: number = 1
    y: number = 2
}

function getPropertyValue(obj: Point, key: string): number {
    if (key == "x") {
        return obj.x
    }
    if (key == "y") {
        return obj.y
    }
    throw new Error()  // 处理没有该属性的分支
    return 0
}

function main(): void {
    let obj = new Point()
    console.log(getPropertyValue(obj, "x"))  // 打印"1"
    console.log(getPropertyValue(obj, "y"))  // 打印"2"
}
```

### 展开运算符仅支持函数剩余参数为数组类型

**规则：**`arkts-no-spread`

**级别：错误**

展开运算符唯一支持的场景是函数剩余参数为数组类型。

**TypeScript**

```typescript
function foo(x : number, y : number, z : number) {
    console.log(x, y, z)
}

let args : [number, number, number] = [0, 1, 2]
foo(...args)

let list1 = [1, 2]
let list2 = [...list1, 3, 4]

let point2d = {x: 1, y: 2}
let point3d = {...point2d, z: 3}
```

**ArkTS**

```typescript
function sum_numbers(...numbers: number[]): number {
    let res = 0
    for (let n of numbers)
        res += n
    return res
}
console.log(sum_numbers(1, 2, 3))

function log_numbers(x : number, y : number, z : number) {
    console.log(x, y, z)
}

let numbers: number[] = [1, 2, 3]
log_numbers(numbers[0], numbers[1], numbers[2])

let list1 : number[] = [1, 2]
let list2 : number[] = [list1[0], list1[1], 3, 4]

class Point2D {
    x: number = 0; y: number = 0
}

class Point3D {
    x: number = 0; y: number = 0; z: number = 0
    constructor(p2d: Point2D, z: number) {
        this.x = p2d.x
        this.y = p2d.y
        this.z = z
    }
}

let p3d = new Point3D({x: 1, y: 2} as Point2D, 3)
console.log(p3d.x, p3d.y, p3d.z)
```

### 接口不能继承具有相同属性的两个接口

**规则：**`arkts-no-extend-same-property`

**级别：错误**

在TypeScript中，如果一个接口继承了具有相同方法的两个接口，则该接口必须使用联合类型来声明该方法。在ArkTS中，由于一个接口中不能包含两个无法区分的方法（例如两个参数列表相同但返回类型不同的方法），因此，接口不能继承具有相同属性的两个接口。

**TypeScript**

```typescript
interface Mover {
    getStatus(): { speed: number }
}
interface Shaker {
    getStatus(): { frequency: number }
}

interface MoverShaker extends Mover, Shaker {
    getStatus(): {
        speed: number
        frequency: number
    }
}

class C implements MoverShaker {
    private speed: number = 0
    private frequency: number = 0

    getStatus() {
        return { speed: this.speed, frequency: this.frequency }
    }
}
```

**ArkTS**

```typescript
class MoveStatus {
    public speed : number
    constructor() {
        this.speed = 0
    }
}
interface Mover {
    getMoveStatus(): MoveStatus
}

class ShakeStatus {
    public frequency : number
    constructor() {
        this.frequency = 0
    }
}
interface Shaker {
    getShakeStatus(): ShakeStatus
}

class MoveAndShakeStatus {
    public speed : number
    public frequency : number
    constructor() {
        this.speed = 0
        this.frequency = 0
    }
}

class C implements Mover, Shaker {
    private move_status : MoveStatus
    private shake_status : ShakeStatus

    constructor() {
        this.move_status = new MoveStatus()
        this.shake_status = new ShakeStatus()
    }

    public getMoveStatus() : MoveStatus {
        return this.move_status
    }

    public getShakeStatus() : ShakeStatus {
        return this.shake_status
    }

    public getStatus(): MoveAndShakeStatus {
        return {
            speed: this.move_status.speed,
            frequency: this.shake_status.frequency
        }
    }
}
```

### 不支持声明合并

**规则：**`arkts-no-decl-merging`

**级别：错误**

ArkTS不支持合并声明。所用类、接口等的声明必须唯一。

**TypeScript**

```typescript
interface Document {
    createElement(tagName: any): Element
}

interface Document {
    createElement(tagName: string): HTMLElement
}

interface Document {
    createElement(tagName: number): HTMLDivElement
    createElement(tagName: boolean): HTMLSpanElement
    createElement(tagName: string, value: number): HTMLCanvasElement
}
```

**ArkTS**

```typescript
interface Document {
    createElement(tagName: number): HTMLDivElement
    createElement(tagName: boolean): HTMLSpanElement
    createElement(tagName: string, value: number): HTMLCanvasElement
    createElement(tagName: string): HTMLElement
    createElement(tagName: Object): Element
}
```

### 接口不能继承类

**规则：**`arkts-extends-only-class`

**级别：错误**

ArkTS不支持接口继承类。接口只能继承接口。

**TypeScript**

```typescript
class Control {
    state: number = 0
}

interface SelectableControl extends Control {
    select(): void
}
```

**ArkTS**

```typescript
interface Control {
    state: number
}

interface SelectableControl extends Control {
    select(): void
}
```

### 禁止运行时检查对象属性

**规则：**`arkts-no-prop-existence-check`

**级别：错误**

ArkTS中，对象布局在编译时就确定了，且不能在运行时被更改。禁止运行时检查对象属性。使用`as`运算符进行类型转换以读取相应的属性和方法。读取对象中不存在的属性将导致编译时错误。

**TypeScript**

```typescript
class A {
    foo() {}
    bar() {}
}

function getSomeObject() {
    return new A()
}

let obj: any = getSomeObject()
if (obj && obj.foo && obj.bar) {
    console.log("Yes")  // 此示例中将打印 "Yes"
} else {
    console.log("No")
}
```

**ArkTS**

```typescript
class A {
    foo(): void {}
    bar(): void {}
}

function getSomeObject(): A {
    return new A()
}

function main(): void {
    let tmp: Object = getSomeObject()
    let obj: A = tmp as A
    obj.foo()       // OK
    obj.bar()       // OK
    obj.some_foo()  // 编译时错误：方法some_foo不存在于此类型上
}
```

**相关约束**

* 仅支持属性名称为标识符的对象
* 不支持Symbol() API
* 访问未定义的属性将导致编译时错误
* 不支持delete运算符
* 仅允许运算符typeof在表达式上下文中使用
* 不支持in运算符
* 不支持声明动态属性
* 限制使用标准库

### 不支持构造函数类型

**规则：**`arkts-no-ctor-signatures-funcs`

**级别：错误**

ArkTS不支持使用构造函数类型。改用lambda函数。

**TypeScript**

```typescript
class Person {
    constructor(
        name: string,
        age: number
    ) {}
}
type PersonCtor = new (name: string, age: number) => Person

function createPerson(Ctor: PersonCtor, name: string, age: number): Person
{
    return new Ctor(name, age)
}

const person = createPerson(Person, 'John', 30)
```

**ArkTS**

```typescript
class Person {
    constructor(
        name: string,
        age: number
    ) {}
}
type PersonCtor = (n: string, a: number) => Person

function createPerson(Ctor: PersonCtor, n: string, a: number): Person {
    return Ctor(n, a)
}

let Impersonizer: PersonCtor = (n: string, a: number): Person => {
    return new Person(n, a)
}

const person = createPerson(Impersonizer, "John", 30)
```

### 不支持声明动态属性

**规则：**`arkts-no-dyn-prop-decl`

**级别：错误**

ArkTS不支持声明动态属性。必须在类中声明所有的属性。尽管可以用对象数组来实现动态特性，但更推荐使用静态类型范式来显式声明字段、名称和类型。

**TypeScript**

```typescript
class Person {
    name: string = ""
    age: number = 0; // 此处需要分号
    [key: string]: string | number
}

const person: Person = {
    name: "John",
    age: 30,
    email: "john@example.com",
    phone: 1234567890,
}
```

**ArkTS**

```typescript
class Person {
    name: string
    age: number
    email: string
    phone: number

    constructor(name: string, age: number, email: string, phone: number) {
        this.name = name
        this.age = age
        this.email = email
        this.phone = phone
    }
}

function main(): void {
    const person: Person = new Person("John", 30, "john@example.com", 1234567890)
}
```

**相关约束**

* 仅支持属性名称为标识符的对象
* 不支持Symbol() API
* 访问未定义的属性将导致编译时错误
* 不支持delete运算符
* 仅允许在表达式中使用typeof运算符
* 不支持in运算符
* 禁止运行时检查对象属性
* 限制使用标准库

### 只能使用类型相同的编译期表达式初始化枚举成员

**规则：**`arkts-no-enum-mixed-types`

**级别：错误**

ArkTS不支持使用在运行期间才能计算的表达式来初始化枚举成员。此外，枚举中所有显式初始化的成员必须具有相同的类型。

**TypeScript**

```typescript
enum E1 {
    A = 0xa,
    B = 0xb,
    C = Math.random(),
    D = 0xd,
    E // 推断出0xe
}

enum E2 {
    A = 0xa,
    B = "0xb",
    C = 0xc,
    D = "0xd"
}
```

**ArkTS**

```typescript
enum E1 {
    A = 0xa,
    B = 0xb,
    C = 0xc,
    D = 0xd,
    E // 推断出0xe
}

enum E2 {
    A = "0xa",
    B = "0xb",
    C = "0xc",
    D = "0xd"
}
```

### 不支持`enum`声明合并

**规则：**`arkts-no-enum-merging`

**级别：错误**

ArkTS不支持`enum`声明合并。

**TypeScript**

```typescript
enum Color {
    RED,
    GREEN
}
enum Color {
    YELLOW = 2
}
enum Color {
    BLACK = 3,
    BLUE
}
```

**ArkTS**

```typescript
enum Color {
    RED,
    GREEN,
    YELLOW,
    BLACK,
    BLUE
}
```

### 命名空间不能被用作对象

**规则：**`arkts-no-ns-as-obj`

**级别：错误**

ArkTS不支持将命名空间用作对象。可以使用类或模块。

**TypeScript**

```typescript
namespace MyNamespace {
    export let x: number
}

let m = MyNamespace
m.x = 2
```

**ArkTS**

```typescript
namespace MyNamespace {
    export let x: number
}

MyNamespace.x = 2
```

### 脚本和模块

**规则：**`arkts-no-scripts`

**级别：错误**

通常来说，ArkTS中的脚本和模块与TypeScript非常接近。它们的差异在另外的约束中描述。

**相关约束**

* 不支持import type
* 不支持仅为副作用而导入一个模块
* 不支持import default as ...
* 不支持require
* 不支持重命名导出
* 不支持导出列表
* 不支持重导出
* 不支持通过export = ... 

### 不支持命名空间中的非声明语句

**规则：**`arkts-no-ns-statements`

**级别：错误**

ArkTS不支持命名空间中的非声明语句。可以将非声明语句写在函数中。

**TypeScript**

```typescript
namespace A {
    export let x: number
    x = 1
}
```

**ArkTS**

```typescript
namespace A {
    export let x: number

    export function init() {
      x = 1
    }
}

// 调用初始化函数来执行：
A.init()
```

### 不支持`import type`

**规则：**`arkts-no-special-imports`

**级别：错误**

ArkTS不支持`import type`。改为`import`。

**TypeScript**

```typescript
// 通用导入语法
import { APIResponseType } from "./api"

// 导入类型
import type { APIResponseType } from "./api"
```

**ArkTS**

```typescript
import { APIResponseType } from "./api"
```

**相关约束**

* 不支持仅为副作用而导入一个模块
* 不支持import default as ...
* 不支持require

### 不支持仅为副作用而导入一个模块

**规则：**`arkts-no-side-effects-imports`

**级别：错误**

ArkTS不支持`window`等全局变量，避免模块导入时产生副作用。可以通过`*`语法获取所有导出的变量。

**TypeScript**

```typescript
// === “path/to/module.ts”中的模块
export const EXAMPLE_VALUE = 42

// 设置全局变量
window.MY_GLOBAL_VAR = "Hello, world!"

//==== 使用此模块：
import "path/to/module"
```

**ArkTS**

```typescript
import * from "path/to/module"
```

### 不支持`import default as ...`

**规则：**`arkts-no-import-default-as`

**级别：错误**

ArkTS不支持`import default as ...` 语法。使用显式的`import ... from ...` 语法。

**TypeScript**

```typescript
import { default as d } from "mod"
```

**ArkTS**

```typescript
import d from "mod"
```

### 不支持`require` 

**规则：**`arkts-no-require`

**级别：错误**

ArkTS不支持通过`require`导入。改用`import`。

**TypeScript**

```typescript
import m = require("mod")
```

**ArkTS**

```typescript
import * as m from "mod"
```

### 不支持重命名导出

**规则：**`arkts-no-export-renaming`

**级别：错误**

ArkTS不支持重命名导出。可以采用设置别名的方式。

**TypeScript**

```typescript
// file1.ts
class MyClass {
    // ...
}

export { MyClass as RenamedClass }

// file2.ts
import { RenamedClass } from "./file1"

function main(): void {
    const myObject = new RenamedClass()
    // ...
}
```

**ArkTS**

```typescript
// module1
class MyClass {
    // ...
}

export type RenamedClass = MyClass

// module2
import { RenamedClass } from "./module1"

function main(): void {
    const myObject = new RenamedClass()
    // ...
}
```

**相关约束**

* 不支持导出列表
* 不支持重导出
* 不支持通过export = ... 

### 不支持导出列表

**规则：**`arkts-no-export-list-decl`

**级别：错误**

ArkTS不支持导出列表的语法。使用`export`关键字显式导出每个值。

**TypeScript**

```typescript
export { x }
export { x } from "mod"
export { x, y as b, z as c }
```

**ArkTS**

```typescript
let x = 1
class MyClass {}
export let y = x, z: number = 2
export type RenamedClass = MyClass
```

**相关约束**

* 不支持重命名导出
* 不支持重导出
* 不支持通过export = ... 

### 不支持重导出

**规则：**`arkts-no-reexport`

**级别：错误**

ArkTS不支持重导出。从导出模块显式导入。

**TypeScript**

```typescript
// module1
export class MyClass {
    // ...
}

// module2
export { MyClass } from "module1"

// consumer模块
import { MyClass } from "module2"

const myInstance = new MyClass()
```

**ArkTS**

```typescript
// module1
export class MyClass {
  // ...
}

// module2
// some stuff

// consumer模块
import { MyClass } from "module1"
import * from "module2"

const myInstance = new MyClass()
```

**相关约束**

* 不支持重命名导出
* 不支持导出列表
* 不支持通过export = ... 

### 不支持通过`export = ...`

**规则：**`arkts-no-export-assignment`

**级别：错误**

ArkTS不支持`export = ...`语法。改用常规的`export`或`import`。

**TypeScript**

```typescript
// module1
export = Point

class Point {
    constructor(x: number, y: number) {}
    static origin = new Point(0, 0)
}

// module2
import Pt = require("module1")

let p = Pt.origin
```

**ArkTS**

```typescript
// module1
export class Point {
    constructor(x: number, y: number) {}
    static origin = new Point(0, 0)
}

// module2
import * as Pt from "module1"

let p = Pt.origin
```

**相关约束**

* 不支持重命名导出
* 不支持导出列表
* 不支持重导出

### 不支持`export type`
**规则：**`arkts-no-special-exports`

**级别：错误**

ArkTS不支持`export type`。改用`export`。

**TypeScript**

```typescript
class C {}
export type { C }
```

**ArkTS**

```typescript
export class C {}
```

### 不支持ambient module声明

**规则：**`arkts-no-ambient-decls`

**级别：错误**

ArkTS不支持ambient module声明，因为ArkTS本身有与JavaScript交互的机制。

**TypeScript**

```typescript
declare module "someModule" {
    export function normalize(s : string) : string;
}
```

**ArkTS**

```typescript
// 从原始模块中导入需要的内容
import { normalize } from "../someModule"
```

**相关约束**

* 不支持在模块名中使用通配符
* 模块标识符中不允许使用.js扩展名

### 不支持在模块名中使用通配符

**规则：**`arkts-no-module-wildcards`

**级别：错误**

由于在ArkTS中，导入是编译时而非运行时行为，因此，不支持在模块名中使用通配符。

**TypeScript**

```typescript
declare module "*!text" {
    const content: string
    export default content
}
```

**相关约束**

* 不支持ambient module声明
* 不支持通用模块定义(UMD)
* 模块标识符中不允许使用.js扩展名

### 不支持通用模块定义(UMD)

**规则：**`arkts-no-umd`

**级别：错误**

ArkTS不支持通用模块定义（UMD）。因为在ArkTS中没有“脚本”的概念（相对于“模块”）。此外，在ArkTS中，导入是编译时而非运行时特性。改用`export`和`import`语法。

**TypeScript**

```typescript
// math-lib.d.ts
export const isPrime(x: number): boolean
export as namespace mathLib

// 脚本中
mathLib.isPrime(2)
```

**ArkTS**

```typescript
// math-lib.d.ts
namespace mathLib {
    export isPrime(x: number): boolean
}

// 程序中
import { mathLib } from "./math-lib"
mathLib.isPrime(2)
```

**相关约束**

* 不支持在模块名中使用通配符

### 模块标识符中不允许使用.js扩展名

**规则：**`arkts-no-js-extension`

**级别：错误**

ArkTS不允许在模块标识符中使用`.js`扩展名，因为ArkTS本身有与JavaScript交互的机制。

**TypeScript**

```typescript
import { something } from "./module.js"
```

**ArkTS**

```typescript
import { something } from "./module"
```

**相关约束**

* 不支持ambient module声明
* 不支持在模块名中使用通配符

### 不支持`new.target`

**规则：**`arkts-no-new-target`

**级别：错误**

ArkTS没有原型的概念，因此不支持`new.target`。此特性不符合静态类型的原则。

**TypeScript**

```typescript
class CustomError extends Error {
    constructor(message?: string) {
        // 'Error'在此处断开原型链
        super(message)

        // 恢复原型链
        Object.setPrototypeOf(this, new.target.prototype)
    }
}
```

**相关约束**

* 不支持在原型上赋值

### 不支持动态导入

**规则：**`arkts-no-runtime-import`

**级别：错误**

由于在ArkTS中，导入是编译时而非运行时特性，因此，ArkTS不支持动态导入，如`await import...`。改用静态`import`语法。

**TypeScript**

```typescript
const zipUtil = await import("./utils/create-zip-file")
```

**ArkTS**

```typescript
import { zipUtil } from "./utils/create-zip-file"
```

**相关约束**

* 不支持在模块名中使用通配符
* 不支持通用模块定义(UMD)
* 不支持导入断言

### 不支持确定赋值断言

**规则：**`arkts-no-definite-assignment`

**级别：错误**

ArkTS不支持确定赋值断言`let v!: T`，这是一种过度的编译器提示。改用带初始化的声明。

**TypeScript**

```typescript
let x!: number // 提示：在使用前将x初始化

initialize()

function initialize() {
    x = 10
}

console.log("x = " + x)
```

**ArkTS**

```typescript
function initialize() : number {
    return 10
}

let x: number = initialize()

console.log("x = " + x)
```

### 不支持IIFE作为命名空间的声明

**规则：**`arkts-no-iife`

**级别：错误**

由于在ArkTS中，匿名函数不能作为命名空间，因此不支持IIFE作为命名空间的声明。请使用命名空间的常规语法。

**TypeScript**

```typescript
var C = (function() {
    function C(n) {
        this.p = n
    }
    return C
})()
C.staticProperty = 1
```

**ArkTS**

```typescript
namespace C {
    // ...
}
```

### 不支持在原型上赋值

**规则：**`arkts-no-prototype-assignment`

**级别：错误**

ArkTS没有原型的概念，因此不支持在原型上赋值。此特性不符合静态类型的原则。

**TypeScript**

```typescript
var C = function(p) {
    this.p = p
}

C.prototype = {
    m() {
        console.log(this.p)
    }
}

C.prototype.q = function(r) {
    return this.p === r
}
```

**相关约束**

* 不支持new.target

### 不支持`globalThis`

**规则：**`arkts-no-globalthis`

**级别：错误**

由于ArkTS不支持动态更改对象的布局，因此不支持全局作用域和`globalThis`。

**TypeScript**

```typescript
// 全局文件中
var abc = 100

// 从上面引用'abc'。
globalThis.abc = 200
```

**ArkTS**

```typescript
// file1
export let abc : number = 0

// file2
import * as M from "../file1"

M.abc = 200
```

**相关约束**

* 不支持声明函数的属性
* 标准库使用限制

### 不支持utility类型

**规则：**`arkts-no-utility-types`

**级别：错误**

当前ArkTS不支持从TypeScript扩展到标准库的utility类型（例如`Omit`、`Partial`、`Readonly`、`Record`、`Pick`等)。

**TypeScript**

```typescript
type Person = {
    name: string
    age: number
    location: string
}

type QuantumPerson = Omit<Person, "location">
```

**ArkTS**

```typescript
class Person {
    name: string
    age: number
    location: string
}

class QuantumPerson {
    name: string
    age: number
}
```

### 不支持对函数声明属性

**规则：**`arkts-no-func-props`

**级别：错误**

由于ArkTS不支持动态改变函数对象布局，因此，不支持对函数声明属性。

**TypeScript**

```typescript
class MyImage {
    // ...
}

function readImage(
    path: string, callback: (err: any, image: MyImage) => void
)
{
    // ...
}

function readFileSync(path : string) : number[] {
    return []
}

function decodeImageSync(contrents : number[]) {
    // ...
}

readImage.sync = (path: string) => {
    const contents = readFileSync(path)
    return decodeImageSync(contents)
}
```

**ArkTS**

```typescript
class MyImage {
    // ...
}

function readImage(
    path: string, callback: (err: Error, image: MyImage) => void
) : Promise<MyImage>
{
    // 异步实现
}

function readImageSync(path: string) : MyImage {
    // 同步实现
}
```

**相关约束**

* 不支持globalThis

### 不支持`Function.apply`、`Function.bind`以及`Function.call`

**规则：**`arkts-no-func-apply-bind-call`

**级别：错误**

ArkTS不允许使用标准库函数`Function.apply`、`Function.bind`以及`Function.call`。标准库使用这些函数来显式设置被调用函数的`this`参数。在ArkTS中，`this`的语义仅限于传统的OOP风格，函数体中禁止使用`this`。

**TypeScript**

```typescript
class P1 {
  firstName: string = "Mary";
}

class P2 {
  firstName: string = "Jack";
  fullName(): string {
    return this.firstName
  }
}

const person2 = new P2();

const person1 = new P1();
// 将会打印 Mary
console.log(person2.fullName.apply(person1))
```

**ArkTS**

```typescript
class Person {
    firstName : string

    constructor(firstName : string) {
        this.firstName = firstName
    }
    fullName() : string {
        return this.firstName
    }
}

let person = new Person("")
let person1 = new Person("Mary")

// 将打印“Mary”
console.log(person1.fullName())
```

**相关约束**

* 不支持在函数中使用this

### 不支持`readonly`修饰函数参数

**规则：**`arkts-no-readonly-params`

**级别：错误**

当前ArkTS中，`readonly`可以用于修饰属性，但不能用于修饰函数参数。

**TypeScript**

```typescript
function foo(arr: readonly string[]) {
    arr.slice()        // OK
    arr.push("hello!") // 编译时错误
}
```

**ArkTS**

```typescript
function foo(arr: string[]) {
    arr.slice()        // OK
    arr.push("hello!") // OK
}
```

### 不支持`as const`断言

**规则：**`arkts-no-as-const`

**级别：错误**

ArkTS不支持`as const`断言。在标准TypeScript中，`as const`用于标注字面量的相应字面量类型，而ArkTS不支持字面量类型。

**TypeScript**

```typescript
// 'hello'类型
let x = "hello" as const

// 'readonly [10, 20]'类型
let y = [10, 20] as const

// '{ readonly text: "hello" }'类型
let z = { text: "hello" } as const
```

**ArkTS**

```typescript
// 'string'类型
let x : string = "hello"

// 'number[]'类型
let y : number[] = [10, 20]

class Label {
    text : string
}

// 'Label'类型
let z : Label = {
    text: "hello"
}
```

### 不支持导入断言

**规则：** `arkts-no-import-assertions`

**级别：错误**

由于在ArkTS中，导入是编译时而非运行时特性，因此，ArkTS不支持导入断言。在运行时检查导入的API是否正确，对于静态类型的语言来说是没有意义的。改用常规的`import`语法。

**TypeScript**

```typescript
import { obj } from "./something.json" assert { type: "json" }
```

**ArkTS**

```typescript
// 编译时将检查导入T的正确性
import { something } from "./module"
```

**相关约束**

* 不支持在模块名中使用通配符
* 不支持通用模块定义(UMD)
* 不支持运行时导入断言

### 限制使用标准库

**规则：**`arkts-limited-stdlib`

**级别：错误**

ArkTS不允许使用TypeScript或JavaScript标准库中的某些接口。大部分接口与动态特性有关。ArkTS中禁止使用以下接口：

全局对象的属性和方法：`eval`、
`Infinity`、`NaN`、`isFinite`、`isNaN`、`parseFloat`、`parseInt`、
`encodeURI`、`encodeURIComponent`、`Encode`、
`decodeURI`、`decodeURIComponent`、`Decode`、
`escape`、`unescape`、`ParseHexOctet`

`Object`：`__proto__`、`__defineGetter__`、`__defineSetter__`、
`__lookupGetter__`、`__lookupSetter__`、`assign`、`create`、
`defineProperties`、`defineProperty`、`entries`、`freeze`、
`fromEntries`、`getOwnPropertyDescriptor`、`getOwnPropertyDescriptors`、
`getOwnPropertyNames`、`getOwnPropertySymbols`、`getPrototypeOf`、
`hasOwn`、`hasOwnProperty`、`is`、`isExtensible`、`isFrozen`、
`isPrototypeOf`、`isSealed`、`keys`、`preventExtensions`、
`propertyIsEnumerable`、`seal`、`setPrototypeOf`、`values`

`Reflect`：`apply`、`construct`、`defineProperty`、`deleteProperty`、
`get`、`getOwnPropertyDescriptor`、`getPrototypeOf`、`has`、
`isExtensible`、`ownKeys`、`preventExtensions`、`set`,
`setPrototypeOf`

`Proxy`：`handler.apply()`、`handler.construct()`、
`handler.defineProperty()`、`handler.deleteProperty()`、`handler.get()`、
`handler.getOwnPropertyDescriptor()`、`handler.getPrototypeOf()`、
`handler.has()`、`handler.isExtensible()`、`handler.ownKeys()`、
`handler.preventExtensions()`、`handler.set()`、`handler.setPrototypeOf()`

`Array`：`isArray`

`ArrayBuffer`：`isView`

**相关约束**

* 仅支持属性名称为标识符的对象
* 不支持Symbol() API
* 访问未定义的属性将导致编译时错误
* 仅允许在表达式中使用typeof运算符
* 不支持in运算符
* 禁止运行时检查对象属性
* 不支持声明动态属性
* 不支持globalThis