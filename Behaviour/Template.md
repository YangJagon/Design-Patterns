# 模板方法模型

在面向对象程序设计过程中，程序员常常会遇到这种情况：设计一个系统时知道了算法所需的关键步骤，而且确定了这些步骤的执行顺序，但某些步骤的具体实现还未知，或者说某些步骤的实现与具体的环境相关。

例如，一个人每天会起床、吃饭、做事、睡觉等，其中“做事”的内容每天可能不同。我们把这些规定了流程或格式的实例定义成模板，允许使用者根据自己的需求去更新它，像简历模板、论文模板等。

模板方法（Template Method）模式的定义：**定义一个操作中的算法骨架，而将算法的一些步骤延迟到子类中，使得子类可以不改变该算法结构的情况下重定义该算法的某些特定步骤**。

**组成：**

1. 抽象类：负责给出一个算法的轮廓和骨架。它由一个模板方法和若干个基本方法构成：
   - 模板方法：定义了算法的骨架，按某种顺序调用其包含的基本方法。
   - 基本方法：是整个算法中的一个步骤，包含以下几种类型：
     - 抽象方法：在抽象类中申明，由具体子类实现。
     - 具体方法：在抽象类中已经实现，在具体子类中可以继承或重写它。
     - 钩子方法：在抽象类中已经实现，包括用于判断的逻辑方法和需要子类重写的空方法两种。
2. 具体子类：实现抽象类中所定义的抽象方法和钩子方法，它们是一个顶级逻辑的一个组成步骤。

**示例：**

1. 抽象类

   ```java
   public abstract class Game {
      // 基本方法
      abstract void initialize();
      abstract void startPlay();
      abstract void endPlay();
    
      // 模板方法
      public final void play(){
         // 初始化游戏
         initialize();
         // 开始游戏
         startPlay();
         // 结束游戏
         endPlay();
      }
   }
   ```

2. 具体类

   ```java
   public class Cricket extends Game {
      // 棒球游戏
      @Override
      void endPlay() {
         System.out.println("Cricket Game Finished!");
      }
      @Override
      void initialize() {
         System.out.println("Cricket Game Initialized! Start playing.");
      }
      @Override
      void startPlay() {
         System.out.println("Cricket Game Started. Enjoy the game!");
      }
   }
   ```

   ```java
   public class Football extends Game {
      // 足球游戏
      @Override
      void endPlay() {
         System.out.println("Football Game Finished!");
      }
      @Override
      void initialize() {
         System.out.println("Football Game Initialized! Start playing.");
      }
      @Override
      void startPlay() {
         System.out.println("Football Game Started. Enjoy the game!");
      }
   }
   ```

3. 测试

   ```java
   public class Client{
      public static void main(String[] args) {
      	  // 调用棒球游戏
         Game game = new Cricket();
         game.play();
         
         // 调用足球游戏
         game = new Football();
         game.play();      
      }
   }
   ```

   