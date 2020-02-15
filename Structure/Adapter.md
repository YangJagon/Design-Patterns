# 适配者模式

在现实生活中，经常出现两个对象因接口不兼容而不能在一起工作的实例，这时需要第三者进行适配。如用计算机访问照相机的 SD 内存卡时需要一个读卡器等。

在软件设计中也可能出现：需要开发的具有某种业务功能的组件在现有的组件库中已经存在，但它们与当前系统的接口规范不兼容，如果重新开发这些组件成本又很高，这时用适配器模式能很好地解决这些问题。

适配者模式是指**将一个类的接口转换成客户希望的另外一个接口，使得原本由于接口不兼容而不能一起工作的那些类能一起工作**。

**组成：**

1. 目标（Target）接口：当前系统业务所期待的接口，它可以是抽象类或接口。
2. 适配者（Adaptee）类：它是被访问和适配的现存组件库中的组件接口。
3. 适配器（Adapter）类：它是一个转换器，通过继承或引用适配者的对象，把适配者接口转换成目标接口，让客户按目标接口的格式访问适配者。

**实现：**

适配器模式分为类结构型模式和对象结构型模式两种，前者通过继承适配者类实现，后者则通过引用适配者类来提供接口。因此前者类之间的耦合度比后者高，且要求程序员了解现有组件库中的相关组件的内部结构，所以应用相对较少些。

1. 类结构型模式：

   ```java
   // 目标接口（期待的接口）
   interface Target
   {
       public void request();
   }
   
   // 适配者（现存接口）
   class Adaptee
   {
       public void specificRequest()
       {       
           System.out.println("适配者中的业务代码被调用！");
       }
   }
   
   // 适配器类（转换器）
   class ClassAdapter extends Adaptee implements Target
   {
       public void request()
       {
           specificRequest();
       }
   }
   ```

2. 对象型模式

   ```java
   // 目标接口（期待的接口）
   interface Target
   {
       public void request();
   }
   
   // 适配器类
   class ObjectAdapter implements Target
   {
       private Adaptee adaptee; // 引用适配者类
       public ObjectAdapter(Adaptee adaptee)
       {
           this.adaptee=adaptee;
       }
       public void request()
       {
           adaptee.specificRequest(); // 调用相应的方法
       }
   }
   ```

   

