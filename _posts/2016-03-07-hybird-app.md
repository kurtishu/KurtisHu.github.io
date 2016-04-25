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
```  java
   <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
```    
一般情况，在你的html中加入上面一行代码，就可以实现html的自适应了。  


### 混合开发在Android平台上的实现   

### 在iOS平台的实现

> [简单混合应用开发](http://bbs.gfan.com/android-6198184-1-1.html)  

### 三种不同的混合型APP应用开发解决方案
>   [Link](http://cache.baiducontent.com/c?m=9d78d513d9d431df4f9ae5697d65c0176d4381132ba1d1020cd0843e92732a405321a3e52878564291d27d141cb20c19afe736056e4470ecc29fd011cabbe57972d73a676d54c11a588845e7900c629d3d9058eaae1ae7b9fb3293add8c4df23098c0c5b&p=882a9645dcd90be00abe9b7c4205cf&newp=8679df0486cc42af52fec7710f598d231610db2151ddda06&user=baidu&fm=sc&query=%BB%EC%BA%CF%D3%A6%D3%C3&qid=95bad1f2000dfea4&p1=16)
### 常见框架
[Cordova](http://cordova.apache.org/) 、 [ionic](http://ionicframework.com/) 、 [AppCan](http://www.appcan.cn/) 、 [ApiCloud](http://www.apicloud.com/)   
[HTML5来了，7个混合式移动开发框架](http://www.cocoachina.com/webapp/20141222/10718.html)

[好好和h5沟通！几种常见的hybrid通信方式](http://zjutkz.net/2016/04/17/%E5%A5%BD%E5%A5%BD%E5%92%8Ch5%E6%B2%9F%E9%80%9A%EF%BC%81%E5%87%A0%E7%A7%8D%E5%B8%B8%E8%A7%81%E7%9A%84hybrid%E9%80%9A%E4%BF%A1%E6%96%B9%E5%BC%8F/)
### React Native
> React Native使你能够在Javascript和React的基础上获得完全一致的开发体验，构建世界一流的原生APP。  
> React Native着力于提高多平台开发的开发效率 —— 仅需学习一次，编写任何平台。(Learn once, write anywhere)

React Native 是使用html + Javascript 开发原生app的框架

<br/>
