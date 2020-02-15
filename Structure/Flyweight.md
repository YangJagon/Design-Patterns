# 享元模式

在面向对象程序设计过程中，有时会面临要创建大量相同或相似对象实例的问题，如围棋和五子棋中的黑白棋子，图像中的坐标点或颜色等。这些对象有很多相似的地方，如果能把它们相同的部分提取出来共享，则能节省大量的系统资源，这就是享元模式的产生背景。

享元（Flyweight）模式，又称轻量级模式，其定义是**运用共享技术来有効地支持大量细粒度对象的复用**。它通过共享已经存在的又橡来大幅度减少需要创建的对象数量、避免大量相似类的开销，从而提高系统资源的利用率。

**组成：**

1. 抽象享元角色（Flyweight）：是所有的具体享元类的基类，为具体享元规范需要实现的公共接口，非享元的外部状态以参数的形式通过方法传入。
2. 具体享元（Concrete Flyweight）角色：实现抽象享元角色中所规定的接口。
3. 非享元（Unsharable Flyweight)角色：是不可以共享的外部状态，它以参数的形式注入具体享元的相关方法中。
4. 享元工厂（Flyweight Factory）角色：负责创建和管理享元角色。当客户对象请求一个享元对象时，享元工厂检査系统中是否存在符合要求的享元对象，如果存在则提供给客户；如果不存在的话，则创建一个新的享元对象。

**示例：**

假设我们需要许多不同位置且不同颜色的圆，考虑到颜色种类较少，可以对不同颜色的圆对象进行共享：

1. 抽象享元角色

   ```java
   public interface Shape {
       // 坐标x, y属于非享元角色，不可共享，以参数形式传入
   	void draw(int x, int y); 
   }
   ```

2. 具体享元角色

   ```java
   public class Circle implements Shape {
   	private String color;
   	public Circle(String color){
   		this.color = color;     
   	}
    
   	@Override
   	public void draw(int x, int y) {
   	System.out.println("A " + color + " circle in (" + x + ", " + y + ").");
   	}
   }
   ```

3. 享元工厂

   ```java
   public class ShapeFactory {
      private static final HashMap<String, Shape> circleMap = new HashMap<>();
    
      public static Shape getCircle(String color) {
         Circle circle = (Circle)circleMap.get(color);
    
         if(circle == null) {
            circle = new Circle(color);
            circleMap.put(color, circle);
            System.out.println("Creating circle of color : " + color);
         }
         return circle;
      }
   }
   ```

4. 客户访问

   ```java
   public class FlyweightPatternDemo {
      private static final String colors[] = 
         { "Red", "Green", "Blue", "White", "Black" };
      public static void main(String[] args) {
    
         for(int i=0; i < 20; ++i) {
            Circle circle = 
               (Circle)ShapeFactory.getCircle(getRandomColor());
            circle.draw(getRandomX(), getRandomY());
         }
      }
       
      private static String getRandomColor() {
         return colors[(int)(Math.random()*colors.length)];
      }
      private static int getRandomX() {
         return (int)(Math.random()*100 );
      }
      private static int getRandomY() {
         return (int)(Math.random()*100);
      }
   }
   ```

   

