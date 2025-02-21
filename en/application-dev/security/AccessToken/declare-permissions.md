# Declaring Permissions


To apply for permissions for your application, declare all the permissions one by one in the project configuration file.


In the **module.json5** file of the application, declare the permission required in [requestPermissions](../../quick-start/module-configuration-file.md#requestpermissions).


| Name| Description| Value Range|
| -------- | -------- | -------- |
| name | Permission name. This field is mandatory.| The value must be a permission defined in the system. For details, see [Permissions for All Applications](permissions-for-all.md).|
| reason | Reason for requesting the permission. This field is mandatory only when a **user_grant** permission is requested.<br>**NOTE**<br>This field is used for application release verification. It is mandatory for a user_grant permission, and must be a resource reference to support multiple languages.| The value is a resource reference of the string type, in the $string: \*\*\* format.<br>For details, see [Specifications for reason](#specifications-for-reason).|
| usedScene | Scene under which the permission is used. It consists of **abilities** and **when**. **abilities** is an array of multiple UIAbility components, and **when** specifies when the permission is used. This field is optional.<br>**NOTE**<br>If a **user_grant** permission is requested, **abilities** is mandatory and **when** is optional.| **abilities**: an array of UIAbility or ExtensionAbility names.<br>**when**: **inuse** (when used) and **always** (always).|


```json
{
  "module" : {
    // ...
    "requestPermissions":[
      {
        "name" : "ohos.permission.PERMISSION1",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "FormAbility"
          ],
          "when":"inuse"
        }
      },
      {
        "name" : "ohos.permission.PERMISSION2",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "FormAbility"
          ],
          "when":"always"
        }
      }
    ]
  }
}
```


## Specifications for reason

The **reason** field (reason for requesting the permission) is mandatory when a user_grant permission is requested. You must declare each required permission in the application's configuration file.

On the dialog box displayed for the user to grant the permission, the [permission group](app-permission-mgmt-overview.md#permission-groups-and-permissions) is displayed. For details about the permission groups, see [Application Permission Groups](app-permission-group-list.md).

**How to Set**

1. Keep the sentence concise without redundant separators.

   **Recommended sentence pattern**: Used for something/Used to do something/Used for doing something.

   **Example**: Used for code scanning and photographing.

2. To ease multi-language adaptation, the recommended length of **reason** is fewer than 72 characters (36 Chinese characters displayed in two lines on the UI)  and the maximum length is 256 characters.

3. If **reason** is not set, the default reason will be used.

**How to Present**

The reason for requesting a permission is normally presented in an authorization window or a permission details page of an application in **Settings** > **Privacy** > **Permission manager**.

1. For a permission in the **Phone**, **Messaging**, **Calendar**, **Contacts**, and **Call logs** permission groups, the content and usage of the permissions must be presented to the user.
   
   **Sentence pattern**: Permissions A, used to/for ... Permission B, used to/for ...

   **Example**: Permission A, used to obtain the call status and mobile network information. Permission B, used for secure operation and statistics charging services.

2. For a permission in other permission groups, the reason for using the first requested permission in the permission group is presented to the user. The permissions are sorted according to the sequence of the permission array for each permission group under **Permission manager**.
   
   **Example**: If permission group A = {permission A, permission B, permission C} and {permission C, permission B} are requested, the reason for using permission B is presented to the user.
