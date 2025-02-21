# OpenSL ES Interfaces Supported by Native APIs

## Introduction

Open Sound Library for Embedded Systems (OpenSL ES) is a set of audio acceleration standards for embedded systems. It provides objects and APIs for developers to implement high-performance, low-latency audio features. OpenHarmony implements some native APIs based on [OpenSL ES](https://www.khronos.org/opensles/) 1.0.1 API specifications. The following table lists the related APIs.

## Supported APIs

|Object               |External Interface              |Interface Invocation                                                                          |Supported  |Description                 |
| ------------------ | -------------------- | -------------------------------------------------------------------------------------|----------| -------------------- |
|SLEngineItf         |CreateAudioPlayer     |CreateAudioPlayer(SLEngineItf self, SLObjectItf *pPlayer, SLDataSource *pAudioSrc, SLDataSink *pAudioSnk, SLuint32 numInterfaces, const SLInterfaceID *pInterfaceIds, const SLboolean *pInterfaceRequired) |Yes       |Creates an audio player.       |
|SLEngineItf         |CreateAudioRecorder   |reateAudioRecorder(SLEngineItf self, SLObjectItf *pRecorder, SLDataSource *pAudioSrc, SLDataSink *pAudioSnk, SLuint32 numInterfaces, const SLInterfaceID *pInterfaceIds, const SLboolean *pInterfaceRequired)|Yes       |Creates an audio recorder.       |
|SLEngineItf         |CreateAudioOutputMix  |CreateOutputMix(SLEngineItf self, SLObjectItf *pMix, SLuint32 numInterfaces, const SLInterfaceID *pInterfaceIds, const SLboolean *pInterfaceRequired)|Yes       |Creates an audio output mixer.           |
|SLObjectItf         |Realize               |Realize(SLObjectItf self, SLboolean async)                                            |Yes       |Realizes an audio player.       |
|SLObjectItf         |getState              |GetState(SLObjectItf self, SLuint32 *state)                                           |Yes       |Obtains the state.            |
|SLObjectItf         |getInterface          |GetInterface(SLObjectItf self, const SLInterfaceID iid, void *interface)              |Yes       |Obtains the interface.            |
|SLObjectItf         |Destroy               |Destroy(SLObjectItf self)                                                             |Yes       |Destroys an object.            |
|SLOHBufferQueueItf  |Enqueue               |Enqueue(SLOHBufferQueueItf self, const void *buffer, SLuint32 size)                   |Yes       |Adds a buffer to the queue.|
|SLOHBufferQueueItf  |clear                 |Clear(SLOHBufferQueueItf self)                                                        |Yes       |Releases the buffer queue.        |
|SLOHBufferQueueItf  |getState              |GetState(SLOHBufferQueueItf self, SLOHBufferQueueState *state)                        |Yes       |Obtains the BufferQueue status. |
|SLOHBufferQueueItf  |getBuffer             |GetBuffer(SLOHBufferQueueItf self, SLuint8 **buffer, SLuint32 *size)                  |Yes       |Obtains a buffer.          |
|SLOHBufferQueueItf  |RegisterCallback      |RegisterCallback(SLOHBufferQueueItf self, SlOHBufferQueueCallback callback, void *pContext) |Yes |Registers a callback.         |
|SLPlayItf           |SetPlayState          |SetPlayState(SLPlayItf self, SLuint32 state)                                          |Yes       |Sets the playback state.         |
|SLPlayItf           |GetPlayState          |GetPlayState(SLPlayItf self, SLuint32 *state)                                         |Yes       |Obtains the playback state.         |
|SLRecordItf         |SetRecordState        |SetRecordState(SLRecordItf self, SLuint32 state)                                      |Yes       |Sets the recording state.         |
|SLRecordItf         |GetRecordState        |GetRecordState(SLRecordItf self, SLuint32 *pState)                                    |Yes       |Obtains the recording state.         |
|SLVolumeItf         |SetVolumeLevel        |SetVolumeLevel(SLVolumeItf self, SLmillibel *level)                                   |Yes       |Sets the volume.             |
|SLVolumeItf         |GetVolumeLevel        |GetVolumeLevel(SLVolumeItf self, SLmillibel level)                                    |Yes       |Obtains the volume.             |
|SLVolumeItf         |GetMaxVolumeLevel     |GetMaxVolumeLevel(SLVolumeItf self, SLmillibel *maxLevel)                             |Yes       |Obtains the maximum volume.         |
