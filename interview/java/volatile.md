## volatile

###  volatile的原理

 总线（MESI缓存一致性协议）：当有store会开启一个监听机制（CPU总线嗅探机制）导致失效

（1）Lock前缀指令会引起处理器缓存会写到内存

（2）一个处理器的缓存会写到内存会导致其他处理器的缓存无效



```
private volatile x；
转为汇编代码之后
·····lock ···；
```

注意点：volatile只要保证线程可见性，而不保证原子性

ex：

```java
public class Test{
    public volatile static int count =0;
    public static void main(String[] args){
        for(int i=0;i<10;i++){
            new Thread(
            	new Runnable(){
                    public void run(){
                        try{
                            Thread.sleep(1);
                        }catch(Exception e){}
                        for(int j=0;j<100;j++){
                            count++;
                        }
                    }
                }
            ).start();
        }
        try{
            Thread.sleep(2000);
        }catch(Exception e){}
        System.out.print("count="+count);
    }
}
打印结果<=count
```



原因：字节码层面

```jav 

```



