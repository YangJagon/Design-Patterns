# 单例模式

在有些系统中，为了节省内存资源、保证数据内容的一致性，对某些类要求只能创建一个实例，这就是所谓的单例模式。如 Windows 中只能打开一个任务管理器。其定义是**一个类只有一个实例，且该类能自行创建这个实例的一种模式**。

单例模式有如下特点：

1. 单例类只有一个实例对象
2. 该实例对象由单例类自行创建
3. 单例类对外提供一个访问该实例对象的全局接口

**实现：**

1. **懒汉式**

   该模式在类加载时没有生成实例对象，直到第一次调用 getInstance 接口时才创建单例。

   ```java
   class LazySingleton
   {	
       // volatile 和 synchronized 关键字保证多线程时同步
       // static 保证全局只有一个统一的实例对象
       private volatile static LazySingleton instance = null;
       private LazySingleton(){...};
       public synchronized static LazySingleton getInstance()
       {
           if(instance == null)
               instance = new LazySingleton();
           return instance;
       }
   }
   ```

2. **饿汉式**

   该模式在类加载时就创建一个实例对象，保证在调用 getInstance 方法之前该单例就已经存在。

   ```java
   class HungrySingleton
   {
       private static final HungrySingleton instance = new HungrySingleton();
       private HungrySingleton(){...};
       public static HungrySingleton getInstance(){ return instance; }
   }
   ```

   