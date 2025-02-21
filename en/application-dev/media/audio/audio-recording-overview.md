# Audio Recording Development

## Selecting an Audio Recording Development Mode

The system provides a variety of APIs for you to develop audio recording applications. You can select them based on the recording output formats, audio usage scenarios, and even the programming language you use. Selecting a suitable class helps you reduce development workload and your application deliver a better effect.

- [AudioCapturer](using-audiocapturer-for-recording.md): provides ArkTS and JS API to implement audio input. It supports only the PCM format and requires applications to continuously read audio data. The application can perform data processing after audio output. This class can be used to develop more professional and diverse recording applications. To use this class, you must have basic audio processing knowledge.

- [OpenSL ES](using-opensl-es-for-recording.md): provides a set of standard, cross-platform native audio APIs. It supports audio input in PCM format and is suitable for recording applications that are ported from other embedded platforms or that implement audio input at the native layer.

- [Using OHAudio for Audio Recording](using-ohaudio-for-recording.md): provides a set of native APIs for audio input. These APIs are normalized in design and support both common and low-latency audio channels. They are suitable for playback applications that implement audio input at the native layer.

In addition to the preceding classes, you can also use Media Kit to implement audio playback.

- [AVRecorder](../media/using-avrecorder-for-recording.md): provides ArkTS and JS APIs to implement audio recording. It also supports audio input, audio encoding, and media encapsulation. You can directly call device hardware, such as microphone, for recording and generate M4A audio files.

## Precautions for Developing Audio Recording Applications

The application must request the **ohos.permission.MICROPHONE** permission from the user before invoking the microphone to record audio.

1. [Declare the permission](../../security/AccessToken/declare-permissions.md).
2. [Request user authorization](../../security/AccessToken/request-user-authorization.md).

For details about how to use and manage microphones, see [Microphone Management](mic-management.md).
