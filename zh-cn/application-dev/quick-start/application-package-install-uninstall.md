# 应用程序包安装卸载与更新

本章节简要介绍应用程序包的安装卸载流程、以及应用程序包的两种更新方式。

## 应用程序包的安装卸载
开发者可以通过调试命令进行应用的安装和卸载，可参考[编译发布与上架部署流程图](./application-package-structure-stage.md#发布态包结构)。

**图1** 应用程序包安装和卸载流程（开发者）

![hap-intall-uninstall](figures/hap-install-uninstall-developer.png)


开发者将应用上架应用市场后，终端设备用户可以在终端设备上使用应用市场进行应用的安装和卸载。

**图2** 应用程序包安装和卸载流程（终端设备用户）

![hap-intall-uninstall](figures/hap-install-uninstall-user.png)

## 应用程序包的更新


对于开发者，应用程序包的更新，首先需要更新[app.json5配置文件](./app-configuration-file.md#appjson5配置文件)中的versionCode版本号字段，通过IDE打包后在应用市场发布，发布流程与首次发布一致。对于终端设备用户，可以通过以下两种方式更新应用程序包：

- [应用市场内更新](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V14/store-update-V14?catalogVersion=V14)：新版本应用通过应用市场上架后，应用市场通知终端用户该应用有新版本，终端用户可以根据通知到应用市场（客户端）进行应用升级。
- [应用内检测升级](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/appgallerykit-app-update-0000001055118286)：终端用户启动应用时，应用市场检测到该应用有新版本会通知终端用户，可以到应用市场进行应用的下载更新。
