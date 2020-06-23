---
layout: post
title:  "Video audio basic knowledge"
date:   2013-01-31 15:47:34
---

1. Codec(code + decode)

  Because of the video file is very big, so need code(compress) the file to it smaller. when playing the file, decode the video to play. Common video encoding format: H264, VP8, mpeg4, msmpeg4v2... Common audio encoding format: aac, ac3, DTS, mp3, vorbis...

2. Container

  a file format store codeced file, can contain multi streams(video stream, audio stream, subtitle stream). Common video format: mkv, mp4, webm, mov, flv, avi... Common audio format: mp3, aac, ac3, ogg, wma...

3. Demux/Mux

  Demux: use demuxer parse the different stream from container.
  Mux: use muxer into the different stream according to rules to container.

4. Playback

    * access
    * demux
    * decode
    * output
