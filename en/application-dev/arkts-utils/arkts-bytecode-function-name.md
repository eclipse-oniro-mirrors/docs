# Naming Rules of Ark Bytecode Functions

## Abstract
This topic describes the naming rules of the string pointed by the **name_off** field of [Method](arkts-bytecode-file-format.md#method) in the bytecode file. These rules take effect since the Ark Bytecode in version **12.0.4.0**.
## Entry Point Function
Function that is executed when the module is loaded. The function name is fixed to **func_main_0**.
## Non-entry Point Function
The name structure of other functions in the bytecode file is as follows:
```ts
##Prefix#Original function name
```
The following sections will describe the prefix and original function name in detail.
### Prefix
The prefix contains the scope information when the function is defined. It consists of the following parts:
* Scope Label
* Scope Name
* Duplicate Sequence Number

The prefix structure is as follows:
```ts
<Scope Label 1><Scope Name 1>[<Duplicate Sequence Number>]<Scope Label 2><Scope Name 2><[Duplicate Sequence Number]>...<Scope Label n><Scope Name n>[<Duplicate Sequence Number >]<Scope Label n+1>
```
In this case, angle brackets (< >) are separators for easy reading and are excluded from the actual prefix; square brackets ([ ]) indicate that the value can be empty. [\<Duplicate Sequence Number>] is required only when duplicate scopes exist, which indicates that [\<Duplicate Sequence Number>] can be empty. The last scope label is the one corresponding to the function.
#### Scope Label
The scope label indicates the scope type. The following table lists the scopes and corresponding labels. Other scopes are not recorded in the function name.
| Scope| Scope Label| Description|
| --- | --- | --- |
| Class| `~` | Scope defined by the **class** keywords.|
| Instance function| `>` | Scope defined by the instance functions of a class|
| Static function| `<` | Scope defined by the static functions of a class|
| Constructor used to create a worker object.| `=` | Scope defined by the constructors of a class|
| Common function| `*` | Scopes defined by all functions except the preceding types|
| namespace/module | `&` | Scope defined by the **namespace** or **module** keywords|
| enum | `%` | Scope defined by the **enum** keywords|
#### Scope Name
The name used to define the scope in the source code. If the value is anonymous, the value is an empty string. To reduce the bytecode size, the ArkCompiler optimizes long scope names. In this case, the scope names are displayed in the format of **@hexadecimal number**. This number indicates the index of the scope name in a string array. In the bytecode file, there is a [field](arkts-bytecode-file-format.md#field) named **ScopeNames** in the [Class](arkts-bytecode-file-format.md#class) corresponding to the source code. This **field** value points to an offset of [LiteralArray](arkts-bytecode-file-format.md#literalarray) which stores a string array. The hexadecimal number is the index of the scope name in this array. The original function name is not converted to an index.
Example:
```ts
function longFuncName() {                  // The function name of longFuncName is "#*#longFuncName", in which "longFuncName" is the original function name and will not be converted to an index.
    function A() { }                       // The function name of A is "#*@0*#A", where "@0" indicates the string whose index is 0 in the corresponding LiteralArray. In this case, the string is "longFuncName", which means that the original name of this function is "#*longFuncName*#A".
    function B() { }                       // The function name of B is "#*@0*#B".
}  
```
#### Duplicate Sequence Number
If an entity with the same name exists in the same scope within the source code, the entity name is suffixed with a duplicate sequence number. This number is written in the format of **^ hexadecimal number**. If duplicate names exist, the first one is not numbered, that is, the duplicate sequence number is empty. And the entities are numbered from the second one, starting from **1**.

Example:
```ts
namespace A {
    function bar() { }                      // The function name of bar is "#&A*#bar".
}

namespace A {
    function foo() { }                      // The function name of foo is "#&A^1*#foo", where "^1" indicates the duplicate sequence number.
}
```
### Original Function Name
It indicates function name in the source code. For an anonymous function, the value is an empty string. Similarly, if a function with the same name exists in the same scope within the source code, the function name is followed by a duplicate sequence number, so does an anonymous function.

```ts
function foo() {}                           // The original function name is "foo".
() => { }                                   // The original function name is "".
() => { }                                   // The original function name is "^1".
```

#### Special Situations
1. If an anonymous function is stored in a variable when the function is defined, the original function name is the variable name. An example is as follows:
    ```ts
    let a = () => {}                            // The original function name is "a".
    ```
2. If an anonymous function is defined in an object literal and stored in a literal attribute:
* If the attribute name does not contain a **slash (\)** or a **period (.)**, the original function name is the attribute name.
    ```ts
    let B = {
        b : () => {}                            // The original function name is "b".
    }
    ```
* If the attribute name contains a **slash (\)** or a **period (.)**, the original function is named as an anonymous function to prevent ambiguity.
    ```ts
    let a = {
        "a.b#c^2": () => {}                     // The original function name is "".
        "x\\y#": () => {}                       // The original function name is "^1".
    }
    ```

**You should avoid using characters other than letters, digits, and underscores (_) to name functions to avoid ambiguity.**
## Example
```ts
namespace A {                               // The function name of namespace in bytecode is "#&#A".
    class B {                               // The function name of the constructor in bytecode is "#&A~B=#B".
        m() {                               // The function name of m in bytecode is "#&A~B>#m".
            return () => {}                 // The function name of the anonymous function in bytecode is "#&A~B>m*#".
        }
        static s() {}                       // The function name of static function s in bytecode is "#&A~B<#s".
    }
    enum E {                                // The function name of enum in bytecode is "#&A %#E".

    }
}
```
```ts
namespace LongNamespaceName {               // The function name of namespace in bytecode is "#&#LongNamespaceName".
    class LongClassName {                   // The function name of the constructor in bytecode is "#&@1~@0=#LongClassName".
        longFunctionName() {                // The function name of the instance function in the bytecode is "#&@1~@0>#longFunctionName".
        }
        longFunctionName() {                // The function name in bytecode is "#&@1~@0>#longFunctionName^1".
            function inSecondFunction() {}  // The function name in bytecode is "#&@1~@0>@2^1*#inSecondFunction".
        }
    }
}
```
