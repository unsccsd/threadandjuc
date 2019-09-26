### 什么是线程安全???

    当多个线程访问某个方法时，不管你通过怎样的调用方式或者说这些线程如何交替的执行，
    我们在主程序中不需要去做任何的同步，都不需要进行额外的处理,这个类的结果行为都是我们设想的正确行为
    那么我们就可以说这个类时线程安全的
    
### 一共有几类线程安全的问题???

   ![整体流程](https://raw.githubusercontent.com/qiurunze123/imageall/master/threadsafe001.png)
   
   
   1.运行结果错误
   
   com.geekagain.threadsafe.ThreadSafeError1 index++  会导致运行结果错误
   
   属于read-modify-write ++ 操作不具备原子性 
   
   2.死锁活锁等问题
   
   两个或多个线程相互等待对方释放锁，则会出现死锁现象
   
   如果在持有锁的情况下调用了某个外部方法，那么就需要警惕死锁
   
   com.geekagain.threadsafe.ThreadSafeError4
   
   3.发布逸出问题 
   
   com.geekagain.threadsafe
   
   ![整体流程](https://raw.githubusercontent.com/qiurunze123/imageall/master/threadsafe002.png)

   **4.各种需要考虑线程的安全情况**
   
   
   **多线程安全问题原因是在cpu执行多线程时，在执行的过程中可能随时切换到其他的线程上执行**
   
   1.访问共享资源变量 会有并发危险 共享缓存 共享实例 数据库等
   
   2.所有依赖时序的问题 即使每一步是安全的的 是存在并发的问题
   
   3.不同数据之间存在绑定关系 ip和端口号
   
   4.尽量避免 如果没有声明自己是安全的 那么大概率会存在并发问题  example -- hashMap
   
   
### 5.为什么会有线程性能问题
   
   由于线程需要协作所以引起调度  当你线程的数量大于cpu的数量的时候系统就会进行分配与调度
   
   1.调度就会引起上下文切换
   
   2.什么是上线文?
   
   操作系统的核心在CPU上对于进程进行以下的活动 挂起一个线程将这个进程在CPU上对于进程包括线程进行以下活动
   
   ① 挂起一个线程 将这个进程在CPU的中的状态存储在内存的某处 
   
   ② 在内存中检索下一个进程 的上下文并在cpu的寄存器恢复
   
   ③ 跳到程序计数器所指的位置 恢复该进程
   
### 6.何时会导致密集的上下文切换
 
 频繁竞争锁 或者 IO读写阻塞 