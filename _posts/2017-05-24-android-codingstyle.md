--- 
published: true
title:  Coding Style
layout: post
author: Kurtis Hu
category: 
  - Android
tags: 
- Coding Style
---
 
Android编程规范

### 基本原则 
 * 代码风格与android源码保持一致
 * 命名要清晰明了、有明确含义
 * 同一产品命名风格要保持一致，避免一意多词
 * 同一作用域，不能有变量重名，如局部变量与全局变量重名

### 包名  
 * package命名如com.brian.xx.yy.zz，xx为产品，yy为模块，zz为子模块
 * 模块划分，按以下两种方式均可，但需要项目组统一
按产品业务划分，如
com.brian.example.homepage 和 com.brian.example.player 按逻辑功能划分，如
com.brian.example.homepage.ui 和 com.brian.example.homepage.logic

### 类成员命名，参考android源码，如 android.content.pm.PackageManager
 * 类： public abstract class PackageManager
 * 函数： public abstract PackageInfogetPackageInfo(String packageName)
 * 常量： public static final int GET_ACTIVITIES= 0x00000001;
 * 静态变量： static ComponentName sComponent;
 * 成员变量： ComponentName mComponent;
 * 临时变量： ComponentName component;
 
### 资源命名
 * 文件名（字母小写和下划线组成）activity_main.xml ic_launcher.png
 * 资源名id（字母小写和下划线组成）android:id="@+layout/loading_view" 应用名称 代码排版
 
### 文字编码
 * 统一使用utf8编码
### 缩进对齐
 * 代码缩进采用 4个空格
 * 代码行首，合理缩进，以简洁明了为原则
### 空格
 * 条件语句，关键字与“(”用空格隔开，如 if (xx)、while (i> 3)
 * 注释内容，左右用空格隔开，如 // xxx，/ xxx /
 * 比较操作符、赋值操作符、算术操作符、逻辑操作符、位操作符，等双目操作符的前后加空格
 
 ```java
    if ( (a >= b) && (c <= d) )
    if (size >= MAX_SIZE)
    a = b + c;
    a *= 2;
    a = b ^ 2;
 ```   
 
 *  "!"、"~"、"++"、"--"、"&"（地址运算符）等单目操作符前后不加空格
 * 逗号、分号（非行结束符号）在后面加空格，前面不加空格
 ```java
    int x = 1, y = 2, z = 3;
    function(x, y, z);
    for (inti = 0; i < 10; i++)
```  

### 条件语句（if、for、while、do）

 * 条件语句，使用完备的括号
 * 条件语句，独自占一行，执行语句不得紧跟其他
 
 ```java
     // BAD
    if (flag) doSomething();
    // GOOD
    if (flag) {
      doSomething();
    }
```   
 * 条件语句，不论语执行句有多少行都要加“{}”
 
### 代码结构
 * 一行只写一条语句
 * 代码以“段”来编写，作用相近的代码写在一段，段与段间以空行分开，注释也相应以“段”来注释
 * 代码文件中从上到下，函数依次按照调度、被调度的顺序出现
 
### 代码注释
#### 基本原则
 * 注释语言必须准确、简洁、易懂，能直接反映编程思路
 * 统一使用中文作为注释语言，除非直接拷贝第三方的英语注释
 * 注释比例没有严格的要求，建议不低于15%
 * 注释要与代码保持一致，代码作用变了，注释也要更新
 * 对于逻辑复杂、使用有限制的代码，需要重点注释
#### 必须注释
 * 文件
 * 类
 * 函数（对外接口public函数）
 * 常量
 * 成员变量（有特殊含义）
 * 静态变量
 * 特殊逻辑、定制逻辑、有坑逻辑、临时逻辑
#### 建议注释
 * 复杂的逻辑
 * 重要的分支，如 if-else，switch-case
 * 重要的循环，说明，“每次循环遍历…”
#### 注释样式
 * 注释样式参考android源码
 * 代码以“段”来编写，注释也相应以“段”来注释
 
 
### 其他参考
[《Android Code Style》](https://source.android.com/source/code-style.html)
[《Java Programming Style Guidelines》] (http://geosoft.no/development/javastyle.html)
[《Google Java Style》] (https://google.github.io/styleguide/javaguide.html)
> 来自：[http://www.jianshu.com/p/e4229061fceb](http://www.jianshu.com/p/e4229061fceb)