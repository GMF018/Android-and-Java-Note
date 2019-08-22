### Databinding 错误排查

排查错误的方式:
 在Android Studio 的terminal 里运行

> ./gradlew clean assembleDebug

或者

> ./gradlew compileDebugJavaWithJavac

因为DataBinding是编译生成代码的，很多错误都是xml中表达式写的有问题导致的，所以运行以上命令容易在terminal中打印出具体错误的信息。这些命令对于需要编译生成代码的框架排查错误十分有用，比如Dagger2

