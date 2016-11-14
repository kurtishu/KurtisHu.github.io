title: ZhiBo
speaker: Kurtis Hu
url: https://github.com/ksky521/nodePPT
transition: cards
files: /js/demo.js,/css/demo.css

[slide]

# ZhiBo
## 演讲者：Kurtis Hu

[slide]

## 直播效果图 {:&.flexbox.vleft}
----
![](http://upload-images.jianshu.io/upload_images/304825-17ee0ce99bde2de0.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]

## 一个完整直播app功能
1. 聊天
   私聊、聊天室、点亮、推送、黑名单等;
2. 直播列表
   关注、热门、最新、分类直播用户列表等；
3. 直播
   录制、推流、解码、播放、美颜、心跳、后台切换、主播对管理员操作、管理员对用户等；
4. 房间逻辑
   创建房间、进入房间、退出房间、关闭房间、切换房间、房间管理员设置、房间用户列表等;
5. 用户逻辑
   普通登陆、第三方登陆、注册、搜索、修改个人信息、关注列表、粉丝列表、忘记密码、查看个人信息、收入榜、关注和取关、检索等；
6. 观看直播
   聊天信息、滚屏弹幕、礼物显示、加载界面等；
7. 礼物
   普通礼物、豪华礼物、红包、排行榜、第三方充值、内购、礼物动态更新、提现等；
8. 统计
   APP业务统计、第三方统计等；
9. 超管
   禁播、隐藏、审核等；

[slide]
## 直播app原理
----
直播原理：把主播录制的视频，推送到服务器，在由服务器分发给观众观看。

直播环节：推流端（采集、美颜处理、编码、推流）、服务端处理（转码、录制、截图、鉴黄）、播放器（拉流、解码、渲染）、互动系统（聊天室、礼物系统、赞）

[slide]
## 整直播app实现流程
----
![](http://upload-images.jianshu.io/upload_images/1728484-acb8378b97c469f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]
## 采集
----
采集是整个视频推流过程中的第一个环节，它从系统的采集设备中获取原始视频数据，将其输出到下一个环节。
** 音频采集 **
通过设备将环境中的模拟信号采集成 PCM 编码的原始数据. 常见的音频压缩格式有：MP3，AAC，OGG，WMA，Opus，FLAC，APE，m4a 和 AMR 等。

音频采集和编码主要面临的挑战在于：延时敏感、卡顿敏感、噪声消除（Denoise）、回声消除（AEC）、静音检测（VAD）和各种混音算法等。

** 图像采集 **
图像的采集过程主要由摄像头等设备拍摄成 YUV 编码的原始数据，然后经过编码压缩成 H.264 等格式的数据分发出去。常见的视频封装格式有：MP4、3GP、AVI、MKV、WMV、MPG、VOB、FLV、SWF、MOV、RMVB 和 WebM 等。

[slide]
## 处理
---- 
![](http://upload-images.jianshu.io/upload_images/311249-133b2caa206a8720?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]
## 编码和封装
---- 
H.264
HEVC/H.265
VP8
VP9

FFmpeg
在流媒体传输，尤其是直播中主要采用的就是 FLV 和 MPEG2-TS 格式，分别用于 RTMP/HTTP-FLV 和 HLS 协议。

[slide]
## 传输
----

[slide]
## 服务端处理
----
为了让主播推上来的流适配各个平台端各种不同协议，需要在服务端做一些流处理工作，比如转码成不同格式支持不同协议如 RTMP、HLS 和 FLV，一路转多路流适配各种不同的网络状况和不同分辨率的终端设备


[slide]
## 拉流
---- 
直播协议选择：
 即时性要求较高或有互动需求的可以采用RTMP,RTSP
 对于有回放或跨平台需求的，推荐使用HLS
直播协议对比 :
 ![](http://upload-images.jianshu.io/upload_images/304825-f92e85515845e107.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]
## 解码
---- 

解封装 *
demuxing（分离）：从视频流、音频流，字幕流合成的文件(容器格式（FLV，TS）)中， 分解出视频、音频或字幕，各自进行解码。

解码介绍(硬解码, 解码)

[slide]
## 播放
视频播放器
ijkplayer:一个基于FFmpeg的开源Android/iOS视频播放器


[slide]
## 第三方直播云系统
----
七牛云
网易视频云

[slide]
## 直播功能：自研还是使用第三方直播SDK开发?
第三方SDK开发: 对于一个初创团队来讲，自研直播不管在技术门槛、CDN、带宽上都是有很大的门槛的，而且需要耗费大量的时间才能做出成品，不利于拉投资。
   1. 降低成本
   2. 提升效率
   3. 降低风险
   4. 专业的事，找专业的人来做

自研：公司直播平台大，从长远看，自研可以节省成本，技术成面比直接用SDK可控多了。

[slide]
## 参考
----
[http://www.jianshu.com/p/339041855364](http://www.jianshu.com/p/339041855364)
[http://www.jianshu.com/p/bd42bacbe4cc](http://www.jianshu.com/p/bd42bacbe4cc)
[http://www.jianshu.com/p/ddb640ac4fec](http://www.jianshu.com/p/ddb640ac4fec)
[https://www.zhihu.com/question/42162310](https://www.zhihu.com/question/42162310)








