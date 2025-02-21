# Using OpenSL ES for Audio Recording

OpenSL ES, short for Open Sound Library for Embedded Systems, is an embedded, cross-platform audio processing library that is free of charge. It provides high-performance and low-latency APIs for you to develop applications running on embedded mobile multimedia devices. OpenHarmony have implemented certain native APIs based on [OpenSL ES](https://www.khronos.org/opensles/) 1.0.1 API specifications developed by the [Khronos Group](https://www.khronos.org/). You can use these APIs through <OpenSLES.h\> and <OpenSLES_OpenHarmony.h\>.

## OpenSL ES on OpenHarmony

Currently, OpenHarmony implements parts of [OpenSL ES APIs](https://gitee.com/openharmony/third_party_opensles/blob/master/api/1.0.1/OpenSLES.h) to implement basic audio recording functionalities.

If an API that has not been implemented on OpenHarmony is called, **SL_RESULT_FEATURE_UNSUPPORTED** is returned.

The following lists the OpenSL ES APIs that have been implemented on OpenHarmony. For details, see the [OpenSL ES](https://www.khronos.org/opensles/) specifications.

- **Engine APIs implemented on OpenHarmony**
  - SLresult (\*CreateAudioPlayer) (SLEngineItf self, SLObjectItf \* pPlayer, SLDataSource \*pAudioSrc, SLDataSink \*pAudioSnk, SLuint32 numInterfaces, const SLInterfaceID \* pInterfaceIds, const SLboolean \* pInterfaceRequired)
  - SLresult (\*CreateAudioRecorder) (SLEngineItf self, SLObjectItf \* pRecorder, SLDataSource \*pAudioSrc, SLDataSink \*pAudioSnk, SLuint32 numInterfaces, const SLInterfaceID \* pInterfaceIds, const SLboolean \* pInterfaceRequired)
  - SLresult (\*CreateOutputMix) (SLEngineItf self, SLObjectItf \* pMix, SLuint32 numInterfaces, const SLInterfaceID \* pInterfaceIds, const SLboolean \* pInterfaceRequired)

- **Object APIs implemented on OpenHarmony**
  - SLresult (\*Realize) (SLObjectItf self, SLboolean async)
  - SLresult (\*GetState) (SLObjectItf self, SLuint32 \* pState)
  - SLresult (\*GetInterface) (SLObjectItf self, const SLInterfaceID iid, void \* pInterface)
  - void (\*Destroy) (SLObjectItf self)

- **Recorder APIs implemented on OpenHarmony**
  - SLresult (\*SetRecordState) (SLRecordItf self, SLuint32 state)
  - SLresult (\*GetRecordState) (SLRecordItf self,SLuint32 \*pState)

- **BufferQueue APIs implemented on OpenHarmony**
  
  The APIs listed below can be used only after <OpenSLES_OpenHarmony.h\> is introduced.
  | API| Description| 
  | -------- | -------- |
  | SLresult (\*Enqueue) (SLOHBufferQueueItf self, const void \*buffer, SLuint32 size) | Adds a buffer to the corresponding queue.<br>For an audio playback operation, this API adds the buffer with audio data to the **filledBufferQ_** queue. For an audio recording operation, this API adds the idle buffer after recording data storage to the **freeBufferQ_** queue.<br>The **self** parameter indicates the **BufferQueue** object that calls this API.<br>The **buffer** parameter indicates the pointer to the buffer with audio data or the pointer to the idle buffer after the recording data is stored.<br>The **size** parameter indicates the size of the buffer.| 
  | SLresult (\*Clear) (SLOHBufferQueueItf self) | Releases a **BufferQueue** object.<br>The **self** parameter indicates the **BufferQueue** object that calls this API.| 
  | SLresult (\*GetState) (SLOHBufferQueueItf self, SLOHBufferQueueState \*state) | Obtains the state of a **BufferQueue** object.<br>The **self** parameter indicates the **BufferQueue** object that calls this API.<br>The **state** parameter indicates the pointer to the state of the **BufferQueue** object.| 
  | SLresult (\*RegisterCallback) (SLOHBufferQueueItf self, SlOHBufferQueueCallback callback, void\* pContext) | Registers a callback.<br>The **self** parameter indicates the **BufferQueue** object that calls this API.<br>The **callback** parameter indicates the callback to be registered for the audio playback or recording operation.<br>The **pContext** parameter indicates the pointer to the audio file to be played for an audio playback operation or the pointer to the audio file to be recorded for an audio recording operation.| 
  | SLresult (\*GetBuffer) (SLOHBufferQueueItf self, SLuint8\*\* buffer, SLuint32\* size) | Obtains a buffer.<br>For an audio playback operation, this API obtains an idle buffer from the **freeBufferQ_** queue. For an audio recording operation, this API obtains the buffer that carries recording data from the **filledBufferQ_** queue.<br>The **self** parameter indicates the **BufferQueue** object that calls this API.<br>The **buffer** parameter indicates the double pointer to the idle buffer or the buffer carrying recording data.<br>The **size** parameter indicates the size of the buffer.| 

## Sample Code

Refer to the sample code below to record an audio file.

1. Add the header files.
     
   ```c++
   #include <OpenSLES.h>
   #include <OpenSLES_OpenHarmony.h>
   #include <OpenSLES_Platform.h>
   ```

2. Use the **slCreateEngine** API to create and instantiate an **engine** object.
     
   ```c++
   SLObjectItf engineObject = nullptr;
   slCreateEngine(&engineObject, 0, nullptr, 0, nullptr, nullptr);
   (*engineObject)->Realize(engineObject, SL_BOOLEAN_FALSE);
   ```

3. Obtain the **engineEngine** instance of the **SL_IID_ENGINE** API.
     
   ```c++
   SLEngineItf engineItf = nullptr;
   (*engineObject)->GetInterface(engineObject, SL_IID_ENGINE, &engineItf);
   ```

4. Configure the recorder information (including the input source **audiosource** and output source **audiosink**), and create a **pcmCapturerObject** instance.
     
   ```c++
   SLDataLocator_IODevice io_device = {
       SL_DATALOCATOR_IODEVICE,
       SL_IODEVICE_AUDIOINPUT,
       SL_DEFAULTDEVICEID_AUDIOINPUT,
       NULL
   };
   SLDataSource audioSource = {
       &io_device,
       NULL
   };
   SLDataLocator_BufferQueue buffer_queue = {
       SL_DATALOCATOR_BUFFERQUEUE,
       3
   };
   // Configure the parameters based on the audio file format.
   SLDataFormat_PCM format_pcm = {
       SL_DATAFORMAT_PCM,           // Input audio format.
       1,                                              // Mono channel.
       SL_SAMPLINGRATE_44_1,        // Sampling rate, 44100 Hz.
       SL_PCMSAMPLEFORMAT_FIXED_16, // Audio sampling format, a signed 16-bit integer in little-endian format.
       0,
       0,
       0
   };
   SLDataSink audioSink = {
       &buffer_queue,
       &format_pcm
   };
   
   SLObjectItf pcmCapturerObject = nullptr;
   (*engineItf)->CreateAudioRecorder(engineItf, &pcmCapturerObject,
       &audioSource, &audioSink, 0, nullptr, nullptr);
   (*pcmCapturerObject)->Realize(pcmCapturerObject, SL_BOOLEAN_FALSE);
   
   ```

5. Obtain the **recordItf** instance of the **SL_IID_RECORD** API.
     
   ```c++
   SLRecordItf  recordItf;
   (*pcmCapturerObject)->GetInterface(pcmCapturerObject, SL_IID_RECORD, &recordItf);
   ```

6. Obtain the **bufferQueueItf** instance of the **SL_IID_OH_BUFFERQUEUE** API.
     
   ```c++
   SLOHBufferQueueItf bufferQueueItf;
   (*pcmCapturerObject)->GetInterface(pcmCapturerObject, SL_IID_OH_BUFFERQUEUE, &bufferQueueItf);
   ```

7. Register the **BufferQueueCallback** function.
     
   ```c++
   static void BufferQueueCallback(SLOHBufferQueueItf bufferQueueItf, void *pContext, SLuint32 size)
   {
       // Obtain the user information passed in during the registration from pContext.
       SLuint8 *buffer = nullptr;
       SLuint32 pSize = 0;
       (*bufferQueueItf)->GetBuffer(bufferQueueItf, &buffer, &pSize);
       if (buffer != nullptr) {
           // The recording data can be read from the buffer for subsequent processing.
           (*bufferQueueItf)->Enqueue(bufferQueueItf, buffer, size);
       }
   }
   void *pContext; // This callback can be used to obtain the custom context information passed in.
   (*bufferQueueItf)->RegisterCallback(bufferQueueItf, BufferQueueCallback, pContext);
   ```

8. Start audio recording.
     
   ```c++
   (*recordItf)->SetRecordState(recordItf, SL_RECORDSTATE_RECORDING);
   ```

9. Stop audio recording.
     
   ```c++
   (*recordItf)->SetRecordState(recordItf, SL_RECORDSTATE_STOPPED);
   (*pcmCapturerObject)->Destroy(pcmCapturerObject);
   ```
