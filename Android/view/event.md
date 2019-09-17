## Android 事件分发机制

### 概念

(1)用户通过屏幕与手机交互时，每一次点击、长按、移动等都为一个事件

(2)事件分发机制：某一个事件从屏幕传递各个View，由View来使用这一事件（消费事件）或者忽略这一事件（不消费事件），这整个过程的控制

### 事件类型

+ 按下（ACTION_DOWN）
+ 移动（ACTION_MOVE）
+ 抬起（ACTION_UP）
+ 取消（ACTION_CANCEL）

### 传递层级

Activity -> Window -> DecorView ->ViewGroup ->View

**事件传递犹如领导层分发任务给下级，一级一级分发，谁接了这个这个任务就代表由他掌管，然后做完反馈给上级**

### 主要过程

+ Activity的事件分发
+ ViewGroup的事件分发
+ View的事件分发

![图片](https://github.com/chenxiaowu018/Android-and-Java-Note/blob/master/image/event.png)

