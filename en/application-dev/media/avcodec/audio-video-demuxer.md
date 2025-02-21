# Audio and Video Demuxing

You can call the native APIs provided by the **AVDemuxer** module to demux audio and video, that is, to extract audio and video frame data from bit stream data.

Currently, two data input types are supported: remote connection (over HTTP) and File Descriptor (FD).

The following demuxing formats are supported:

| Media Format | Muxing Format                     | Stream Format                     |
| -------- | :----------------------------| :----------------------------|
| Audio/Video    | mp4                        |Video stream: AVC (H.264); audio stream: AAC and MPEG (MP3)|
| Audio/Video    | mkv                        |Video stream: AVC (H.264); audio stream: AAC, MPEG (MP3), and OPUS|
| Audio/Video    | mpeg-ts                    |Video stream: AVC (H.264); audio stream: AAC and MPEG (MP3)|
| Audio      | m4a                        |Audio stream: AAC|
| Audio      | aac                        |Audio stream: AAC|
| Audio      | mp3                        |Audio stream: MPEG (MP3)|
| Audio      | ogg                        |Audio stream: OGG|
| Audio      | flac                        |Audio stream: FLAC|
| Audio      | wav                        |Audio stream: PCM|
| Audio      | amr                        |Audio stream: AMR (AMR-NB and AMR-WB)|

**Usage Scenario**

- Audio and video playback
  
  Demux audio and video streams, decode the frame data obtained through demuxing, and play the decoded data.

- Audio and video editing
  
  Demux audio and video streams, and edit the specified frames.

- Media file format conversion

  Demux audio and video streams, and encapsulate them into a new file format.

## How to Develop

Read [AVDemuxer](../../reference/apis-avcodec-kit/_a_v_demuxer.md) and [AVSource](../../reference/apis-avcodec-kit/_a_v_source.md) for the API reference.

> **NOTE**
>
> - To call the demuxing APIs to parse a network playback path, declare the **ohos.permission.INTERNET** permission by following the instructions provided in [Declaring Permissions](../../security/AccessToken/declare-permissions.md).
> - To call the demuxer APIs to write a local file, request the **ohos.permission.READ_MEDIA** permission by following the instructions provided in [Requesting User Authorization](../../security/AccessToken/request-user-authorization.md).
> - You can also use **ResourceManager.getRawFd** to obtain the FD of a file packed in the HAP file. For details, see [ResourceManager API Reference](../../reference/apis-localization-kit/js-apis-resource-manager.md#getrawfd9).

### Linking the Dynamic Library in the CMake Script

``` cmake
target_link_libraries(sample PUBLIC libnative_media_avdemuxer.so)
target_link_libraries(sample PUBLIC libnative_media_avsource.so)
target_link_libraries(sample PUBLIC libnative_media_core.so)
```

### How to Develop

1. Add the header files.

   ```c++
   #include <multimedia/player_framework/native_avdemuxer.h>
   #include <multimedia/player_framework/native_avsource.h>
   #include <multimedia/player_framework/native_avcodec_base.h>
   #include <multimedia/player_framework/native_avformat.h>
   #include <multimedia/player_framework/native_avbuffer.h>
   ```

2. Create a demuxer instance.

   ```c++
   // Create the FD. You must have the read permission on the file handle when opening the file. (filePath indicates the path of the file to be demuxed. The file must exist.)
   std::string filePath = "test.mp4";
   int fd = open(filePath.c_str(), O_RDONLY);
   struct stat fileStatus {};
   size_t fileSize = 0;
   if (stat(filePath.c_str(), &fileStatus) == 0) {
      fileSize = static_cast<size_t>(fileStatus.st_size);
   } else {
      printf("get stat failed");
      return;
   }
   // Create a source resource object for the FD resource file. If offset is not the start position of the file or size is not the actual file size, the data obtained may be incomplete. Consequently, the source resource object may fail to create or subsequent demuxing may fail.
   OH_AVSource *source = OH_AVSource_CreateWithFD(fd, 0, fileSize);
   if (source == nullptr) {
      printf("create source failed");
      return;
   }
   // (Optional) Create a source resource object for the URI resource file.
   // OH_AVSource *source = OH_AVSource_CreateWithURI(uri);
   ```

   ```c++
   // Create a demuxer for the resource object.
   OH_AVDemuxer *demuxer = OH_AVDemuxer_CreateWithSource(source);
   if (demuxer == nullptr) {
      printf("create demuxer failed");
      return;
   }
   ```
3. (Optional) Register a [callback to obtain the media key system information](../../reference/apis-drm-kit/_drm.md#drm_mediakeysysteminfocallback). If the stream is not a DRM stream or the [media key system information](../../reference/apis-drm-kit/_drm.md#drm_mediakeysysteminfo) has been obtained, you can skip this step.

   Import the header file.
   ```c++
   #include <multimedia/drm_framework/native_drm_common.h>
   ```
   Link the dynamic library in the cmake script.

   ``` cmake
   target_link_libraries(sample PUBLIC libnative_drm.so)
   ```

   The following is the sample code:
   ```c++
   // Implement the OnDrmInfoChanged callback.
   static void OnDrmInfoChanged(DRM_MediaKeySystemInfo *drmInfo)
   {
      // Parse the media key system information, including the quantity, DRM type, and corresponding PSSH.
   }

   // Set the asynchronous callbacks.
   DRM_MediaKeySystemInfoCallback callback = &OnDrmInfoChanged;
   int32_t ret = OH_AVDemuxer_SetMediaKeySystemInfoCallback(demuxer, callback);

   // After the callback is invoked, you can call the API to proactively obtain the media key system information.
   DRM_MediaKeySystemInfo mediaKeySystemInfo;
   OH_AVDemuxer_GetMediaKeySystemInfo(demuxer, &mediaKeySystemInfo);
   ```

4. (Optional) Obtain the number of tracks. If you know the track information, skip this step.

   ```c++
   // Obtain the number of tracks from the file source information.
   OH_AVFormat *sourceFormat = OH_AVSource_GetSourceFormat(source);
   if (sourceFormat == nullptr) {
      printf("get source format failed");
      return;
   }
   int32_t trackCount = 0;
   OH_AVFormat_GetIntValue(sourceFormat, OH_MD_KEY_TRACK_COUNT, &trackCount);
   OH_AVFormat_Destroy(sourceFormat);
   ```

5. (Optional) Obtain the track index and format. If you know the track information, skip this step.

   ```c++
   uint32_t audioTrackIndex = 0;
   uint32_t videoTrackIndex = 0;
   int32_t w = 0;
   int32_t h = 0;
   int32_t trackType;
   for (uint32_t index = 0; index < (static_cast<uint32_t>(trackCount)); index++) {
      // Obtain the track format.
      OH_AVFormat *trackFormat = OH_AVSource_GetTrackFormat(source, index);
      if (trackFormat == nullptr) {
         printf("get track format failed");
         return;
      }
      OH_AVFormat_GetIntValue(trackFormat, OH_MD_KEY_TRACK_TYPE, &trackType);
      static_cast<OH_MediaType>(trackType) == OH_MediaType::MEDIA_TYPE_AUD ? audioTrackIndex = index : videoTrackIndex = index;
      // Obtain the width and height of the video track.
      if (trackType == OH_MediaType::MEDIA_TYPE_VID) {
         OH_AVFormat_GetIntValue(trackFormat, OH_MD_KEY_WIDTH, &w);
         OH_AVFormat_GetIntValue(trackFormat, OH_MD_KEY_HEIGHT, &h);
      }
      OH_AVFormat_Destroy(trackFormat);
   }
   ```

6. Select a track, from which the demuxer reads data.

   ```c++
   if(OH_AVDemuxer_SelectTrackByID(demuxer, audioTrackIndex) != AV_ERR_OK){
      printf("select audio track failed: %d", audioTrackIndex);
      return;
   }
   if(OH_AVDemuxer_SelectTrackByID(demuxer, videoTrackIndex) != AV_ERR_OK){
      printf("select video track failed: %d", videoTrackIndex);
      return;
   }
   // (Optional) Deselect the track.
   // OH_AVDemuxer_UnselectTrackByID(demuxer, audioTrackIndex);
   ```

7. (Optional) Seek to the specified time for the selected track.

   ```c++
   // Demuxing is performed from this time.
   // Note:
   // 1. If OH_AVDemuxer_SeekToTime is called for an MPEG TS file, the target position may be a non-key frame. You can then call OH_AVDemuxer_ReadSampleBuffer to check whether the current frame is a key frame based on the obtained OH_AVCodecBufferAttr. If it is a non-key frame, which causes display issues on the application side, cyclically read the frames until you reach the first key frame, where you can perform processing such as decoding.
   // 2. If OH_AVDemuxer_SeekToTime is called for an OGG file, the file seeks to the start of the time interval (second) where the input parameter millisecond is located, which may cause a certain number of frame errors.
   OH_AVDemuxer_SeekToTime(demuxer, 0, OH_AVSeekMode::SEEK_MODE_CLOSEST_SYNC);
   ```

8. Start demuxing and cyclically obtain frame data. The code snippet below uses a file that contains audio and video tracks as an example.

   ```c++
   // Create a buffer to store the data obtained after demuxing.
   OH_AVBuffer *buffer = OH_AVBuffer_Create(w * h * 3 >> 1);
   if (buffer == nullptr) {
      printf("build buffer failed");
      return;
   }
   OH_AVCodecBufferAttr info;
   bool videoIsEnd = false;
   bool audioIsEnd = false;
   int32_t ret;
   while (!audioIsEnd || !videoIsEnd) {
      // Before calling OH_AVDemuxer_ReadSampleBuffer, call OH_AVDemuxer_SelectTrackByID to select the track from which the demuxer reads data.
      // Obtain audio frame data.
      if(!audioIsEnd) {
         ret = OH_AVDemuxer_ReadSampleBuffer(demuxer, audioTrackIndex, buffer);
         if (ret == AV_ERR_OK) {
            // Obtain the process the audio frame data in the buffer.
            OH_AVBuffer_GetBufferAttr(buffer, &info);
            printf("audio info.size: %d\n", info.size);
            if (info.flags == OH_AVCodecBufferFlags::AVCODEC_BUFFER_FLAGS_EOS) {
               audioIsEnd = true;
            }
         }
      }
      if(!videoIsEnd) {
         ret = OH_AVDemuxer_ReadSampleBuffer(demuxer, videoTrackIndex, buffer);
         if (ret == AV_ERR_OK) {
            // Obtain the process the video frame data in the buffer.
            OH_AVBuffer_GetBufferAttr(buffer, &info);
            printf("video info.size: %d\n", info.size);
            if (info.flags == OH_AVCodecBufferFlags::AVCODEC_BUFFER_FLAGS_EOS) {
               videoIsEnd = true;
            }
         }
      }
   }
   OH_AVBuffer_Destroy(buffer);
   ```

9. Destroy the demuxer instance.

   ```c++
   // Manually set the instance to NULL after OH_AVSource_Destroy is called. Do not call this API repeatedly for the same instance; otherwise, a program error occurs.
   if (OH_AVSource_Destroy(source) != AV_ERR_OK) {
      printf("destroy source pointer error");
   }
   source = NULL;
   // Manually set the instance to NULL after OH_AVDemuxer_Destroy is called. Do not call this API repeatedly for the same instance; otherwise, a program error occurs.
   if (OH_AVDemuxer_Destroy(demuxer) != AV_ERR_OK) {
      printf("destroy demuxer pointer error");
   }
   demuxer = NULL;
   close(fd);
   ```
