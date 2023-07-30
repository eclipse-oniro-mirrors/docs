# Introduction

Welcome to the “TypeScript to ArkTS” cookbook. This document gives you short
recipes to rewrite your standard TypeScript code to ArkTS. Although ArkTS is
designed to be close to TypeScript, some limitations were added for the sake of
performance. As a result, all TypeScript features can be divided into the following
categories:

1. **Fully supported features**: the original code requires no modification
   at all. According to our measurements, projects that already follow the
   best TypeScript practices can keep 90% to 97% of their codebase intact.
2. **Partially supported features**: some minor code refactoring is needed.
   Example: The keyword `let` must be used in place of `var` to declare
   variables. Please note that your code will still remain a valid TypeScript code
   after rewriting according to our recipes.
3. **Unsupported features**: a greater code refactoring effort can be required.
   Example: The type `any` is unsupported, and you are to introduce explicit
   typing to your code everywhere `any` is used.

# How to Use The Cookbook

The main goal of this cookbook is to provide recipes for all partially
supported features and explicitly list all unsupported features.

The document is built on the feature-by-feature basis, and if you do not find
some feature, you can safely consider it **supported**. Otherwise, a recipe
will give you a suggestion on how to rewrite your code and work around an
unsupported case.

## Recipe explained

The original TypeScript code containing the keyword `var`:

```typescript
function addTen(x: number): number {
    var ten = 10
    return x + ten
}
```

This code must be rewritten as follows:

```typescript
// Important! This is still valid TypeScript.
function addTen(x: number): number {
    let ten = 10
    return x + ten
}
```

## Status of Unsupported Features

Currently unsupported are mainly the features which

- relate to dynamic typing that degrades runtime performance, or
- require extra support in the compiler, thus degrading project build time.

However, the ArkTS team reserves the right to reconsider the list and
**shrink** it in the future releases based on the feedback from the developers
and more real-world data experiments.

# Recipes Summarized

This documents provides an informal summary of TypeScript features that ArkTS either
does not support or supports with limitations. For the full list, with more
detailed code examples and workaround suggestions, please see
[this section](#recipes).

## Static typing is enforced

ArkTS was designed with following goals in mind:

- It should be easy for developers to read and understand ArkTS programs,
  because the code is read more often than written;
- ArkTS should execute fast with as little power consumption as possible,
  which is critical for mobile devices which ArkTS targets.

Static typing is one of the most important features of ArkTS, which helps
achieve both goals. Indeed, if your program is statically typed, i.e. all
types are known at the compile time, it’s much easier to understand which data
structures are used in the code. At the same time, since all types are known
before the program actually runs, code correctness can be verified by the
compiler, which eliminates many runtime type checks and improves the
performance.

Therefore, it was decided to prohibit usage of the type `any`.

### Example

```typescript
//
// Not supported:
//

let res : any = some_api_function("hello", "world")

// What is `res`? A numeric error code? Some string? An object?
// How should we work with it?

//
// Supported:
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

### Rationale and impact

Our research and experiments let us conclude that this feature is already
not welcome in the modern TypeScript. According to our measurements, it is used
in approximately 1% of TypeScript code bases. Moreover, code linters (e.g., ESLint)
already include a set of rules that prohibit usage of `any`. Thus, although
prohibiting `any` requires code refactoring, we consider it a low-effort
change with the high impact result.

## Changing object layout in runtime is prohibited

To achieve maximum performance benefits, ArkTS requires that layout of objects
does not change during program execution. In other words, it is prohibited to:

- add new properties or methods to the objects;
- delete existing properties or methods from the objects;
- assign values of arbitrary types to object properties.

It’s worth noticing that many such operations are already prohibited by the TypeScript
compiler. However, it still can be “tricked” by e.g. `as any` casts, wchich
ArkTS does not support (see the detailed example below).

### Example

```typescript
class Point {
    public x : number = 0
    public y : number = 0

    constructor(x : number, y : number) {
        this.x = x
        this.y = y
    }
}

/* It is impossible to delete a property
   from the object. It is guaranteed that
   all Point objects have the property x:
*/
let p1 = new Point(1.0, 1.0)
delete p1.x           // Compile-time error in TypeScript and ArkTS
delete (p1 as any).x  // OK in TypeScript, compile-time error in ArkTS

/* Class Point does not define any property
   named `z`, and it is impossible to add
   it while the program runs.
*/
let p2 = new Point(2.0, 2.0)
p2.z = "Label";         // Compile-time error in TypeScript and ArkTS
(p2 as any).z = "Label" // OK in TypeScript, compile-time error in ArkTS

/* It is guaranteed that all Point objects
   have only properties x and y, it is
   impossible to generate some arbitrary
   identifier and use it as a new property:
*/
let p3 = new Point(3.0, 3.0)
let prop = Symbol();     // OK in TypeScript, compile-time error in ArkTS
(p3 as any)[prop] = p3.x // OK in TypeScript, compile-time error in ArkTS
p3[prop] = p3.x          // Compile-time error in TypeScript and ArkTS

/* It is guaranteed that all Point objects
   have properties x and y of type number,
   so assigning a value of any other type
   is impossible:
*/
let p4 = new Point(4.0, 4.0)
p4.x = "Hello!";         // Compile-time error in TypeScript and ArkTS
(p4 as any).x = "Hello!" // OK in TypeScript, compile-time error in ArkTS

// Usage of Point objects which is compliant with the class definition:
function distance(p1 : Point, p2 : Point) : number {
    return Math.sqrt(
      (p2.x - p1.x) * (p2.x - p1.x) + (p2.y - p1.y) * (p2.y - p1.y)
    )
}
let p5 = new Point(5.0, 5.0)
let p6 = new Point(6.0, 6.0)
console.log("Distance between p5 and p6: " + distance(p5, p6))
```

### Rationale and impact

Unpredictable changing of object layout contradicts both good readability and
good performance of the code. Indeed, having class definition at one place and
modifying actual object layout elsewhere is confusing and error-prone from the
developer’s point of view. Additionally, it requires extra runtime support,
which brings undesired execution overhead. Moreover, it contradicts the idea of
static typing. If we want to make typing as explicit as possible, why would we
need to add or remove additional properties?

At the same time, according to our observations and experiments, this feature
is already not welcome in the modern TypeScript. It is used in the marginal number of
cases in real-world projects and state of the art linters have rules to
prohibit its usage.

Thus, we conclude that prohibiting runtime changes to objects’ layout results
in low-effort refactoring with the high positive impact on performance.

## Semantics of operators is restricted

To achieve better performance and encourage developers write clearer code,
ArkTS restricts semantics of some operators. A couple of examples are given
below, and the full list of restrictions is outlined [here](#recipes).

### Example

```typescript
// Operator `+` is defined for numbers and strings, but not for other types:
class C {
    // ...
}
let c1 : C = new C()
let c2 : C = new C()
console.log(c1 + c2) // Compile-time error
```

### Rationale and impact

Overloading language operators with extra semantics complicates language
specification and makes developers remember about all possible corner cases
and their handling rules. Besides, in certain cases it incurs some runtime
overhead, which is undesired.

At the same time, according to our observations and experiments, this feature
is not popular in the modern TypeScript. It is used in less than 1% of real-world
code bases. Besides, such cases are very easy to refactor.

Thus, although restricting semantics of operators requires changing the code,
this is a low-effort change which results in a clearer and more performant code.

## Structural typing is not supported (yet)

Let’s consider a situation when two unrelated classes `T` and `U` have the
same public API:

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

Can we assign a value of `T` to a variable of `U`?

```typescript
let u : U = new T() // Is this allowed?
```

Can we pass a value of `T` to a function that accepts a parameter of `U`?

```typescript
function greeter(u : U) {
    console.log("To " + u.name)
    u.greet()
}

let t : T = new T()
greeter(t) // Is this allowed?
```

Or, in other words, which approach will we take:

- `T` and `U` are not related by inheritance or any common interface, but
  since they have the same public API, they are “somewhat equivalent”, so the
  answer to both questions above is “yes”;
- `T` and `U` are not related by inheritance or any common interface, and
  should always be considered as totally different types, so the
  answer to both questions above is “no”.

Languages that take the first approach are said to support structural typing,
while languages that take the second approach do not support it. Currently,
TypeScript supports structural typing, and ArkTS does not.

It is debatable if structural typing helps produce clear and
understandable code, arguments can be found both for and against it.
Moreover, structural typing does not harm program performance (at least in some
cases). Why is it not supported then?

The answer is that support for structural typing is a major feature which needs
lots of consideration and careful implementation in language specification,
compiler and runtime. Safe and efficient implementation requires that other
aspects (static typing, restrictions on changing object layout) are also
taken into account. That’s why support for this feature is postponed. The team
will be ready to reconsider based on real-world scenarios and feedback. More
cases and suggested workarounds can be found in [Recipes](#recipes).

# Recipes

## Recipe: Objects with property names that are not identifiers are not supported

**Rule `arkts-identifiers-as-prop-names`**

**Severity: error**

ArkTS does not support Objects with name properties that are numbers or
strings. Use classes to access data by property names. Use arrays to access
data by numeric indices.

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

// If you still need a container to store keys of different types,
// use Map<Object, some_type>:
let z = new Map<Object, number>()
z.set("name", 1)
z.set(2, 2)
console.log(z.get("name"))
console.log(z.get(2))
```

**See also**

* Recipe: Symbol() API is not supported
* Recipe: Attempt to access an undefined property is a compile-time error
* Recipe: delete operator is not supported
* Recipe: typeof operator is allowed only in expression contexts
* Recipe: in operator is not supported
* Recipe: Property-based runtime type checks are not supported
* Recipe: Dynamic property declaration is not supported
* Recipe: Usage of standard library is restricted

## Recipe: `Symbol()` API is not supported

**Rule `arkts-no-symbol`**

**Severity: error**

TypeScript has `Symbol()` API, which can be used among other things to generate
unique property names at runtime. ArkTS does not support `Symbol()` API
because its most popular use cases make no sense in the statically typed
environment. In particular, the object layout is defined at compile time
and cannot be changed at runtime.

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

**See also**

* Recipe: Objects with property names that are not identifiers are not supported
* Recipe: Attempt to access an undefined property is a compile-time error
* Recipe: delete operator is not supported
* Recipe: typeof operator is allowed only in expression contexts
* Recipe: in operator is not supported
* Recipe: Property-based runtime type checks are not supported
* Recipe: Dynamic property declaration is not supported
* Recipe: Usage of standard library is restricted

## Recipe: Private ‘#’ identifiers are not supported

**Rule `arkts-no-private-identifiers`**

**Severity: error**

ArkTS does not private identifiers started with `#` symbol, use `private`
keyword instead.

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

## Recipe: Use unique names for types, namespaces, etc.

**Rule `arkts-unique-names`**

**Severity: error**

Names for types, namespaces and so on must be unique and distinct from other
names, e.g., variable names.

**TypeScript**

```typescript
let X: string
type X = number[] // Type alias with the same name as the variable
```

**ArkTS**

```typescript
let X: string
type T = number[] // X is not allowed here to avoid name collisions
```

## Recipe: Use `let` instead of `var`

**Rule `arkts-no-var`**

**Severity: error**

ArkTS does not support `var`, always use `let` instead.

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
scoped_var = 5 // Visible
scoped_let = 5 // Compile-time error
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
scoped_let = 5 // Compile-time error
```

## Recipe: Use explicit types instead of `any`, `undefined`, `unknown`

**Rule `arkts-no-any-undefined-unknown`**

**Severity: error**

ArkTS does not support `any`, `undefined`, and `unknown` types.
Specify types explicitly.

**TypeScript**

```typescript
var x
console.log(x) // undefined

var y: any
console.log(y) // undefined
```

**ArkTS**

```typescript
// All variables should have their types specified explicitly:
let x: Object = {}
console.log(x) // {}
```

**See also**

* Recipe: Use Object[] instead of tuples

## Recipe: `bigint` is not a builtin type, suffix `n` for numeric literals is not supported

**Rule `arkts-no-n-suffix`**

**Severity: error**

ArkTS supports `bigint` as a part of the standard library, not as a builtin
type. `n` suffix for numeric literals is not supported, `BigInt` factory
function can be used to produce values of `bigint` type.

**TypeScript**

```typescript
let a: bigint = 1n
```

**ArkTS**

```typescript
let a = BigInt(1)
let b: bigint = BigInt(2)
```

## Recipe: Use `Object[]` instead of tuples

**Rule `arkts-no-tuples`**

**Severity: error**

Currently, ArkTS does not support tuples. You can use arrays of `Object`
(`Object[]`) to emulate tuples.

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

## Recipe: Use `class` instead of a type with call signature

**Rule `arkts-no-call-signatures`**

**Severity: error**

ArkTS does not support call signatures in object types. Use classes instead.

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

**See also**

* Recipe: Use class instead of a type with constructor signature

## Recipe: Use `class` instead of a type with constructor signature

**Rule `arkts-no-ctor-signatures-type`**

**Severity: error**

ArkTS does not support constructor signatures in object types. Use classes
instead.

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

**See also**

* Recipe: Use class instead of a type with call signature

## Recipe: Only one static block is supported

**Rule `arkts-no-multiple-static-blocks`**

**Severity: error**

ArkTS does not allow to have sevaral static block for class initialization,
combine static blocks statements to the one static block.

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

## Recipe: Indexed signatures are not supported

**Rule `arkts-no-indexed-signatures`**

**Severity: error**

ArkTS does not allow indexed signatures, use arrays instead.

**TypeScript**

```typescript
// Interface with an indexed signature:
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

## Recipe: Use inheritance instead of intersection types

**Rule `arkts-no-intersection-types`**

**Severity: error**

Currently, ArkTS does not support intersection types. You can use inheritance
as a work-around.

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

## Recipe: Returning `this` type is not supported

**Rule `arkts-no-this-as-return-type`**

**Severity: error**

ArkTS does not support the returning `this` type. Use explicit type instead.

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

## Recipe: Conditional types are not supported

**Rule `arkts-no-conditional-types`**

**Severity: error**

ArkTS does not support conditional type aliases. Introduce a new type with
constraints explicitly or rewrite logic with use of `Object`. `infer`
keyword is not supported.

**TypeScript**

```typescript
type X<T> = T extends number ? T : never

type Y<T> = T extends Array<infer Item> ? Item : never
```

**ArkTS**

```typescript
// Provide explicit contraints within type alias
type X1<T extends number> = T

// Rewrite with Object. Less type control, need more type checks for safety
type X2<T> = Object

// Item has to be used as a generic parameter and need to be properly
// instantiated
type YI<Item, T extends Array<Item>> = Item
```

## Recipe: Optional parameters are not supported for primitive types

**Rule `arkts-no-opt-params`**

**Severity: error**

ArkTS does not support optional parameters of primitive types.
You can use default parameter values or reference types. For reference types,
non-specified optional parameter is set to `null`.

**TypeScript**

```typescript
// x is an optional parameter:
function f(x?: number) {
    console.log(x) // log undefined or number
}

// x is a required parameter with the default value:
function g(x: number = 1) {
    console.log(x)
}
```

**ArkTS**

```typescript
// You can use reference type (will be set to null if missing):
function f(x?: Number) {
    console.log(x) // log null or some number
}

// You can use a required parameter with the default value:
function g(x: number = 1) {
    console.log(x)
}
```

## Recipe: Declaring fields in `constructor` is not supported

**Rule `arkts-no-ctor-prop-decls`**

**Severity: error**

ArkTS does not support declaring class fields in the `constructor`.
You must declare them inside the `class` declaration instead.

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

## Recipe: Construct signatures not supported in interfaces

**Rule `arkts-no-ctor-signatures-iface`**

**Severity: error**

ArkTS does not support construct signatures. Use methods instead.

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

**See also**

* Recipe: Use class instead of a type with constructor signature

## Recipe: Indexed access types are not supported

**Rule `arkts-no-aliases-by-index`**

**Severity: error**

ArkTS does not support indexed access types. Use the type name instead.

**TypeScript**

```typescript
type Point = {x: number, y: number}
type N = Point["x"] // is equal to number
```

**ArkTS**

```typescript
class Point {x: number = 0; y: number = 0}
type N = number
```

## Recipe: Indexed access is not supported for fields

**Rule `arkts-no-props-by-index`**

**Severity: error**

ArkTS does not support indexed access for class fields. Use dot notation
instead.

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

## Recipe: Structural identity is not supported

**Rule `arkts-no-structural-identity`**

**Severity: error**

Currently, ArkTS does not support structural identity, i.e., the compiler
cannot compare two types’ public APIs and decide whether such types are
identical. Use other mechanisms (inheritance, interfaces or type aliases)
instead.

For the examples below, types `X` and `Y` are equivalent (interchangeble)
in TypeScript, while in ArkTS they are not.

**TypeScript**

```typescript
interface X {
    f(): string
}

interface Y { // Y is equal to X
    f(): string
}
```

**ArkTS**

```typescript
interface X {
    f(): string
}

type Y = X // Y is equal to X
```

**See also**

* Recipe: Structural typing is not supported for subtyping / supertyping
* Recipe: Structural typing is not supported for assignability checks
* Recipe: Structural typing is not supported for type inference

## Recipe: Structural typing is not supported for subtyping / supertyping

**Rule `arkts-no-structural-subtyping`**

**Severity: error**

Currently, ArkTS does not check structural equivalence for type inference,
i.e., the compiler cannot compare two types’ public APIs and decide whether
such types are identical. Use other mechanisms (inheritance or interfaces)
instead.

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

// Y is derived from X, which explicitly set subtype / supertype relations:
class Y extends X {
    constructor() {
        super()
    }
}

let x = new X()
let y = new Y()

console.log("Assign Y to X")
x = y // ok, X is the super class of Y

// Cannot assign X to Y
//y = x - compile-time error
```

**See also**

* Recipe: Structural identity is not supported
* Recipe: Structural typing is not supported for assignability checks
* Recipe: Structural typing is not supported for type inference

## Recipe: Structural typing is not supported for assignability checks

**Rule `arkts-no-structural-assignability`**

**Severity: error**

Currently, ArkTS does not check structural equivalence when checking if types
are assignable to each other, i.e., the compiler cannot compare two types’
public APIs and decide whether such types are identical. Use other mechanisms
(inheritance or interfaces) instead.

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

// X implements interface Z, which makes relation between X and Y explicit.
class X implements Z {
    public foo: number

    constructor() {
       this.foo = 0
    }
}

// Y implements interface Z, which makes relation between X and Y explicit.
class Y implements Z {
    public foo: number

    constructor() {
       this.foo = 0
    }
}

let x: Z = new X()
let y: Z = new Y()

console.log("Assign X to Y")
y = x // ok, both are of the same type

console.log("Assign Y to X")
x = y // ok, both are of the same type
```

**See also**

* Recipe: Structural identity is not supported
* Recipe: Structural typing is not supported for subtyping / supertyping
* Recipe: Structural typing is not supported for type inference

## Recipe: Optional properties are not supported for primitive types

**Rule `arkts-no-opt-props`**

**Severity: error**

ArkTS does not support optional properties of primitive types. You can use
properties with default values or reference types. For reference types,
non-specified optional property is set to `null`. This rule applies both to
classes and interfaces.

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
    // Some logic
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
    // targetPath is implicitly set to null
}

if (options.targetPath == null) {
    // Some logic
}
```

## Recipe: Type inference in case of generic function calls is limited

**Rule `arkts-no-inferred-generic-params`**

**Severity: error**

ArkTS allows to omit generic type parameters if it is possible to infer
the concrete types from the parameters passed to the function. Otherwise a
compile-time error occurs. In particular, inference of generic type parameters
based only on function return types is prohibited.

**TypeScript**

```typescript
function choose<T>(x: T, y: T): T {
    return Math.random() < 0.5 ? x : y
}

let x = choose(10, 20)   // OK, choose<number>(...) is inferred
let y = choose("10", 20) // Compile-time error

function greet<T>(): T {
    return "Hello" as T
}
let z = greet() // Type of x is inferred as "unknown"
```

**ArkTS**

```typescript
function choose<T>(x: T, y: T): T {
    return Math.random() < 0.5 ? x : y
}

let x = choose(10, 20)   // OK, choose<number>(...) is inferred
let y = choose("10", 20) // Compile-time error

function greet<T>(): T {
    return "Hello" as T
}
let z = greet<string>()
```

## Recipe: Structural typing is not supported for type inference

**Rule `arkts-no-structural-inference`**

**Severity: error**

Currently, ArkTS does not support structural typing, i.e., the compiler cannot
compare two types’ public APIs and decide whether such types are identical.
Use inheritance and interfaces to specify the relation between the types
explicitly.

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

// X and Y are equivalent because their public API is equivalent.
// Thus the second call is allowed:
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

// X and Y implement the same interface Z, thus both calls are allowed:
bar(new X(1))
bar(new Y(2))
```

**See also**

* Recipe: Structural identity is not supported
* Recipe: Structural typing is not supported for subtyping / supertyping
* Recipe: Structural typing is not supported for assignability checks

## Recipe: RegExp literals are not supported

**Rule `arkts-no-regexp-literals`**

**Severity: error**

Currently, ArkTS does not support RegExp literals. Use library call with string
literals instead.

**TypeScript**

```typescript
let regex: RegExp = /bc*d/
```

**ArkTS**

```typescript
let regex: RegExp = new RegExp("/bc*d/")
```

## Recipe: Object literal must correspond to some explicitly declared class or interface

**Rule `arkts-no-untyped-obj-literals`**

**Severity: error**

ArkTS supports usage of object literals if the compiler can infer to what
classes or interfaces such literals correspond to. Otherwise, a compile-time
error occurs. Specifically, using literals to initialize classes and interfaces
is not supported in following contexts:

* Initialization of anything that has `any`, `Object`, or `object` type
* Initialization of classes or interfaces with methods
* Initialization of classes which declare a `constructor` with parameters
* Initialization of classes with `readonly` fields

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

// Structural typing is used to deduce that p is Point:
let p = {x: 5, y: 10}
id_x_y(p)

// A literal can be contextually (i.e., implicitly) typed as Point:
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
let o6: C = {} // or let o6: C = new C()

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

    // constructor() is used before literal initialization
    // to create a valid object. Since there is no other Point constructors,
    // constructor() is automatically added by compiler
}

function id_x_y(o: Point): Point {
    return o
}

// Explicit type is required for literal initialization
let p: Point = {x: 5, y: 10}
id_x_y(p)

// id_x_y expects Point explicitly
// New instance of Point is initialized with the literal
id_x_y({x: 5, y: 10})
```

**See also**

* Recipe: Object literals cannot be used as type declarations
* Recipe: Array literals must contain elements of only inferrable types

## Recipe: Object literals cannot be used as type declarations

**Rule `arkts-no-obj-literals-as-types`**

**Severity: error**

ArkTS does not support the usage of object literals to declare
types in place. Declare classes and interfaces explicitly instead.

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

**See also**

* Recipe: Object literal must correspond to some explicitly declared class or interface
* Recipe: Array literals must contain elements of only inferrable types

## Recipe: Array literals must contain elements of only inferrable types

**Rule `arkts-no-noninferrable-arr-literals`**

**Severity: error**

Basically, ArkTS infers the type of an array literal as a union type of its
contents. But if there is at least one element with a non-inferrable type
(e.g. untyped object literal), a compile-time error occurs.

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

let a1 = [{n: 1, s: "1"} as C, {n: 2, s : "2"} as C] // a1 is of type "C[]"
let a2: C[] = [{n: 1, s: "1"}, {n: 2, s : "2"}]      // ditto
```

**See also**

* Recipe: Object literal must correspond to some explicitly declared class or interface
* Recipe: Object literals cannot be used as type declarations

## Recipe: Lambdas require explicit type annotation for parameters

**Rule `arkts-explicit-param-types-in-lambdas`**

**Severity: error**

Currently, ArkTS requires the types of lambda parameters
to be explicitly specified.

**TypeScript**

```typescript
let f = (s) => { // type any is assumed
    console.log(s)
}
```

**ArkTS**

```typescript
// Explicit types for lambda parameters are mandatory:
let f = (s: string) => {
    console.log(s)
}
```

## Recipe: Use arrow functions instead of function expressions

**Rule `arkts-no-func-expressions`**

**Severity: error**

ArkTS does not support function expressions, use arrow functions instead
to be explicitly specified.

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

## Recipe: Use generic functions instead of generic arrow functions

**Rule `arkts-no-generic-lambdas`**

**Severity: error**

ArkTS does not support generic arrow functions. Use normal generic functions
instead.

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

## Recipe: Class literals are not supported

**Rule `arkts-no-class-literals`**

**Severity: error**

ArkTS does not support class literals. A new named class type must be
introduced explicitly.

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

## Recipe: Classes cannot be specified in `implements` clause

**Rule `arkts-implements-only-iface`**

**Severity: error**

ArkTS does not allow to specify a class in implements clause. Only interfaces
may be specified.

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

## Recipe: Attempt to access an undefined property is a compile-time error

**Rule `arkts-no-undefined-prop-access`**

**Severity: error**

ArkTS supports accessing only those class properties that are either declared
in the class, or accessible via inheritance. Accessing any other properties is
prohibited and causes compile-time errors. Use proper types to check property
existence during compilation.

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
let s = person.office // Compile-time error
```

**See also**

* Recipe: Objects with property names that are not identifiers are not supported
* Recipe: Symbol() API is not supported
* Recipe: delete operator is not supported
* Recipe: typeof operator is allowed only in expression contexts
* Recipe: in operator is not supported
* Recipe: Property-based runtime type checks are not supported
* Recipe: Dynamic property declaration is not supported
* Recipe: Usage of standard library is restricted

## Recipe: Only `as T` syntax is supported for type casts

**Rule `arkts-as-casts`**

**Severity: error**

ArkTS supports `as` keyword as the only syntax for type casts.
Incorrect cast causes a compile-time error or runtime `ClassCastException`.
`<type>` syntax for type casts is not supported.

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

// No report is provided during compilation
// nor during runtime if cast is wrong:
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

// ClassCastException during runtime is thrown:
let c3 = createShape() as Square
```

## Recipe: JSX expressions are not supported

**Rule `arkts-no-jsx`**

**Severity: error**

Do not use JSX since no alternative is provided to rewrite it.

## Recipe: Unary operators `+`, `-` and `~` work only on numbers

**Rule `arkts-no-polymorphic-unops`**

**Severity: error**

ArkTS allows unary operators to work on numeric types only. A compile-time
error occurs if these operators are applied to a non-numeric type. Unlike in
TypeScript, implicit casting of strings in this context is not supported and must
be done explicitly.

**TypeScript**

```typescript
let a = +5   // 5 as number
let b = +"5" // 5 as number
let c = -5   // -5 as number
let d = -"5" // -5 as number
let e = ~5   // -6 as number
let f = ~"5" // -6 as number
let g = +"string" // NaN as number
```

**ArkTS**

```typescript
let a = +5   // 5 as number
let b = +"5" // Compile-time error
let c = -5   // -5 as number
let d = -"5" // Compile-time error
let e = ~5   // -6 as number
let f = ~"5" // Compile-time error
let g = +"string" // Compile-time error
```

**See also**

* Recipe: Binary operators \*, /, %, -, <<, >>, >>>, &, ^ and | work only on numeric types
* Recipe: Binary + operator supports implicit casts only for numbers and strings

## Recipe: Unary `+` cannot be used for casting to `number`

**Rule `arkts-no-unary-plus-cast`**

**Severity: error**

ArkTS does not support casting from any type to a numeric type
by using the unary `+` operator, which can be applied only to
numeric types.

**TypeScript**

```typescript
function returnTen(): string {
    return "-10"
}

function returnString(): string {
    return "string"
}

let a = +returnTen()    // -10 as number
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

let a = +returnTen()    // Compile-time error
let b = +returnString() // Compile-time error
```

**See also**

* Recipe: Unary operators +, - and ~ work only on numbers
* Recipe: Binary operators \*, /, %, -, <<, >>, >>>, &, ^ and | work only on numeric types
* Recipe: Binary + operator supports implicit casts only for numbers and strings

## Recipe: `delete` operator is not supported

**Rule `arkts-no-delete`**

**Severity: error**

ArkTS assumes that object layout is known at compile time and cannot be
changed at runtime. Thus the operation of deleting a property makes no sense.

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
// To mimic the original semantics, you may declare a nullable type
// and assign null to mark value absence:

class Point {
    x: number | null
    y: number | null
}

let p = new Point()
p.y = null
```

**See also**

* Recipe: Objects with property names that are not identifiers are not supported
* Recipe: Symbol() API is not supported
* Recipe: Attempt to access an undefined property is a compile-time error
* Recipe: typeof operator is allowed only in expression contexts
* Recipe: in operator is not supported
* Recipe: Property-based runtime type checks are not supported
* Recipe: Dynamic property declaration is not supported

## Recipe: `typeof` operator is allowed only in expression contexts

**Rule `arkts-no-type-query`**

**Severity: error**

ArkTS supports `typeof` operator only in the expression context. Specifying
type notations using `typeof` is not supported.

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

**See also**

* Recipe: Objects with property names that are not identifiers are not supported
* Recipe: Symbol() API is not supported
* Recipe: Attempt to access an undefined property is a compile-time error
* Recipe: delete operator is not supported
* Recipe: in operator is not supported
* Recipe: Property-based runtime type checks are not supported
* Recipe: Dynamic property declaration is not supported
* Recipe: Usage of standard library is restricted

## Recipe: Binary operators `*`, `/`, `%`, `-`, `<<`, `>>`, `>>>`, `&`, `^` and `|` work only on numeric types

**Rule `arkts-no-polymorphic-binops`**

**Severity: error**

ArkTS allows applying binary operators `*`, `/`, `%`, `-`, `<<`,
`>>`, `>>>`, `&`, `^` and `|` only to values of numeric types.
Implicit casts from other types to numeric types are prohibited and cause
compile-time errors.

**TypeScript**

```typescript
let a = (5 & 5)     // 5
let b = (5.5 & 5.5) // 5, not 5.5
let c = (5 | 5)     // 5
let d = (5.5 | 5.5) // 5, not 5.5

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
let b = (5.5 & 5.5) // Compile-time error
let c = (5 | 5)     // 5
let d = (5.5 | 5.5) // Compile-time error

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

**See also**

* Recipe: Unary operators +, - and ~ work only on numbers
* Recipe: Unary + cannot be used for casting to number
* Recipe: Binary + operator supports implicit casts only for numbers and strings

## Recipe: Binary `+` operator supports implicit casts only for numbers and strings

**Rule `arkts-no-polymorphic-plus`**

**Severity: error**

ArkTS supports implicit casts for `+` only for strings and numbers.
Elsewhere, any form of an explicit cast to string is required.

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

**See also**

* Recipe: Unary operators +, - and ~ work only on numbers
* Recipe: Unary + cannot be used for casting to number
* Recipe: Binary operators \*, /, %, -, <<, >>, >>>, &, ^ and | work only on numeric types

## Recipe: `instanceof` operator is partially supported

**Rule `arkts-instanceof-ref-types`**

**Severity: error**

In TypeScript, the left-hand side of an `instanceof` expression must be of type
`any`, an object type or a type parameter, otherwise the result is `false`.
In ArkTS, the left-hand side expression may be of any reference type, otherwise
a compile-time error occurs. In addition, the left operand in ArkTS cannot be
a type.

**TypeScript**

```typescript
class X {}

let a = (new X()) instanceof Object // true
let b = (new X()) instanceof X // true
// left operand is a type:
let c = X instanceof Object // true
let d = X instanceof X // false

// left operand is not of type any
let e = (5.0 as Number) instanceof Number // false
```

**ArkTS**

```typescript
class X {}

let a = (new X()) instanceof Object // true
let b = (new X()) instanceof X // true
// left operand is a type:
let c = X instanceof Object // Compile-time error
let d = X instanceof X // Compile-time error

// left operand may be of any reference type, like number
let e = (5.0 as Number) instanceof Number // true
```

## Recipe: `in` operator is not supported

**Rule `arkts-no-in`**

**Severity: error**

ArkTS does not support the `in` operator. However, this operator makes
little sense since the object layout is known at compile time and cannot
be modified at runtime. Use `instanceof` as a work-around if you still need
to check whether certain class members exist.

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

let b = p instanceof Person // true, and "name" is guaranteed to be present
```

**See also**

* Recipe: Objects with property names that are not identifiers are not supported
* Recipe: Symbol() API is not supported
* Recipe: Attempt to access an undefined property is a compile-time error
* Recipe: delete operator is not supported
* Recipe: typeof operator is allowed only in expression contexts
* Recipe: Property-based runtime type checks are not supported
* Recipe: Dynamic property declaration is not supported
* Recipe: Usage of standard library is restricted

## Recipe: Destructuring assignment is not supported

**Rule `arkts-no-destruct-assignment`**

**Severity: error**

ArkTS does not support destructuring assignment. Other idioms (e.g.,
using a temporary variable, where applicable) can be used for replacement.

**TypeScript**

```typescript
let [one, two] = [1, 2]; // semicolon is required here
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
let tail = new Number[data.length - 1]
for (let i = 1; i < data.length; ++i) {
    tail[i - 1] = data[i]
}
```

## Recipe: The comma operator `,` is supported only in `for` loops

**Rule `arkts-no-comma-outside-loops`**

**Severity: error**

ArkTS supports the comma operator `,` only in `for` loops. Otherwise,
it is useless as it makes the execution order harder to understand.

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

// Use explicit execution order instead of the comma operator:
let x = 0
++x
x = x++
```

## Recipe: Destructuring variable declarations are not supported

**Rule `arkts-no-destruct-decls`**

**Severity: error**

ArkTS does not support destructuring variable declarations. This is a dynamic
feature relying on structural compatibility. In addition, names in destructuring
declarations must be equal to properties within destructured classes.

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

// Create an intermediate object and work with it field by field
// without name restrictions:
let zp = returnZeroPoint()
let x = zp.x
let y = zp.y
```

## Recipe: Inference of implied types is not supported

**Rule `arkts-no-implied-inference`**

**Severity: error**

Currently, ArkTS does not support inference of implied types. Use explicit
type notation instead. Use `Object[]` if you need containers that hold
data of mixed types.

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

## Recipe: Type annotation in catch clause is not supported

**Rule `arkts-no-types-in-catch`**

**Severity: error**

In TypeScript catch clause variable type annotation must be `any` or `unknown`
if specified. As ArkTS does not support these types, a type annotation should
be omitted.

**TypeScript**

```typescript
try {
    // some code
}
catch (a: unknown) {}
```

**ArkTS**

```typescript
try {
    // some code
}
catch (a) {}
```

**See also**

* Recipe: throw statements cannot accept values of arbitrary types

## Recipe: `for .. in` is not supported

**Rule `arkts-no-for-in`**

**Severity: error**

ArkTS does not support the iteration over object contents by the
`for .. in` loop. For objects, iteration over properties at runtime is
considered redundant because object layout is known at compile time and cannot
change at runtime. For arrays, you can iterate with the regular `for` loop.

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

**See also**

* Recipe: Iterable interfaces are not supported
* Recipe: for-of is supported only for arrays and strings

## Recipe: Iterable interfaces are not supported

**Rule `arkts-noiterable`**

**Severity: error**

ArkTS does not support the `Symbol` API, `Symbol.iterator` and
eventually iterable interfaces. Use arrays and library-level containers to
iterate over data.

**See also**

* Recipe: Symbol() API is not supported
* Recipe: for .. in is not supported
* Recipe: for-of is supported only for arrays and strings

## Recipe: `for-of` is supported only for arrays and strings

**Rule `arkts-for-of-str-arr`**

**Severity: error**

ArkTS supports the iteration over arrays and strings by the `for .. of` loop,
but does not support the iteration of objects content.

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

**See also**

* Recipe: for .. in is not supported
* Recipe: Iterable interfaces are not supported

## Recipe: Mapped type expression is not supported

**Rule `arkts-no-mapped-types`**

**Severity: error**

ArkTS does not support mapped types. Use other language idioms and regular
classes to achieve the same behaviour.

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

**See also**

* Recipe: keyof operator is not supported

## Recipe: `with` statement is not supported

**Rule `arkts-no-with`**

**Severity: error**

ArkTS does not support the `with` statement. Use other language idioms
(including fully qualified names of functions) to achieve the same behaviour.

## Recipe: Values computed at runtime are not supported in `case` statements

**Rule `arkts-no-computed-case`**

**Severity: error**

ArkTS supports `case` statements that contain only compile-time values.
Use `if` statements as an alternative.

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

## Recipe: `switch` statements cannot accept values of arbitrary types

**Rule `arkts-limited-switch`**

**Severity: error**

ArkTS restricts the types that are supported in `switch` statements. In
particular, values of the types `number`, `Number`, `string`, `String`
or `enum` are supported. Use `if` statements in case of unsupported types.

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

## Recipe: `throw` statements cannot accept values of arbitrary types

**Rule `arkts-limited-throw`**

**Severity: error**

ArkTS supports throwing only objects of the class `Error` or any
derived class. Throwing an arbitrary type (i.e., a `number` or `string`)
is prohibited.

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

## Recipe: Function return type inference is limited

**Rule `arkts-no-implicit-return-types`**

**Severity: error**

ArkTS supports type inference for function return types, but this functionality
is currently restricted. In particular, when the expression in the `return`
statement is a call to a function or method whose return value type is omitted,
a compile-time error occurs. In case of any such error, specify the return type
explicitly.

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
// Explicit return type is required:
function f(x: number) : number {
    if (x <= 0) {
        return x
    }
    return g(x)
}

// Explicit return type is required:
function g(x: number) : number {
    return f(x - 1)
}

// In this case, return type will be inferred
function doOperation(x: number, y: number) {
    return x + y
}

console.log(f(10))
console.log(doOperation(2, 3))
```

## Recipe: Destructuring parameter declarations are not supported

**Rule `arkts-no-destruct-params`**

**Severity: error**

ArkTS requires that parameters must be passed directly to the function, and
local names must be assigned manually.

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

## Recipe: Nested functions are not supported

**Rule `arkts-no-nested-funcs`**

**Severity: error**

ArkTS does not support nested functions. Use lambdas instead.

**TypeScript**

```typescript
function addNum(a: number, b: number): void {

    // nested function:
    function logToConsole(message: String): void {
        console.log(message)
    }

    let result = a + b

    // Invoking the nested function:
    logToConsole("result is " + result)
}
```

**ArkTS**

```typescript
function addNum(a: number, b: number): void {
    // Use lambda instead of a nested function:
    let logToConsole: (message: string) => void = (message: string): void => {
        console.log(message)
    }

    let result = a + b

    logToConsole("result is " + result)
}
```

## Recipe: Using `this` inside stand-alone functions is not supported

**Rule `arkts-no-standalone-this`**

**Severity: error**

ArkTS does not support the usage of `this` inside stand-alone functions.
`this` can be used in methods only.

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
console.log(a.count) // prints "1"
a.m(2)
console.log(a.count) // prints "2"
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
    console.log(a.count)  // prints "1"
    a.m(2)
    console.log(a.count)  // prints "2"
}
```

**See also**

* Recipe: Function.apply, Function.bind, Function.call are not supported

## Recipe: Generator functions are not supported

**Rule `arkts-no-generators`**

**Severity: error**

Currently, ArkTS does not support generator functions.
Use the `async` / `await` mechanism for multitasking.

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
    // Some complex logic for proccessing the number here
    return n
}

async function foo() {
    for (let i = 1; i <= 5; i++) {
        console.log(await complexNumberProcessing(i))
    }
}

foo()
```

## Recipe: Type guarding is supported with `instanceof` and `as`

**Rule `arkts-no-is`**

**Severity: error**

ArkTS does not support the `is` operator, which must be replaced by the
`instanceof` operator. Note that the fields of an object must be cast to the
appropriate type with the `as` operator before use.

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
        console.log(arg.bar)    // Compile-time error
    } else {
        console.log(arg.foo)    // Compile-time error
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
        console.log(arg.bar)        // Compile-time error
    } else {
        let barArg = arg as Bar
        console.log(arg.foo)        // Compile-time error
        console.log(barArg.bar)     // OK
    }
}

function main(): void {
    doStuff(new Foo())
    doStuff(new Bar())
}
```

## Recipe: `keyof` operator is not supported

**Rule `arkts-no-keyof`**

**Severity: error**

ArkTS has no keyof operator because the object layout is defined
at compile time and cannot be changed at runtime. Object fields can only be
accessed directly.

**TypeScript**

```typescript
class Point {
    x: number = 1
    y: number = 2
}

type PointKeys = keyof Point  // The type of PointKeys is "x" | "y"

function getPropertyValue(obj: Point, key: PointKeys) {
    return obj[key]
}

let obj = new Point()
console.log(getPropertyValue(obj, "x"))  // prints "1"
console.log(getPropertyValue(obj, "y"))  // prints "2"
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
    throw new Error()  // No such property
    return 0
}

function main(): void {
    let obj = new Point()
    console.log(getPropertyValue(obj, "x"))  // prints "1"
    console.log(getPropertyValue(obj, "y"))  // prints "2"
}
```

## Recipe: It is possible to spread only arrays into the rest parameter

**Rule `arkts-no-spread`**

**Severity: error**

The only supported scenario for the spread operator is to spread an array into
the rest parameter. Otherwise manually “unpack” data from arrays and objects,
where necessary.

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

## Recipe: Interface declarations (extends same property)

**Rule `arkts-no-extend-same-property`**

**Severity: error**

In TypeScript, an interface that extends two other interfaces with the same method,
must declare that method with a combined result type. It is not allowed in
ArkTS because ArkTS does not allow an interface to contain two methods with
signatures that are  not distinguishable, e.g., two methods that have the same
parameter lists, but different return types.

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

## Recipe: Declaration merging is not supported

**Rule `arkts-no-decl-merging`**

**Severity: error**

ArkTS does not support merging declratations. All definitions of classes,
interfaces and so on must be kept compact in the code base.

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

## Recipe: Interfaces cannot extend classes

**Rule `arkts-extends-only-class`**

**Severity: error**

ArkTS does not support interfaces that extend classes. Interfaces can extend
only interfaces.

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

## Recipe: Property-based runtime type checks are not supported

**Rule `arkts-no-prop-existence-check`**

**Severity: error**

ArkTS requires that object layout is determined in compile-time and cannot
be changed at runtime. There for no runtime property-based checks are supported.
If you need to do a type cast, use `as` operator and use desired properties
and methods. If some property doesn’t exist then an attempt to reference it
will result in a compile-time error.

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
    console.log("Yes")  // prints "Yes" in this example
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
    obj.some_foo()  // Compile-time error: Method some_foo does not
                    // exist on this type
}
```

**See also**

* Recipe: Objects with property names that are not identifiers are not supported
* Recipe: Symbol() API is not supported
* Recipe: Attempt to access an undefined property is a compile-time error
* Recipe: delete operator is not supported
* Recipe: typeof operator is allowed only in expression contexts
* Recipe: in operator is not supported
* Recipe: Dynamic property declaration is not supported
* Recipe: Usage of standard library is restricted

## Recipe: Constructor function type is not supported

**Rule `arkts-no-ctor-signatures-funcs`**

**Severity: error**

ArkTS does not support the usage of the constructor function type.
Use lambdas instead.

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

## Recipe: Dynamic property declaration is not supported

**Rule `arkts-no-dyn-prop-decl`**

**Severity: error**

ArkTS does not support dynamic property declaration. All object properties must
be declared immediately in the class. While it can be replaced with an array
of objects, it is still better to adhere to the static language paradigm and
declare fields, their names and types explicitly.

**TypeScript**

```typescript
class Person {
    name: string = ""
    age: number = 0; // semicolon is required here
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

**See also**

* Recipe: Objects with property names that are not identifiers are not supported
* Recipe: Symbol() API is not supported
* Recipe: Attempt to access an undefined property is a compile-time error
* Recipe: delete operator is not supported
* Recipe: typeof operator is allowed only in expression contexts
* Recipe: in operator is not supported
* Recipe: Property-based runtime type checks are not supported
* Recipe: Usage of standard library is restricted

## Recipe: Enumeration members can be initialized only with compile time expressions of the same type

**Rule `arkts-no-enum-mixed-types`**

**Severity: error**

ArkTS does not support initializing members of enumerations with expressions
that are evaluated during program runtime. Besides, all explicitly set
initializers must be of the same time.

**TypeScript**

```typescript
enum E1 {
    A = 0xa,
    B = 0xb,
    C = Math.random(),
    D = 0xd,
    E // 0xe inferred
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
    E // 0xe inferred
}

enum E2 {
    A = "0xa",
    B = "0xb",
    C = "0xc",
    D = "0xd"
}
```

## Recipe: `enum` declaration merging is not supported

**Rule `arkts-no-enum-merging`**

**Severity: error**

ArkTS does not support merging declratations for `enum`.
The declaration of each `enum` must be kept compact in the code base.

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

## Recipe: Namespaces cannot be used as objects

**Rule `arkts-no-ns-as-obj`**

**Severity: error**

ArkTS does not support the usage of namespaces as objects.
Classes or modules can be interpreted as analogues of namespaces.

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

## Recipe: Scripts and modules

**Rule `arkts-no-scripts`**

**Severity: error**

In general, scripts and modules in ArkTS are very close to TypeScript.
Differences are described in separate recipes.

**See also**

* Recipe: Special import type declarations are not supported
* Recipe: Importing a module for side-effects only is not supported
* Recipe: import default as ... is not supported
* Recipe: require is not supported
* Recipe: Renaming in export declarations is not supported
* Recipe: Export list declaration is not supported
* Recipe: Re-exporting is not supported
* Recipe: export = ... assignment is not supported

## Recipe: Non-declaration statements in namespaces are not supported

**Rule `arkts-no-ns-statements`**

**Severity: error**

ArkTS does not support statements in namespaces. Use a function to exectute
statements.

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

// Initialization function should be called to execute statements:
A.init()
```

## Recipe: Special import type declarations are not supported

**Rule `arkts-no-special-imports`**

**Severity: error**

ArkTS does not have a special notation for importing types.
Use ordinary import instead.

**TypeScript**

```typescript
// Re-using the same import
import { APIResponseType } from "./api"

// Explicitly use import type
import type { APIResponseType } from "./api"
```

**ArkTS**

```typescript
import { APIResponseType } from "./api"
```

**See also**

* Recipe: Importing a module for side-effects only is not supported
* Recipe: import default as ... is not supported
* Recipe: require is not supported

## Recipe: Importing a module for side-effects only is not supported

**Rule `arkts-no-side-effects-imports`**

**Severity: error**

ArkTS does not support global variables like `window` to avoid
side-effects during module importing. All variables marked as export can be
accessed through the `*` syntax.

**TypeScript**

```typescript
// === module at "path/to/module.ts"
export const EXAMPLE_VALUE = 42

// Set a global variable
window.MY_GLOBAL_VAR = "Hello, world!"

// ==== using this module:
import "path/to/module"
```

**ArkTS**

```typescript
import * from "path/to/module"
```

## Recipe: `import default as ...` is not supported

**Rule `arkts-no-import-default-as`**

**Severity: error**

ArkTS does not support `import default as ...` syntax.
Use explicit `import ... from ...` instead.

**TypeScript**

```typescript
import { default as d } from "mod"
```

**ArkTS**

```typescript
import d from "mod"
```

## Recipe: `require` is not supported

**Rule `arkts-no-require`**

**Severity: error**

ArkTS does not support importing via `require`. Use `import` instead.

**TypeScript**

```typescript
import m = require("mod")
```

**ArkTS**

```typescript
import * as m from "mod"
```

## Recipe: Renaming in export declarations is not supported

**Rule `arkts-no-export-renaming`**

**Severity: error**

ArkTS does not support renaming in export declarations. Similar effect
can be achieved through setting an alias for the exported entity.

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

**See also**

* Recipe: Export list declaration is not supported
* Recipe: Re-exporting is not supported
* Recipe: export = ... assignment is not supported

## Recipe: Export list declaration is not supported

**Rule `arkts-no-export-list-decl`**

**Severity: error**

ArkTS does not support syntax of export list declarations. All exported
entities must be explicitly annotated with the `export` keyword.

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
export RenamedClass = MyClass
```

**See also**

* Recipe: Renaming in export declarations is not supported
* Recipe: Re-exporting is not supported
* Recipe: export = ... assignment is not supported

## Recipe: Re-exporting is not supported

**Rule `arkts-no-reexport`**

**Severity: error**

ArkTS does not support re-exporting. All desired entities must be
imported explicitly from the modules that export them.

**TypeScript**

```typescript
// module1
export class MyClass {
    // ...
}

// module2
export { MyClass } from "module1"

// consumer module
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

// consumer module
import { MyClass } from "module1"
import * from "module2"

const myInstance = new MyClass()
```

**See also**

* Recipe: Renaming in export declarations is not supported
* Recipe: Export list declaration is not supported
* Recipe: export = ... assignment is not supported

## Recipe: `export = ...` assignment is not supported

**Rule `arkts-no-export-assignment`**

**Severity: error**

ArkTS does not support `export = ...` syntax.
Use regular `export` / `import` instead.

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

**See also**

* Recipe: Renaming in export declarations is not supported
* Recipe: Export list declaration is not supported
* Recipe: Re-exporting is not supported

## Recipe: Special export type declarations are not supported

**Rule `arkts-no-special-exports`**

**Severity: error**

ArkTS does not have a special notation for exporting types.
Use ordinary export instead.

**TypeScript**

```typescript
class C {}
export type { C }
```

**ArkTS**

```typescript
export class C {}
```

## Recipe: Ambient module declaration is not supported

**Rule `arkts-no-ambient-decls`**

**Severity: error**

ArkTS does not support ambient module declaration because it has its
own mechanisms for interoperating with JavaScript.

**TypeScript**

```typescript
declare module "someModule" {
    export function normalize(s : string) : string;
}
```

**ArkTS**

```typescript
// Import what you need from the original module
import { normalize } from "../someModule"
```

**See also**

* Recipe: Wildcards in module names are not supported
* Recipe: .js extension is not allowed in module identifiers

## Recipe: Wildcards in module names are not supported

**Rule `arkts-no-module-wildcards`**

**Severity: error**

ArkTS does not supported wildcards in module names because in ArkTS, import
is a compile-time, not a runtime feature. Use ordinary export syntax instead.

**TypeScript**

```typescript
declare module "*!text" {
    const content: string
    export default content
}
```

**See also**

* Recipe: Ambient module declaration is not supported
* Recipe: Universal module definitions (UMD) are not supported
* Recipe: .js extension is not allowed in module identifiers

## Recipe: Universal module definitions (UMD) are not supported

**Rule `arkts-no-umd`**

**Severity: error**

ArkTS does not support universal module definitions (UMD) because in ArkTS
there is no concept of “script” (as opposed to “module”). Besides, in ArkTS
import is a compile-time, not a runtime feature. Use ordinary syntax for
`export` and `import` instead.

**TypeScript**

```typescript
// math-lib.d.ts
export const isPrime(x: number): boolean
export as namespace mathLib

// in script
mathLib.isPrime(2)
```

**ArkTS**

```typescript
// math-lib.d.ts
namespace mathLib {
    export isPrime(x: number): boolean
}

// in program
import { mathLib } from "./math-lib"
mathLib.isPrime(2)
```

**See also**

* Recipe: Wildcards in module names are not supported

## Recipe: `.js` extension is not allowed in module identifiers

**Rule `arkts-no-js-extension`**

**Severity: error**

ArkTS does not allow to use `.js` extension in module identifiers because it
has its own mechanisms for interoperating with JavaScript.

**TypeScript**

```typescript
import { something } from "./module.js"
```

**ArkTS**

```typescript
import { something } from "./module"
```

**See also**

* Recipe: Ambient module declaration is not supported
* Recipe: Wildcards in module names are not supported

## Recipe: `new.target` is not supported

**Rule `arkts-no-new-target`**

**Severity: error**

ArkTS does not support `new.target` because there is no concept of runtime
prototype inheritance in the language. This feature is considered not applicable
to the statically typing.

**TypeScript**

```typescript
class CustomError extends Error {
    constructor(message?: string) {
        // 'Error' breaks prototype chain here:
        super(message)

        // Restore prototype chain:
        Object.setPrototypeOf(this, new.target.prototype)
    }
}
```

**See also**

* Recipe: Prototype assignment is not supported

## Recipe: Runtime import expressions are not supported

**Rule `arkts-no-runtime-import`**

**Severity: error**

ArkTS does not support such “runtime” import expressions as `await import...`
because in ArkTS import is a compile-time, not a runtime feature. Use regular
import syntax instead.

**TypeScript**

```typescript
const zipUtil = await import("./utils/create-zip-file")
```

**ArkTS**

```typescript
import { zipUtil } from "./utils/create-zip-file"
```

**See also**

* Recipe: Wildcards in module names are not supported
* Recipe: Universal module definitions (UMD) are not supported
* Recipe: Import assertions are not supported

## Recipe: Definite assignment assertions are not supported

**Rule `arkts-no-definite-assignment`**

**Severity: error**

ArkTS does not support definite assignment assertions `let v!: T` because
they are considered an excessive compiler hint. Use declaration with
initialization instead.

**TypeScript**

```typescript
let x!: number // Hint: x will be initialized before usage

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

## Recipe: IIFEs as namespace declarations are not supported

**Rule `arkts-no-iife`**

**Severity: error**

ArkTS does not support IIFEs as namespace declarations because in ArkTS,
anonymous functions cannot serve as namespaces. Use regular syntax for
namespaces instead.

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

## Recipe: Prototype assignment is not supported

**Rule `arkts-no-prototype-assignment`**

**Severity: error**

ArkTS does not support prototype assignment because there is no concept of
runtime prototype inheritance in the language. This feature is considered not
applicable to the static typing.

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

**See also**

* Recipe: new.target is not supported

## Recipe: `globalThis` is not supported

**Rule `arkts-no-globalthis`**

**Severity: error**

ArkTS does not support both global scope and `globalThis` because untyped
objects with dynamically changed layout are not supported.

**TypeScript**

```typescript
// in a global file:
var abc = 100

// Refers to 'abc' from above.
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

**See also**

* Recipe: Declaring properties on functions is not supported
* Recipe: Usage of standard library is restricted

## Recipe: Utility types are not supported

**Rule `arkts-no-utility-types`**

**Severity: error**

Currently ArkTS does not support utility types from TypeScript extensions to the
standard library (`Omit`, `Partial`, `Readonly`, `Record`, `Pick`,
etc.).

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

## Recipe: Declaring properties on functions is not supported

**Rule `arkts-no-func-props`**

**Severity: error**

ArkTS does not support declaring properties on functions because there is no
support for objects with dynamically changing layout. Function objects follow
this rule and their layout cannot be changed in runtime.

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
    // async implementation
}

function readImageSync(path: string) : MyImage {
    // sync implementation
}
```

**See also**

* Recipe: globalThis is not supported

## Recipe: `Function.apply`, `Function.bind`, `Function.call` are not supported

**Rule `arkts-no-func-apply-bind-call`**

**Severity: error**

ArkTS does not allow to use standard library functions `Function.apply`,
`Function.bind`, `Function.call`. These APIs are needed in the standard
library to explicitly set `this` parameter for the called function.
In ArkTS semantics of `this` is restricted to the conventional OOP style,
and usage of `this` in stand-alone functions is prohibited. Thus these
functions are excessive.

**TypeScript**

```typescript
const person = {
    firstName: "aa",

    fullName: function(): string {
        return this.firstName
    }
}

const person1 = {
    firstName: "Mary"
}

// This will log "Mary":
console.log(person.fullName.apply(person1))
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

// This will log "Mary":
console.log(person1.fullName())
```

**See also**

* Recipe: Using this inside stand-alone functions is not supported

## Recipe: `readonly T[]` syntax is not supported

**Rule `arkts-no-readonly-params`**

**Severity: error**

Currently ArkTS supports `readonly` for properties, but not for parameters.

**TypeScript**

```typescript
function foo(arr: readonly string[]) {
    arr.slice()        // OK
    arr.push("hello!") // Compile-time error
}
```

**ArkTS**

```typescript
function foo(arr: string[]) {
    arr.slice()        // OK
    arr.push("hello!") // OK
}
```

## Recipe: `as const` assertions are not supported

**Rule `arkts-no-as-const`**

**Severity: error**

ArkTS does not support `as const` assertions because in the standard TypeScript
`as const` annotates literals with corresponding literal types, and ArkTS
does not support literal types.

**TypeScript**

```typescript
// Type 'hello':
let x = "hello" as const

// Type 'readonly [10, 20]':
let y = [10, 20] as const

// Type '{ readonly text: "hello" }':
let z = { text: "hello" } as const
```

**ArkTS**

```typescript
// Type 'string':
let x : string = "hello"

// Type 'number[]':
let y : number[] = [10, 20]

class Label {
    text : string
}

// Type 'Label':
let z : Label = {
    text: "hello"
}
```

## Recipe: Import assertions are not supported

**Rule `arkts-no-import-assertions`**

**Severity: error**

ArkTS does not support import assertions because in ArkTS, import is a
compile-time, not a runtime feature. So asserting correctness of imported APIs
in runtime does not make sense for the statically typed language. Use ordinary
`import` syntax instead.

**TypeScript**

```typescript
import { obj } from "./something.json" assert { type: "json" }
```

**ArkTS**

```typescript
// Correctness of importing T will be checked in compile-time:
import { something } from "./module"
```

**See also**

* Recipe: Wildcards in module names are not supported
* Recipe: Universal module definitions (UMD) are not supported
* Recipe: Runtime import expressions are not supported

## Recipe: Usage of standard library is restricted

**Rule `arkts-limited-stdlib`**

**Severity: error**

ArkTS does not allow usage of some APIs from the TypeScript/JavaScript standard library.
The most part of the restricted APIs relates to manipulating objects in
dynamic manner, which is not compatible with the static typing. Following APIs
are prohibited from usage:

Properties and functions of the global object: `eval`,
`Infinity`, `NaN`, `isFinite`, `isNaN`, `parseFloat`, `parseInt`,
`encodeURI`, `encodeURIComponent`, `Encode`,
`decodeURI`, `decodeURIComponent`, `Decode`,
`escape`, `unescape`, `ParseHexOctet`

`Object`: `__proto__`, `__defineGetter__`, `__defineSetter__`,
`__lookupGetter__`, `__lookupSetter__`, `assign`, `create`,
`defineProperties`, `defineProperty`, `entries`, `freeze`,
`fromEntries`, `getOwnPropertyDescriptor`, `getOwnPropertyDescriptors`,
`getOwnPropertyNames`, `getOwnPropertySymbols`, `getPrototypeOf`,
`hasOwn`, `hasOwnProperty`, `is`, `isExtensible`, `isFrozen`,
`isPrototypeOf`, `isSealed`, `keys`, `preventExtensions`,
`propertyIsEnumerable`, `seal`, `setPrototypeOf`, `values`

`Reflect`: `apply`, `construct`, `defineProperty`, `deleteProperty`,
`get`, `getOwnPropertyDescriptor`, `getPrototypeOf`, `has`,
`isExtensible`, `ownKeys`, `preventExtensions`, `set`,
`setPrototypeOf`

`Proxy`: `handler.apply()`, `handler.construct()`,
`handler.defineProperty()`, `handler.deleteProperty()`, `handler.get()`,
`handler.getOwnPropertyDescriptor()`, `handler.getPrototypeOf()`,
`handler.has()`, `handler.isExtensible()`, `handler.ownKeys()`,
`handler.preventExtensions()`, `handler.set()`, `handler.setPrototypeOf()`

`Array`: `isArray`

`ArrayBuffer`: `isView`

**See also**

* Recipe: Objects with property names that are not identifiers are not supported
* Recipe: Symbol() API is not supported
* Recipe: Attempt to access an undefined property is a compile-time error
* Recipe: typeof operator is allowed only in expression contexts
* Recipe: in operator is not supported
* Recipe: Property-based runtime type checks are not supported
* Recipe: Dynamic property declaration is not supported
* Recipe: globalThis is not supported
