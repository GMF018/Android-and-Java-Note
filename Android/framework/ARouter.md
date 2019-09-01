## ARouter

阿里巴巴出品

 一个用于帮助 Android App 进行组件化改造的框架 —— 支持模块间的路由、通信、解耦

具体功能介绍请参考github仓库[网址](https://github.com/alibaba/ARouter)

阿里官方 [路由框架的由来与设计](https://yq.aliyun.com/articles/71687?t=t1)

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

