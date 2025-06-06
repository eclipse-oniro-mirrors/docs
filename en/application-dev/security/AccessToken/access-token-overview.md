# Access Control Overview

Applications can access limited system resources by default. However, to provide extended features, an application may need to access excess system data (or personal data) or functions. The system must also provide explicit APIs to share data or functions.

To prevent improper or malicious use of data or functions, the system provides a variety of access control mechanisms, including the application sandbox, application permissions, and system components.

## Application Sandbox

All applications running on the system are deployed in independent sandbox directories, which isolate the data of different applications and prevent improper application behavior, such as unauthorized data access between applications and device tampering. Each application has a unique ID ([TokenID](app-permission-mgmt-overview.md#basic-concepts-in-the-permission-mechanism)), which can be used to identify the application and restrict its access behavior.

The application sandbox directory specifies the data range visible to an application. For details, see [Application Sandbox](../../file-management/app-sandbox-directory.md).

## Application Permissions

The system has process domain and data domain labels set based on the Ability Privilege Level (APL) of an application, and uses the access control mechanism to restrict the data accessible to each application. This minimizes the risks of application data leakage.

Applications of different APLs are assigned permissions at different levels. The strict hierarchical permission management provides robust defense against malicious attacks and ensures system security and reliability. In addition to system resources (such as Contacts) and system capabilities (such as Camera and Microphone), some kernel resources (such as executable anonymous memory) are also protected by permissions. These permissions are called KernelPermissions.

For more information, see [Application Permission Management Overview](app-permission-mgmt-overview.md).

## Secure Access Mechanism

OpenHarmony provides a secure access mechanism to redefine the way for applications to obtain private data. Instead of managing permissions, users only need to manage data and grant system data as required. For example, when a user wants to change a profile photo on a social platform, the application can only use the photo selected by the user instead of accessing the Gallery. This mechanism isolates the user's privacy data from the application, safeguarding user privacy.

Specifically, the secure access mechanism is implemented by system Pickers and security components, which allow an application to temporarily access a restricted resource without requesting the permission from the user. This mechanism implements precise permission control while better protecting user privacy.

- [System Pickers](../../application-models/system-app-startup.md)

  A Picker is implemented by an independent system process. It provides a safe, built-in way for users to grant your application access to only selected resources. By starting a Picker component, the application can access the resources, such as images or documents, selected by the user using the Picker. For example, before accessing a user's image, an application normally needs to request user authorization. However, by using **PhotoViewPicker**, the application can directly access the image selected by the user.

- [Security components](security-component-overview.md)

  Security components are a set of button-like ArkUI components provided with certain permissions. You can integrate them to your application UI. When a security component is tapped, the application is temporarily granted with the related permission. For example, if your application needs to access pasteboard data, you can use **PasteButton** in the UI. After the user taps the **PasteButton** button, the application can access the pasteboard data without displaying any permission request dialog box. This ensures security while minimizing the interference of pop-ups to users.
