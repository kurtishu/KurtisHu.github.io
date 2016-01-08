---
layout: post
title: 图解Activity四种启动模式
author: kurtis.hu
categories:
  - Android
tags:
  - launchMode
---
<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; ">Android应用运行起来后就会开启一条线程，线程中会运行一个任务栈，当Activity实例创建后就会放入任务栈中。Activity启动模式的设置在AndroidManifest.xml文件中，通过配置Activity的属性android:launchMode=""设置。</span>

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "></span>

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><strong>1.&nbsp;Standard模式（默认）</strong><br />Android activity 默认的启动模式， 每次启动一个activity 都是重新创建一个新的实例，并且置于栈顶，点击Back键， activity销毁的顺序按照出栈顺序(LIFO)执行。</span>

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><strong style="font-family: Simsun; text-align: left; white-space: normal; "><span style="font-family: 宋体; font-size: 14px; "></span></strong></span>



<img src="/content/images/Standard.png" width="431" height="390" />

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><strong><span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: medium; text-align: left; ">2.&nbsp;SingleTop模式<br /></span></strong><span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: medium; text-align: left; ">这种模式会考虑当前要激活的Activity实例在任务栈中是否正处于栈顶，如果处于栈顶则无需重新创建新的实例，会重用已存在的实例，否则会在任务栈中创建新的实例。注：Activity2 的launchMode 为singleTop。</span></span>

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><strong style="font-family: Simsun; font-size: medium; text-align: left; "><img src="/content/images/SingleTop.png" width="358" height="386" /></strong></span>

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><strong><span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: medium; text-align: left; ">3.&nbsp;SingleTask模式<br /></span></strong><span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: medium; text-align: left; ">如果任务栈中存在该模式的Activity实例，则把栈中该实例以上的Activity实例全部移除，调用该实例的newIntent()方法重用该Activity，使该实例处於栈顶位置，否则就重新创建一个新的Activity实例。<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: medium; text-align: left; ">注：Activity2 的launchMode 为singleTask。</span></span></span>

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><strong style="font-family: Simsun; font-size: medium; text-align: left; "><img src="/content/images/SingleTask.png" width="541" height="418" /></strong></span>

<p class="p0" style="font-family: Simsun; font-size: medium; white-space: normal; text-align: left; ">
  <span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><strong>4.&nbsp;SingleInstance模式</strong><br />当该模式Activity实例在任务栈中创建后，只要该实例还在任务栈中，即只要激活的是该类型的Activity，都会通过调用实例的newIntent()方法重用该Activity，此时使用的都是同一个Activity实例，它都会处于任务栈的栈顶。此模式一般用于加载较慢的，比较耗性能且不需要每次都重新创建的Activity。<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: medium; text-align: left; ">注：Activity2 的launchMode 为singleInstance。</span></span>
</p>

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><img src="/content/images/SingleInstance.png" width="508" height="428" /></span>

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><strong>总结：</strong><br />standard：默认模式，始终创建新的实例。<br />singleTop： 要激活的Activity处于栈顶，则不新建实例，重用该实例，否则新建实例。<br />singleTask： 检查要激活Activity在栈中是否存在，如果存在把该实例pop 到栈顶，该实例栈以上的实例出栈，如果不存在，新建一个栈并把该实例置于栈底。<br />singleInstance：检查要激活Activity在栈中是否存在，不存在，新建一个栈并把该实例置于栈底，存在直接使用该实例，singleInstance的实例在所在的栈的栈底，并且该栈中只有唯一该对象。</span>

<span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; "><strong>signleTask 和singleInstance的区别<br /></strong>这两种启动模式存在某些共同点，也是稍微难以理解的两种模式。<br /></span><strong style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; ">相同点：<br /></strong><span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; ">1. 都只存在唯一的实例<br /></span><span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; ">2.存在实例的时候都是会新建一个栈，并且把新建的对待置于栈底。<br /></span><strong style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; ">不同点：<br /></strong><span style="font-family: 微软雅黑, &#39;Microsoft YaHei&#39;; font-size: 16px; ">1. singleTask 实例所在的栈中可以存放其他的实例，singleInstance 实例只存在其本身一个实例</span>