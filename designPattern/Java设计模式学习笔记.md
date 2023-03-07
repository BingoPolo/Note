# Java设计模式学习笔记

前言：参考菜鸟教程，菜鸟教程地址：https://www.runoob.com/design-pattern/factory-pattern.html

## 创建型模式

### 一、简单工厂模式

#### 1、个人理解：

1)  **不同对象** 的 **同一行为**的实现。

2)  通过抽象工厂模式反过来思考什么是**同一行为**，**同一行为**不是单只一个行为，其实是一组行为，用来描述同一个对象的不同变现。比如下列代码。在shape接口中完全可以再定一个接口 void angleSum(); 内角和函数。每一个形状拥有自己的内角和。

#### 2、代码实现：

同一行为：

```java
public interface Shape {
   void draw();
}
```

不同对象：

```java
public class Rectangle implements Shape {
 
   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}
```



```java
public class Square implements Shape {
 
   @Override
   public void draw() {
      System.out.println("Inside Square::draw() method.");
   }
}
```



```java
public class Circle implements Shape {
 
   @Override
   public void draw() {
      System.out.println("Inside Circle::draw() method.");
   }
}
```

工厂根据类型返回不同值：

```java
public class ShapeFactory {
    
   //使用 getShape 方法获取形状类型的对象
   public Shape getShape(String shapeType){
      if(shapeType == null){
         return null;
      }        
      if(shapeType.equalsIgnoreCase("CIRCLE")){
         return new Circle();
      } else if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();
      } else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }
      return null;
   }
}
```

工厂类的使用：

```
public class FactoryPatternDemo {
 
   public static void main(String[] args) {
      ShapeFactory shapeFactory = new ShapeFactory();
 
      //获取 Circle 的对象，并调用它的 draw 方法
      Shape shape1 = shapeFactory.getShape("CIRCLE");
 
      //调用 Circle 的 draw 方法
      shape1.draw();
 
      //获取 Rectangle 的对象，并调用它的 draw 方法
      Shape shape2 = shapeFactory.getShape("RECTANGLE");
 
      //调用 Rectangle 的 draw 方法
      shape2.draw();
 
      //获取 Square 的对象，并调用它的 draw 方法
      Shape shape3 = shapeFactory.getShape("SQUARE");
 
      //调用 Square 的 draw 方法
      shape3.draw();
   }
}
```

### 二、抽象工厂模式

#### 1、个人理解：

**工厂的工厂**。针对于普通工厂的横向抽象，多个工厂继承于同一个抽象工厂。