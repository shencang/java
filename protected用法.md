protected的使用范围
类NewObject中有protected修饰的方法或者属性，则：

同一个包中：

可在同一个包里的子类中实例化NewObject类获得对象，然后可用该对象访问protected修饰的方法或者属性，即.操作访问。
可在同一个包里的非子类中实例化NewObject类获得对象，然后可用该对象访问protected修饰的方法或者属性。
可在同一个包里的非子类中实例化NewObject类的子类（该子类和NewObject类在同一个包中）获得对象，然后可用该对象访问protected修饰的方法或者属性。
可在同一个包里的NewObject类的子类中调用NewObject类中protected修饰的方法或者属性，即protected修饰的方法和属性可被同一个包中的子类继承。
非同一个包中：

可在非同一个包里的子类中实例化NewObject类获得对象，但无法用该对象问protected修饰的方法或者属性。
可在非同一个包里的非子类中实例化NewObject类获得对象，但无法用该对象问protected修饰的方法或者属性。
可在非同一个包里的非子类中实例化NewObject类的子类（该子类和NewObject类不在同一个包中）获得对象，但无法用该对象问protected修饰的方法或者属性。
可在非同一个包里的NewObject类的子类中调用NewObject类中protected修饰的方法或者属性，即protected修饰的方法和属性可被不同一个包中的子类继承。
```java
package 1：

BaseClass:


package package_1;
// 相当于NewObject类
public class BaseClass {
    // protected方法
    protected void protectedMethod() {
        System.out.println("This is BaseClass");
    }
 
}
```
SubClass:
```java
package package_1;
 
public class SubClass extends BaseClass {
}
MainClass:

package package_1;
 
public class MainClass {
    public static void main(String[] args) {
        BaseClass b1 = new BaseClass();
        SubClass s1 = new SubClass();
        b1.protectedMethod(); // 父类的protected方法可在同一个包中的其它类中被访问
        s1.protectedMethod(); // 子类中继承了父类的protected方法
    }
}
```
package 2：

SubClass:
```java
package package_2;
 
import package_1.BaseClass;
// 继承了不在同一个包中的父类 BaseClass
public class SubClass extends BaseClass {
    public void testMesthod(){
        BaseClass b1 = new BaseClass();
        b1.protectedMethod(); // 编译器报错。父类的protected方法不可以在不同一个包中的子类中被访问
        this.protectedMethod(); // 子类继承了父类protected方法
    }
}
```
MainClass:
```java

package package_2;
 
import package_1.*;
 
public class MainClass {
    public static void main(String[] args) {
        BaseClass b1 = new BaseClass();
        b1.protectedMethod(); // 编译器报错。父类的protected方法不可以在不同一个包中的其它类中被访问
        SubClass s1 = new SubClass();
        s1.protectedMethod(); // 编译器报错。子类的protected方法不可以在不同一个包中的其它类中被访问
    }
}
```
