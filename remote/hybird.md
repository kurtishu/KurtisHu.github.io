title: Hybird App Introduction
speaker: Kurtis Hu
url: https://github.com/ksky521/nodePPT
transition: slide2
theme: dark
files: /js/demo.js,/css/demo.css
date: 2016年05月20日

[slide]

# Hybird App
## @Kurtis Hu

<i class="fa fa-apple"></i>
<i class="fa fa-android"></i>
<i class="fa fa-css3"></i>
<i class="fa fa-html5"></i>

[slide style="background-image:url('/img/bg1.png')"]

## Hybird App(混合模式移动应用)
> A mobile application that is coded in both browser-supported language and computer language. 

[slide]
  ## web-app、native-app、hybrid app
  -----
  ![3者的优缺点解析](/img/app-analys.png)
  
[slide]
  ## native-app(原生应用)
  -----
  * 优点：
     * 可访问手机所有硬件（GPS、摄像头）设备 {:&.moveIn} 
     * 速度更快、性能高、整体用户体验不错
     * 可线下使用
     * 支持大量图形和动画
     * 容易获取
  * 缺点：
     * 开发成本高 {:&.moveIn} 
     * 支持设备非常有限
     * 上线时间不确定（App Store审核过程不一）
     * 内容限制（App Store限制）
     * 获得新版本时需重新下载应用更新

[slide]
  ## web-app(Web应用)
  -----
   <small>Web应用本质上是为移动浏览器设计的基于Web的应用，它们是用普通Web开发语言开发的，可以在各种智能手机浏览器上运行</small>
  * 优点：
     * 支持设备广泛 {:&.moveIn} 
     * 较低的开发成本
     * 可即时上线
     * 无内容限制
     * 用户可以直接使用最新版本
  * 缺点：
     * 表现略差(对联网的要求比较大) {:&.moveIn}  
     * 用户体验没那么炫
     * 图片和动画支持性不高
     * 要求联网
     * 对手机特点有限制（摄像头、GPS等）

[slide]
  ## hybrid app(混合应用)
  -----
  <small>混合应用大家都知道是原生应用和Web应用的结合体，采用了原生应用的一部分、Web应用的一部分，所以必须在部分在设备上运行、部分在Web上运行</small>  
  <span class="red">混合应用中比例很自由，比如Web 占90%，原生占10%；或者各占50%</span>  
  * 优点：
     * 兼容多平台 {:&.moveIn} 
     * 顺利访问手机的多种功能
     * App Store中可下载（Web应用套用原生应用的外壳）
     * 可线下使用
  * 缺点：
     * 用户体验不如本地应用 {:&.moveIn} 
     * 性能稍慢（需要连接网络）
     * 技术还不是很成熟 

[slide]
## Hybrid App开发实战
----
## 三种不同的解决方案

[slide]

 [magic data-transition="earthquake"]
  ## 以WebView作为用户界面层，以Javascript作为基本逻辑，以及和中间件通讯，再由中间件访问底层API的方式，进行应用开发
  -----
  <i>![Cordova](/img/cordova.jpg)</i>
  <i>![Ionic](/img/ionic.jpg)</i>
  <i>![AppCan](/img/appcan.jpg)</i>
  <i>![ApiCould](/img/apicould.jpg)</i>

  ====
  ## 使用非官方语言的工具，打包成原生应用的方式开发
  -----
  <i>![React](/img/react.png)</i>
  <i>![Kotlin](/img/kotlin.jpg)</i>
   ====
  ## 在开发原生应用的基础上，嵌入WebView但是整体的架构使用原生应用提供
  -----
 [/magic]

[slide]
## 常见的hybrid通信方式
传统的JSInterface

[slide]
## Demo
-----
<div class="columns-2">
<pre><code class="javascript">


( function showToast(toast) {
   javascript:control.showToast(toast);
  }
  function log(msg){
   console.log(msg);
  }
)


</code></pre>
<pre><code class="javascript">
   {
     WebSettings webSettings = webView.getSettings();
     webSettings.setJavaScriptEnabled(true);
     webView.addJavascriptInterface(new JsInterface(), "control");
     webView.loadUrl("file:///android_asset/interact.html");
  }
 
  public class JsInterface {
    @JavascriptInterface
    public void showToast(String toast) {
      Toast.makeText(MainActivity.this, toast, Toast.LENGTH_SHORT).show();
      log("show toast success");
   }
</code></pre>
</div>

[slide]
## 常见的hybrid通信方式
JSBridge

[slide]
<span class="blue">WebChromeClient</span>
``` java  
 @Override
public boolean onJsPrompt(WebView view, String url, String message, String defaultValue, JsPromptResult result) {
    return super.onJsPrompt(view, url, message, defaultValue, result);
}

@Override
public boolean onJsAlert(WebView view, String url, String message, JsResult result) {
    return super.onJsAlert(view, url, message, result);
}

@Override
public boolean onJsConfirm(WebView view, String url, String message, JsResult result) {
    return super.onJsConfirm(view, url, message, result);
}
```  
<span class="label label-warning">hybrid://JSBridge:1538351/method?{“message”:”msg”}</span>


[slide]
## 常见的hybrid通信方式
JavascriptCore

[slide]
## React Native
----
> A framework for building native apps using React.
> <smal>Learn once, write anywhere </small> {:&.pull-right} 

[slide]
## React Demo

[slide]
## 使用React Native编写的应用
----
<iframe data-src="http://reactnative.cn/cases.html" src="about:blank;" width="1024" height="640" style="width:1024px;height:640px;  background-color: transparent;"></iframe>

[slide]
## Thank You!
