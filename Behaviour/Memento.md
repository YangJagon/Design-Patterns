# 备忘录模式

每个人都有犯错误的时候，都希望有种“后悔药”能弥补自己的过失，让自己重新开始，但现实是残酷的。在计算机应用中，客户同样会常常犯错误，我们却可以、也应该提供“后悔药”给他们，如 Word、记事本等软件在编辑时按 Ctrl+Z 组合键时能撤销当前操作、在 IE 中的后退键等等。这个功能可以由“备忘录模式”来实现。

备忘录（Memento）模式的定义：**在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态，以便以后当需要时能将该对象恢复到原先保存的状态**。该模式又叫快照模式。

**组成：**

1. 发起人（Originator）角色：是记录当前内部状态信息的需求的发起人，提供创建备忘录和恢复备忘录数据的功能，它可以访问备忘录里的所有信息。
2. 备忘录（Memento）角色：存储发起人一个时刻的内部状态的对象，在需要的时候提供这些内部状态给发起人。
3. 管理者（Caretaker）角色：对众多备忘录对象进行管理，提供保存与获取备忘录对象的功能，但其不能对备忘录对象的内容进行访问与修改。

**实现：**

1. 备忘录类

   ```java
   public class Memento {
      private String state;
    
      public Memento(String state){
         this.state = state;
      }
    
      public String getState(){
         return state;
      }  
   }
   ```

2. 发起人类

   ```java
   public class Originator {
      private String state;
    
      public void setState(String state){
         this.state = state;
      }
    
      public String getState(){
         return state;
      }
    
      public Memento saveStateToMemento(){
         return new Memento(state);
      }
    
      public void getStateFromMemento(Memento Memento){
         state = Memento.getState();
      }
   }
   ```

3. 管理者类

   ```java
   public class CareTaker {
      private List<Memento> mementoList = new ArrayList<Memento>();
    
      public void add(Memento state){
         mementoList.add(state);
      }
    
      public Memento get(int index){
         return mementoList.get(index);
      }
   }
   ```

4. 测试

   ```java
   public class MementoPatternDemo {
      public static void main(String[] args) {
         Originator originator = new Originator();
         CareTaker careTaker = new CareTaker();
         originator.setState("State #1");
         originator.setState("State #2");
         careTaker.add(originator.saveStateToMemento());
         originator.setState("State #3");
         careTaker.add(originator.saveStateToMemento());
         originator.setState("State #4");
    
         System.out.println("Current State: " + originator.getState());    
         originator.getStateFromMemento(careTaker.get(0));
         System.out.println("First saved State: " + originator.getState());
         originator.getStateFromMemento(careTaker.get(1));
         System.out.println("Second saved State: " + originator.getState());
      }
   }
   
   // 输出：
   // Current State: State #4
   // First saved State: State #2
   // Second saved State: State #3
   ```

   

   

   