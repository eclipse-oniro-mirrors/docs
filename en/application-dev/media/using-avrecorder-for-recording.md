# Using AVRecorder for Audio Recording

You will learn how to use the AVRecorder to develop audio recording functionalities including starting, pausing, resuming, and stopping recording.

During application development, you can use the **state** attribute of the AVRecorder to obtain the AVRecorder state or call **on('stateChange')** to listen for state changes. Your code must meet the state machine requirements. For example, **pause()** is called only when the AVRecorder is in the **started** state, and **resume()** is called only when it is in the **paused** state.

**Figure 1** Recording state transition 

![Recording state change](figures/recording-status-change.png)

For details about the state, see [AVRecorderState](../reference/apis/js-apis-media.md#avrecorderstate9).


## How to Develop

Read [AVRecorder](../reference/apis/js-apis-media.md#avrecorder9) for the API reference.

1. Create an **AVRecorder** instance. The AVRecorder is the **idle** state.
     
   ```ts
   import media from '@ohos.multimedia.media';
   
   let avRecorder = undefined;
   media.createAVRecorder().then((recorder) => {
     avRecorder = recorder;
   }, (err) => {
     console.error(`Invoke createAVRecorder failed, code is ${err.code}, message is ${err.message}`);
   })
   ```

2. Set the events to listen for.
   | Event Type| Description| 
   | -------- | -------- |
   | stateChange | Mandatory; used to listen for changes of the **state** attribute of the AVRecorder.| 
   | error | Mandatory; used to listen for AVRecorder errors.| 

     
   ```ts
   // Callback function for state changes.
   avRecorder.on('stateChange', (state, reason) => {
     console.log(`current state is ${state}`);
     // You can add the action to be performed after the state is switched.
   })
   
   // Callback function for errors.
   avRecorder.on('error', (err) => {
     console.error(`avRecorder failed, code is ${err.code}, message is ${err.message}`);
   })
   ```

3. Set audio recording parameters and call **prepare()**. The AVRecorder enters the **prepared** state.
   > **NOTE**
   >
   > Pay attention to the following when configuring parameters:
   > 
   > - In pure audio recording scenarios, set only audio-related parameters in **avConfig** of **prepare()**.
   > If video-related parameters are configured, an error will be reported in subsequent steps. If video recording is required, follow the instructions provided in [Video Recording Development](video-recording.md).
   > 
   > - The [recording formats](avplayer-avrecorder-overview.md#supported-formats) in use must be those supported by the system.
   > 
   > - The recording output URL (URL in **avConfig** in the sample code) must be in the format of fd://xx (where xx indicates a file descriptor). You must call [ohos.file.fs](../reference/apis/js-apis-file-fs.md) to implement access to the application file. For details, see [Application File Access and Management](../file-management/app-file-access.md).

     
   ```ts
   let avProfile = {
     audioBitrate: 100000, // Audio bit rate.
     audioChannels: 2, // Number of audio channels.
     audioCodec: media.CodecMimeType.AUDIO_AAC, // Audio encoding format. Currently, only AAC is supported.
     audioSampleRate: 48000, // Audio sampling rate.
     fileFormat: media.ContainerFormatType.CFT_MPEG_4A, // Encapsulation format. Currently, only M4A is supported.
   }
   let avConfig = {
     audioSourceType: media.AudioSourceType.AUDIO_SOURCE_TYPE_MIC, // Audio input source. In this example, the microphone is used.
     profile: avProfile,
     url: 'fd://35', // Obtain the file descriptor of the created audio file by referring to the sample code in Application File Access and Management.
   }
   avRecorder.prepare(avConfig).then(() => {
     console.log('Invoke prepare succeeded.');
   }, (err) => {
     console.error(`Invoke prepare failed, code is ${err.code}, message is ${err.message}`);
   })
   ```

4. Call **start()** to start recording. The AVRecorder enters the **started** state.

5. Call **pause()** to pause recording. The AVRecorder enters the **paused** state.

6. Call **resume()** to resume recording. The AVRecorder enters the **started** state again.

7. Call **stop()** to stop recording. The AVRecorder enters the **stopped** state.

8. Call **reset()** to reset the resources. The AVRecorder enters the **idle** state. In this case, you can reconfigure the recording parameters.

9. Call **release()** to switch the AVRecorder to the **released** state. Now your application exits the recording.


## Sample Code

  Refer to the sample code below to complete the process of starting, pausing, resuming, and stopping recording.
  
```ts
import media from '@ohos.multimedia.media';

export class AudioRecorderDemo {
  private avRecorder;
  private avProfile = {
    audioBitrate: 100000, // Audio bit rate.
    audioChannels: 2, // Number of audio channels.
    audioCodec: media.CodecMimeType.AUDIO_AAC, // Audio encoding format. Currently, only AAC is supported.
    audioSampleRate: 48000, // Audio sampling rate.
    fileFormat: media.ContainerFormatType.CFT_MPEG_4A, // Encapsulation format. Currently, only M4A is supported.
  };
  private avConfig = {
    audioSourceType: media.AudioSourceType.AUDIO_SOURCE_TYPE_MIC, // Audio input source. In this example, the microphone is used.
    profile: this.avProfile,
    url: 'fd://35', // Create, read, and write a file by referring to the sample code in Application File Access and Management.
  };

  // Set AVRecorder callback functions.
  setAudioRecorderCallback() {
    // Callback function for state changes.
    this.avRecorder.on('stateChange', (state, reason) => {
      console.log(`AudioRecorder current state is ${state}`);
    })
    // Callback function for errors.
    this.avRecorder.on('error', (err) => {
      console.error(`AudioRecorder failed, code is ${err.code}, message is ${err.message}`);
    })
  }

  // Process of starting recording.
  async startRecordingProcess() {
    // 1. Create an AVRecorder instance.
    this.avRecorder = await media.createAVRecorder();
    this.setAudioRecorderCallback();
    // 2. Obtain the file descriptor of the recording file and assign it to the URL in avConfig. For details, see FilePicker.
    // 3. Set recording parameters to complete the preparations.
    await this.avRecorder.prepare(this.avConfig);
    // 4. Start recording.
    await this.avRecorder.start();
  }

  // Process of pausing recording.
  async pauseRecordingProcess() {
    if (this.avRecorder.state ==='started') { // pause() can be called only when the AVRecorder is in the started state .
      await this.avRecorder.pause();
    }
  }

  // Process of resuming recording.
  async resumeRecordingProcess() {
    if (this.avRecorder.state === 'paused') { // resume() can be called only when the AVRecorder is in the paused state .
      await this.avRecorder.resume();
    }
  }

  // Process of stopping recording.
  async stopRecordingProcess() {
    // 1. Stop recording.
    if (this.avRecorder.state === 'started'
    || this.avRecorder.state ==='paused') { // stop() can be called only when the AVRecorder is in the started or paused state.
      await this.avRecorder.stop();
    }
    // 2. Reset the AVRecorder.
    await this.avRecorder.reset();
    // 3. Release the AVRecorder instance.
    await this.avRecorder.release();
    // 4. Close the file descriptor of the recording file.
  }

  // Complete sample code for starting, pausing, resuming, and stopping recording.
  async audioRecorderDemo() {
    await this.startRecordingProcess(); // Start recording.
    // You can set the recording duration. For example, you can set the sleep mode to prevent code execution.
    await this.pauseRecordingProcess(); // Pause recording.
    await this.resumeRecordingProcess(); // Resume recording.
    await this.stopRecordingProcess(); // Stop recording.
  }
}
```
