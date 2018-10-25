---
layout:     post
title:      "使用you-get模块下载爱奇艺视频"
subtitle:   ""
date:       2018-10-25
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    true
tags:
    - Python
---
>之前写过一篇用youtube-dl的模块来下载视频的博文，但是今天在使用youtube-dl下载爱奇艺视频的时候竟然失败了。如果使用爱奇艺的客户端进行下载，下载完成之后还需要进行转码，很麻烦。所以想到了之前用的you-get模块，竟然可以下载成功

## 使用you-get下载爱奇艺成功

```
PS C:\Users\Tesla Lau> you-get "http://www.iqiyi.com/w_19rs6ucehx.html"
ffmpeg version N-90173-gfa0c9d69d3 Copyright (c) 2000-2018 the FFmpeg developers
  built with gcc 7.3.0 (GCC)
  configuration: --enable-gpl --enable-version3 --enable-sdl2 --enable-bzlib --enable-fontconfig --enable-gnutls --enable-iconv --enable-libass --enable-libbluray --enable-libfreetype --enable-libmp3lame --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenjpeg --enable-libopus --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libtheora --enable-libtwolame --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxml2 --enable-libzimg --enable-lzma --enable-zlib --enable-gmp --enable-libvidstab --enable-libvorbis --enable-libvo-amrwbenc --enable-libmysofa --enable-libspeex --enable-libxvid --enable-libmfx --enable-amf --enable-cuda --enable-cuvid --enable-d3d11va --enable-nvenc --enable-dxva2 --enable-avisynth
  libavutil      56.  7.101 / 56.  7.101
  libavcodec     58. 13.100 / 58. 13.100
  libavformat    58. 10.100 / 58. 10.100
  libavdevice    58.  2.100 / 58.  2.100
  libavfilter     7. 12.100 /  7. 12.100
  libswscale      5.  0.101 /  5.  0.101
  libswresample   3.  0.101 /  3.  0.101
  libpostproc    55.  0.100 / 55.  0.100
...
...
...
[hls,applehttp @ 000001e3383eb000] Opening 'http://dx.data.video.iqiyi.com/videos/v1/20141112/5b/57/9051cadad84effc34235a54c87002267.ts?qypid=2820435209_04022000001000000000_2&start=6246916&end=6462378&hsize=42080&tag=2&v=&contentlength=78584&qdv=1&qd_uid=&qd_vip=0&qd_src=e29f36f91ee7418da930eb6cfb2b1316&qd_tm=1540443874849&qd_ip=315a8c49&qd_p=315a8c49&qd_k=ed2d29eb24834a7c02f8e59d51870344&sgti=&dfp=&qd_sc=6a39e883561c8cd67f0502ea49e81f6e' for reading
[mp4 @ 000001e3384be080] pts has no value
[mp4 @ 000001e3384be080] pts has no valueB time=00:01:15.46 bitrate= 611.4kbits/s speed=4.99x
    Last message repeated 2 times
[mp4 @ 000001e3384be080] pts has no valueB time=00:01:22.20 bitrate= 586.8kbits/s speed=5.17x
frame= 1258 fps= 79 q=-1.0 Lsize=    6324kB time=00:01:23.96 bitrate= 617.0kbits/s speed=5.27x
video:5618kB audio:646kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.959344%
site:                爱奇艺 (Iqiyi)
title:               “双十一”来了：网民疯狂购物 自嘲不理性消费
stream:
    - format:        HD
      container:     m3u8
      video-profile: 540p
      m3u8_url:      http://cache.m.iqiyi.com/mus/2820435209/5753e1c6e4094f4eb890e92646491884/afbe8fd3d73448c9//20141112/5b/57/211171c6b9d0e450abf1f77a95552536.m3u8?qd_originate=tmts_py&tvid=2820435209&bossStatus=0&qd_vip=0&px=&src=&prv=&previewType=&previewTime=&from=&qd_time=1540443874584&qd_p=315a8c49&qd_asc=d5f30812769fd255553d54b886518e24&qypid=2820435209_04022000001000000000_2&qd_k=ed2d29eb24834a7c02f8e59d51870344&isdol=0&code=2&ff=f4v&iswb=0&qd_s=otv&vf=56132ad12b9ff9f69539205268563836&np_tag=nginx_part_tag
    # download-with: you-get --format=HD [URL]

Downloading streaming content with FFmpeg, press q to stop recording...
ffmpeg -y -i http://cache.m.iqiyi.com/mus/2820435209/5753e1c6e4094f4eb890e92646491884/afbe8fd3d73448c9//20141112/5b/57/211171c6b9d0e450abf1f77a95552536.m3u8?qd_originate=tmts_py&tvid=2820435209&bossStatus=0&qd_vip=0&px=&src=&prv=&previewType=&previewTime=&from=&qd_time=1540443874584&qd_p=315a8c49&qd_asc=d5f30812769fd255553d54b886518e24&qypid=2820435209_04022000001000000000_2&qd_k=ed2d29eb24834a7c02f8e59d51870344&isdol=0&code=2&ff=f4v&iswb=0&qd_s=otv&vf=56132ad12b9ff9f69539205268563836&np_tag=nginx_part_tag -c copy -bsf:a aac_adtstoasc “双十一”来了：网民疯狂购物 自嘲不理性消费.mp4
```

## 使用youtube-dl下载爱奇艺失败

```
PS C:\Users\Tesla Lau> youtube-dl   "http://www.iqiyi.com/w_19rs6ucehx.html"
[iqiyi] temp_id: download video page
ERROR: Can't find any video; please report this issue on https://yt-dl.org/bug . Make sure you are using the latest version; see  https://yt-dl.org/update  on how to update. Be sure to call youtube-dl with the --verbose flag and include its complete output.
```