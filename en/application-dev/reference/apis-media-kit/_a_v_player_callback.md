# AVPlayerCallback


## Overview

The AVPlayerCallback struct contains the set of the **OH_AVPlayerOnInfo** and **OH_AVPlayerOnInfo** callback function pointers. To ensure the normal running of **OH_AVPlayer**, you must register the instance of this struct with the **OH_AVPlayer** instance and process the information reported by the callback functions.

**System capability**: SystemCapability.Multimedia.Media.AVPlayer

**Since**: 11

**Deprecated from**: 12

**Substitute**: [OH_AVPlayerOnInfoCallback](_a_v_player.md#oh_avplayeroninfocallback) and [OH_AVPlayerOnErrorCallback](_a_v_player.md#oh_avplayeronerrorcallback)

**Related module**: [AVPlayer](_a_v_player.md)


## Summary


### Member Variables

| Name| Description| 
| -------- | -------- |
| [onInfo](_a_v_player.md#oninfo) | AVPlayer process information. For details, see [OH_AVPlayerOnInfo](_a_v_player.md#oh_avplayeroninfo).| 
| [onError](_a_v_player.md#onerror) | AVPlayer error information. For details, see [OH_AVPlayerOnError](_a_v_player.md#oh_avplayeronerror).| 
