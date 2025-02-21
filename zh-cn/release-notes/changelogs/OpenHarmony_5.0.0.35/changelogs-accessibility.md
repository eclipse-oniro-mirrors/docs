# 无障碍子系统Changelog

## cl.accessibility.1 Accessibility扩展服务相关API废弃

**访问级别**

公开接口

**变更原因**

为提升系统安全性，无障碍不再开放扩展服务接口能力。

**变更影响**

1. 该变更为不兼容变更；

2. Accessibility模块扩展服务接口废弃；

3. 设置-辅助功能下，不再提供已安装的服务查询和管理功能。

**变更发生版本**

从OpenHarmony SDK 5.0.0.35开始。

**变更的接口/组件**

1. 以下接口废弃：

    | 所属包名         | 方法声明                        |起始API Level|
    | ----------- | ------------------------- |------------------------- |
    | AccessibilityExtensionContext | setTargetBundleName(targetNames: Array<string>, callback: AsyncCallback<void>): void;   |9   |
    | AccessibilityExtensionContext | setTargetBundleName(targetNames: Array<string>): Promise<void>;   |9   |
    | AccessibilityExtensionContext | getFocusElement(isAccessibilityFocus: boolean, callback: AsyncCallback<AccessibilityElement>): void;   |9   |
    | AccessibilityExtensionContext | getFocusElement(isAccessibilityFocus?: boolean): Promise<AccessibilityElement>;   |9   |
    | AccessibilityExtensionContext | getFocusElement(callback: AsyncCallback<AccessibilityElement>): void;   |9   |
    | AccessibilityExtensionContext | getWindowRootElement(windowId: number, callback: AsyncCallback<AccessibilityElement>): void; |9   |
    | AccessibilityExtensionContext | getWindowRootElement(windowId?: number): Promise<AccessibilityElement>; |9   |
    | AccessibilityExtensionContext |  getWindowRootElement(callback: AsyncCallback<AccessibilityElement>): void; |9   |
    | AccessibilityExtensionContext |  getWindows(displayId: number, callback: AsyncCallback<Array<AccessibilityElement>>): void; |9   |
    | AccessibilityExtensionContext |   getWindows(displayId?: number): Promise<Array<AccessibilityElement>>; |9   |
    | AccessibilityExtensionContext |  getWindows(callback: AsyncCallback<Array<AccessibilityElement>>): void; |9   |
    | AccessibilityExtensionContext |  injectGestureSync(gesturePath: GesturePath): void; |10   |
    | AccessibilityExtensionContext |   attributeNames<T extends keyof ElementAttributeValues>(callback: AsyncCallback<Array<T>>): void; |9   |
    | AccessibilityExtensionContext |   attributeNames<T extends keyof ElementAttributeValues>(): Promise<Array<T>>; |9   |
    | AccessibilityExtensionContext |   attributeValue<T extends keyof ElementAttributeValues>(attributeName: T, callback: AsyncCallback<ElementAttributeValues[T]>): void; |9   |
    | AccessibilityExtensionContext | attributeValue<T extends keyof ElementAttributeValues>(attributeName: T): Promise<ElementAttributeValues[T]>; |9   |
    | AccessibilityExtensionContext |   actionNames(callback: AsyncCallback<Array<string>>): void; |9   |
    | AccessibilityExtensionContext |   actionNames(): Promise<Array<string>>; |9   |
    | AccessibilityExtensionContext | performAction(actionName: string, parameters: object, callback: AsyncCallback<void>): void; |9   |
    | AccessibilityExtensionContext |   performAction(actionName: string, parameters?: object): Promise<void>; |9   |
    | AccessibilityExtensionContext |   performAction(actionName: string, callback: AsyncCallback<void>): void; |9   |
    | AccessibilityExtensionContext |  findElement(type: 'content', condition: string, callback: AsyncCallback<Array<AccessibilityElement>>): void; |9   |
    | AccessibilityExtensionContext | findElement(type: 'content', condition: string): Promise<Array<AccessibilityElement>>; |9   |
    | AccessibilityExtensionContext | findElement(type: 'focusType', condition: FocusType, callback: AsyncCallback<AccessibilityElement>): void; |9   |
    | AccessibilityExtensionContext | findElement(type: 'focusType', condition: FocusType): Promise<AccessibilityElement>; |9   |
    | AccessibilityExtensionContext | findElement(type: 'focusDirection', condition: FocusDirection, callback: AsyncCallback<AccessibilityElement>): void; |9   |
    | AccessibilityExtensionContext |   findElement(type: 'focusDirection', condition: FocusDirection): Promise<AccessibilityElement>; |9   |
    | ohos.accessibility | function on(type: 'accessibilityStateChange', callback: Callback<boolean>): void; |7   |
    | ohos.accessibility |  function on(type: 'touchGuideStateChange', callback: Callback<boolean>): void; |7   |
    | ohos.accessibility | function off(type: 'accessibilityStateChange', callback?: Callback<boolean>): void; |7   |
    | ohos.accessibility | function off(type: 'touchGuideStateChange', callback?: Callback<boolean>): void; |7   |
    | ohos.accessibility |   function getCaptionsManager(): CaptionsManager; |8   |
    | ohos.application.AccessibilityExtensionAbility |   onConnect(): void; |9   |
    | ohos.application.AccessibilityExtensionAbility |   onDisconnect(): void; |9   |
    | ohos.application.AccessibilityExtensionAbility |   onAccessibilityEvent(event: AccessibilityEvent): void; |9   |
    | ohos.application.AccessibilityExtensionAbility |   onKeyEvent(keyEvent: KeyEvent): boolean; |9   |
    | ohos.accessibility.GesturePath |   constructor(durationTime: number); |9   |
    | ohos.accessibility.GesturePoint |  constructor(positionX: number, positionY: number); |9   |


2. 以下接口删除：

    | 所属包名         | 方法声明                        |起始API Level|
    | ----------- | ------------------------- |------------------------- |
    | AccessibilityExtensionContext | getCursorPosition(callback: AsyncCallback<number>): void;   |12   |
    | AccessibilityExtensionContext | getCursorPosition(): Promise<number>;   |12   |
    | AccessibilityExtensionContext | findElement(type: 'textType', condition: string): Promise<Array<AccessibilityElement>>;   |12   |
    | AccessibilityExtensionContext | findElement(type: 'elementId', condition: number): Promise<AccessibilityElement>;   |12   |


3. 设置-辅助功能下，不再提供已安装的服务查询和管理功能。

**适配指导**

此变更开发者无需适配。