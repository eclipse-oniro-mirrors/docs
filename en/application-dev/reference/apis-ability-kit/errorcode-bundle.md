# Bundle Error Codes

> **NOTE**
>
> This topic describes only module-specific error codes. For details about universal error codes, see [Universal Error Codes](../errorcode-universal.md).

## 17700001 Bundle Name Does Not Exist

**Error Message**

The specified bundle name is not found.

**Description**

When a query API is called, the bundle name passed in does not exist.

**Possible Causes**

1. The bundle name is misspelled.
2. The corresponding bundle is not installed.

**Solution**
1. Check whether the spelling of the bundle name is correct.
2. Check whether the corresponding bundle is installed.

## 17700002 Module Name Does Not Exist

**Error Message**

The specified module name is not found.

**Description**

When a query API or an installation-free API is called, the module name passed in does not exist.

**Possible Causes**
1. The module name is misspelled.
2. The module is not installed.

**Solution**
1. Check whether the spelling of the module name is correct.
2. Check whether the module is installed.

## 17700003 Ability Name Does Not Exist

**Error Message**

The specified ability name is not found.

**Description**

When a query API is called, the ability name passed in does not exist.

**Possible Causes**
1. The ability name is misspelled.
2. The application does not have the ability specified by **abilityName**.

**Solution**
1. Check whether the spelling of the ability name is correct.
2. Check whether the application has the ability specified by **abilityName**.

## 17700004 User ID Does Not Exist

**Error Message**

The specified user ID is not found.

**Description**

When a user-related API is called, the user ID passed in does not exist.

**Possible Causes**
1. Incorrect username.
2. The user does not exist in the system.

**Solution**
1. Check whether the user ID is correct.
2. Check whether the user exists.

## 17700005 appId Is an Empty String

**Error Message**

The specified app ID is an empty string.

**Description**

When an API of the **appControl** module is called, the application ID passed in does not exist.

**Possible Causes**

**appId** is an empty string.

**Solution**

Check whether **appId** is an empty string.

## 17700006 Permission Does Not Exist

**Error Message**

The specified permission is not found.

**Description**

When the **getPermissionDef** API of the **bundleManager** module is called, the permission passed in does not exist.

**Possible Causes**
1. The permission name is misspelled.
2. The permission does not exist.

**Solution**
1. Check whether the spelling of the permission name is correct.
2. Check whether the permission exists.

## 17700007 Incorrect Device ID

**Error Message**

The specified device ID is not found.

**Description**

When an API of the **distributedBundle** module is called, the device ID passed in does not exist.

**Possible Causes**
1. The device ID is incorrect.
2. The device ID does not exist.

**Solution**
1. Check whether the device ID is correct.
2. Check whether the device ID exists.

## 17700010 Bundle Installation Failure Due to File Parsing Failure

**Error Message**

Failed to install the HAP because the HAP fails to be parsed.

**Description**

When the **install** API of the **installer** module is called, the HAP passed in fails to be parsed.

**Possible Causes**
1. The HAP is not in ZIP format.
2. The profile in the HAP is not in JSON format.
3. Necessary fields are missing in the profile.

**Solution**
1. Check whether the HAP is in ZIP format.
2. Check whether the profile is in [JSON format](../../quick-start/application-configuration-file-overview-stage.md).
3. Check whether an error message is displayed when DevEco Studio compiles the HAP. If necessary fields are missing, an error message will be displayed.

## 17700011 Bundle Installation Failure Due to Signature Verification Failure

**Error Message**

Failed to install the HAP because the HAP signature fails to be verified.

**Description**

Calling the **install** API of the **installer** module to install the bundle fails due to signature verification failure.

**Possible Causes**

1. The HAP is not signed.
2. The source of the HAP signature information is unreliable.
3. The signature information of the HAP used for an upgrade is different from that of the installed HAP.
4. The signature information of multiple HAPs is inconsistent.

**Solution**
1. Check whether the HAP is signed.
2. Ensure that the signing certificate of the HAP is applied for from the application market.
3. Check whether the same certificate is used for signing multiple HAPs.
4. Check whether the certificate used for signing the upgrade HAP is the same as the certificate used for signing the installed HAP.

## 17700012 Bundle Installation Failure Due to Invalid File Path or Too Large File

**Error Message**

Failed to install the HAP because the HAP path is invalid or the HAP is too large.

**Description**

Calling the **install** API of the **installer** module to install the bundle fails because the HAP path is invalid or the HAP is too large.

**Possible Causes**
1. The path of the HAP does not exist.
2. The path of the HAP is inaccessible.
3. The size of the HAP exceeds the upper limit 4 GB.

**Solution**
1. Check whether the HAP path exists.
2. Check whether the HAP is read only or executable.
3. Check whether the size of the HAP exceeds 4 GB.

## 17700015 Bundle Installation Failure Due to Different Configuration Information of Multiple HAPs

**Error Message**

Failed to install the HAPs because they have different configuration information.

**Description**

Calling the **install** API of the **installer** module to install the bundle fails because the HAPs have different configuration information.

**Possible Causes**

The fields under **app** in the profiles of these HAPs are inconsistent.

**Solution**

Check whether the fields under **app** are the same.

## 17700016 Bundle Installation Failure Due to Insufficient System Disk Space

**Error Message**

Failed to install the HAP because of insufficient system disk space.

**Description**

Calling the **install** API of the **installer** module to install the bundle fails due to insufficient system disk space.

**Possible Causes**

The system disk space is insufficient.

**Solution**

Check whether the system has sufficient disk space.

## 17700017 Bundle Installation Failure Because the Version to Install is Too Earlier

**Error Message**

Failed to install the HAP since the version of the HAP to install is too early.

**Description**

Calling the **install** API of the **installer** module to install the bundle fails because the version to install is earlier than the version in use.

**Possible Causes**

The version number is earlier than the version in use.

**Solution**

Ensure that the version of the bundle to install is not earlier than the version in use.

## 17700018 Bundle Installation Failure Because the Dependent Module Does Not Exist

**Error Message**

Failed to install the HAP or HSP because the dependent module does not exist.

**Description**

The dependent module does not exist during the HAP or HPS installation.

**Possible Causes**

The dependent module is not installed.

**Solution**

Install the dependent modules first.

## 17700020 Failure to Uninstall Preinstalled Applications

**Error Message**

The preinstalled app cannot be uninstalled.

**Description**

Calling the **uninstall** API of the **installer** module to uninstall a preinstalled application fails.

**Possible Causes**

1. You might want to uninstall a non-preinstalled application but passed the bundle name of a preinstalled app.
2. The preinstalled application cannot be uninstalled.

**Solution**
1. Check whether the bundle name is correct.
2. Check whether the preinstalled application can be uninstalled.

## 17700021 Invalid UID

**Error Message**

The specified uid is invalid.

**Description**

When the **getBundleNameByUid** API of the **bundleManager** module is called, the UID passed in is invalid.

**Possible Causes**
1. The UID is misspelled.
2. The UID does not exist.

**Solution**
1. Check whether the UID is correct.
2. Check whether the UID exists.

## 17700022 Invalid Source File

**Error Message**

The input source file is invalid.

**Description**

When the **getBundleArchiveInfo** API of the **bundleManager** module is called, the HAP path passed in is invalid.

**Possible Causes**
1. The source file to be parsed does not exist.
2. The source file to be parsed is not in ZIP format.

**Solution**
1. Check whether the source file to be parsed exists.
2. Check whether the source file to be parsed is in ZIP format.

## 17700023 Default Application Does Not Exist

**Error Message**

The specified default app does not exist.

**Description**

When the **getDefaultApplication** API of the **defaultAppManager** module is called, the specified default application does not exist.

**Possible Causes**

No default application is set for the device.

**Solution**

Check whether the default application is set on the device.

## 17700024 Profile Does Not Exist

**Error Message**

Failed to get the profile because the specified profile is not found in the HAP.

**Description**

When an API for querying the profile is called, the profile does not exist.

**Possible Causes**

1. The metadata name passed in the API does not exist in the profile.
2. The content of the profile is not in JSON format.
3. The type of the profile to query does not exist.

**Solution**
1. Check whether the metadata name in the **ability** or **extensionAbility** to be queried exists.
2. Check whether the content of the profile to be queried is in JSON format.
3. Check whether the application contains a profile that matches the value of **profileType** passed in.

## 17700025 Invalid Type

**Error Message**

The specified type is invalid.

**Description**

When an API of the **defaultAppManager** module is called, the type passed in is invalid.

**Possible Causes**
1. The type passed in the API is misspelled.
2. The type passed in the API does not exist.

**Solution**
1. Check whether the spelling of type is correct.
2. Enter a type that exists.

## 17700026 Bundle Disabled

**Error Message**

The specified bundle is disabled.

**Description**

When an API for querying bundle information is called, the specified bundle is disabled.

**Possible Causes**

The bundle on the device has been disabled and cannot be queried.

**Solution**

Check whether the bundle on the device is disabled.

## 17700027 Distributed Service Is Not Started

**Error Message**

The distributed service is not running.

**Description**

When an API of the **distributedBundle** module is called, the distributed service is not started.

**Possible Causes**

The device is not networked.

**Solution**

Check whether the device is networked.

## 17700028 Mismatch Between Ability and Type

**Error Message**

The ability does not match the type.

**Description**

When the **setDefaultApplication** API of the **defaultAppManager** module is called, the **ability** and **type** passed in do not match.

**Possible Causes**

The ability and type are misspelled.

**Solution**

Check whether the spellings of ability and type are correct.

## 17700029 Disabled Ability

**Error Message**

The specified ability is disabled.

**Description**

When an API for querying ability information is called, the specified ability is disabled.

**Possible Causes**

The specified ability is disabled.

**Solution**

Check whether the ability is disabled. You can use [Bundle Manager](../../tools/bm-tool.md) to query the information.

## 17700030 Failure in Clearing Cache Files

**Error Message**

The specified bundle does not support clearing of cache files.

**Description**

When the **cleanBundleCacheFiles** API of the **bundleManager** module is called, the specified bundle does not support cache file clearing.

**Possible Causes**

The application is a system application and the **AllowAppDataNotCleared** field is configured in the signing certificate.

**Solution**
1. Check whether the application is a system application. You can use [Bundle Manager](../../tools/bm-tool.md) to query the application information and check whether the value of **isSystemApp** is **true**.
2. Check whether the **AllowAppDataNotCleared** field is configured for the application. You can use [Bundle Manager](../../tools/bm-tool.md) to query the application information and check whether the value of **userDataClearable** is **true**.

## 17700031 HAP Installation Fails Due to Overlay Feature Verification Failure

**Error Message**

Failed to install the HAP because the overlay check of the HAP failed.

**Description**

The target application and the to-be-installed application with the overlay feature are not preset applications, or the target application or target module is one with the overlay feature.

**Possible Causes**
1. To use the overlay feature between applications, the following conditions must be met:<br>The application with the overlay feature must be a preset application.
2. The target application must be a preset application.
3. The target application cannot be an application with the overlay feature.
4. The target module cannot be a module with the overlay feature.

**Solution**
1. Ensure that the application with the overlay feature is a preset application.
2. Ensure that the target application is a preset application.
3. Ensure that the target application is not an application with the overlay feature.
4. Ensure that the target module is not a module with the overlay feature.

## 17700032 Application Does Not Contain a Module with the Overlay Feature

**Error Message**

The specified bundle does not contain any overlay module.

**Description**

An API is called to obtain the **overlayModuleInfo** object of another application, but that application does not contain a module with the overlay feature.

**Possible Causes**

The specified application does not contain a module with the overlay feature.

**Solution**

Check whether the application contains a module with the overlay feature.

## 17700033 Module Is Not Configured with the Overlay Feature

**Error Message**

The specified module is not an overlay module.

**Description**

An API is called to obtain the **overlayModuleInfo** object of a module, but the module is not configured with the overlay feature.

**Possible Causes**

The specified module is not a module with the overlay feature.

**Solution**

Check whether the module is configured with the overlay feature.

## 17700034 Module Is Configured with the Overlay Feature

**Error Message**

The specified module is an overlay module.

**Description**

An API is called to obtain the **overlayModuleInfo** object based on the target module name, but that module is configured with the overlay feature.

**Possible Causes**

The specified module is configured with the overlay feature.

**Solution**

Check whether the specified module is configured with the overlay feature.

## 17700035 Application Contains Only Modules with the Overlay Feature

**Error Message**

The specified bundle is an overlay bundle.

**Description**

An API is called to obtain the **overlayModuleInfo** object based on the target module name of another application, but that application contains only modules with the overlay feature.

**Possible Causes**

The specified application contains only modules with the overlay feature.

**Solution**

Check whether the application contains only modules with the overlay feature.

## 17700036 Failure in Installing the Shared Library Because of No AllowAppShareLibrary Privilege

**Error Message**

Failed to install the HSP due to the lack of required permission.

**Description**

The shared library is not configured with the **AllowAppShareLibrary** privilege, resulting in security and privacy risks. As a result, the installation fails.

**Possible Causes**

The shared library does not request the **AllowAppShareLibrary** privilege before being released.

**Solution**

Configure the **AllowAppShareLibrary** privilege for the shared library, re-sign the library, and release it.

## 17700037 Failure in Uninstalling the Shared Library Due to Dependency

**Error Message**

The version of the shared bundle is dependent on other applications.

**Description**

Other applications depend on the shared library, causing the uninstall to fail.

**Possible Causes**
1. The version specified during the uninstall is the latest version of the shared library, and the shared library is depended on by other applications.
2. No version is not specified during the uninstall, meaning that all versions of the shared library will be uninstalled, and the shared library is depended on by other applications.

**Solution**
1. Check whether the shared library to uninstall is depended on by other applications.
2. Check whether the version of the shared library to uninstall is the latest version of the shared library.

## 17700038 Shared Library to Uninstall Does Not Exist

**Error Message**

The specified shared bundle does not exist.

**Description**

The shared library to uninstall does not exist.

**Possible Causes**
1. The version specified during the uninstall is different from the version of the shared library installed.
2. The shared library to uninstall is not installed.

**Solution**
1. Check whether the shared library exists.
2. Check whether the version of the shared library is the same as that installed.

## 17700039 Failure in Installing an Inter-Application Shared Library

**Error Message**

Failed to install the HSP because disallow install a shared bundle by hapFilePaths.

**Description**

During application installation, the installation package passed in is of the inter-application shared library type.

**Possible Causes**
1. When [Bundle Manager](../../tools/bm-tool.md) is used to install an application, the **-p** parameter is set to the installation package path of an inter-application shared library.
2. When the **install** API is called to install an application, the **hapFilePaths** parameter is set to the installation package path of an inter-application shared library.

**Solution**
1. Use the **-s** parameter to specify the installation package path of an inter-application shared library.
2. Use the **sharedBundleDirPaths** parameter in **installParam** to specify the installation package path of an inter-application shared library.

## 17700040 Failure in Uninstalling an Inter-Application Shared Library

**Error Message**

The specified bundle is a shared bundle which cannot be uninstalled.

**Description**

During application uninstall, the bundle name of an inter-application shared library is passed in.

**Possible Causes**
1. When [Bundle Manager](../../tools/bm-tool.md) is used to uninstall an application, the **-n** parameter is set to the bundle name of an inter-application shared library.
2. When the **install** API is called to uninstall an application, the **bundleName** parameter is set to the bundle name of an inter-application shared library.

**Solution**
1. Use the **-s** parameter to specify the application to be uninstalled as a shared library application.
2. Use the **bundleName** and **versionCode** parameters in **UninstallParam** to specify the bundle name and version of the shared library to be uninstalled.

## 17700041 Application Installation Is Not Allowed by Enterprise Device Management

**Error Message**

Failed to install the HAP because enterprise device management disallow install.

**Description**

The installation of this application is prohibited by enterprise device management.

**Possible Causes**

The enterprise device management does not allow the installation of this application.

**Solution**

Check whether the application installation is prohibited by the enterprise device management.

## 17700042 Incorrect URI in the Data Proxy

**Error Message**

Failed to install the HAP because of incorrect URI in the data proxy.

**Description**

During application installation, the URI of the data proxy is incorrectly configured.

**Possible Causes**

1. The bundle name in the URI is different from that of the current application.
2. The URI is duplicate.

**Solution**

1. Change the bundle name in the URI to that of the current application.
2. Change duplicate URIs. Ensure that the URI of each data proxy is unique.

## 17700043 Incorrect Permission Configuration in the Data Proxy

**Error Message**

Failed to install the HAP because of low APL in the non-system data proxy (required APL: system_basic or system_core).

**Description**

During application installation, the permission level of the data proxy of a non-system application is too low. The permission level should be **system_basic** or **system_core**.

**Possible Causes**

1. No permission is configured for the data proxy of a non-system application.
2. The permission level of the data proxy of a non-system application is too low.

**Solution**

1. Configure the read and write permissions in the data proxy.
2. Change the read and write permissions in the data proxy and ensure that the permission level is **system_basic** or **system_core**.

## 17700044 Field isolationMode in the HAP Conflicts with the Device Isolation Mode

**Error Message**

Failed to install the HAP because the isolationMode configured is not supported.

**Description**

During application installation, the value of **isolationMode** in the HAP conflicts with the isolation mode of the device.

**Possible Causes**
1. The device supports the isolation mode (the value of **persist.bms.supportIsolationMode** is **true**), whereas the value of **isolationMode** in the HAP is **nonisolationOnly**.
2. The device does not support the isolation mode (the value of **persist.bms.supportIsolationMode** is **false**), whereas the value of **isolationMode** in the HAP is **isolationOnly**.

**Solution**

Set the **isolationMode** field in the HAP based on the isolation mode of the device.

## 17700045 Application Uninstall Is Not Allowed by Enterprise Device Management

**Error Message**

Failed to uninstall the HAP because enterprise device management disallow uninstall.

**Description**

The uninstall of this application is prohibited by enterprise device management.

**Possible Causes**

The enterprise device management does not allow the uninstall of this application.

**Solution**

Check whether the application uninstall is prohibited by the enterprise device management.

## 17700047 Application Version To Be Updated Is Not Later Than the Current Version

**Error Message**

Failed to install the HAP because the VersionCode to be updated is not greater than the current VersionCode.

**Description**

The version of the application to be updated is not later than the current version.

**Possible Causes**

1. The version number of the application to be updated is earlier than or equal to that of the current version number.
2. When **installFlag** is set to **NORMAL**, the version number of the application to be updated must be later than the installed version number.

**Solution**

1. Set the version number of the application to be later than the current version number.
2. If you want to update the application without changing the version number, set **installFlag** to **REPLACE_EXISTING**.

## 17700048 Code Signature Verification Failure
**Error Message**

Failed to install the HAP because the code signature verification failed.

**Description**

During application installation, the code signature file of the installation package fails to be verified.

**Possible Causes**

1. The module corresponding to the code signature file does not exist in the installation package.
2. The path of the code signature file is invalid.
3. The code signature file does not match the installation package.

**Solution**

1. Ensure that the module corresponding to the code signature file is contained in the installation package.
2. Provide a valid path of the code signature file.
3. Use the code signature file that matches the installation package.

## 17700049 Update Failure Because of Incorrect Bundle Name

**Error Message**

Failed to install the HAP because the bundleName is different from the bundleName of the caller application.

**Description**

During the update of an enterprise MDM application, the bundleName passed in is different from that of the caller.

**Possible Causes**

The HAP or HSP to be installed does not belong to the current application.

**Solution**

Ensure that the HAP or HSP to be installed belongs to the current application.

## 17700050 Enterprise Device Verification Failure

**Error Message**

Failed to install the HAP because an enterprise normal/MDM bundle cannot be installed on non-enterprise device.

**Description**

Users try to install an enterprise Normal or MDM application on a non-enterprise device.

**Possible Causes**

The device is not an enterprise device.

**Solution**

1. Use an enterprise device.

2. Ensure that **const.bms.allowenterprisebundle** is set to **true**.

## 17700051 Update Failure Because of Incorrect Bundle Name

**Error Message**

Failed to install the HAP because the distribution type of the caller application is not enterprise_mdm.

**Description**

During the update of an enterprise MDM application, the distribution type of the caller is not enterprise MDM.

**Possible Causes**

The distribution type of the caller is not enterprise MDM.

**Solution**

Ensure that the signature file of the application is correctly configured.

## 17700052 Installation of Debugging Applications Allowed Only in Developer Mode

**Error Message**

Failed to install the HAP because a debug bundle can be installed only in developer mode.

**Description**

A debugging application can be installed only in the developer mode.

**Possible Causes**

The application is a debugging application, but the device is not in developer mode.

**Solution**

Run the **hdc shell param get const.security.developermode.state** command. If **false** is returned, a debugging application cannot be installed on the device.

## 17700053 Not Invoked by AppGallery

**Error Message**

The caller is not AppGallery.

**Description**

This API is called by AppGallery.

**Possible Causes**

The caller is not AppGallery.

**Solution**

Use AppGallery to call the API.

## 17700054 Bundle Installation Failure Due to Permission Verification Failure

**Error Message**

Failed to install the HAP because the HAP requests wrong permissions.

**Description**

The application has applied for an incorrect permission, causing the installation to fail.

**Possible Causes**

1. The application is not an MDM application and has applied for the MDM permission.
2. The ability privilege level (APL) of the application is lower than the level of the permission that the application has applied for.

**Solution**

1. Check whether the application has applied for the [MDM permission](../../security/AccessToken/permissions-for-mdm-apps.md), which is available only for MDM applications.
2. Check whether the requested permission is open. For details, see [Permission List](../../security/AccessToken/permissions-for-all.md).

## 17700201 .abc File Verification Failure

**Error Message**

Failed to verify the abc file.

**Description**

Failed to verify the .abc file.

**Possible Causes**

The .abc file is untrusted.

**Solution**

Pass in the path of a trusted .abc file.

## 17700202 .abc File Deletion Failure

**Error Message**

Failed to delete the abc file.

**Description**

Failed to delete the .abc file.

**Possible Causes**

The .abc file does not exist.

**Solution**

Pass in a valid path of the .abc file.

