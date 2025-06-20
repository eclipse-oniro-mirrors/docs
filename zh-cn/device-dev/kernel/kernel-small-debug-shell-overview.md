# Shell介绍


OpenHarmony内核提供的Shell支持调试常用的基本功能，包含系统、文件、网络和动态加载相关命令。同时OpenHarmony内核的Shell支持添加新的命令，可以根据需求来进行定制。


- 系统相关命令：提供查询系统任务、内核信号量、系统软件定时器、CPU占用率、当前中断等相关信息的能力。

- 文件相关命令：支持基本的ls、cd等功能。

- 网络相关命令：支持查询接到开发板的其他设备的IP、查询本机IP、测试网络连接、设置开发板的AP和station模式等相关功能。

  新增命令的详细流程可参见[Shell命令开发指导](../kernel/kernel-small-debug-shell-guide.md)和[Shell命令编程实例](../kernel/kernel-small-debug-shell-build.md)。


 **注意事项** 

在使用Shell功能的过程中，需要注意以下几点：

- Shell功能支持使用exec命令来运行可执行文件。

- Shell功能支持默认模式下英文输入。如果出现用户在UTF-8格式下输入了中文字符的情况，只能通过回退三次来删除。

- Shell功能支持shell命令、文件名及目录名的Tab键联想补全。若有多个匹配项，则根据共同字符， 打印多个匹配项。对于过多的匹配项（打印多于24行），将会进行打印询问（Display all num  possibilities?（y/n）），用户可输入y选择全部打印，或输入n退出打印，选择全部打印并打印超过24行后，会进行--More--提示，此时按回车键继续打印，按q键退出（支持Ctrl+c退出)。

- Shell端工作目录与系统工作目录是分开的，即通过Shell端cd、pwd等命令是对Shell端工作目录进行操作，通过chdir、getcwd等命令是对系统工作目录进行操作，两个工作目录相互之间没有联系。当文件系统操作命令入参是相对路径时要格外注意。

- 在使用网络Shell指令前，需要先调用tcpip_init函数完成网络初始化并完成telnet连接后才能起作用，内核默认不初始化tcpip_init。

- 不建议使用Shell命令对/dev目录下的设备文件进行操作，这可能会引起不可预知的结果。

- Shell功能不符合POSIX标准，仅供调试使用。
  > ![icon-notice.gif](public_sys-resources/icon-notice.gif) **须知：**
  > Shell功能仅供调试使用，在Debug版本中开启（使用时通过menuconfig在配置项中开启"LOSCFG_DEBUG_VERSION"编译开关进行相关控制），商用产品中禁止包含该功能。
