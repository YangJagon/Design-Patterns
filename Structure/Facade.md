# 外观模式

在现实生活中，常常存在办事较复杂的例子，如办房产证或注册一家公司，有时要同多个部门联系，这时要是有一个综合部门能解决一切手续问题就好了。软件设计也是这样，当一个系统的功能越来越强，子系统会越来越多，客户对系统的访问也变得越来越复杂。所以有必要为多个子系统提供一个统一的接口，从而降低系统的耦合度，这就是外观模式的目标。

外观模式：**一种通过为多个复杂的子系统提供一个一致的接口，而使这些子系统更加容易被访问的模式**。该模式对外有一个统一接口，外部应用程序不用关心内部子系统的具体的细节，这样会大大降低应用程序的复杂度，提高了程序的可维护性。

**实现：**

```java
public interface Shape {
   void draw();
}

// 对应的两个子系统
public class Rectangle implements Shape {
   @Override
   public void draw() {
      System.out.println("Rectangle::draw()");
   }
}
public class Square implements Shape {
   @Override
   public void draw() {
      System.out.println("Square::draw()");
   }
}

// 统一接口
public class ShapeMaker {
   private Shape rectangle;
   private Shape square;
 
   public ShapeMaker() {
      rectangle = new Rectangle();
      square = new Square();
   }
    
   public void drawRectangle(){
      rectangle.draw();
   }
   public void drawSquare(){
      square.draw();
   }
}
```



