
## Concurrency - OS can execute many processes at the same time.
 

| Process | Thread |
| ---- | ---- |
|  is an instance of a program or application. Each processor has multiple core to run processes or threads so application must be multithreaded to utilise full potential of processor. | is a sequence of instructions, practically that thing that executes our code. Each process has one thread called main thread but can create many thread to run many tasks concurrently  e.g web server serving many clients at the same time.(Multithreading) |


```java
System.out.println(Thread.activeCount());  
System.out.println(Runtime.getRuntime().availableProcessors());
```

## Starting a thread

ThreadDemo.java
```java  
public class ThreadDemo {  
  
public static void show() {  
  
System.out.println(Thread.currentThread().getName());  
  
for(int i=0; i<10; i++) {  
Thread thread = new Thread(new DownloadFileTask());  
thread.start();  
} 
}  
}
```

DownloadFileTask.java
```java
public class DownloadFileTask implements Runnable{  
  
@Override  
public void run() {  
System.out.println("Downloading a file " + Thread.currentThread().getName());  
}  
}
```

## Pausing a thread
```java
try {  
Thread.sleep(5000);  
} catch (InterruptedException e) {  
throw new RuntimeException(e);  
}
```


jvm - thread scheduler - task is to decide what thread to run and for what time when there is more tasks than available threads.

## Joining a thread
```java
Thread thread = new Thread(new DownloadFileTask());  
thread.start();  
try {  
thread.join();  
} catch (InterruptedException e) {  
throw new RuntimeException(e);  
}  
System.out.println("File is ready to be scanned.");
```

## Interrupting a Thread

ThreadDemo.java
```java
public class ThreadDemo {  
  
public static void show() {  
Thread thread = new Thread(new DownloadFileTask());  
thread.start();  
  
try {  
Thread.sleep(1000);  
} catch (InterruptedException e) {  
throw new RuntimeException(e);  
}  
thread.interrupt();  
}  
}
```

DownloadFileTask.java

```java
public class DownloadFileTask implements Runnable{  
  
@Override  
public void run() {  
System.out.println("Downloading a file " + Thread.currentThread().getName());  
for (int i=0; i<Integer.MAX_VALUE; i++) {  
if(Thread.currentThread().isInterrupted()) return;  
System.out.println("Downloading byte " + i);  
}  
  
System.out.println("Download complete " + Thread.currentThread().getName());  
}  
}
```


Sometimes, our threads need to access and modify shared resources e.g for each download thread it have to access totalBytes to share how many bytes it has dowloaded.

Issues
1.  Multiple threads try to modify same data at same time. ( RACE Condition) multiple threads racing or competing to modify same data.
2. one thread changes not visible to other threads. ( Visibility problem)

Thread-safe Code

## Race Condition

ThreadDemo.java
```java
package com.javaadvanced.thread;  
  
import java.util.ArrayList;  
import java.util.List;  
  
public class ThreadDemo {  
  
public static void show() {  
DownloadStatus status = new DownloadStatus();  
  
List<Thread> threads = new ArrayList<>();  
for(int i=0; i<10; i++) {  
Thread thread = new Thread(new DownloadFileTask(status));  
thread.start();  
threads.add(thread);  
}  
for(Thread thread: threads) {  
try {  
thread.join();  
} catch (InterruptedException e) {  
e.printStackTrace();  
}  
}  
  
System.out.println(status.getTotalBytes());  
  
}  
}
```

DownloadStatus.java
```java
package com.javaadvanced.thread;  
  
public class DownloadStatus {  
private int totalBytes;  
  
public int getTotalBytes() {  
return totalBytes;  
}  
  
public void incrementTotalBytes() {  
totalBytes++;  
}  
}
```

DownloadFIleTask.java
```java
package com.javaadvanced.thread;  
  
public class DownloadFileTask implements Runnable{  
  
private final DownloadStatus status;  
  
public DownloadFileTask(DownloadStatus status) {  
this.status = status;  
}  
  
@Override  
public void run() {  
System.out.println("Downloading a file " + Thread.currentThread().getName());  
for (int i=0; i<10000; i++) {  
if(Thread.currentThread().isInterrupted()) return;  
status.incrementTotalBytes();  
}  
  
System.out.println("Download complete " + Thread.currentThread().getName());  
}  
}
```

## Strategies for thread safety

- Confinement - each have its own data 
- Immutable objects 
- Synchronization - do by using locks only one thread at a time can execute that part. Implementing sychronization can be challenging and problems like deadlock.
- Atomic objects
- Partitioning -data into segments that can access data concurrently  

## Lock
```java  
import java.util.concurrent.locks.Lock;  
import java.util.concurrent.locks.ReentrantLock;  
  
public class DownloadStatus {  
private int totalBytes;  
private Lock lock = new ReentrantLock();  
  
public int getTotalBytes() {  
return totalBytes;  
}  
  
public void incrementTotalBytes() {  
lock.lock();  
try {  
totalBytes++;  
}  
finally {  
lock.unlock();  
} // inside finally block to unlock in case of exception and prevent deadlock.  
  
}  
}
```


- the synchronized keyword


volatile - solve visibility problem by not relying data in cache and always checking main memory.
## Thread signalling with wait() and notify()

ThreadDemo.java
```java
public class ThreadDemo {  
public static void show() {  
DownloadStatus status = new DownloadStatus();  
var thread1 = new Thread(new DownloadFileTask(status));  
var thread2= new Thread(() -> {  
while(!status.isDone()) {  
synchronized (status) {  
try {  
status.wait(); // go to sleep until other thread wakes it up  
} catch (InterruptedException e) {  
throw new RuntimeException(e);  
}  
}  
}  
System.out.println(status.getTotalBytes());  
});  
thread1.start();  
thread2.start();  
  
}  
}
```

 DownloadFileTask.java
```java
 @Override  
public void run() {  
System.out.println("Downloading a file " + Thread.currentThread().getName());  
for (int i=0; i<100000; i++) {  
if(Thread.currentThread().isInterrupted()) return;  
status.incrementTotalBytes();  
}  
status.done();  
synchronized (status) {  
status.notifyAll(); // notify second thread to wake up  
}  
System.out.println("Download complete " + Thread.currentThread().getName());  
}
```

## Atomic objects

Works on compare and swap technique supported by most of CPUs.
Compare the current value with expected if not equal swap them.



```java

private AtomicInteger totalBytes = new AtomicInteger();  
  
public int getTotalBytes() {  
return totalBytes.get();  
}  

public void incrementTotalBytes() {  
totalBytes.incrementAndGet();  
}  
```

## Adders

Faster than atomic objects.

```java
private LongAdder totalBytes = new LongAdder();  
  
public int getTotalBytes() {  
return totalBytes.intValue();  
}  
  
public void incrementTotalBytes() {  
totalBytes.increment();  
}
```

## Synchronized Collections

```java
Collection<Integer> collection = Collections.synchronizedCollection(new ArrayList<>());
```

## Concurrent Collections
```java
Map<Integer, String> map = new ConcurrentHashMap<>();
```

