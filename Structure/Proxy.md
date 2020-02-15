# 代理模式

在有些情况下，一个客户不能或者不想直接访问另一个对象，这时需要找一个中介帮忙完成某项任务，这个中介就是代理对象。例如，购买火车票不一定要去火车站买，可以通过专门的网站、软件购买。

在软件设计中，使用代理模式的例子也很多，例如，要访问的远程对象比较大（如视频或大图像等），其下载要花很多时间。还有因为安全原因需要屏蔽客户端直接访问真实对象，如某单位的内部数据库等。代理模式将客户端与目标对象分离，不仅能起到保护目标对象的作用，同时在一定程度上也降低了系统的耦合度。

代理模式的定义：**由于某些原因需要控制访问对象对目标对象的访问时，即访问对象不适合或者不能直接引用目标对象，可以创建代理对象作为访问对象和目标对象之间的中介**。

**组成：**

1. 抽象主题（Subject）类：通过接口或抽象类声明真实主题和代理对象实现的业务方法。
2. 真实主题（Real Subject）类：实现了抽象主题中的具体业务，是代理对象所代表的真实对象，是最终要引用的对象。
3. 代理（Proxy）类：提供了与真实主题相同的接口，其内部含有对真实主题的引用，它可以访问、控制或扩展真实主题的功能。

**实现：**

1. 抽象主题

   ```java
   interface Subject
   {
   	void request();
   }
   ```

2. 真实主题

   ```java
   class RealSubject implements Subject
   {
       public void request()
       {
           System.out.println("这里是被访问的真实对象");
       }
   }
   ```

3. 代理

   ```java
   class Proxy implements Subject // 实现同一公开接口，方便客户访问
   {
       private RealSubject realSubject;
       public void request()
       {
           if (realSubject==null)
           {
               realSubject=new RealSubject();
           }
           beforeRequest();
           realSubject.request(); // 代理调用真实对象的接口
           afterRequest();
       }
       public void beforeRequest(){...}
       public void afterRequest(){...}
   }
   ```

4. 用户使用

   ```java
   public class Client
   {
       public void main(String ...args)
       {
           Proxy proxy = new Proxy();
           proxy.request();
       }
   }
   ```

   