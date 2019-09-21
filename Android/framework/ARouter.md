## ARouter

阿里巴巴出品

 一个用于帮助 Android App 进行组件化改造的框架 —— 支持模块间的路由、通信、解耦

具体功能介绍请参考github仓库[网址](https://github.com/alibaba/ARouter)

阿里官方 [路由框架的由来与设计](https://yq.aliyun.com/articles/71687?t=t1)

**原生的路由方案存在的问题**
首先谈一谈原生的路由方案存在的问题以及为什么需要路由框架。我们所使用的原生路由方案一般是通过显式intent和隐式intent两种方式实现的，而在显式intent的情况下，因为会存在直接的类依赖的问题，导致耦合非常严重；而在隐式intent情况下，则会出现规则集中式管理，导致协作变得非常困难。而且一般而言配置规则都是在Manifest中的，这就导致了扩展性较差。除此之外，使用原生的路由方案会出现跳转过程无法控制的问题，因为一旦使用了StartActivity()就无法插手其中任何环节了，只能交给系统管理，这就导致了在跳转失败的情况下无法降级，而是会直接抛出运营级的异常。

#### How to use？

1. Configuration(配置)

```java
android {
    defaultConfig {
        ...
        javaCompileOptions {
            annotationProcessorOptions {
                arguments = [AROUTER_MODULE_NAME: project.getName()]
            }
        }
    }
}

dependencies {
    // Replace with the latest version
    compile 'com.alibaba:arouter-api:?'
    annotationProcessor 'com.alibaba:arouter-compiler:?'
    ...
}
// Old version of gradle plugin (< 2.2), You can use apt plugin, look at 'Other#1'
// Kotlin configuration reference 'Other#2'
```

2 . initialize the SDK(初始化SDK)

```java 
if (isDebug()) {           // These two lines must be written before init, otherwise these configurations will be invalid in the init process
    ARouter.openLog();     // Print log
    ARouter.openDebug();   // Turn on debugging mode (If you are running in InstantRun mode, you must turn on debug mode! Online version needs to be closed, otherwise there is a security risk)
}
ARouter.init(mApplication); // As early as possible, it is recommended to initialize in the Application
```

3. Add annotations(添加注解)

```
// Add annotations on pages that support routing (required)
// The path here needs to pay attention to need at least two levels : /xx/xx
@Route(path = "/test/activity")
public class YourActivity extend Activity {
    ...
}
```

4. Initiate the routing(跳转)

```
ARouter.getInstance().build("/test/activity").navigation();
```

5. Add confusing rules (If Proguard is turn on)

```java
-keep public class com.alibaba.android.arouter.routes.**{*;}
-keep public class com.alibaba.android.arouter.facade.**{*;}
-keep class * implements com.alibaba.android.arouter.facade.template.ISyringe{*;}

# If you use the byType method to obtain Service, add the following rules to protect the interface:
-keep interface * implements com.alibaba.android.arouter.facade.template.IProvider

# If single-type injection is used, that is, no interface is defined to implement IProvider, the following rules need to be added to protect the implementation
# -keep class * implements com.alibaba.android.arouter.facade.template.IProvider
```

### 源码分析

从入口切入

```java
ARouter.init(mApplication);
```

