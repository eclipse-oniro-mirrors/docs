# Full SDK Compilation

The full SDK provides a full set of APIs available in OpenHarmony, including system APIs required by system applications. Vendors can leverage this SDK to develop applications.

Since OpenHarmony 3.2 Beta5, the full SDK is not provided with the version. If necessary, you can compile the SDK using the full source code.

## Compiling the Full SDK

**Preparation**

1. Register an SSH public key for access to Gitee.
2. Configure the server environment. For details, see [Setting Up the Ubuntu Environment](../../device-dev/quick-start/quickstart-ide-env-ubuntu.md).

**Procedure**

1. Download and initialize the manifest repository: **repo init -u https://gitee.com/openharmony/manifest.git -b $manifest_branch --no-repo-verify --repo-url=https://gitee.com/oschina/repo --no-clone-bundle**

2. Download source code based on the downloaded manifest repository: **repo sync -c -d --force-sync**

3. Perform precompilation: **yes y | apt install libxinerama-dev libxcursor-dev libxrandr-dev libxi-dev && rm -rf prebuilts/clang/ohos/darwin-x86_64/clang-480513 && rm -rf prebuilts/clang/ohos/windows-x86_64/clang-480513 && rm -rf prebuilts/clang/ohos/linux-x86_64/clang-480513 && bash build/prebuilts_download.sh -ndk && apt-get update -qqy && apt-get install doxygen -y --force-yes**

4. Perform compilation: **./build.sh --product-name ohos-sdk**


If the compilation is successful, export the files in the **out/sdk/packages/ohos-sdk/** directory.

## Replacing the SDK

After the full SDK is compiled, switch to it in DevEco Studio. For details, see [Guide to Switching to Full SDK](full-sdk-switch-guide.md).
