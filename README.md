# MemoryOptimization
内存优化
    App运行内存限制，OOM导致app崩溃
    App性能：流畅性、响应速度、和用户体验

    一．Android的内存管理方式：
    1.Android系统内存分配和回收方式：
    A. 一个app通常就是一个进程对应一个虚拟机（adb shell进入安卓底层linux	   系统命令，ps查看系统里面进程的命令）
    B. GC只在Heap剩余空间不够时才发出垃圾回收
    C. GC触发时，所有的线程都会被暂停的

    2.App内存限制机制
    A.每个App内存奉陪的最大限制，虽不同设备而不同
    B.吃内存大户：图片

    3.切换应用时后台APP清理机制
    A.APP切换的LRU Cache（最近最少使用原则）
    B.onTrimMemory()回调方法	

    二．APP内存优化方法
    1.数据结构的优化：
    A. 频繁字符串用StringBuilder
    B. ArrayMap、SparseArray替代HaspMap
    C. 内存抖动 
    D. 再小的Class耗费0.5k
    E. HaspMap一个Entity需要额外占用32B

    2.对象复用：
      A.  复用系统自带的资源
    B.  ListView/GrideView的ConvertView复用
    C.  避免在onDraw方法里面对象的创建

    三．避免内存泄漏
    1. 由于代码瑕疵，导致这块内存，虽然停止不用了，但依然被其他东西引用着，使	   GC没法对它回收
    2. 内存泄漏会导致剩余可用的Heap越来越少，频繁触发GC
    尤其Activity泄漏
    3. 用Application Context而不是Activity Context（因为Activity会经常退出）
    注意Cursor对象是否关闭

    四．OOM问题优化
     1.OOM问题分析
    OOM的绝大部分发生在图片

     2.强引用、软引用（SoftReference）
    强引用：在其生命周期期间不会被回收的
    软引用：SoftReference<String> 如果内存不足，在其在其生命周期期间会被回收的

     3.优化OOm问题的方法
     A.  注意临时Bitmap对象的垃圾及时回收
     B.  避免Bitmap的浪费
     C.  Try catch某些内存分配的操作
     D.  加载Bitmap：缩放比例、解码格式、局部加载
