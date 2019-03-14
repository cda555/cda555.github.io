## 简述

*ThreadLocal*起源于*JDK 1.2*。

*ThreadLocal*,即线程变量，是一个以*ThreadLocal*对象为键、任意对象为值的存储结构。这个结构被附带在线程上，也就是一个线程可以根据一个*ThreadLocal*对象查询到绑定在这个线程上的值。

## 使用

```java
public class ThreadLocalDemo{
    // 第一次get()方法调用会进行初始化（如果set方法没有调用），每个线程只会调用一次
    private static final ThreadLocal<Long> TIME_THREADLOCAL = new ThreadLocal<Long>(){
        protected Long initialValue(){
            return System.currentTimeMillis();
        }
    }
    
}
```



## 原理

