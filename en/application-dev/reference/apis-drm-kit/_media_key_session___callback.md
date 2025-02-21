# MediaKeySession_Callback


## Overview

The MediaKeySession_Callback struct describes the callback used to listen for events such as media key expiry or change, without returning media key session instances. It applies to the scenario where a single media key session needs to be decrypted.

**Since**: 11

**Related module**: [Drm](_drm.md)


## Summary


### Member Variables

| Name| Description| 
| -------- | -------- |
| [MediaKeySession_EventCallback](_drm.md#mediakeysession_eventcallback) [eventCallback](_drm.md#eventcallback) | Event callback, for example, a media key expiry event.| 
| [MediaKeySession_KeyChangeCallback](_drm.md#mediakeysession_keychangecallback) [keyChangeCallback](_drm.md#keychangecallback) | Callback of the media key change event.| 
