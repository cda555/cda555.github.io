## 概述

*Thread.join()*方法

| 方法                                              | 说明                                                         |
| ------------------------------------------------- | ------------------------------------------------------------ |
| join()                                            | 线程等待另一个线程执行完。                                   |
| join(long millis) or join(long millis, int nanos) | 如果线程在给定的超时时间内没有终止，那么将会从超时方法中返回。 |

## 实现原理

```java

public class Thread implements Runnable{
    //...
    
    /**
 	 * Waits for this thread to die.
 	 * <p> An invocation of this method behaves in exactly the same way
	 * as the invocation
	 */
    public final void join() throws InterrupterdException{
        join(0);
    }
    
    public final synchronized void join(long millis) throws InterruptedException{
        long base = System.currentTimeMillis();
        long now = 0;
        
        if(millis < 0){
            throw new IllegalArgumentException("timeout value is negative");
        }
        
        if(millis == 0){
            while(isAlive()){//防止被误唤醒
                wait(0);
            }
        }else{
            while(isAlive()){
                long delay = millis - now; 
                if(delay <= 0){
                    break;
                }
                wait(delay);
                now = System.currentTimeMillis() - base;
            }
        }
        
    }
    
    //...
}
```









































































































