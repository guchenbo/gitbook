# 线程的wait()和notify()、notifyAll()

Object.wait()方法是让当前线程释放同步锁，并且进入等待阻塞状态；

Object.notify()和Object.notifyAll()方法是唤醒与当前对象关联的线程，获得同步锁使之进入就绪状态，notify()唤醒一个，notifyAll()是唤醒所有。



`jdk 中wait()方法的说明（其中wait()有几个重载，wait(long timeout)，wait()就是调用wait(0)的，表示永不超时）`

**使得当前线程等待，直到其他线程调用当前对象的notify()或者notifyAll()方法唤醒它。当前线程必须持有当前对象的同步锁**

调用这三个方法由几个共同点：

**1、调用方法的当前线程必须持有当前对象（该方法的所有者）的同步锁**

**2、调用这些方法的当前线程都和同一个同步锁关联**

不同点：

**1、wait()方法，使当前线程等待，并释放同步锁**

**2、notify()、notifyAll()方法，唤醒wait()，不会释放同步锁**

看几个例子：

只测试wait()方法，notify()一样的

1、当前线程没有获取同步锁

```java
public static void main(String[] args) {
    TestWait testWait = new TestWait();
    TestWait testWait2 = new TestWait();
    try {
        //synchronized (testWait) {
            testWait.wait(300);
        
        //}
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}    
```

运行结果：

wait()会报错

2、当前线程获取了另一个同步锁

```java
public static void main(String[] args) {
    TestWait testWait = new TestWait();
    TestWait testWait2 = new TestWait();
    try {
        synchronized (testWait2) {
            testWait.wait(300);
        }
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}
```

运行结果：

wait()会报错

3、

```java
public static void main(String[] args) {
    TestWait testWait = new TestWait();
    TestWait testWait2 = new TestWait();
    try {
        synchronized (testWait) {
            testWait.wait(300);
        }
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}
```

运行结果

不会报错