# 常见问题


## 如何将用户的堆内存挂载进内核

内核堆内存配置的相关宏如下，用户可根据实际情况，在target_config.h中配置：

  **表1** 内核堆内存配置相关宏

  | 宏名称 | 描述 | 
  | -------- | -------- |
  | LOSCFG_SYS_EXTERNAL_HEAP | 这个宏决定系统是使用内核的内部堆内存还是用户的堆内存，默认为0（即使用内部的堆内存），大小为0x10000；如果用户需要基于外部的堆内存，那么可以将该宏设置为1。 | 
  | LOSCFG_SYS_HEAP_ADDR | 内核堆内存的起始地址。 | 
  | LOSCFG_SYS_HEAP_SIZE | 内核堆内存的大小，即LOSCFG_SYS_HEAP_ADDR指定的内存块大小。 | 


> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 指定的堆内存范围务必保证没有其他模块使用，避免踩内存，破坏堆内存功能。
