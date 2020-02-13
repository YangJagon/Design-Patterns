# 原型模式

在有些系统中，存在大量相同或相似对象的创建问题，如果用传统的构造函数来创建对象，会比较复杂且耗时耗资源，而用原型模式生成对象就很高效。原型模式就是==用一个已经创建的实例作为原型，通过复制该原型对象来创建一个和原型相同或相似的新对象==。

**实现：**

Java 中提供了对象的 clone 方法，但 Object 里默认的 clone 方法是 protect 的，无法被其它类访问。若我们需要使用原型模式，可以通过实现 Cloneable 接口来满足需求。

如下，我们只需实现 Coneable 接口并调用 super.clone 方法就能实现原型类了。但是 Object.clone 方法实现的是对象的**浅克隆**，若需**深克隆**，还需自行编写代码修改。

```java
public class Draft
{
    public static void main(String ...args) throws CloneNotSupportedException
    {
        TestClone t1 = new TestClone();
        TestClone t2 = t1.clone();
        out.println(t1 == t2);  // print: false
        out.println(t1.a == t2.a);  // print: true
    }
}

class TestClone implements Cloneable
{
    Integer a = 10;
    TestClone()
    { }

    @Override
    public TestClone clone() throws CloneNotSupportedException
    {
        return (TestClone)super.clone();
    }
}
```

