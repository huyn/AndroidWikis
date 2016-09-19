* List all the decoders, software decoder and hardware decoder
```
private void printAvailableDecoder() {
    int numCodecs = MediaCodecList.getCodecCount();
    MediaCodecInfo codecInfo = null;
    for (int i = 0; i < numCodecs && codecInfo == null; i++) {
      MediaCodecInfo info = MediaCodecList.getCodecInfoAt(i);
      if (info.isEncoder()) {
        continue;
      }
      String[] types = info.getSupportedTypes();
      for (String s : types) {
        System.out.println("======================mime: " + s + " decoder: " + info.getName());
      }
    }
  }
  ```
  different mobiles has seprate decoders, for example, there are what I get from `oppo R9`
  ```
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/mpeg decoder: OMX.google.mp3.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/3gpp decoder: OMX.google.amrnb.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/amr-wb decoder: OMX.google.amrwb.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/mp4a-latm decoder: OMX.google.aac.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/g711-alaw decoder: OMX.google.g711.alaw.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/g711-mlaw decoder: OMX.google.g711.mlaw.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/vorbis decoder: OMX.google.vorbis.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/opus decoder: OMX.google.opus.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/raw decoder: OMX.google.raw.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/gsm decoder: OMX.google.gsm.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/mp4a-latm decoder: OMX.google.aac.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/qcelp decoder: OMX.qcom.audio.decoder.Qcelp13
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: audio/evrc decoder: OMX.qcom.audio.decoder.evrc
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/avc decoder: OMX.qcom.video.decoder.avc
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/mpeg2 decoder: OMX.qcom.video.decoder.mpeg2
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/mp4v-es decoder: OMX.qcom.video.decoder.mpeg4
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/3gpp decoder: OMX.qcom.video.decoder.h263
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/x-ms-wmv decoder: OMX.qcom.video.decoder.vc1
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/divx decoder: OMX.qcom.video.decoder.divx
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/divx311 decoder: OMX.qcom.video.decoder.divx311
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/divx4 decoder: OMX.qcom.video.decoder.divx4
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/x-vnd.on2.vp8 decoder: OMX.qcom.video.decoder.vp8
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/hevc decoder: OMX.qcom.video.decoder.hevc
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/mp4v-es decoder: OMX.google.mpeg4.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/mp4v-esdp decoder: OMX.google.mpeg4.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/3gpp decoder: OMX.google.h263.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/avc decoder: OMX.google.h264.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/hevc decoder: OMX.google.hevc.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/x-vnd.on2.vp8 decoder: OMX.google.vp8.decoder
09-19 18:08:29.243 3792-13514/com.aube.phone I/System.out: ======================mime: video/x-vnd.on2.vp9 decoder: OMX.google.vp9.decoder
```
  `OMX`(`OpenMax`) is a framework for video display
  software decoders are like `OMX.google.***`
  
  * Get Decoder
  you can get decoder by `codecname` like this:
  ```
  codec = MediaCodec.createByCodecName("OMX.MTK.VIDEO.DECODER.MPEG4");
  ```
  or you can get decoder by mimetype:
  ```
  codec = MediaCodec.createDecoderByType("video/avc");
  ```
  
  * Last
  software decode is not efficient, avoid using it.
