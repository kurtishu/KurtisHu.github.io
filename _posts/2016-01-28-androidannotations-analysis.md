---
layout: post
title: 图解Activity四种启动模式
author: kurtis.hu
categories:
  - Android
---

#AndroidAnnotions 源码解析
AndroidAnnotions 官方的给出的定义是
```
AndroidAnnotations is an Open Source framework that speeds up Android development. It takes care of the plumbing, and lets you concentrate on what's really important. By simplifying your code, it facilitates its maintenance.
```
AndroidAnnotations 使用标准的Java注解处理工具自动添加一个额外的编译步骤生成的源代码(会生成一个加了"_"的同名类)，在新生产的源文件中实现View的实例化、Class的注入等工作，以达到减轻开发者工作量的目的。
####关于 APT(Annotion Processing Tool)
APT 是java 注解处理工具，它的作用就是在源代码中找到并处理Annotation Processors(Annnotation Processors 简单说就是实现了AnnotationProcessor interface 的类)，更多关于APT的内容请参考：[oracle apt doc](http://docs.oracle.com/javase/1.5.0/docs/guide/apt/GettingStarted.html) 

#### Android Stuio使用AndroidAnnotation
在Android Stuio使用AndroidAnnotion，在网上有具体的配置步骤，引入这个框架会涉及到两个jar包
```
 dependencies {
    apt "org.androidannotations:androidannotations:$AAVersion"
    compile "org.androidannotations:androidannotations-api:$AAVersion"
}
```
其中上面一个是AndroidAnnotations的处理核心包，包含了一个 Annotation Processor，另一个则是暴露出来的所有Annotions，例如@EActivity，@EBean等, API这个包没什么好说的，下面主要讲下androidannotations.jar。

#### 解密androidannotations.jar
解压androidannotations.jar文件，在META-INF\services\下有个javax.annotation.processing.Processor，该文件会‘告诉’apt来处理这个文件指定的Processor。这个文件所指定的Processor是org.androidannotations.AndroidAnnotationProcessor。所以重点关注AndroidAnnotationProcessor这个类。
###org.androidannotations.AndroidAnnotationProcessor

```java
public class AndroidAnnotationProcessor extends AbstractProcessor {

    @Override
    public boolean process(Set<? extends TypeElement> annotations, RoundEnvironment roundEnv) {
      ...
    }
    
    @Override
    public SourceVersion getSupportedSourceVersion() {
        return SourceVersion.latestSupported();
    }
    
    @Override
    public Set<String> getSupportedAnnotationTypes() {
      ...
    }

```
从代码可以看到 AndroidAnnotationProcessor继承至AbstractProcessor需要实现三个方法, process是处理Annotation的核心方法，Annatation解析s所需要的java
的版本好，一般使用lastestSupported(最新的java版本), getSupportedAnnotationTypes 返回需要解析的Annotation的Class集合。这里重点讲下process方法
###process方法
先贴出核心代码
```java
    @Override
    public boolean process(Set<? extends TypeElement> annotations, RoundEnvironment roundEnv) {
    ...
	   try {
            // *检查API的版本和处理核心包的版本是否匹配
			checkApiAndCoreVersions();
            
            // *处理Annotations的核心方法
			processThrowing(annotations, roundEnv);
            
		} catch (ProcessingException e) {
			handleException(annotations, roundEnv, e);
		} catch (Exception e) {
			handleException(annotations, roundEnv, new ProcessingException(e, null));
		}
    ...
		return true;
	}
```
重点关注processThrowing方法，该方法主要做了三件事，一是Validate Annotation，二是解析Annotations，三是生产具体的class
```java
private void processThrowing(Set<? extends TypeElement> annotations, RoundEnvironment roundEnv) throws ProcessingException, Exception {
    ...
		IRClass rClass = rClassOption.get();

		AndroidSystemServices androidSystemServices = new AndroidSystemServices();

		annotationHandlers.setAndroidEnvironment(rClass, androidSystemServices, androidManifest);

        // * Validate Annotations
		AnnotationElements validatedModel = validateAnnotations(extractedModel);

        // * 处理Annotations，返回ProcessResult结果
		ModelProcessor.ProcessResult processResult = processAnnotations(validatedModel);

        // * 根据解析到的Annotations 生成相应的类文件
		generateSources(processResult);
	}

```

####更多
关于AndroidAnnotation框架如何去Validate、解析，以及生成类的过程没有具体分析，留到以后再完善。