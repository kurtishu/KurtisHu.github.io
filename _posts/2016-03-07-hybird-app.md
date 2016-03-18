--- 
published: true
title: 混合开发 App（Hybrid App）
layout: post
author: Kurtis Hu
category: 
  - hybrid
tags: 
- 混合开发
- JS
- Jsbrage
- Hybird
- React
- React-Native
---

###  移动应用分类
  * 原生应用
  * Web应用
  * 混合应用

###  三者优缺点比较  
> [原生应用、Web应用、混合应用：3者的优缺点解析](http://www.leiphone.com/news/201406/12921-keats-difference-native-vs-web-apps.html)
>

Native App和Web App都有自己的优缺点，而Hybrid App在具备Native App和Web App优点的同时，也继承了两者的缺点。  

### 混合应用程序实现原理：  
在本地应用程序中添加WebView来显示HTML5（CSS、JavaScript）部分的内容，逻辑操作则集中在JavaScript和本地代码中实现。通过JavaScript来实现本地代码和HTML5之间的互操作。

### UI
**viewport的概念**      
在使用html5开发移动应用的时候，viewport可以让你开发出的页面，适应不同的设备的不同屏幕大小，不同的分辨率，控制用户的缩放、滚动行为，一般具体的设置如下:   
```  
   <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
```    
一般情况，在你的html中加入上面一行代码，就可以实现html的自适应了。  


### 混合开发在Android平台上的实现   

### 在iOS平台的实现

> [简单混合应用开发](http://bbs.gfan.com/android-6198184-1-1.html)  

### 常见框架
[Cordova](http://cordova.apache.org/) 、 [ionic](http://ionicframework.com/) 、 [AppCan](http://www.appcan.cn/) 、 [ApiCloud](http://www.apicloud.com/)   

### React Native
> React Native使你能够在Javascript和React的基础上获得完全一致的开发体验，构建世界一流的原生APP。  
> React Native着力于提高多平台开发的开发效率 —— 仅需学习一次，编写任何平台。(Learn once, write anywhere)

React Native 是使用html + Javascript 开发原生app的框架

<br/>
